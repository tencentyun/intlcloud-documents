## Free Demo
<input type="button" value="Windows" style="height: 30px;width: 150px;min-width: 24px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;white-space: nowrap;margin-right:10px;"  onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education/TRTC_Education_Demo%20Setup%201.1.0.exe')" />

<input type="button" value="macOS" style="height: 30px;width: 150px;margin-top: 5px;min-width: 24px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;white-space: nowrap;" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education/TRTC_Education_Demo-1.1.0.dmg')" />

## Using the Demo UI
[](id:ui.step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g. `TestEduDemo`, and click **Create**.

>?The real-time interactive teaching feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.


[](id:ui.step2)
### Step 2. Download the SDK and demo source code
1. Download the SDK and demo source code for your platform.
2. Click **Next**.

[](id:ui.step3)
### Step 3. Configure demo project files
1. In the **Modify Configuration** step, select the development platform in line with the source package downloaded.
2. Find and open the `Electron/js/GenerateTestUserSig.js` file.
3. Set parameters in the `GenerateTestUserSig.js` file:
<ul>
 <li/>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.
 <li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct UserSig distribution method is to integrate the computing code of UserSig into your server and provide an app-oriented API. When UserSig is required, your app can send a request to the business server to obtain the dynamic UserSig. For more information, please see "Generating a UserSig on the Server" in [Generating UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Run the demo

```typescript
// Install Yarn, which is used to manage the demo
npm install yarn -g
// Install the required dependencies
yarn install
// Develop and debug
yarn dev
// Package
yarn package
```

>!  You can package for macOS only on macOS and for Windows only on Windows.


### Step 5. Modify the demo source code
The following frameworks are used by the demo:
- typescript
- react & react hooks
- electron & electron-react-boilerplate
- element-ui

The following table lists the files and the UI views they represent. You can refer it to when making UI changes.

| File | Description |
| ----- | ----- |
| app/containers/HomePage.tsx | Implementation code for the classroom entry view |
| app/containers/ClassRoomPage.tsx | Implementation code for the classroom view |
| app/components/TeacherClass.tsx | Implementation code for teacher-end views |
| app/components/StudentClass.tsx | Implementation code for student-end views |
| app/components/Chat.tsx | Implementation code for the chat room view |
| app/components/UserList.tsx | Implementation code for the member list view |

## Customizing Your Own UI
If the UI in the demo does not meet your expectations, you can use only the audio and video capabilities of the [trtc-electron-education](https://www.npmjs.com/package/trtc-electron-education) component and customize your own UI.
![](https://main.qcloudimg.com/raw/cba4f331a811dd5dbf31cce80bd1d826.png)

### Step 1. Integrate the SDK

```
// Import via Yarn
yarn add trtc-electron-education
// Import via npm
npm i trtc-electron-education --save
```

### Step 2. Initialize the component
Initialize the component. The table below lists the required key parameters.

| Parameter | Type | Description |
| ----- | ----- | ----- |
| sdkAppId | number | `SDKAppID`, which is required and can be viewed in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a> |
| userID | string | User ID, which is required and can be assigned by your account system |
| userSig | string | User signature, which acts as a login password and is required. It is calculated based on user ID. For more information, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |

```typescript
import TrtcElectronEducation from 'trtc-electron-education';
const rtcClient = new TrtcElectronEducation({
   sdkAppId: 1400***803,
   userID: '123'
   userSig: 'eJwtzM9****-reWMQw_'
 });
```

### Step 3. Start a class as a teacher.
1. Call the [`createRoom`](https://intl.cloud.tencent.com/document/product/647/37279#createRoom) method of the component to create a classroom.
```typescript
const params = {
      classId, // Classroom ID
      nickName // Nickname
}
rtcClient.createRoom(params).then(() => {
	// Classroom created
})
```
2. Call the [`enterRoom`](https://intl.cloud.tencent.com/document/product/647/37279#enterRoom) method of the component to start a class.
```typescript
rtcClient.enterRoom({
      role: 'teacher', // Role
      classId // Classroom ID
})
```
3. Call the [openCamera](https://intl.cloud.tencent.com/document/product/647/37279#openCamera) method of the component to turn on the local camera.
```typescript
const domEle = document.getElementById('test');
rtcClient.openCamera(domEle)
```
4. Share your screen, e.g., a PowerPoint or courseware.
 a. Call the [getScreenShareList](https://intl.cloud.tencent.com/document/product/647/37279#getScreenShareList) method of the component to get the window list.
```typescript
const screenList = rtcClient.getScreenShareList()
```
 b. Call the [startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37279#startScreenCapture) method of the component to push screen sharing streams.
```typescript
rtcClient.startScreenCapture({
      type,// Capture source type
      sourceId,// Capture source ID, which is a window handle if a window is shared or a screen ID if the screen is shared
      sourceName // Capture source name, which is UTF-8-encoded
 })
```
5. To ask students questions, call the [startQuestionTime](https://intl.cloud.tencent.com/document/product/647/37279#startQuestionTime) method of the component to start Q&A. After receiving the event notification, students can "raise hands" to answer the questions.
```typescript
rtcClient.startQuestionTime(classId) // `classId` is the classroom ID
```
6. When students "raise hands", call the [inviteToPlatform](https://intl.cloud.tencent.com/document/product/647/37279#inviteToPlatform) method of the component to invite a student to answer. The student’s mic will be turned on automatically.
```typescript
rtcClient.inviteToPlatform(userID) // `userID` of the invited student
```
7. After the student finishes answering, call the [finishAnswering](https://intl.cloud.tencent.com/document/product/647/37279#finishAnswering) method of the component to turn the student’s mic off.
```typescript
rtcClient.finishAnswering(userID)// `userID` of the student whose mic is to be turned off
```

### Step 4. Attend a class as a student
1. Call the [enterRoom](https://intl.cloud.tencent.com/document/product/647/37279#enterRoom) method of the component to enter a classroom.
```typescript
rtcClient.enterRoom({
      role: 'student', // Role
      classId // Classroom ID
})
```
2. After the teacher starts Q&A, call the [raiseHand](https://intl.cloud.tencent.com/document/product/647/37279#raiseHand) method of the component to request to answer.
```typescript
rtcClient.raiseHand()
```

### Step 5. Implement the chat room feature.

The teacher and students can send text messages to each other in a chat room.
```typescript
const params = {
   classId: classId, // Classroom ID
   message: 'Hello' // Message content
}
rtcClient.sendTextMessage(params) // Send the message in the chat room
```
