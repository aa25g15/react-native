# React Native Course Notes - Academind by Maximilian Schwarzmüller on Udemy
https://docs.google.com/presentation/d/1Uz0JUKz6YeB24xLsKsJpmcyph5DjgJU0pZoUuCA89eU/edit?usp=sharing

--------

* React is platform agnostic!
  * react-dom attaches it to the browser
  * react-native attaches it to the iOS and Android
* React native exposes some special components which will be compiled to native components and also some special APIs such as the camera
* You can make web apps using React Native but the support is botchy, it is not really meant for that
* Remember that these special components such as ```<View></View>``` are compiled to the native ones depending on iOS or Android (RN does this mapping on its own) and not the JS, React Native runs a JS process to execute your logic!
  * So your JS runs as JS and is not compiled!
* https://reactnative.dev/
* Expo CLI vs React Native CLI
  * Expo makes life a little easier, more than RN CLI
* ```npm i -g expo-cli```
* ```Expo init {course name}```
* Install the Expo Go app and scan barcode after running ```npm start```
* Install emulators
  * XCODE - iOS
  * Android Studio
* Remember that HTML elements will not work on RN cause native apps are not browsers and they do not have a DOM
* No CSS in RN as it is again not a browser but you do make Stylesheet objects which have properties similar to CSS
* This is wrong:
```jsx
<View>
 Hello World!
</View>
```
* This is fine:
```jsx
<View>
 <Text>Hello World!</Text>
</View>
```
* However, from web dev we know that it is fine, it is not too strict, in RN, you cannot be flexible with what the components are intended for
* ```<View>``` - Container component, similar to div
* ```<Button title="click me!" />``` - This button will auto adjust to basic styling in iOS and Android
* The style attribute is not supported by all RN components but some like ```<Text>``` and ```<View>```
* Inline styles, remember the styling is inspired by CSS not is not CSS and does not have all the features, for example, "border" property is not supported but there is "borderWidth" and "borderColor":
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/220410912-1f47ec00-af40-48e1-8bd5-5792a345c266.png">

* Better to create Stylesheet object:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/220411870-bda2d68e-af9b-44de-8806-20cb0b56ccb5.png">

* There is flexbox in RN much like CSS and is generally used to create layouts like in web dev
* Every ```<View>``` by default uses Flexbox unlike divs in HTML and using flex-direction column
* Flexbox
  * The most appropriate tool to create views, layouts
  * Main axis - flex-direction and cross-axis (perpendicular)
  * justify-content - Positioning along main axis
  * align-items - Positioning along cross axis (default value is stretch, so flex items with stretch to occupy full size of flex container ONLY along cross-axis)
  * You can set ```flex: 1``` or some other value on children to determine their relative sizes
  * A ```flex: 1``` on all children means that all children will be of equal size along main axis
  * Remember Views have flex enabled by default and also default direction is column
* Button RN component does not support style attribute
* Events - There are some differences from the web, for example, Button does not have onClick but onPress
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/220546586-cfb624f8-2373-4600-9045-db72c66d30ca.png">

* State in a component
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/220547845-05308032-286c-4eee-9402-5e45cfce7a92.png">

* When your state depends on previous state, never assign the state using the set method directly, always pass a function!! Here the courseGoals list needs to be updated with new goal that was just added, its state depends on previous state (previous value of courseGoals array) so we must pass a function:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/220549666-45fa30e8-e595-4443-a095-36c0437c527f.png">

* Remember unlike CSS, RN styles do not cascade! So the children will not derive styling from ancestors
* Not that there are some differences under the hood between iOS and Android, for example if you add ```border-radius``` directly to ```<Text>``` RN element, it is compiled to native iOS or Android element but that native element in Android supports border-radius but on iOS it does not, so you will not see border-radius on iOS applied, what you then need to do is wrap your Text element with a View, which is more versatile and supports border-radius in both iOS and Android
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/220554220-1aa3979a-ca10-4a2b-80c0-2a94ccc6f752.png">

* Sometimes you may need to write different code for each platform cause differences are harder to handle
* ```<ScrollView>``` - Remember to wrap this in a View, that View will control the size the ScrollView occupies, this will make sure you get the expected proportions and this is a standard way of setting up a ScrollView
<img width="651" alt="image" src="https://user-images.githubusercontent.com/26576978/220556490-3b0304e9-3aa9-4ffb-96a0-7be55f1ec2d7.png">

