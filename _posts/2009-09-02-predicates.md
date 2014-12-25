---
layout: post
title: "Predicates"
date: 2009-09-02
comments: false
categories: blog
---

I love predicates. They are a rather recent addition to my toolkit, but already I use them every time I can. What is a predicate you ask?

A predicate is a piece of logic to affirm or deny the subject of a proposition. Programmatically, a predicate is a function that returns true or false when given a class or value. For example.

```
public bool Contains(IProduct product)
{
    Func<IProduct, bool> predicate = x => x.Name == product.Name;

    foreach (var item in products)
    {
        if (predicate(item))
        {
            return true;
        }
    }

    return false;
}
```

Pretty cool, but let’s get rid of that foreach.

```
public bool Contains(IProduct product)
{
    Func<IProduct, bool> predicate = x => x.Name == product.Name;

    return products.FirstOrDefault(predicate) != null;
}
```

And finally…

```
public bool Contains(IProduct product)
{
    return products.FirstOrDefault(x => x.Name == product.Name) != null;
}
```

We can also filter lists in a similar fashion using _Where_

```
public IEnumerable<IProduct> FindByName(IProduct product)
{
    return products.Where(x => x.Name == product.Name);
}
```

Update: Thanks to Conrad for helping me improve this and remove the need for an Extension Method.
