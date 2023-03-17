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
* I think in this course creating a context is much simpler than it was in that other course where we used a reducer and what not, this is how we simply created a context for favourite meals:
```jsx
import { createContext, useState } from 'react';

export const FavoritesContext = createContext({
  ids: [],
  addFavorite: (id) => {},
  removeFavorite: (id) => {},
});

function FavoritesContextProvider({ children }) {
  const [favoriteMealIds, setFavoriteMealIds] = useState([]);

  function addFavorite(id) {
    setFavoriteMealIds((currentFavIds) => [...currentFavIds, id]);
  }

  function removeFavorite(id) {
    setFavoriteMealIds((currentFavIds) =>
      currentFavIds.filter((mealId) => mealId !== id)
    );
  }

  const value = {
    ids: favoriteMealIds,
    addFavorite: addFavorite,
    removeFavorite: removeFavorite,
  };

  return (
    <FavoritesContext.Provider value={value}>
      {children}
    </FavoritesContext.Provider>
  );
}

export default FavoritesContextProvider;
```
* Now wrap your app inside
```jsx
<FavoritesContextProvider>{Your App}</FavoritesContextProvider>
```
* Now to use this context:
```jsx
const favouriteMealsContext = useContext(FavoritesContext); // The object which was created using createContext and is exported
```
* Well I found Redux to be a little more messy when compared to MobX but this is how you use it. Install React Redux Toolkit and React Redux. Note that without the toolkit, you cannot mutate the state in dispatch methods, with the kit you can as it takes care of that under the hood.
* In store/redux/store.js:
```jsx
import { configureStore } from '@reduxjs/toolkit';

import favoritesReducer from './favorites';

export const store = configureStore({
  reducer: {
    favoriteMeals: favoritesReducer
  }
});
```
* In store/redux/favourites.js:
```jsx
import { createSlice } from '@reduxjs/toolkit';

const favoritesSlice = createSlice({
  name: 'favorites',
  initialState: {
    ids: []
  },
  reducers: {
    addFavorite: (state, action) => {
      state.ids.push(action.payload.id);
    },
    removeFavorite: (state, action) => {
      state.ids.splice(state.ids.indexOf(action.payload.id), 1);
    }
  }
});

export const addFavorite = favoritesSlice.actions.addFavorite;
export const removeFavorite = favoritesSlice.actions.removeFavorite;
export default favoritesSlice.reducer;
```
* How to use the store inside a component:
```jsx
import { useLayoutEffect } from 'react';
import { View, Text, Image, StyleSheet, ScrollView } from 'react-native';
import { useDispatch, useSelector } from 'react-redux';

import IconButton from '../components/IconButton';
import List from '../components/MealDetail/List';
import Subtitle from '../components/MealDetail/Subtitle';
import MealDetails from '../components/MealDetails';
import { MEALS } from '../data/dummy-data';
import { addFavorite, removeFavorite } from '../store/redux/favorites';
// import { FavoritesContext } from '../store/context/favorites-context';

function MealDetailScreen({ route, navigation }) {
  // const favoriteMealsCtx = useContext(FavoritesContext);
  const favoriteMealIds = useSelector((state) => state.favoriteMeals.ids);
  const dispatch = useDispatch();

  const mealId = route.params.mealId;
  const selectedMeal = MEALS.find((meal) => meal.id === mealId);

  const mealIsFavorite = favoriteMealIds.includes(mealId);

  function changeFavoriteStatusHandler() {
    if (mealIsFavorite) {
      // favoriteMealsCtx.removeFavorite(mealId);
      dispatch(removeFavorite({ id: mealId }));
    } else {
      // favoriteMealsCtx.addFavorite(mealId);
      dispatch(addFavorite({ id: mealId }));
    }
  }

  useLayoutEffect(() => {
    navigation.setOptions({
      headerRight: () => {
        return (
          <IconButton
            icon={mealIsFavorite ? 'star' : 'star-outline'}
            color="white"
            onPress={changeFavoriteStatusHandler}
          />
        );
      },
    });
  }, [navigation, changeFavoriteStatusHandler]);

  return (
    <ScrollView style={styles.rootContainer}>
      <Image style={styles.image} source={{ uri: selectedMeal.imageUrl }} />
      <Text style={styles.title}>{selectedMeal.title}</Text>
      <MealDetails
        duration={selectedMeal.duration}
        complexity={selectedMeal.complexity}
        affordability={selectedMeal.affordability}
        textStyle={styles.detailText}
      />
      <View style={styles.listOuterContainer}>
        <View style={styles.listContainer}>
          <Subtitle>Ingredients</Subtitle>
          <List data={selectedMeal.ingredients} />
          <Subtitle>Steps</Subtitle>
          <List data={selectedMeal.steps} />
        </View>
      </View>
    </ScrollView>
  );
}

export default MealDetailScreen;

const styles = StyleSheet.create({
  rootContainer: {
    marginBottom: 32,
  },
  image: {
    width: '100%',
    height: 350,
  },
  title: {
    fontWeight: 'bold',
    fontSize: 24,
    margin: 8,
    textAlign: 'center',
    color: 'white',
  },
  detailText: {
    color: 'white',
  },
  listOuterContainer: {
    alignItems: 'center',
  },
  listContainer: {
    width: '80%',
  },
});
```
* Remember ```justifyContent: "space-between";``` can be used to position the flex boxes away from each other, I previously used ```marginLeft: "auto"``` for this
* Also remember that date.getMonth() will return the index of the month starting from 0, so you need to add 1 there
* With this presentation option, the screen will open and close like a modal:
<img width="425" alt="image" src="https://user-images.githubusercontent.com/26576978/221823556-599d1918-1252-4345-b343-411a3156c886.png">

