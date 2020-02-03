# react-semantic-ui-firebase-authentication

## Features

* uses:
  * only React (create-react-app)
  * firebase
  * react-router
  * semantic UI
* features:
  * Sign In
  * Sign Up
  * Sign Out
  * Password Forget
  * Password Change
  * Verification Email
  * Protected Routes with Authorization
  * Roles-based Authorization
  * Social Logins with Google, Facebook and Twitter
  * Linking of Social Logins on Account dashboard
  * Auth Persistence with Local Storage
  * Database with Users and Messages

## Installation

* `git clone https://github.com/shakacu/React-Firebase-Dashboard.git`
* `cd React-Firebase-Dashboard`
* `yarn install`
* `yarn start`
* visit http://localhost:3000

### Firebase Configuration

* copy/paste your configuration from your Firebase project's dashboard into one of these files
  * *src/components/Firebase/firebase.js* file
  * *.env* file
  * *.env.development* and *.env.production* files

*src/components/Firebase/firebase.js* could look like the following then:

```
const config = {
    apiKey: "AIzaSyCw3Wz1WDd15rRxJYCgOIKItPIeNGDYHdo",
    authDomain: "dashboard-0923.firebaseapp.com",
    databaseURL: "https://dashboard-0923.firebaseio.com",
    projectId: "dashboard-0923",
    storageBucket: "dashboard-0923.appspot.com",
    messagingSenderId: "657957574605",
    appId: "1:657957574605:web:95cf2bc79a303b92edd684"
};
```

### Activate Sign-In Methods

![firebase-enable-google-social-login_640](https://user-images.githubusercontent.com/2479967/49687774-e0a31e80-fb42-11e8-9d8a-4b4c794134e6.jpg)

### Security Rules

*In the case of Firebase RealTime Database*

```
{
  "rules": {
    ".read": false,
    ".write": false,
    "users": {
      "$uid": {
        ".read": "$uid === auth.uid || root.child('users/'+auth.uid).child('roles').hasChildren(['ADMIN'])",
        ".write": "$uid === auth.uid || root.child('users/'+auth.uid).child('roles').hasChildren(['ADMIN'])"
      },
      ".read": "root.child('users/'+auth.uid).child('roles').hasChildren(['ADMIN'])",
      ".write": "root.child('users/'+auth.uid).child('roles').hasChildren(['ADMIN'])"
    },
    "messages": {
      ".indexOn": ["createdAt"],
      "$uid": {
        ".write": "data.exists() ? data.child('userId').val() === auth.uid : newData.child('userId').val() === auth.uid"
      },
      ".read": "auth != null",
      ".write": "auth != null",
    },
  }
}
```
