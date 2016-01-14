---
published: true
layout: post
excerpt: New cool developement wordpress customizer toolkit
backgroundpic: ""
tags: 
  - php
  - wordpress
title: New and cool Wordpress customizer toolkit named Kirki
---




## This weekend I played a little

This new and cool toolkit Kirki: https://github.com/aristath/kirki is a thing from the future :) I like it so much and start to develop with it was like 1,2,3..
All documentation is not available yet but as my impression is guys are doing on it over at GH pages / wikis and are doing a great job..

I simply inserted the reference to kirki.php file and added my own fields definition file like this

{% highlight php %}
<?php
// include kirki toolkit
include_once( dirname( __FILE__ ) . '/kirki/kirki.php' );
// add themes customizer options
include_once( dirname( __FILE__ ) . '/kirki-customizer-options.php' );
{% endhighlight %}


inside `functions.php` file and my customizer looked like this in a moment!

![2016_logo-2015-12-13_11.41.05.gif]({{site.baseurl}}media/2016_logo-2015-12-13_11.41.05.gif)


the repo is here if that interest someone..

cheers, k
