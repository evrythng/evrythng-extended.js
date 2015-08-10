# [EVRYTHNG](https://www.evrythng.com) Client Javascript SDK (Extended)

**evrythng-extended.js** is an extended version of [*evrythng.js*](https://github.com/evrythng/evrythng.js)
that adds Operator administrative capabilities (read about
[Scope and Permissions](https://dashboard.evrythng.com/developers/apidoc/scopes#operator-permissions)). This means you need
your Account Operator API key, which you can find in your [Account settings](https://dashboard.evrythng.com/account) page.

**evrythng-extended.js** can be used both in Web applications (Browser) and embedded/server applications using Node.js. The
difference being the transport layer - Browser's XHR vs Node's HTTP.

> **evrythng-extended.js** is intended for administrative operations only - the same sort of actions you would do on 
the [EVRYTHNG Dashboard](https://dashboard.evrythng.com). Be sure to **never** include your EVRYTHNG **Operator API key** 
in any public source code (read more about [Scope Permissions](https://dashboard.evrythng.com/developers/apidoc/scopes#permissions)).
You can use it in a server-side application or if you dynamically retrieve the Operator API key from a server call.

> See [Related Tools](#related-tools) below for other usages.

## Installation

### Node.js

    npm install evrythng-extended --save

### Browsers

**Note**: Most Web Applications will not need the extended features and should use the core version of 
[*evrythng.js*](https://github.com/evrythng/evrythng.js) instead.

##### With [Bower](http://bower.io/)

    bower install evrythng-extended --save
    
The Bower package is [AMD](http://requirejs.org/docs/whyamd.html)-compatible. This means you can load 
it asynchronously using tools like [Require.js](http://requirejs.org/) or simply dropping the script tag 
into your HTML page:

    <script src="bower_components/evrythng-extended/dist/evrythng-extended.js"></script>

See [Usage](#usage) below for more details.

##### Load from CDN

Add the script tag into your HTML page:

    <script src="//cdn.evrythng.net/toolkit/evrythng-js-sdk/evrythng-extended-3.2.0.min.js"></script>
 
Or always get the last release:

    <script src="//cdn.evrythng.net/toolkit/evrythng-js-sdk/evrythng-extended.js"></script>
    <script src="//cdn.evrythng.net/toolkit/evrythng-js-sdk/evrythng-extended.min.js"></script>
    
For HTTPS you need to use:

    <script src="//d10ka0m22z5ju5.cloudfront.net/toolkit/evrythng-js-sdk/evrythng-extended-3.2.0.min.js"></script>
    <script src="//d10ka0m22z5ju5.cloudfront.net/toolkit/evrythng-js-sdk/evrythng-extended.js"></script>
    <script src="//d10ka0m22z5ju5.cloudfront.net/toolkit/evrythng-js-sdk/evrythng-extended.min.js"></script>

## Usage

**evrythng-extended.js** works exactly the same way as *evrythng.js*, just with more resources (endpoints). 
See all Operator permissions in [API key permissions](https://dashboard.evrythng.com/developers/apidoc/scopes#permissions) 
and the usage examples in [*evrythng.js* documentation](https://github.com/evrythng/evrythng.js#examples).

**Note:** **DO NOT include your Operator API Key in any public code**. This includes committing to any 
public repositories (GitHub, BitBucket, etc.). If you have done so, you can reset your key in your 
[Account settings](https://dashboard.evrythng.com/account) page.

For advanced usage and options, see [Documentation](#documentation) below.

#### Node.js

```javascript 
var EVT = require('evrythng-extended');

// Initialise Operator Scope
var operator = new EVT.Operator(OPERATOR_API_KEY);
...
```

#### RequireJS (AMD)

```javascript
requirejs.config({
  paths: {
    'evrythng-extended': '../bower_components/evrythng-extended/dist/evrythng-extended'
  }
});
    
require(['evrythng-extended'], function (EVT) {

  var operator = new EVT.Operator(OPERATOR_API_KEY);
  ...

});
```

#### Globals

If you aren't using any of the above script loading mechanisms, the EVT module is available
as a browser global (`EVT`):

```javascript
var operator = new EVT.Operator(OPERATOR_API_KEY);
...
```

## Examples 

#### General

```javascript
// Read all thngs in your account (not scoped)
operator.thng().read().then(function(thngs){
  console.log(thngs);
  
  // Delete a thng
  thngs[0].delete();
});

// Create an action type
operator.actionType().create({
  name: '_orderPizza',
  customFields: {
    displayname: 'Order Pizza Now!'
  }
});

// Read Default Redirection a thng
EVT.api({
  apiUrl: 'https://tn.gg',
  url: '/redirections',
  params: {
    evrythngId: '12345'
  },
  authorization: OPERATOR_API_KEY
}).then(function(redirections){
  console.log(redirections);
});

// Get QR code
EVT.api({
  apiUrl: 'https://tn.gg',
  url: '/1234.png',
  accept: 'image/png'
});

...
```

---

## Documentation

The [EVRYTHNG API](https://dashboard.evrythng.com/developers/apidoc) has *evrythng.js* examples whenever applicable.
If you'd like to see what's going on under the hood, check out the [Annotated Source](http://evrythng.github.io/evrythng-source.js).

## Source Maps

Source Maps are available, which means that when using the minified version, if you open 
Developer Tools (Chrome, Safari, Firefox), *.map* files will be downloaded to help you debug code using the 
original uncompressed version of the library.

## Related tools

#### evrythng.js

[`evrythng.js`](https://github.com/evrythng/evrythng.js) is the core version of *evrythng.js* intended to be used in 
public applications and/or devices.

#### evrythng-scan.js

[`evrythng-scan.js`](https://github.com/evrythng/evrythng-scan.js) is an *evrythng.js* plugin that lets you identify 
Products and Thngs right from your browser, without using a standalone QR Code scanning app. It also supports 
[Image Recognition](https://dashboard.evrythng.com/developers/quickstart/image-recognition).

#### evrythng-mqtt.js

[`evrythng-mqtt`](https://www.npmjs.com/package/evrythng-mqtt) is an *evrythng.js* plugin for Node.js that adds support
for real-time MQTT methods to any resource.

#### evrythng-hub.js

[`evrythng-hub`](https://github.com/evrythng/evrythng-hub.js) is an *evrythng.js* plugin for both Browser and Node.js that
adds smart routing of local requests when in the context of a Thng-Hub Gateway.

## License

Apache 2.0 License, check `LICENSE.txt`

Copyright (c) EVRYTHNG Ltd.