* FlatList is better than ScrollView cause it lazy renders children as the user scrolls so it is ideal for long or dynamic lists, ScrollView will render every children regardless of scroll
* Your data can be a list of objects with each object containing key property which will be automatically picked up by FlatList or you can pass a keyExtractor function to generate a key for each time
* Remember renderItem function gets itemData which has list item but also some metadata
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/220562933-ec512a11-4262-439f-986f-8cf9bb40f512.png">

* Two way binding on TextInput, attach onChangeText to a handler that updates component state and attach value of TextInput to the state, this is not really specific to RN but is simple React:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/220569082-d9e178aa-0c05-4e18-ac0a-b15a5812a226.png">

* To make something pressable which is not a button, for example, its a View, we cannot directly add onClick or onPress like in HTML but we need to wrap it in ```<Pressable onPress={handler}>```
* Adding click feedback for iOS and Android - Notice android_ripple and the use of a function in style attribute. The function gives states such as pressed which can be used to set styles for that state.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/220605175-c9cd7842-b6e7-44e5-a38f-610c95e827c0.png">

* Using a modal, look at docs if you need more info:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/220606549-f5fd130c-e035-49a8-a7a5-0a827ab062f4.png">

* You can build your own button using ```<Pressable>``` component but remember that styles will not get applied to ```<Button>```, if for example, you need to position these in a row and add margin, you might need to wrap each ```<Button>``` in a ```<View>```
* Adding an image - Note that this is not the same as the web, we cannot "fetch" and image from an endpoint as such, the ```<Image>``` component also supports the style attribute
<img width="970" alt="image" src="https://user-images.githubusercontent.com/26576978/220612762-bf9d07b0-aaf1-4512-ba60-00719b5ec877.png">

* Expo allows us to set background-color for all screens in one go by using the config file App.js
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/220614514-345358e4-6e97-4b44-9519-68b3667b5ee3.png">

* But remember that on dark background the status bar (the bar with battery percentage, time etc.) can get hard to see, so expo provides a solution for that, you can set the style to 'light' on darker backgrounds to make the status bar white in color, read more on docs:
<img width="552" alt="image" src="https://user-images.githubusercontent.com/26576978/220614943-f2e5b401-4053-4d2e-b5be-f5f5eed65ae1.png">

* Remote Debugging - You can open the developer menu from terminal by pressing m (I think) and then you can choose the option to remotely debug JS. This will open a devtools window in Chrome and you can see network requests, logs etc.
* You can also use react-devtools - ```npm i -g react-devtools```
* Then, in separate terminal, run command - `react-devtools`
* Then, enable remote debugging in the developer menu and the devtools will connect, you can see component tree, state etc.
* Maximillian created:
  * A folder screens, for all screens
  * A folder components, for all reusable components used on the screens such as buttons, inputs etc.
* Custom button - This is how it is implemented in official RN button too, this does not have ```<Pressable>``` for now:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/220853362-13aa0e57-ed34-4a0d-a648-7eca3d74934f.png">

* Adding shadows, elevation is Android-only, rest properties are for iOS:
<img width="552" alt="image" src="https://user-images.githubusercontent.com/26576978/220858286-f9be8722-b423-4707-80fd-48c9af1e6b8c.png">

* Use maxLength to limit the number of characters, notice this has to be a number in braces and not in quotes - ```<TextInput maxLength={2}>```
* Notice keyboardType and other props:
<img width="360" alt="image" src="https://user-images.githubusercontent.com/26576978/220863467-f562e013-3ecf-4b1f-9397-ef5a29db8e33.png">

* Custom button - When using an array of styles, all styles will be considered by React Native, notice that the Pressable is around Text and not View, this is because the ripple effect in android needs this type of configuration otherwise you will have the ripple outside the button rather than inside
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/220948750-76151144-0b7f-4325-8105-29c6be7c6c8f.png">

* Every View creates a new flexbox container
* By default, Views only take as much space as they need to fit their content inside themselves
* To use gradient - ```expo install expo-linear-gradient```
<img width="1022" alt="image" src="https://user-images.githubusercontent.com/26576978/221119172-a97f7b96-f94e-40bd-9ef3-0a95ec6f3c7f.png">

* Adding background image using ```<ImageBackground>``` from RN:
<img width="1022" alt="image" src="https://user-images.githubusercontent.com/26576978/221120085-c6ea9546-a115-4fa4-b765-148906606711.png">

* The value you get from TextInput will always be a string, even if you intend it to be a number
* Showing native alerts - Remember the Alert is imported from RN:
<img width="1022" alt="image" src="https://user-images.githubusercontent.com/26576978/221122851-68194fbb-c607-43e6-93b8-52fba2db5314.png">

