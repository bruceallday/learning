---
layout: slidedeck
title: Navigation and Dependencies Slides
---

{% highlight html %}
name: inverse
layout: true
class: center, middle, inverse

---

# Navigation and Dependencies

.title-logo[![Red logo](/public/img/red-logo-white.svg)]

---

layout: false

# Agenda

1.  Reasoning about mobile navigation
2.  Navigation options in React Native
3.  Implement React Navigation in an app
4.  Use third-party modules with native dependencies

---

template: inverse

# Navigation in Mobile Apps

---

# Browserless Nav

What we don't have:

- The usual back and forward buttons
- Browser history
- Hypertext and URLs

What we do have:

- Established **platform-specific patterns** that people are accustomed to when navigating around native mobile apps

---

class: center, middle

### iOS Human Interface Guidelines:

People tend to be unaware of an app's navigation until it doesn't meet their expectations.

_So while mobile nav may seem simple on the surface, we have to put a bit of thought into it to build it out well._

---

# Basic Infrastructure

A basic navigation infrastructure for our apps will hold a **navigation stack**.

The stack will hold **screens**, and those screens will hold **components** and **data**.

We can also **nest** navigation stacks within one another.

We may also use **tab bars** and **drawer-style navigation**.

---

class: center, middle

.inline-images[
![Nav stack screens](/public/img/slide-assets/nav-stack-screens.png)
]

---

class: center, middle

.inline-images[
![Nav stack screens stacked](/public/img/slide-assets/nav-stack-stacked.png)
]

---

class: center, middle

.inline-images[
![Tabs can have nav stacks](/public/img/slide-assets/nav-tab-stacks.png)
]

---

template: inverse

# Navigation Components

---

class: center, middle

.large[
React Native has some built-in navigation components...
]

---

# NavigatorIOS

