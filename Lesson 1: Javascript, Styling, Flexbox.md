# Lesson 1: Javascript Crash Course, Styling and Flexbox

This section serves as an intro to the Javascript language, ES6 and JSX. If you're familiar with any of those three topics feel free to skip to the second part of this lesson on Styling.

## Javascript
We're only covering the core concepts in Javascript required for React Native development here, so if you're a complete beginner in Javascript, the links below are worth checking out.
-   See here for a good introduction to the language: https://www.learn-js.org 
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

## Styling

With React Native, we use Javascript to style our components. No need to deal with stylesheets unlike in web development. 

However, if you do have a web background, styling in React Native will be familiar to CSS, but with the main difference being style names are written with camel case rather than slashes. E.g. React Native uses `backgroundColor` instead of `background-color`. In addition, in React Native the values of the `style` object have to be strings.

All of the core React Native components accept a `style` prop. To see what style props are supported by each component, check the component's documentation page on the [React Native Documentation](http://facebook.github.io/react-native/docs/getting-started)

One way of declaring the style of a component is by passing an object to the component's `style` prop, as shown below.
```
export default class App extends React.Component {
  render() {
    return (
      <View style={{backgroundColor: 'green'}}/>
    );
  }
}
```
Another way to style components is to define the style object in `StyleSheet.create()` . Both methods are equivalent, but this method this is helpful for organizing code when projects grow in size. See below for an example of how to do use `StyleSheet.create()`.

```
export default class App extends React.Component {
 render() {
   return (
     <View style={styles.viewStyle}/>
   );
 }
}

const styles = StyleSheet.create({
  viewStyle: {
    backgroundColor: 'green',
  }
})
```

-   Note that `styles` is defined outside the component, not inside the component class. 
-   A common mistake is to forget the key when defining the stylesheet. For example the following code would not compile because all styles must have a key

```
// WRONG
const styles = StyleSheet.create({
  flex: 1,
  backgroundColor: 'blue',
}): 

// 😎
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: 'blue',
  }
}): 
```

You can also pass an array of styles to the `styles` prop. The last style in the array has precedence, so you can use this to inherit styles.

```
<View style={[
  {backgroundColor: 'blue'},
  {backgroundColor: 'pink'},
]}/>
```

The background color of the view declared above will be pink as the last declared style takes precedence.


### Styling Exercise

Before we continue, style the button component in the Snack https://snack.expo.io/BJFFxNFUX so that it looks like the image below

![](https://storage.googleapis.com/slite-api-files-production/files/e7ec6ee5-a63f-41c8-8237-f52391e83b12/image.png)

Hint: to style the button, the `backgroundColor`, `padding` and `borderRadius` props will be useful.

## Flexbox
Flexbox comes from CSS, and is a way of creating responsive layouts with React Native. When styling your app, it's pretty much required to use flexbox to make your app responsive and adaptable to different screen sizes. Below are the details about all the different flex properties you can set. 

We distinguish between parent and children container properties in the next section. 

![](https://storage.googleapis.com/slite-api-files-production/files/2f6fb354-cccd-4364-a0f8-6b1fb8e16f49/flexbox.png)

### Parent Container Properties

#### Flex Direction
```
flexDirection: 'row' | 'row-reverse' |
               'column' | 'column-reverse' 
```
Flex direction establishes the main-axis, thus defining the direction flex items are placed in the flex container. If the blue views were defined in the view from lighest to darkest, the following would be the appearance on screen for different flex values. 

`flexDirection: 'row'`

![](https://storage.googleapis.com/slite-api-files-production/files/40d07d8a-7553-418d-8f2d-15c51a3eec59/Screen%2520Shot%25202018-08-21%2520at%252012.46.59%2520PM.png)

`flexDirection: 'column'` 

![](https://storage.googleapis.com/slite-api-files-production/files/de0f1782-298f-40f2-95d9-2127763d10e2/Screen%2520Shot%25202018-08-21%2520at%252012.47.15%2520PM.png)

#### Justify Content
```
justifyContent: 'flex-start' | 'flex-end' |
                'center' | 'space-between' |
                'space-around' | 'space-evenly' 
```
![](https://storage.googleapis.com/slite-api-files-production/files/ab7cc1c6-2b0d-4fb8-9ac2-48e09134a812/image.png)

Difference between space around and space evenly:

-   In space evenly, there is an equal length between child components. 
-   In space around, there is the same amount of **buffer** around each element. Visually the spaces aren't equal, since all the items have equal space on both sides.

#### Align Items
```
alignItems:  'flex-start' | 'flex-end' |
             'center' | 'stretch' |
```
![](https://storage.googleapis.com/slite-api-files-production/files/edce852f-7e52-4d67-b15b-a7358659a347/image.png)

#### Align Content
```
alignContent: 'flex-start' | 'flex-end' |
               'center' | 'stretch' |
               'space-between' | 'space-around' 
```
![](https://storage.googleapis.com/slite-api-files-production/files/0851580f-928d-45dd-b1a2-706ff915797e/alignContent.png)

`alignContent` controls how rows align in the cross direction. (if the main direction were `row`, the cross direction would be `column`).

**Side Note**: A common error when you don't see children component displaying is not setting `{flex: 1}` in the parent's style prop. Setting the flex will enable the parent to take up all the available space. 

### Child Container Properties

#### Flex
Flex is a number, and can either be positive, negative or 0.

-   When flex is positive, it determines the amount of space the component proportional to other components, based on the flex number. For example, a view with `flex: 3` will take up 3 times the space as a view with `flex: 1` with the same parent view.
-   When flex is 0, the component is sized according to `width` and `height` and it is inflexible.
-   When `flex` is -1, the component is normally sized according to `width` and `height`. However, if there's not enough space, the component will shrink to its `minWidth` and `minHeight`.

#### Align Self
```
alignSelf: 'auto' | 'flex-start' |
           'flex-end' | 'center' | 
           'stretch' | 'baseline'
```

![](https://storage.googleapis.com/slite-api-files-production/files/b9dff3c6-1060-4896-9b99-d4f9cc16243a/alignSelf.png)

`alignSelf` controls how a child aligns in the cross direction, overriding the `alignItems` of the parent.

### Additional Child Container Properties

If you look on the [React Native layout documentation](https://facebook.github.io/react-native/docs/layout-props#flexgrow), you'll find more flex props, and a quick overview of these props are given below. Note that even developing production apps using React Native, I've never had to use these props, so don't worry too much about them right now as you're starting off.

-   `flexGrow` and `flexShrink` behave pretty much the same as `flex`, so you'll probably won't have a use for those props
-   `flexBasis` takes one of two values: `0` or `'auto'`. If set to `0`, the extra space around content isn't factored in. If set to `auto`, the extra space is distributed based on its `flex` value. See the image below:

![](https://storage.googleapis.com/slite-api-files-production/files/8eae5961-b94e-46fb-86e2-8ebaf1b8b904/Screen%2520Shot%25202018-08-23%2520at%252011.01.08%2520PM.png)

