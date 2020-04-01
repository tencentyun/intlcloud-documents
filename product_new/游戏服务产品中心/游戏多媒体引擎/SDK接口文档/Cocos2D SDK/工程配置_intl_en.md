This document describes how to configure a Cocos2d project for the GME APIs for Cocos2d.



## SDK Preparations
1. Download the applicable demo and SDK. For more information, please see [Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).
2. Decompress the obtained SDK resources.
3. The folder contains:
 - GMESDK: GME SDK framework file.
 - GMECocosDemo: GME SDK demo project.

>The SDK supports compilation on macOS.




## iOS Xcode Configuration

1. Add the framework to the Xcode project and set the header file import location (the framework file in the `GMESDK` folder must be added to the project).
2. Add dependent libraries as shown below:
![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)

## Android Configuration

1. Add `gmesdk.jar` to the libs library.
![](https://main.qcloudimg.com/raw/167b3fb575b65539aeaf9c700383e7c8.png)
2. Import the `so` file into `Activity` as shown below:
```
public class AppActivity extends Cocos2dxActivity {
    static final String TAG = "AppActivity";
    static OpensdkGameWrapper gameWrapper ;
    static {
        OpensdkGameWrapper.loadSdkLibrary();
    }
}
```
3. Initialize in the `oncreate` function exactly in the following sequence:
```
protected void onCreate(Bundle savedInstanceState) {
        super.setEnableVirtualButton(false);
        super.onCreate(savedInstanceState);

        // Initialize exactly in the following sequence
        gameWrapper = new OpensdkGameWrapper(this);
        runOnGLThread(new Runnable() {
            @Override
            public void run() {
                gameWrapper.initOpensdk();
            }
        });
}
```
4. Configure your project for compilation options by referring to the `Android.mk` in the GME Demo for Cocos.
 - Path: GMECocos/GMECocosDemo/proj.android-studio/app/jni/Android.mk
 - Path to the `preBuild.mk` file: /Users/username/Downloads/GMECocos/GMESDK/android/bin/preBuild.mk


## Exporting for Different Platforms

Project configuration is required before you can export executables from the Cocos2d engine for different platforms:

| OS | Project Configuration           
| ------------- |:-------------:|
| Android |[Android Project Configuration](https://intl.cloud.tencent.com/document/product/607/10783)|
| iOS     	|[iOS Project Configuration](https://intl.cloud.tencent.com/document/product/607/10783)|
| macOS     	|[macOS Project Configuration](https://intl.cloud.tencent.com/document/product/607/10783)|





