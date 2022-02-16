## Introduction to TUIKit
TUIKit is a set of TUI components based on IM SDKs. It provides features such as the conversation, chat, search, relationship chain, group, and audio/video call features. You can use these TUI components to quickly build your own business logic.
<img style="width:800px" src="https://qcloudimg.tencent-cloud.cn/raw/033a69e0bec31ea140d59ee90bde1416.png"  /> 

## TUIKit Integration
### Environment requirements
- Android Studio 3.6.1
- Gradle-5.1.1
- Android Gradle Plugin Version 3.4.0

### Integrating module source code
1. Download the TUIKit source code from [GitHub](https://github.com/tencentyun/TIMSDK/tree/master/Android). Ensure that the TUIKit folder is at the same level as your project folder, for example:
<img src="https://qcloudimg.tencent-cloud.cn/raw/00bc0470857b850436663d9bf2ef9164.png" width="500"/>
2. According to your business requirements, add the corresponding TUI components in `settings.gradle`. For example, you can add tuichat to include the chat feature, add tuiconversation to include the conversation list feature, and add tuicalling to include the audio/video call feature. TUI components are independent of each other, and adding or removing them does not affect project compilation.
```groovy
// Include the upper-layer app module
include ':app'

// Include the internal communication module (require module)
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

// Include the search feature module (To use this module, you need to purchase the Flagship Edition package.)
include ':tuisearch'
project(':tuisearch').projectDir = new File(settingsDir, '../TUIKit/TUISearch/tuisearch')

// Include the group feature module
include ':tuigroup'
project(':tuigroup').projectDir = new File(settingsDir, '../TUIKit/TUIGroup/tuigroup')

// Include the audio/video call feature module
include ':tuicalling'
project(':tuicalling').projectDir = new File(settingsDir, '../TUIKit/TUICalling/tuicalling')
```
3. Add the following to `build.gradle` in App:
```groovy
dependencies {
    api project(':tuiconversation')
    api project(':tuicontact')
    api project(':tuichat')
    api project(':tuisearch')
    api project(':tuigroup')
    api project(':tuicalling')    
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
<img src="https://qcloudimg.tencent-cloud.cn/raw/510872c1232f6cf81d6678c41092164d.png" width="400"/>

## Quick Build
Instant messaging software usually consists of several basic UIs such as the conversation list, chat window, friend list, and audio/video call UIs. It only takes a few lines of code to build these UIs in your project. The process is as follows:

### Step 1. Log in to TUIKit

```java

// Initialize TUIKit during program startup, usually in the `onCreate` method of Application
TUILogin.init(this, SDKAPPID, null, null);
    
// Click Login on the user UI to log in to TUIKit
TUILogin.login(userId, userSig, new V2TIMCallback() {
	@Override
	public void onError(final int code, final String desc) {
	}

	@Override
	public void onSuccess() {
	}
});
```

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
// Conversation UI provided by tuiconversation
fragments.add(new TUIConversationFragment());
// Contacts UI provided by tuicontact
fragments.add(new TUIContactFragment());
ViewPager2 mainViewPager = findViewById(R.id.view_pager);
FragmentAdapter fragmentAdapter = new FragmentAdapter(this);
fragmentAdapter.setFragmentList(fragments);
mainViewPager.setOffscreenPageLimit(2);
mainViewPager.setAdapter(fragmentAdapter);
mainViewPager.setCurrentItem(0, false);
```

### Step 4. Build the audio/video call feature
TUI components allow users to initiate audio/video calls in chat UIs and can be quickly integrated with a few steps:

<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" ><b>Video Call<br></b></th>
    <th style="text-align:center;"><b>Audio Call</b><br></th>
  </tr>
  <tr>
    <td><img  src="https://qcloudimg.tencent-cloud.cn/raw/7519a451cd73bc1ec93c738dc3a0b18b.png"  />    </td>
    <td><img  src="https://qcloudimg.tencent-cloud.cn/raw/4d10292b10b72e719340a85c1a17aa59.png" />     </td>
	 </tr>
</table>


1. **Activate the TRTC service:**
	1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
	2. Click **Activate** under **Activate Tencent Real-Time Communication (TRTC)**.
	3. Click **Confirm** in the pop-up dialog box.
	 A TRTC app with the same SDKAppID as the IM app will be created in the [TRTC console](https://console.cloud.tencent.com/trtc). You can use the same account and authentication information for IM and TRTC.
2. **Integrate the TUICalling component:**
Add tuicalling dependencies to the `build.gradle` file in App:
```groovy
api project(':tuicalling')
```
3. **Initiate and answer a video or audio call:**
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
        <th style="text-align:center;" ><b>Initiate an Audio/Video Call<br></b></th>
    <th style="text-align:center;" ><b>Answer a Video Call<br></b></th>
    <th style="text-align:center;" ><b>Answer an Audio Call</b><br></th>
  </tr>
  <tr>
        <td><img style="width:212px" src="https://qcloudimg.tencent-cloud.cn/raw/f7d4b75ff1f299e655805518984a6e58.png"  />    </td>
    <td><img style="width:200px" src="https://qcloudimg.tencent-cloud.cn/raw/e201ea282ef9e757df2ade9bd8c71955.png"  />    </td>
    <td><img style="width:200px" src="https://qcloudimg.tencent-cloud.cn/raw/314875a92058f1e46296f458767cb0ba.png" />     </td>
     </tr>
</table>


	- After you integrate the TUICalling component, the chat UI displays the **Video Call** and **Audio Call** buttons by default. When a user clicks either button, TUIKit automatically displays the call invitation UI and sends the call invitation request to the callee.
	- When an **online** user receives a call invitation with **the app running in the foreground**, TUIKit automatically displays the call receiving UI, where the user can answer or reject the call.
	- When an **offline** user receives a call invitation, offline push is required to wake up the App call. For more information about offline push, see [Add the offline push feature](#Step5).
4. **Add the offline push feature:**[](id:Step5)
To implement offline push for audio/video calls, follow these steps:
	1. Configure offline push for App.
	2. Integrate the TUICalling component.
	3. Use TUICalling to initiate a call invitation. An offline push message will be generated by default. For more information about the message generation logic, see the `sendOnlineMessageWithOfflinePushInfo` method in the [TRTCCallingImpl.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUICalling/tuicalling/src/main/java/com/tencent/liteav/trtccalling/model/impl/TRTCCalling.java) class of the TUICalling module.
	4. After the peer receives the offline push message, refer to the `redirect` method in the [OfflineMessageDispatcher.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/OfflineMessageDispatcher.java) class in App to wake up the call UI.

## FAQs

### 1. Why do I receive the message "Manifest merger failed : Attribute application@allowBackup value=(true) from AndroidManifest.xml"?
In the IM SDK, the value of `allowBackup` is `false` by default, indicating that the backup and restore feature of the application is disabled. You can delete the `allowBackup` property from the `AndroidManifest.xml` file to disable the backup and restore feature. You can also add `tools:replace="android:allowBackup"` to the `application` node of the `AndroidManifest.xml` file to overwrite the IM SDK configuration with your own configuration. For example:
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

### 2. Why do I receive the message "NDK at /Users/***/Library/Android/sdk/ndk-bundle did not have a source.properties file"?
The possible cause is that the versions of the Gradle and Gradle plugin in use are higher than expected. You can use the recommended versions shown as follows:
<img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/ae3416874722fb086abcdfc8e2ed8a39.png" />

Alternatively, you can keep using your current Gradle version by adding your NDK path to the `local.properties` file. For example:
`ndk.dir=/Users/***/Library/Android/sdk/ndk/16.1.4479499`

### 3. Why do I receive the message "Cannot fit requested classes in a single dex file"?
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

### 4. What should I be aware of if I have created the TRTC and IM SDKAppIDs and want to integrate the IM SDK and TRTC SDK at the same time?
If you have created the TRTC and IM SDKAppIDs, you cannot use the same account or authentication information for these two apps. You need to generate a UserSig corresponding to the TRTC SDKAppID to perform authentication. For more information on how to generate UserSig, see [How to Generate Usersig](https://intl.cloud.tencent.com/document/product/647/35166).
After obtaining the TRTC SDKAppID and UserSig, you need to use them to replace the corresponding values in the [TRTCCallingImpl](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUICalling/tuicalling/src/main/java/com/tencent/liteav/trtccalling/model/impl/TRTCCalling.java) source code:
```
 private void enterTRTCRoom() {
	...
    TRTCCloudDef.TRTCParams TRTCParams = new TRTCCloudDef.TRTCParams(mSdkAppId, mCurUserId, mCurUserSig, mCurRoomID, "", "");
	...
 }
```

### 5. How long is the default call invitation timeout duration? How can I modify the default timeout duration?
The default call invitation timeout duration is 30s. You can modify the `TIME_OUT_COUNT` field in [TRTCCallingImpl.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/TUIKit/TUICalling/tuicalling/src/main/java/com/tencent/liteav/trtccalling/model/impl/TRTCCalling.java) to customize the timeout duration.

### 6. Will an invitee receive a call invitation if the invitee goes offline and then online within the call invitation timeout duration?
- If the call invitation is initiated in a one-to-one chat, the invitee can receive the call invitation.
- If the call invitation is initiated in a group chat, the invitee cannot receive the call invitation.
