---
layout: single
title:  "Difference between URL, URI and URN"
date:   2015-08-25 15:00:00 -0800
categories: URL URI URN
permalink: /difference-between-url-uri-and-urn
classes: wide
---
This is a classic tech debate, and many people will sooner or later ask themselves what's the difference between URLs, URIs and most possibly even URNs. As of today one can simply refer to URNs and URLs as URIs, but it may be very interesting and useful to know the difference between these three terms since technically a URI can still be further classified as URL, URN or both. If you happen to find these terms somewhere, you should at least know what they mean.

If regular people don't know the technical difference between these three acronyms and what they represent it shouldn't be an issue for them, in my opinion. But if you're a Software Engineer or, more generally, if you work in the IT field then it might be well worth to have this knowledge in your bag.

This post is intended to be a clear explanation of the difference between URLs, URIs and URNs and will help you to quickly understand what you need to know. Are you confused about this topic? Let's begin!

## Origins

These three acronyms are specified by Tim Berners-Lee as an Internet standards track protocol in the document called [RFC 3986: Uniform Resource Identifier (URI): Generic Syntax](https://tools.ietf.org/html/rfc3986).

Citing the document:
> A Uniform Resource Identifier (URI) provides a simple and extensible means for identifying a resource. This specification of URI syntax and semantics is derived from concepts introduced by the World Wide Web global information initiative, whose use of these identifiers dates from 1990 and is described in "Universal Resource Identifiers in WWW".

This means that the Uniform Resource Identifier was conceptualized back in the 1990s with the purpose of distinguishing between **who** and **where**.

Let's get more technical on this.

<figure>
  <img src="{{site.url}}/assets/images/2015-08-25/tim.jpg" alt="Tim Berners-Lee"/>
  <figcaption>Tim Berners-Lee, the man who invented the World Wide Web and actual director of the W3C. Photo by Paul Clarke - Licensed under CC BY-SA 4.0.</figcaption>
</figure>

## The Difference

Let's start by making one thing clear. **URL and URN are both subsets of URI.**

In other words, URL and URN are always a URI, but a URI is not always a URL or a URN. To better understand this concept look at the image below.

<figure>
  <img src="{{site.url}}/assets/images/2015-08-25/uriurlurn.png" alt="URI, URN and URL as sets"/>
</figure>

A great example to understand the difference between URN and URL is the following (taken from [Wikipedia](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier)): in the case of a person, we can take in consideration his name and his address. 
The URL is similar to the latter one, the address; it tells you a **method** to find that object (the person by its street address, in this example). Keep in mind that, by the definition we gave above, this also a URI.

Instead, we can see the name of a person as a URN; the **URN is therefore used to unequivocally identify a generic object**. To be more precise, in the case of a person's name this is not entirely true since there may be another person with the same name (and surname), so a more appropriate example may be the ISBN code of a book or a product's serial number inside of a system; while this doesn't tell you how or where to find that object, you indeed have enough information to retrieve it by yourself. Formally, URNs also have their syntax. From [this document](https://tools.ietf.org:80/html/rfc2141):

> All URNs have the following syntax (phrases enclosed in quotes are REQUIRED):
```
< URN > ::= "urn:" < NID > ":" < NSS >
```
where NID is the Namespace Identifier, and NSS is the Namespace Specific String.

## One example to understand them all

Let's start by looking at how the concepts above apply to what matters to us: the Internet. 
The following quotes from [Wikipedia](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier) give us a bit more technical explanation in comparison to the generic person-address example we used above.

For URL:
> A URL is a URI that, in addition to identifying a web resource, specifies the means of acting upon or obtaining the representation, specifying both its primary access mechanism and network location.

For URN: 

> A URN is a URI that identifies a resource by name in a particular namespace. A URN can be used to talk about a resource without implying its location or how to access it.

Now, if you look around the web you will find a lot of examples and these can sometimes create more confusion than anything else. I will present you only **one** example, which is very simple and clearly shows the difference between URI, URL and URN in contest of the Internet.

Let's consider the following fictitious example. This will be our **_URI_**:
```
https://garry.bhatt.al/posts/hello.html#intro
```

Let's start by saying that
```
https://
```
is the **method** that defines how to access that resource. Instead,
```
garry.bhatt.al/posts/hello.html
```
is the **location** where the resource resides, while, in this example,
```
#intro
```
is the resource.

So we can say that the **URL**, a subset of the URI that tells us how to access a network location, is the following part of our complete example:
```
https://garry.bhatt.al/posts/hello.html
```

The URN, defined as the URI subset that includes a name (within a given space) but does not provide a method to access it, is:
```
garry.bhatt.al/posts/hello.html#intro
```

That's it! Now you should be able to tell the difference between URL and URN.

___

Should you ever forget the content of this article, you have to options. One is to get back here and read again about the differences. But URIs can be classified as URLs, URNs or both, right? So the other option is to always use the term **URI**. This way, you will never be wrong.

Should you find any mistakes, technical or grammatical, please don't hesitate to let me know!