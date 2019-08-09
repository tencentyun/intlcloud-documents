## Overview

Thank you for using Tencent Cloud Game Multimedia Engine (GME) SDK. This document provides project configuration that makes it easy for Cocos2D developers to debug and access the APIs for GME.

## SDK Preparation

Download applicable Demo and SDK from [Download Instructions](https://intl.cloud.tencent.com/document/product/607/18521).

### Decompressing SDK resources

1. Decompress obtained SDK resources
2. The folders are as follows:

| Folder Name | Description
| ----------------------|-----------------------------------        |
| TMG_SDK                    |Mobile Gaming SDK framework file        |
| TMGCocosDemo          | Mobile Gaming SDK project sample	|

## System Requirement

The SDK can be compiled on Mac.

## iOS Xcode Preparations

### 1. Import SDK related framework file

Add the framework to Xcode project and set the reference location of the header file.

GMESDK.framework, the Mobile Gaming SDK framework file in TMG_SDK folder, must be added to the project.

### 2. Add dependent libraries
Refer to the figure below:  
![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)

## Android Preparations

### 1. Add gmesdk.jar to libs library.
![](https://main.qcloudimg.com/raw/167b3fb575b65539aeaf9c700383e7c8.png)

### 2. Import so file to Activity.

```
public class AppActivity extends Cocos2dxActivity {
    static final String TAG = "AppActivity";
    static OpensdkGameWrapper gameWrapper ;
    static {
        OpensdkGameWrapper.loadSdkLibrary();
    }
}
```

### 3. Initialization

Initialization is in oncreate function and the sequence cannot be wrong.
```
protected void onCreate(Bundle savedInstanceState) {
        super.setEnableVirtualButton(false);
        super.onCreate(savedInstanceState);

        //Initialization, the sequence cannot be wrong
        gameWrapper = new OpensdkGameWrapper(this);
        runOnGLThread(new Runnable() {
            @Override
            public void run() {
                gameWrapper.initOpensdk();
            }
        });
}
```

## Export to different platforms

To export to different platforms from the Cocos2D engine, you need to perform the corresponding project configuration:

|Platform       | Project configuration           
| ------------- |:-------------:|
| Android |[Android Project Configuration Documentation](https://intl.cloud.tencent.com/document/product/607/15203)|
| iOS     	|[iOS Project Configuration Documentation](https://intl.cloud.tencent.com/document/product/607/15219)|
| Mac     	|[Mac Project Configuration Documentation](https://intl.cloud.tencent.com/document/product/607/18617)|