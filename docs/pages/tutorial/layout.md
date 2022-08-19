---
title: Build a layout
---

import SnackInline from '~/components/plugins/SnackInline';
import ImageSpotlight from '~/components/plugins/ImageSpotlight'

In this module, you will create the first layout of your app. It displays an image and two buttons. The image is later used as a background image to put an emoji sticker on it. We will provide a default image as a placeholder in case you do not want to pick a new image. The first button is going to allow you to pick an image from the device's media library. The second button is going to allow you to use the placeholder image.

You will build the following layout as the first screen of your app:

<ImageSpotlight alt="Initial layout." src="/static/images/tutorial/initial-layout.jpg" style={{ maxWidth: 300 }} containerStyle={{ marginBottom: 0 }} />

## Step 1: Break down the layout

Let's break down the layout of the screen into basic elements. Most of these elements directly correspond to the build-in [Core Components](https://reactnative.dev/docs/components-and-apis) from React Native. In the first example, there are four basic elements:

<ImageSpotlight alt="Break down of initial layout." src="/static/images/tutorial/breakdown-of-layout.jpg" style={{ maxWidth: 300 }} containerStyle={{ marginBottom: 0 }} />

On breaking down the initial layout, you get:

- The screen background uses a specific background color
- There is a large image displayed at the center of the screen
- There are two buttons in the bottom half of the screen

One of the basic elements of the layout is composed of multiple components. For example, the first button that is encapsulated inside a yellow border contains a parent element that provides this border, and also wraps around an icon component and a text component to display the label inside a row.

<ImageSpotlight alt="Break down of the button component with row." src="/static/images/tutorial/breakdown-of-buttons.jpg" style={{ maxWidth: 480 }} containerStyle={{ marginBottom: 0 }} />

