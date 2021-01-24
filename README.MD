### Project Setup

1) Install `Expo` client

	- this behaves as a `wrapper` around your `React Native App`
	- `Expo` is a third-party service that provides a convenient development workflow to reduce the complexity of implementing `React Native` features from scratch
	- `Expo` limits the full control available in the `React Native` development environments available in `Xcode` and `Android Studio`

		~~~ bash
		npm install expo-cli --global
		~~~

2) Create a `React Native` project using `expo-init  [projectName]`

   - choose the `blank` template
   - in the underlined `name` field, enter a name. This will show up in the browser tab when the project is launched

		~~~ bash
		expo init reactnative_components_exp
		~~~

3) Launch project into the browser
	- use `yarn start` or `npm start` from the terminal
	- this will launch in the browser on port `http://localhost:19002/`
	- use `CTRL + C` to quit
	- while launched, open `VS Code` to see the default code and review `App.js`

4) Launch the project on your iPhone
	- Install `Expo client` from the app store
	- Open the `iPhone camera app` and hold it over the `QR code`

5) Launch the project on the Xcode iPhone simulator
	- install Xcode
	- make sure `Command Line Tools` is installed under `Preferences/Locations`

	- Launch the iPhone simulator by either:
		- select `Run on iOS simulator` from the `Expo client` browser window on port `http://localhost:19002/`
    	- pressing `i` from the terminal window after starting project

6)  Launch the project on the Android simulator
	- install Android Studio
    - under Configure-SDK Manager, select several Android SDK Platform packages
    - under Configure-AVD Manager, select the `play` button on one of the installed `Virtual Devices`

  	- Launch the iPhone simulator by either:
        - select `Run on Android simulator` from the `Expo client` browser window on port `http://localhost:19002/`
        - pressing `a` from the terminal window after starting project

### App Setup

1) Update `App.js`

    - a custom `Header` component is imported
    - the `flex: 1` style defines the proportion of available space this component will fill
    - the `title` prop is passed into the `Header` component

    ~~~ js
    // App.js
    import { StatusBar } from 'expo-status-bar';
    import React from 'react';
    import { StyleSheet, Text, View } from 'react-native';
    import Header from './components/Header';

    export default function App() {
    return (
        <View style={styles.screen}>
            <Header title = "Guess a Number" />
        </View>
    );
    }

    const styles = StyleSheet.create({
    screen: {
        flex: 1,

    },
    });
    ~~~

2) Create custom Header component

    ~~~ js
    // components/Header.js
    import React from 'react';
    import {View, Text, StyleSheet} from 'react-native';

    const Header = props => {
        return (
            <View style = {styles.header}>
                <Text style = {styles.headerTitle} > {props.title} </Text>
            </View>    
        )
    }

    export default Header;

    const styles = StyleSheet.create({
        header: {
            width: '100%',
            height: 90,
            paddingTop: 36, 
            backgroundColor: '#f7290b',
            alignItems: 'center',
            justifyContent: 'center',


        },
        headerTitle: {
            color: 'black',
            fontSize: 18
        }

    })
    ~~~

3) Create StartGameScreen component

    - style attributes that are prefixed with `shadow` only work with `iOS`
    - the `elevation` style only works with `Android`

    ~~~ js
    import React from 'react';
    import {View, Text, TextInput, StyleSheet, Button} from 'react-native';

    const StartGameScreen = props => {
        return (
            <View style = {styles.screen}>
                <Text style = {styles.title} > Start a New Game </Text>
                <View style = {styles.inputContainer}>
                    <Text> Select a Number </Text> 
                    <TextInput />
                    <View style = {styles.buttonContainer}>
                        <Button title = 'Reset' onPress = {() => {}} />
                        <Button title = 'Confirm' onPress = {() => {}} />
                    </View>                
                </View>
            </View>       
        )
    };

    const styles = StyleSheet.create({
        screen: {
            flex: 1,
            padding: 10,
            alignItems: 'center',

            },
        inputContainer: {
            backgroundColor: 'white',
            padding: 22,
            borderRadius: 10,   
            width: 300,
            maxWidth: '80%',
            alignItems: 'center',
            // shadow____   only works on iOS
            shadowColor: 'black',
            shadowOffset: {
                width: 0,
                height: 2,
            },
            shadowRadius: 6,
            shadowOpacity: 0.26,
            // these only work on Android
            elevation: 5,

            },
        title: {
            fontSize: 22,
            marginVertical: 10,

        
            },
        buttonContainer: {
            flexDirection: 'row',
            width: '100%',
            justifyContent: 'space-between',
            paddingHorizontal: 15,

        
            },

    })

    export default StartGameScreen;
    ~~~

4) Create `Card` component

    - overriding styles defined in `Card` with props is done using the `spread` operator 

        ~~~ js
        style = {{...styles.card, ...props.style}}
        ~~~

    - IMPORTANT !! putting spaces around `{props.children}` results in a `Component Exception Error`
    <img src = 'reactnative_guess_num/screenshots/Spacing_error_Text_Component.png' width = '40%'/>

    ~~~ js
    <View style = {{...styles.card, ...props.style}}> {props.children} </View>
    ~~~

    - add import and replace `View` with `Card` component in `StartGameScreen.js`
    - add the  `style` prop to the imported `Card` component

        ~~~ js
        // StartGameScreen.js
        ...
        import Card from '../components/Card';

        const StartGameScreen = props => {
            return (
                <View style = {styles.screen}>
                    <Text style = {styles.title} > Start a New Game </Text>
                    <Card style = {styles.inputContainer}>

                            <Text> Select a Number </Text> 
                            <TextInput />
                            <View style = {styles.buttonContainer}>
                                <Button title = 'Reset' onPress = {() => {}} />
                                <Button title = 'Confirm' onPress = {() => {}} />
                            </View>

                    </Card>
                </View>
            );
        };
        ...
        ~~~
  
    - the completed `Card` component

        ~~~ js
        // Card.js
        import React from 'react';
        import {View, StyleSheet} from 'react-native';


        const Card = props => {

            return (
                <View style = {{...styles.card, ...props.style}}> {props.children} </View>
            );

        };


        const styles = StyleSheet.create({
            card: {
                backgroundColor: 'white',
                padding: 22,
                borderRadius: 10,   
                // shadow____   only works on iOS
                shadowColor: 'black',
                shadowOffset: {
                    width: 0,
                    height: 2,
                },
                shadowRadius: 6,
                shadowOpacity: 0.26,
                // these only work on Android
                elevation: 5,

            },

        });


        export default Card;
        ~~~



        TEST COMMIT 2
        AGAIN 2
