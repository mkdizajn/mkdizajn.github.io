---
layout: post
title: Select2 ajax hook to trigger cascade on phpgrid form
published: true
tags: 
  - first
  - second
  - mirko
---

## Select2 hook on phpGrid

{% gist 11364571 %}

phpGrid has builtin form that have basic lookup feature, and in this gist I'm showing couple of methods that I do on aftershowform event.

* Hiding / Showing controls that have dependance of other controls
* Redirecting result value from one select2 to another
* Getting / setting multiselect for column
* Getting / setting form column count

cheers, k