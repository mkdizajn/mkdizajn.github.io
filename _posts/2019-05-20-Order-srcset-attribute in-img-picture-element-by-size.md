---
published: true
backgroundpic: /media/Untitled_.jpg
tags:
  - javascript regex
  - wordpress srcset unordered
  - sort srcset
---
## Order srcset attribute in picture elements


If your favorite CMS (WordPress in my case) is outputing `srcset` attribute in strange order (not by viewport size as I'd expected it — from smallest to biggest) then you can use this peace of javascript to find the biggest image if you need it!

```javascript
$.each( $('img'), function(){
	if( ! $(this).attr('srcset') ) return;
	var urls = $(this).attr('srcset').split(/,/);
	urls = urls.sort(function(a, b){
		return a.match( / (\d+)/, 'g' )[0].trim()-b.match( / (\d+)/, 'g' )[0].trim();
	});
	urls = urls.pop().trim().replace( / .*$/g, '') ;
	var dir = $(this).attr('src');
	if( dir.indexOf('gif') > 0 ) return;
	$(this).parent().attr('href', urls );
});
```

In the code above I'm setting the `href` attr to the biggest image from srcset that this peace of code does :)

<img src="https://i.imgur.com/mxOGfWG.gif" >

Hope someone ever find it usefull like I did today :)

cheers, k
