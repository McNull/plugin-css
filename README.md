css
===

JSPM CSS loading plugin

Basic Use
---

```javascript
import './style.css!'
```

Modular CSS Concepts
---

CSS in the dependency tree implies a CSS modularisation where styles can be scoped directly to the render code that they are bundled with.

Just like JS requires, the order of CSS injection can't be guaranteed. The idea here is that whenever there are style overrides, they should be based on using a more specific selector with an extra id or class at the base, and not assuming a CSS load order. Reset and global styles are a repeated dependency of all modular styles that build on top of them.

Builder Support
---

When building with [SystemJS Builder](https://github.com/systemjs/builder), by default CSS will be inlined into the JS bundle and injected on execution.

To alter this behaviour use the SystemJS configuration options:


* `buildCSS`: true / false whether to build CSS or leave them as separate file requests with the plugin running in production. Defaults to true.
* `separateCSS`: true / false whether to build a CSS file at the same output name as the bundle itself to be included with a link tag. Defaults to false.

### Build Example

```javascript
  var builder = require('systemjs-builder');

  // `builder.loadConfig` will load config from a file
  builder.loadConfig('./cfg.js')
  .then(function() {
    // additional config can also be set through `builder.config`
    builder.config({
      baseURL: 'file:' + process.cwd(),
      // buildCSS: false,
      separateCSS: true
    });

    return builder.build('myModule', 'bundle.js');
  });
```

Will generate `bundle.js` containing the JS files and `bundle.css` containing the compressed CSS for the bundle.
