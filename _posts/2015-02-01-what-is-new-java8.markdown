---
layout: post
title:  "What do we have in Java 8 (Part 1)"
date:   2015-02-01 10:25:41 +0100
categories: java java8
---
<p dir="ltr"><strong>Stream API</strong></p>
<p dir="ltr">A Stream in the new Java 8 is a typed interface, where we can use a Stream of T elements, being T an integer, a String, an Employer object, etc.</p>
<p dir="ltr">With Stream we can handle data the same way we would work in a <a href="http://en.wikipedia.org/wiki/Big_data">Big Data</a> environment, applying map-filter-reduce operations, for example.<!--more--></p>
<p dir="ltr">But aware you must! a Stream may look like a <a href="http://docs.oracle.com/javase/7/docs/api/java/util/Collection.html">Collection</a> at first sight, but it is NOT a collection. I repeat. It is <b>not </b>a collection. Collections and Streams work in a total different way. In fact, a Stream object does not store any info, unlike a Collection.</p>

{% highlight java %}

List<String> employees = Arrays
                .asList( "John \"Hannibal\" Smith ", 
                         "Templeton Peck", 
                         " H.M. \"Howling Mad\" Murdock", 
                         "\"Bad Attitude\", Baracus " ); 

//We want all items that start with T 
employees 
   .stream() 
   .filter(s -> s.startsWith("T")) 
   .forEach(e -> System.out.println(e)); 

//But at the end, the employees list remains intact 
System.out.println(employees.size());

{% endhighlight %}

&nbsp;
If we execute this code, we would get the following console output.

{% highlight java %}

Templeton Peck

4

{% endhighlight %}

<p dir="ltr">One of the most interesting features of this Stream interface is the fact that it will work in parallel, meaning, will use all processors we may have in our machine, avoiding the programmer to handle this work for him, in a total transparent way.</p>
<p dir="ltr"><b>Filtering</b></p>
<p dir="ltr">What we have done in the last piece of code was a nice filter. Filtering data with Streams is fairly simple. In the following example, we want to get all the employees that contains the word 'Attitude'</p>

{% highlight java %}

Stream streamEmployees = listEmployees.stream();

Stream  employeesFiltered = streamEmployees.filter(s -> s.contains("Attitude"));

employeesFiltered.forEach(s -> System.out.println(s));

{% endhighlight %}

<p dir="ltr">In this case we would get what we were searching for:</p>

{% highlight java %}

"Bad Attitude", Baracus

{% endhighlight %}

<p dir="ltr">There is something <b>very important to remember</b> when we work with Streams. Once we have used a Stream, it cannot be reused, or we will have a nice exception in our console. Hence, if we try to apply the forEach method again:</p>

{% highlight java %}

employeesFiltered.forEach(s -> System.out.println(s));

{% endhighlight %}

<p dir="ltr">We will get this message in our console:</p>

{% highlight java %}

Exception in thread "main" java.lang.IllegalStateException: stream has already been operated upon or closed

at java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:229)

at java.util.stream.ReferencePipeline.forEach(ReferencePipeline.java:418)

at com.sergiolealdev.java8.streams.Main.main(Main.java:33)

{% endhighlight %}

<p dir="ltr">This is it for the first part of the new features in Java8. New posts arriving soon!!</p>
<p dir="ltr"><img  src="http://assets-cdn.github.com/images/modules/logos_page/GitHub-Mark.png" alt="github_24px" width="24" height="24" /></a> <a href="https://github.com/sergiolealdev/SampleStreamAPIJava8" target="_blank">Watch/Download this code in Github</a></p>