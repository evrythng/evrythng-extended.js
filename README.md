# [EVRYTHNG](https://www.evrythng.com) Extended JS SDK for Node.js

**evrythng-extended.js** is the extended version of a Javascript library making it a breeze to interact with the EVRYTHNG API thanks to its fluent API.
We provide two environment-specific versions: AMD and CommonJS to utilise the best of both browser and Node.js.


## Installation

**Note**: `evrythng-extended.js` uses [Promises/A+](https://promisesaplus.com/). Node.js in versions before 0.12 does not support that natively and support in 0.12 is buggy; to deal with this, we use the [Native Promise Only](https://github.com/getify/native-promise-only) polyfill internally.

**Warning: DO NOT include your Operator API Key in any public code**, this includes committing to any public repositories (GitHub, BitBucket, etc.)! This is very important especially when using evrythng-extended.js in a web app.

### Node.js

**evrythng-extended.js** is available as a NPM package. Install it using:

    npm install evrythng-extended

### Browsers

**Note**: most web apps will not need the extended features and should only use the basic version of [**evrythng.js**](https://github.com/evrythng/evrythng.js).

#### With [Bower](http://bower.io/)

The Bower package includes the AMD build of evrythng-extended.js. You can either load it directly or use a loader like [require.js](http://requirejs.org/).

    bower install evrythng-extended
    
Then just load the script in your page:

    <script src="bower_components/evrythng-extended/dist/evrythng-extended.js"></script>

Once the script loads, `EVT` becomes available as a browser global. 

If you want to automate this, there are several [Grunt](http://gruntjs.com/) plugins which you may find useful:

* [grunt-wiredep](https://github.com/stephenplusplus/grunt-wiredep) finds your components and injects them directly into the HTML file you specify.
* [grunt-bower-concat](https://github.com/sapegin/grunt-bower-concat) does automatic concatenation of installed Bower components (JS and/or CSS) in the right order.

Or if you prefer [Gulp](http://gulpjs.com/):

* [main-bower-files](https://github.com/ck86/main-bower-files) (works with Grunt too)
* [gulp-bower-src](https://github.com/bclozel/gulp-bower-src) - `gulp.src` files from your bower components directory, using your bower.json configuration file.

## Usage

For advanced usage and options, see the [Documentation section](#documentation) below and the API 
documentation on [EVRYTHNG's Developer Portal](https://dashboard.evrythng.com/developers). 

**Note:** Be sure to only include your EVRYTHNG App API key and **not** your Operator or App User key in any public application code (read more [here](https://dashboard.evrythng.com/developers/apidoc#appusers)).

### Node.js

```javascript 
var EVT = require('evrythng-extended');

// Initialise Operator Scope
// **DO NOT include your Operator API Key in any public code**, this includes committing to any public repositories (GitHub, BitBucket, etc.)!
var operator = new EVT.Operator(OPERATOR_API_KEY);

// Initialise Application Scope, passing the Operator Scope as parent
var app = new EVT.App('appApiKey', operator);
...
```

### Browsers

**Note**: most web apps will not need the extended features and should only use the basic version of [**evrythng.js**](https://github.com/evrythng/evrythng.js).

### With RequireJS (AMD)

```javascript
var bowerPath = '../bower_components/'; // replace with path to your local bower directory
requirejs.config({
    paths: {
        evrythng: bowerPath + 'evrythng-extended/dist/evrythng-extended'
    }
});
    
require(['evrythng'], function (EVT) {

  var app = new EVT.App('apiKey');
  ...

});
```

### Plain Javascript

If you aren't using any of the above script loading mechanisms, the EVT module is available
as a browser global:

```javascript
var app = new EVT.App('apiKey');
...
```

## What's included

All features of **evrythng.js** are available without changes.

Features available only in **evrythng-extended.js**:
1. Work in account context (as an operator):
```javascript
// Initialise Operator Scope using Operator API key
//    **DO NOT include your Operator API Key in any public code**,
//    this includes committing to any public repositories (GitHub, BitBucket, etc.)!
var operator = new EVT.Operator(OPERATOR_API_KEY);

// Read all Thngs in your account
operator.thng().read().then(function(thngs){
  console.log(thngs);
  
  // Delete a Thng
  thngs[0].delete();
});
```

2. Use an app as operator 
```javascript
// Initialize App Scope using application API key and pass the operator as parent scope
var app = new EVT.App(APP_API_KEY, operator);

// Use as you would with `evrythng.js`
...
```
This lets you perform operations that require operator access but limited to a single app and retain the app scope.

## Documentation

The [EVRYTHNG API is documented here](https://dashboard.evrythng.com/developers/apidoc).

## License

Apache 2.0 License, check `LICENSE.txt`

Copyright (c) EVRYTHNG Ltd.
