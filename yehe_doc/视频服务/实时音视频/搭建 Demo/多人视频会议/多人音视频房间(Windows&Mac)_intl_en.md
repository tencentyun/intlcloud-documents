This document describes the `TUIRoom` component for PC, an audio/video communication and collaboration tool with flexible layout and high adaptability. It can be used in various scenarios such as online collaboration, remote recruitment, remote diagnosis, insurance claim, online customer service, video interview, digital government services, finance digitization, online conferencing, and online education. It is integrated in depth with many industrial scenarios to help enterprises reduce costs, improve efficiency, and promote digitization for higher competitiveness.
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the app we provide to try out the component.

## Solution Strengths
- `TUIRoom` integrates various capabilities such as ultra-low-latency audio/video call, chat room, screen sharing, beauty filter, device detection, and statistics, covering the common features of group audio/video room.
- It can be further developed as needed to quickly implement custom UI and layout, helping you quickly launch your business.
- It encapsulates the basic TRTC and IM SDKs to implement basic logic control and provides APIs for you to call features easily.

## Connection Guide
To quickly implement the group audio/video room feature, you can modify the demo app we provide and adapt it to your needs. You can also use the `Module` module in the app and customize your own UI.

[](id:step1_1)
### Step 1. Download the app source code
Click [RoomApp](https://github.com/tencentyun/TUIMeeting) to clone or download the source code.

[](id:step1_2)
### Step 2. Configure the application file
<dx-tabs>
::: Configuration for Windows
1. Find and open `Windows\RoomApp\utils\usersig\win\GenerateTestUserSig.h`.
2. Set parameters in `GenerateTestUserSig.h`:
	- **SDKAPPID**: `0` by default. Set it to the actual `SDKAPPID`.
	- **SECRETKEY**: empty by default. Set it to the actual `SECRETKEY`.
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
:::
::: Configuration for macOS
1. Find and open `Windows\RoomApp\utils\usersig\mac\UserSigConfig.h`.
2. Set parameters in `UserSigConfig.h`:
	- **SDKAPPID_**: `0` by default. Set it to the actual `SDKAPPID`.
	- **SecretKey_**: empty by default. Set it to the actual `SECRETKEY`.
:::
</dx-tabs>

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the app**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:step1_3)
### Step 3. Configure and run the app
<dx-tabs>
::: Configuration for Windows
1. Use Virtual Studio 2015 or above as the compilation environment.
2. The app UI is the currently popular Qt framework on 5.9. Download and install Qt and add it to Visual Studio, or modify the Qt configuration in the app project based on your Qt version.
3. Open the `RoomApp.vcxproj` source code project under `RoomApp` and compile and run the program.

:::
::: Configuration for macOS
1. Use QtCreator as the compilation environment. To use QtCreator, select it when installing Qt, and its version is the same as that of the Qt official installation package.
2. The app UI is the currently popular Qt framework on 5.9. Download and install Qt 5.9 and configure the `QTDIR` system environment variable to point it to the installation directory of Qt.
3. Open the `RoomApp.pro` source code project under `RoomApp` and compile and run the program.
:::
</dx-tabs>

[](id:step1_4)
### Step 4. Modify the demo app’s source code
- The module layer encapsulates TRTC and IM to implement basic logic control and provides feature APIs for you to call features easily.
- The `App` module is a UI module, which contains the UI feature implementation. You can further develop UI as needed or replace the entire UI.

## Tryout
>! You need at least two devices to try out the application.
### Login page
Enter a room ID and a unique username to log in as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/71f2649be2c654e1c5f217dc10e88efc.png)

### Device detection page
Here, you can detect devices or set the device that will be used when a user enters the room and set the beauty filter as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/e5aed81f7ad0c07193c5506ebe0466d1.png)

### Homepage
The first user entering the room will be the anchor. The homepage contains components such as the mic-on list, bottom toolbar, and top toolbar.
![](https://qcloudimg.tencent-cloud.cn/raw/33d901c254c6c37c8afa4bce759b0bb3.png)

### Mic-on list
It displays all users in the current room. If a user enables the camera and mic, you can watch the video image and hear the voice of the user.

### Bottom toolbar
It implements features such as local mic/camera control, screen sharing control, user list, and chat room.

### Top toolbar
It implements features such as network information display, page settings, and mic-on list layout.

### Settings window
In the settings window, you can select devices, set beauty filter parameters, and set other parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/9eb20c81799dddc5be3f3fa7ef88dbac.png)

