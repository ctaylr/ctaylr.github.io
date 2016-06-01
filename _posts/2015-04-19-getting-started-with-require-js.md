---
published: true
title: Getting started with require.js
layout: post
---
## So, what is require.js?
Require.js is  - simply put - a library which allows you a method of managing multiple modules and scripts within a javascript application. You define your applications with modules, and then you can pick and choose which scripts get loaded on which pages. It handles loading dependencies in order (as long as you've configured it correctly), and helps you to organise your code.

## When should I be using this?
As usual, this isn't always useful in EVERY project you're likely to undertake. Using require.js is best suited to large scale-able websites/applications, that can sensibly split in lots of small components which span multiple "pages"/views - especially if they aren't really necessary on every individual one.

## Getting set up
The initial setup for require.js is fairly simple - go to the homepage and download a copy of the script. Then include it at the bottom of your page like any other script. There is one extra attribute to be aware of. "data-main" tells require.js of the first module to include once it has loaded:

    &lt;script type="text/javascript" data-main="js/main" src="js/require.js"&gt;&lt;/script&gt;

Here, I'm telling require.js to load, and using this attribute to pass "js/main.js", which will be the file it loads initially - the file that will control the rest of the application. Note here, that I haven't specified the .js extension on my main file - this is intentional, as require.js will add this for me when it requests the document.

## Starting a new application
Within this main file, I have added the following code:

    require(['jquery','mod1','mod2','mod3','mod4'],function($,mod1,mod2,mod3,mod4){
    ....
    })();

Here I am defining the very base of my application. The require statement I've given here takes two parameters - an array with a list of modules to load as dependencies for this section of code, and a function that is called when they are all loaded (with named references to each). These are processed in order - so the first item in the array, will be loaded and passed through to the function as the first parameter in its call etc.

In this example, I'm including (from the same folder as my main.js) the files "jquery.js" (to which I'm assigning the variable '$'), 'mod1.js' - that I'm assigning to the variable mod1, 'mod2.js' is included and returned in the variable mod2 - I'm sure you get the idea. These modules are (by default) referred to by filename, related to the path of main.js, but with the file extension removed. It is also possible to refer to these modules by a set "alias", which I'll talk about a little later.

Within the function call, I can write code as usual - safe in the knowledge that require.js will have ensured all the required scripts I've specified are available for me to use in advance.

## Modules in require.js
Modules in require.js are written in "AMD" format (which stands for Asynchronous Module Definition, if you are really interested). This is a very simple format that allows me to list dependencies from within a module. An example of a module can be found below:

    define(['jquery'],function($){
	    return {
    		"setText" : function(){
	    		$('.text').text('Hello World');
		    }
	    }
    });

The format for this is similar to the main.js file - except instead of using "require", I'm using "define" to specify the list of scripts/modules to ensure are loaded before the function is called. You could also use require here, but there is a subtle difference between the two different statements - using "require" will load all specified modules AND all dependencies of those modules too. Define will just load the modules, but not their dependencies.

In the code above, I'm loading JQuery as a dependency, then creating a simple Javascript object with a basic function in it - this is a very simplified cut down example, but hopefully you get the idea.

## Working with non-AMD modules
Many JQuery plugins come with AMD support out-of-the-box, but some haven't been updated or just don't have support. Luckily, require.js allows you to handle these files using a special configuration named a "shim". Within the main.js file, we can add a require.config call, which takes a JSON object which allows various configurations to be set, including allowing us to use non-AMD modules in the same way as supported ones. Here's an example of this "shim" config:

    require.config({
    	"shim": {
    		"mod4": {
		    	"deps":["jquery"],
	    		"exports": "module4"
	    	}
    	}
    });

Here I'm adding support for the non-AMD module "mod4" - by specifying its dependencies, and the variable that it returns which I wish to use in my application. If you are using a javascript file that doesn't return a single value (If it is just a set of functions or something similar), you can consider wrapping them all in a closure and returning the ones you require as a JSON object - something like:

    (function(){
       function blah(){
         ....
       }

      function stuff(){
       .....
      }

      function doodah(){
       .....
      }

      return {
       "blah":blah,
       "stuff":stuff,
       "doodah": doodah
      }
    })();


So now, we can add non-AMD modules in the same way as normal - we have already defined the dependencies for them, and told our require.js application which variables we want it to use.

## Using alias' for modules and setting a base file path
By default, require.js will look for its referenced files relative to the folder as the main.js file. You can specify file paths/names in the calls for each individual include, but this can cause problems - first up, if your using a lot of long file paths, it can be ugly. Secondly, if you are using version numbers in your filenames (as many libraries do) upgrading a library becomes a slightly irritating find and replace (OK - not really THAT irritating, but surely it'd be better to only have to change this stuff in one place?)

The require.config function allows you to set alias' for certain module names. You can then refer to these alias' in the same way as file names. For instance, at time of writing, the default jquery 1.x version is "jquery-1.11.2.min.js". If I wanted to refer to this simply as "jquery", I can write the following code in my main.js :

    require.config({
      "paths": {
        'jquery': 'jquery-1.11.2.min'
      }
    });

This tells Require that when I refer to "jquery", I actually want it to load jquery-1.11.2.min.js. This is also really useful when using scripts hosted on a CDN, as you can use fully qualified "paths" to refer to files on remote servers (see this example for more info).

Finally, the last feature I'll cover in this particular post, is changing the default base path/root for your javascript modules. This saves you from having to keep writing relative paths over and over again if your code is in a different location, and is again changed by setting values in require.config:

    requirejs.config({
        "baseUrl": "js/lib"
    });

So, that's about it for now. I've added a brief (and very simple) project to github so you can peruse and see what I've been talking about in practice all together (link is below). There is more you can do with require than just what I've covered here, and some of it is very handy - this has mainly been an overview of the initial setup - but the API documentation is pretty good (with examples!), and you can reach them on the links below.

Happy modularising!

RequireJS
RequireJS API
Very simple example project (Github)
