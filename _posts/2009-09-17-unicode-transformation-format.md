---
layout: post
title: "Unicode Transformation Format"
date: 2009-09-17
categories: blog
---

Had another one of those days yesterday where you get deep in discussion about some of the nitty gritty. This time it was surrounding Unicode and though I knew some pieces of the picture, I could have certainly done with more information.

First and foremost, Unicode is a way of encoding characters as a sequence of bytes. In this case, characters (and even more so strings) are an abstraction. UTF-8/16/32 define different encoding schemes that we can use for those _bytes_. Each of those bytes are being represented by one [hexidecimal](http://en.wikipedia.org/wiki/Hexadecimal) value.

![Some sample character encodings](http://i2.sitepoint.com/g/nl/tt/character-encodings-fixed.gif)

[source](http://www.sitepoint.com/blogs/2006/03/15/do-you-know-your-character-encodings/)

Looking at the UTF-8/16/32 section of the diagram, we see the different byte representations of the three characters. Also notice that UTF-8 byte representation of 'A' is identical to ASCII. This is true for a large set of the Latin alphabet and ties into why UTF-8, in Latin languages, is usually the most compact Unicode encoding choice. For this reason, storage and data exchange systems prefer it.

C# for example uses UTF-16 encoding for _strings_, but will default to UTF-8 for streams. UTF-8 isn’t all good though and it should be noted that UTF-8 is significantly more complex to process than UTF-16 because lead bytes have a relatively complex encoding and up to three trail bytes must be counted. This is due to the fact that Unicode is optimized for 16 bits.

If this interests you, the below documents provide even more insightful information.

[Unicode Technical Notes](http://unicode.org/notes/tn12/#UTF8)

[Unicode is not UTF-\d{1,2}](http://enjoydoingitwrong.wordpress.com/2009/06/22/unicode-is-not-utf/)

[Python Document on Unicode](http://diveintopython3.org/strings.html)