### Chat room
- Group members can chat in the chat room.
- The anchor can mute/unmute all members.
![](https://qcloudimg.tencent-cloud.cn/raw/9d927c98a595667d9f3f16d597abc77e.png)

### Exiting a room
There are two options when the anchor exits the room:
- **Dismiss the room**: all users need to exit the room.
- **Leave the room**: the room's anchor permission will be transferred to another user.

![](https://qcloudimg.tencent-cloud.cn/raw/e2485085cdb43de94ef9d8bc6851a436.png)

## Customizing UI
The `Module` module in the source code encapsulates the TRTC and IM SDKs. You can view the API functions and other definitions provided by this module in `TUIRoomCore.h`, `TUIRoomCoreCallback.h`, and `TUIRoomDef.h` files and use the corresponding APIs to implement your own custom UI.

[](id:step2_1)
### Step 1. Integrate the SDK
Download the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/34615) and [IM SDK](https://intl.cloud.tencent.com/document/product/1047/33996) at the official website. Then, replace the files in the `IM SDK` and `LiteAVSDK` directories in the SDK directory at the outer layer with them respectively.
>! The IM SDK for C++ is used.

| SDK | Download Page | Integration Guide |
|--|--|--|
|TRTC SDK|[Download](https://intl.cloud.tencent.com/document/product/647/34615)|[Windows](https://intl.cloud.tencent.com/document/product/647/35095)|
|IM SDK|[Download](https://intl.cloud.tencent.com/document/product/1047/33996)|[SDK Integration (Windows)](https://intl.cloud.tencent.com/document/product/1047/34310)|

[](id:step2_2)
### Step 2. Configure the SDK directories and library files of the project
- **For Windows**: in Visual Studio, configure the header file directory, static library directory, and static dependency library files.
- **For macOS**: add the dependency libraries and file directories to the `pro` and `pri` files.

[](id:step2_3)
### Step 3. Create a singleton and log in
1. Call the `IUIRoomCore::Instance` API to create and use the `IUIRoomCore` singleton.
2. Call the `AddCallback` API to set the callback class in order to receive the callback notifications of the SDK.
3. Call the `Login` API for login.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>sdk_appid</td>
<td>You can view `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr>
<tr>
<td>user_id</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend you set it based on your business account system.</td>
</tr>
<tr>
<td>user_sig</td>
<td>Tencent Cloud's proprietary security signature. To obtain one, see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr>
</tbody></table>

[](id:step2_4)
### Step 4. Set a nickname
After successful login, call `SetSelfProfile` to set the user profile.

[](id:step2_5)
### Step 5. Create a room
1. A member calls the `CreateRoom` API to create a room. After successful room creation, the member enters the rooms (including chat room and TRTC room) as the anchor.
2. The member calls the `StartCameraPreview` API to start capturing and displaying the local video.

![](https://qcloudimg.tencent-cloud.cn/raw/485afdb0dc5218a03410de86b215004d.png)

[](id:step2_6)
### Step 6. Dismiss the room
1. The anchor calls the `DestoryRoom` API to dismiss the room and IM group chat and exit the TRTC room.
2. Room members receive the `OnExitRoom` callback message that notifies them of group dismissal and exit the TRTC room.

[](id:step2_7)
### Step 7. Transfer the room
1. The anchor calls the `TransferRoomMaster` API to transfer the room to another user before leaving the room.
2. Room members receives the `OnRoomMasterChanged` callback message that notifies them of room anchor change.
3. The new anchor gets the anchor permission to control the group members.

[](id:step2_8)
### Step 8. Enter a room
1. The room entry process is basically the same as the room creation process. When entering a room, the member needs to create a room first and will enter the room as a member if room creation fails.
2. After room creation fails, the member will get the room information first and then enter the room.
3. Other members receive the `OnRemoteUserEnter` callback that notifies them of room entry by the member.

![](https://qcloudimg.tencent-cloud.cn/raw/89d63df3ad5243e3b45386777fbb07e5.png)

[](id:step2_9)
### Step 9. Exit a room
1. The member calls the `LeaveRoom` API to exit the IM and TRTC rooms.
2. Other members receive the `OnRemoteUserLeave` callback that notifies them of the room exit by the member.

[](id:step2_10)
### Step 10. Enable screen sharing.
1. The member calls the `StartScreenCapture` API for screen sharing.
2. Other members receive the `OnRemoteUserScreenAvailable` callback that notifies them of screen sharing by the member.

>? You need to implement the window selection logic for the screen sharing module. For the specific implementation, see `ScreenShareWindow.h` in `App`.

[](id:step2_11)
### Step 11. Implement text chat and muting notifications.
1. Call the `SendChatMessage` API to send a text message. Other members in the room can receive the `OnRecevieChatMessage` callback message and get the chat message for display.
2. The anchor can call the `MuteChatRoom` API to mute/unmute other members in the chat room. The members will receive the `OnChatRoomMuted` callback, and the UI layer will process the callback accordingly.
