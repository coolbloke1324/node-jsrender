# Node-JSRender

!!! UPDATE 5th Feb 2016: Boris Moore (the creator of jsrender) recently released a new official ***jsrender*** version (https://www.npmjs.com/package/jsrender) that includes full support for Node.js and Browserify. This ***node-jsrender*** wrapper package is therefore no longer needed. Please use the official ***jsrender*** package, directly, instead:

```bash
npm install jsrender
```

The official package github repo is available here: https://github.com/BorisMoore/jsrender

**This project will no longer be actively maintained**.



# PREVIOUS README CONTENTS

An ~~actively maintained~~ wrapper for the jsrender project by @borismoore (https://github.com/BorisMoore/jsrender). Uses latest source from the jsrender project and extends functionality for easy use in Node.js.

## Install

> PLEASE SEE NOTE ABOVE - THIS LIBRARY IS NO LONGER MAINTAINED AND HAS BEEN REPLACED

```bash
npm install node-jsrender
```

## Using With Express
If you use express and wish to use jsRender as your express template engine you can now do so.
You can specify the engine to use via:

	var express = require('express');
	var app = express();
	var nodeJsRender = require('node-jsrender');
	
	// Register jsRender with express to handle html files
	nodeJsRender.express('html', app);
	
	// Set express template engine to jsrender
	app.set('view engine', 'html');

## Usage Without Express (Manually Rendering)

### Loading a Template From a String
```javascript
// Require the node module
var jsrender = require('node-jsrender');

// Load a template from string
jsrender.loadString('#myTemplate', '{{:data}}');

// Render the template with data
jsrender.render['#myTemplate']({data: 'hello'});

// Output is: "hello"
```

### Loading a Template From a File (Synchronously)
```javascript
// Require the node module
var jsrender = require('node-jsrender');

// Load a template from ./templates/myTemplate.html
//     Contents of ./templates/myTemplate.html is: "{{:data}}"
jsrender.loadFileSync('#myTemplate', './templates/myTemplate.html');

// Render the template with data
jsrender.render['#myTemplate']({data: 'hello'});

// Output is: "hello"
```

### Loading a Template From a File (Asynchronously)
```javascript
// Require the node module
var jsrender = require('node-jsrender');

// Load a template from ./templates/myTemplate.html
//     Contents of ./templates/myTemplate.html is: "{{:data}}"
jsrender.loadFile('#myTemplate', './templates/myTemplate.html', function (err, template) {
	if (!err) {
		// Template was loaded
		// Render the template with data
		jsrender.render['#myTemplate']({data: 'hello'});
		
		// Output is: "hello"
	} else {
		throw(err);
	}
});
```

### Nested Templates

In jsrender, you can have templates that reference other templates, nested templates. But to work, you must register the nested templates before rending the parent template.

```javascript
// Require the node module
var jsrender = require('node-jsrender');

// Load parent template from string
//     {{for items tmpl="#listItem" //}} indicates a nested template
jsrender.loadString('#list', '<ul>Grocery List</ul>{{for items tmpl="#listItem" /}}</ul>');

// Load child template from string
//      Nested templates must be registered with a name matching the parent template before rendering the parent template
jsrender.loadString('#listItem', '<li>{{:name}}</li>');

// Render the parent template with data
jsrender.render['#list']({items: [{name:'Carrots'}, {name: "Banana"}]});

// Output is: "<ul>Grocery List</ul><li>Carrots</li><li>Banana</li></ul>"
```
