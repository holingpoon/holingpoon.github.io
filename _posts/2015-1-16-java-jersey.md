---
layout: post
title: Java and Jersey
---

In Java API for RESTful Web Services using Jersey, you can have the minimal url-pattern in the web.xml configuration file:

 ~~`<url-pattern>/*</url-pattern>`~~

But can't skip annotations in the head of the class. That identifies where the url path starts.

```
@Path("/")
public class HelloWorldService
```
```
@ApplicationPath("/")
public class HelloApp extends Application
```
*(Edit: Turns out you can skip the url-pattern in web.xml. You only need to specify the @Path and @ApplicationPath in the classes for Jersey 2.18).*
