# Deployment

This document will guide you through the steps for running the app on your machine.

## Prerequisites

Before you start, install
- [Node.js](https://nodejs.org/en)
- [npm](https://www.npmjs.com/)

or check if you have already installed both by running the following commands in the terminal:
    
    node -v
    npm -v

Install the Ionic CLI to use ionic commands:

    npm i -g @ionic/cli

Navigate to the momenTUM-app folder and install the dependencies:

    cd .../momenTUM-app
    npm i


Run a development server with live-reload in your browser:

    ionic serve

## Native Platforms

The projects for iOS and Android are build using [Capacitor](https://capacitorjs.com/).
Consider looking into their documentation for more information.

### Build and run on iOS

> **Note**: iOS apps can only be developed on macOS with [Xcode](https://developer.apple.com/xcode/) installed.
> Make sure the command-line tools are selected for use:
>
>       xcode-select --install

Build the native project:

    ionic cap build ios


Run the app from Xcode first.
> You may need to sign the app before being able to run it.
> You may also need to create an emulator beforehand.

Once you've managed to run the app in Xcode, you can close Xcode and run it from the command line with live reload functionality:

    ionic cap run ios -l

For debugging, you can use the _Safari_ Browser:
1. Open Safari
2. In the menubar select _develop_ > _name_of_emulator_ > localhost

If you encounter further problems or want more documenation on deployment, read the [Ionic docs for iOS development](https://ionicframework.com/docs/developing/previewing). 

## Android

Install [Android Studio](https://developer.android.com/studio/install) and the Android SDK by opening Android Studio. It will lead you through the installation.
Open ~/.bashrc, ~/.bash_profile, or similar bash startup scripts and add the following lines:

    export ANDROID_SDK_ROOT=/Path/to/android/sdk
    export PATH=$PATH:$ANDROID_SDK_ROOT/tools/bin
    export PATH=$PATH:$ANDROID_SDK_ROOT/platform-tools
    export PATH=$PATH:$ANDROID_SDK_ROOT/emulator

In _Android Studio_, open the _Virtual Device Manager_ and create a _Virtual Device_. Run the Device and keep the emulator running.

Build the android native project by running the following inside of the momenTUM-app directory:

    ionic cap build android

Run the app with live-reload:

    ionic cap run android -l

For debugging, open [chrome://inspect](chrome://inspect) with the Chrome Web Browser.

If you encounter any problems or want further documentation, read the [Ionic docs](https://ionicframework.com/docs/developing/android).