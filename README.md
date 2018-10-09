# wp-theme-doc-01
Custom Template How To - G


1. #### When you have WordPress installed, go into
- In `Settings > General`, and remove the __WordPress tag line__.
- In `Reading`, make sure the __Discourage search engines from indexing this site__ is checked.
- In `Discussion`, uncheck the __first three check__ boxes, and disable the __Avatar Display checkbox__. 
- In `Media`, uncheck the __Organize my uploads into month..__ checkbox. 
- In `Permalink` Section, choose __Custom Structure__ , and make it the following > ```/%category%/%postname%/```


2. #### Add the following plugins:
- All In One WP Security
- Eggplant 301 Redirects
- Nested Pages
- Yoast SEO
- WP Accessibility
- Autoptimize


3. #### Start with homepage, make `index.html` into `index.php`. Take the __comments__ from the twenty seventeen theme’s front-page.php file and change the __verbiage__.


4. #### Make sure header/footer match on the secondary and home page. Note any differences. 


5. #### Create a header.php file and footer.php file (don’t forget the hooks!) based on this Take the comments from the twenty seventeen files. 


6. #### In the footer file, please replace the date with:
```php
<?php echo date('Y'); ?>
```
`This will dynamically change the date.`


7. #### Also set the information about Glacial to:
```php
All Rights Reserved.
<a href="https://www.glacial.com/our-services/medical-website-design/" target="_blank" title="Medical Website Design">
  Medical website design
</a> by 
<a href="http://www.glacial.com" title="Glacial Multimedia" target="_blank">
  Glacial Multimedia
</a> &copy;
```

8. #### In the header.php file, be sure and add the following code into the body tag:
```php
<?php body_class( $class ); ?>
```
`This will give each page a unique set of classes so you can have better control of elements with CSS. If there already is a class on the body, for example,`

```php
<body class=”sample-class”>, simply change the code to this:
<?php body_class( ‘sample-class’ ); ?>
```


9. #### Add the calls for the header and footer onto the index file. Once this is set, go into the CMS, then `Settings – Reading`. Where it says, "__Your homepage displays__", change to “__A static page__” to the page you wish to be your homepage (create a page called Home).


10. #### Next, copy all the content in index.php and paste it into a new file called, `front-page.php`. Next, grab the contents in the twenty seventeen theme from index.php and paste it directly into the `index.php file in our theme`. This file will just be a placeholder for now. Be sure to change the verbiage in the comments.


11. #### Next, create a file called page.php. Open up the secondary page provided from webflow and take out the header and footer. Copy what’s left and put it into page.php. Grab the comments from the twenty seventeen page.php file and put it onto yours. Next add the header/footer call. Also, wherever the title of the page is, replace it with the following code:
```php
  <?php the_title(); ?>
```
`This will dynamically pull the title of whatever page you are on.`


12. #### If the secondary pages have a sidebar, create a file called sidebar.php and place all the sidebar content into this file. Be sure and grab the comments from the sidebar.php file in the twenty seventeen theme. Use the following to call the sidebar:
```php
<?php get_sidebar(); ?>
```


12. #### Now we are going to want to replace the related page elements (from the mockup) with the following. For the title, replace it with:
```php  
<a href="<?php echo get_permalink( $post->post_parent ); ?>" title="<?php
$parent_title = get_the_title($post->post_parent);
echo $parent_title; ?>" class="related-page-title"><?php
$parent_title = get_the_title($post->post_parent);
echo $parent_title; ?>
</a>
```
`This will dynamically change the title to the parent page.`



12. #### Next, replace the actual related pages with:
```php
<ul>
  <?php
    if($post->post_parent)
    $children = mytheme_list_pages("title_li=&child_of=".$post->post_parent."&echo=0&sort_column=menu_order");
    else
    $children = mytheme_list_pages("title_li=&child_of=".$post->ID."&echo=0&sort_column=menu_order");
    if ($children) { 
  ?>
    <?php echo $children; ?>
  <?php } ?>
</ul>
```
`And place the following into functions.php:`
```php
function mytheme_list_pages($param) {
	$pages = get_pages($param); 
	foreach ( $pages as $page ) {
	$li  = '<li><a href="' . get_page_link( $page->ID ) . '" title="';
	$li .= esc_attr($page->post_title);
	$li .= '">';
	$li .= $page->post_title;
	$li .= '</a></li>';
	echo $li;
	}
}
```

