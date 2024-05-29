# Cordova App Template
Using Cordova we can build native apps using any frontend web framework such as Angular. The final result is a Android .aab file or an iOS file that can be uploaded to the Google Play Store or Apple App Store.


## Angular for the User Interface
npm run build

We can put any HTML, CSS, and JS into the Cordova project. So in your Angular build it is importaqnt we note the location of the output and the location of the input for Cordova.

This is why we need to do this in the Cordova build steps so we get recent files.
```
cp -r dist/cordovatest/* cordova-project/www/
```


## Android (.aab)
npm run build:android
```
ng build && cp -r dist/cordovatest/* cordova-project/www/ && cd cordova-project && cordova build android --release
```


## iOS
npm run build:ios

```
ng build && cp -r dist/cordovatest/* cordova-project/www/ && cd cordova-project && cordova build ios --release
```

This will give error on Linux/Windows saying xcodebuild was not found. Please install version 11.0.0 or greater from App Store. This is why are going to use https://codemagic.io/ to build on a Mac. The documentation for CodeMagic says to add a codemagic.yaml to the project root.


## How to Setup a New Project
```
npm install -g cordova
cordova create cordova-project
cd cordova-project
cordova platform add android
cd ..
ng build --prod
cd cordova-project
cordova build android --release
```

**Sign the AAB File**: If you don't already have a keystore, create one with this command:

```
keytool -genkey -v -keystore my-release-key.keystore -keyalg RSA -keysize 2048 -validity 10000 -alias my-key-alias
```

Then, sign the AAB file using the `jarsigner` tool:

```
jarsigner -verbose -sigalg SHA256withRSA -digestalg SHA-256 -keystore my-release-key.keystore platforms/android/app/build/outputs/bundle/release/app-release.aab my-key-alias
```