* Going back to the screen which opened the current screen:
<img width="351" alt="image" src="https://user-images.githubusercontent.com/26576978/221830435-7401fad6-2a90-45ea-9fc8-0992c3773c17.png">

* Note that here we have used the Context API with ```useReducer``` hook to manage state instead of ```useState``` hook which is better when you have a more complicated state. Note that for some reason, Maximillian keeps saying that the object we pass to ```createContext()``` is not really used for initial state but only provides autocompletion, but confirm this.
```jsx
import { createContext, useReducer } from 'react';

const DUMMY_EXPENSES = [
  {
    id: 'e1',
    description: 'A pair of shoes',
    amount: 59.99,
    date: new Date('2021-12-19'),
  },
  {
    id: 'e2',
    description: 'A pair of trousers',
    amount: 89.29,
    date: new Date('2022-01-05'),
  },
  {
    id: 'e3',
    description: 'Some bananas',
    amount: 5.99,
    date: new Date('2021-12-01'),
  },
  {
    id: 'e4',
    description: 'A book',
    amount: 14.99,
    date: new Date('2022-02-19'),
  },
  {
    id: 'e5',
    description: 'Another book',
    amount: 18.59,
    date: new Date('2022-02-18'),
  },
  {
    id: 'e6',
    description: 'A pair of trousers',
    amount: 89.29,
    date: new Date('2022-01-05'),
  },
  {
    id: 'e7',
    description: 'Some bananas',
    amount: 5.99,
    date: new Date('2021-12-01'),
  },
  {
    id: 'e8',
    description: 'A book',
    amount: 14.99,
    date: new Date('2022-02-19'),
  },
  {
    id: 'e9',
    description: 'Another book',
    amount: 18.59,
    date: new Date('2022-02-18'),
  },
];

export const ExpensesContext = createContext({
  expenses: [],
  addExpense: ({ description, amount, date }) => {},
  deleteExpense: (id) => {},
  updateExpense: (id, { description, amount, date }) => {},
});

function expensesReducer(state, action) {
  switch (action.type) {
    case 'ADD':
      const id = new Date().toString() + Math.random().toString();
      return [{ ...action.payload, id: id }, ...state];
    case 'UPDATE':
      const updatableExpenseIndex = state.findIndex(
        (expense) => expense.id === action.payload.id
      );
      const updatableExpense = state[updatableExpenseIndex];
      const updatedItem = { ...updatableExpense, ...action.payload.data };
      const updatedExpenses = [...state];
      updatedExpenses[updatableExpenseIndex] = updatedItem;
      return updatedExpenses;
    case 'DELETE':
      return state.filter((expense) => expense.id !== action.payload);
    default:
      return state;
  }
}

function ExpensesContextProvider({ children }) {
  const [expensesState, dispatch] = useReducer(expensesReducer, DUMMY_EXPENSES);

  function addExpense(expenseData) {
    dispatch({ type: 'ADD', payload: expenseData });
  }

  function deleteExpense(id) {
    dispatch({ type: 'DELETE', payload: id });
  }

  function updateExpense(id, expenseData) {
    dispatch({ type: 'UPDATE', payload: { id: id, data: expenseData } });
  }

  const value = {
    expenses: expensesState,
    addExpense: addExpense,
    deleteExpense: deleteExpense,
    updateExpense: updateExpense,
  };

  return (
    <ExpensesContext.Provider value={value}>
      {children}
    </ExpensesContext.Provider>
  );
}

export default ExpensesContextProvider;
```
* Remember that for inputs such as email addresses, ```autoCapitalize``` and ```autoCorrect``` props on ```<TextInput>``` should be disabled so that the user does not have an annoying experience
* Remember when using multiline input, you must set textAlignVertical set to 'top', this is also in the docs - https://reactnative.dev/docs/textinput
* When managing form state which has multiple inputs, you can use this technique to manage state on ```onTextChange``` event effectively, note how we are setting object key dynamically, this is a JS feature and has nothing to do with RN:
<img width="817" alt="image" src="https://user-images.githubusercontent.com/26576978/222095324-a577f89a-bb0b-452c-8a76-c91fac415455.png">

