
This document describes how to quickly integrate the Tencent Cloud IM SDK (iOS) to your projects. To configure and integrate the SDK, follow these steps.

## Production Environment Requirements
- Xcode 9.0+.
- iPhone or iPad on iOS 8.0 or above.
- Your project has a valid developer signature.

## Integrating the IM SDK
You can either automatically integrate the IM SDK using CocoaPods, or manually download the [SDK](https://github.com/tencentyun/TIMSDK/tree/master/iOS/ImSDK) and import it to your current project.

### Automatic loading using CocoaPods
#### 1. Install CocoaPods
Enter the following command in the terminal window (you need to install the Ruby environment on your macOS in advance):
```
sudo gem install cocoapods
```

#### 2. Create a Podfile
Go to the path where the project is located and run the following command. Then, a Podfile will appear under the project path.
```
pod init
```

#### 3. Edit the Podfile
If you are using the SDK standard edition, edit the Podfile as follows:

```
platform :ios, '8.0'
source 'https://github.com/CocoaPods/Specs.git'

target 'App' do
pod 'TXIMSDK_iOS'
end
```

If you are using the SDK lite edition, edit the Podfile as follows:
```
platform :ios, '8.0'
source 'https://github.com/CocoaPods/Specs.git'

target 'App' do
pod 'TXIMSDK_Smart_iOS'
end
```

If you are using the SDK bitcode lite edition, edit the Podfile as follows:
```
platform :ios, '8.0'
source 'https://github.com/CocoaPods/Specs.git'

target 'App' do
pod 'TXIMSDK_Smart_iOS_Bitcode'
end
```

If you are using the SDK XCFramework lite edition, edit the Podfile as follows:
```
platform :ios, '8.0'
source 'https://github.com/CocoaPods/Specs.git'

target 'App' do
pod 'TXIMSDK_Smart_iOS_XCFramework'
end
```

If you are using the SDK XCFramework lite edition (bitcode supported), edit the Podfile as follows:
```
platform :ios, '8.0'
source 'https://github.com/CocoaPods/Specs.git'

target 'App' do
pod 'TXIMSDK_Smart_iOS_Bitcode_XCFramework'
end
```

#### 4. Update and install the SDK
Run the following command in the terminal window to update the local library file and install the TXIMSDK:
```
pod install
```
Or, run the following command to update the local repository:
```
pod update
```

After the pod command is executed, an .xcworkspace project file integrated with the SDK will be generated. Double-click this file to open it.
>?If the pod search fails, you are advised to update the local repo cache of the pod by running the following commands:
>```
>pod setup
>pod repo update
>rm ~/Library/Caches/CocoaPods/search_index.json
>```


### Manual integration
#### 1. Download the SDK
Download the latest SDK version from [GitHub](https://github.com/tencentyun/TIMSDK/tree/master/iOS/ImSDK):

- `ImSDK.framework` and `ImSDK_Smart.framework` are the core dynamic library files of the IM SDK.
<table>
<thead>
<tr>
<th>Package Name</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>ImSDK.framework</td>
<td>IM SDK standard edition</td>
</tr>
<tr>
<td>ImSDK_Smart.framework</td>
<td>IM SDK lite edition</td>
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
<td>Extension package for recording and editing short videos</td>
<td>This package provides short video recording and editing features. For more information, see <a href="https://intl.cloud.tencent.com/zh/product/ugsv">UGSV SDK Documentation</a>.</td>
</tr>
</tbody></table>

#### 2. Create a project
**Create a project.**
![](https://main.qcloudimg.com/raw/de4a148165dbfafd1f403e88018b0012.jpg)
**Enter a project name, for example, IMDemo.**
![](https://main.qcloudimg.com/raw/d9aebb74fe2fb4740c88e7cbda31987a.jpg)

#### 3. Integrate the IM SDK

**Add the dependency library**: select **Target** for IMDemo. On the **General** panel, add the dependency library under **Embedded Binaries** and **Linked Frameworks and Libraries**. If you use the SDK standard edition, select **ImSDK.framework**. If you use the SDK lite edition, select **ImSDK_Smart.framework**.
![](https://main.qcloudimg.com/raw/3a1cc30c280362be2d99058dde347d4f.png)
**Set link parameters: add `-ObjC` in **Build Setting** -> **Other Linker Flags**.
>?For manual integration, you need to change `ImSDK.framework` to `Embed&Sing` in **Target** -> **General** -> **Frameworks** -> **Libraries and Embedded Content**.
## Referencing the IM SDK
There are two ways to use the SDK in your project code.

#### Method 1
Choose **Xcode** -> **Build Setting** -> **Header Search Paths**, and set the SDK header file path. In files that require the SDK API, reference the corresponding header file.

- If you use the SDK Standard Edition, reference the header file as follows:
```
#import "ImSDK.h"
```
- If you use the SDK Lite Edition, reference the header file as follows:
```
#import "ImSDK_Smart.h"
```

#### Method 2

Use the following codes to import specific header files into the project's files that need to use the SDK APIs.
- If you use the SDK Standard Edition, reference the header file as follows:
```
#import <ImSDK/ImSDK.h>
```
- If you use the SDK Lite Edition, reference the header file as follows:
```
#import <ImSDK_Smart/ImSDK_Smart.h>
```
