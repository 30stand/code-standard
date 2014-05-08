# JavaScript code standard

Work in progress

Todo:

1. ~~Add references~~
1. ~~no Parentheses for `typeof`~~
1. space requirements
1. more info about `eval()`, also the correct syntax for `setTimeout` / `setInterval` (sure add a new section about security)
1. ~~Best practice: how to check undefined variables~~
1. ~~Best practice: how to bind `this`~~
1. ~~Best practice: Use Array and Object literals instead of Array and Object constructors.~~
1. Performance part: `array.join()` or string concatenation
1. Performance part: `a.b = null;` or `delete b;`
1. ~~Rewrite OO part, only need private variables and prototype~~
1. Unit tests: checkout DOH & qUnit
1. Checkout MDN for js part

## Naming convention:

1.  Constructors: ```CapitalCase```

1.  Constants: ```UPPER_CASE_WITH_UNDERSCORE```

1.  Everything else: ```camelCase```


## Style

1. Indentation

    4 spaces

1. Semicolons

    Required.

1. Parentheses

    Use it only when it's required by the syntax and semantics, operators like `typeof`, `instanceof`, `new` does not require parentheses to work.

    ```javascript
    typeof 'undefined' === 'string';
    ```

1. Curly brackets

    Required after statements such as ... ```if, switch, try, catch``` ... etc.

    For ```{```, place it at the end of the previous line, NOT the begining of the next line, to avoid wrong semicolon insertion causes misinterpretation of the program.

    ```javascript
    if ( ... ) {
        // do something;
    }
    ```

1. `var`

    Required, declare all variables at the top of each function.

1. Literals

    Use object literals, array literals, instead of calling the constructors.

    ```javascript
    var newObj = {}; // preferred
    var newObj = new Object(); // avoid

    var newArray = []; // preferred
    var newArray = new Array(); // avoid
    ```

1. Quotes

    `'` is preferred over `"`


## Comments

At least one line of short description is required for functions and methods.

