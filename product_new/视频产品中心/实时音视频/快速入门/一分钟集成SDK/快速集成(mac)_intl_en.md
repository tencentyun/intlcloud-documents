This document describes how to quickly integrate the Tencent Cloud TRTC SDK for macOS into your project in the following steps.


## Development Environment Requirements
- Xcode 9.0+.
- A Mac on macOS X10.10+.
- Your project has a valid developer signature.

## Integrating the TRTC SDK
You can choose to use CocoaPods for automatic loading or manually download the SDK first and then import it into your current project.

### CocoaPods
#### 1. Install CocoaPods
Enter the following command in the terminal window (you need to install the Ruby environment on your macOS in advance):
```
sudo gem install cocoapods
```

#### 2. Create a Podfile
Go to the path to the project, enter the following command, and a Podfile will appear in the project path.
```
pod init
```

#### 3. Edit the Podfile
There are two ways to edit the Podfile:
- Method 1: use the pod path of the Tencent Cloud LiteAV SDK.

```
	platform :osx, '10.10'

	target 'Your Target' do
	pod 'TXLiteAVSDK_TRTC_Mac', :podspec => 'http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_TRTC_Mac.podspec'
	end
```

- Method 2: use the official source of CocoaPod, which supports choosing the version number.

```
	platform :osx, '10.10'
	source 'https://github.com/CocoaPods/Specs.git'

	target 'Your Target' do
	pod 'TXLiteAVSDK_TRTC_Mac'
	end
```

#### 4. Install and update the SDK
Enter the following command in the terminal window to install the TRTC SDK:
```
pod install
```
Or, run the following command to update the local library:
```
pod update
```

After the pod command is executed, a project file with the .xcworkspace extension integrated with the SDK will be generated. Double-click it to open it.

### Manual integration
1. Download the macOS version of the [TRTC-SDK](https://github.com/tencentyun/TRTCSDK/tree/master/Mac).

2. Open your Xcode project and import the framework downloaded in the first step into it.

3. Select the target you want to run and check "Build Phases".
![](https://main.qcloudimg.com/raw/b5097f8ac4cbaa5044d92b2a96ea2b9e.jpg)

4. Click **Link Binary with Libraries** to expand it and then click the "+" icon at the bottom to add the dependent library.
![](https://main.qcloudimg.com/raw/17046154417930f9d31b6452782df55d.jpg)

5. Add the downloaded SDK Framework and its required dependent library in sequence.
    - `AudioUnit.framework` 
    - `libc++.tbd`
    
 Successful addition is as shown below:
![](https://main.qcloudimg.com/raw/7bddb832347a971f3e69238480fa3e8d.jpg)

## Granting Camera and Mic Access
To use the audio/video features of the SDK, you need to grant the mic and camera access. Add the following two items to the application's `Info.plist` which correspond to the prompt messages of the mic and camera respectively when the authorization dialog box pops up.
- **Privacy - Microphone Usage Description**; enter the prompt for mic usage purpose.
- **Privacy - Camera Usage Description**; enter the prompt for camera usage purpose.
See the figure below:
![](https://main.qcloudimg.com/raw/be76bd6f3f22d31385d871710b51b771.jpg) 


## Importing the TRTC SDK
There are two ways to use the SDK in your project code:
- Method 1: add an import module to the project's files that need to use an SDK API.
```
@import TXLiteAVSDK_TRTC_Mac;
```

- Method 2: import specific header files into the project's files that need to use an SDK API.
```
#import TXLiteAVSDK_TRTC_Mac/TRTCCloud.h
```


