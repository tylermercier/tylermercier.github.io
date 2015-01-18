---
layout: post
title: "Disposable Discoveries"
date: 2009-02-08
categories: blog
---

A few days ago, there was a discussion at work about the using statement. The question was around what exactly the code snippet below gets transformed into

```
using (FileStream fileStream = new FileStream(sourceFile))
{
    // do something
}
```

It was generally agreed you would get something like this.

```
FileStream fileStream = null;
try
{
    fileStream = new FileStream(sourceFile);
    // do something
}
finally
{
    if (fileStream != null)
    {
        fileStream.Close();
        fileStream.Dispose();
    }
}
```

The focus was on whether the Close() method gets called and if it would be better to just call everything explicitly to be sure. It turns out the Close() method is called, but not by the using statement. In this case, the FileStream inherits from System.IO.Stream which will call Close() from within its Dispose() method. A number of other &quot;base&quot; classes will also do the same.
