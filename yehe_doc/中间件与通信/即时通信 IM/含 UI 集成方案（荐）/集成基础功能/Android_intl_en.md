## Environment Requirements
- Android Studio 3.6.1
- Gradle 5.1.1
- Android Gradle Plugin Version 3.4.0

## Integrating Module Source Code
1. Download the TUIKit source code from [GitHub](https://github.com/tencentyun/TIMSDK/tree/master/Android). Ensure that the TUIKit folder is at the same level as your project folder, for example:
<img src="https://qcloudimg.tencent-cloud.cn/raw/00bc0470857b850436663d9bf2ef9164.png" width="500"/>
2. According to your business requirements, add the corresponding TUI components in `settings.gradle`. For example, you can add TUIChat to implement the chat feature, add TUIConversation to implement the conversation list feature, and add TUICallKit to implement the audio/video call feature. TUI components are independent of each other, and adding or removing them does not affect project compilation.
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
    api project(':tuicallkit')  
}
```
4. Add the following to the `gradle.properties` file to automatically convert third-party libraries to use AndroidX:
```properties
android.enableJetifier=true
```
5. Add the following to the `build.gradle` file of the root project to add the Maven repository:
```groovy
allprojects {
    repositories {
        mavenCentral()
        maven { url "https://mirrors.tencent.com/nexus/repository/maven-public/" }
    }
}
```
6. Sync the project, and compile and run it. The expected project structure is shown in the following figure:<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/454abb6051a7a94a08559d8404e5aec7.png" width="400"/>

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

Add the following to the `onCreate` method in `MainActivity.java`:
```java
List<Fragment> fragments = new ArrayList<>();
// Conversation UI provided by TUIConversation
fragments.add(new TUIConversationFragment());
// Contacts UI provided by TUIContact
fragments.add(new TUIContactFragment());
ViewPager2 mainViewPager = findViewById(R.id.view_pager);
FragmentAdapter fragmentAdapter = new FragmentAdapter(this);
fragmentAdapter.setFragmentList(fragments);
mainViewPager.setOffscreenPageLimit(2);
mainViewPager.setAdapter(fragmentAdapter);
mainViewPager.setCurrentItem(0, false);
```

### Step 4. Build the audio/video call feature
TUI components allow users to start audio/video calls in chat UIs and can be quickly integrated with a few steps:

<table style="text-align:center;vertical-align:middle;width: 800px">
  <tr>
    <th style="text-align:center;" ><b>Video Call<br></b></th>
    <th style="text-align:center;"><b>Audio Call</b><br></th>
  </tr>
  <tr>
    <td><img src="https://qcloudimg.tencent-cloud.cn/raw/b9f362503d25179db6f75fc91cfd000a.jpg"/></td>
    <td><img src="https://qcloudimg.tencent-cloud.cn/raw/2f037d7de8270c0edef68c0b829465ec.png"/></td>
	 </tr>
</table>

1. **Activate the TRTC service**
	1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
	2. Click **Free trial** under **Activate Tencent Real-Time Communication (TRTC)** to activate the 7-day free trial service of TUICallKit.
	3. Click **Confirm** in the pop-up dialog box. A TRTC app with the same SDKAppID as the IM app will be created in the [TRTC console](https://console.cloud.tencent.com/trtc). You can use the same account and authentication information for IM and TRTC.
2. **Integrate the TUICallKit component**
Add the `tuicallkit` dependency to the `build.gradle` file in App:
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
        <td><img style="width:400px" src="https://qcloudimg.tencent-cloud.cn/raw/b34f84493214ca44bef32d0257d66693.png"  />    </td>
    <td><img style="width:400px" src="https://qcloudimg.tencent-cloud.cn/raw/65d76fa2bea287a22c11b1f972996397.png"  />    </td>
     </tr>
</table>

<ul>
<li>After integrating the TUICallKit component, the chat UI and contact profile UI display the <b>Video Call</b> and <b>Audio Call</b> buttons by default. When a user clicks either of the buttons, TUIKit automatically displays the call invitation UI and sends the call invitation request to the callee.</li>
<li>When an <strong>online</strong> user receives a call invitation with <strong>the app running in the foreground</strong>, TUIKit automatically displays the call receiving UI, where the user can answer or reject the call.</li>
<li>When an <strong>offline</strong> user receives a call invitation and wants to start the app to accept the call, the offline push capability is required. For how to implement offline push, see the next step.</li>
</ul>

4. **Add the offline push feature:**[](id:Step5)
	To implement offline push for audio/video calls, follow the steps below:
	1. Configure offline push for the app. For more information, see [Offline Push Configuration](https://www.tencentcloud.com/document/product/1047/39156).
	2. Integrate the TUICallKit component.
	3. Use TUICallKit to initiate a call invitation. An offline push message is generated by default.

## FAQs
#### What should I do when I receive the message "Manifest merger failed : Attribute application@allowBackup value=(true) from AndroidManifest.xml"?
In the IM SDK, the value of `allowBackup` is `false` by default, indicating that the backup and restore feature of the app is disabled.
You can delete the `allowBackup` property from the `AndroidManifest.xml` file to disable the backup and restore feature. You can also add `tools:replace="android:allowBackup"` to the `application` node of the `AndroidManifest.xml` file to overwrite the IM SDK configuration with your own configuration. 

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
The possible cause is that the versions of the Gradle and Gradle plugin in use are higher than expected. You can use the recommended versions shown as follows:
<img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/ae3416874722fb086abcdfc8e2ed8a39.png" />

Alternatively, you can keep using your current Gradle version by adding your NDK path to the `local.properties` file. For example:
`ndk.dir=/Users/***/Library/Android/sdk/ndk/16.1.4479499`

#### What should I do when I receive the message "Cannot fit requested classes in a single dex file"?
The possible cause is that your API level is lower than expected. You need to enable `MultiDex` support in the `build.gradle` file in App and add `multiDexEnabled true` and the corresponding dependencies:
```groovy
android {
    defaultConfig {
        ...
        minSdkVersion 15
        targetSdkVersion 28
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

#### What should I do if the resource file cannot be found during TUIKit compilation, for example, when `getString(R.string.sure)` is invoked in the code and a message indicating the failure to find the `sure` symbol is reported during the compilation?
For Android Studio of the latest version and Gradle Android of later versions, `android.nonTransitiveRClass=true` is added to the `gradle.properties` file by default when you create a project, and you only need to change it to `android.nonTransitiveRClass=false`.

