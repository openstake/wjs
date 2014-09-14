WJS - 
======



COPYRIGHT
---------
Copyright Romain WEEGER 2010 / 2014  
http://www.wexample.com  
  
Licensed under the MIT and GPL licenses :  
  
 - http://www.opensource.org/licenses/mit-license.php  
 - http://www.gnu.org/licenses/gpl.html

DESCRIPTION
-----------
wJs is a Javascript package manager written in PHP, and working trough AJAX for your personnal applications. It provides dynamic transfert of custom scripts packages between web clients and server. It contain an API to create custom packages (called collections to avoid conflicts with the "package" reserved keyword of ECMAScript) on server side and prepare it to be transferred to Javascript, and to receive it on clients side (parsing it to use result in your own applications).  
  
    w.load("packageType", "packageName", completeCallback);  
  
More than requireJs, witch is a powerful Javascript loader, wJs is able to transfert not only Javascript, but potentially any custom kind of data. For that, developers can create custom "loaders" to adjust behavior of it both on server and client sides.  
  
The original requirement of wJs was to load visual HTML elements in one shot, witch is composed by not only one kind of data, ex : HTML + images urls + CSS + some Javascript. In this way, wJs encourages to create independent libraries for your scripts, then allow access them in one simple line of code.  
  
It is free and open source, available for forking and contribution on GitHub. If you want to post reviews, comments or issues, please post on the project page.

FEATURES
--------
 - Load Javascript packages from client side.  
 - Define custom packages types / loaders  
 - Parse folders to register package automatically  
 - Create libraries containing grouped definitions  
 - Use PHP class ready to be transfert as Javascript prototypes (transcodes)  
 - Use shorthands function for objects and prototypes manipulations

INSTALL
-------
In order to use wJs you need to have some base element to transfert data from PHP to Javascript. Due to the lot of different projects and the amout of changes, this install file may not be up to date. If you have some questions, please contact me on my web page.  
  
  
  
###Install wJs  
Download and unpack wJs, place it into your library folder.  
  
  
###Configure Javascript  
Make a html script link to the jQuery library    
```  
<script type="text/javascript" src="http://code.jquery.com/jquery-1.10.2.min.js"></script>  
```  
  
	  
###Configure PHP  
Require PHP wjs internal classes.  
```  
require_once "library/wjs/wjs.inc";  
```  
	   
Create a new wJs global instance (default loaders are automatically registered).  
```  
$w = new wjs();  
```  
      
Configure response file path from client side (see section below).   
```  
$w->js_setting('path_response', 'response.php');  
```  
	  
Print wJs header in the head of your page, before the head end tag. This will load required wJs core files.  
```  
print $w->js_header();  
```  
	  
Print wJs footer at the bottom of your page before the body end tag. This will print startup package for wJs containing default loaders and preloaded page contents.   
```  
print $w->js_footer();  
```  
  
  
  
###Configure PHP response file  
In order to work correctly you need to specify a PHP response file who handle request from wJs. Let's call it "response.php", and place it at our site's root, then call wJs again.  
```  
// Load wjs.  
require_once "library/wjs/wjs.inc";  
$w = new wjs('library/wjs', TRUE);  
```  
  
Now we need to register our available scripts, use TRUE as last argument to append it to output package (see next step). This let you de filter if you want to load all available scripts or not.   
```  
// Register your scripts.    
$w->collection_item_register('javascript', 'my_script', 'library/scripts/my_script.js');  
```  
    
We need to know which script is requested by client. This example do not include security management to filter variables. WJs use two queries variables t = script_type, s=script_name.    
```  
// Using this simple script is not secure.      
// You may filter data to ensure that values     
// are safe, according your own security policy.     
$script_type = (isset($_GET['t'])) ? $_GET['t'] : FALSE;      
$script_name = (isset($_GET['s'])) ? $_GET['s'] : FALSE;  
```     
  
With theses variables, we ask wJs to add script to response.  
```  
// Append requested scripts.     
$w->output_append($script_type, $script_name);  
```  
	  
Finally, we print result.  
```  
// Render.     
print $w->js_package();  
```  
  
  
###Check result  
wJs is now configured and ready to work. In order to test result, we create an alert into our 'library/scripts/my_script.js' file, and a button in our page containing a request to wJs.    
```  
w.load('javascript','my_script');  
```    
      
This is the whole button code.    
  
```  
<input type="button" onclick="w.load('javascript','my_script');" value="Click me"/>  
```

THANKS
------
I would like to thanks all people who have trusted an encouraged me, consciously or not. Like all of my projects, this program is the result of a lot of loneliness, questions, doubts, pain, but hope and love too. I sincerely hope you'll enjoy it. Thanks to Carole for her incredible Love.