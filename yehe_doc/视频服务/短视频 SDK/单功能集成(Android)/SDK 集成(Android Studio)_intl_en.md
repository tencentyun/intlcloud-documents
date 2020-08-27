## Android Project Configuration
### 1. System requirements
The SDK is supported on Android 4.0.3 (API 15) or above; however, hardware encoding can be enabled only on Android 4.3 (API 18) or above.

### 2. Development environment
The following are the requirements for the SDK development environment. The development environments of the application and the SDK can be different but must be compatible with each other.

- Android NDK: android-ndk-r12b
- Android SDK Tools: android-sdk_25.0.2
- minSdkVersion: 15
- targetSdkVersion: 26
- Android Studio (it is recommended; you can also use Eclipse + ADT)

### 3. Integration directions
#### 3.1. Integrate by using .aar file
1. **Create a project**
![](https://main.qcloudimg.com/raw/ca473c3bf484da3d7d959dbb83b192b1.png)

2. **Configure the project**
	1. Add the code that imports the .aar package into `build.gradle` in the `App` directory of the project:
```
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    // Import the UGSV SDK .aar file. Please replace `x.y.zzzz` in `LiteAVSDK_UGC_x.y.zzzz` with the latest version number
    compile(name: 'LiteAVSDK_UGC_7.4.9211', ext: 'aar')
    ...
}
```
	2. In `build.gradle` in the project directory, add `flatDir` to specify the local repository:
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
	3. Specify the architectures compatible with the NDK in `defaultConfig` in `build.gradle` in the `App` directory of the project:
```
defaultConfig {
    ...
    ndk {
        abiFilters "armeabi", "armeabi-v7a"
    }
}
```
	4. Click "Sync Now" to compile the project.

#### 3.2. Integrate by using .jar and .so files
1. **Library description**
After decompressing the ZIP package, you can get the `libs` directory which contains the .jar files and .so folders as listed below:
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th>.jar File</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>liteavsdk.jar </td>
<td >Core library of UGSV SDK for Android</td>
</tr>
</tbody></table>
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th>.so File</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td> libliteavsdk.so  </td>
<td >Core component of UGSV SDK</td>
</tr>
<tr>
<td>libtxffmpeg.so    </td>
<td >Basic FFmpeg library (ijkplayer edition) used to fix certain video format compatibility issues for VOD playback</td>
</tr>
<tr>
<td>libtxplayer.so   </td>
<td >Open-source ijkplayer library used to fix certain video format compatibility issues for VOD playback</td>
</tr>
<tr>
<td>libtxsdl.so</td>
<td >Open-source ijkplayer library used to fix certain video format compatibility issues for VOD playback</td>
</tr>
</tbody></table>
2. **Copy the files**
If you have not specify the JNI load path for your project, we recommend you copy the .jar package and .so libraries obtained in the previous step to the **Demo\app\src\main\jniLibs** directory, which is the default JNI load directory in Android Studio.

	If you use the Enterprise Edition, after the ZIP package is decompressed, in addition to the .jar package and .so libraries, files in the `assets` directory are also extracted, which are required for the animated effects and need to be copied to the `assets` directory in the project as instructed in [Animated Effects and Face Changing - Project Configuration](https://intl.cloud.tencent.com/document/product/1069/38031#.E5.B7.A5.E7.A8.8B.E8.AE.BE.E7.BD.AE).
3. **Configure the project**
Add the code that imports the .jar package and .so libraries into `build.gradle` in the `App` directory of the project.
```
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    // Import the .jar file of the UGSV SDK
    compile fileTree(dir: 'src/main/jniLibs', includes: ['*.jar'])
    ...
}
```
4. **Reduce the APK size**
The size of the entire SDK is subject to the .so files, which include the audio/video codec libraries, image processing libraries, and acoustic processing components on which the SDK is dependent to run normally. If the features of the UGSV SDK are not the core features of your application, you can use the online load method to reduce the size of the final APK installation package.
	1. **Upload the .so files**
Upload the .so files in the SDK package to COS and record the download address such as `http://xxx-appid.cossh.myqcloud.com/so_files.zip`.
	2. **Prepare for the start**
Before an SDK feature such as video playback is started by the user, use a loading animation to prompt the user that the relevant feature module is being loaded.
	3. **Download the .so files**
When the user is waiting, the application can download the .so files from `http://xxx-appid.cossh.myqcloud.com/so_files.zip` and store the files in the application directory (such as the `files` folder in the application's root directory). To ensure that this process is not affected by ISP DNS blocking, please verify the integrity of the .so files after download.
	4. **Load the .so files**
After all .so files are ready, call `setLibraryPath` of `TXLiveBase` to set the target paths of the downloaded .so files to the paths in the SDK and call the relevant SDK feature. Then, the SDK can load the required .so files at those paths and start the relevant feature.

#### 3.3. Configure the application permissions

Configure application permissions in `AndroidManifest.xml`. Generally, an audio/video application requires the following permissions:

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
#### 3.4. Set the license
Apply for a license as instructed in [License Application](https://intl.cloud.tencent.com/document/product/1069/38041) and copy the key and URL from the [console](https://console.cloud.tencent.com/vod/license) as shown below:
![](https://main.qcloudimg.com/raw/c48435846e63a66f6b80453b4c356e7e.png)
Before you integrate UGSV features into your application, we recommend you set `Application onCreate()` as follows:
```
public class DemoApplication extends Application {
    String ugcLicenceUrl = ""; // Enter the URL of the license applied for in the console
    String ugcKey = "";        // Enter the key of the license applied for in the console

    @Override
    public void onCreate() {
        super.onCreate();
        TXUGCBase.getInstance().setLicence(instance, ugcLicenceUrl, ugcKey);
    }
}
```

#### 3.5. Print logs
In `TXLiveBase`, you can set whether to print logs in the console and the log level. The specific code is as follows:
- **setConsoleEnabled**
It is used to set whether to print the SDK output content in the Android Studio Console.
- **setLogLevel**
It is used to set whether the SDK can print local logs. The SDK will write logs into the **Android/data/com.tencent.liteav.demo/files/log/tencent/liteav** folder on the SD card by default. If you need Tencent Cloud technical support, we recommend you toggle on this switch and provide the log file after reproducing the problem. We will appreciate your support.
- **View log files**
To reduce the log size of the UGSV SDK, the locally stored log files are encrypted, and the number of logs is limited. Therefore, to view the log content in plaintext, you need to use the log [decompression tool](http://dldir1.qq.com/hudongzhibo/log_tool/decode_mars_log_file.py).
```
TXLiveBase.setConsoleEnabled(true);
TXLiveBase.setLogLevel(TXLiveConstants.LOG_LEVEL_DEBUG);
```

#### 3.6. Compile and run

Call an SDK API in the project to get the SDK version information so as to check whether the project configuration is correct.

1. **Import the SDK**
Import an SDK class in `MainActivity.java`:
```
import com.tencent.rtmp.TXLiveBase;
```
2. **Call the API**
Call the `getSDKVersioin` API in `onCreate` to get the version number:
```
String sdkver = TXLiveBase.getSDKVersionStr();
Log.d("liteavsdk", "liteav sdk version is : " + sdkver);
```
3. **Compile and run**
If the previous steps are correctly performed, the demo project will be compiled successfully, and the following log information will be displayed in logcat after project execution:
`09-26 19:30:36.547 19577-19577/ D/liteavsdk: liteav sdk version is : 7.4.9211`

### Troubleshooting
If an error similar to the following one occurs when you compile and run your project after importing the SDK into it:

```
Caused by: android.view.InflateException:
Binary XML file #14:Error inflating class com.tencent.rtmp.ui.TXCloudVideoView
```

You can troubleshoot the problem in the following steps:
- Check whether the .jar package and .so libraries in the SDK are placed in the `jniLibs` directory.
- If you use the full edition integrated with the .aar file, check whether the .so libraries for the x64 architecture are filtered out in `defaultConfig` in `build.gradle` in the project directory, as the acoustic component used by the mic connect feature in the full edition currently does not support phones on x64 architecture.
```
defaultConfig {
    ...		
    ndk {
        abiFilters "armeabi", "armeabi-v7a"
    }
}
```
- Check the obfuscation rules to confirm that the SDK-related package names have been added to the "do not obfuscate" list.
```
-keep class com.tencent.** { *; }
```
- Configure the application packaging parameters.
![](https://main.qcloudimg.com/raw/b2dd9bde1cdf13ad5c77c1e00c4092aa.png)

## Quick Integration of Feature Module
This document describes how to quickly integrate the UGSV SDK into an existing project and implement the complete process from shoot and preview to editing.
All required code and resource files are provided in the SDK package in [SDK Download](https://intl.cloud.tencent.com/document/product/1069/37914).

### Integration steps
**Step 1.** Create an empty Android Studio project and name it `UGC`. Make sure that the package name is the same as that (com.tencent.liteav.demo) in the figure below, so that the project can be successfully compiled. Please note that if you do not use the same package name, you need to apply for a license. If you have no license, you can still complete the following steps to integrate the UIs, but certain features may fail.
![](https://main.qcloudimg.com/raw/e6b08ecfca9d6d789da7cc99d501c69d.png)

**Step 2.** Copy the three Android Studio modules `videoediter`, `videorecorder`, and `videojoiner` in the SDK to the new project `UGC/`.
- videoediter: short video editing UI component in the SDK
- videorecord: short video shoot UI component in the SDK
- videojoiner: short video composition UI component in the SDK
	
Import the following modules in `UGC/settings.gradle` of the new project:
```
include ':videorecorder'
include ':videoediter'
include ':videojoiner'
```
Import the following modules in `build.gradle` in `module:app` of the new project:
```
dependencies {
	compile fileTree(dir: 'libs', include: ['*.jar'])
    ...
	compile project(':videoediter')
	compile project(':videojoiner')
	compile project(':videorecorder')
    ...
}
```
**Step 3.** Modify the configuration of `build.gradle` in the project's root directory. 
```
allprojects {
	repositories {
		...
		flatDir {
			 dirs project(':videoediter').file('libs')
             dirs project(':videojoiner').file('libs')
         	 dirs project(':videorecorder').file('libs')
		}
	}
}
```
**Step 4.** Copy the latest SDK .aar file to the `libs` folder in the three copied modules `videoediter`, `videojoiner`, and `videorecorder` and configure the SDK in `build.gradle` in each module. The following sample code uses `videoediter` as an example:
```
dependencies {
    compile fileTree(include: ['*.jar'], dir: 'libs')
    // Rename it to the name of the SDK copied to `libs`
    compile(name: 'LiteAVSDK_UGC_7.4.9211', ext: 'aar')
    ...
}
```
**Step 5.** Make sure that the versions of Android Gradle plugin and local Gradle are compatible.
```
The versions of the Android Gradle plugin and Gradle are not compatible.
```
You can configure as follows to ensure the Gradle version compatibility. Modify the Gradle version in the `gradle-wrapper.properties` file:
```
distributionUrl=https\://services.gradle.org/distributions/gradle-5.4.1-all.zip
```
**Step 6.** Configure the license.
Create a `DemoApplication` class to set the license and declare the application in `AndroidManifest.xml`.
```
//DemoApplication.java
import com.tencent.ugc.TXUGCBase;

public class DemoApplication extends Application {
	String ugcLicenceUrl = "xxx";
	String ugcKey = "xxx";

	@Override
	public void onCreate() {
		super.onCreate();
		TXUGCBase.getInstance().setLicence(this, ugcLicenceUrl, ugcKey);

		String string = TXUGCBase.getInstance().getLicenceInfo(this);
		Log.i("SDK", "string=" + string);
	}
}

// AndroidManifest.xml
<application
	android:name=".DemoApplication"
	 ...
</application>
```
**Step 7.** Call UGSV modules.
Create three buttons in `activity_main.xml`.
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/record"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Record" />

    <Button
        android:id="@+id/editer"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Editer" />

    <Button
        android:id="@+id/joiner"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Joiner" />
</LinearLayout>
```
Start the class of each module in `MainActivity.java`.
```
public class MainActivity extends AppCompatActivity implements View.OnClickListener {

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);

		Button button1 = (Button) findViewById(R.id.record);
		Button button2 = (Button) findViewById(R.id.editer);
		Button button3 = (Button) findViewById(R.id.joiner);

		button1.setOnClickListener(this);
		button2.setOnClickListener(this);
		button3.setOnClickListener(this);
	}

	@Override
	public void onClick(View v) {
		switch (v.getId()) {
		case R.id.record:
			Intent intent1 = new Intent(this, TCVideoSettingActivity.class)								startActivity(intent1)
			break;
		case R.id.editer:
			Intent intent2 = new Intent(this, TCVideoEditChooseActivity.class);
			startActivity(intent2);
			break;
		case R.id.joiner:
			Intent intent3 = new Intent(this, TCVideoJoinChooseActivity.class);
			startActivity(intent3);
			break;
		}
	}
}
```
**Step 8.** Clean the project, and you can run it to see the effect.

### Description of relevant files
#### Short video shoot

```
└── videorecord
    ├── RecordDef.java (background music selection API)
    ├── TCBGMRecordAdapter.java (background music list adapter)
    ├── TCBGMRecordChooseLayout.java (background music list page)
    ├── TCBGMRecordManager.java (background music management class)
    ├── TCBGMRecordView.java (background music operation panel on shoot page)
    ├── TCVideoRecordActivity.java (shoot homepage)
    ├── TCVideoRecordSmartActivity.java (shoot homepage for `UGC_Smart` edition)
    ├── TCVideoSettingActivity.java (shoot settings page)
    └── view
        ├── ComposeRecordBtn.java (custom shoot button)
        ├── MusicListView.java
        ├── RecordProgressView.java (custom shoot progress bar)
        ├── TCAudioControl.java
        └── TCMusicSelectView.java
```
#### Short video editing
```
└── videoediter
    ├── PictureChooseFragment.java (image selection page)
    ├── TCVideoEditChooseActivity.java (page for selecting single video editing file)
    ├── TCVideoEditerActivity.java (editing homepage)
    ├── TCVideoEditerWrapper.java (API class information storage)
    ├── TCVideoPreprocessActivity.java (editing preprocessing page)
    ├── TabFragmentPagerAdapter.java (image/video page adapter)
    ├── VideoChooseFragment.java (video file selection page)
    ├── bgm
    │   ├── TCBGMSettingFragment.java (background music settings page)
    │   ├── TCMusicAdapter.java (background music adapter)
    │   └── utils
    │       └── TCMusicManager.java (background music management class)
    ├── bubble
    │   ├── TCWordEditActivity.java (bubble subtitles homepage)
    │   │   ├── others
    │   │   │   └── TCWordInputDialog.java (subtitles input box)
    ├── common
    │   ├── TCConfirmDialog.java (confirmation dialog box)
    │   ├── TCToolsView.java (toolbar at the bottom of editing page)
    │   └── widget
    │       ├── RangeSeekBar.java (SeekBar control)
    │       └── videotimeline (thumbnail control package)
    ├── cutter
    │   └── TCCutterFragment.java (video clipping settings page)
    ├── filter
    │   └── TCStaticFilterFragment.java (static filter settings page)
    ├── motion
    │   ├── TCMotionFragment.java (animated filter settings page)
    │   └── view
    │       └── TCColorfulSeekBar.java (colored SeekBar for animated filter)
    ├── paster
    │   ├── AnimatedPasterConfig.java (animated sticker configuration)
    │   ├── TCPasterActivity.java (sticker page)
    ├── time
    │   ├── TCTimeFragment.java (time-based special effect settings page)
    └── transition
        └── TCTransitionFragment.java (image transition settings page)
```
#### Short video composition
```
└── videojoiner
    ├── TCVideoJoinerActivity.java (page for adjusting the composition sequence of multiple video segments)
    ├── TCVideoJoinerPreviewActivity.java (page for previewing and generating multiple video segments)
    └── swipemenu (control for dragging/deleting video by pressing and holding/swiping left on it)
```

### Detailed description
The following is the detailed description of each module:
- [Video shoot](https://intl.cloud.tencent.com/document/product/1069/38019)
- [Video editing](https://intl.cloud.tencent.com/document/product/1069/38024)
- [Video splicing](https://intl.cloud.tencent.com/document/product/1069/38025)
- [Video upload](https://intl.cloud.tencent.com/document/product/1069/38026)
- [Video playback](https://intl.cloud.tencent.com/document/product/1069/38027)
- [Animated effects and face changing (Enterprise Edition)](https://intl.cloud.tencent.com/document/product/1069/38031)
