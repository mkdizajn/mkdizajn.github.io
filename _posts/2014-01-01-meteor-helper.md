---
layout: post
title: Meteor event hangling helper
published: true
---

<div class="message">
  Ohh that meteorjs.. here is something that I like very much with this kind of approach to handling events 
</div>

> This is very clean way how to hangle event calls on various input elements. Meteor use this on their todo demo. Here:


{% highlight js %}
////////// Helpers for in-place editing //////////

// Returns an event map that handles the "escape" and "return" keys and
// "blur" events on a text input (given by selector) and interprets them
// as "ok" or "cancel".
var okCancelEvents = function (selector, callbacks) {
  var ok = callbacks.ok || function () {};
  var cancel = callbacks.cancel || function () {};

  var events = {};
  events['keyup '+selector+', keydown '+selector+', focusout '+selector] =
    function (evt) {
      if (evt.type === "keydown" && evt.which === 27) {
        // escape = cancel
        cancel.call(this, evt);

      } else if (evt.type === "keyup" && evt.which === 13 ||
                 evt.type === "focusout") {
        // blur/return/enter = ok/submit if non-empty
        var value = String(evt.target.value || "");
        if (value)
          ok.call(this, value, evt);
        else
          cancel.call(this, evt);
      }
    };

  return events;
};
{% endhighlight %}

And to see it in action you can use it like:

{% highlight js %}
// Attach events to keydown, keyup, and blur on "New list" input box.
Template.lists.events(okCancelEvents(
  '#new-list',
  {
    ok: function (text, evt) {
      var id = Lists.insert({name: text});
      Router.setList(id);
      evt.target.value = "";
    }
  }));
{% endhighlight %}

-----
Have questions or suggestions? Feel free to [open an issue on GitHub](https://github.com/mkdizajn/mkdizajn.github.io/issues/new) or [ask me on Twitter](https://twitter.com/mkdizajn).