# About

This module generates a userscript header string to append to your scripts.

# Usage

First install: `npm install generate-userscript-header`

Then you can use it:

```javascript
var generateUserscriptHeader = require('generate-userscript-header');

var userscript = {
	'name': 'ACME Userscript Maker',
	'namespace': 'http://example.com/',
	'author': '{{{pkg.author}}}',
	'homepage': '{{{pkg.homepage}}}',
	'grant': 'none',
	'include': [
		'http://google.com/*',
		'https://google.com/*'
	]
};

var context = {
	pkg: {
		author: 'John Doe',
		homepage: 'http://example.com/johndoe'
	}
};

var header = generateUserscriptHeader(userscript, context);

console.log(header);
```

Output:

```
// ==UserScript==
// @name ACME Userscript Maker
// @namespace http://example.com/
// @author John Doe
// @homepage http://example.com/johndoe
// @grant none
// @include http://google.com/*
// @include https://google.com/*
// ==/UserScript==

```

# API

This module exports a single method that outputs a userscript metadata block as a string given the data to convert. Data is parsed with [mustache][mustache] and replaced with the data of a certain context.

### Syntax

```javascript
var generate = require('generate-userscript-header');
generate(userscript, context)
```

### Parameters

| Name | Type | Description |
|------|------|-------------|
| userscript | object | The object containing the userscript data. |
| context | object | The data used to parse values with [mustache][mustache]. Use {{{yourKey}}} in the data to parse. |

### Return

| Type | Description |
|------|-------------|
| string | The finalized metadata block. |

[mustache]: http://mustache.github.io/mustache.5.html
