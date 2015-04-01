# Introduction #
The purpose of this plugin is to minimise initial loading times.

It's very easy to use:
**1) Define the scripts you normally use**
```
var load_elements = {
    test : {
       funcName : "testing",
       attributes : {"id" : "test"},
       source : { script: '<script type="text/javascript" src="test.js"></script>'}
    }
};
```
**where,**
  * 'test' is the general name of your script
  * 'funcName' is the main function of your script
  * 'attributes' are the attributes of elements which your script acts upon
  * 'source' is the source of all scripts and styles to be loaded as necessary


**2) Execute your functions**
```
i.   $.loader().init('testing',function(){alert('hello world');testing();});
```
or
```
ii.  $.loader().init($.loader().isNeeded("test"),function(){alert('hello world');testing();});
```


That's pretty much it. Suggestions, contributions, and everything else are welcome.

# Notes #
  1. **funcName** must be string
  1. **attributes** must be object
  1. **source** must be object
  1. **load\_elements** is the object containing all necessary info for loading scripts.
---
  1. **$.loader(`load_elements`)**: This function checks for DOM elements that have the attributes you specified. Upon finding such elements, the function loads the scripts and styles specified. **Best used after the DOM has finished loading (e.g. $(document).bind("ready",function(){` .. here .. `}))**
  1. **$.loader().isNeeded(`var`)**: This function checks whether the `attributes` of the element you specified (`var`) are found in the DOM. If they exists, it will return the `funcName` for that element. Otherwise, returns false.
  1. **$.loader().init(`function`,function(){ `.. callback ..` })**: This function makes sure that `function` is loaded before executing it. If the script including this function is not loaded, it will load it. After 5 (timed) attempts the script stops executing and throws an error (in console). Once the script is loaded and the function is ready for use, the `callback function` is executed.

# Example #
Consider I specify my elements as:
```
var load_elements = {
	test : {
		funcName : "function_testing",
		attributes : {"id" : "test"},
		source : {
			script: '<script type="text/javascript" src="test.js"></script>',
			script_1: '<script type="text/javascript" src="test.js"></script>'
		}
	},
	test_2 : {
		funcName : "function_testing_2",
		attributes : {"id" : "test2", "maxlength": true},
		source : {
			script: '<script type="text/javascript" src="test_2.js"></script>',
			script2: '<script type="text/javascript" src="test_2_1.js"></script>',
			css: '<link href="test_2.css" rel="stylesheet" media="screen" type="text/css" />'
		}
	}
};

```

I check whether or not the scripts and styles are needed by using:
```
$(document).bind('ready',function(){
	$.loader().init($.loader().isNeeded("test"),function(){
           alert("There is an element with ID = 'test'. Function 'function_test' is ready to be used");
        });

	$.loader().init('test_2',function(){
           alert("I don't know if there is an element with ID ='test2' or maxlength attribute, but I just loaded the necessary files and 'function_testing_2' is ready for use");
        });
});
```


# Download Lazy Loader #
http://code.google.com/p/lazyloader/downloads/detail?name=jquery.loader.js