# [EVRYTHNG](https://www.evrythng.com) Extended JS SDK for Node.js


**evrythng-extended.js** is the extended version of a Javascript library making it a breeze to interact with the EVRYTHNG API thanks to its fluent API. It's primarily meant to be used in **Node.js** apps, but thanks to  [UMD](https://github.com/umdjs/umd) compatibility it can be used for your Web (mobile, desktop or hybrid) apps too.

## Installation

### Node.js

**evrythng-extended.js** is available as an NPM package. Install it using:

    npm install evrythng-extended

### Browser

Not recommended - web apps should not need the extended features and only use the basic version of [**evrythng.js**](https://github.com/evrythng/evrythng.js).
If you know what you're doing, you can install the NPM package as described above, or include the script from our CDN in your HTML file using:
                                                       
    <script src="//cdn.evrythng.net/toolkit/evrythng-js-sdk/evrythng-extended-2.1.0.min.js"></script>

Or always get the last stable release:

    <script src="//cdn.evrythng.net/toolkit/evrythng-js-sdk/evrythng-extended.js"></script>
    <script src="//cdn.evrythng.net/toolkit/evrythng-js-sdk/evrythng-extended.min.js"></script>
   
For HTTPs you'll have to use:

    <script src="//d10ka0m22z5ju5.cloudfront.net/toolkit/evrythng-js-sdk/evrythng-extended-2.1.0.min.js"></script>

respectively

    <script src="//d10ka0m22z5ju5.cloudfront.net/toolkit/evrythng-js-sdk/evrythng-extended.min.js"></script>


## Usage

**evrythng.js** uses UMD, which makes it available in every environment running Javascript.

For advanced usage and options, see the [Documentation section](#documentation) below and the API 
documentation on [EVRYTHNG's Developer Portal](https://dashboard.evrythng.com/developers). 

**Note:** Be sure to only include your EVRYTHNG App API key and **not** your Operator or App User key in any public application code (read more [here](https://dashboard.evrythng.com/developers/apidoc#appusers)).

### Node.js

```javascript
var EVT = require('evrythng-extended');

// Initialise Account Scope
// **DO NOT include your Account API Key in any public code**, that includes committing to any public repositories (GitHub, BitBucket, etc.)!
var account = new EVT.Account(ACCOUNT_API_KEY);

// Initialise Application Scope, passing the Sccount Scope as parent
var app = new EVT.App('appApiKey', account);
...
```

### Browser

Not recommended - web apps should not need the extended features and only use the basic version of [**evrythng.js**](https://github.com/evrythng/evrythng.js).
If you know what you're doing, please refer to [**evrythng.js** documentation](https://github.com/evrythng/evrythng.js#browser) for details.

## What's included

All features of **evrythng.js** are available without changes.

Features available only in **evrythng-extended.js**:
1. Work in account context:
```javascript
// Initialise Account Scope using account API key
// **DO NOT include your API Key in any public code**, that includes committing to any public repositories (GitHub, BitBucket, etc.)!
var account = new EVT.Account(ACCOUNT_API_KEY);

// Read all Thngs in your account
account.thng().read().then(function(thngs){
  console.log(thngs);
  
  // Delete a Thng
  thngs[0].delete();
});
```

2. Use an app as operator 
```javascript
// Initialize App Scope using application API key and pass the account as parent scope
var app = new EVT.App(APP_API_KEY, account);

// Use as you would with `evrythng.js`
...
```
This lets you perform operations that require operator access but limited to a single app and retain the app scope.

## Documentation

The [EVRYTHNG API is documented here](https://dashboard.evrythng.com/developers/apidoc).

## License

Apache 2.0 License, check `LICENSE.txt`

Copyright (c) EVRYTHNG Ltd.
