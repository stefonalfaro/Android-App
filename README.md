# Cordova Test
Yes, in your project root, you'll create a new Cordova project. Here's a step-by-step guide with more detailed instructions to ensure everything is clear:

1. **Install Cordova**: If you haven't installed Cordova yet, you can install it globally:

   ```bash
   npm install -g cordova
   ```

2. **Create a New Cordova Project**: Navigate to your Angular project's root directory and create a new Cordova project inside it. This will create a Cordova project with the necessary directory structure.

   ```bash
   cd /path/to/your/angular-project
   cordova create cordova-project
   cd cordova-project
   ```

3. **Add the Android Platform**: Add the Android platform to your Cordova project:

   ```bash
   cordova platform add android
   ```

4. **Build Your Angular App**: Navigate back to your Angular project directory and build your Angular app for production:

   ```bash
   cd ..
   ng build --prod
   ```

   This will create a `dist/your-app-name` directory with your Angular build files.

5. **Copy Angular Build Files to Cordova**: Copy the contents of the Angular `dist/your-app-name` directory to the `www` directory of your Cordova project:

   ```bash
   cp -r dist/your-app-name/* cordova-project/www/
   ```

6. **Build the Cordova Project for Android**: Navigate back to your Cordova project directory and build the project:

   ```bash
   cd cordova-project
   cordova build android --release
   ```

7. **Generate an AAB File**: To generate an Android App Bundle (AAB) file, use the following command:

   ```bash
   cordova build android --release -- --packageType=bundle
   ```

   This will create an AAB file in the `platforms/android/app/build/outputs/bundle/release/` directory.

8. **Sign the AAB File**: If you don't already have a keystore, create one with this command:

   ```bash
   keytool -genkey -v -keystore my-release-key.keystore -keyalg RSA -keysize 2048 -validity 10000 -alias my-key-alias
   ```

   Then, sign the AAB file using the `jarsigner` tool:

   ```bash
   jarsigner -verbose -sigalg SHA256withRSA -digestalg SHA-256 -keystore my-release-key.keystore platforms/android/app/build/outputs/bundle/release/app-release.aab my-key-alias
   ```