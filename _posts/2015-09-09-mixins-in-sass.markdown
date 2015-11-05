---
layout: post
title:  "Mixins in SASS"
---
Sass is a great technology that allows us to handle our style files by adding features like variables, nesting, mixins, inheritance…… Basically is like “programming” your css.

The purpose of this post is not to explain how to use and install Sass; If you don’t have any previous experience with Sass, you may want to have a look at the <a href="http://sass-lang.com/">official webpage</a>.<!--more-->

To help me with the preprocessing, I have used a brilliant tool called <a href="http://mhs.github.io/scout-app/">Scout</a>, very simple to use, to install and to configure.

Mixins is basically a way to refactor and to re-use parts of the code that we will called from different places; it has basically the look of a function. We can even pass arguments.

Let’s imagine we have declared a couple of buttons and we have used some Sass to define their look.

{% highlight css %}
//Style for the main button
.main-button {
background-color: $main-button-color;
width:            $width-all-buttons;
padding:          $padding-all-buttons;
}

//Style for the regular button
.regular-button {
background-color: $regular-button-color;
width:            $width-all-buttons;
padding:          $padding-all-buttons;
}
{% endhighlight %}

I won’t add all the code here, you can download it on my Github account using the link at the bottom of the post.

Here we have just defined  the width, padding and background color of our two buttons. Note that both width and padding are exactly the same in this example, the buttons only differentiate in the background color.

So, let’s use mixins to declare our ‘function’ and also pass it an argument to pass for the background color (which is the only element that is different in each case).

To create a mixin, we just need to add the special element @mixin, name the mixin and add (optionally) some arguments. Inside of the mixin we will define what this ‘function’ will do:

{% highlight css %}
@mixin all-buttons($button-background-color) {
background-color: $button-background-color;
width:            $width-all-buttons;
padding:          $padding-all-buttons;
}
{% endhighlight %}

That’s it, we only need to call this mixin from each button with the @include element, and also pass the parameter to define the color of each background:

{% highlight css %}
.main-button {
@include all-buttons($main-button-color);
}

.regular-button {
@include all-buttons($regular-button-color);
}
{% endhighlight %}

As we can see, the refactor leaves our scss file cleaner and easier to use and understand. Also, in the final css file we can check that both before and after treatment gives exactly the same result.

{% highlight css %}
.main-button {
 background-color: #81c3e5;
 width: 250px;
 padding: 5px 5px 5px 5px;
}

.regular-button {
 background-color: #47c333;
 width: 250px;
 padding: 5px 5px 5px 5px;
}
{% endhighlight %}

Feel free to fork the sample and play with it to understand how it works and also to try many other capabilities that are not included in this post.

<img  src="http://assets-cdn.github.com/images/modules/logos_page/GitHub-Mark.png" alt="github_24px" width="24" height="24" /><a href="https://github.com/sergiolealdev/SampleMixinsSass" target="_blank">Watch / Download example on Github</a>

<a href="http://icons.iconarchive.com/icons/dakirby309/windows-8-metro/256/Web-YouTube-Metro-icon.png" alt="youtube-icon-24px" width="24" height="24" /></a> <a href="https://www.youtube.com/watch?v=Roe93U8X9LE" target="_blank">Watch how to setup Scout</a>