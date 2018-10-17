# Lesson 4: Networking
## Promises

Before we cover the networking part, we need to cover promises within Javascript first, as promises are used pretty much any time you need to make an asyncronous operation like a network request. Whenever you make a function call that makes network request or does a slow operation (such as writing to system storage), the function will return a **promise**.

A promise is an object with two main functions that can be called on it: `then()` and `catch()`. `then()` is used to handle the success case, (e.g. when the network call returns successfully), and `catch()` is used to handle the failure case (e.g. when the network call failed for whatever reason).

An example API call and handling of the response is shown below

```
fetch('https://facebook.github.io/react-native/movies.json')
   .then((response) => console.log(response.json())) 
```
       
`fetch('https://facebook.github.io/react-native/movies.json')` returns a promise. We handle the promise and access the return value of the API call by calling the method `then` on that promise. 

`then` takes in a callback, `(response) => console.log(response.json())` which just prints the response as JSON when data is received from the API. 

This callback is executed when the promise is resolved (i.e. the network request successfully returned the data). The response can be accessed via the first argument of the callback that's passed in. In this example, the argument name is `response`, but you can name this variable whatever you want.

However, if the API call fails, the app may throw an error because we haven't handled failure cases. To make our app handle failure cases, we need to call `catch`, which also takes in a callback that is executed ONLY when the request couldn't be successfully completed. The error object, which contains more information about the error can be accessed via the the callback. For example, the callback, `(e) => console.log(e.toString())` prints out the error.

Now our code handles errors!
```
fetch('https://facebook.github.io/react-native/movies.json')    
   .then((response) => console.log(response)) 
   .catch((e) => console.log(e.toString())
```
NOTE: A common mistake is shown below, where we attempt to access `this.response` before it's set. Read the code below, then come back here. When line 4 is reached, Javascript won't wait for the API call to facebook.github.io to end before continuing. It will continue executing, and will reach line 7 far before the API call returns (and `this.response` is set). Hence, when we try to print `this.response` in line 7, it will be `undefined`.
```
1 class Example extends React.Component {
2    onPressButton() {
3       // Call an API to get network data, then store the data in this.response
4       fetch('https://facebook.github.io/react-native/movies.json')
5       .then((response) => this.response = response)
6       // Attempt to access the data and get undefined
7       console.log(this.response)
8 }
```
Here's the key takeaway: the `then()` function also returns a promise by default, that resolves when the callback passed into `then` finishes executing. You can override this behavior and return a promise within the callback. This allows for **promise chaining**, where you can pass promises along from one then block to the next. That way, you can execute code that depends on the result of a previous asyncronous operation to not be executed until the previous operation is complete. See the code block below for an example of how this works.

```
// Call an API that returns a promise
fetch('https://someApiThatReturnsAPromise/')   
   .then((response) => {
      // We return a promise, which passes the result of the promise the next promise block
      return newPromise();
   })
   .then((dataReturnedFromPromise) => {
      // This code won't be executed UNTIL the previous promise finishes executing
      console.log(dataReturnedFromPromise)
   })
```

## Networking
Let's go back to our network request we covered previously. 
```
fetch('https://facebook.github.io/react-native/movies.json')   
   .then((response) => console.log(response)) 
```
If we ran the code, `fetch()` makes a network request to get movie information. When the network call returns data, we get the response as the variable `response` in the callback. However, if we just go ahead and `console.log` the response, we'll get something like what's shown below — not exactly the movie data we're looking for. 
```
[object Response] {
   arrayBuffer: function arrayBuffer() {
      [native code]
},
   blob: function blob() {
      [native code]
 },
   body: [object ReadableStream] { ... },
   bodyUsed: false,
   clone: function clone() {
      [native code]
},
   formData: function formData() {
      [native code]
},
   headers: [object Headers] {
      append: function append() {
         [native code]
},
{...}
   json: function json() {
      [native code]
},
   ok: true,
   redirected: false,
   status: 200,
   statusText: "",
   text: function text() {
      [native code]
},
   type: "cors",
   url: "https://facebook.github.io/react-native/movies.json"
}
```
Fetch will return raw HTTP response. To extract the useful data from it, we will need to convert the response data into JSON format. To do that, Javascript has a `.json()` method you can call on the `response` object to do exactly that. 

However, we can't do something like `responseJson = response.json()`, because `json()` is asyncronous and returns another promise!

This is where we need to use promise chaining. `response.json()` returns a promise, so to get the JSON data from the promise, we need to call `then()` on the promise, and pass in a callback to handle the JSON response. (I know this is super confusing at first, so flag someone down if you don't understand)

As an example, the code below handles the JSON response in lines 5–7, where we print out the JSONed response `jsonResponse`.
```
fetch('https://facebook.github.io/react-native/movies.json')   
   .then((response) => {
     return response.json()
   })
   .then((jsonResponse) => {
      console.log(jsonResponse)
   })
   .catch(error => console.log(error))
```
Now, when we run this code, the response that is printed looks like the following:
```
[object Object] {
   description: "Your app fetched this from a remote endpoint!",
   movies: [[object Object] {
   id: "1",
   releaseYear: "1977",
   title: "Star Wars"
}, [object Object] {
   id: "2",
   releaseYear: "1985",
   title: "Back to the Future"
}, [object Object] {
   id: "3",
   releaseYear: "1999",
   title: "The Matrix"
}, [object Object] {
   id: "4",
   releaseYear: "2010",
   title: "Inception"
}, [object Object] {
   id: "5",
   releaseYear: "2014",
   title: "Interstellar"
}],
   title: "The Basics - Networking"
}
```
And we have the movie data we're looking for

## Exercise: Weather App
For this exercise, we're going to access the [OpenWeatherMap](https://openweathermap.org) API to get real time weather information and display it in our app. Here's the documentation of the API for more info: https://openweathermap.org/current

To get it to work, you'll need to paste an API key in. An API key you can use is `fedc167923fce9420541de468ccc7151`

Navigate to this link to the exercise: https://snack.expo.io/ByGnYbBiX
