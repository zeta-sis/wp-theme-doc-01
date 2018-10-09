# wp-theme-doc-01
Custom Template How To - G


1. __When you have WordPress installed, go into__
- In `Settings > General`, and remove the __WordPress tag line__.
- In `Reading`, make sure the __Discourage search engines from indexing this site__ is checked.
- In `Discussion`, uncheck the __first three check__ boxes, and disable the __Avatar Display checkbox__. 
- In `Media`, uncheck the __Organize my uploads into month..__ checkbox. 
- In `Permalink` Section, choose __Custom Structure__ , and make it the following > ```/%category%/%postname%/```

2. __Add the following plugins:__
- All In One WP Security
- Eggplant 301 Redirects
- Nested Pages
- Yoast SEO
- WP Accessibility
- Autoptimize

3. Start with homepage, make `index.html` into `index.php`. Take the __comments__ from the twenty seventeen theme’s front-page.php file and change the __verbiage__.

4. Make sure header/footer match on the secondary and home page. Note any differences. 

5. Create a header.php file and footer.php file (don’t forget the hooks!) based on this Take the comments from the twenty seventeen files. 

6. In the footer file, please replace the date with: ```php <?php echo date('Y'); ?> ``` This will dynamically change the date. 

7. This will dynamically change the date. Also set the information about Glacial to:
```php
All Rights Reserved. <a href="https://www.glacial.com/our-services/medical-website-design/" target="_blank" title="Medical Website Design">Medical website design</a> by <a href="http://www.glacial.com" title="Glacial Multimedia" target="_blank">Glacial Multimedia</a> &copy;
```
