This document introduces how to quickly run through the IM demo.


## Step 1: Create an App
1. Log in to the [IM console](https://console.cloud.tencent.com/im).
 >? If you already have an app, record its SDKAppID and [obtain key information](#step2).
 > A Tencent Cloud account can create a maximum of 300 IM apps. If you want to create more apps, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app first and then create a new one. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost**. **Proceed with caution**.
 >
2. Select a region.
3. Click **+Add App**.
4. In the **Create App** dialog box, enter your app name, and click **OK**.
    After creation, you can see the status, service version, SDKAppID, creation time, and expiry time of the new app on the overview page of the console. Record the SDKAppID.
    


## Step 2: Obtain Key Information

1. Click the target app card to enter the basic configuration page of the app.
2. In the **Basic Information** area, click **Display Key**, and then copy and save the key information.
 >! Please store the key information properly to prevent leakage.

## Step 3: Download and Configure the Demo Source Code

1. Download the IM Demo project. For more information about the specific download address, see [SDK Download](https://intl.cloud.tencent.com/document/product/1047/33996).
>? To respect the copyright of emoji design, the downloaded Demo project does not contain sliced images of major emoji elements. You can use your local emoji packs to configure the code. Unauthorized use of the emoji packs in the IM Demo may infringe on design copyrights.
2. Open the project in the terminal directory and find the `GenerateTestUserSig` file.
 <table>
     <tr>
         <th nowrap="nowrap">Platform</th>  
         <th nowrap="nowrap">Relative Path to File</th>  
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
      <td>Mini Program</td>   
      <td>WXMini/dist/wx/debug/GenerateTestUserSig.js</td>   
     </tr>  
</table>
3. Set relevant parameters in the `GenerateTestUserSig` file:
 >? In this document, an Android project is opened by using Android Studio as an example.
  >
 - SDKAPPID: set it to the actual SDKAppID obtained in [Step 1](#step1).
 - SECRETKEY: enter the actual key information obtained in [step 2](#step2).
 


>! In this document, the method to obtain UserSig is to configure a SECRETKEY in the client code. In this method, the SECRETKEY is vulnerable to decompilation and reverse engineering. Once your SECRETKEY is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running a demo project and feature debugging**.
> The correct `UserSig` distribution method is to integrate the computing code of `UserSig` into your server and provide an app-oriented API. When `UserSig` is needed, your app can send a request to the business server to obtain the dynamic `UserSig`. For more information, see [How to Generate UserSig on the Server](https://intl.cloud.tencent.com/document/product/1047/34385).

## Step 4: Compile and Run the Demo
Use the IDE on each end to compile and run the demo. For more information, see the `README.md` file in the corresponding directory of the demo project cloned in [Step 3](#step3).

**The compilation and running of the iOS and Mac Demo require the integration of pods. The detailed steps are as follows:**
1. Run the following command on the terminal to check the pod version:
```
pod --version
```
If the system indicates that no pod exists or that the pod version is earlier than 1.7.5, run the following command to install the latest pod.
```
// Change gem sources.
gem sources --remove https://rubygems.org/
gem sources --add https://gems.ruby-china.com/
// Install pods.
sudo gem install cocoapods -n /usr/local/bin
// If multiple Xcodes are installed, run the following command to choose an Xcode version (usually the latest Xcode version should be chosen):
sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer
// Update the local pod library.
pod setup
```
2. Run the following commands on the terminal to install dependent libraries:
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
3. Compile and run the demo:
 - iOS: go to the iOS/TUIKitDemo folder and open `TUIKitDemo.xcworkspace` to compile and run the demo.
 - Mac: go to the Mac/TUIKitDemo folder, and open `TUIKitDemo.xcworkspace` to compile and run the demo.


## Enabling Advanced Features
- [Enabling Video Calls](https://intl.cloud.tencent.com/document/product/1047/38740)
- [Enabling Group Livestreaming](https://intl.cloud.tencent.com/document/product/1047/37310)
- [Enabling Live Rooms](https://intl.cloud.tencent.com/document/product/1047/38519)

## Reference
- [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350)
