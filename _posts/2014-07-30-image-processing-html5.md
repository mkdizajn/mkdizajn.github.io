---
published: true
layout: post
excerpt: HTML5 getImageData object to alter images in browser
backgroundpic: ""
tags: 
  - javascript
  - html5
title: Image processing html5
---

<div class="message">
HTML5 getImageData object to alter images in browser,, so many possibilities..
</div>

**Simple** examples of using image filters ..

{% highlight js %}
/**
 * Image filters
 * @type {Object}
 */


Filters = {};
Filters.getPixels = function(img) {
	var c = this.getCanvas(img.width, img.height);
	var ctx = c.getContext('2d');
	ctx.drawImage(img);
	return ctx.getImageData(0, 0, c.width, c.height);
};

Filters.getCanvas = function(w, h) {
	var c = document.createElement('canvas');
	c.width = w;
	c.height = h;
	return c;
};

Filters.filterImage = function(filter, image, var_args) {
	var args = [this.getPixels(image)];
	for (var i = 2; i < arguments.length; i++) {
		args.push(arguments[i]);
	}
	return filter.apply(null, args);
};


Filters.grayscale = function(pixels, args) {
	var d = pixels.data;
	for (var i = 0; i < d.length; i += 4) {
		var r = d[i];
		var g = d[i + 1];
		var b = d[i + 2];
		// CIE luminance for the RGB
		// The human eye is bad at seeing red and blue, so we de-emphasize them.
		var v = 0.2126 * r + 0.7152 * g + 0.0722 * b;
		d[i] = d[i + 1] = d[i + 2] = v
	}
	return pixels;
};
{% endhighlight %}

-----
cheers, k