12. #### Now let’s create the function file. Create a new file called functions.php. Now place an open and close php tag. 
```php
<?php ?>
```
`Within that, is where we will put all of the function content. Let’s start by adding the following:`
```php
add_theme_support( 'title-tag' );
add_theme_support( 'post-thumbnails' );
set_post_thumbnail_size( 270, 270 );
add_filter( 'post_thumbnail_html', 'remove_width_attribute', 10 );
add_filter( 'image_send_to_editor', 'remove_width_attribute', 10 );

function remove_width_attribute( $html ) {
   $html = preg_replace( '/(width|height)="\d*"\s/', "", $html );
   return $html;
}
```
`This adds support for title tags, activates thumbnail images for blogs, sets the thumbnail dimensions and removes the height and width attribute when images are added through the cms.`

12. #### Now lets create the primary navigation. Add the following to the functions file:
```php
function register_my_menus() {
  register_nav_menus(
    array(
      'primary-nav' => __( 'Primary Navigation' ),
	  'mobile-menu' => __( 'Mobile Navigation' ),
      'footer-menu' => __( 'Footer Menu' )
    )
  );
}
add_action( 'init', 'register_my_menus' );
```
`This will make “Menu” appear under “Appearance” in the CMS. It also creates 3 different menus, 
  - Primary Navigation 
  - Mobile Navigation
  - Footer Menu.`
  
`While you may not need all of these, there are setup just in case. You can also create more than these. You now have access to create a navigation menu. You will want to add all of the pages into the CMS and create the menu under “__Apperance__” then “__Menu__”.`



12. #### Next, add the following code to the header.php file where you would like the menu to be placed and replace what’s there already for a menu, with:
```php
<?php wp_nav_menu( array( 'theme_location' => 'primary-nav' ) ); ?>
```



12. #### Then add the following CSS to the style.css file:

```css
/* Dropdown Menus */
/* ===== Top ===== */
#navigation .current-menu-item a { color:#007fba;}
#navigation ul { list-style:none; margin:0; padding:0; display:flex; justify-content:center; }
#navigation ul li{ display:inline-block; text-align:left; }

/* ===== First Level ===== */				
#navigation ul li { position:relative; padding:0; margin:0; }
#navigation ul ul li { border:none; }
#navigation ul li a 
	{
		margin-bottom: 0; color: #1b1b1b; display: inline-block;
		font-size: 16px; line-height: 20px; padding: 10px 20px;
		font-weight:400; font-family:Lato, sans-serif; text-decoration: none;
		transition: all 400ms ease; -webkit-transition: all 400ms ease;
		-moz-transition: all 400ms ease; -ms-transition: all 400ms ease;
	}
#navigation ul li:hover a { position:relative; background-color: #febd62;}
#navigation ul ul,	#navigation ul li:hover ul ul { position:absolute; display:none; }
#navigation ul ul li:hover ul,
#navigation ul li:hover ul li:hover ul { display:block; top:0px; left: 100%;}
	
/* ===== Second and Third Level ===== */
#navigation ul li:hover ul 
	{
		display:block; position:absolute; left:0; top:100%;
		width:auto; height:auto; margin:0; padding:0;
	}

#navigation ul ul ul
	{
		background:#e4e4e4 !important;
		border-color:#e4e4e4 !important; margin-left:-14px;
	}
#navigation ul ul li a 
	{
		float:none; line-height:normal; font-variant:normal;
		font-weight:normal; width:320px; font-size:16px;
		color:#353535 !important; text-transform:none; padding:16px 10px;
		background:#f4f9fd !important; border-bottom:1px solid #f9e6cb;
	}
#navigation ul ul li a { color:#fff; }
#navigation ul ul li:hover a {
    color:#fff !important;
	background-color:#079dad !important;
}
#navigation ul ul li:hover ul li a { color:#353535 !important; background:#fff2e0 !important; }
#navigation ul ul li:hover ul li:hover a { color:#fff; background:#079dad !important;}
```
`Also add the following into the __media query with a max width of 990px__:`
```css
#navigation ul{ display:block; }
#navigation ul li{ float:none; width:100%; display:block; text-align:center; }
#navigation ul li:hover ul{ display:none; }
```