See the docs: [NavigatorIOS](https://facebook.github.io/react-native/docs/navigatorios.html)

- Integrated with UIKit (leverages its animation)
- Built on top of `UINavigationController`
- Uses routes to represent screens
- Very stateful
- No Android support

---

# Other Nav Components

**Tabs and Drawers:**

- [TabBarIOS](https://facebook.github.io/react-native/docs/tabbarios.html)
- [DrawerLayoutAndroid](https://facebook.github.io/react-native/docs/drawerlayoutandroid.html)

**Deprecated:**

- Navigator (cross-platform JS navigator)
- NavigationExperimental

---

# Third-Party Solutions

Some of third-party solutions wrap the built-in navigator, others expose the platform's native navigation. Some popular options include:

- [react-community/react-navigation](https://github.com/react-community/react-navigation)
- [wix/react-native-navigation](https://github.com/wix/react-native-navigation)
- [aksonov/react-native-router-flux](https://github.com/aksonov/react-native-router-flux)

---

# What We Need

Ideally, we want an all-in-one navigation solution with:

- Support for **Android back button**
- Integration with a (potentially cross-platform) **tab bar**
- Support for **nested nav stacks** without creating state management headaches for ourselves
- Good **performance** (uses native animation)

---

# React Navigation

- A JS-based navigator implementation
- But with animation that run on the native UI thread!
- Provides a set of defaults that can be customized
- Supports tab navigation, sliding drawer navigation, the Android back button, and modals
- Easily nests stack navigation within tab navigation
- Can integrate its navigation state with your own Redux store (but this is optional, and we will skip it)

---

# Configuration

- `createAppContainer` is responsible for state management and linking your root navigator to the app enviroment. On Android, it handles the back button.

- `createStackNavigator` returns a React component and allows the app to transition between screens and manage history
- `createStackNavigator` takes a route configuration object and options as arguments

---

# Hello React Navigation

A Hello World Example with `React Navigation`

```js
import { createAppContainer } from "react-navigation";
import { createStackNavigator } from "react-navigation-stack";

class HomeScreen extends React.Component {
  render() {
    return (
      <View>
        <Text>Home Screen</Text>
      </View>
    );
  }
}

const AppNavigator = createStackNavigator({
  Home: {
    screen: HomeScreen
  }
});

export default createAppContainer(AppNavigator);
```

---

# Exercise 1

First, follow [installation steps](https://reactnavigation.org/docs/en/getting-started.html) to install `react-navigation` in your R10 project. Next, create a `navigation` sub-directory in the `js` directory of R10. Add a file called `RootStackNavigator.js` to it.

Import [createStackNavigator](https://reactnavigation.org/docs/en/stack-navigator.html) and [createAppContainer](https://reactnavigation.org/docs/en/app-containers.html#docsNav) in this new file, and use it to create a stack navigator with your About screen as its only route. Make this your default export from `RootStackNavigator.js`.

Finally, import your new `RootStackNavigator` component into `App.js`, and nest it inside your `ApolloProvider`. Does it work? How do you add a title to the navigation bar?

---

# Next Steps

For our purposes it will be best to leave this navigator defined at the highest level of our app, and then **nest our tab bar navigation within it** (or drawer navigation for Android).

Why do it this way? Eventually, when we add our lightbox-style Speaker screen, we will need to **push this screen onto our top-level stack navigator.**

If we were to simply push this screen onto the stack inside the tab bar, we would have tab fixed on top of the lightbox (which does not adhere to the prototype).

---

# More Set-up

Create a `NavigationLayout.js` file your `navigation` directory. Add this code to it:

```js
import React from "react";
import { createBottomTabNavigator } from "react-navigation-tabs";
import { createStackNavigator } from "react-navigation-stack";

import AboutScreen from "../screens/About";

const AboutStack = createStackNavigator({
  About: AboutScreen
});

// Dedicated stacks for Schedule, Map and Faves will go here too!

export default createBottomTabNavigator(/* ...some args go here */);
```

---

# Exercise 2

Read through the **[Tab navigation docs](https://reactnavigation.org/docs/en/tab-based-navigation.html)** learn how to add your new About stack to your `createBottomTabNavigator`. If you have created other screens already, create stacks for those those as well and add them to the tab navigator.

Next, instead of using your About screen directly inside your `RootStackNavigator`, use `NavigationLayout` instead.

But we have a problem now! There are two navigation bars at the top of the app (one for the root stack, the other for the nested stack). You can find a hint for hiding the nav bar for the `RootStackNavigator` **[in this example in the docs](https://reactnavigation.org/docs/en/stack-navigator.html#modal-stacknavigator-with-custom-screen-transitions)**.

---

# Exercise 3

Add **[some tab bar options](https://reactnavigation.org/docs/en/bottom-tab-navigator.html#bottomtabnavigatorconfig)** to configure its style.

Tab bar options are passed into `createBottomTabNavigator` as its second argument, e.g.:

`{ tabBarOptions: { /* your options here... */ } }`

Set the `activeTintColor` (white), `inactiveTintColor` (medium grey), the font size to `10` using `labelStyle`, and the background color (black) using `style`.

We'll add the icons next!

---

template: inverse

# Linking Dependencies

---

# Native Modules are now Autolinked

As of React Native 0.60, most of the packages will be auto-linked.

If you are using React Native < `0.60` then use we need to use `react-native link` command. (We are using RN `0.60`)

---

# Installation and Linkning

Our app is going to need some icons, so for that we're going to add the **[React Native Vector Icons package](https://github.com/oblador/react-native-vector-icons)**.

`Note:` Until React Native Vector Icons README provides official information on linking this library use this.

`yarn add react-native-vector-icons`

Next, navigate to the `ios` dir, install Pods and get back to the root level of your project.

```bash
cd ios/
pod install
cd ..
```

---

#Next

create a file named `react-native.config.js` in the root of your project and add this snippet to link dependency.

```js
module.exports = {
  assets: ["react-native-vector-icons"]
};
```

and finally run

```bash
yarn react-native link
```

These steps should link the React Native Vector Icons package to your project.

---

# Exercise 4

Next, import Ionicons into `NavigationLayout.js`. Add a `navigationOptions` key to your tab bar config object, and render the correct icon for each tab. An icon should be `white` if selected, and medium grey if not.

**[Use this example from the React Navigation docs](https://reactnavigation.org/docs/en/tab-based-navigation.html#customizing-the-appearance)** to help complete this exercise.

---

# Exercise 5

We want to use Montserrat as a custom font in our app.

Inside of the app's `react-native.config.js` file, add the following:

```js
module.exports = {
  assets: ["react-native-vector-icons", "./js/assets/fonts"]
};
```

Move your project's fonts into the above directory and run `yarn react-native link` again.

Use Montserrat as the `fontFamily` for the tab bar labels now to test it out.

---

class: center, middle

.large[ Finishing touches...]

---

# Gradient Header

R10 has a linear gradient background in the navigation bar. We will need another package (with dependencies to add) for that.

`Hint:` follow the steps we performed to add `React Native Vector Icons` to our project, to add `React Native Linear Gradient` package.

Add a `config.js` file to the `navigation` directory with this:

```js
import React from "react";
import { StyleSheet, View } from "react-native";
import { Header } from "react-navigation-stack";
import LinearGradient from "react-native-linear-gradient";

// ...more to come here!
```

---

# Gradient Header

Next, in `config.js` create the component that we will use as the navigation bar background:

```js
// ...

const GradientHeader = props => (
  <View style={% raw %}{{ backgroundColor: 'white', overflow: 'hidden' }}{% endraw %}>
    <LinearGradient
      colors={['#cf392a', '#9963ea']}
      start={% raw %}{{ x: 0.0, y: 1.0 }}{% endraw %}
      end={% raw %}{{ x: 1.0, y: 0.0 }}{% endraw %}
      style={[StyleSheet.absoluteFill, { height: 64, width: '100%' }]}
    />
    <Header {...props} />
  </View>
);
```

---

# Navigation Options

Lastly, create `sharedNavigationOptions` in `config.js` and set the custom background there:

```js
// ...

export const sharedNavigationOptions = navigation => ({
  headerBackTitle: null,
  header: props => <GradientHeader {...props} />,
  headerStyle: {
    backgroundColor: "transparent"
  }
});
```

You can also **set the style of the navigation bar text** to white and use Montserrat here as well. (Hint: Check the docs!)

---

# Navigation Options

Finally, use your `sharedNavigationOptions` in `NavigationLayout.js`:

```js
// ADD THIS!
import { sharedNavigationOptions } from "./config";

const AboutStack = createStackNavigator(
  {
    About: AboutScreen
  },
  // AND THIS!
  {
    defaultNavigationOptions: ({ navigation }) => ({
      ...sharedNavigationOptions(navigation)
    })
  }
);
```

---

# What We've Learned

- Special considerations for building out user-friendly navigation in mobile apps
- What navigation options are built into React Native, and what third-party options are available
- How to use a stack navigator and tab bar
- How to add third-party libraries and link font dependencies

---

template: inverse

# Questions?

{% endhighlight %}
