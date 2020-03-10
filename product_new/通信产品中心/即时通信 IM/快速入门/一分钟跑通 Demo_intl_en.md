This document describes how to quickly run through the IM experience demo.

<span id="step1"></span>
## Step 1: Create an App
1. Log in to [IM Console] (https://console.cloud.tencent.com/im).
 > If you already have an app, record its SDKAppID and [obtain key information](#step2).
 >
2. Click **+Add App**.
3. In the **Create App** dialog box, enter a name for the app and click **OK**.
  After the app is created, you can view the status, service version, SDKAppID, creation time, and expiry time of the newly created app on the overview page of the console. Then, record the SDKAppID.
  ![](https://main.qcloudimg.com/raw/2753962b67754a9ebb2a2a5b8042f2ef.png)
  

<span id="step2"></span>
## Step 2: Obtain Key Information

1. Click the target app card to enter its basic configuration page.
2. In the **Basic Information** section, click **Display Key**. Then, copy and save the key information.
 > Keep the key information properly against disclosure.

<span id="step3"></span>
## Step 3: Download and Configure the Source Code of the Demo

1. Download the IM Demo project. For the specific download address, see [Downloading the SDK](https://cloud.tencent.com/document/product/269/36887).
2. Open the project in the corresponding directory on the platform and find the `GenerateTestUserSig` file.
 <table>
     <tr>
         <th nowrap="nowrap">Platform</th>  
         <th nowrap="nowrap">Relative File Path</th>  
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
3. Set relevant parameters in the `GenerateTestUserSig` file.
 > Here, we use Android Studio to open an Android project.
  >
 - SDKAPPID: set it to the actual SDKAppID obtained in [Step 1](#step1).
 - SECRETKEY: set it to the actual key information obtained in [Step 2](#step2). 
 ![](https://main.qcloudimg.com/raw/e7f6270bcbc68c51595371bd48c40af7.png)


> Here, a SECRETKEY is configured in the client code to obtain UserSig. The SECRETKEY is easy to decompile and reversely crack. If the SECRETKEY is leaked, hackers can steal your Tencent Cloud traffic. Therefore, **this method is used only to locally run through a demo project and commission features.**
> The correct way to issue UserSig is to integrate the UserSig computing code into your server and provide app-oriented APIs. When UserSig is needed, your app will send requests to the business server to obtain a dynamic UserSig. For details, see [Generating UserSig on the Server End](https://cloud.tencent.com/document/product/269/32688#GeneratingdynamicUserSig).

## Step 4: Compile and Run the Project
You can compile and run the IDE on each end. For details, see the `README.md` file in the corresponding directory of the demo project cloned in [Step 3](#step3).

**The compilation and running of the iOS and Mac demos require pod integration. The detailed procedure is as follows:**
1. Run the following command on the terminal to check the pod version:
```
pod --version
```
If you are prompted that no pod exists or the pod version is earlier than version 1.7.5, run the following command to install the latest pod version:
```
// Change gem sources.
gem sources --remove https://rubygems.org/
gem sources --add https://gems.ruby-china.com/
// Install pods.
sudo gem install cocoapods -n /usr/local/bin
// If multiple versions of Xcode are installed, run the following command to choose one version (which is normally the latest Xcode version):
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
 If the installation fails, run the following commands to update the local CocoaPods repository list:
 ```bash
 pod repo update
```
3. Compile and run the project:
 - For iOS: Navigate to the iOS/TUIKitDemo folder and open `TUIKitDemo.xcworkspace` to compile and run the project.
 - For Mac: Navigate to the Mac/TUIKitDemo folder and open `TUIKitDemo.xcworkspace` to compile and run the project.



