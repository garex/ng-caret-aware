Caret aware inputs
==================

[![Bower](https://img.shields.io/bower/v/ng-caret-aware.svg?style=flat-square)](http://bower.io/search/?q=ng-caret-aware) [![Codeship](https://img.shields.io/codeship/440cb4a0-d558-0132-89dc-4aea429a9964/master.svg?style=flat-square)]() [![Coveralls branch](https://img.shields.io/coveralls/leodido/ng-caret-aware/master.svg?style=flat-square)](https://coveralls.io/r/leodido/ng-caret-aware?branch=master)

**AngularJS directive for caret aware elements**.

Put it on your HTML elements (inputs or textareas, for now) and it will **track the caret** (i.e. cursor) exporting its **position** in a variable (named after the value assigned to the directive attribute) appended to the parent scope.

Moreover, it will expose an **API** (via its **controller**) to read and write caret position.

Caret aware directive is designed to be **cross-browser**.

Weight: < 2KB.

See input demo live [here](http://bit.ly/input-ng-caret) or textarea demo live [here](http://bit.ly/textarea-ng-caret).

#### Releases

Latest release files are in the [dist](dist/) directory of this repository.

#### Note

At the moment this directive can be used as attribute or as comment.

Usage
-----

Include AngularJS, and the build you desire (e.g., [dist/caretaware.min.js](dist/caretaware.min.js)).
 
Then load the **leodido.caretAware** AngularJS module. E.g.,

```javascript
var app = angular.module('myAwesomeModule', ['leodido.caretAware']);
```

Instantiate the directive.

```html
<input type="text" name="myname" caret-aware="cursor"/>
```

And the parent scope of this element will contain a **cursor** variable - e.g., `$scope.cursor` - tracking the caret position of your element's content.

Alternatively you can simply instantiate it this way:

```html
<input type="text" name="myname" caret-aware/>
```

In such case the parent scope will contain a **caret** variable - e.g., `$scope.caret` - tracking the caret position of your input element.

### Controller usage

- Want to use this directive APIs/controller?

See [example](/example) directory for further details. For example [here](example/input01.html#L39-L40).

- Want to use this directive APIs in your **custom directive**?

Simply require it. E.g.,

```javascript
var a = angular.module('demo', []);
a.directive('test', function() {
  return {
      restrict: 'A',
      require: ['caretAware'],
      // ...
      link: function(scope, iElem, iAttrs, caretAwareController) {
        // caretAwareController.setPosition(1);
        // ...
      }
  }
});
```

APIs
----

This is the public API to **manipulate and retrieve the caret position**.

```
/**
 * Retrieve the namespace of the directive instance
 *
 * @return {!string}
 */
caretAwareController.getNamespace()
/**
 * Retrieve the element caret position
 *
 * @return {!number}
 */
caretAwareController.getPosition()
/**
 * Manually set the element caret position and the scope caret variable
 *
 * @param {!number} pos
 * @return {!leodido.controller.Caret}
 * @throws TypeError
 */
caretAwareController.setPosition(pos)
/**
 * Retrive information about the current selection
 *
 * @return {{start: !number, end: !number, length: !number, text: !string}}
 */
caretAwareController.getSelection()
/**
 * Replace text of current selection
 *
 * @param {!string} text
 * @return {!leodido.controller.Caret}
 */
caretAwareController.setSelectionText(text)
```

#### Note

1. the scope caret variable value - i.e., `$scope.caret` - is asynchronously bound to the actual element caret position,
   so during the digest cycle the `getPosition()` could not reflect the scope caret variable value
   
2. in some browser (e.g., Chrome 42.0.2331) can happen that `setPosition()` will not be instantly applied, so the `getPosition()` could return the previous value;
   see this [issue](https://code.google.com/p/chromium/issues/detail?id=32865).

Installation
------------

Install it via `bower`.

```
bower install ng-caret-aware
```

Or, you can clone this repo and install it locally (you will need `npm`, of course).

```
$ git clone git@github.com:leodido/ng-caret-aware.git
$ cd ng-caret-aware/
$ npm install
```

Distribution
------------

In the **dist** directory you can find both development and production ready library files:

1. [dev.caretaware.min.js](dist/dev.caretaware.min.js) and its sourcemap (i.e., [dev.caretaware.min.js.map](dist/dev.caretaware.min.js.map) file) can be used for development purposes

2. [caretaware.min.js](dist/caretaware.min.js) is the production version of this AngularJS module

Build
-----

Build is handled through [Gulp](https://github.com/gulpjs/gulp/) and performed mainly via [Google Closure Compiler](https://github.com/google/closure-compiler).

Need help? Run `gulp help`!

```
# Usage
#   gulp [task]
# 
# Available tasks
#   build                                  Build the library 
#    --banner                              Prepend banner to the built file
#    --env=production|development          Kind of build to perform, defaults to production
#  bump                                    Bump version up for a new release 
#   --level=major|minor|patch|prerelease   Version level to increment
#   clean                                  Clean build directory
#   help                                   Display this help text
#   lint                                   Lint JS source files
#   protractor                             Run protractor E2E tests
#   version                                Print the library version
```

Tests
-----

This library has been unit tested for Chrome and Firefox.

At the moment coverage is almost complete.

Furthermore E2E tests are provided for Chrome and Firefox, too.

See [test](test) directory for details.

Aknowledgements
---------------

* Thanks to [@leogr](http://github.com/leogr) for his suggestions, and improvements. Particularly for his help fixing issue [#14](https://github.com/leodido/ng-caret-aware/issues/14).

* Thanks for the inspiration to all authors of snippets (that are present on the web) related to the caret management.

---

[![Analytics](https://ga-beacon.appspot.com/UA-49657176-1/ng-caret-aware)](https://github.com/igrigorik/ga-beacon)
