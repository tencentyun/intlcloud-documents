This article describes how to configure, compile, and run the IM trial demo in minutes.


<span id="step1"></span>
## Step 1: Create an App
1. Log in to the [IM Console](https://console.cloud.tencent.com/im).
 > If you already have an app, take note of its SDKAppID and [skip to Step 2](#step2).
 > A Tencent Cloud account supports a maximum of 100 IM apps. If you have reached that limit, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app before creating a new one. **Once an app is deleted, all the data and services associated with the SDKAppID are removed and cannot be recovered, so proceed with caution.**
 >
2. Click **Add Application**.
3. In the **Create Application** dialog box, enter an app name and click **OK**.
    After the app is created, you can view the status, version, SDKAppID, creation time, and expiry time of the new app on the overview page of the console. Take note of the SDKAppID.
    


<span id="step2"></span>
## Step 2: Obtain Key Information

1. Click the target app card to enter the basic configuration page of the app.
2. In the **Basic Info** area, click **Display key**. Copy and save the key information.
 > Store the key information properly to prevent disclosure.

<span id="step3"></span>
## Step 3: Download and Configure the Demo Source Code

1. Download the IM Demo project. For more information about the specific download address, see [SDK Download](https://intl.cloud.tencent.com/document/product/1047/33996).
2. Open the project in the corresponding directory on the platform and find the `GenerateTestUserSig` file.
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
3. Set the relevant parameters in the `GenerateTestUserSig` file.
 > Here, we use Android Studio to open an Android project.
  >
 - SDKAPPID: set it to the actual SDKAppID obtained in [step 1](#step1).
 - SECRETKEY: enter the actual key information obtained in [step 2](#step2).



> In this article, a SECRETKEY is configured in the client code to obtain UserSig. The SECRETKEY is easily decompiled and reverse cracked. If the SECRETKEY is leaked, hackers can steal your Tencent Cloud traffic. Therefore, **this method only applies to locally run a demo project and commission features**.
> The correct `UserSig` distribution method is to integrate the computing code of `UserSig` into your server and provide an app-oriented API. When `UserSig` is required, your app sends a request to the service server to obtain the dynamic `UserSig`. For more information, see [Generating a UserSig on the Server](https://intl.cloud.tencent.com/document/product/1047/34385).

## Step 4: Compile and Run the Demo
Use the IDE on each end to compile and run the demo. For more information, see the `README.md` file in the corresponding directory of the demo project cloned in [Step 3](#step3).

**The compilation and running of the iOS and Mac demo require pod integration. The detailed procedure is as follows:**
1. Run the following command on the terminal to check the pod version:
```
pod --version
```
If the system prompts that no pod exists or the pod version is earlier than 1.7.5, run the following command to install the latest pod:
```
// Change gem sources.
gem sources --remove https://rubygems.org/
gem sources --add https://gems.ruby-china.com/
// Install pods.
sudo gem install cocoapods -n /usr/local/bin
// If multiple versions of Xcode are installed, run the following command to choose an Xcode version (usually the latest Xcode version should be chosen):
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
3. Compile and run the project:
 - iOS: enter the iOS/TUIKitDemo folder and open `TUIKitDemo.xcworkspace` to compile and run the project.
 - Mac: enter the Mac/TUIKitDemo folder and open `TUIKitDemo.xcworkspace` to compile and run the project.

## Related Documentation
- [Pricing](https://intl.cloud.tencent.com/zh/document/product/1047/34350)


