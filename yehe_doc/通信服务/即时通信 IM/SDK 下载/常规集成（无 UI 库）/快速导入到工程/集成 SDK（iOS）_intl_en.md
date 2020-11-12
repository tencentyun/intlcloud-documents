
This document describes how to quickly integrate the Tencent Cloud IM SDK (iOS) into your projects. To configure and integrate the SDK, complete the following steps.

## Development Environment Requirements
- Xcode 9.0+ has been installed
- An iPhone or iPad running iOS 8.0 or later is available.
- The project has been configured with a valid developer signature.

## Integrating the IM SDK
You can automatically integrate the IM SDK by using CocoaPods or manually download the [SDK](https://github.com/tencentyun/TIMSDK/tree/master/iOS/ImSDK) and import it to your current project.

### CocoaPods automatic loading
#### 1. Installing CocoaPods
Run the following command in the terminal window (you need to install the Ruby environment on your MacOS device in advance):
```
sudo gem install cocoapods
```

#### 2. Creating a Podfile
Navigate to the path where the project is located and run the following command. Then, a Podfile appears under the project path.
```
pod init
```

#### 3. Editing the Podfile
If you are using the standard edition of SDK, edit the Podfile as follows:

```
platform: ios, '8.0'
source 'https://github.com/CocoaPods/Specs.git'

target 'App' do
pod 'TXIMSDK_iOS'
end
```

If you are using the lite edition of SDK, edit the Podfile as follows:
```
platform: ios, '8.0'
source 'https://github.com/CocoaPods/Specs.git'

target 'App' do
pod 'TXIMSDK_Smart_iOS'
end
```

#### 4. Updating and installing the SDK
Run the following command in the terminal window to update the local library file and install TXIMSDK:
```
pod install
```
Alternatively, run the following command to update the local library version:
```
pod update
```

After the pod command is executed, a project file integrated with the SDK and suffixed .xcworkspace appears. Double-click the project file to open it.
>? If the pod search fails, we recommend that you update the local repo cache of the pod by running the following commands:
>```
> pod setup
> pod repo update
> rm ~/Library/Caches/CocoaPods/search_index.json
>```

### Manual integration
#### 1. Downloading the SDK
Download the latest version of the [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/iOS/ImSDK) from GitHub.

- IMSDK.framework and ImSDK_Smart.framework are the core dynamic library files of the IM SDK.
<table>
<thead>
<tr>
<th>Package Name</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>ImSDK.framework</td>
<td>Standard-edition IM feature pack</td>
</tr>
<tr>
<td>ImSDK_Smart.framework</td>
<td>Lite-edition IM feature pack</td>
</tr>
</tbody></table>
- TXLiteAVSDK_UGC.framework is the Tencent Cloud UGSV SDK that implements short-video sending and receiving in IM. It is an optional component.
<table>
<thead>
<tr>
<th>Package Name</th>
<th>Description</th>
<th>Feature</th>
</tr>
</thead>
<tbody><tr>
<td>TXLiteAVSDK_UGC.framework</td>
<td>Extension pack for recording and editing short videos</td>
<td>This pack provides the short-video recording and editing features. For more information, see <a href="https://cloud.tencent.com/product/ugsv">UGSV SDK Documentation</a></td>
</tr>
</tbody></table>

#### 2. Creating a project
**Create a new project.**
![](https://main.qcloudimg.com/raw/de4a148165dbfafd1f403e88018b0012.jpg)
**Enter a project name, for example, IMDemo.**
![](https://main.qcloudimg.com/raw/d9aebb74fe2fb4740c88e7cbda31987a.jpg)

#### 3. Integrating the IM SDK

**Add the dependent library**: select **Target** for IMDemo. On the **General** panel, add the dependent library under **Embedded Binaries** and **Linked Frameworks and Libraries**. If you are using the standard edition of SDK, select ImSDK.framework. If you are using the lite edition of SDK, select ImSDK_Smart.framework.
![](https://main.qcloudimg.com/raw/3a1cc30c280362be2d99058dde347d4f.png)
**Configure link parameters: Choose **Build Setting** > **Other Linker Flags** and add `-ObjC`.

## Referencing the IM SDK
You can use the SDK in project code in two ways:

#### Method 1
Choose **Xcode** > **Build Setting** > **Header Search Paths** and specify the SDK header file path. In files that require the SDK API, reference the corresponding header file.

- If you are using the standard edition of SDK, reference the header file as follows:
```
#import "ImSDK.h"
```
- If you are using the lite edition of SDK, reference the header file as follows:
```
#import "ImSDK_Smart.h"
```

#### Method 2

In files that require the SDK API, reference the corresponding header file.
- If are you using the standard edition of SDK, reference the header file as follows:
```
#import <ImSDK/ImSDK.h>
```
- If you are using the lite edition of SDK, reference the header file as follows:
```
#import <ImSDK_Smart/ImSDK_Smart.h>
```