These elements are also using custom styles. In React Native, the styling of the application is done using JavaScript. All the Core components accept a `style` prop that accepts a JavaScript object as its value. For more information, see [Styling in React Native](https://reactnative.dev/docs/styles).

If you want to dive deep and understand the layout mechanism in React Native, start with React Native's [Layout with Flexbox](https://reactnative.dev/docs/flexbox).

Once the layout has been diagrammed, it becomes easier to implement.

## Step 2: Style the background

First, you are going to change the background color of the app screen. From the layout, you can notice that it is using a specific background color. This value is defined in the `styles` object in the **App.js** file.

Replace the default value of `#fff` with `#25292e` in the `styles.container.backgroundColor`. This will change the background color of the screen.

<!-- prettier-ignore -->
```js
import { StatusBar } from "expo-status-bar";
import { StyleSheet, Text, View } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <Text>Open up App.js to start working on your app!</Text>
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    /* @info Replace the default value of backgroundColor property to "#25292e". */
    backgroundColor: "#25292e", 
    /* @end */
    alignItems: "center",
    justifyContent: "center",
  },
});
```

### Step 2.1: Change the text color

The `Text` component uses the color value of `#000` as the default text color. Setting up the new background color value on the `View` component is going to make the text harder to read. Let's also add an inline style on the `Text` to change the text color to `#fff`.

<SnackInline label="Styled Background" dependencies={['expo-status-bar']}>

<!-- prettier-ignore -->
```js
import { StatusBar } from "expo-status-bar";
import { StyleSheet, Text, View } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      /* @info Replace the default value of color property to "#fff". */
      <Text style={{color: '#fff'}}>Open up App.js to start working on your app!</Text>
      /* @end */
      <StatusBar style="auto" />
    </View>
  );
}

/* @hide const styles = StyleSheet.create({*/
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#25292e", 
    alignItems: "center",
    justifyContent: "center",
  },
});
/* @end */
```

</SnackInline>

> **Tip**: The color value `#fff` is equal parts red, green, and blue, which creates a nice readable white. React Native uses the same color format as the web. It supports hex triplets (this is what `#fff` is), `rgba`, `hsl`, and a set of named colors like `red`, `green`, `blue`, `peru` and `papayawhip`. For more information, see [Colors in React Native](https://reactnative.dev/docs/colors).

## Step 3: Display the image

The `Image` component from React Native is used to display the image on the screen. It requires a source of the image. This source can be a [static asset](https://reactnative.dev/docs/images#static-image-resources) that can be required. for example, from the app's **assets/images** directory, or the source can come from the [Network](https://reactnative.dev/docs/images#network-images) in the form of a URI.

Our designers have provided a placeholder image that we will use for this tutorial:

<ImageSpotlight alt="Background image that we are going to use as a placeholder for the tutorial." src="/static/images/tutorial/background-image.png" style={{ maxWidth: 250 }} containerStyle={{ marginBottom: 0 }} />

You can download the above image and save it inside **assets/images** directory of your Expo app. If you are starting from scratch, you will have to create an **images** folder inside **assets**.

> **Tip**: If you cloned the repository when initializing the app, you will find it inside **assets/images** directory with file name of `background-image.png`.

Let's import and use `Image` component from React Native to display the image from the static resource. Let's also import the `background-image.png` in the **App.js** file:

<SnackInline label="Display placeholder image" dependencies={['expo-status-bar']} files={{
    'assets/images/background-image.png': 'https://snack-code-uploads.s3.us-west-1.amazonaws.com/~asset/503001f14bb7b8fe48a4e318ad07e910'
}}>

<!-- prettier-ignore -->
```js
import { StatusBar } from "expo-status-bar";
import { StyleSheet, View, /* @info Import the image component */ Image /* @end */} from "react-native";

/* @info Import the image from the "/assets/images" directory. Since the Image is a static resource, you have to reference it using "require". */
const PlaceholderImage = require("./assets/images/background-image.png");
/* @end */

export default function App() {
  return (
    <View style={styles.container}>
      /* @info Wrap the Image component inside a container. Also, add the image component to display the placeholder image. */
      <View style={styles.imageContainer}>              
        <Image source={PlaceholderImage} style={styles.image} />        
      </View>
      /* @end */
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    /* @info Modify container styles to remove justifyContent property. */
    flex: 1,
    backgroundColor: "#25292e",
    alignItems: "center",
    /* @end */
  },
  imageContainer: {
    flex: 1,
    paddingTop: 58,
    backgroundColor: "transparent",
  },
  image: {   
    width: 320,
    height: 440,
    borderRadius: 18,
  },
});
```

</SnackInline>

The `PlaceholderImage` variable holds the reference to the static background image. It is used as the value of the `source` prop on the `Image` component.

The `Image` component uses a `borderRadius` to apply rounded corners on the image. It is also wrapped inside a `View` component that will be useful to add touch-based gesture events in a later module. The `backgroundColor` on the `View` component is set to `transparent` to make the rounded corners visible.

### Step 2.1: Dividing components into files

The code snippets are going to get quite big, especially, with each snippet requiring custom styles. From this point, let's divide the code into multiple files.

- Create a folder called **components** at the root of the project. This will contain all the custom components that are created throughout this tutorial.
- Then, create a new file called **ImageViewer.js** inside the **components** folder.
- Move the code to display the image into this file.

```js
import { StyleSheet, View, Image } from 'react-native';

export default function ImageViewer({ placeholderImageSource }) {
  return (
    <View style={styles.imageContainer}>
      <Image source={placeholderImageSource} style={styles.image} />
    </View>
  );
}

const styles = StyleSheet.create({
  imageContainer: {
    flex: 1,
    paddingTop: 58,
    backgroundColor: 'transparent',
  },
  image: {
    width: 320,
    height: 440,
    borderRadius: 18,
  },
});
```

Next, let's import this component and use it in the **App.js** file:

<!-- prettier-ignore -->
```js
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, View } from 'react-native';

/* @info */ import ImageViewer from './components/ImageViewer'; /* @end */


const PlaceholderImage = require('./assets/images/background-image.png');

export default function App() {
  return (
    <View style={styles.container}>
      <ImageViewer placeholderImageSource={PlaceholderImage} />
      <StatusBar style="auto" />
    </View>
  );
}

/* @hide const styles = StyleSheet.create({ */
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
});
/* @end */
```

## Step 3: Create buttons using Pressable

A modern mobile device typically constitutes a touch screen as the primary interface between an application and the user. Any level of event interaction in an application can be achieved by using a button that on a physical device is a simple finger touch.

React Native provides various components to handle touch events on native platforms. For this tutorial, let's use the [`Pressable`](https://reactnative.dev/docs/pressable) API. It is a core component wrapper that can detect various stages of interactions from basic single tap events to advance events such as the long press. It can be customized in terms of style and appearance, and you can extend the functionality by creating a custom wrapper component around it.

### Step 3.1 Create a simple reusable button component

From the app's layout, there ate two buttons you have to implement. Each has different styles and labels. Let's start by creating a function component that can be reused to create the two buttons.

- Create a new file called **Button.js** inside the **components** folder.
- Then, import the `Pressable`component from React Native and then create a function component called `Button` with the following code snippet:

<!-- prettier-ignore -->
```js
import { StyleSheet, View, Pressable, Text } from 'react-native';

export default function Button({ label }) {
  return (
    <View style={styles.buttonContainer}>
      <Pressable style={styles.button} onPress={() => alert('You pressed a button.')}>
        <Text style={styles.buttonLabel}>{label}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  buttonContainer: {
    width: 356,
    height: 68,
    marginHorizontal: 20,
    alignItems: 'center',
    justifyContent: 'center',
    padding: 3,
  },
  button: {
    borderRadius: 10,
    width: '100%',
    height: '100%',
    alignItems: 'center',
    justifyContent: 'center',
    flexDirection: 'row',
  },
  buttonIcon: {
    paddingRight: 8,
  },
  buttonLabel: {
    color: '#fff',
    fontSize: 16,
  },
});
```

The `Button` component receives a `label` [prop](https://reactnative.dev/docs/intro-react#props) so that anytime this component is used, the button can have its own text.

When the user touches any of the buttons on the screen, it displays a dialog box. This is done by using an `alert()` function to display a static message. Currently, it is used as a placeholder since both buttons do not trigger any functionality right now.

Now let's import this component into **App.js** file and see it in action:

<!-- prettier-ignore -->
```js
import { StatusBar } from "expo-status-bar";
import { StyleSheet, View} from "react-native";

/* @info */ import Button from './components/Button'; /* @end */

import ImageViewer from './components/ImageViewer';

const PlaceholderImage = require("./assets/images/background-image.png");

export default function App() {
  return (
    <View style={styles.container}>      
      <ImageViewer placeholderImageSource={PlaceholderImage} />
      /* @info Use the reusable Button component to create two buttons. */
      <View style={styles.footerContainer}>
        <Button label="Choose a photo" />
        <Button label="Use this photo" />
      </View>
      /* @end */
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  /* @hide // Styles that are unchanged from previous step are hidden for brevity. */
  container: {    
    flex: 1,
    backgroundColor: "#25292e",
    alignItems: "center",    
  },
  imageContainer: {
    flex: 1,
    paddingTop: 58,
    backgroundColor: "transparent",
  },
  image: {    
    width: 356,
    height: 522,
    borderRadius: 18,
  },
  /* @end */

  footerContainer: {
    flex: 1 / 3,
    alignItems: "center",
  },  
});
```

The second button that has the label "Use this photo" resembles the actual button from the layout. However, the first button needs more styling to match the layout.

### Step 3.2: Enhance the reusable button component

To differentiate the two buttons, let's add another prop to the `Button` component called `isBorderLess` which is a boolean. When this prop's value is true, the unstyled button is displayed. Otherwise, the component is shown with enhanced styling.

The styled button that has the label "Choose a photo", also has an icon before the label. [`@expo/vector-icons` library](/guides/icons/#expovector-icons) provides icons from popular icon sets such as Ionicons, Feather, FontAwesome, MaterialCommunityIcons and so on. To load and display the icon on the button, let's use `FontAwesome` from the library.

Modify the **Button.js** to add the following code snippet:

<!-- prettier-ignore -->
```js
import { StyleSheet, View, Pressable, Text } from 'react-native';
/* @info Import FontAwesome. */import FontAwesome from "@expo/vector-icons/FontAwesome";/* @end */


export default function Button({ label, /* @info The prop isBorderLess has a default value of false. */ isBorderLess = false /* @end */ }) {
  /* @info Conditionally render the borderless button when isBorderLess is true */
  if (isBorderLess) {
    return (
      <View style={styles.buttonContainer}>
        <Pressable style={styles.button} onPress={() => alert('You pressed a button.')}>
          <Text style={styles.buttonLabel}>{label}</Text>
        </Pressable>
      </View>
    );
  }
  /* @end */

  return (
    <View
      style={[
        styles.buttonContainer,
        { borderWidth: 4, borderColor: '#ffd33d', borderRadius: 18 },
      ]}>
      <Pressable
        style={[styles.button, { backgroundColor: '#fff' }]}
        onPress={() => alert('You pressed a button.')}>
         /* @info The FontAwesome icon is used on the Pressable component. */
        <FontAwesome name="picture-o" size={18} color="#25292e" style={styles.buttonIcon} />
        /* @end */
        <Text style={[styles.buttonLabel, { color: '#25292e' }]}>{label}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  // Styles from previous step remain unchanged.
  buttonIcon: {
    paddingRight: 8,
  },
});
```

In the above code snippet, the styled button uses **inline styles** to append the styles from the `StyleSheet.create()`. For example, the `Pressable` component in the styled button uses a `backgroundColor` property of `#fff` to set the background color of the button. If you add this property to the `styles.button`, then the background color value will be set for both the styled button and the unstyled one. However, using inline styles allows you to override the default styles for a specific value.

Let's modify the **App.js** file to use `isBorderLess` prop on the second button.

<SnackInline label="Complete Layout"
templateId="tutorial/01-layout/App"
dependencies={['expo-status-bar', '@expo/vector-icons', '@expo/vector-icons/FontAwesome']}
files={{
    'assets/images/background-image.png': 'https://snack-code-uploads.s3.us-west-1.amazonaws.com/~asset/503001f14bb7b8fe48a4e318ad07e910',
    'components/ImageViewer.js': 'tutorial/01-layout/ImageViewer.js',
    'components/Button.js': 'tutorial/01-layout/Button.js'
}}>

<!-- prettier-ignore -->
```js
// ...
export default function App() {
  return (
    <View style={styles.container}>      
      <View style={styles.imageContainer}>              
        <Image source={PlaceholderImage} style={styles.image} />        
      </View>      
      <View style={styles.footerContainer}>
        <Button label="Choose a photo" />
        /* @info Add isBorderLess prop on the second button */
        <Button label="Use this photo" isBorderLess />
        /* @end */
      </View>      
      <StatusBar style="auto" />
    </View>
  );
}
```

</SnackInline>

On running the app, you will get a similar output on any device or emulator:

<ImageSpotlight alt="Complete layout screen running on multiple platforms." src="/static/images/tutorial/complete-layout.jpg" style={{ maxWidth: 720 }} containerStyle={{ marginBottom: 0 }} />

## Next steps

You have now created the initial layout. In the next step, let's add the functionality to [pick an image from the device's media library](/tutorial/image-picker).
