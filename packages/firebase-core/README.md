# @nativescript/firebase-core

```cli
npm install @nativescript/firebase-core
```

## Usage

### Android
Ensure `google-services.json` file located in `App_Resources/Android/src`.

### iOS
Ensure `GoogleService-Info.plist` file located in `App_Resources/iOS`.

### Initialize Default App

```ts
import { firebase } from '@nativescript/firebase-core'
const defaultApp = await firebase().initializeApp();
```

### Initialize Secondary App

```ts
import { firebase, FirebaseOptions } from '@nativescript/firebase-core'
const config = new FirebaseOptions()
const secondaryApp = await firebase().initializeApp(config, 'SECONDARY_APP');
```

### Updating from legacy firebase plugin

Remove the old plugin of ```json "@nativescript/firebase" ``` from the package.json file.
The new library is now split into separate libraries.  For example, messaging, analytics and crashaltyics are imported as their own individual library.  Such libraries are imported like the following ->

```json    
"@nativescript/firebase-analytics": "^2.4.4",
"@nativescript/firebase-crashlytics": "^2.4.4",
"@nativescript/firebase-messaging": "^2.4.4",
"@nativescript/firebase-messaging-core": "^2.4.4"
```

In main.ts replace ```json require("@nativescript/firebase");``` with ```json require("@nativescript/firebase-core");```


Where firebase is called, replace 
    ```ts 
    firebase.init({
      showNotifications: showNotifcationAccepted,
      showNotificationsWhenInForeground: false,
      analyticsCollectionEnabled: true,
      crashlyticsCollectionEnabled: true
    });
```

with 
  ```ts
    firebase().initializeApp().then( app => {
      firebase().messaging().showNotificationsWhenInForeground = false,
      firebase().analytics().setAnalyticsCollectionEnabled(true),
      firebase().crashlytics().setCrashlyticsCollectionEnabled(true)
    });
  ```

Replace ```ts firebase.addOnMessageReceivedCallback((message: any) => {``` with ```ts firebase().messaging().onMessage( message => { ```


For Android, move the google-services.json file to ```Android -> src```


## License

Apache License Version 2.0
