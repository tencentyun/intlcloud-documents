TUIKit supports modular integration starting from version 5.7.1435. You can integrate modules for integration according to your needs.
Starting from version 6.9.3557, TUIKit provides a new set of minimalist version UI components. The previous version UI components are still retained, which are called the classic version UI components. You can choose either the classic or minimalist version as needed.

For more information about TUIKit components, see [here](https://intl.cloud.tencent.com/document/product/1047/50062).

The following describes how to integrate TUIKit components. 

## Environment Requirements
- Android Studio-Chipmunk 
- Gradle-6.7.1
- Android Gradle Plugin Version-4.2.0
- kotlin-gradle-plugin-1.5.31
  
## Integrating Module Source Code
1. Download the TUIKit source code from [GitHub](https://github.com/tencentyun/TIMSDK/tree/master/Android). Ensure that the TUIKit folder is at the same level as your project folder, for example:
<img src="https://qcloudimg.tencent-cloud.cn/raw/00bc0470857b850436663d9bf2ef9164.png" width="500"/> 
1. Add the corresponding TUIKit components to `settings.gradle` according to your business requirements. TUIKit components are independent of each other, and adding or removing them does not affect project compilation.
```groovy
// Include the upper-layer app module
include ':app'

// Include the internal communication module (required module)
include ':tuicore'
project(':tuicore').projectDir = new File(settingsDir, '../TUIKit/TUICore/tuicore')

// Include the chat feature module (basic feature module)
include ':tuichat'
project(':tuichat').projectDir = new File(settingsDir, '../TUIKit/TUIChat/tuichat')

// Include the relationship chain feature module (basic feature module)
include ':tuicontact'
project(':tuicontact').projectDir = new File(settingsDir, '../TUIKit/TUIContact/tuicontact')

// Include the conversation list feature module (basic feature module)
include ':tuiconversation'
project(':tuiconversation').projectDir = new File(settingsDir, '../TUIKit/TUIConversation/tuiconversation')

// Include the search feature module (To use this module, you need to purchase the Ultimate edition)
include ':tuisearch'
project(':tuisearch').projectDir = new File(settingsDir, '../TUIKit/TUISearch/tuisearch')

// Include the group feature module
include ':tuigroup'
project(':tuigroup').projectDir = new File(settingsDir, '../TUIKit/TUIGroup/tuigroup')

// Include the offline push feature module
include ':tuiofflinepush'
project(':tuiofflinepush').projectDir = new File(settingsDir, '../TUIKit/TUIOfflinePush/tuiofflinepush')

// Include the community topic feature module (To use this module, you need to purchase the Ultimate edition)
include ':tuicommunity'
project(':tuicommunity').projectDir = new File(settingsDir, '../TUIKit/TUICommunity/tuicommunity')

// Include the audio/video call feature module
include ':tuicallkit'
project(':tuicallkit').projectDir = new File(settingsDir, '../TUIKit/TUICallKit/tuicallkit')
```
3. Add the following to `build.gradle` in App:
```groovy
dependencies {
    api project(':tuiconversation')
    api project(':tuicontact')
    api project(':tuichat')
    api project(':tuisearch')
    api project(':tuigroup')
    api project(':tuiofflinepush')
    api project(':tuicommunity')
    api project(':tuicallkit')  
}
```
4. Add the following to the `gradle.properties` file to automatically convert third-party libraries to use AndroidX:
```properties
android.enableJetifier=true
```
[](id:buildStep5)
5. Add the following to the `build.gradle` file (in the same level as `settings.gradle`) of the root project to add the Maven repository and Kotlin support:
```groovy
buildscript {
    ext.kotlin_version = '1.5.31'
    repositories {
        mavenCentral()
        maven { url "https://mirrors.tencent.com/nexus/repository/maven-public/" }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:4.2.0'
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
    }
}
```
6. Sync the project, and compile and run it. The expected project structure is shown in the following figure:<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/454abb6051a7a94a08559d8404e5aec7.png" width="400"/> 
7. (Optional) Delete unnecessary UI files
The classic and minimalist versions of UIs do not affect each other, and they can run independently. The classic and minimalist version UI files are in separate folders within each TUIKit component. Take TUIChat as an example:
<img src="https://qcloudimg.tencent-cloud.cn/raw/179a15bb72b24a09cf7440c50e5c3442.png" width="400"/> 
The `classicui` folder stores the classic version UI files, and the `minimalistui` folder stores the minimalist version UI files. If you are to integrate the minimalist version UIs, directly delete the `classicui` folder and delete `Activity` and `Service` corresponding to the classic version UIs in the `AndroidManifest.xml` file.
> ? The classic and minimalist versions of UI components cannot be used together. If you integrate multiple components, all the integrated components must be of the same version: classic or minimalist.

## Quick Build
Instant messaging software usually consists of several basic UIs such as the conversation list, chat window, contacts, and audio/video call UIs. It only takes a few lines of code to build these UIs in your project. The process is as follows:

### Step 1. Log in to TUIKit

```java
// Called when Login is clicked on the user UI
TUILogin.login(context, sdkAppID, userID, userSig, new TUICallback() {
    @Override
    public void onError(final int code, final String desc) {
    }

    @Override
    public void onSuccess() {
    }
});
```
>! An object of the `Application` class must be passed in via `context`. Otherwise, some images cannot be loaded.

### Step 2. Create viewPager
1. Add the UI layout in `activity_main.xml`:
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    
    <androidx.viewpager2.widget.ViewPager2
    android:id="@+id/view_pager"
    android:layout_width="match_parent"
    android:layout_height="0dp"
    android:layout_weight = "1"/>
</LinearLayout>
```
2. Create `FragmentAdapter.java` to work with ViewPager2 to display the conversation and contacts UIs.
```java
import androidx.annotation.NonNull;
import androidx.fragment.app.Fragment;
import androidx.fragment.app.FragmentActivity;
import androidx.fragment.app.FragmentManager;
import androidx.lifecycle.Lifecycle;
import androidx.viewpager2.adapter.FragmentStateAdapter;


import java.util.List;

public class FragmentAdapter extends FragmentStateAdapter {
    private static final String TAG = FragmentAdapter.class.getSimpleName();

    private List<Fragment> fragmentList;

    public FragmentAdapter(@NonNull FragmentActivity fragmentActivity) {
        super(fragmentActivity);
    }

    public FragmentAdapter(@NonNull Fragment fragment) {
        super(fragment);
    }

    public FragmentAdapter(@NonNull FragmentManager fragmentManager, @NonNull Lifecycle lifecycle) {
        super(fragmentManager, lifecycle);
    }

    public void setFragmentList(List<Fragment> fragmentList) {
        this.fragmentList = fragmentList;
    }

    @NonNull
    @Override
    public Fragment createFragment(int position) {
        if (fragmentList == null || fragmentList.size() <= position) {
            return new Fragment();
        }
        return fragmentList.get(position);
    }

    @Override
    public int getItemCount() {
        return fragmentList == null ? 0 : fragmentList.size();
    }
}
```

### Step 3. Build the core fragment

The getting, synchronization, display, and interaction of the conversation list `TUIConversationFragment` and contact list `TUIContactFragment` UI data are already encapsulated in TUI components, and UIs can be used as easily as common Android fragments.

Add the following code to the `onCreate` method in `MainActivity.java`:

<dx-tabs>
::: Classic version
```java
List<Fragment> fragments = new ArrayList<>();
// Add the classic version of conversation UI provided by TUIConversation
fragments.add(new TUIConversationFragment());

// Add the classic version of contacts UI provided by TUIContact
fragments.add(new TUIContactFragment());

ViewPager2 mainViewPager = findViewById(R.id.view_pager);
FragmentAdapter fragmentAdapter = new FragmentAdapter(this);
fragmentAdapter.setFragmentList(fragments);
mainViewPager.setOffscreenPageLimit(2);
mainViewPager.setAdapter(fragmentAdapter);
mainViewPager.setCurrentItem(0, false);

```
:::

::: Minimalist version
```java
List<Fragment> fragments = new ArrayList<>();
// Add the minimalist version of conversation UI provided by TUIConversation
fragments.add(new TUIConversationMinimalistFragment());

// Add the minimalist version of contacts UI provided by TUIContact
fragments.add(new TUIContactMinimalistFragment());

ViewPager2 mainViewPager = findViewById(R.id.view_pager);
FragmentAdapter fragmentAdapter = new FragmentAdapter(this);
fragmentAdapter.setFragmentList(fragments);
mainViewPager.setOffscreenPageLimit(2);
mainViewPager.setAdapter(fragmentAdapter);
mainViewPager.setCurrentItem(0, false);

```
:::

</dx-tabs>



### Step 4. Build the audio/video call feature
TUI components allow users to start audio/video calls in chat UIs and can be quickly integrated with a few steps:

<table style="text-align:center;vertical-align:middle;width: 800px">
  <tr>
    <th style="text-align:center;" ><b>Video Call<br></b></th>
    <th style="text-align:center;"><b>Audio Call</b><br></th>
  </tr>
  <tr>
    <td><img src="https://qcloudimg.tencent-cloud.cn/raw/44d4c8a412752abda898341665a90016.png"/></td>
    <td><img src="https://qcloudimg.tencent-cloud.cn/raw/5eb84936666da81b0331a28c3c779b77.png"/></td>
	 </tr>
</table>


1. **Activate the TRTC service**
	1. Log in to the [Chat console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
	2. Click **Free trial** under **Activate Tencent Real-Time Communication (TRTC)** to activate the 7-day free trial service of TUICallKit.
	3. Click **Confirm** in the pop-up dialog box. A TRTC app with the same SDKAppID as the Chat app will be created in the [TRTC console](https://console.cloud.tencent.com/trtc). You can use the same account and authentication information for Chat and TRTC.
2. **Integrate the TUICallKit component**
Add the `TUICallKit` dependency to the `build.gradle` file in App:
```groovy
api project(':tuicallkit')
```
3. **Start and answer a video or audio call**
<table style="text-align:center;vertical-align:middle;width: 800px">
  <tr>
    <th style="text-align:center;" ><b>Starting a Call via a Message Page<br></b></th>
    <th style="text-align:center;" ><b>Starting a Call via a Contact Profile Page<br></b></th>
  </tr>
  <tr>
        <td><img style="width:400px" src="https://staticintl.cloudcachetci.com/yehe/backend-news/EseX367_%E9%9B%86%E5%90%88%281%29.png"  />    </td>
    <td><img style="width:400px" src="https://staticintl.cloudcachetci.com/yehe/backend-news/EseX367_%E9%9B%86%E5%90%88%281%29.png"  />    </td>
     </tr>
</table>
<ul>
<li>After integrating the TUICallKit component, the chat UI and contact profile UI display the **Video Call** and **Audio Call** buttons by default. When a user clicks either of the buttons, TUIKit automatically displays the call invitation UI and sends the call invitation request to the callee.</li>
<li>When an <strong>online</strong> user receives a call invitation with <strong>the app running in the foreground</strong>, TUIKit automatically displays the call receiving UI, where the user can answer or reject the call.</li>
<li>When an <strong>offline</strong> user receives a call invitation and wants to start the app to accept the call, the offline push capability is required. For how to implement offline push, see the next step.</li>
</ul>

4. **Add the offline push feature:**[](id:Step5)
To implement offline push for audio/video calls, follow the steps below:
	1. Configure offline push for the app. For more information, see [Offline Push Configuration](https://www.tencentcloud.com/document/product/1047/39156).
	2. Integrate the TUICallKit component.
	3. Use TUICallKit to initiate a call invitation. An offline push message is generated by default.

5. **Add value-added capabilities.**
After TUIChat and TUICallKit are integrated, when you send a voice message on the chat UI, **the voice message can be recorded with AI-based noise reduction and automatic gain control**. This feature relies on the audio/video call capability of Premium Edition or higher-level plans of the Chat service, which is supported in Chat SDK 7.0 and later versions. If the dependent plan expires, voice message recording is switched to the system API.
The following compares the voice messages recorded simultaneously using two Huawei P10 phones:
<table style="text-align:center;vertical-align:middle;width: 800px">
  <tr>
    <th style="text-align:center;" ><b>Voice Message Recorded by the System<br></b></th>
    <th style="text-align:center;" ><b>Voice Message with AI-based Noise Reduction and Automatic Gain Control Recorded by TUICallkit<br></b></th>
  </tr>
  <tr>
    <td>
      <audio id="audio" controls="" preload="none" >
	<source id="m4a" src="https://im.sdk.cloudcachetci.com/tools/resource/rain_system_record.m4a">
      </audio>
    </td>

    <td>
      <audio id="audio" controls="" preload="none">
    <source id="m4a" src="https://im.sdk.cloudcachetci.com/tools/resource/rain_tuicallkit_record_with_agc_aidenoise.m4a">
      </audio>
    </td>
  </tr>
</table>
	

>? For more hands-on tutorial videos, see [TUIKit Quick Integration (Android)](https://cloud.tencent.com/edu/learning/course-3130-56399)


[](id:textTranslation)
## Enabling Text Message Translation
When you are on the chat UI, you can tap and hold a text message in the message list, and tap the **Translate** button on the pop-up menu to translate the text message.
The translation feature is disabled by default, and the **Translate** button is not displayed on the menu that pops up when you tap and hold a text message.

To enable the translation feature, perform the following steps:
1. Text translation is a **value-added paid service**, and is billed based on the number of characters translated. The feature is currently in beta test. To try it out, please contact your Tencent Cloud rep. **If the translation service is not activated, even if the Translate button is displayed on the UI, the translation service cannot work properly.**
2. After the translation service is activated and before the chat UI is initialized, you can configure the system to display the **Translate** button. Sample code:
```java
// Display the Translate button
TUIChatConfigs.getConfigs().getGeneralConfig().setEnableTextTranslation(true);
```

> ! 
> 1. The text message translation feature is supported from TUIChat 7.0.
> 2. Only text messages, and quote and reply text messages support translation. Image, audio, video, file, and emoji messages do not support translation.
> 3. When you click **Translate**, the text will be translated into the language that is currently used by TUIChat. For example, if the current TUIChat language is English, the text will be translated into English regardless of which language it is in.

The following figure shows the effect after the translation service is activated and the **Translate** button display is enabled.
<dx-tabs>
::: Classic version

<table style="text-align:center;vertical-align:middle;width: 900px">
  <tr>
    <th style="text-align:center;" width="300px">Not Displaying the Translate Button</th>
    <th style="text-align:center;" width="300px">Displaying the Translate Button</th>
    <th style="text-align:center;" width="300px">Text Message Translation Effect</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/398a628b6a0a885c1f63c0f8d320c702.jpg"/></td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/ec5fa852d7ffa0ec8236418e09427bbc.jpg"/></td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/0e1b9927120ff048561270fcc7475595.jpg"/></td>
	 </tr>
</table>
:::
::: Minimalist version
<table style="text-align:center;vertical-align:middle;width: 900px">
  <tr>
    <th style="text-align:center;" width="300px">Not Displaying the Translate Button</th>
    <th style="text-align:center;" width="300px">Displaying the Translate Button</th>
    <th style="text-align:center;" width="300px">Text Message Translation Effect</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/b65557255c88aa0a1cc557c40515be80.jpg"/></td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/254884ffcd7cf16b3d4db58698e9314f.jpg"/></td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/4528dc6a31b06782d0279fc5cc81ab1a.jpg"/></td>
	 </tr>
</table>
:::
</dx-tabs>


## FAQs
#### What should I do when I receive the message "Manifest merger failed : Attribute application@allowBackup value=(true) from AndroidManifest.xml"?
In the Chat SDK, the value of `allowBackup` is `false` by default, indicating that the backup and restore feature of the app is disabled.
You can delete the `allowBackup` property from the `AndroidManifest.xml` file to disable the backup and restore feature. You can also add `tools:replace="android:allowBackup"` to the `application` node of the `AndroidManifest.xml` file to overwrite the Chat SDK configuration with your own configuration. 

For example:
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.tencent.qcloud.tuikit.myapplication">

    <application
        android:allowBackup="true"
        android:name=".MApplication"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.MyApplication"
        tools:replace="android:allowBackup">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

#### What should I do when I receive the message "NDK at /Users/***/Library/Android/sdk/ndk-bundle did not have a source.properties file"?
You only need to add you NDK path to the `local.properties` file. For example:
`ndk.dir=/Users/***/Library/Android/sdk/ndk/16.1.4479499`

#### What should I do when I receive the message "Cannot fit requested classes in a single dex file"?
The possible cause is that your API level is lower than expected. You need to enable `MultiDex` support in the `build.gradle` file in App and add `multiDexEnabled true` and the corresponding dependencies:
```groovy
android {
    defaultConfig {
        ...
        minSdkVersion 19
        targetSdkVersion 30
        multiDexEnabled true
    }
    ...
}
dependencies {
    implementation "androidx.multidex:multidex:2.0.1"
}
```
In addition, add the following code to the Application file:
```java
public class MyApplication extends SomeOtherApplication {
    @Override
    protected void attachBaseContext(Context base) {
        super.attachBaseContext(base);
        MultiDex.install(this);
    }
}
```

#### What should I do when I receive the message "Plugin with id 'kotlin-android' not found."?
Because TUIChat uses Kotlin code, you need to add the Kotlin build plug-in. For details, see [step 5 in the "Integrating Module Source Code" section](#buildStep5).
