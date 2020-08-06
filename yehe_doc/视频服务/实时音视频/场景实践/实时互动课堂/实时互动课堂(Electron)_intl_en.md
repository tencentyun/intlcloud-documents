## Demo
<table style="text-align:center;vertical-align:middle;width: 300px">
  <tr>
    <th width="150px">macOS</th>
    <th width="150px">Windows</th>
  </tr>
  <tr>
    <td><a href="https://trtc-1252463788.cos.ap-guangzhou.myqcloud.com/electron_sdk/solution/education/TRTC_Education_Demo-1.1.0.dmg"><img width="125px" height="125px" src="https://main.qcloudimg.com/raw/d03160ca4e5342a96464aaba1de97923.png"></a></td>
    <td><a href="https://trtc-1252463788.cos.ap-guangzhou.myqcloud.com/electron_sdk/solution/education/TRTC_Education_Demo%20Setup%201.1.0.exe"><img width="125px" height="125px" src="https://main.qcloudimg.com/raw/d03160ca4e5342a96464aaba1de97923.png"></a></td>
  </tr>
</table>


## Effect Demo
You can download and install the demo to experience the capabilities and effect of the real-time interactive teaching feature, such as teaching modes (audio, video, and screen sharing, etc.) and interactions (Q&A, raise hand, invite, end, etc.).

