## Android Project Configuration
### System requirement
The UGSV SDK is supported on Android 4.0.3 (API level 15) and above, but hardware encoding can be enabled only on Android 4.3 (API level 18) or above.

### Development environment
Below are the environment requirements for SDK development. You don’t need to meet the same requirements for application development, but make sure that your application is compatible with the SDK.

- Android NDK: android-ndk-r12b
- Android SDK Tools: android-sdk_25.0.2
- minSdkVersion: 15
- targetSdkVersion: 26
- Android Studio (Android Studio is recommended. You can also use Eclipse + ADT.)

[](id:step1)
### Step 1. Integrate the SDK
<dx-tabs>
::: AAR Integration
1. **Create a project**
![](https://main.qcloudimg.com/raw/ca473c3bf484da3d7d959dbb83b192b1.png)
2. **Configure the project**
  1. In `build.gradle` of your project directory, add code that references the AAR file:
```
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    // Import the SDK AAR file. Replace `x.y.zzzz` in `LiteAVSDK_UGC_x.y.zzzz` with the latest version number.
    compile(name: 'LiteAVSDK_UGC_7.4.9211', ext: 'aar')
    ...
}
```
  2. Add `flatDir` to `build.gradle` of your project directory, and specify the local repository:
```
allprojects {
  repositories {
      jcenter()
      flatDir {
          dirs 'libs'
      }
  }
}
```
  3. Under `defaultConfig` in `build.gradle` of your project directory, specify architectures compatible with the NDK:
```
defaultConfig {
    ...
    ndk {
        abiFilters "armeabi", "armeabi-v7a"
    }
}
```
  4. Click **Sync Now** to build the project.
:::
::: JAR + SO Integration
1. **Library description**
Decompress the ZIP file, and you will find a `libs` directory that contains a JAR file and several SO files, as shown below:
<table>
<tr><th>JAR</th><th>Description</th></tr>
<tr><td>liteavsdk.jar </td><td >Core library for the UGSV SDK for Android </td>
</tr></tbody>
</table>
<table>
<tr><th>SO</th><th>Description</th></tr>
<tr><td> libliteavsdk.so</td><td >Core component of the UGSV SDK </td></tr>
<tr><td>libtxffmpeg.so</td><td >FFmpeg basic library (ijk), which is used for VOD and solves some video format compatibility issues</td>
</tr><tr><td>libtxplayer.so</td><td >Open-source ijkplayer library, which is used for VOD and solves some video format compatibility issues</td>
</tr><tr><td>  libtxsdl.so</td><td >Open-source ijkplayer libraryy, which is used for VOD and solves some video format compatibility issues </td>
</tr></table>
2. **Copy files**
    If you haven’t specified a JNI library loading path for your project, we recommend that you copy the above JAR and SO files to **Demo\app\src\main\jniLibs**, which is Android Studio’s default path for loading JNI libraries.
    If you use the enterprise edition SDK, after decompressing the ZIP file, you will find an `assets` directory in addition to the JAR and SO files. The directory contains files that enable animated effects, which you must copy to the `assets` directory of your project. For details, please see [Animated Effects and Face Changing - Configuring the Project](https://intl.cloud.tencent.com/document/product/1069/38031).
3. **Configure your project**
In `build.gradle` of your project directory, add code that references the JAR and SO files.
```
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    // Import the JAR file of the UGSV SDK
    compile fileTree(dir: 'src/main/jniLibs', includes: ['*.jar'])
    ...
}
```
4. **Reduce APK size**
The SO files, which provide the audio/video codec library, image processing library, and audio processing component, take up a big chunk of the SDK’s size. If UGSV-related features are not the main features of your application, you may consider loading the SO files online to reduce your APK size.
  1. **Upload SO files**
Upload the SO files in the SDK package to COS and note the download address, e.g., `http://xxx-appid.cossh.myqcloud.com/so_files.zip`.
  2. **Show loading animation**
When users start the SDK, for example, to play a video, show on the UI a loading animation and a message that relevant modules are being loaded.
    3 **Download SO files**
While users wait, your application can download the SO files from `http://xxx-appid.cossh.myqcloud.com/so_files.zip` and save them in your project directory, for example, in the `files` folder of your application’s root directory. Given the possibility of DNS hijacking by ISPs, please check the integrity of the SO files after download.
    4 **Load SO files**
After all the SO files are in place, call `setLibraryPath` of `TXLiveBase` to set the SDK’s library path to the directory of the downloaded SO files. The SDK will load from the directory the SO files needed to enable the requested UGSV feature.
:::
</dx-tabs>

[](id:step2)
### Step 2. Configure application permissions

Configure application permissions in `AndroidManifest.xml`. Audio/Video applications generally need the following permissions:

```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.CALL_PHONE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.READ_LOGS" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.Camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```

[](id:step3)
### Step 3. Configure the license
1. Follow the steps in [License Application](https://intl.cloud.tencent.com/document/product/1069/38041) to apply for a license, and copy the key and license URL in the [VOD console](https://console.cloud.tencent.com/vod/license), as shown below:
![](https://main.qcloudimg.com/raw/7bbf7fb9e3d13944bc3b6823fd786269.png)
2. Before you use UGSV features in your application, we recommend that you complete the following configuration in `- Application onCreate()`:
```
public class DemoApplication extends Application {
    String ugcLicenceUrl = ""; // Enter the license URL obtained from the console.
    String ugcKey = "";        // Enter the license key obtained from the console.

    @Override
    public void onCreate() {
        super.onCreate();
        TXUGCBase.getInstance().setLicence(instance, ugcLicenceUrl, ugcKey);
    }
}
```

> ?If you use a v4.7 license and have updated the SDK to v4.9, you can click **Switch to New License** in the console to generate a new license key and URL. A new license can be used only on v4.9 or above and should be configured as described above.

[](id:step4)
### Step 4. Print logs
You can enable/disable console log printing and set the log level in `TXLiveBase`. See the sample code below.
- **setConsoleEnabled**
Sets whether to print the SDK logs in the Android Studio console.
- **setLogLevel**
Sets whether to allow the SDK to print local logs. By default, the SDK writes logs to the SD card in **Android/data/com.tencent.liteav.demo/files/log/tencent/liteav**. We recommend that you enable local log printing and provide the log file after a problem occurs so that we can offer technical support.
- **Viewing log files**
To reduce the storage space taken up by log files, the UGSV SDK encrypts local logs and limits their number. You need a log [decompression tool](http://dldir1.qq.com/hudongzhibo/log_tool/decode_mars_log_file.py) to view the content of log files.
```
TXLiveBase.setConsoleEnabled(true);
TXLiveBase.setLogLevel(TXLiveConstants.LOG_LEVEL_DEBUG);
```

[](id:step5)
### Step 5. Build and run your project

Call an SDK API in your project to get the SDK version number and verify whether your project is correctly configured.

1. **Import the SDK**:
Import the SDK class in `MainActivity.java`:
```
import com.tencent.rtmp.TXLiveBase;
```
2. **Call the API**:
Call `getSDKVersioin` in `onCreate` to get the version number:
```
String sdkver = TXLiveBase.getSDKVersionStr();
Log.d("liteavsdk", "liteav sdk version is : " + sdkver);
```
3. **Build and run the project**:
If the above steps are performed correctly, you will build the project successfully and, after running it, you will see the following log information in `logcat`.
`09-26 19:30:36.547 19577-19577/ D/liteavsdk: liteav sdk version is : 7.4.9211`

[](id:que1)
### Troubleshooting
After importing the UGSV SDK, when you build and run your project, if the following error occurs:

```
Caused by: android.view.InflateException:
Binary XML file #14:Error inflating class com.tencent.rtmp.ui.TXCloudVideoView
```

Follow the steps below to troubleshoot the problem:

1. Check whether you have copied the JAR and SO files to the `jniLibs` directory.
2. If you use the AAR method to integrate all features of the SDK, check in `defaultConfig` of `build.gradle` if the x64 SO libraries have been filtered out. The audio processing component, which enables the co-anchoring feature, does not support x64 phones currently.
```
defaultConfig {
    ...   
    ndk {
        abiFilters "armeabi", "armeabi-v7a"
    }
}
```
3. Check if the package name of the SDK has been added to the “do not obfuscate” list.
```
-keep class com.tencent.** { *;}
```
4. [Configure](https://intl.cloud.tencent.com/document/product/1069/37914) packaging options for your application.
![](https://main.qcloudimg.com/raw/94320d4327cf90f19f98b8715e6b466a.png)

[](id:module)
## Integrating UGSV Modules
This section describes how to quickly integrate the UGSV SDK into your existing project to enable a complete range of UGSV features including shooting, editing, and composition. The code and resources mentioned in this section can be found in the [SDK ZIP file](https://intl.cloud.tencent.com/document/product/1069/37914) and the [UGSV demo](https://github.com/tencentyun/UGSVSDK).

[](id:integrated)
### Integrating `UGCKit`

[](id:UGCKit_step1)
#### Step 1. Create a project (Empty Activity)
1. Create an empty Android Studio project. You can name it `ugc` and give it a custom package name. Make sure the project can be built and run successfully.
2. Configure `build.gradle` of the project.
```
// Top-level build file where you can add configuration options common to all sub-projects/modules.
buildscript {
    repositories {
        google()
        jcenter()

    }
    dependencies {
        # Copying starts.
        classpath 'com.android.tools.build:gradle:3.6.1'
        # Copying ends.
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        google()
        jcenter()
        # Copying starts.
        flatDir {
            dirs 'src/main/jniLibs'
            dirs project(':ugckit').file('libs')
        }
        # Copying ends.
        jcenter() // Warning: this repository is going to shut down soon
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}

# Copying starts.
ext {
    compileSdkVersion = 25
    buildToolsVersion = "25.0.2"
    supportSdkVersion = "25.4.0"
    minSdkVersion = 16
    targetSdkVersion = 23
    versionCode = 1
    versionName = "v1.0"
    proguard = true
    rootPrj = "$projectDir/.."
    ndkAbi = 'armeabi-v7a'
    noffmpeg = false
    noijkplay = false
    aekit_version = '1.0.16-cloud'
    liteavSdk="com.tencent.liteav:LiteAVSDK_Professional:latest.release"
}
# Copying ends.
```
3. Configure `build.gradle` of your application.
```
plugins {
    id 'com.android.application'
}

android {
    # Copying starts.
    compileSdkVersion = rootProject.ext.compileSdkVersion
    buildToolsVersion = rootProject.ext.buildToolsVersion
    # Copying ends.
    defaultConfig {
        applicationId "com.yunxiao.dev.liteavdemo"
        # Copying starts.
        minSdkVersion rootProject.ext.minSdkVersion
        targetSdkVersion rootProject.ext.targetSdkVersion
        versionCode rootProject.ext.versionCode
        versionName rootProject.ext.versionName
        renderscriptTargetApi = 19
        renderscriptSupportModeEnabled = true
        multiDexEnabled = true
        ndk {
            abiFilters rootProject.ext.ndkAbi
        }
         # Copying ends.
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}

    # If you use the Enterprise or Enterprise Pro edition of the SDK, add the code below (not required for the Lite or Basic edition).
    packagingOptions {
        pickFirst '**/libc++_shared.so'
        doNotStrip "*/armeabi/libYTCommon.so"
        doNotStrip "*/armeabi-v7a/libYTCommon.so"
        doNotStrip "*/x86/libYTCommon.so"
        doNotStrip "*/arm64-v8a/libYTCommon.so"
    }
    # If you use the Enterprise or Enterprise Pro edition of the SDK, add the above code (not required for the Lite or Basic edition).

dependencies {
    # Copying starts.
    compile fileTree(include: ['*.jar'], dir: 'libs')
    compile fileTree(include: ['*.jar'], dir: 'src/main/jniLibs')
    compile 'com.mcxiaoke.volley:library:1.0.19'
    compile 'com.android.support:design:25.3.1'
    compile 'com.android.support:recyclerview-v7:25.3.1'
    compile 'com.google.code.gson:gson:2.3.1'
    compile 'com.github.bumptech.glide:glide:3.7.0'
    compile 'com.github.ctiao:dfm:0.4.4'
    compile project(':ugckit')
    compile 'com.android.support.constraint:constraint-layout:1.1.3'
    # Copying ends.
}
```
4. Specify the Gradle version.
```
distributionUrl=https\://services.gradle.org/distributions/gradle-5.6.4-bin.zip
```



[](id:UGCKit_step2)
#### Step 2. Import modules
1. Copy `ugckit module` to the `ugc` directory of your newly created project.
2. Copy `beautysettingkit module` to the `ugc` directory of your newly created project.
3. Import `ugckit` to `settings.gradle` of the project.
4. In `UGC/settings.gradle` of the project, import the modules below:
```
include ':ugckit'
include ':beautysettingkit'
```
5. Add `ugckit` as a dependency for the app modules of your project.
```
compile project(':ugckit')
```

[](id:UGCKit_step3)
#### Step 3. Apply for a license
Before using `UGCKit`, you must configure the license. For how to obtain a license, please see [License Application](https://intl.cloud.tencent.com/document/product/1069/38041).


[](id:fun)

### Enabling shooting, importing, clipping, and special effects

[](id:initialize)
#### 1. Configure the license and initialize `UGCKit`
Configure the license in `Application.java` and initialize `UGCKit`.

```
// Configure the license
TXUGCBase.getInstance().setLicence(this, ugcLicenceUrl, ugcKey);
// Initialize `UGCKit`
UGCKit.init(this);
```

[](id:record)
#### 2. Implement video shooting
1. Create an XML file for shooting and add the code below:
``` xml
<com.tencent.qcloud.ugckit.UGCKitVideoRecord
    android:id="@+id/video_record_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
```
2. Create an empty theme for shooting in `res/values/styles.xml` and inherit the default shooting theme of `UGCKit`.
```
<style name="RecordActivityTheme" parent="UGCKitRecordStyle"/>
```
3. Create an activity for shooting, inherit `FragmentActivity`, implement the `ActivityCompat.OnRequestPermissionsResultCallback` API, get a `UGCKitVideoRecord` object, and set the callback.
```
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    // You must configure the theme in the code (`setTheme`) or in `AndroidManifest` (android:theme).
    setTheme(R.style.RecordActivityTheme);
    setContentView(R.layout.activity_video_record);
    // Get `UGCKitVideoRecord` 
    mUGCKitVideoRecord = (UGCKitVideoRecord) findViewById(R.id.video_record_layout);
    // Listen for shooting events
    mUGCKitVideoRecord.setOnRecordListener(new IVideoRecordKit.OnRecordListener() {
        @Override
        public void onRecordCanceled() {
            // Shooting was canceled.
        }

        @Override
        public void onRecordCompleted(UGCKitResult result) {
            // Shooting was completed.
        }
    });
}

@Override
protected void onStart() {
    super.onStart();
    // Get whether the camera and audio recording permissions are granted. For details, see `Github/Demo`.
    if (hasPermission()) {
        // `UGCKit` takes over the shooting lifecycle. For details, see `Github/Demo`.
        mUGCKitVideoRecord.start();
    }
}

@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
    if (grantResults != null && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
        mUGCKitVideoRecord.start();
    }
}
```

**The UI view looks like this:**
![Image description](https://main.qcloudimg.com/raw/077aa281195ba33fcaa67da2a13b1b60.png)

[](id:v_import)
#### 3. Implement video importing
1. Create an XML file and add the code below:
```xml
 <com.tencent.qcloud.ugckit.UGCKitVideoPicker
        android:id="@+id/video_picker"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
```
2. Create an empty theme in `res/values/styles.xml` and inherit the default video importing theme of `UGCKit`.
```
<style name="PickerActivityTheme" parent="UGCKitPickerStyle"/>
```
3. Create an activity, inherit `Activity`, get a `UGCKitVideoPicker` object, and set the callback.
``` java
@Override
public void onCreate(Bundle icicle) {
    super.onCreate(icicle);
    // You must configure the theme in the code (`setTheme`) or in `AndroidManifest` (android:theme).
    setTheme(R.style.PickerActivityTheme);
    setContentView(R.layout.activity_video_picker);
    // Get `UGCKitVideoPicker`
    mUGCKitVideoPicker = (UGCKitVideoPicker) findViewById(R.id.video_picker);
    // Listen for video importing events
    mUGCKitVideoPicker.setOnPickerListener(new IPickerLayout.OnPickerListener() {
        @Override
        public void onPickedList(ArrayList<TCVideoFileInfo> list) {
            // `UGCKit` returns the paths of selected videos.
        }
    });
}
```

**The UI view looks like this:**
![Image description](https://main.qcloudimg.com/raw/cf043d198ce9bdbe32c3035b83afc18e.png)

[](id:v_cut)
#### 4. Implement video clipping
1. Create an XML file and add the code below:
```xml
<com.tencent.qcloud.ugckit.UGCKitVideoCut
        android:id="@+id/video_cutter"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
```
2. Create an empty theme in `res/values/styles.xml` and inherit the default video editing theme of `UGCKit`.
```
<style name="EditerActivityTheme" parent="UGCKitEditerStyle"/>
```
3. Create an activity, implement the `FragmentActivity` API, get a `UGCKitVideoCut` object, and set the callback.
```java
@Override
protected void onCreate(@Nullable Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    // You must configure the theme in the code (`setTheme`) or in `AndroidManifest` (android:theme).
    setTheme(R.style.EditerActivityTheme);
    setContentView(R.layout.activity_video_cut);
    mUGCKitVideoCut = (UGCKitVideoCut) findViewById(R.id.video_cutter);
    // Get the paths of videos imported via the previous view
    mVideoPath = getIntent().getStringExtra(UGCKitConstants.VIDEO_PATH);
    // `UGCKit` sets the video path.
    mUGCKitVideoCut.setVideoPath(mVideoPath);
    // Listen for the generation of videos
    mUGCKitVideoCut.setOnCutListener(new IVideoCutKit.OnCutListener() {
        
        @Override
        public void onCutterCompleted(UGCKitResult ugcKitResult) {
            // Callback for the completion of video clipping
        }

        @Override
        public void onCutterCanceled() {
            // Callback for clipping being canceled
        }
    });
}

@Override
protected void onResume() {
    super.onResume();
    // `UGCKit` takes over the lifecycle of the video clipping view. For details, see `Github/Demo`.
    mUGCKitVideoCut.startPlay();
}
```

**The UI view looks like this:**
![Image description](https://main.qcloudimg.com/raw/5ffcdda31393c6994a93297bd6f9b25c.png)

[](id:v_effect_edit)
#### 5. Implement special effects
1. In the XML file of the editing activity, add the code below:
``` xml
<com.tencent.qcloud.ugckit.UGCKitVideoEdit
        android:id="@+id/video_edit"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
```
2. Create an editing activity, inherit `FragmentActivity`, get a `UGCKitVideoEdit` object, and set the callback.
```java
@Override
protected void onCreate(@Nullable Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    // You must configure the theme in the code (`setTheme`) or in `AndroidManifest` (android:theme).
    setTheme(R.style.EditerActivityTheme);
    setContentView(R.layout.activity_video_editer);
    // Set the video path (optional). You can skip this if the previous view is video clipping and `setVideoEditFlag(true)` is called.
    mVideoPath = getIntent().getStringExtra(UGCKitConstants.VIDEO_PATH);
    mUGCKitVideoEdit = (UGCKitVideoEdit) findViewById(R.id.video_edit);
    if (!TextUtils.isEmpty(mVideoPath)) {
        mUGCKitVideoEdit.setVideoPath(mVideoPath);
    }
    // Initialize the player
    mUGCKitVideoEdit.initPlayer();
    mUGCKitVideoEdit.setOnVideoEditListener(new IVideoEditKit.OnEditListener() {
        @Override
        public void onEditCompleted(UGCKitResult ugcKitResult) {
            // Video editing completed.
        }

        @Override
        public void onEditCanceled() {
            
        }
    });
}

@Override
protected void onResume() {
    super.onResume();
    // `UGCKit` takes over the lifecycle of the editing view. For details, see `Github/Demo`.
    mUGCKitVideoEdit.start();
}
```

**The UI view looks like this:**
![Image description](https://main.qcloudimg.com/raw/fe56207213a5838189bf6583e10677bc.png)

## Module Description

See the documents below for a detailed description of different UGSV modules.
- [Capturing and Shoot](https://intl.cloud.tencent.com/document/product/1069/38019)
- [Video Editing](https://intl.cloud.tencent.com/document/product/1069/38024)
- [Video Splicing](https://intl.cloud.tencent.com/document/product/1069/38025)
- [Video Upload](https://intl.cloud.tencent.com/document/product/1069/38026)
- [Player](https://intl.cloud.tencent.com/document/product/1069/38027)
- [Animated Effects and Face Changing (Enterprise)](https://intl.cloud.tencent.com/document/product/1069/38031)


[](id:que2)

## FAQs

[](id:que2_1)

### Can I use AndroidX?
 Since most of our users use Android Support Library, `UGCKit` is based on Android Support Library currently. However, to meet the demand of users using AndroidX, we provide a scheme for you to migrate `UGCKit` to AndroidX.

The directions below use the UGSV SDK as an example, and the `UGCKit` module is used in the demo.
1. **Prerequisites:**
	- Update Android Studio to v3.2 or above.
	- Update the Android Gradle plugin to v4.6 or above.
	<img src="https://main.qcloudimg.com/raw/4d71f185511450a40bf1e569d903d37d.png" width="700">
	- Update `compileSdkVersion` to 28 or above.
	- Update `buildToolsVersion` to 28.0.2 or above.
	<img src="https://main.qcloudimg.com/raw/9a31ee56da63f6ca397a8ec2aae6564d.png" width="700">
2. **Migrate to AndroidX:**
	1. Import the project to Android Studio and select **Refactor > Migrate to AndroidX**.
<img src="https://main.qcloudimg.com/raw/2df246f4fcbb616aca744c8ad65877ff.png" width="700">
	2. Click **Migrate** to migrate the project to AndroidX.
<img src="https://main.qcloudimg.com/raw/aefcbe1331037db4e0bea585c090cf1c.png" width="700">

[](id:que2_2)
### What should I do if a `UGCKit` build version error occurs?

-**Error message**:
```
ERROR: Unable to find method 'org.gradle.api.tasks.compile.CompileOptions.setBootClasspath(Ljava/lang/String;)V'.
Possible causes for this unexpected error include:
```
-**Cause**: The problem occurs because the version of the Gradle plugin used for `UGCKit` is v2.2.3, but that of Gradle is v3.3.
- **Solution**: Check whether the versions of `Android Studio Gradle` and Gradle match. For details, please see [Update the Android Gradle plugin](https://developer.android.google.cn/studio/releases/gradle-plugin.html#updating-plugin).

[](id:que2_3)

### What should I do if the following error occurs when I build `UGCKit`?
- **Error message**:
![](https://main.qcloudimg.com/raw/e153fe9637d18f9d4df4c1a9fde51ee2.png)
- **Cause**: The problem occurs because `renderscript-v8.jar` is missing from `ugckit module`. `renderscript-v8.jar` is responsible for image processing, blurring, and rendering.
- **Solution**: Create a libs folder under `ugckit module` and add `renderscript-v8.jar`, which you can find in `\sdk\build-tools\`, to the folder.