* Custom input we created in the course:
```jsx
import { StyleSheet, Text, TextInput, View } from 'react-native';

import { GlobalStyles } from '../../constants/styles';

function Input({ label, invalid, style, textInputConfig }) {

  const inputStyles = [styles.input];

  if (textInputConfig && textInputConfig.multiline) {
    inputStyles.push(styles.inputMultiline)
  }

  if (invalid) {
    inputStyles.push(styles.invalidInput);
  }

  return (
    <View style={[styles.inputContainer, style]}>
      <Text style={[styles.label, invalid && styles.invalidLabel]}>{label}</Text>
      <TextInput style={inputStyles} {...textInputConfig} />
    </View>
  );
}

export default Input;

const styles = StyleSheet.create({
  inputContainer: {
    marginHorizontal: 4,
    marginVertical: 8
  },
  label: {
    fontSize: 12,
    color: GlobalStyles.colors.primary100,
    marginBottom: 4,
  },
  input: {
    backgroundColor: GlobalStyles.colors.primary100,
    color: GlobalStyles.colors.primary700,
    padding: 6,
    borderRadius: 6,
    fontSize: 18,
  },
  inputMultiline: {
    minHeight: 100,
    textAlignVertical: 'top' // Note this is important for multiline input
  },
  invalidLabel: {
    color: GlobalStyles.colors.error500
  },
  invalidInput: {
    backgroundColor: GlobalStyles.colors.error50
  }
});
```
* Expenses form submit handler, notice the validations and how we have converted string input to appropriate data type:
```jsx
function submitHandler() {
    const expenseData = {
      amount: +inputs.amount.value,
      date: new Date(inputs.date.value),
      description: inputs.description.value,
    };

    const amountIsValid = !isNaN(expenseData.amount) && expenseData.amount > 0;
    const dateIsValid = expenseData.date.toString() !== 'Invalid Date';
    const descriptionIsValid = expenseData.description.trim().length > 0;

    if (!amountIsValid || !dateIsValid || !descriptionIsValid) {
      // Alert.alert('Invalid input', 'Please check your input values');
      setInputs((curInputs) => {
        return {
          amount: { value: curInputs.amount.value, isValid: amountIsValid },
          date: { value: curInputs.date.value, isValid: dateIsValid },
          description: {
            value: curInputs.description.value,
            isValid: descriptionIsValid,
          },
        };
      });
      return;
    }

    onSubmit(expenseData);
  }
```
* To handle form error state, we changed the state of the form as follows, notice now each input key has a value object which stores both value and isValid state, we are utilising this isValid state to make style changes on changing validity:
```jsx
const [inputs, setInputs] = useState({
    amount: {
      value: defaultValues ? defaultValues.amount.toString() : '',
      isValid: true,
    },
    date: {
      value: defaultValues ? getFormattedDate(defaultValues.date) : '',
      isValid: true,
    },
    description: {
      value: defaultValues ? defaultValues.description : '',
      isValid: true,
    },
  });
```
* We created a realtime DB using Firebase, Firebase automatically adds REST APIs in the foreground that communicate with this DB
* You can use the fetch API too in RN but we will use Axios as is standard and popular
* Do not convert useEffect function to an async function, that is discouraged by the React team
* Util ```https.js``` file for working with Firebase, we focused on RN only, so if you want to see how to work with Firebase, use another source:
```javascript
import axios from 'axios';

const BACKEND_URL =
  'https://react-native-course-3cceb-default-rtdb.firebaseio.com';

export async function storeExpense(expenseData) {
  const response = await axios.post(BACKEND_URL + '/expenses.json', expenseData);
  const id = response.data.name;
  return id;
}

export async function fetchExpenses() {
  const response = await axios.get(BACKEND_URL + '/expenses.json');

  const expenses = [];

  for (const key in response.data) {
    const expenseObj = {
      id: key,
      amount: response.data[key].amount,
      date: new Date(response.data[key].date),
      description: response.data[key].description
    };
    expenses.push(expenseObj);
  }

  return expenses;
}

export function updateExpense(id, expenseData) {
  return axios.put(BACKEND_URL + `/expenses/${id}.json`, expenseData);
}

export function deleteExpense(id) {
  return axios.delete(BACKEND_URL + `/expenses/${id}.json`);
}
```
* This is how you can add a spinner in RN:
```jsx
import { View, ActivityIndicator, StyleSheet } from 'react-native';

import { GlobalStyles } from '../../constants/styles';

function LoadingOverlay() {
  return (
    <View style={styles.container}>
      <ActivityIndicator size="large" color="white" />
    </View>
  );
}

export default LoadingOverlay;

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 24,
    backgroundColor: GlobalStyles.colors.primary700,
  },
});
```
* We have used Firebase Authentication (email and password) for another app in the course, see docs
* We can use replace like this here to not have the back button when navigating and essentially replacing the screen, useful for switching between sign in and sign up for example
<img width="480" alt="image" src="https://user-images.githubusercontent.com/26576978/223975101-a3ff2169-1063-4171-afc5-e6614715dcdb.png">

