# Lesson 3: More Components

Components have a lifecycle: they are instantiated, mounted, rendered, and eventually updated, unmounted, and destroyed. The lifecycle also allows you to optionally execute custom code at each step for more fine-grained control of the rendering. 

When you create a class that inherits from `React.Component`, they will have access to all these component methods. However, only one of the methods, the `render` method, is required. The others are optional, meaning that you don't have to include them in the class for your app to run.

## Mounting Cycle

Let's look at each phase of the component lifecycle. The methods here are listed in the order they're called

`constructor(object props)` 

The component class is instantiated. The parameters to the constructor are the element's initial props, as specified by the parent element. You can optionally specify an initial state for the element by assigning an object to `this.state`. At this point, no native UI has been rendered yet for this element.

`render()`

The render method returns a React Element to render (or null, to render nothing).

`componentDidMount()`

This method is invoked only once, after rendering occurs for the first time. At this point, the native UI for this element has finished rendering, and may be accessed through this.refs for direct manipulation. If you need to make async API calls or execute delayed code with setTimeout, that should generally be done in this method.

Updating Cycle

`componentWillReceiveProps(object nextProps)` 

The parent of this component has passed a new set of props. This component will re-render. You may optionally call `this.setState()` to update this component's internal state before the render method is called.

`shouldComponentUpdate(object nextProps, object nextState)` 

Based on the next values of props and state, a component may decide to re-render or not to re-render. The base class's implementation of this method always returns true (the component should re-render). For optimization, override this method and check if either props or state have been modified, e.g. run an equality test of each key/value in these objects. Returning `false` will prevent the render method from being called.

`componentWillUpdate(object nextProps, object nextState)`

This method is invoked, after the decision has been made to re-render. You may not call this.setState() here, since an update is already in progress.

`componentDidUpdate(object prevProps, object prevState)`

This method is invoked after re-rendering occurs. At this point, the native UI for this component has been updated to reflect the React Element returned from the render() method.

### Buttons
This is a basic button, matching the design style of the operating system that it's deployed on (so iOS and Android will look different). It only supports a basic level of customization, so if you want mroe control over the look and feel of the button, considering using a `TouchableOpacity` instead (covered below).

`Button` has these main props

-   `onPress`: accepts a callback that is called whenever the button is pressed
-   `title`: the button text
-   `color`: accepts a string indicating the color of the button (e.g. `#DAC345` or `aquamarine`)
-   `disabled`: accepts a boolean value indicating whether the interactions for the button are disabled or not

```
import { Button } from 'react-native';
...
<Button
   onPress={() => console.log("Button Pressed"}
   title="Learn More"
   color="#841584"
/>
```

## Exercise
**Try this short coding challenge to apply what you've learned about components**
https://snack.expo.io/S1kA86Au7

### Touchable Opacity
Touchable Opacity works similarly to button; it has all the props that button has, but also much more for customizing the specific style and behavior of the button. For a complete reference, see the documentation: https://facebook.github.io/react-native/docs/touchableopacity

### ScrollView
`ScrollView` is used for scrollable content. They're like a view except everything inside the view is scrollable. They can scroll horizontally or vertically. `ScrollViews` They're well suited for scrolling small quantities of content (< 30 items).

### FlatList
Unlike `ScrollView`, `FlatList` doesn't render all of its child content at once. It only renders the list items that show on screen (plus 2-3 immeidately above or under the visible content). So, when you're dealing with a long list, use `FlatList`. The performance of your app will be much better.

Usage example
```
<FlatList
   data={[{key: 'a'}, {key: 'b'}]}
   renderItem={({item}) => <Text>{item.key}</Text>}
/>
```

## Project
