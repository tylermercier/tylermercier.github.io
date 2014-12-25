---
layout: post
title: "ORM Tradeoffs"
date: 2012-11-06 11:14
comments: true
categories: blog
---

There has been much talk about [ORM hate](http://martinfowler.com/bliki/OrmHate.html). I have had many discussions with colleagues at [ThoughtWorks](http://www.thoughtworks.com/) about their feelings on ORMs from their personal experience. Some think they are wonderful and couldn’t imagine life without them. Others think they are abused and included in projects too often. I have a theory where this latter argument is really coming from, but I will save that for the conclusion.

Make no mistake, ORMs are a compromise. Choosing to use an ORM library will not make all your SQL problems go away and will even introduce some new ones. Given that, let’s go through some of the main ORM attributes, starting with the negative ones.

## Where ORM’s Hurt

### [Leaky Abstraction](http://www.joelonsoftware.com/articles/LeakyAbstractions.html)

Every ORM has some SQL concepts bleeding into it and you can never fully abstract away the implementation details. Configuration, mappings and relationships will require a deep understanding of how relational databases work and how to optimize them. There are no silver bullets.

```csharp
var catNames = session.QueryOver<Cat>()
  .WhereRestrictionOn(c => c.Age).IsBetween(2).And(8)
  .Select(c => c.Name)
  .OrderBy(c => c.Name).Asc
  .List<string>();
```

### Inefficient Abstraction

Depending on your needs, you may only use parts of the data stored in a table. For example, you only want a User’s name, but have to get the entire record out of the database because of your mappings, which may also include getting the User’s address from another table. This results in selecting more data than you need and includes an unnecessary join.

### Performance Problems

Leaky as the abstraction may be, developers can still remain ignorant of the underlying SQL queries. This often results in poor application performance. SQL queries could be less than optimal, but you could also have other issues. For example, I have yet to see someone using an ORM and not be bitten by an [N+1 problem](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).

### Learn another tool

You should expect to spend time reading up on, experimenting with and debugging issues in the ORM of your choosing. This also provides a barrier to entry if a team member is not familiar with your particular ORM. This is true of any major library you would choose to use, but can easily be forgotten when including NHibernate for the 12th time on that new web project.

### Batching and Reporting

Because these generally don’t fit into any domain model, your ORM will not be able to handle these concerns very well. Your ORM of choice will need to support writing SQL by hand for these queries. The more focus in this area you application has, the more your ORM will get in the way. Each ORM will have varying levels of support here.

## Where ORM’s Help

### Impedance Mismatch

This is primarily what ORMs were created for, so it shouldn’t be surprising they excell here. Impedance mismatches include figuring out the data types for fields, but can also cover handling relationships. For example, getting both the User and Address because the User mapping defines a *has a* relationship between the User and Address tables.

### Developer Efficiency

An ORM easily generates most of your SQL queries from your data models and mappings. Some SQL queries will bleed the underlying query details into your application, but generally in a way that can be kept [DRY](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself) and still ignore impedance mismatch details. For example, the code below has some knowledge of SQL, but manages to handle all CRUD operations in a highly reusable fashion.

```csharp
public class Repository : IRepository {
    public ISession Session { get; private set; }

    public Repository(ISession session) {
        Session = session;
    }

    // Find by ID
    // Eg: var user = repo.Find<User>(1);
    public T Find<T>(int id) where T : DataModel {
        return Session.Get<T>(id);
    }

    // Find by predicate
    // Eg: var user = repo.Find<User>(x => x.name == "Tom");
    public T Find<T>(Expression<Func<T, bool>> criteria) where T : DataModel {
        return Session
            .Query<T>()
            .Where(criteria)
            .SingleOrDefault();
    }

    // Create or update
    // Eg: repo.Save(user);
    public T Save<T>(T item) where T : DataModel {
        using (var trans = Session.BeginTransaction()) {
            Session.SaveOrUpdate(item);
            trans.Commit();
        }

        return item;
    }

    // Delete
    // Eg: repo.Delete(user);
    public void Delete<T>(T entity) where T : DataModel {
        using (var trans = Session.BeginTransaction()) {
            Session.Delete(entity);
            trans.Commit();
        }
    }
}
```

### Separation of Concerns

An ORM provides an excellent barrier between your application and your database. This makes adding cross cutting concerns, such as security and logging, much easier. For example, it is generally a trivial task to log all of your SQL queries with an ORM.

### Caching is Much Easier

Related to the previous point, but there are two other things helping out here. First, many ORMs have great caching support. Most natively cache objects by their IDs and some will support third party caching through configuration. Second, the Inefficient Abstractions your domain models represent are often ideal caching candidates. The fewer ways you can get the same information, the fewer concerns your caching layer needs to get in front of.

## Alternatives

When discussing the viability of using an ORM, Ad Hoc Queries and Stored Procedures often come up. DBAs usually favor stored procedures and procedural programmers usually favor Ad Hoq queries or some combination of the two.

### Ad Hoc SQL Queries

SQL cannot be easily decomposed. There is basically no good way to share and reuse SQL inside your application. The effect of this is that your data access layer will become very procedural and it will end up consuming a disproportionate amount of your time solving the same problems repeatedly. You will also have the same leaky abstraction problems as an ORM, without a layer to protect you.

### Stored Procedures

The same deficiencies as Ad Hoc SQL apply, but we have some additional problems. First, stored procedures are incredibly difficult to test in an automated fashion. Second, stored procedures tend to grow with time because they provide few techniques for restructuring and refactoring. The end result is something that is difficult to comprehend and impossible to test. This is why many developers will tell you that business logic in your database is almost never a good idea.

## Conclusion

If you want to write object oriented code and persist those models into a relational database, you are going to be dealing with an ORM in some form. That doesn’t mean you have to use an ORM library, but beware of the [cost involved](http://www.ohloh.net/p/nhibernate/estimated_cost) in creating one before you get started on a “simpler” and likely less maintainable version.

At this point, it probably sounds like your options are to use an ORM or to store your data in a flat file. Before you go read up on file access, there is another option and this ties into what most of these discussions about the negative points of ORMs are really alluding to, the use of NoSQL. To avoid ORMs, while writing object oriented code, you could choose to go with a non-relational alternative (NoSQL). If you choose to go down this road, you should pick the alternative that best fits your domain model. For example, a blog or a CMS fits a document store like [MongoDB](http://www.mongodb.org/) really well, but not a graph database like [Neo4j](http://neo4j.org/). Adding to that from personal experience, some of these alternatives can be a pleasure to work with. Most are many times easier to setup, develop on and to scale than a traditional relational database will be. For example, setting up a high availability [MongoDB](http://www.mongodb.org/) instance to test how it reacts to failure can be done on one machine in a couple of hours, most of that time spent reading. Have you ever done that with a traditional RDBS?

When choosing a NoSQL option, remember that you are giving up decades of research, tooling and support. You are also giving up an incredible powerful and prevalent querying language. Sometimes the tradeoffs (ease of developer use, scalability, cost, etc..) are worth it, but that is something you should carefully weigh, including things like the use of an ORM.
