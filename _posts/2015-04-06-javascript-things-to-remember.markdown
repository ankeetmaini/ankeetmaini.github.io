---
title: 'JavaScript: Things to Remember'
layout: post
tags: javascript tutorial
---

# **This is a WIP**. I will update this as I'll read more and find time.

_The content is not my own, but taken from various books, blogs and internet which I do not own. I'll try to add the references some day._

### Character Set ###
- JavaScript programs are written in _Unicode character set_

### Semicolons ###
- Semicolons are optional if line breaks are used after each statement.
- But, JavaScript doesn't treat every line break as a semicolon.
- It only inserts the semi-colon if it can't parse the code without it.

    ```javascript
    var a // perfectly fine
    a // JavaScript puts a semicolon on the above line as it can't parse var a a
    = // continues without semicolon, as a =, makes sense thus far
    3 // continues without semicolon as a = 3 makes sense
    console.log(a) // now it puts the semicolon after 3 and gives the result 3.
    ```
- But if you happen to give line breaks after **return, break or continue**, JavaScript will take that as semicolon and will execute.

    ```javascript
    return
    true
    ```
> This will be interpreted as

    ```javascript
    return;
    true;
    ```
> When you actually meant to say

    ```javascript
    return true;
    ```
- If you cannot use ++, -- operators as postfix if you were to miss the semicolons.
- They are interpreted differently.

    ```javascript
    a
    ++
    b
    ```
> is interpreted as

    ```javascript
    a;
    ++b;
    ```
> when you wanted it to be

    ```javascript
    a++;
    b;
    ```
- I would suggest to end every statement with a semicolon, and keep your linter happy.

### Basic Types ###

There are six basic types of values in JavaScript.

1. Numbers
 * JavaScript uses 64 bits to store a number value.
 * Fractional numbers should be treated as approximations.
 * 0.1 + 0.2 != 0.3 (the result varies from browser to browser)
2. strings
3. Booleans
4. objects
5. functions
6. undefined
 * This is a special value along with *null*
 * Operations which do not produce a meaningful result, produce **undefined**

- Special Cases
 - __Infinity__

    ```javascript
    Infinity + Infinity // -> Infinity
    Infinity - Infinity // -> NaN
    ```

#### Getting to know the type ####

- Using __typeof__

    ```javascript
    var a = 4;
    typeof a // -> "number"

    a = "IronMan";
    typeof a // -> "string"

    a = {};
    typeof a // -> "object"

    a = undefined;
    typeof a // -> "undefined"

    a = null;
    typeof a // -> "object"

    a = [];
    typeof a // -> "object"
    ```
> In _typeof_ both Object, null and Array evaluate to object, which is a little ambiguous.

- Using __Object.prototype.toString__

    ```javascript
    var a = 4;
    Object.prototype.toString.call(a) // -> "[object Number]"

    a = "IronMan";
    Object.prototype.toString.call(a) // -> "[object String]"

    a = {};
    Object.prototype.toString.call(a) // -> "[object Object]"

    a = undefined;
    Object.prototype.toString.call(a) // -> "[object Undefined]"

    a = null;
    Object.prototype.toString.call(a) // -> "[object Null]"

    a = [];
    Object.prototype.toString.call(a) // -> "[object Array]"
    ```
> The second option is a more definitive way to find out the type.

### Operators ###

1. When multiple operators with the same precedence appear together, they're evaluated from __left to right__.
2. There's only one value in JavaScript which is not equal to itself, __NaN__

    ```javascript
    console.log(NaN == NaN); //false
    ```
3. Type Coercion
    > JavaScript automatically converts some values to the type it expects

    ```javascript
    console.log(8 * null)
    // → 0
    console.log("5" - 1)
    // → 4
    console.log("5" + 1)
    // → 51
    console.log("five" * 2)
    // → NaN
    console.log(false == 0)
    // → true
    ```

### Falsy values ###
1. Empty string - ""
2. null
3. undefined
4. 0
5. NaN
6. false

### Closures ###
__TODO__

### Objects ###

#### Creation of Objects ####
1. Object literal way

    ```javascript
    var hero = {
      name: 'Iron Man',
      occupation: 'Adventurer',
      greet: function () {
        return 'I am ' + this.name + '!';
      }
    };
    ```
2. Using __Contructor__ functions

    ```javascript
    function Hero (name) {
      this.name = name;
      this.greet = function () {
        return 'I am ' + this.name + '!';
      };
    // no need of doing return this;
    // new operator automatically returns this
    }

    //using constructor function
    var ironMan = new Hero('Iron Man');
    ironMan.greet(); // I am Iron Man!
    ```
   - But if you forget to use the *new* operator, the above variable _ironMan_ will be initialized with __undefined__. The call to greet() will not work as expected.
   - As we do not return anything from the construction function defined above, had we returned _this_ from the Hero() function in the end, omitting the _new_ operator also would've been fine ;)

### Functions ###
1. Function declaration

    ```javascript
    function hero () {
    // some code
    }
    ```
2. Function expression

    ```javascript
    var hero = function () {  // anonymous
        // some code
    }
    ```
    > always use named function expressions, easier to debug

    ```javascript
    var hero = function hero() {
        // hero() is valid inside the function body
        // else you can use arguments.callee
        // but it is not recommended.
    }
    ```
