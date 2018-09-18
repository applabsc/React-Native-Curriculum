# Lesson 2: Components, Props, State

## Components

A component is pretty much any part of a UI in a React Native app. They can be built in components such as `TextInput` and `View`, or they can be custom components built out of other components.

For example, in the screen below, taken from a React Native app, the Jetty quote (highlighted in dark blue) is a component, which is made out of several sub-components (highlighted in light blue). The subcomponents (in order from left to right are an `Image` component showing the logo, a `Text` component showing the price and an `Icon` component showing the disclosure indicator.

![](https://storage.googleapis.com/slite-api-files-production/files/d2f102fe-9a12-47d6-b502-5ec5f612b9f3/image.png)

The standard way to create a component is to define a class. For the class to be a component, it should extend from `React.Component`.

Components only have a single required method, the `render` method. As a example, see below for a simple component definition

```
class HelloWorld extends React.Component {
   render() {
      return (
         <Text>
            Hello, {this.props.name}
         </Text>
      );
   }
}
```
We should note that the `render` method can return only a single element. For example, the render method could not be like this:
```
render() {
   return (
      // WRONG
      <Text>
         Hello, {this.props.name}
      </Text>

      // Because it returns two text components
      <Text>
         Also, hello, {this.props.name}
      </Text>
   );
}
```
If you need to return multiple elements, wrap them in a `<View>` element

If you're coming from a React background, note that `Views` are comparable to `divs` in React.

## Props

A component accepts props (short for properties), which are passed to them by a parent component. These props are used for component configuration.

However, `props` must **not be altered** from within the component's methods.

A parent element may alter a child element's `props` at any time. The child element will call its `render` method upon receinving the new peops and re-render itself to reflect its new configuration parameters. 

As an example, a parent component can declare a child image component by including  `<Image source={require('./jetty-icon.png')}/>`, in its `render` method. `source` is a prop  indicating the source of the image. However, the image component cannot modify image if the image URL/source changes. Only the parent component is allowed to do that.

This is an important paradigm in React and React Native. Data generally flows from top to bottom, meaning parent components pass data to child components and not the other way around.

A child component may decide not to re-render itself even though its configuration has changed, as determined by `shouldComponentUpdate()` (we will talk more about this in when discussing Component Lifecycles).

## State

Each component has state, which describes the current state of the component. E.g. example state properties include 'selected' or 'currentPage'. The initial state is by setting `this.state` in the constructor of a component.

However, if you're setting the component state anywhere other than the constructor, you must call the method `this.setState()`, which takes a object with the updated state parameters.

For example, if you want to set the state property `selected` of a button component to `true`, you would invoke the following code:
```
this.setState({
   selected: true
})
```
Unlike `props`, parent elements may not access a child's `state`, as it is intended to manage the child's internal state rather than external configuration.

TL;DR: components accept props, which are immultable and have state, which are mutable.

## Exercise
Try this short exercise to solidify your understanding of the concepts covered: https://snack.expo.io/By17ewH8m


