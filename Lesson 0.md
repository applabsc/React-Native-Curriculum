# Administrivia

-   Bookmark our Github org: https://github.com/applabsc. It contains starter and solution code for the projects, so you'll be needing to refer to it often throughout this semester.

# Intro to React Native

React Native is a cross platform app development tool that allows you to deploy to both iOS and Android with a single Javascript code base

## Pros

-   Easy to get started with (especially if you come from a web dev background)
-   Lots of components available to use in your app so you're not reinventing the wheel
-   Making beautifully styled apps is far easier with React Native

## Cons

-   Functionality isn't as good as native iOS and Android apps. Companies who start off with React Native usually transition to native mobile as they grow. E.g. Airbnb started off writing their mobile app with React Native. However, they've recently started the transition to a native iOS and Android codebase as the functionalities of React Native were not enough to cover their use cases.

# Installation

## React Native

-   First, make sure you have the latest version of [Node.JS](https://nodejs.org/en/) downloaded. You should have node > 6.0 installed
-   Run the following command from a terminal window: `npm install -g create-react-native-app` 

You'll also want to install Expo to run react native apps on physical devices.

Expo

-   Download [Expo for iOS](https://itunes.apple.com/us/app/expo-client/id982107779?mt=8) or [Expo for Android](https://play.google.com/store/apps/details?id=host.exp.exponent&hl=en_US) on your phone
-   Run the following command in a terminal window: `npm install expo-cli --global` 

## Hello World!

Now we're ready to create our first app with React Native

-   `cd` to the directory where you want your app to live
-   To create and initialize a project, run the following commands
-   `create-react-native-app YourProjectName`
    -   `cd YourProjectName`

# React Native Project Structure

Open the project and run `ls -a` to see all of the files in the project.

We can already see there are a ton of files already in the React Native project--even though we haven't written code yet. Before we proceed, let's learn the purpose of each of the files.

 

-   `node_modules/` contains all third party packages in our application. Any new dependencies and development dependencies are stored here once they are installed.
-   `.babelrc` allows us to define presets and plugins for configuring [Babel](https://babeljs.io). Babel is a transpiler that compiles newer experimental JavaScript into older versions so that it stays compatible with different platforms.
-   `.flowconfig` allows us to configure [Flow](https://flow.org/en/), a static type checker for JavaScript. Flow is part of the React Native toolchain and this file is included automatically in any React Native application. It's mainly used for prop validations using prop-types (we'll be covering props later).
-   `.gitignore` is where we specify which files should be ignored by Git. We can see that both the `node_modules/` and `.expo/` directories are already included.
-   `.watchmanconfig` defines configurations for Watchman. You don't have to worry about Watchman right now--as it's mainly only used in large production apps
-   `App.js` is where our application code lives.
-   `app.json` is a configuration file that allows us to add information about our Expo app. The list of properties that can be included in this file is listed in the [documentation](< https://docs.expo.io/versions/v18.0.0/guides/configuration.html>).
-   `App.test.js` is included as a sample test file and contains a single test. CRNA (create-react-native-app) is packaged with [Jest](https://facebook.github.io/jest/) as its testing platform. If we've got time, we’ll learn unit testing React Native applications later on in the curriculum.
-   `package.json` is where we provide information of the application to our package manager as well as specify all our project dependencies.
-   `README.md`  is a markdown file commonly used to provide a description of a project.
-   `yarn.lock` is where yarn keeps a record of the versions of each dependency installed.

Don't worry if you didn't get all of the above. The only file we're really interested in are the `.js` files, particularly `App.js` 

# Running your first React Native App

## Expo

Execute `npm start`  in the React Native PROJECT directory

You should then see something like the following appear on your terminal window

![](https://storage.googleapis.com/slite-api-files-production/files/a8e9b36f-e057-4455-a47c-3c42db4495de/image.png)

Scan the QR code using the Expo app on your phone to run the app.

## Running on iOS

-   If you have a Mac and want to run on iOS simulator, run `react native run-ios` 
-   This should automatically launch your react native app in the running within the Expo app in the simulator.

## Running on Android

-   The same steps as above, just replace `react native run-ios` with `react-native run-android` 
-   Make sure you have set up an AVD (Android Virtual Device) first before running on the Android simulator. See this link for instructions on how to do so: https://facebook.github.io/react-native/docs/getting-started.html#preparing-the-android-device
-   It's important you follow the steps exactly as described, speficially note the following details for the AVD: **Marshmallow **API Level 23, x86_64 ABI image with a Android 6.0 (Google APIs) target.

# Setting up your IDE

-   Having an IDE is not strictly necessary for React Native programming; in fact you can write React Native programs perfectly well with only a text editor. 
-   However, depending on your preferences, you may appreciate the additional features an IDE brings (e.g. code completion or syntax checking) 
-   Linked below are two IDEs that can handle React Native. Visual Studio Code is free and open source, while Webstorm is a paid software, but you can use it for free if you're a student. Webstorm does feature more funcionality than Visual Studio Code, but does have an initial learning curve. 
-   Visual Studio Code: https://code.visualstudio.com
-   Webstorm: https://www.jetbrains.com/webstorm/

## 

\*\* NOTE \*\*

A common error is to initialize a project and run it without running `npm start`. 

If you get an error that says "Unable to resolve module..." , make sure you have run `npm install` in your project directory.


