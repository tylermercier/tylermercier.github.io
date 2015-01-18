---
layout: post
title: "Google Translation Service"
date: 2009-03-30
categories: blog
---

I was tasked with some localization jobs. Generally our portals use resource files for all text, so localizing them mostly involves translating that content. The resource files are generally of the following form.

```
<?xml version="1.0" encoding="utf-8"?>
<root>
  <data name="some_title" xml:space="preserve">
    <value>some value</value>
    <comment>a comment</comment>
  </data>
</root>
```

Now most of the translations were done by hand, plugging them into google translator like a good little monkey. I, however, am not a good little monkey. Why do by hand what can be automated right?

After some quick searching, I found a few sample applications that did what I was trying to do. Unfortunately, they were dated and didn't play well with the latest version. The google translator API is open and supported for development like I had in mind (sort of), but does not play well with screen scrappers because of it's ajax data retrieval. That asynchronous data retrieve is pretty much what you latch onto for the API. Submit a request to a url, get some JSON back.

Sample INPUT

[http://ajax.googleapis.com/ajax/services/language/translate?v=1.0&amp;q=hello%20world&amp;langpair=en%7ciw&amp;key=YOUR_API_KEY](http://ajax.googleapis.com/ajax/services/language/translate?v=1.0&amp;q=hello%20world&amp;langpair=en%7ciw&amp;key=YOUR_API_KEY)

Sample RESPONSE

`{"responseData": {"translatedText":"세계 안부"}, "responseDetails": null, "responseStatus": 200}`

Really strait forward to implement this type of request automatically. The previous apps even gave me all the language pairs I needed, so no work there either.

The only real work was, and I am ashamed to admit this, the serialization of the JSON response. Obviously this is easily done in javascript, but I needed the response in code.

Fortunately, this was also easier than I would have thought. Though a reference to a .NET AJAX library is required (System.Web.Script.Serialization from System.Web.Extensions)

```
// Container for data
public class GoogleTranslation
{
    public ResponseData responseData { get; set; }
    public string responseDetails { get; set; }
    public string responseStatus { get; set; }
}

// Response
public class ResponseData
{
    public string translatedText { get; set; }
}

// Serialization method
public string GetLocalizedResult(string jsonResponse)
{
    JavaScriptSerializer ser = new JavaScriptSerializer();
    GoogleTranslation trans = ser.Deserialize<GoogleTranslation>(jsonResponse);

    return trans.responseData.translatedText;
}
```