* Notice that functions like ```parseInt()``` and ```isNaN()``` are available in RN environment
* In the course while making the number guessing game, he used useState to switch screen components in the App component based on whether a number was picked or not:
<img width="1022" alt="image" src="https://user-images.githubusercontent.com/26576978/221125283-2bf730a1-8596-438e-a320-a9bd1548d31f.png">

* Wrap your screen output in ```<SafeAreaView>``` to ensure that device notches, status bar etc. do not conflict with your content, this component automatically detects the device and adds appropriate spacing on the top
* It is common to do this to manage global colors etc.
<img width="1244" alt="image" src="https://user-images.githubusercontent.com/26576978/221127874-25d0a7ef-a4f5-4a67-8972-0d24c0f8aab9.png">

* This is how you can add overriding styles to your custom component, in the styles array, the styles on the right will override the styles on the left:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/221142729-315c8072-4942-40f1-b429-cb20168474d1.png">

* For icons you can use ```import {IonIcons} from '@expo/vector-icons';```. Note that there are many other exports available, check documentation.
<img width="787" alt="image" src="https://user-images.githubusercontent.com/26576978/221143726-8e147fe5-6ee9-4cc5-af24-ebcb042c62df.png">

* Custom fonts - ```import { useFonts } from 'expo-font'```, install expo-font using expo install
<img width="816" alt="image" src="https://user-images.githubusercontent.com/26576978/221147791-f101b6ef-4d0c-47eb-99ca-19b831171b84.png">

* You can simply use ```fontFamily: 'open-sans-bold'``` in your style object
* Also, while fonts are loading, you might want to show a splashscreen, you can use - ```import AppLoading from 'expo-app-loading'```
* To make an image inside a circle, you need to wrap ```<Image />``` in a View and then add same height and width to that view and a borderRadius half of that width or height to make a circle, you need to add ```overflow: 'hidden'``` to make sure everything outside is clipped
* You can put Text inside Text and style nested Texts differently but remember that unlike View, nested Texts do get influenced by parent Text styling. This is just cause of how the compilation to native components happens.
* ```maxWidth: '80%'``` - Remember that you can use percentage units too and these will always be in reference to the parent container
* The Dimensions API allows us to get screen/window sizes which can be used for responsive styling. ```import { Dimensions } from 'react-native'```. Note that there is window and screen, on iOS there is no difference but on Android screen is with status bar and window is without status bar.
<img width="816" alt="image" src="https://user-images.githubusercontent.com/26576978/221186143-7e95cf0e-64cf-401e-a3d7-4fc79e3daef8.png">

* You can change the orientation using the same flag in App.json, default sets the app to rotate with device rotation, landscape and portrait lock the orientation.
* Remember that using Dimensions API directly like this will not react to dimension changes while the app is being used, for example, if device rotates from portrait to landscape, so for this, we need to use a hook:
```javascript
import { useWindowDimensions } from 'react-native'

const Component = () => {
 const [width, height] = useWindowDimensions(); // Will listen to size changes
 
 const marginTopDistance = height < 380 ? 30 : 100;
 
 return (
  <View style={[styles.container, {marginTop: marginTopDistance}]}>
   <Text>Hello World</Text>
  </View>
 );
}
```
* Making sure keyboard does not block the UI:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/221350045-6069f6fa-b87a-4fe3-9cc5-738be6fdf496.png">

* With the Platform API imported from RN, you can make changes specific to different platforms such as iOS and Android:
<img width="816" alt="image" src="https://user-images.githubusercontent.com/26576978/221350634-1754f2ca-0e15-4bb1-af9f-304d0f8f8191.png">

* You can even make different files for Android and iOS like ```Title.android.js``` and ```Title.ios.js``` and import it ONLY as Title and not with platform extensions. This way, RN will select the right file automatically under the hood for the platform. This is not limited to components but can also be done for files like ```Colors.adroid.js``` and ```Colors.ios.js```.
* Remember in iOS shadow will not be applied unless you add a backgroundColor!
* On FlatList, you can add ```numColumns={2}``` for example, to show the content in 2 columns etc.
* Adding routing - Will install a package called React Navigation
```npm install @react-navigation/native```
```expo install react-native-screens react-native-safe-area-context```
* There are different types of navigators but we will for now use Stack navigator:
```npm install @react-navigation/native-stack```
* Then in App component:
<img width="816" alt="image" src="https://user-images.githubusercontent.com/26576978/221352083-ebd37203-89fb-41c2-a9be-430443a8db45.png">

