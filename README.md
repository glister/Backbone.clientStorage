# Backbone clientStorage Adapter v0.0.1

A fork from [Backbone.localStorage](https://github.com/jeromegn/Backbone.localStorage) which removes the direct dependancy on HTML5 localStorage, allowing 
use of any storage mechanism which uses the same interface as HTML5 localStorage such as sessionStorage or [cookieStorage](https://gist.github.com/remy/350433)

## Usage

Include Backbone.clientStorage after having included Backbone.js:

```html
<script type="text/javascript" src="backbone.js"></script>
<script type="text/javascript" src="backbone.localStorage.js"></script>
```

Create your Backbone collections like so for localStorage:

```javascript
window.PersistentCollection = Backbone.Collection.extend({
  
  localStorage: new Backbone.ClientStorage("My.Persistent.Collection", window.localStorage), // Unique name within your app. localStorage specified as persistence mechanism
  
  // ... everything else is normal.
  
});
```

or like so for sessionStorage

```javascript
window.SessionedCollection = Backbone.Collection.extend({

	localStorage: new Backbone.ClientStorage("My.Sessioned.Collection", window.sessionStorage), // Unique name within your app, sessionStorage specified as persistence mechanism

	// ... everything else is normal

});
```

or you can use constructor parameters to push control of the storage mechanism futher up to a composition root.

```javascript

window.Collection = Backbone.Collection.extend({

	constructor: function (storage, models, options) {
        this.localStorage = new Backbone.ClientStorage("My.Collection", storage);
        Backbone.Collection.call(this, models, options);
    }

	// ... everything else is normal

});

var myCollection = new Collection(window.localStorage); // Collection using localStorage
```


### RequireJS

Include [RequireJS](http://requirejs.org):

```html
<script type="text/javascript" src="lib/require.js"></script>
```

RequireJS config: 
```javascript
require.config({
    paths: {
        jquery: "lib/jquery",
        underscore: "lib/underscore",
        backbone: "lib/backbone",
        localstorage: "lib/backbone.localStorage"
    }
});
```

Define your collection as a module:
```javascript
define("someCollection", ["localstorage"], function() {
    var SomeCollection = Backbone.Collection.extend({
        localStorage: new Backbone.LocalStorage("SomeCollection") // Unique name within your app.
    });
  
    return new SomeCollection();
});
```

Require your collection:
```javascript
require(["someCollection"], function(someCollection) {
  // ready to use someCollection
});
```

### CommonJS

If you're using [browserify](https://github.com/substack/node-browserify).

```javascript
var Backbone.LocalStorage = require("backbone.localstorage");
```

## Contributing

You'll need node and to `npm install` before being able to run the minification script.

1. Fork;
2. Write code, with tests;
4. `make test` or `open spec/runner.html`;
6. Create a pull request.

Have fun!

## Acknowledgments

- [Mark Woodall](https://github.com/llad): initial tests (now refactored);
- [Martin Häcker](https://github.com/dwt): many fixes and the test isolation.

## License

Licensed under MIT license

Copyright (c) 2010 Jerome Gravel-Niquet

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
