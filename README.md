# RT Slider

RT Slider plugin helps theme developers by Creating a Slider Section in WordPress Customizer. That's all it does.
The Developer Can use it with any Slider he wants like Nivo Slider, BX-Slider, etc. 

The CSS, JS, etc are still in the hands of theme Developer and to be added via theme. 

This plugin only creates Data for the slider, so that users do not loose their slider everytime they switch from one theme to another.

This Plugin is Available on WordPress.org [here](https://wordpress.org/plugins/rt-slider). So, you can recommened it to your theme users via __TGM__.

#### Benefits of integrating RT Slider in your Theme

* No need to Write any Code to Creat Slider Sections, Options, etc in Customizer
* Fully Sanitized Code
* No loss of Slider Data while switching between themes that support RT Slider.
* Very Easy to Use and Set up.
* Works with Any Slider you want to use in your theme.
* CSS is fully in your hands. Plugin doesn't render any styles at all.


#### How to Use RT Slider with your Theme?

First, Declare Support in your theme's functions.php file inside a function, which will be called at `after_setup_theme` hook. This the place, where you declare support for other stuff like `custom-logo` or `title-tag`.

```php
  	/*
	 * Enable support for RT Slider Plugin.
	 */
	 add_theme_support('rt-slider', array( 10 , 'pages', 'front-page-only', 
		 'config' => array(
			 'options' => array('speed', 'duration','random', 'autoplay','pager'),
			 'effects' => array('fade','sliceUp'),
		 )
	 ));
```
	 
###### Explanation of the Values in the Array

* 10 -> This is the Maximum no. of slides you want the user to have. **THIS MUST BE THE FIRST TERM IN THE ARRAY**
* 'pages' -> If you want user to be able to Choose upto 2 Individual Pages, on which He should Enable the slider. (Optional)
* 'front-page-only' -> If you want user to have the option to Enable the slider on Front Page only. By default, user will have the option to choose from blog, static front page, all posts & all pages. (Optional)
* 'config' -> Add this only if you want user to have control over the slider. (Optional)
  * 'options -> The list of options you want to choose from. You can choose from the Following 5 only.
    * 'speed' -> Transition Speed of the slider. (Returns value in ms) (Default = 500)
    * 'duration' -> Duration of Each Slide. (Returns value in ms) (Default = 5000)
    * 'random' -> Start Slider from Random Position. (Boolean) (Default = false)
    * 'autoplay' -> Autoplay the Slider. (Boolean) (Default = true)
    * 'pager' -> Enable the Pager. The navigation generally present below the slider. (Boolean) (Default = true)
  * 'effects' -> Add the names of all the effects your slider supports. Values in this array depend on the slider you are using. Some sliders support either fade or slide, and some sliders support over 20 effects. (Optional)

##### Most Common Usage Example.

If you want to just Enable a basic slider in your theme. Just add the following code.

```php
	 add_theme_support('rt-slider', array( 5 , 'pages' )); //Max Slides = 5, Options to Choose pages = enabled.
```

#### Place your Slider in your theme.

For example, your slider code is a file called `slider-nivo.php`
Then add this code, wherever you want the slider to show up. Generally, somewhere in header.php or front-page.php

```php
if( class_exists('rt_slider') ) {
	rt_slider('slider', 'nivo' ); 
}
```		
  
### RT Slider Functions

The list of Functions available for the Theme Developer by this plugin. 
There is just one function, which has 2 forms.

##### Function 1: 
```php
rt_slider_get( $param )
```
e.g. `$no_of_slides = rt_slider_get('count');`

Possible Values of `$param`

* count -> The No. of sliders set by user.
* speed
* duration
* random
* autoplay
* pager

The Last 5 options above, are available if you have added support for 'config' and 'options'

--------

##### Function 2
```php
rt_slider_get( $param, $slide_number )
```
This is the function you would use inside your for or foreach loop, used to render each individual slide.
The `$slider_number` is the loop index. Min Value should be 1. So start your For Loop from 1, rather than 0.

Possible Values for `$param`

* img -> the slide image
* url -> url to which the slider should link to
* cta_button -> a call to action button in the slider
* title -> Slide title
* desc -> Slide description

#### Usage Example

```php

$count = $no_of_slides = rt_slider_get('count');

for ( $i = 1; $i <= $no_of_slides; $i++ ) :
    
    $img   = rt_slider_get('img', $i);
    $url   = rt_slider_get('url', $i);
    $title = rt_slider_get('title', $i);
    $desc  = rt_slider_get('desc', $i);
    
    echo "<div class='slide'>;
      echo "<a href='".$url."' target='_blank'>";
      echo "<img src='".$img."'>";
      echo "<div class='caption>
              <div class='slide-title'>".$title ."</div>
              <div class='slide-desc'>".$desc."</div>
            </div>"; //.caption
        echo "</a>"; //.slide   
      echo "</div>"; //.slide      
              
endfor;
```


If you need any help regarding this.
[Contact me here] (http://rohitink.com/contact-me) or create an issue at Github.
