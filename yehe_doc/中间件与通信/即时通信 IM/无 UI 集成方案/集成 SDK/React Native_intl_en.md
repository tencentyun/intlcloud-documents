This document describes how to quickly integrate the Tencent Cloud IM SDK into your React Native project.

## Environment Requirements

| Platform     | Version                                                      |
| ------------ | ------------------------------------------------------------ |
| React Native | 2.2.0 or later                                               |
| Android      | Android Studio 3.5 or later; devices on Android 4.1 or later for applications |
| iOS          | Xcode 11.0 or later. For testing with a real device, make sure that your project has a valid developer signature. |

## Integrating the IM SDK

You can directly integrate the IM SDK for React Native by using nmp.

### Integration through npm

Enter the following command in the terminal window:

```
# npm
npm install react-native-tim-js

# yarn
yarn add react-native-tim-js


# RN >= 0.60
cd ios && pod install

# RN < 0.60
react-native link react-native-tim-js
```

### Importing and initializing the SDK

```javascript
import { TencentImSDKPlugin } from "react-native-tim-js";
```
