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

Short gif can be of help here, so I hope this will help you anyone who is stuck like me. If other blocks of VC to Gutenberg convertion is of interest to anyone let me know in comments and we could start some community backed project - what do you think?


![ezgif.com-gif-maker (24).gif](https://i.imgur.com/HaRdl9F.gif)


```php
// attach that to everywhere
add_action( 'template_redirect', function (){

	$w = new WP_Query( array( 
		'post__in' => array( 823, 817 ),
		'post_type' => 'any' ,
		// 'posts_per_page' => 100, 
		// 'offset' => 400 
	));

	while ( $w->have_posts() ) {
		$w->the_post(); $post_id = get_the_ID();
		$con = get_post_field('post_content', $post_id) ;
		preg_match('/[vcex_image_flexslider].*?image_ids="(.*)"]/msi', $con, $match );
		$gallery = $match[1] ; // image slider reg
		preg_match('/\[vc_column_text](.*)\[\/vc_column_text]/msi', $con, $mat );
		$info = $mat[1] ; // text regex

		if( $gallery ){
			$h = '<!-- wp:gallery {"ids":[' . $gallery . '],"columns":1,"sizeSlug":"full","className":"slider"} --><figure class="wp-block-gallery columns-1 is-cropped slider"><ul class="blocks-gallery-grid">' ;
			$arr = explode(',', $gallery );
			foreach ($arr as $vall ) {
				$h .= '<li class="blocks-gallery-item"><figure><img src="' . wp_get_attachment_url( $vall ) . '" alt="" /></figure></li>' ;
			}
			$h .= '</ul></figure><!-- /wp:gallery -->' ;
		}
		if( $info ){
			$h .= '<p>' . $info . '</p>' ;
		}
		// REPLACE VisualComposer with Gutenberg
		$post = array(
			'ID'		=> $post_id,
			'post_content' => $h
		);
		wp_update_post( $post );
	}	

```
