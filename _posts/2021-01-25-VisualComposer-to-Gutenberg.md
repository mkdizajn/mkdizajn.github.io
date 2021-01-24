---
published: true
---
## Covert site with Visual Composer tags to Gutenberg tags

That moment, when you realise, that Visual Composer and such +premium+ like builders are to expensive for your backend, you go back to vanila WordPress +that now is backed with super awesome visual builder Gutenberg that is included natively, but there is a catch. When you disable Visual Composer you end up with nesty generated tags like this one:

```
[vc_row][vc_column][vcex_image_flexslider animation="fade_slides" loop="true" control_nav="false" control_thumbs="false" image_ids="2805,2796,2797,2798,2806,2800,2801,2802"][/vc_column][/vc_row][vc_row][vc_column][vc_column_text]<strong>SPAR Rujevica, Rijeka, HR — photography ⓒ Bosnić+Dorotić — clients / architecture:&nbsp;Idis Turato / Turato Architects</strong>[/vc_column_text][/vc_column][/vc_row]
```

and you realise that you are stuck .. this should be rendered on page like slideshow or slider that should swipe images on page, but it's not, it+s only shortcode 

To go around that issue, we need to compare output of generated Gutenberg gallery (or slider) and create it from VC generated shortcodes. We can see that VC uses only attachement ID's of images and that is only thing that is needed. So, there is need to very carefully compare it, make a loop, use regex to be faster and result will be brilliant Gutenberg page (even backend of WordPress see and renders blocks without any issue)

Short gif can be of help here, so give your eyes little info - if anyone stuck with other blocks of VC to Gutenberg convertion let me know in comments we could start some community backed project

![ezgif.com-gif-maker (24).gif](https://i.imgur.com/HaRdl9F.gif)
