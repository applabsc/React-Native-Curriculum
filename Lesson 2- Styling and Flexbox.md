# Styling

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


## Styling Exercise

Before we continue, style the button component in the Snack

https://snack.expo.io/BJFFxNFUX so that it looks like the image below


![](https://storage.googleapis.com/slite-api-files-production/files/e7ec6ee5-a63f-41c8-8237-f52391e83b12/image.png)

Hint: to style the button, the `backgroundColor`, `padding` and `borderRadius` props will be useful.

# Flexbox
Flexbox comes from CSS, and is a way of creating responsive layouts with React Native. When styling your app, it's pretty much required to use flexbox to make your app responsive and adaptable to different screen sizes. Below are the details about all the different flex properties you can set. 

We distinguish between parent and children container properties in the next section. 

![](https://storage.googleapis.com/slite-api-files-production/files/2f6fb354-cccd-4364-a0f8-6b1fb8e16f49/flexbox.png)

## Parent Container Properties

Flex Direction
```
flexDirection: 'row' | 'row-reverse' |
               'column' | 'column-reverse' 
```
Flex direction establishes the main-axis, thus defining the direction flex items are placed in the flex container. If the blue views were defined in the view from lighest to darkest, the following would be the appearance on screen for different flex values. 

`flexDirection: 'row'`

![](https://storage.googleapis.com/slite-api-files-production/files/40d07d8a-7553-418d-8f2d-15c51a3eec59/Screen%2520Shot%25202018-08-21%2520at%252012.46.59%2520PM.png)

`flexDirection: 'column'` 

![](https://storage.googleapis.com/slite-api-files-production/files/de0f1782-298f-40f2-95d9-2127763d10e2/Screen%2520Shot%25202018-08-21%2520at%252012.47.15%2520PM.png)

Justify Content
```
justifyContent: 'flex-start' | 'flex-end' |
                'center' | 'space-between' |
                'space-around' | 'space-evenly' 
```
![](https://storage.googleapis.com/slite-api-files-production/files/ab7cc1c6-2b0d-4fb8-9ac2-48e09134a812/image.png)

Difference between space around and space evenly:

-   In space evenly, there is an equal length between child components. 
-   In space around, there is the same amount of **buffer** around each element. Visually the spaces aren't equal, since all the items have equal space on both sides.

Align Items
```
alignItems:  'flex-start' | 'flex-end' |
             'center' | 'stretch' |
```
![](https://storage.googleapis.com/slite-api-files-production/files/edce852f-7e52-4d67-b15b-a7358659a347/image.png)

Align Content
```
alignContent: 'flex-start' | 'flex-end' |
               'center' | 'stretch' |
               'space-between' | 'space-around' 
```
![](https://storage.googleapis.com/slite-api-files-production/files/0851580f-928d-45dd-b1a2-706ff915797e/alignContent.png)

`alignContent` controls how rows align in the cross direction. (if the main direction were `row`, the cross direction would be `column`).

**Side Note**: A common error when you don't see children component displaying is not setting `{flex: 1}` in the parent's style prop. Setting the flex will enable the parent to take up all the available space. 

## Child Container Properties

### Flex
Flex is a number, and can either be positive, negative or 0.

-   When flex is positive, it determines the amount of space the component proportional to other components, based on the flex number. For example, a view with `flex: 3` will take up 3 times the space as a view with `flex: 1` with the same parent view.
-   When flex is 0, the component is sized according to `width` and `height` and it is inflexible.
-   When `flex` is -1, the component is normally sized according to `width` and `height`. However, if there's not enough space, the component will shrink to its `minWidth` and `minHeight`.

### Align Self
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
