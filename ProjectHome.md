**$.plugin** is a jQuery Plugin that allows you to better manage the different plugins you use in your website or web application.

This is especially useful if you use a number of plugins each with its own .js and .css files. It is even more useful if not all plugins are needed for each page.

## Performance Improvements ##

  1. Users will only download scripts and styles that are required (accoding to selectors you specify)
  1. **Page Caching** - Scripts and styles are only downloaded once
  1. **Session Caching** - Scripts and styles are stored in browser's _sessionStorage_ to reduce http requests (Firefox 3 only, for now)

$.plugin itself is just 10KB uncompressed, 4KB minified, and 3KB compressed

## Sample Code ##
### Define your plugins ###
```
$.plugin('tabs',{
	files: ['../styles/style.css',
		'../scripts/jq.tabs.pack.js'],
	selectors: ['.nav-tabs'],
	callback : function(){ $(".nav-tabs").tabs(); } 
});
$.plugin('anotherPlugin', ... );
```

### Import them where necessary ###
```
$(document).bind('ready',function(){
	$.plugin('tabs').get(); // to get files associated with 'tabs' plugin	
	// or $.plugin('tabs',function(){ alert('Tabs loaded!') })
	
	// or $.plugin() to get all files associated with all plugins
});
```

**Latest Version: 0810.02 (October 2, 2008)**