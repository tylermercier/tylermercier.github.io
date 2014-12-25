---
layout: post
title: "PURE HTML Templates"
date: 2010-05-26
comments: false
categories: blog
---

I’ve been pressured into writing about [PURE templates](http://beebole.com/pure/) by a couple of my colleagues at [ThoughtWorks](http://www.thoughtworks.com/). My blogging has died down after rolling off my previous iPhone project, but while doing some work in ASP.NET MVC I came across something useful. A very nice HTML templating engine.

My biggest complaint when looking at HTML templating engines is that they are very similar to PHP or ASP code, littering my HTML with different forms of placeholders. They are very simple and quick to pick up, but very limited once you need to do something more than map A onto B without creating a lot of one off functions that will fit in one line.

```
<script type="text/html" id="item_tmpl">
  <div id="<%=id%>" class="<%=(i % 2 == 1 ? " even" : "")%>">
    <div class="grid_1 alpha right">
      <img class="righted" src="<%=profile_image_url%>"/>
    </div>
    <div class="grid_6 omega contents">
      <p><b><a href="/<%=from_user%>"><%=from_user%></a>:</b> <%=text%></p>
    </div>
  </div>
</script>
```

Have a look at this fully functional [example](http://beebole.com/pure_git/tutorial/tuto1.html) (view source) using PURE. There is some HTML and a small script block. In the block is a javascript object literal representing the data and a single call to PURE giving the root of the HTML template and the data to render. Clean HTML, very little code and no dirty template placeholders. This shows that, in the happy day scenario, PURE is very simple and easy to use, like most other templating engines.

However, as the web becomes more and more about creating and interacting with services. Consuming third party sources becomes necessity and those sources will not be providing data in the human readable format your require, nor will their names be exactly what you need.

For these situations, we need something more powerful than all these happy day templates can provide (assuming you don’t just want to remap everything you consume). In PURE, they accommodate this by way of a [Directive](http://beebole.com/pure/documentation/what-is-a-directive/). At a basic level, a directive is a javascript object literal defining how to map your data onto your HTML. The keys are [CSS Selectors](http://www.w3.org/TR/css3-selectors/#selectors) and the values are Actions, where Actions can be strings, objects or functions.

```
<!-- HTML template -->
  <ul>
    <li></li>
  </ul>

  <script>
    var data = {
      legs:4,
      animals:[
        {name:'dog', legs:4},
        {name:'cat', legs:4},
        {name:'bird', legs:2},
        {name:'mouse', legs:4}
      ]
    };

    //declaration of the actions PURE has to do
    var directive = {
      'li':{
        'animal<-animals':{
          '.':'animal.name'
        },
        sort:function(a, b){
          return a.name > b.name ? 1 : -1;
        },
        filter:function(a){
          return a.context.legs === a.item.legs;
        }
      }
    };

    // note the use of render instead of autoRender, and the 2nd argument
    $('ul').render(data, directive);
</script>
```
[source](http://beebole.com/pure/documentation/iteration-with-directives/)

The above example&#160; shows what a directive looks like while consuming data that must be iterated over. It also shows how the directive can accommodate sorting and filtering, which can come in handy at times. If you like what you see, check out the rest of the [demos](http://beebole.com/pure/demos/) or the [tutorials](http://beebole.com/pure/documentation/tutorials/).
