---
published: true
---
## WP SmashIt auto click script

If you have big archive like me, and don't like the fact to click like 63 time on continue button on plugin page, just to compress your initial archive, use this `oneliner` script.

<img src="https://i.imgur.com/LH1Yqp5.png" />

{% highlight js %}
setInterval(function(){ if( $('.wp-smush-all.wp-smush-button.wp-smush-started').not('[disabled]').length ) $('.wp-smush-all.wp-smush-button.wp-smush-started').click() }, 15000)

{% endhighlight %}

as usuall run it in `console` on plugin admin page like I did and do not close tab when you run it :)
