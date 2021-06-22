This document describes how to integrate GME SDK into an Android project so that the Android developers can easily debug and integrate the APIs for Game Multimedia Engine (GME).

## Preparing SDK

1. Download the applicable demo and SDK. For more information, please see [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).
2. Decompress the obtained SDK resources.
3. The SDK development resources are in the `libs` folder.

>?The SDK supports running on Android 4.2 or later. However, hardware encoding can be enabled only on Android 4.3 (API 18) or later.

## Configuration Guide

#### Importing SDK files

1. Copy the gmesdk.jar file under the libs directory to the libs directory of the Android project.
2. **Copy the library file of the corresponding architecture based on the project requirements**. For example, if the project requires the armeabi-v7a architecture, you need to copy the library file under the armeabi-v7a directory to the armeabi-v7a directory in the project. If there is no armeabi-v7a directory in the project, please create one.

#### Project configuration

Add the code that imports the library to build.gradle under the App directory of the project.  
```
sourceSets {
        main {
            jniLibs.srcDirs = ['libs']
        }
}
```

