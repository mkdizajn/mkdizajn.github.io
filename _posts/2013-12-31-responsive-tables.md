---
layout: post
title: Responsive tables css
published: true
tags:
  - css
  - responsive tables
  - css responsive tables
---

<div class=message>
   If you have some data laying around in html table, you can have it responsive via css
</div>

Try this classes and play with it little to get best results..

{% highlight css %}
  @media only screen and (max-width: 760px),
  (min-device-width: 768px) and (max-device-width: 1024px)  {
  
    /* Force table to not be like tables anymore */
    table, thead, tbody, th, td, tr { 
      display: block; 
    }
    
    /* Hide table headers (but not display: none;, for accessibility) */
    thead tr { 
      position: absolute;
      top: -9999px;
      left: -9999px;
    }
    
    tr { border: 1px solid #ccc; }
    
    td { 
      /* Behave  like a "row" */
      border: none;
      border-bottom: 1px solid #eee; 
      position: relative;
      padding-left: 50%; 
    }
    
    td:before { 
      /* Now like a table header */
      position: absolute;
      /* Top/left values mimic padding */
      top: 6px;
      left: 6px;
      width: 45%; 
      padding-right: 10px; 
      /*white-space: nowrap;*/
    }
  }
    
{% endhighlight %}

-------------
cheers, k
