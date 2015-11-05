---
layout: post
title:  "Static Resources Handling in Spring 4.1"
date:   2015-04-25 10:25:41 +0100
---

Not long time ago I faced the need of handling static resources with Spring, and I came up with this <a href="http://www.infoq.com/presentations/resource-spring-mvc-4-1">presentation</a> from Spring Framework committers <a href="https://twitter.com/brianclozel">Brian Clozel</a> and <a href="https://twitter.com/rstoya05">Rossen Stoyanchev</a>.

In the video Brian and Rossen explain how they have developed a new way of handling this type of files and propose from version 4.1 of Spring a very easy and simple way of implement this idea.

In the presentation they explain how they used this in a project called <a href="https://github.com/spring-io/sagan">Sagan</a>, which it turns out to be the new Spring’s home page.<!--more-->

Also in this presentation they try to explain how to use this new feature by referring to a much more <a href="https://github.com/bclozel/spring-resource-handling">simple project</a>, based in two parts, a client part, where they handle all the js,css and other static resources, and a server side, where they implement Spring’s part.

I wanted to go one more step in terms of simplifying this demonstration and I’ve created a little <a href="https://github.com/sergiolealdev/SpringStaticResourceHandling">boilerplate project</a> with Spring MVC, Spring Boot and a jsp that uses bootstrap and jquery, and in the Spring’s side I use this new implementation to handle my static resources.

There are basically two main parts that we have to take into account in the project.

1. In the jsp presentation, I handle my resources by using a jstl core tag, for Spring to notice and be aware of them.

{% highlight html %}

<head>
   <link href="<c:url value="resources/css/bootstrap.min.css"/>" rel="stylesheet">
   <script type="text/javascript" src="<c:url value="resources/js/jquery-2.1.3.min.js"/>"></script>
</head>

{% endhighlight %}

2. In the server side, when we configure our files, we extend the <a href="http://docs.spring.io/autorepo/docs/spring/3.2.3.RELEASE/javadoc-api/org/springframework/web/servlet/config/annotation/WebMvcConfigurerAdapter.html">WebMvcConfigurerAdapter</a> and we override the addResourceHandlers method to basically tell Spring where to find our resources, how much time we want the resources to be cached in the client and which type of resolvers and transformers we may want to use.

{% highlight java %}

@Override
public void addResourceHandlers(ResourceHandlerRegistry registry) {
   registry.addResourceHandler("/resources/**")
           .addResourceLocations("/resources/")
           .setCachePeriod(10)
           .resourceChain(true)
           .addResolver(new VersionResourceResolver());
}

{% endhighlight %}

As of version 4.1.6 of Spring, several things have changed and I have noticed that even classes that I have used in version 4.1.1 don’t exist anymore in the current version, so I have the feeling maybe more things will change in the future about this, but there are many great features in this new part of Spring, having even the possibility of versioning our resources (maybe in another post) and control when and how we want our clients to refresh their versions of our resources.

Again, I encourage you to watch Brian &amp; Rossen’s presentation, where they explain this concept much better than I do.

<img  src="http://assets-cdn.github.com/images/modules/logos_page/GitHub-Mark.png" alt="github_24px" width="24" height="24" /></a> <a href="https://github.com/sergiolealdev/SpringStaticResourceHandling" target="_blank">Watch / Download this demo in Github</a>