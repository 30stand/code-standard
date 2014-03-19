# JavaScript code standard
Work in progress
* TODO:
    * update loop part,
    * update lazy load

## Naming convention:

Constructors: ```CapitalCase```

Constants: ```UPPER_CASE_WITH_UNDERSCORE```

Everything else: ```camelCase```

## Style

1. Indentation: 4 spaces

2. Comments: at least one line of short description is required, more lines or even comments following [JSDoc](http://usejsdoc.org/) rules will be appreciated.

    > Your code should be elegant, self-explanatory, not heavily relied on comments.

2. Curly brackets:
Required after statements such as ... ```if, switch, try, catch``` ... etc.

    > For ```{```, place it at the end of the previous line,
    > NOT the begining of the next line,
    > to avoid wrong semicolon insertion causes misinterpretation of the program.

3. Simecolons:Required.

4. Var: required, declare all variables at the top of each function.
> Always remember that JavaScript does NOT have block scope, only functions have scope.

## Do NOT use ...

No language is perfect, there are something you should avoid ...

1. ```eval()```
2. ```with```
3. ```==```: too many unexpected results, use```===```instead.

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

4. Constructors without protection, which when called without "new", will contaminate other context wherever "this" points to (like "window").

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

5. Reserved words, a common error like this ...

    ```javascript
    { class: 'my-class-name' }
    ```

    "class" is a reserved word, the browsers with ECMAScript 3 standard will throw an error, but not the ones with ECMAScript 5 standard.
    

## Object-oriented (Thanks to Douglas Crockford)

> Every object is linked to a prototype object from which it inherits properties.

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

2. Object Specifiers

    This pattern is identical to pseudoclassical,
    except replace the auguments of constructors with a single object,
    this pattern can take the additional advantage when working with JSON.
    
    ```javascript
    var Mammal = function (obj) {
        this.name = obj.name;
    };
    ```

3. Prototypal

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

4. Functional

    > The functional pattern has a great deal of flexibility. 
    > It requires less effort than the pseudoclassical pattern,
    > and gives us better encapsulation and information hiding and access to super methods.


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

5. Parts

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
    2. manipulate less nodes the better;
        
        > for example, you want to change color of certain `<li>` elements,
        > instead of assign new class names for each `<li>` element,
        > assign a new class name for their parent `<ul>` or `<ol>` element,
        > ```css
        > .navigation-bar .button { color: #000; }
        > .navigation-bar-alternative .button { color: #fff; }
        > ```

        > another example, if you want to show / hide certain elements,
        > try `display: none`, or `visibility: hidden`,
        > instead of insert / remove DOM nodes from the context.

2. Loops

    try `jQuery.each()` or `Dojo.array.forEach()` to loop through arrays,
    not native ECMAScript 5 forEach which has terrible performance at this moment.
    
    > Also you may want to encapsulate `for` when you are coding without framework,
    > the reason behind this is one terrible thing about JavaScript, no block context,
    > ```javascript
    > var index = 0, item;
    > for (index; item = array[index]; index++) { fn(item); ... }
    > ```
    > `index` and `item` here is going to pollute the function context this `for` loop is in,
    > encapsulated functions solves this problem by introducing a lambda function to contain these variables.
    > ```javascript
    > jQuery.each(theArray, function (index, value) { ... });
    > ```
    
3. Go test it!

    When in doubt, [go test it!](http://jsperf.com/)