- Teacher client
 ![](https://main.qcloudimg.com/raw/35d33cb6003bd3575ee6bbfb0cbe6450.png)
- Student client
 ![](https://main.qcloudimg.com/raw/30e62d5c96c1ba31fc24c113ecfdb395.png)

To quickly implement real-time interactive teaching, you can directly modify the demo provided by TRTC for adaptation or use the provided [trtc-electron-education](https://intl.cloud.tencent.com/document/product/647/37279) component and implement custom UI.

## Reusing Demo UI
### Step 1. Create an application
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter the application name such as `TestEduDemo`, and click **Create Application**.

>?Note: this feature uses two basic PaaS services of Tencent Cloud, namely, [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When TRTC is activated, IM will be activated automatically.

<span id="ui.step2"></span>
### Step 2. Download the SDK and demo source code
1. Click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTCScenesDemo/TRTCEducation)** to enter GitHub and download the relevant SDK and supporting demo source code.
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.

### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#ui.step2).
2. Find and open the `TRTCEducation/app/debug/GenerateTestUserSig.js` file.
3. Set the relevant parameters in the `GenerateTestUserSig.js` file:
  <ul style="margin:0;"><li>SDKAPPID: it is 0 by default. Please replace it with your real `SDKAppID`.</li>
  <li>SECRETKEY: it is an empty string by default. Please replace it with your real key information.</li></ul> 
  <img src="https://main.qcloudimg.com/raw/1732ea2401af6111b41259a78b5330a4.png">
4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console** to manage the application.

>!The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Run the demo

```typescript
// Install YARN, which is used to manage the demo
npm install yarn -g
// Install required dependencies
yarn install
// Develop and debug
yarn dev
// Package
yarn package
```

>!
>- You can package for macOS only on macOS and package for Windows only on Windows.


### Step 5. Modify the demo source code
The following frameworks are used by the demo:
- typescript
- react & react hooks
- electron & electron-react-boilerplate
- element-ui

The following table lists the files and the corresponding UIs for easy adjustment:

| File | Feature Description |
| ----- | ----- |
| app/containers/HomePage.tsx | Implementation code for classroom entry UI |
| app/containers/ClassRoomPage.tsx | Implementation code for classroom UI |
| app/components/TeacherClass.tsx | Implementation code for teacher client UI of classroom |
| app/components/StudentClass.tsx | Implementation code for student client UI of classroom |
| app/components/Chat.tsx | Implementation code for chat room UI of classroom |
| app/components/UserList.tsx | Implementation code for member list UI of classroom |

## Implementing Custom UI
If the UI implemented by default in the demo does not meet your expectations, you can implement your own UI as needed simply by using the audio/video capabilities provided by the encapsulated [trtc-electron-education](https://www.npmjs.com/package/trtc-electron-education) component.
![](https://main.qcloudimg.com/raw/cba4f331a811dd5dbf31cce80bd1d826.png)

### Step 1. Integrate the SDK

```
// Import by using YARN
yarn add trtc-electron-education
// Import by using npm
npm i trtc-electron-education --save
```

### Step 2. Initialize the component
Initialize the component. The required key parameters are as detailed below:

| Parameter | Type | Description |
| ----- | ----- | ----- |
| sdkAppId | number | `SDKAppID`, which is required and can be viewed in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC Console</a>. |
| userID | string | User ID, which is required and can be specified by your account system. |
| userSig | string | Identity signature, which is required and acts as the login password. It can be calculated based on the `userID`. For more information on the calculation method, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |

```typescript
import TrtcElectronEducation from 'trtc-electron-education';
const rtcClient = new TrtcElectronEducation({
   sdkAppId: 1400***803,
   userID: '123'
   userSig: 'eJwtzM9****-reWMQw_'
 });
```

### Step 3. Start a class on the teacher client
1. The teacher calls the [createRoom](https://intl.cloud.tencent.com/document/product/647/37279#createRoom) method of the component to create a classroom.
```typescript
const params = {
      classId, // Classroom ID
      nickName // Nickname
}
rtcClient.createRoom(params).then(() => {
	// Created classroom successfully
})
```
2. The teacher calls the [enterRoom](https://intl.cloud.tencent.com/document/product/647/37279#enterRoom) method of the component to start a class.
```typescript
rtcClient.enterRoom({
      role: 'teacher', // Role
      classId // Classroom ID
})
```
3. The teacher calls the [openCamera](https://intl.cloud.tencent.com/document/product/647/37279#openCamera) method of the component to enable the local camera.
```typescript
const domEle = document.getElementById('test');
rtcClient.openCamera(domEle)
```
4. The teacher can share the local screen with students to present slides, courseware, etc.
 a. Call the [getScreenShareList](https://intl.cloud.tencent.com/document/product/647/37279#getScreenShareList) method of the component first to get the window list.
```typescript
const screenList = rtcClient.getScreenShareList()
```
b. Call [startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37279#startScreenCapture) of the component to start pushing the screen sharing stream.
```typescript
rtcClient.startScreenCapture({
      type,// Capture source type
      sourceId,// Capture source ID. For a window, this field indicates a window handle; for a screen, this field indicates a screen ID
      sourceName // Capture source name encoded in UTF-8
 })
```
5. During teaching, if the teacher wants to ask students a question to interact with them, the teacher can call the [startQuestionTime](https://intl.cloud.tencent.com/document/product/647/37279#startQuestionTime) method of the component to start Q&A. After the student client receives the command, the student can "raise hand" to ask to answer the question.
```typescript
rtcClient.startQuestionTime(classId) // `classId` is the classroom ID
```
6. After the student "raises hand", the teacher can call the [inviteToPlatform](https://intl.cloud.tencent.com/document/product/647/37279#inviteToPlatform) method of the component to invite the student to answer, and the invited student will automatically mic on.
```typescript
rtcClient.inviteToPlatform(userID) // `userID` of the invited student
```
7. The teacher can call the [finishAnswering](https://intl.cloud.tencent.com/document/product/647/37279#finishAnswering) method of the component to mic off the student.
```typescript
rtcClient.finishAnswering(userID)// `userID` of the student whose mic is disabled
```

### Step 4. Attend a class on the student client
1. The student calls the [enterRoom](https://intl.cloud.tencent.com/document/product/647/37279#enterRoom) method of the component to enter a classroom and prepare to listen.
```typescript
rtcClient.enterRoom({
      role: 'student', // Role
      classId // Classroom ID
})
```
2. After the teacher starts Q&A, the student can call the [raiseHand](https://intl.cloud.tencent.com/document/product/647/37279#raiseHand) method of the component to ask to speak.
```typescript
rtcClient.raiseHand()
```

### Step 5. Implement the chat room feature

The teacher and students can send text messages to each other in the chat room.
```typescript
const params = {
   classId: classId, // Classroom ID
   message: 'Hello' // Message content
}
rtcClient.sendTextMessage(params) // Send the message in the chat room
```
