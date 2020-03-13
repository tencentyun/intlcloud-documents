
This document describes how to quickly integrate the Tencent Cloud IM SDK (iOS) into your projects. To configure and integrate the SDK, follow these steps.

## Development Environment Requirements
- Xcode 9.0+.
- iPhone or iPad running iOS 8.0 or later.
- The project has been configured with a valid developer signature.

## Integrating the IM SDK
You can either automatically integrate the IM SKD by using CocoaPods, or manually [download](https://github.com/tencentyun/TIMSDK) the SDK and import it to your current project.

### Automatically loading CocoaPods
#### 1. Install CocoaPods
Run the following command in a terminal window (you need to install the Ruby environment on your Mac device in advance):
```
sudo gem install cocoapods
```

#### 2. Create a Podfile
Navigate to the path where the project is located and run the following command. Then, a Podfile will appear under the project path.
```
pod init
```

#### 3. Edit the Podfile
Edit the Podfile as follows:

```
platform :ios, '8.0'
source 'https://github.com/CocoaPods/Specs.git'

target 'App' do
pod 'TXIMSDK_iOS'
end
```

#### 4. Update and install the SDK
Run the following command in a terminal window to update the local library file and install TXIMSDK:
```
pod install
```
Alternatively, run the following command to update the local library version:
```
pod update
```

After the pod command is executed, a project file integrated with the SDK and suffixed .xcworkspace will be generated. Double-click the file to open it.
>If the pod search fails, we recommend that you try to update the pod's local repo cache. The update command is as follows:
>```
pod setup
pod repo update
rm ~/Library/Caches/CocoaPods/search_index.json
```

### Manual integration
#### 1. Obtain the SDK download URL from [Github](https://github.com/tencentyun/TIMSDK):


- IMSDK.framework is the core dynamic library file of the IM SDK.

| Package Name | Description | 
| --- | --- |
| ImSDK.framework | IM feature pack |

- TXLiteAVSDK_UGC.framework is the Tencent Cloud UGSV SDK that is used to implement short-video sending and receiving in IM. It is an optional component.

| Pack Name | Description | Features |
| --- | --- | --- |
| TXLiteAVSDK_UGC.framework | Extension pack for recording and editing short videos | This pack provides the short-video recording and editing features.  |

#### 2. Create a project
**Create a new project**:
![](https://main.qcloudimg.com/raw/de4a148165dbfafd1f403e88018b0012.jpg)
**Enter a project name** (for example, IMDemo):
![](https://main.qcloudimg.com/raw/d9aebb74fe2fb4740c88e7cbda31987a.jpg)

#### 3. Integrate the IM SDK

**Add the dependent library:** select the **Target** of IMDemo. On the **General** panel, add the dependent library under **Embedded Binaries** and **Linked Frameworks and Libraries**.

![](https://main.qcloudimg.com/raw/3a1cc30c280362be2d99058dde347d4f.png)

**Add the dependent library:**
```
ImSDK.framework
```
>You need to add `-ObjC` in **Build Setting** > **Other Linker Flags**.

## Referencing the IM SDK
You can use the SDK in project code in two ways:
- Method 1: navigate to **Xcode** > **Build Setting** > **Header Search Paths**, and set the ImSDK.framework/Headers path. In files that require the SDK API, directly reference the header file "ImSDK.h":
```
#import "ImSDK.h"
```

- Method 2: in files that require the SDK API, import the header file <ImSDK/ImSDK.h>:
```
#import <ImSDK/ImSDK.h>
```
