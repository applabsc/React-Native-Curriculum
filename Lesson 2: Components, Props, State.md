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

# Exercise
Try this short exercise to solidify your understanding of the concepts covered: https://snack.expo.io/By17ewH8m

## Common Components
### View
Views in React Native are analogous to divs in React and HTML. They are used to group sub-components. They are built upon the native view objects (UIView on iOS and android.view on Android)

Typically you won't pass that many props into Views. The most common prop that you'll pass is the style prop. 

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
### SafeAreaView
The purpose of SafeAreaView is to render content within the safe area boundaries of a device. It is currently only applicable to iOS devices with iOS version 11 or later.

SafeAreaView renders nested content and automatically applies paddings to reflect the portion of the view that is not covered by navigation bars, tab bars, toolbars, and other ancestor views. Moreover, and most importantly, Safe Area's paddings reflect the physical limitation of the screen, such as rounded corners or camera notches (i.e. the sensor housing area on iPhone X).

Usage Example

Simply wrap your top level view with a SafeAreaView with a `flex: 1` style applied to it. 
```
<SafeAreaView style={{flex: 1, backgroundColor: '#fff'}}>
   <View style={{flex: 1}}>
      <Text>Hello World!</Text>
   </View>
</SafeAreaView>
```
