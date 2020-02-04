---
title: AppDelegate
permalink: /docs/app-delegate/
---

#### On app startup, following logic and services are executed

### 1. Realm Migration
The app checks for the `Realm` database version, and if the current installed version is less than that of current build, it is migrated to the latest version.

This part is important whenever any changes are made in the Realm models in the app. The `Realm` version should be increased every time any changes are made in `Realm` models. Failing to do this, the app will face crashes on client devices.

### 2. IQKeyboardManager
`IQKeyboardManager` is used for handling keyboard related animations and utilities. It is enabled at the launch of the app.

### 3. Social Media Integration
Facebook, Twitter and Google Maps/Places libraries are invoked at this stage with their respective app keys. The callback URL's are also configured in this file.

### 4. Enable Push Notifications
Prompt user for providing permission to receive and show push notifications. When the device token is received, it is saved to UserDefaults with the key `DEVICE_TOKEN`.

### 5. SDWebImage
For handling image downloads from url's and caching them in memory, a third party library - `SDWebImage` is used. We faced an issue where the imageViews didn't refresh the images every time. To overcome this issue, we clear the image cache on the app launch.
```
SDImageCache.shared().clearMemory()
SDImageCache.shared().clearDisk(onCompletion: nil)
```

### 6. Check logged in user
Check if the user is logged in the app.

If logged in:
* Set landing TabBar screen as rootViewController by passing window instance to `SideDrawerController`.
* Set the user data from UserDefaults into the `UserProfile` shared object.
* Start the logging mechanism, using `GTLumberJack`.

If not logged in:
* Set Login screen as rootViewController.

### 7. App wide services
Following services are launched with the app:
* `LocationEngine`: A separate file is created as an extension for AppDelegate, for managing the location updates in the app.
* `ContactsEngine`: Fetching contacts from device, filtering and storing in app db, sending it to server.
* `ChatEngine`: For managing XMPP based one-one and group chat.

### 8. App launched using Push Notification
Check for `aps` key in launch options. If present, that means the app is launched using notification. Parse the content, and the xml from the content to find the relevant module, and set the current screen accordingly.

### 9. Check app version
For notifying and forcing the user to update the app in case of available update on AppStore, we use this feature.
* An api call is made to the server to fetch the latest app store app build number.
* This build number is then compared with the app's build number.
* If the app's version is lower than that of the version available on App Store, the screen `UpdateAppViewController` is set as root, such that the user cannot perform any other action other than updating it to the latest version.   
