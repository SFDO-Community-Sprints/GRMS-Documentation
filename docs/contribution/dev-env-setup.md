---
layout: default
title: Development Environment Setup
parent: Contribution
nav_order: 1
has_children: false
---
# Development Environment Setup

* [Prerequisites](#prerequisites)
* [Setup](#setup)
* [Run the app](#run-the-app)

## Prerequisites
* Complete [Salesforce Initial Setup](./Salesforce-Initial-Setup) and [Heroku Initial Setup](./Heroku-Initial-Setup).
* Go to https://expo.io/ and sign up. Then install the Expo client on your [iOS](https://apps.apple.com/jp/app/expo-client/id982107779)/[Android]( https://play.google.com/store/apps/details?id=host.exp.exponent) device.

## Setup
### 1. Install git (for Windows)
https://gitforwindows.org/

### 2. Install node.js
https://nodejs.org/en/

### 3. Install yarn
https://classic.yarnpkg.com/en/docs/install

### 4. Install expo-cli
```
yarn add global expo-cli
```

### 5. Clone the repository
```
git clone https://github.com/SFDO-Community-Sprints/GrassrootsMobileSurveyApp.git
```

### 6. Install plugins
On the mobile app directory, run the following command.

```
yarn install
```

### 7. Create an environment variable file
Create a file called `.env` in the root folder of the repository and copy and paste this line into it:

```.env
LOGGING_LEVEL=DEBUG
```

## Run the app
First make sure that your computer and mobile device are connected to the same network.

In the root folder of the repository, run the following command.

```
yarn start --clear
```

A new browser tab will open. Scan the QR code at the bottom left (or follow the alternative instructions there). The app will launch on your device.

![Metro bundler](https://user-images.githubusercontent.com/1404346/93891832-cdb50a80-fd26-11ea-82c6-8852d08b5fbc.png)