* Note that by just using this setup, we automatically get a safe area, a background and a header with Screen name etc. We can obviously configure this.
* Every screen component (the one we defined in ```<Stack.Screen compoment={CategoriesScreen} name="MealsCategories" />```) will get a navigation prop which can be used to navigate between different screens - ```navigation.navigate("MealsOverview");```
* When setting up a Navigator (like ```<Stack.Navigator>```) and registering its screens (via ```<Stack.Screen>```), you can decide which screen will be shown as a default when the app starts. Out of the box, the top-most screen (i.e. the first child inside of ```<Stack.Navigator>```) is used as the initial screen.
* You can therefore change the initial screen by changing the ```<Stack.Screen>``` order. Alternatively, there also is an ```initialRouteName``` prop that can be set on the navigator component (i.e., on ```<Stack.Navigator>``` in this case)
* If you have to trigger navigation deep down the component tree, you might not want to keep passing down the navigation object from screen component, instead, you can use this hook, note that tis is being imported from native only and not native-stack:
<img width="742" alt="image" src="https://user-images.githubusercontent.com/26576978/221353241-fe92729a-343c-4eb7-825c-6c48c0f5d9c6.png">

* The Native Stack navigator will use native elements for navigation which is more performant, so this should be the default choice, however, if we run into problems, there is also a Stack navigator that emulates the native behaviour
* To pass data to next route:
```javascript
navigation.navigate("MealsOverview", {
 mealId: 98 // For example only
});
```
* Then to get this in the next screen:
```javascript
const mealId = route.params.mealId; // route will be available as prop in the next screen component, same as navigation
// Or we can use:
const route = useRoute(); // Gives the same route object as before, remember this is from "@react-navigation/native"
```
* When getting image from a URL, we need to write source like this and also, it is must to set height and width in this case since RN cannot know this for an image fetched from the web:
<img width="742" alt="image" src="https://user-images.githubusercontent.com/26576978/221358679-5d702fad-1b1c-4111-acb4-2da66f6bed86.png">

* You can add an options prop like this on each screen to configure that particular screen's navigation header, you can also move some styles to the Navigator wrapper to have default styles for every screen using prop ```screenOptions``` and not just options
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/221373770-fc81be0a-b4e8-432f-be52-6a19d9891923.png">

* Setting navigation option dynamically - Approach 1:
<img width="705" alt="image" src="https://user-images.githubusercontent.com/26576978/221395240-3fd39e49-f61d-4f8b-a46e-7ad527bcc33e.png">

* Setting navigation option dynamically - Approach 2 - Note that we have used useLayoutEffect rather than useEffect cause useEffect is called when the component has rendered, this will cause a flash of wrong text, useLayoutEffect is triggered before the layout is painted (I think) so there is no flash of wrong text:
<img width="977" alt="image" src="https://user-images.githubusercontent.com/26576978/221395317-fc2c2956-1e3d-4259-bc96-646be6adf0ef.png">

* Adding custom components to header, as before you can also do it directly on ```Stack.Screen```:
<img width="977" alt="image" src="https://user-images.githubusercontent.com/26576978/221397045-45bf716f-4e92-4d13-9e51-e18530929141.png">

* Using a drawer navigation - Remember all these different types of navigation are there in the documentation of React Navigation, you can check implementation from there:
<img width="977" alt="image" src="https://user-images.githubusercontent.com/26576978/221404323-3341e314-27ad-485c-a14c-965123aacd3c.png">

* There are a lot of customization options available for drawers, check documentation
* This is how you can toggle drawer using navigation object:
<img width="523" alt="image" src="https://user-images.githubusercontent.com/26576978/221405328-2a35fd67-24f3-4047-b972-58c9b92bfb5a.png">

* There are also tab navigators, super simple to setup, have a look at docs
* You can even nest navigators such as a stack and a drawer, this might cause 2 headers, so you might have to manually hide one in options
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/221406162-f723e3d8-91f4-4ed2-b652-7f1e81c6dd9a.png">

```jsx
const drawerNavigator = () => {
 <Drawer.Navigator>
  <Drawer.Screen component={Screen1Component} name="Screen 1" />
  <Drawer.Screen component={Screen3Component} name="Screen 3" />
 </Drawer.Navigator>
}

<NavigationContainer>
 <Stack.Navigator>
   <Stack.Screen component={drawerNavigator} name="Screen 1" options={{
    headerShown: false
   }} /> // Notice the nesting here
   <Stack.Screen component={Screen2Component} name="Screen 2" />
 </Stack.Navigator>
</NavigationContainer>
```
