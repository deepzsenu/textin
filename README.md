<!-- PROJECT TITLE -->
<br />
<div align="center">
<img src="./images/logo.png" alt="Logo" width="80" height="80">
<h1 align="center">Spotlist Frontend</h1>
</div>

<!-- TABLE OF CONTENTS -->

## Table of contents

---

1. [Getting Started](#getting-started)
   1. [Installations](#installations)
   2. [Running the App](#running-the-app)
   3. [React Native crash course](#crash-course)
2. [How to Use Github](#how-to-use-github)
   1. [General Rules](#general-rules)
   2. [Git Workflow](#git-workflow)
   3. [Writing good commit messages](#writing-good-commit-messages)
3. [How to Use Trello](#how-to-use-trello)
   1. [Creating a Task](#creating-a-task)
4. [How the Code Works](#how-the-code-works)
   1. [Adding a Page](#adding-a-page)
   2. [Redux Tutorial](#redux-tutorial)
5. [Spotlist APK](#spotlist-apk)
   1. [Installations-APK](#installations-apk)
6. [Common Issues](#common-issues)
   1. [SDK Version No Longer Supported](#sdk-version-no-longer-supported)

<!-- GETTING STARTED -->

## Getting Started <a name="getting-started"></a>

---

### Installations <a name="installations"></a>

- **IOS Simulator**
  - Follow these instructions https://docs.expo.dev/workflow/ios-simulator/
- **Android Emulator**
  - Follow these instructions https://developer.android.com/studio
- **Phyiscal device**
  - install expo go app

### Running the App <a name="running-the-app"></a>

1. Install Node and npm https://docs.npmjs.com/downloading-and-installing-node-js-and-npm
2. Clone the project, ensuring that the project name in the terminal is 'spotlist-mobile' instead of 'spotlist-mobile-master.' Make sure you have Git Bash installed if you cannot run the git command like 'git clone,'
3. Open up the code in your IDE(VSCode), go to your terminal and cd the project
4. add an extension called "prettier" in the VSCode
5. Install all dependencies by running `npm i --legacy-peer-deps`
   - if `npm i --legacy-peer-deps` didn't work or you encountered: `Uncaught TypeError: Cannot read properties of 'null' (reading 'children')`, then you can try to downgrade npm version to v16.14.0 or using NVM to install a different nodejs version. You can also run `npm install -g npm@8.3.0`
6. Run `npx expo start`
7. Press `i` from the terminal for the ios simulator or `a` for the android emulator
8. If the app doesn't start, try closing and reopening the app, VSCode, or cold booting the device
   - Alternatively, try running `npx expo r -c` to clear the cache

### React Native crash course <a name="crash-course"></a>

Watch this video:

[![](https://yt3.googleusercontent.com/z8m8Nc31z3PdVqbMPzS_MEApQKgXjP6faDEto0lIPXy9S50QSSMtCYHZ5V-opH73q9BAjxpb_g=s176-c-k-c0x00ffffff-no-rj)](https://www.youtube.com/watch?v=VozPNrt-LfE&ab_channel=Academind "React Native Crash Course | Build a Complete App")

<!-- HOW TO USE GITHUB -->

## How to Use Github <a name="how-to-use-github"></a>

---

### General Rules <a name="general-rules"></a>

- Branches should have the same name as the tasks on Trello
- Delete your branch after merging into masters
- Resolve potential conflicts while rebasing and before making a Pull Request

### Git Workflow <a name="git-workflow"></a>

1. Pull from the master --- if aborts, then you can stash ---> pull ---> unstash
2. Fix merge conflicts on local
3. Add, commit, and push your local branch to your remote GitHub branch(make sure no new changes from master before pushing)
4. Make pull request
5. Review by two people
6. merge to master
7. Delete local branch
8. Pull inside the master branch
9. Create a new local branch and switch to it
   ```
     git checkout -b <branchname>
   ```

### Writing good commit messages <a name="writing-good-commit-messages"></a>

- Separate the subject from the body with a newline between the two
- Give a 1-3 sentence description of the commit
  - Alternatively use bullets

<!-- HOW TO USE TRELLO -->

## How to Use Trello <a name="how-to-use-trello"></a>

---

<img src="./images/trello.PNG" alt="trello">

Each column is kind of self-explanatory, but its getting explained anyways

- **To Do**: Tasks that aren't being worked on yet
- **Doing**: Tasks that people are currently working on
- **Blocked**: Tasks that peaople are stuck on
- **In Review**: Tasks that are finished but awaiting a review from 2 other engineers
- **INTEGRATION | CONNECT**:
- **Done**: Its done lol

### Creating a Task <a name="creating-a-task"></a>

1. Click on the **...** button on top right of the **To Do** column and click **Add Card**
2. Give the task a title: adding `[BE]` means it's a backend task; `[FE]` is frontend
3. After the task is created hover over the card and click the little pencil button then edit card
4. Add a short summary of the task
5. On the right under **Add to card**:
   1. Click **Members** to assign someone to a task
   2. Click **Dates** to set an estimated completion date\
      <img src="./images/trello_task.PNG" alt="trello">

<!-- HOW THE CODE WORKS -->

## How The Code Works <a name="how-the-code-works"></a>

---

**Username and password for testing:**

username: mayfourth@gmail.com
password: password

```javascript react native
import { useState } from "react";
import { StatusBar } from "expo-status-bar";
import {
  StyleSheet,
  Text,
  View,
  TextInput,
  Button,
  Image,
  KeyboardAvoidingView,
  TouchableOpacity,
  ImageBackground,
  ScrollView,
  SafeAreaView,
} from "react-native";
import { render } from "react-dom";
import styles from "./../../styles/index";
import axios from "axios";
import { useDispatch, useSelector } from "react-redux";
import useAuth from "./auth/useAuth";
import Signup from "./SignUp";
import { AntDesign } from "@expo/vector-icons";
import { NavigationContainer, useNavigation } from "@react-navigation/native";
import { createStackNavigator } from "@react-navigation/stack";
////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////
//
// Section one, import statements
//
////////////////////////////////////////////////////////////////////////

export default function Login() {
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  //
  // Section two, export default statement for a function
  //
  ////////////////////////////////////////////////////////////////////////
  const [username, setUsername] = useState("");
  const [password, setPassword] = useState("");
  const { logIn } = useAuth();

  const refreshKey = useSelector((state) => state.refreshStatus.value);
  const dispatch = useDispatch();
  const navigation = useNavigation();
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  //
  // Section three, stating your variables and the method used for
  // changining your variable's value,
  //
  // we are using useState for variables local to the login page,
  // username is a variable while setUsername is a function
  // used to change the value of the state. Look at TextInput
  // below in the return statement to see how they're used. The useState
  // lines of code should be the first things that appear after the default export
  // function line of code
  //
  // useSelector is used for the redux, redux is used to allow certain
  // variables to be accessable throughout the entire application
  // refreshKey is used to send back to backend for a new access token
  // which allow access to the django backend
  //
  // isLogged is used to tell if the user is logged in (look at AppUse.js
  // for more info)
  //
  ////////////////////////////////////////////////////////////////////////

  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////

  const baseURL =
    "http://django-jwt-env.eba-hisvhgpd.us-west-2.elasticbeanstalk.com/api/";
  //"http://127.0.0.1:8000/api/";

  const axiosInstance = axios.create({
    baseURL: baseURL,
    timeout: 10000,
    headers: {
      "Content-Type": "application/json",
      accept: "application/json",
    },
  });

  axiosInstance.interceptors.response.use(
    (response) => response,
    (error) => {
      try {
        const originalRequest = error.config;

        // Prevent infinite loops early

        if (
          error.response.status === 401 &&
          originalRequest.url === baseURL + "token/refresh/"
        ) {
          Promise.reject(error);
          return <LoginNavigator />;
        }

        if (
          error.response.data.code === "token_not_valid" &&
          error.response.status === 401 &&
          error.response.statusText === "Unauthorized"
        ) {
          const refreshToken = refreshKey;

          if (refreshToken) {
            const tokenParts = JSON.parse(atob(refreshToken.split(".")[1]));

            // exp date in token is expressed in seconds, while now() returns milliseconds:
            const now = Math.ceil(Date.now() / 1000);
            console.log(tokenParts.exp);

            if (tokenParts.exp > now) {
              return axiosInstance
                .post("token/refresh/", { refresh: refreshToken })
                .then((response) => {
                  dispatch(access(response.data.access));
                  dispatch(refresh(response.data.refresh));

                  axiosInstance.defaults.headers["Authorization"] =
                    "JWT " + response.data.access;
                  originalRequest.headers["Authorization"] =
                    "JWT " + response.data.access;

                  return axiosInstance(originalRequest);
                })
                .catch((error) => {
                  console.error(Error(error));
                });
            } else {
              console.log("Refresh token is expired", tokenParts.exp, now);
              window.location.href = "/login/";
            }
          } else {
            console.log("Refresh token not available.");
            window.location.href = "/login/";
          }
        }

        // specific error handling done elsewhere
        return Promise.reject(error);
      } catch (error) {
        console.error(Error(error));
      }
    }
  );
  // the above axios code is here because it cant be exported from a file
  // due to the axios being made for object oriented programming
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  /*
  in case you want to write the handleSubmit in a different format
  //
  const handleSubmitWThen = () => {
    axiosInstance
      .post("token/obtain/", {
        username: username,
        password: password,
      })
      .then((result) => {
        axiosInstance.defaults.headers["Authorization"] =
          "JWT " + result.data.access;

        dispatch(access(result.data.access));
        dispatch(refresh(result.data.refresh));
        dispatch(login());
        console.log("refresh");
        console.log(result.data.refresh);
      })
      .catch((error) => {
        console.error(Error(error));
      });
  };
  */

  const handleSubmit = async () => {
    try {
      const response = await axiosInstance.post(
        "token/obtain/",
        JSON.stringify({
          username: username,
          password: password,
        })
      );
      axiosInstance.defaults.headers["Authorization"] =
        "JWT " + response.data.access;
      console.log(response.data.refresh);
      dispatch(access(response.data.access));
      dispatch(refresh(response.data.refresh));
      dispatch(login());
      console.log("refresh");
      console.log(response.data.refresh);
      return response;
    } catch (error) {
      console.error(Error(error));
    }
  };
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  ////////////////////////////////////////////////////////////////////////
  //
  // Section four, the fuctions or const's the page will use
  // to log the user in,
  //
  // handleSubmit sends the login info to the django backend, sets the
  // redux value of the access and refresh key to the value of the keys
  // sent by the django backend. And sets isLogged to true
  //
  ////////////////////////////////////////////////////////////////////////
  return (
    <KeyboardAvoidingView
      behavior={Platform.OS == "ios" ? "padding" : "height"}
      style={styles.container}
    >
      <ImageBackground
        source={require("./../../assets/Splash_Page.png")}
        style={styles.backgroundImg}
      >
        <View style={styles.logoContainer}>
          <Image
            style={styles.img}
            source={require("./../../assets/spotlistlogo_withname.png")}
          />
        </View>
        <View style={styles.textContainer}>
          <TextInput
            placeholder="User Name"
            placeholderTextColor="#86b4b5"
            returnKeyType="next"
            keyboardType="default"
            autoCapitalize="none"
            style={styles.input}
            value={username}
            onChangeText={setUsername}
          />

          <TextInput
            placeholder="Password"
            secureTextEntry={true}
            placeholderTextColor="#86b4b5"
            autoCapitalize="none"
            style={styles.input}
            value={password}
            onChangeText={setPassword}
          />

          <TouchableOpacity style={styles.button} onPress={handleSubmit}>
            <Text style={styles.text}>LOGIN</Text>
          </TouchableOpacity>

          <View style={styles.rowContainer}>
            <View style={styles.rowContainer}>
              <TouchableOpacity
                onPress={() => navigation.push("Type of Account")}
              >
                <Text style={styles.buttonText}>Create an</Text>
                <Text style={styles.buttonText}>Account</Text>
              </TouchableOpacity>
            </View>
            <View style={styles.rowContainer2}>
              <TouchableOpacity
                onPress={() => navigation.push("Forgot Password")}
              >
                <Text style={styles.buttonText}>Forgot</Text>
                <Text style={styles.buttonText}>Password?</Text>
              </TouchableOpacity>
            </View>
          </View>

          <View style={styles.rowContainer}>
            <TouchableOpacity style={styles.rowContainer}>
              <Text style={styles.buttonText}>Login With </Text>
              <AntDesign
                name="facebook-square"
                size={24}
                color="black"
                style={styles.imgSmall}
              />
            </TouchableOpacity>
          </View>
        </View>
      </ImageBackground>
    </KeyboardAvoidingView>
  );
  ///////////////////////////////////////////////////////////////////////
  ///////////////////////////////////////////////////////////////////////
  //
  // Section five, the return statement, this is the code that is loaded
  // onto the phone screen
  //
  // The main difference in this section are the functions inside the
  // onPress and onChangeText elements of the TouchableOpacity and
  // TextInput. And the value in the TextInput
  //
  //////////////////////////////////////////////////////////////////////
  //////////////////////////////////////////////////////////////////////
}

{
  //////////////////////////////////////////////////////////////////////
  //////////////////////////////////////////////////////////////////////
  //
  // Section six, stylesheet for above containers
  //
  //////////////////////////////////////////////////////////////////////
  //////////////////////////////////////////////////////////////////////
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#106868",
    justifyContent: "center",
    alignItems: "center",
  },

  img: {
    height: 200,
    width: 100,
  },

  bottombtnContainer: {
    flexDirection: "row",
    justifyContent: "center",
  },
  loginbtnContainer: {
    justifyContent: "center",
  },

  input: {
    alignSelf: "center",
    width: 300,
    height: 40,
    paddingTop: 20,
    marginBottom: 20,
    borderBottomWidth: 2,
    borderBottomColor: "#86b4b5",
  },
  loginbtnContainer: {
    alignSelf: "center",
    borderColor: "#76be77",
    borderRadius: 10,
    backgroundColor: "#07494e",
    width: 250,
    height: 50,
    borderWidth: 4,
  },
  loginbtnText: {
    color: "yellow",
    textAlign: "center",

    color: "#86b4b5",
    fontSize: 30,
  },
  createaccbtnContainer: {
    paddingTop: 50,
    width: 90,
    height: 90,
  },
  createaccText: {
    color: "#86b4b5",
    fontSize: 16,
    textDecorationLine: "underline",
  },
});
```

Importing resuable css component unless you are 100% sure it will be reused. Otherwise, the css should be added within each page.

### Adding a Page <a name="adding-a-page"></a>

check https://reactnavigation.org/docs/stack-navigator/

### Redux <a name="redux-tutorial"></a>

Watch this video:

[![](https://i.ytimg.com/vi/iBUJVy8phqw/mqdefault.jpg)](https://www.youtube.com/watch?v=iBUJVy8phqw "Redux Tutorial (with Redux Toolkit)")

<!-- SPOTLIST APK -->

## Spotlist APK <a name="spotlist-apk"></a>

This will show you how to generate an APK for the android play store

### Requirements

[expo](https://docs.expo.io/get-started/installation/) to develop your app

### Installations-APK

after [expo](https://docs.expo.io/get-started/installation/) is installed, open up your terminal and cd into a folder you want the repository to be in.

```git
git clone git@github.com:Surfield/spotlist-mobile.git
```

```git
cd spotlist-mobile
git checkout daniel-branch
```

Now Instal Expo CLI

run `git npm install -g expo-cli` or `git yarn global add expo-cli` to get it

### Configure app.json

```json
{
  "expo": {
    "name": "Your App Name",
    "icon": "./path/to/your/app-icon.png",
    "version": "1.0.0",
    "slug": "your-app-slug",
    "ios": {
      "bundleIdentifier": "com.yourcompany.yourappname",
      "buildNumber": "1.0.0"
    },
    "android": {
      "package": "com.yourcompany.yourappname",
      "versionCode": 1
    }
  }
}
```

your final app.json should look similar to the following

```json
{
  "expo": {
    "name": "Spotlist",
    "slug": "spotlist-slug",
    "version": "1.0.0",
    "orientation": "portrait",
    "icon": "./assets/icon.png",
    "splash": {
      "image": "./assets/spotlistlogo_withname.png",
      "resizeMode": "contain",
      "backgroundColor": "#ffffff"
    },
    "updates": {
      "fallbackToCacheTimeout": 0
    },
    "assetBundlePatterns": ["**/*"],
    "ios": {
      "supportsTablet": true
    },
    "web": {
      "favicon": "./assets/favicon.png"
    },
    "android": {
      "package": "com.spotlistinc.spotlist",
      "versionCode": 1
    }
  }
}
```

to generate the apk, run the following in the terminal

```git
expo build:android -t apk
```

### Saving The APK

After building the APK there will be a message with a link

![readme2](./assets/readme/readme2.png)

Copy and paste this link into your web browser and the APK will be downloaded to your computer

### Saving the Keystore

you will be asked if you want a new keystore or if you want to use an old one. if you generate a new one make sure to save it. you will not be able to change the app on the playstore if the keystore is lost

```git
expo fetch:android:keystore
```

will show you your keystore

<!-- COMMON ISSUES -->

## Common Issues <a name="common-issues"></a>

### SDK Version No Longer Supported

check https://docs.expo.dev/workflow/upgrading-expo-sdk-walkthrough/
