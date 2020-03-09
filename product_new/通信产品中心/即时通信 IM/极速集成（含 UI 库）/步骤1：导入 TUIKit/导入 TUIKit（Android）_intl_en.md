## Development Environment Requirements

- Android Studio 3.3.2
- Gradle-4.1


## Integration Description

TUIKit can be integrated through gradle, aar, or module source code.

### Gradle integration

```
dependencies {
    ...
     compile 'com.tencent.imsdk:tuikit:xxx version'
    ...
}
```
Replace the `xxx` in `xxx version` with the [latest aar version number](https://github.com/tencentyun/TIMSDK/tree/master/Android/SDK).

### Module source code integration

```
implementation project(':tuikit')
```

### aar integration

1. Specify the name of the aar under the libs folder.
```
android {
    ...
    repositories {
        flatDir {
            dirs 'libs'
        }
    }
}
```

2. Add dependencies.
```
dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    ....
    implementation(name: 'tuikit-xxx version', ext: 'aar')
}
```
Replace the `xxx` in `tuikit-xxx version` with the [latest aar version number](https://github.com/tencentyun/TIMSDK/tree/master/Android/SDK).


## Initialization

Initialize in onCreate for the app:

```java
public class DemoApplication extends Application {

    public static final int SDKAPPID = 0; // Your SDKAppID

    @Override
    public void onCreate() {
        super.onCreate();

       // Set Config according to your needs
       TUIKitConfigs configs = TUIKit.getConfigs();
       configs.setSdkConfig(new TIMSdkConfig(SDKAPPID));
       configs.setCustomFaceConfig(new CustomFaceConfig());
       configs.setGeneralConfig(new GeneralConfig());

       TUIKit.init(this, SDKAPPID, configs);
    }
}
```

Description of the init method:

<pre>
/**
 * TUIKit initialization function
 *
 * @param context  App context, which is usually the ApplicationContext of the app
 * @param sdkAppID SDKAppID that is assigned to you when registering the app in Tencent Cloud
 * @param configs TUIKit configuration items. Use default settings for these configuration items in most cases. For special configuration, see <a href="https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/TUIKit/com/tencent/qcloud/tim/uikit/config/TUIKitConfigs.html">API Documentation</a>.
 */
public static void init(Context context, int sdkAppID, TUIKitConfigs configs)
</pre>

