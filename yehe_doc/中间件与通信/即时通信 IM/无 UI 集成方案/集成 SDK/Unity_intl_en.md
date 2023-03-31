4. This document describes how to quickly integrate the Chat SDK for Unity to your projects. To configure and integrate the SDK, follow these steps.
   
   ## Environment Requirements
   
   | Platform | Version                                                      |
   | -------- | ------------------------------------------------------------ |
   | Unity    | 2019.4.15f1 or later                                         |
   | Android  | Android Studio 3.5 or later; devices with Android 4.1 or later for apps |
   | iOS      | Xcode 11.0 or later. Ensure that your project has a valid developer signature. |
   
   ## UPM Integration (Recommended)
   
   1. Find the `manifest.json` file:
   ![](https://qcloudimg.tencent-cloud.cn/raw/88597bf131303e1b444baa33c641924e.png)
   2. Modify it as follows:
   ```json
      {
        "dependencies":{
          "com.tencent.imsdk.unity":"https://github.com/TencentCloud/chat-sdk-unity.git#unity"
        }
      }
   ```
   3. Open the project in the Unity Editor, wait until dependencies are loaded, and confirm the Tencent Cloud Chat is successfully loaded.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/d98dfb17bbee6c0319e370de6f2ba9dd.jpg)
   4. This is a test step. You can download [IM_Api_Example](https://github.com/TencentCloud/tc-chat-sdk-unity/tree/main/Assets/IM_Api_Example) and put it in your project after decompression.
      <img src="https://qcloudimg.tencent-cloud.cn/raw/7c7e35b688673c3bca02b95f6ca74e4a.png" width="70%">
      
       > ?IM_Api_Example is a demo used to test the callback data of the SDK's API. You can also call the API during early project development to manipulate your project.
      
       Drag all the scenes under the `IM_Api_Example/Assets` folder to `Build Settings`, and make sure that the `Main` scene is put at the first place.
       <img src="https://qcloudimg.tencent-cloud.cn/raw/b4235594ea96e60960a31f8c7e7edd67.jpg" width="35%">
      
       Double-click the `Main` scene under `IM_Api_Example/Assets` to start the demo. Here, you can select the language.
       <img src="https://qcloudimg.tencent-cloud.cn/raw/16d9c669d4c5b4932490452ec421ca89.jpg" width="35%">
      
       Click ![](https://qcloudimg.tencent-cloud.cn/raw/471e34746e4accceea25945e12223000.png) on the right of the header and enter the information.
       <img src="https://qcloudimg.tencent-cloud.cn/raw/5b5641156812d46d7e03218e856385a8.jpg" width="35%">
      
       Click **InitSDK** and **Login** in **Base Module** for initialization and login. Then you can call the APIs available in IM_Api_Example.
       <img src="https://qcloudimg.tencent-cloud.cn/raw/4b5cff4c369a770f980b16a017f6d329.jpg" width="23%"> <img src="https://qcloudimg.tencent-cloud.cn/raw/a2d0dfab936904bf8703ef8240656ab6.jpg" width="23%"> <img src="https://qcloudimg.tencent-cloud.cn/raw/cc01b9a6b752f26b056d04f346bc1056.jpg" width="23%">