* Auth:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/223975739-ef5c676e-1a58-4f00-8de4-fb54a6788756.png">

* Rules for protecting Firebase APIs:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/224007335-0d9261fe-6a9c-4d50-ba70-11b22fe1a9f4.png">

* I think using Firebase is actually easier than AWS, it seems like this at least in this course, you simply need to send auth url param which is equal to the token received after logging in to access the routes which are protected using the rules above
* Token management
  * The token we're managing in our context and which we're storing on our device could expire. To be precise, it will depend on your backend, whether it expires or not.
  * In Firebase' case, there indeed is a 1h timer on the token. Therefore, the token can still used after 1h but if you're sending it to Firebase, to access some protected resources, after that hour, it won't work anymore. Firebase will deny access.
  * Therefore, you might want to consider doing at least one of two things in your app code:
  * Automatically log the user out after 1h (to avoid that the user thinks he or she is logged in)
    * Can be achieved with help of setTimeout(). You can set a timer which runs in the background and logs the user out after 1h. Of course you should set that timer to a correct duration. If you just got a new token, the duration will be 1h. If you logged a user in because the token was stored on the device, the remaining duration is likely less than 1 hour. You should then calculate the remaining duration by subtracting the current time from the expiration time determine when the token was first received. Therefore, this expiration time should also be derived and stored, whenever a new token is received.
  * Refresh the token and get a new auth token
    * Can be achieved with help of a specific auth API endpoint provided by Firebase - this endpoint: https://firebase.google.com/docs/reference/rest/auth#section-refresh-token
    * Whenever you get an auth token (i.e., after logging in or creating a new user), you also get a refresh token (see the official documentation for logging in and signing up. The refreshToken field in the responses carries a token that can be sent to the refresh token API endpoint (https://firebase.google.com/docs/reference/rest/auth#section-refresh-token) to get a new auth token. For this to work, the refresh token should of course also be stored (in Context and on the device).
    * You could set a timer to refresh the token periodically, or you refresh it whenever the auth token expired.
  * If you have a backend where tokens don't expire, the above steps of course won't apply to you.
  * Alternatively, many third-party services (like Firebase) offer official SDKs which handle token management (and refreshing the token) for you.
* Protecting, routes, and storing tokens on device using a library called AsyncStorage and using another library AppLoading to prevent screen flicker while the app is trying to auto-login:
```jsx
import { useContext, useEffect, useState } from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import { StatusBar } from 'expo-status-bar';
import AsyncStorage from '@react-native-async-storage/async-storage';
import AppLoading from 'expo-app-loading';

import LoginScreen from './screens/LoginScreen';
import SignupScreen from './screens/SignupScreen';
import WelcomeScreen from './screens/WelcomeScreen';
import { Colors } from './constants/styles';
import AuthContextProvider, { AuthContext } from './store/auth-context';
import IconButton from './components/ui/IconButton';

const Stack = createNativeStackNavigator();

function AuthStack() {
  return (
    <Stack.Navigator
      screenOptions={{
        headerStyle: { backgroundColor: Colors.primary500 },
        headerTintColor: 'white',
        contentStyle: { backgroundColor: Colors.primary100 },
      }}
    >
      <Stack.Screen name="Login" component={LoginScreen} />
      <Stack.Screen name="Signup" component={SignupScreen} />
    </Stack.Navigator>
  );
}

function AuthenticatedStack() {
  const authCtx = useContext(AuthContext);
  return (
    <Stack.Navigator
      screenOptions={{
        headerStyle: { backgroundColor: Colors.primary500 },
        headerTintColor: 'white',
        contentStyle: { backgroundColor: Colors.primary100 },
      }}
    >
      <Stack.Screen
        name="Welcome"
        component={WelcomeScreen}
        options={{
          headerRight: ({ tintColor }) => (
            <IconButton
              icon="exit"
              color={tintColor}
              size={24}
              onPress={authCtx.logout}
            />
          ),
        }}
      />
    </Stack.Navigator>
  );
}

function Navigation() {
  const authCtx = useContext(AuthContext);

  return (
    <NavigationContainer>
      {!authCtx.isAuthenticated && <AuthStack />}
      {authCtx.isAuthenticated && <AuthenticatedStack />}
    </NavigationContainer>
  );
}

function Root() {
  const [isTryingLogin, setIsTryingLogin] = useState(true);

  const authCtx = useContext(AuthContext);

  useEffect(() => {
    async function fetchToken() {
      const storedToken = await AsyncStorage.getItem('token');

      if (storedToken) {
        authCtx.authenticate(storedToken);
      }

      setIsTryingLogin(false);
    }

    fetchToken();
  }, []);

  if (isTryingLogin) {
    return <AppLoading />;
  }

  return <Navigation />;
}

export default function App() {
  
  return (
    <>
      <StatusBar style="light" />
      <AuthContextProvider>
        <Root />
      </AuthContextProvider>
    </>
  );
}
```
* We are making an app that allows you to store favourite places (the image of the place clicked from camera), for this expo-camera package can be used, there are similar packages for other native features but for this tutorial expo-camera package is too advanced, so we will use the expo-image-picker package.
* You need to add this in your app.json to properly manage permissions for native device features:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/224472713-056ab053-b774-4e0f-89c4-22399efa4094.png">

* On Android, it automatically asks for permissions, in iOS we have to handle this ourselves
* For location, we are using expo-location package and since our app does not require getting location in the background, the permissions setup is automatic and will be handled by the package itself. For getting position in background, the setup is more challenging. But remember thae even though permissions are declared automatically, you need to still ask for them in code in both Android and iOS.
* To show Google Maps in our app for location (either picked on map or using the locate user feature), we are using the Maps Static API from Google.
* Helper util for working with Google Maps Static API:
```js
const GOOGLE_API_KEY = 'AIzaSyD2mP_sDlloOcwv6OLmYtATOJIcnDhcZcg';

export function getMapPreview(lat, lng) {
  const imagePreviewUrl = `https://maps.googleapis.com/maps/api/staticmap?center=${lat},${lng}&zoom=14&size=400x200&maptype=roadmap&markers=color:red%7Clabel:S%7C${lat},${lng}&key=${GOOGLE_API_KEY}`;
  return imagePreviewUrl;
}

export async function getAddress(lat, lng) {
  const url = `https://maps.googleapis.com/maps/api/geocode/json?latlng=${lat},${lng}&key=${GOOGLE_API_KEY}`;
  const response = await fetch(url);

  if (!response.ok) {
    throw new Error('Failed to fetch address!');
  }

  const data = await response.json();
  const address = data.results[0].formatted_address;
  return address;
}
```
* For showing a full screen map we are using react-native-maps package
* useCallback hook ensures that a function defined inside a component is not re-created unneccesarily
* Remember that when you are navigating, the screens are pushed or popped on top of each other, they are not recreated, so some of your code will not run without the use of useIsFocused hook which is a hook that gives a value true when the screen is in focus and false otherwise. Look at the ```LocationPicker.js``` component and you will understand.
* We are using the Geocoding API to translate corrdinated to human readable addresses
* For storing data on the device, we are using expo-sqlite, as always, look at the official docs
* Interesting new concept, if you do not want to use a parameter but have to write it as such, for example you want only the second argument of a function and not the first, you can do this:
```js
(_, secondArg) => { // the _ signifies here that i have to write it but i dont want to use it
 console.log(secondArg);
}
```
* THe SQLite DB will persist across app restarts but will be deleted on app uninstall
* ImagePicker.js
```jsx
import { Alert, Image, StyleSheet, Text, View } from 'react-native';
import {
  launchCameraAsync,
  useCameraPermissions,
  PermissionStatus,
} from 'expo-image-picker';
import { useState } from 'react';

import { Colors } from '../../constants/colors';
import OutlinedButton from '../UI/OutlinedButton';

function ImagePicker({ onTakeImage }) {
  const [pickedImage, setPickedImage] = useState();

  const [cameraPermissionInformation, requestPermission] =
    useCameraPermissions();

  async function verifyPermissions() {
    if (cameraPermissionInformation.status === PermissionStatus.UNDETERMINED) {
      const permissionResponse = await requestPermission();

      return permissionResponse.granted;
    }

    if (cameraPermissionInformation.status === PermissionStatus.DENIED) {
      Alert.alert(
        'Insufficient Permissions!',
        'You need to grant camera permissions to use this app.'
      );
      return false;
    }

    return true;
  }

  async function takeImageHandler() {
    const hasPermission = await verifyPermissions();

    if (!hasPermission) {
      return;
    }

    const image = await launchCameraAsync({
      allowsEditing: true,
      aspect: [16, 9],
      quality: 0.5,
    });

    setPickedImage(image.uri);
    onTakeImage(image.uri);
  }

  let imagePreview = <Text>No image taken yet.</Text>;

  if (pickedImage) {
    imagePreview = <Image style={styles.image} source={{ uri: pickedImage }} />;
  }

  return (
    <View>
      <View style={styles.imagePreview}>{imagePreview}</View>
      <OutlinedButton icon="camera" onPress={takeImageHandler}>
        Take Image
      </OutlinedButton>
    </View>
  );
}

export default ImagePicker;

const styles = StyleSheet.create({
  imagePreview: {
    width: '100%',
    height: 200,
    marginVertical: 8,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: Colors.primary100,
    borderRadius: 4,
    overflow: 'hidden',
  },
  image: {
    width: '100%',
    height: '100%',
  },
});
```
* LocationPicker.js
```jsx
import { useEffect, useState } from 'react';
import { Alert, View, StyleSheet, Image, Text } from 'react-native';
import {
  getCurrentPositionAsync,
  useForegroundPermissions,
  PermissionStatus,
} from 'expo-location';
import {
  useNavigation,
  useRoute,
  useIsFocused,
} from '@react-navigation/native';

import { Colors } from '../../constants/colors';
import OutlinedButton from '../UI/OutlinedButton';
import { getAddress, getMapPreview } from '../../util/location';

function LocationPicker({ onPickLocation }) {
  const [pickedLocation, setPickedLocation] = useState();
  const isFocused = useIsFocused();

  const navigation = useNavigation();
  const route = useRoute();

  const [locationPermissionInformation, requestPermission] =
    useForegroundPermissions();

  useEffect(() => {
    if (isFocused && route.params) {
      const mapPickedLocation = {
        lat: route.params.pickedLat,
        lng: route.params.pickedLng,
      };
      setPickedLocation(mapPickedLocation);
    }
  }, [route, isFocused]);

  useEffect(() => {
    async function handleLocation() {
      if (pickedLocation) {
        const address = await getAddress(
          pickedLocation.lat,
          pickedLocation.lng
        );
        onPickLocation({ ...pickedLocation, address: address });
      }
    }

    handleLocation();
  }, [pickedLocation, onPickLocation]);

  async function verifyPermissions() {
    if (
      locationPermissionInformation.status === PermissionStatus.UNDETERMINED
    ) {
      const permissionResponse = await requestPermission();

      return permissionResponse.granted;
    }

    if (locationPermissionInformation.status === PermissionStatus.DENIED) {
      Alert.alert(
        'Insufficient Permissions!',
        'You need to grant location permissions to use this app.'
      );
      return false;
    }

    return true;
  }

  async function getLocationHandler() {
    const hasPermission = await verifyPermissions();

    if (!hasPermission) {
      return;
    }

    const location = await getCurrentPositionAsync();
    setPickedLocation({
      lat: location.coords.latitude,
      lng: location.coords.longitude,
    });
  }

  function pickOnMapHandler() {
    navigation.navigate('Map');
  }

  let locationPreview = <Text>No location picked yet.</Text>;

  if (pickedLocation) {
    locationPreview = (
      <Image
        style={styles.image}
        source={{
          uri: getMapPreview(pickedLocation.lat, pickedLocation.lng),
        }}
      />
    );
  }

  return (
    <View>
      <View style={styles.mapPreview}>{locationPreview}</View>
      <View style={styles.actions}>
        <OutlinedButton icon="location" onPress={getLocationHandler}>
          Locate User
        </OutlinedButton>
        <OutlinedButton icon="map" onPress={pickOnMapHandler}>
          Pick on Map
        </OutlinedButton>
      </View>
    </View>
  );
}

export default LocationPicker;

const styles = StyleSheet.create({
  mapPreview: {
    width: '100%',
    height: 200,
    marginVertical: 8,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: Colors.primary100,
    borderRadius: 4,
    overflow: 'hidden',
  },
  actions: {
    flexDirection: 'row',
    justifyContent: 'space-around',
    alignItems: 'center',
  },
  image: {
    width: '100%',
    height: '100%',
    // borderRadius: 4
  },
});
```
* Map.js
```jsx
import { useCallback, useLayoutEffect, useState } from 'react';
import { Alert, StyleSheet } from 'react-native';
import MapView, { Marker } from 'react-native-maps';

import IconButton from '../components/UI/IconButton';

function Map({ navigation, route }) {
  const initialLocation = route.params && {
    lat: route.params.initialLat,
    lng: route.params.initialLng,
  };

  const [selectedLocation, setSelectedLocation] = useState(initialLocation);

  const region = {
    latitude: initialLocation ? initialLocation.lat : 37.78,
    longitude: initialLocation ? initialLocation.lng : -122.43,
    latitudeDelta: 0.0922,
    longitudeDelta: 0.0421,
  };

  function selectLocationHandler(event) {
    if (initialLocation) {
      return;
    }
    const lat = event.nativeEvent.coordinate.latitude;
    const lng = event.nativeEvent.coordinate.longitude;

    setSelectedLocation({ lat: lat, lng: lng });
  }

  const savePickedLocationHandler = useCallback(() => {
    if (!selectedLocation) {
      Alert.alert(
        'No location picked!',
        'You have to pick a location (by tapping on the map) first!'
      );
      return;
    }

    navigation.navigate('AddPlace', {
      pickedLat: selectedLocation.lat,
      pickedLng: selectedLocation.lng,
    });
  }, [navigation, selectedLocation]);

  useLayoutEffect(() => {
    if (initialLocation) {
      return;
    }
    navigation.setOptions({
      headerRight: ({ tintColor }) => (
        <IconButton
          icon="save"
          size={24}
          color={tintColor}
          onPress={savePickedLocationHandler}
        />
      ),
    });
  }, [navigation, savePickedLocationHandler, initialLocation]);

  return (
    <MapView
      style={styles.map}
      initialRegion={region}
      onPress={selectLocationHandler}
    >
      {selectedLocation && (
        <Marker
          title="Picked Location"
          coordinate={{
            latitude: selectedLocation.lat,
            longitude: selectedLocation.lng,
          }}
        />
      )}
    </MapView>
  );
}

export default Map;

const styles = StyleSheet.create({
  map: {
    flex: 1,
  },
});
```
* location.js util:
```js
const GOOGLE_API_KEY = 'AIzaSyD2mP_sDlloOcwv6OLmYtATOJIcnDhcZcg';

export function getMapPreview(lat, lng) {
  const imagePreviewUrl = `https://maps.googleapis.com/maps/api/staticmap?center=${lat},${lng}&zoom=14&size=400x200&maptype=roadmap&markers=color:red%7Clabel:S%7C${lat},${lng}&key=${GOOGLE_API_KEY}`;
  return imagePreviewUrl;
}

export async function getAddress(lat, lng) {
  const url = `https://maps.googleapis.com/maps/api/geocode/json?latlng=${lat},${lng}&key=${GOOGLE_API_KEY}`;
  const response = await fetch(url);

  if (!response.ok) {
    throw new Error('Failed to fetch address!');
  }

  const data = await response.json();
  const address = data.results[0].formatted_address;
  return address;
}
```
* database.js util
```js
import * as SQLite from 'expo-sqlite';

import { Place } from '../models/place';

const database = SQLite.openDatabase('places.db');

export function init() {
  const promise = new Promise((resolve, reject) => {
    database.transaction((tx) => {
      tx.executeSql(
        `CREATE TABLE IF NOT EXISTS places (
          id INTEGER PRIMARY KEY NOT NULL,
          title TEXT NOT NULL,
          imageUri TEXT NOT NULL,
          address TEXT NOT NULL,
          lat REAL NOT NULL,
          lng REAL NOT NULL
        )`,
        [],
        () => {
          resolve();
        },
        (_, error) => {
          reject(error);
        }
      );
    });
  });

  return promise;
}

export function insertPlace(place) {
  const promise = new Promise((resolve, reject) => {
    database.transaction((tx) => {
      tx.executeSql(
        `INSERT INTO places (title, imageUri, address, lat, lng) VALUES (?, ?, ?, ?, ?)`,
        [
          place.title,
          place.imageUri,
          place.address,
          place.location.lat,
          place.location.lng,
        ],
        (_, result) => {
          resolve(result);
        },
        (_, error) => {
          reject(error);
        }
      );
    });
  });

  return promise;
}

export function fetchPlaces() {
  const promise = new Promise((resolve, reject) => {
    database.transaction((tx) => {
      tx.executeSql(
        'SELECT * FROM places',
        [],
        (_, result) => {
          const places = [];

          for (const dp of result.rows._array) {
            places.push(
              new Place(
                dp.title,
                dp.imageUri,
                {
                  address: dp.address,
                  lat: dp.lat,
                  lng: dp.lng,
                },
                dp.id
              )
            );
          }
          resolve(places);
        },
        (_, error) => {
          reject(error);
        }
      );
    });
  });

  return promise;
}

export function fetchPlaceDetails(id) {
  const promise = new Promise((resolve, reject) => {
    database.transaction((tx) => {
      tx.executeSql(
        'SELECT * FROM places WHERE id = ?',
        [id],
        (_, result) => {
          const dbPlace = result.rows._array[0];
          const place = new Place(
            dbPlace.title,
            dbPlace.imageUri,
            { lat: dbPlace.lat, lng: dbPlace.lng, address: dbPlace.address },
            dbPlace.id
          );
          resolve(place);
        },
        (_, error) => {
          reject(error);
        }
      );
    });
  });

  return promise;
}
```
* How Expo works:
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/26576978/225819410-de0f7348-aa44-44c8-8e38-b82a2656549e.png">

* XYZ
