---
layout: post
title: Getting started with Firebase tools
date: 2020-04-14 03:14 +0000
---

## Install

In alpine linux 

```bash
apk add npm --update --no-cache --quiet
npm install -g firebase-tools
```

## Login fetch token

### Prepare

Make sure `9005` port is open. 

If using docker 
```bash
docker run -it -v 9005:9005
```

### Login and Token

```bash

firebase login:ci

```

```bash

Visit this URL on this device to log in:
https://accounts.google.com/o/oauth2/auth?client_id=563584335869-fgrhgmd47bqnekij5i8b5pr03ho849e6.apps.googleusercontent.com&scope=email%20openid%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloudplatformprojects.readonly%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Ffirebase%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform&response_type=code&state=440385764&redirect_uri=http%3A%2F%2Flocalhost%3A9005

Waiting for authentication...

✔  Success! Use this token to login on a CI server:

1//0gJSgFM6hf9EmCgYIARAAGBASNwF-L9Irzno8K6HCtmiWxiOUgS6b9KfTxSxRQD-L26ucReSVNcx-rUPG2W2KexgC3Y0EjARq7KA

Example: firebase deploy --token "$FIREBASE_TOKEN"
```


Copy link and open on browser. 

```bash
export FIREBASE_TOKEN=token_hash
```


## Hosting

### Init hosting service

```bash

$ firebase init


     ######## #### ########  ######## ########     ###     ######  ########
     ##        ##  ##     ## ##       ##     ##  ##   ##  ##       ##
     ######    ##  ########  ######   ########  #########  ######  ######
     ##        ##  ##    ##  ##       ##     ## ##     ##       ## ##
     ##       #### ##     ## ######## ########  ##     ##  ######  ########

You're about to initialize a Firebase project in this directory:

  /firebase/hosting

Before we get started, keep in mind:

  * You are currently outside your home directory

? Which Firebase CLI features do you want to set up for this folder? Press Space to select features, then Enter to confirm your choices. (Press <space> to select, <a> to toggle all, <i> to invert selection)
 ◯ Database: Deploy Firebase Realtime Database Rules
❯◯ Firestore: Deploy rules and create indexes for Firestore
 ◯ Functions: Configure and deploy Cloud Functions
 ◯ Hosting: Configure and deploy Firebase Hosting sites
 ◯ Storage: Deploy Cloud Storage security rules
 ◯ Emulators: Set up local emulators for Firebase features


```

#### `firebase.json`

```json
{
  "hosting": {
    "public": "public",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ],
    "rewrites": [
      {
        "source": "**",
        "destination": "/index.html"
      }
    ]
  }
}
```

#### .firebaserc

```json
{
  "projects": {
    "default": "project-id"
  }
}

```


```bash
firebase deploy
```

## Functions

#### `firebase.json`

```json
{
  "functions": {
    "predeploy": [
      "npm --prefix \"$RESOURCE_DIR\" run lint"
    ]
  }
}
```

#### .firebaserc

```json
{
  "projects": {
    "default": "project-id"
  }
}

```


## Auth 

```html
<script src="https://cdn.firebase.com/libs/firebaseui/3.5.2/firebaseui.js"></script>
<link type="text/css" rel="stylesheet" href="https://cdn.firebase.com/libs/firebaseui/3.5.2/firebaseui.css" />
```

```html
<script>
    var ui = new firebaseui.auth.AuthUI(firebase.auth());

    ui.start('#firebaseui-auth-container', {
      signInSuccessUrl: 'https://taste-firebase-e78f2.web.app',
      signInOptions: [
        {
          provider: "password"
        }
      ]
      // Other config options...
    });
  });
</script>
```
