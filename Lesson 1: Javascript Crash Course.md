# Lesson 1: Javascript Crash Course.md
This section serves as an intro to the Javascript language, ES6 and JSX. If you're familiar with any of those three topics feel free to skip the respective sections in the guide.

## Javascript

-   If you're a beginner at Javascript, check here for a good introduction to the language: https://www.learn-js.org 
-   For more info, reference the Javascirpt documentation here: https://developer.mozilla.org/en-US/docs/Web/JavaScript

### Javascript Functions

-   One important part of Javascript that differs from other programming languages is that functions are _first class objects_. 
-   This means that functions are objects, and can be passed around, just like any other variable, like a `string`. 
-   The below code shows callback functions in action
    -   The function `callback` is just a regular function that prints something out.
    -   `call` takes in a function as a parameter, and calls the function (note the `()` after `functionToCall`, which indicates we're calling the function)
    -   We're calling `call`, and passing in `callback`, which prints `Callbacks are fun!11!!`

```
function callback() {
   console.log('Callbacks are fun!11!!');
}

function call(functionToCall) {
   functionToCall();
}

// Prints out 'Callbacks are fun!11!!'
call(callback); 
```
## ES6

### Variable Declarations

In Javascript, `var` is used to declare variables. ES6 replaces `var` with `const` and `let`. Variables declared with `const` are immutable. Once their value is set, they can't be changed. Note that if the value assigned to a `const` variable is an object or array, the object or array may still be modified.



### Fat Arrow Functions (=>)

Fat arrow functions are an alternative to using  `function () { ... }`  to declare functions in Javascript.

In fat arrow functions, `this` refers to the same object inside and outside , unlike Javascript function declarations. By default, regular Javascript functions don't bind `this`, so it's up to you to bind `this` if needed. A common error is to use `this` without binding in a regular `function` declaration. In that case you'll receive an "Undefined is not an object" error at runtime.

To bind you need to bind `this` (or another object) to the function by calling `this.printName = this.printName.bind(this)` before using the function in a component.
```
    this.name = "Alice";
    function printName() {
       console.log(this.name)
    }

    const printNameFatArrow = () => {
       console.log(this.name)
    }

    printName() // prints "undefined"
    printNameFatArrow() // prints "Alice"
    this.printName = this.printName.bind(this)
    printName() // prints "Alice"
```
### Function Parameters

The fat arrow function syntax can vary a bit. If the function takes exactly one parameter, the parentheses can be omitted: `x => Math.pow(x, 2)`. Any other number of arguments will need parentheses:`(x, y) => Math.pow(x, y)`. 

If the function body is not wrapped in curly braces (as in the previous sentences), it is executed as an **expression**, and the return value of the function is the value of the expression. In this case, the function body can only be a single statement.

The function body can be wrapped in curly braces to make it a **block**, in which case you will need to explicitly `return` a value, if you want something returned. Blocks can include multuple lines of code, unlike expressions, which makes them more common.

### Imports and Exports

There are two kinds modules that we can import and export: default and regular.

When importing default modules, default exports don't need to have a {} around the component name while regular/named exports do. See line 1 of the code block below for an example. `React` is a default module, but `Component` is a named/regular module.

Additionally, when you import default modules, you can name the module whatever you want in the imported file, but regular modules must retain the same name (they are sometimes called named imports for this reason)

All exported variables need to be prefixed with the keyword `export`. Default exports are indicated by including the keyword `default` in their declaration. The `LoginScreen` declaration in the file below is a default export. 

Meanwhile, regular/named exports just need the export keyword. Note that each Javascript file can only have one default export.
```
import React, {Component} from 'react';

// Default export
export default class LoginScreen extends Component {
   ...
}

// Regular/named export
export function hello() {
   ...
}
```
## JSX

JSX was created to make the JavaScript representation of components easier to understand. It allows us to structure components and show their hierarchy visually in markup.

JSX is an extension to JavaScript that adds a new kind of **expression**. You can use JSX expressions anywhere you could use any other expression.

JSX is a shortcut for using the `React.createElement()` API, that is much more concise, easy to read, and visually looks a little like the generated UI (as both are tree-like). You don't _have to_ use JSX, but there are practically no disadvantages, so you probably should use it.

Each JSX tag, like `<View />`, is transformed into a call to `React.createElement()`. Any attributes become `props` of the instantiated component. Attributes can be strings like `foo='hello'`, or they can be interpolated JavaScript expressions when wrapped in curly braces as in `bar={baz}` (which would refer to the variable baz).

Tags can be self-closing, like `<View />`, or they can include both an opening and closing tag, like `<View></View>`. To include children elements, you will need to use an opening and closing tag and put the children tags within.
