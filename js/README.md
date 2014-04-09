# JavaScript code standard

TODO:

1.  add lazy load

1.  add feature detection


## Naming convention:

1.  Constructors: ```CapitalCase```

1.  Constants: ```UPPER_CASE_WITH_UNDERSCORE```

1.  Everything else: ```camelCase```


## Style

1. Indentation:

    4 spaces

1. Comments:  

    At least one line of short description is required for functions and methods, more lines or even comments following [JSDoc](http://usejsdoc.org/) rules will be appreciated.

    In the meanwhile, your code should be elegant, self-explanatory, not heavily relied on comments.

1. Curly brackets:  

    Required after statements such as ... ```if, switch, try, catch``` ... etc.

    For ```{```, place it at the end of the previous line, NOT the begining of the next line, to avoid wrong semicolon insertion causes misinterpretation of the program.

1. Simecolons:

    Required.

1. `var`:

    Required, declare all variables at the top of each function.

    Always remember that JavaScript does NOT have block scope, only functions have scope.


## Do NOT use ...

No language is perfect, there are something you should avoid ...

1. ```eval( ... )```:

    Improper use of eval makes your webpage an easy target for XSS attack.

1. ```==```: too many unexpected results, use```===```instead.

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

1. Constructors without protection, which when called without "new", will contaminate other context wherever "this" points to (like "window").

    ```javascript
    function Person(name) {
        // return a new instance when
        // "this" is not pointed to the right place
        if(!(this instanceof Person)) {
            return new Person();
        }
        this.name = name;
    }
    ```

1. Reserved words, a common error like this ...

    ```javascript
    { class: 'my-class-name' }
    ```

    "class" is a reserved word, the browsers with ECMAScript 3 standard will throw an error, but not the ones with ECMAScript 5 standard.
    

## Inheritance

1. Pseudoclassical

    ```javascript
    var Mammal = function (name) {
        this.name = name;
    };
    Mammal.prototype.getName = function ( ) {
        return this.name;
    };
    Mammal.prototype.says = function ( ) {
        return this.saying || '';
    };
    var myMammal = new Mammal('Herb the Mammal');
    var Cat = function (name) {
        this.name = name;
        this.saying = 'meow';
    };
    // Replace Cat.prototype with a new instance of Mammal
    Cat.prototype = new Mammal( );
    ```

1. Object Specifiers

    This pattern is identical to pseudoclassical,
    except replace the auguments of constructors with a single object,
    this pattern can take the additional advantage when working with JSON.
    
    ```javascript
    var Mammal = function (obj) {
        this.name = obj.name;
    };
    ```

1. Prototypal

    Instead of the prototype chain between constructors,
    we build upon an existing object, then customize it.
    
    ```javascript
    var myMammal = {
        name : 'Herb the Mammal',
        getName : function ( ) {
            return this.name;
        },
        says : function ( ) {
            return this.saying || '';
        }
    };
    var myCat = (function () {
        var F = function () {};
        F.prototype = myMammal;
        return new F();
    }());
    myCat.name = 'Henrietta';
    ```

1. Functional

    The functional pattern has a great deal of flexibility. 
    It requires less effort than the pseudoclassical pattern,
    and gives us better encapsulation and information hiding and access to super methods.

    ```javascript
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
    ```

1. Parts

    Make objects out of parts.
    
    ```javascript
    var addParts = function (privateObj, obj) {
        obj.getName = function () { return privateObj.name };
        return obj;
    };

    addParts({ ... });
    ```

## Performance

1. DOM manipulation

    1. use `className` to apply styles instead of inline style rules;
    1. manipulate less nodes the better;
        
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
