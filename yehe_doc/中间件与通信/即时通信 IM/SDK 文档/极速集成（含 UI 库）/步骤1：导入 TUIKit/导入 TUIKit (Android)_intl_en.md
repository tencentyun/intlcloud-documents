## Environment Requirements

- Android Studio 3.6.1
- Gradle-5.1.1


## Integration Description

 `TUIKit` can be integrated using the `module` source code.

### Integrating the module source code
[TUIKit source code download address](https://github.com/tencentyun/TIMSDK/tree/master/Android/TUIKit)

1. Download the `Demo` source code from `GitHub`. Note that you need to copy the `tuikit` folder to a directory of your project and use it as a module.

2. Add the following to `settings.gradle`:
```groovy
include ':tuikit'
```
3. Add the following to `build.gradle` in `APP`:
```groovy
dependencies {
    implementation project(':tuikit')
    
    ......
}
```
4. Modify the `build.gradle` file in `tuikit`: replace the version numbers in the file with those in `build.gradle` in `app`. The following is an example:
```groovy
android {
    compileSdkVersion 30

    defaultConfig {
        minSdkVersion 19
        targetSdkVersion 30
        versionCode 1
        versionName "1.0"

        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }

   ......
}
```

5. Add the following to the `gradle.properties` file to replace the class in `AndroidX` with that in `support`:
```properties
android.enableJetifier=true
```
6. Add the following to the `build.gradle` file of the `root` project to add the `maven` repository:
```properties
allprojects {
    repositories {
        maven { url "https://mirrors.tencent.com/nexus/repository/maven-public/" }

        ......
    }
}
```
7. Sync the project, and compile and run it.

## Initialization

Perform initialization in `onCreate` of `Application`:

```java
public class DemoApplication extends Application {

    public static final int SDKAPPID = 0; // Your SDKAppID

    @Override
    public void onCreate() {
        super.onCreate();

       // Set parameters as needed
       TUIKitConfigs configs = TUIKit.getConfigs();
       configs.setSdkConfig(new V2TIMSDKConfig());
       configs.setCustomFaceConfig(new CustomFaceConfig());
       configs.setGeneralConfig(new GeneralConfig());

       TUIKit.init(this, SDKAPPID, configs);
    }
}
```

The `init` method is described as follows:

```java
/**
 * Initializes TUIKit
 *
 * @param context    //App context, usually corresponds to ApplicationContext
 * @param sdkAppID     //`SDKAppID` assigned to you when you register the app in Tencent Cloud
 * @param configs    //Relevant configuration items of TUIKit. Usually, you can use the default configuration.
 */
public static void init(Context context, int sdkAppID, TUIKitConfigs configs)
```

