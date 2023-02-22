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

