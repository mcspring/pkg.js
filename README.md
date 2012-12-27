## What's pkg.js?
pkg.js is a micro javascript lazy-loader and lib-dependence

- forked from [load.js](https://github.com/chriso/load.js)
- built on top of [chain.js](https://github.com/chriso/chain.js)

It allows you to lazy load your scripts sequentially or in parallel and handle complex dependency chains.

I added new `rely` helper on resolving load the same javascript frameworks multiple, such like *jQuery*, *mootools*, *Extjs*, etc.

Also, I renamed the `load` method to `require` for personal angle.

## Example of `require`
```javascript
require('jquery.js')
.then('jquery-ui.js')
.then('myscript.js')
.thenRun(function () {
    alert(typeof jQuery);
});

require('underscore.js')
.thenRun(function () {
  alert(typeof _);
});
```

**Some things to note:**

- `then()` is an alias for the previous method in the chain.
- once *jQuery* has loaded, *jquery-ui.js* is loaded in parallel. When both are complete, *myscript.js* is loaded.
- each chain is separate, so *underscore* and *jQuery* will load in parallel.

## Example of `rely`
```javascript
rely('jQuery', 'jquery.js')
.then('jQuery.ui', 'jquery-ui.js')
.then('MyQuery', 'myscript.js')
.thenRun(function () {
    alert(typeof jQuery);
});

rely('_', 'underscore.js')
.thenRun(function () {
  alert(typeof _)
});
```

**Other things to note:**

- the first argument of `rely` is the name of the object which use for judging whether to load the file of the second or not
- `rely` just use `eval('typeof ' + arguments[0])` for verdict, if the value returned is *undefined* then load the dependence file

## Example of `defer`
```javascript
// Load a script after a 0.5s delay
defer(500).thenRequire('jquery.js');

defer(500).thenRely('jQuery', 'jquery.js');
```

## Example of `onError`
```javascript
require('jquery.js').onError(function (err) {
    //Handle any errors here..
});

rely('jQuery', 'jquery.js').onError(function (err) {
    //Handle any errors here..
});
```

> For more examples of the available methods, see the [chain.js](https://github.com/chriso/chain.js) page

## Contributors
[Spring MC](http://mcspring.apisocial.com)

## License
(MIT License)

Copyright (c) 2010 Spring Mc <Heresy.Mc@gmail.com>

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
