This article describes how to configure, compile, and run the IM trial demo in minutes.
The following video illustrates the steps you must perform:
<div class="doc-video-mod"><iframe src="https://cloud.tencent.com/edu/learning/quick-play/2269-33124?source=gw.doc.media&withPoster=1&notip=1"></iframe></div>

<span id="step1"></span>
## Step 1: Create an App
1. Log in to the [IM console](https://console.cloud.tencent.com/im).
 > If you already have an app, record its SDKAppID and [skip to Step 2](#step2).
 > A Tencent Cloud account can create a maximum of 100 IM apps. If you want to create more apps, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost**. **Proceed with caution**.
 >
2. Click **Add Application**.
3. In the **Create Application** dialog box, enter an app name and click **OK**.
  After the app is created, you can view the status, service version, SDKAppID, creation time, and expiry time of the new app on the overview page of the console. Record its SDKAppID.
  ![](https://main.qcloudimg.com/raw/2753962b67754a9ebb2a2a5b8042f2ef.png)
  

<span id="step2"></span>
## Step 2: Obtain Key Information

1. Click the desired app to enter the basic configuration page of the app.
2. In the **Basic Info** area, click **Display key**. Copy and save the key.
 > Store the key securely so it does not leak.

<span id="step3"></span>
## Step 3: Download and Configure the Demo Source Code

1. Download the IM Demo project. For the address, refer to [SDK Download](https://intl.cloud.tencent.com/document/product/1047/33996).
2. Open the project that corresponds to the desired platform and find the `GenerateTestUserSig` file.
 <table>
     <tr>
         <th nowrap="nowrap">Platform</th>  
         <th nowrap="nowrap">Relative path</th>  
     </tr>
  <tr>      
      <td>Android</td>   
      <td>Android/app/src/main/java/com/tencent/qcloud/tim/demo/signature/GenerateTestUserSig.java</td>   
     </tr> 
  <tr>
      <td>iOS</td>   
      <td>iOS/TUIKitDemo/TUIKitDemo/Debug/GenerateTestUserSig.h</td>
     </tr> 
  <tr>      
      <td>Mac</td>   
      <td>Mac/TUIKitDemo/TUIKitDemo/Debug/GenerateTestUserSig.h</td>   
     </tr>  
  <tr>      
      <td>Windows</td>   
      <td>cross-platform/Windows/IMApp/IMApp/GenerateTestUserSig.h</td>   
     </tr>  
  <tr>      
      <td>Web (general)</td>   
      <td>H5/dist/debug/GenerateTestUserSig.js</td>   
     </tr>  
  <tr>      
      <td>WeChat Mini Program</td>   
      <td>WXMini/dist/wx/debug/GenerateTestUserSig.js</td>   
     </tr>  
</table>
3. Configure parameters in the `GenerateTestUserSig` file.
 > For the purpose of this article, the Android project is used as an example. Use Android Studio to open it.
  >
 - SDKAPPID: enter the SDKAppID obtained in [Step 1](#step1).
 - SECRETKEY: enter the key obtained in [step 2](#step2).
 ![](https://main.qcloudimg.com/raw/e7f6270bcbc68c51595371bd48c40af7.png)


> This article describes how to configure the client code with the SECRETKEY to generate an UserSig. However, this method presents a security risk because the client code can be decompiled to reveal the SECRETKEY. As long as the person have your SECRETKEY, he or she can steal your Tencent Cloud traffic. Use this method **only to run and debug the demo project locally**.
> The correct `UserSig` distribution method is to integrate the `UserSig` code into your server and provide an API that generates `UserSig` dynamically upon client request. For more information, refer to [Server-side UserSig Generation](https://intl.cloud.tencent.com/document/product/1047/34385).

## Step 4: Compile and Run the Demo
Use the IDE of your choice to compile and run the demo. For more information, refer to `README.md` in the corresponding directory of the demo project cloned in [Step 3](#step3).

**The compilation and running of the iOS and Mac demo require pod integration. The detailed procedure is as follows:**
1. Run the following command in a terminal to check the pod version:
```
pod --version
```
If no pod exists or the pod version is earlier than 1.7.5, run the following command to install the latest pod:
```
// Change gem sources.
gem sources --remove https://rubygems.org/
gem sources --add https://gems.ruby-china.com/
// Install pods.
sudo gem install cocoapods -n /usr/local/bin
// If multiple Xcodes are installed, run the following command to select an Xcode version (use the latest Xcode version in most cases):
sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer
// Update the local pod library.
pod setup
```
2. Run the following commands to install dependent libraries:
```
//iOS
cd iOS/TUIKitDemo
pod install
//Mac
cd Mac/TUIKitDemo
pod install
```
 If installation fails, run the following commands to update the local CocoaPods repository list:
 ```bash
 pod repo update
```
3. Compile and run the project.
 - iOS: navigate to iOS/TUIKitDemo and open `TUIKitDemo.xcworkspace` to compile and run the project.
 - Mac: navigate to Mac/TUIKitDemo and open `TUIKitDemo.xcworkspace` to compile and run the project.