Comments following [JSDoc](http://usejsdoc.org/) rules will be appreciated.

    /**
     * Represents a book.
     * @constructor
     * @param {string} title - The title of the book.
     * @param {string} author - The author of the book.
     */
    function Book(title, author) {
    }

In the meanwhile, your code should be elegant, self-explanatory, not heavily relied on comments.


## Awful parts to avoid

No language is perfect, there are something you should avoid ...

1. `eval()`

    Reasons:
    1. Improper use of `eval()` makes your webpage an easy target for XSS attack.
    1. Reduces code performance and readability, also it's harder to debug.

1. `==`

    Leads to too many unexpected results, use```===```instead.

    ```javascript
    '' == '0' // false
    0 == '' // true
    0 == '0' // true
    false == 'false' // false
    false == '0' // true
    false == undefined // false
    false == null // false
    null == undefined // true
    ' \t\r\n ' == 0 // true
    ```


1. Reserved words

    A common error like this,

    ```javascript
    { class: 'my-class-name' }
    ```

    "class" is a reserved word, the browsers with ECMAScript 3 standard will throw an error, but not the ones with ECMAScript 5 standard.

1. `with`

    Use variables to cache objects then access it, instead of using this syntax.


## Performance

1. DOM manipulation

    1. use `className` to apply styles instead of inline style rules.

    1. manipulate less nodes the better.

        for example, you want to change color of certain `<li>` elements,
        instead of assign new class names for each `<li>` element,
        assign a new class name for their parent `<ul>` or `<ol>` element,

        ```css
        .navigation-bar .button { color: #000; }
        .navigation-bar-alternative .button { color: #fff; }
        ```

        another example, if you want to show / hide certain elements,
        try `display: none`, or `visibility: hidden`,
        instead of insert / remove DOM nodes from the context.

1. Loops

    try encapsulated functions like `jQuery.each()` or `Dojo.array.forEach()` to loop through arrays, not native ECMAScript 5 forEach which has terrible performance at this moment, also have compatibility issues in old browsers.

    Also you may want to encapsulate `for` when you are coding without framework, one good reason is to avoid contaminating function variables.

    ```javascript
    var index = 0, item;
    for (index; item = array[index]; index++) { fn(item); ... }
    ```

    `index` and `item` here is going to pollute the function context this `for` loop is in,

    encapsulated functions solves this problem by introducing a lambda function to contain these variables.

    ```javascript
    jQuery.each(theArray, function (index, value) { ... });
    ```

    One way to build your own function to loop through both array & object if you are not using any framework.

    ```javascript
    // "return false" to break the loop
    function each(obj, callback, scope) {
        function isArraylike(obj) {
            return Object.prototype.toString.call(obj) === '[object Array]';
        }

        var
        value,
        i,
        length = obj.length,
        isArray = isArraylike(obj);

        if (isArray) {
            for (i = 0; i < length; i++) {
                value = callback.call(scope || obj[i], obj[i], i);
                if (value === false) {
                    break;
                }
            }
        } else {
            for (i in obj) {
                if (obj.hasOwnProperty(i)) {
                    callback.call(scope || obj[i], obj[i], i);
                    if (value === false) {
                        break;
                    }
                }
            }
        }
    }
    ```

1. Go test it!

    When in doubt, try to create a test case here: [jsperf](http://jsperf.com/)


## Best practices

### Constructors

Constructors without protection, which when called without `new`, it will contaminate outer context wherever "this" points to (most likely to be "window").

    function Person(name) {
        // return a new instance when
        // "this" is not pointed to the right place
        if(!(this instanceof Person)) {
            return new Person();
        }
        this.name = name;
    }

### Lazy load

A very useful technique for feature detections, the following sample code detects `window.addEventListener`, if not, then fall back to `window.attachEvent`.

    var addHandler = (function () {

        if (typeof addEventListener !== 'undefined') {
            return function (el, type, handler) {
                el.addEventListener(type, handler, false);
            };
        } else if (typeof attachEvent !== 'undefined') {
            return function (el, type, handler) {
                el.attachEvent('on' + type, handler);
            };
        }

    }());


### Private variables

We need private variables to protect variables from malicious meddling, to make variables private, we need the help with function scope and closure.

    // a getter & setter example
    function privateVar() {
        var x;

        return {
            get: function () {
                return x;
            },
            set: function (val) {
                x = val;
            }
        };
    }
    var apiAddr = privateVar();
    setApiAddr = apiAddr.set;
    getApiAddr = apiAddr.get;

Another example to use this technique to build Classes.

    var mammal = function (privateObj, parentObj) {

        // inherits with prototypal pattern
        var newObj = (function () {
            var F = function () {};
            F.prototype = parentObj || {};
            return new F();
        }());

        // getters to access private properties
        newObj.getName = function ( ) {
            return privateObj.name;
        };
        newObj.says = function ( ) {
            return privateObj.saying || '';
        };

        return newObj;
    };

    var myMammal = mammal({name: 'Herb'});

### Check variable types

1. `undefined`

    The safest way is to do it with the help of `typeof`

    ```javascript
    // notice only "x" is declared
    var x;

    typeof x === 'undefined' // true
    typeof y === 'undefined' // true

    x === undefined // true
    y === undefined // ReferenceError: y is not defined
    ```

2. `NaN`

    ```javascript
    isNaN( ... );
    ```


### Bind `this`

To avoid mis-reference when using `this`, it's best to cache is with another variable before referencing it, like binding events to DOM objects.

    var initDOM = {
        // ...
        bindEvent: function () {
            var self = this;
            this.domNode.addEventListener('click', function () {
                // self is referencing "initDOM"
                self.popUp();
            });
        },
        // ...
    }


## References

1. [JavaScript: The Good Parts](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742)
1. [Professional JavaScript for Web Developers](http://www.amazon.com/Professional-JavaScript-Developers-Nicholas-Zakas/dp/1118026691)
1. [Google JavaScript Style Guide](https://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml#Parentheses)
