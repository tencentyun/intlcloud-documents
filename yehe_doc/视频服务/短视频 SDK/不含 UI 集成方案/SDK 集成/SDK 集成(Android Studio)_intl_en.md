## Android Project Configuration
### System requirements
We recommend you run the SDK on Android 5.0 (API level 21) or later.

### Development environment
Below are the environment requirements for SDK development. You don't need to meet the same requirements for application development, but make sure that your application is compatible with the SDK.

- Android NDK: android-ndk-r12b
- Android SDK Tools: android-sdk_25.0.2
- minSdkVersion: 21
- targetSdkVersion: 26
- Android Studio (recommended)


[](id:step1)
### Step 1. Integrate the SDK
<dx-tabs>
::: AAR
1. **Create a project**
![](https://main.qcloudimg.com/raw/ca473c3bf484da3d7d959dbb83b192b1.png)
2. **Configure the project**
   -  Add the code that imports the .aar package into `build.gradle` in the `App` directory of the project:
```java
dependencies {
		compile fileTree(dir: 'libs', include: ['*.jar'])
		// Import the SDK AAR file. Replace `x.y.zzzz` in `LiteAVSDK_UGC_x.y.zzzz` with the latest version number.
		compile(name: 'LiteAVSDK_UGC_10.7.1136', ext: 'aar')
		...
}
```
   - In `build.gradle` in the project directory, add `flatDir` to specify the local repository:
```java
allprojects {
	repositories {
			jcenter()
			flatDir {
					dirs 'libs'
			}
	}
}
```
   - Specify the NDK-compatible architectures in `defaultConfig` in `build.gradle` in the `App` directory of the project:
```java
defaultConfig {
		...
		ndk {
				abiFilters "armeabi-v7a", "arm64-v8a"
		}
}
```
   - Click **Sync Now** to compile the project.
:::
::: JAR + SO
1. **Library description**
After decompressing the ZIP package, you can get the `libs` directory, which contains the .jar file and .so files for the two architectures as listed below:
![](https://qcloudimg.tencent-cloud.cn/raw/dc360c935caa3816507faf37e9a51391.png)
2. **Copy files**
    If you have not specified the JNI library loading path for your project, we recommend you copy the .jar package and the .so library for the corresponding architecture obtained in the previous step to the **Demo\app\src\main\jniLibs** directory (Android Studio's default path for loading JNI libraries) and put the .jar package in the `libs` folder.
3. If you have purchased Tencent Effect, you need to integrate the Tencent Effect SDK as instructed in [Integrating Tencent Effect into UGSV (Android)](https://intl.cloud.tencent.com/document/product/1143/45395).
4. **Configure the project**
    In `build.gradle` of your project directory, add code that references the JAR and SO files.
```java
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    // Import the JAR file of the UGSV SDK
    compile fileTree(dir: 'src/main/jniLibs', includes: ['*.jar'])
    ...
}
```
4. **Reduce APK size**
    The SO files, which provide the audio/video codec library, image processing library, and audio processing component, take up a big chunk of the SDK's size. If UGSV-related features are not the main features of your application, you may consider loading the SO files online to reduce your APK size.
    If you have integrated the Tencent Effect SDK, you can downsize the package as instructed in [Reducing SDK size (Android)](https://www.tencentcloud.com/document/product/1143/47831).
  5. **Upload SO files**

    Upload the SO files in the SDK package to COS and note the download address, e.g., `http://xxx-appid.cossh.myqcloud.com/so_files.zip`.
  6. **Show loading animation**

    When users start the SDK, for example, to play a video, show on the UI a loading animation and a message that relevant modules are being loaded.
  7 **Download SO files**

    While users wait, your application can download the SO files from `http://xxx-appid.cossh.myqcloud.com/so_files.zip` and save them in your project directory, for example, in the `files` folder of your application's root directory. Given the possibility of DNS hijacking by ISPs, you should check the integrity of the SO files after download.
  8 **Load SO files**

    After all the SO files are in place, call `setLibraryPath` of `TXLiveBase` to set the SDK's library path to the directory of the downloaded SO files. The SDK will load from the directory the SO files needed to enable the requested UGSV feature.
:::
::: Gradle
1. Add the LiteAVSDK_UGC dependency to `dependencies`.
Run the following command if you use a 3.x version of com.android.tools.build:gradle:
```java
dependencies {
   implementation 'com.tencent.liteav:LiteAVSDK_UGC:latest.release'
}
```
- Run the following command if you use a 2.x version of `com.android.tools.build:gradle`.
```java
dependencies {
   compile 'com.tencent.liteav:LiteAVSDK_UGC:latest.release'
}
```
2. In `defaultConfig`, specify the CPU architecture to be used by your application.
```java
defaultConfig {
   ndk {
       abiFilters "armeabi-v7a", "arm64-v8a"
   }
}
```
>?Currently, the SDK supports armeabi-v7a and arm64-v8a.
3. Click **Sync Now** to automatically download the SDKs and integrate them into your project.
:::
</dx-tabs>

[](id:step2)
### Step 2. Configure app permissions

Configure application permissions in `AndroidManifest.xml`. Audio/Video applications generally need the following permissions:
```java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.Camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```

[](id:step3)
### Step 3. Configure the license
1. After successfully obtaining a license, copy the license key and URL in the [VOD console](https://console.cloud.tencent.com/vod/license/video) as shown below:
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

>? If you use a license for the SDK on v4.7 and have upgraded the SDK to v4.9, you can click **Switch to New License** in the console to generate a new license key and URL. A new license can be used only for the SDK on v4.9 or later and should be configured as described above.
> <img src="https://qcloudimg.tencent-cloud.cn/raw/67f7df5cca54164c10dbf78c5b84ccdf.png" width=600px>

[](id:step4)
### Step 4. Print logs
You can enable/disable console log printing and set the log level in `TXLiveBase`. See the sample code below.
- **setConsoleEnabled**
Sets whether to print the SDK logs in the Android Studio console.
- **setLogLevel**
It is used to set whether the SDK can print local logs. The SDK will write logs into the **Android/data/application package name/files/log/tencent/liteav** folder on the SD card by default. If you need technical support from Tencent Cloud, we recommend you enable this feature and provide the log file after reproducing the problem.
```
TXLiveBase.setConsoleEnabled(true);
TXLiveBase.setLogLevel(TXLiveConstants.LOG_LEVEL_DEBUG);
```

[](id:step5)
### Step 5. Build and run the project

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
2. If you use the full edition integrated with the .aar file, check whether the .so libraries for the x64 architecture are filtered out in `defaultConfig` in `build.gradle` in the project directory.
```
defaultConfig {
    ...   
    ndk {
        abiFilters "armeabi-v7a", "arm64-v8a"
    }
}
```
3. Check if the package name of the SDK has been added to the "do not obfuscate" list.
```
-keep class com.tencent.** { *;}
```
4. [Configure](https://intl.cloud.tencent.com/document/product/1069/37914) packaging options for your application.
![](https://main.qcloudimg.com/raw/b2dd9bde1cdf13ad5c77c1e00c4092aa.png)

[](id:module)
## Integrating UGSV Modules
This section describes how to quickly integrate the UGSV SDK into your existing project to implement a complete range of short video features including shooting, editing, and composition. The code and resources mentioned in this section can be found in the SDK ZIP file as described in [SDK Download](https://intl.cloud.tencent.com/document/product/1069/37914) and the [UGSV demo](https://github.com/LiteAVSDK/UGSV_Android).

[](id:integrated)
### Integrating `UGCKit`

1. **Create a project (empty activity)**[](id:UGCKit_step1)
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
    compileSdkVersion = 29
    buildToolsVersion = "29.0.2"
    supportSdkVersion = "26.1.0"
    minSdkVersion = 21
    targetSdkVersion = 26
    versionCode = 1
    versionName = "v1.1"
    proguard = true
    rootPrj = "$projectDir/.."
    ndkAbi = 'armeabi-v7a'
    liteavSdk = "com.tencent.liteav:LiteAVSDK_UGC:latest.release"
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

dependencies {
    # Copying starts.
    implementation fileTree(include: ['*.jar'], dir: 'libs')
    implementation 'com.google.android.material:material:1.0.0'
    implementation 'androidx.recyclerview:recyclerview:1.0.0'
    implementation 'com.google.code.gson:gson:2.3.1'
    implementation 'com.tencent.rqd:crashreport:3.4.4'
    implementation 'com.tencent.rqd:nativecrashreport:3.9.2'
    implementation 'com.github.castorflex.verticalviewpager:library:19.0.1'
    implementation 'com.squareup.okhttp3:okhttp:3.11.0'
    implementation 'de.hdodenhof:circleimageview:3.1.0'
    implementation rootProject.ext.liteavSdk
    implementation project(':ugckit')
    implementation 'androidx.constraintlayout:constraintlayout:2.1.3'
    implementation('com.blankj:utilcode:1.25.9', {
        exclude group: 'com.google.code.gson', module: 'gson'
    })
    # Copying ends.
}
```
	4. Specify the Gradle version.
```
distributionUrl=https\://services.gradle.org/distributions/gradle-5.6.4-bin.zip
```
2. **Import modules**[](id:UGCKit_step2)
	1. Copy the `ugckit` module to the `ugc` directory of your newly created project.
	2. To integrate basic beauty filters, copy the `beautysettingkit` module to the `ugc` directory of the project.
	3. To integrate the Tencent Effect SDK, copy the `xmagickit` module to the `ugc` directory of the project. For more information, see [SDK Integration Guide (Android)](https://www.tencentcloud.com/document/product/1069/47917).
	4. Import `ugckit` to `settings.gradle` of the project.
	5. In `UGC/settings.gradle` of the project, import the modules below:
```
include ':ugckit'
include ':beautysettingkit'
include ':xmagickit'
```
	5. Add `ugckit` as a dependency for the app modules of your project.
```
implementation project(':ugckit')
```
3. **Apply for a license**[](id:UGCKit_step3)
You need to set the license first before using `UGCKit`.

[](id:fun)
### Enabling shooting, importing, clipping, and special effects
1. **Set the license and initialize `UGCKit`**[](id:initialize)
Set the license and initialize `UGCKit` as early as possible before using UGSV features.
```
// Configure the license
TXUGCBase.getInstance().setLicence(this, ugcLicenceUrl, ugcKey);
// Initialize `UGCKit`
UGCKit.init(this);
```
2. **Implement video shooting**[](id:record)
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
            // Callback for ending shooting
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
![](https://main.qcloudimg.com/raw/077aa281195ba33fcaa67da2a13b1b60.png)
3. **Implement video import**[](id:v_import)
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
![](https://main.qcloudimg.com/raw/cf043d198ce9bdbe32c3035b83afc18e.png)
4. **Implement video clipping**[](id:v_cut)
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
![](https://main.qcloudimg.com/raw/5ffcdda31393c6994a93297bd6f9b25c.png)
5. Implement video special effect editing[](id:v_effect_edit)
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
![](https://main.qcloudimg.com/raw/fe56207213a5838189bf6583e10677bc.png)

### Detailed description
See the documents below for a detailed description of different UGSV modules.
- [Capturing and Shooting](https://intl.cloud.tencent.com/document/product/1069/38019)
- [Video Editing](https://intl.cloud.tencent.com/document/product/1069/38024)
- [Video Splicing](https://intl.cloud.tencent.com/document/product/1069/38025)
- [Video Upload](https://intl.cloud.tencent.com/document/product/1069/38026)
- [Player SDK](https://intl.cloud.tencent.com/document/product/1069/38027)

[](id:que2)
## FAQs

[](id:que2_1)
### Can I use AndroidX?
The latest version of `UGCKit` uses AndroidX. If you still use `UGCKit` based on the Android Support Library, you can update it to the latest version or switch to AndroidX as follows. Here, `UGSVSDK` is used as an example, which also uses the `UGCKit` module in its demo.

1. **Prerequisites:**
	- Update Android Studio to v3.2 or later.
	- Update the Android Gradle plugin to v4.6 or later.
	<img src="https://main.qcloudimg.com/raw/4d71f185511450a40bf1e569d903d37d.png" width="700">
	- Update `compileSdkVersion` to 28 or later.
	- Update `buildToolsVersion` to 28.0.2 or later.
	<img src="https://main.qcloudimg.com/raw/9a31ee56da63f6ca397a8ec2aae6564d.png" width="700">
2. **Migrate to AndroidX:**
	1. Import the project to Android Studio and select **Refactor > Migrate to AndroidX**.
	<img src="https://main.qcloudimg.com/raw/2df246f4fcbb616aca744c8ad65877ff.png" width="700">
	2. Click **Migrate** to migrate the current project to AndroidX.<br>
	<img src="https://main.qcloudimg.com/raw/aefcbe1331037db4e0bea585c090cf1c.png" width="700">

[](id:que2_2)
### What should I do if a `UGCKit` build version error occurs?
- **Error message**:
```
ERROR: Unable to find method 'org.gradle.api.tasks.compile.CompileOptions.setBootClasspath(Ljava/lang/String;)V'.
Possible causes for this unexpected error include:
```
-**Cause**: The problem occurs because the version of the Gradle plugin used for `UGCKit` is v2.2.3, but that of Gradle is v3.3.
- **Solution**: Check whether the versions of `Android Studio Gradle` and Gradle match. For details, see [Update the Android Gradle plugin](https://developer.android.google.cn/studio/releases/gradle-plugin.html#updating-plugin).

[](id:que2_3)
### What should I do if the following error occurs when I build `UGCKit`?
- **Error message**:
![](https://main.qcloudimg.com/raw/e153fe9637d18f9d4df4c1a9fde51ee2.png)
- **Cause**: The problem occurs because `renderscript-v8.jar` is missing from the `ugckit` module. `renderscript-v8.jar` is responsible for image processing, blurring, and rendering.
- **Solution**: Create a libs folder under the `ugckit` module and add `renderscript-v8.jar`, which you can find in `\sdk\build-tools\`, to the folder.