## Prerequisites

### Environment requirements

- Xcode 11 or later (download from App Store or [here](https://developer.apple.com/xcode/resources/)).
- Recommended runtime environment:
  - Device requirements: iPhone 5 or later. iPhone 6 and older models support up to 720p for front camera.
  - System requirements: iOS 10.0 or later.

### Importing the SDK

You can use CocoaPods or download and import the SDK manually into your project.
<dx-tabs>
::: CocoaPods
1. **Install CocoaPods**
Enter the following command in a terminal window (you need to install Ruby on your Mac first):
```
sudo gem install cocoapods
```
2. **Create a Podfile**
Go to the directory of your project and enter the following command to create a Podfile in the directory.
```
pod init
```
3. **Edit the Podfile**
Choose an edition for your project and edit the Podfile:
  - **XMagic Standard**
Edit the Podfile as follows:
```
platform :ios, '8.0'

target 'App' do
pod 'XMagic'
end
```
  - **XMagic Lite**
The installation package of XMagic Lite is smaller than XMagic Standard. It supports only Basic A1- 00, Basic A1 - 01, and Advanced S1 - 00. Edit the Podfile as follows:
```
platform :ios, '8.0'

target 'App' do
pod 'XMagic_Smart'
end
```
4. **Update the local repository and install the SDK**
Enter the following command in a terminal window to update the local repository and install the SDK:
```
pod install
```
An XCWORKSPACE project file integrated with the SDK will be generated. Double-click to open it.
5. **Add effect resources to your project**
Download the [SDK and effect resources](https://www.tencentcloud.com/document/product/1143/45377) for the Tencent Effect package you use, decompress the file, and add **all the bundle files** except **LightCore.bundle**, **Light3DPlugin.bundle**, **LightBodyPlugin.bundle**, **LightHandPlugin.bundle**, and **LightSegmentPlugin.bundle** to your project.
6. Change the bundle ID to the bundle ID bound to your license.
:::
::: Manual import
1. Download the [SDK and effect resources](https://www.tencentcloud.com/document/product/1143/45377) and decompress the file. The SDK is in the `frameworks` folder, and the bundle resources are in `resources`.
2. Open your Xcode project and add the frameworks in the `frameworks` folder to your project: Choose the target to run, select the **General** tab, expand **Frameworks, Libraries, and Embedded Content**, and click **+** to add the frameworks downloaded, including `XMagic.framework`, `YTCommonXMagic.framework`, and `libpag.framework`, as well as `MetalPerformanceShaders.framework`, `CoreTelephony.framework`, `JavaScriptCore.framework`, `VideoToolbox.framework`, and `libc++.tbd`. You can also add `Masonry.framework` (control layout) and `SSZipArchive` (file decompression) if necessary.
![](https://qcloudimg.tencent-cloud.cn/raw/64aacf4305d7adf3a2bbe025920be517.png)
3. Add the effect resources in the `resources` folder to your project.
4. Change the bundle ID to the bundle ID bound to your license.
:::
::: Dynamic download and integration
To reduce the SDK package size, you can dynamically download the necessary module resources and animated effect resources (`MotionRes`, not available in some basic editions of the SDK) from a URL and, after download, pass the path of the resources to the SDK.

You can use your existing download service, but we recommend you use the download logic of the demo. For detailed directions on implementing dynamic download, see [Reducing SDK Size](https://www.tencentcloud.com/document/product/1143/48644).
:::
</dx-tabs>

### Configuring permissions
Add permission descriptions in the `Info.plist` file. If you don’t do so, the application will crash on iOS 10. Grant the application camera access in **Privacy - Camera Usage Description**.

## Directions

### Step 1. Authenticate
1. Apply for a license and get the `LicenseURL` and `LicenseKEY`.
>! Under normal circumstances, the authentication process can be completed by connecting your application to the internet one time, so you **don't need** to put the license file in the project directory. However, if your application needs to use the SDK features without ever connecting to the internet, you can download the license file and put it in the project directory. In this case, the license file must be named `v_cube.license`.
2. Set the URL and key in the initialization code of a business module to download the license. Avoid downloading it just before use. You can also trigger the download in the `didFinishLaunchingWithOptions` method of `AppDelegate` (the values of `LicenseURL` and `LicenseKey` are generated when you bound the license in the console).
```
[TELicenseCheck setTELicense:LicenseURL key:LicenseKey completion:^(NSInteger authresult, NSString * _Nonnull errorMsg) {
	if (authresult == TELicenseCheckOk) {
		NSLog(@"Authentication successful");
	} else {
		NSLog(@"Authentication failed");
	}
}];
```
**Authentication error codes:**
<table>
<thead>
<tr>
<th>Error Code</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td>Successful</td>
</tr>
<tr>
<td>-1</td>
<td>The input parameter is invalid; for example, the `URL` or `KEY` is empty.</td>
</tr><tr>
<td>-3</td>
<td>Download failed. Check the network settings.</td>
</tr><tr>
<td>-4</td>
<td>Unable to obtain any Tencent Effect authentication information from the local system, which may be caused by an I/O failure.</td>
</tr><tr>
<td>-5</td>
<td>The VCUBE TEMP license file is empty, which may be caused by an I/O failure.</td>
</tr><tr>
<td>-6</td>
<td>The JSON field in the `v_cube.license` file is incorrect. Please contact Tencent Cloud team for help.</td>
</tr><tr>
<td>-7</td>
<td>Signature verification failed. Please contact Tencent Cloud team for help.</td>
</tr><tr>
<td>-8</td>
<td>Decryption failed. Please contact Tencent Cloud team for help.</td>
</tr><tr>
<td>-9</td>
<td>The JSON field in `TELicense` is incorrect. Please contact Tencent Cloud team for help.</td>
</tr><tr>
<td>-10</td>
<td>The Tencent Effect authentication information parsed online is empty. Please contact Tencent Cloud team for help.</td>
</tr><tr>
<td>-11</td>
<td>Failed to write Tencent Effect SDK authentication information to the local file, which may be caused by an I/O failure.</td>
</tr><tr>
<td>-12</td>
<td>Download failed, and failed to parse local assets.</td>
</tr><tr>
<td>-13</td>
<td>Authentication failed.</td>
</tr><tr>
<td>Others</td>
<td>Please contact Tencent Cloud team for help.</td>
</tr>
</tbody></table>

[](id:step3)
### Step 2. Load the SDK (`XMagic.framework`)
The following is the process of using the Tencent Effect SDK:
1. Load effect resources.
```
NSDictionary *assetsDict = @{@"core_name":@"LightCore.bundle",
	@"root_path":[[NSBundle mainBundle] bundlePath]
};
```
2. Initialize the Tencent Effect SDK.
```
initWithRenderSize:assetsDict: (XMagic)
self.beautyKit = [[XMagic alloc] initWithRenderSize:previewSize assetsDict:assetsDict];
```
3. The SDK processes each frame of data and returns the results.
```
process: (XMagic)
```
```
// Pass in frame data via the camera callback
- (void)captureOutput:(AVCaptureOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection;

// Get the raw data and process the rendering information for each frame
- (void)mycaptureOutput:(AVCaptureOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)inputSampleBuffer fromConnection:(AVCaptureConnection *)connection originImageProcess:(BOOL)originImageProcess;

// Use the CPU to process the data
- (YTProcessOutput*)processDataWithCpuFuc:(CMSampleBufferRef)inputSampleBuffer;

// Use the GPU to process the data
- (YTProcessOutput*)processDataWithGpuFuc:(CMSampleBufferRef)inputSampleBuffer;

// The data processing API of the Tencent Effect SDK
/// @param input: Input the data to be processed
/// @return: Output the processed data
- (YTProcessOutput* _Nonnull)process:(YTProcessInput * _Nonnull)input;
```
4. Release the Tencent Effect SDK.
```
deinit (XMagic)
// Call this API when you need to release the resources of the SDK
[self.beautyKit deinit]
```

> ?After completing the above steps, you can control the display timing and other device environment parameters as needed.

## FAQs

[](id:que1)
### Question 1. What should I do in case of the compilation error "unexpected service error: build aborted due to an internal error: unable to write manifest to-xxxx-manifest.xcbuild': mkdir(/data, S_IRWXU | S_IRWXG | S_IRWXO): Read-only file system (30):"?

1. Go to **File** > **Project settings** > **Build System** and select **Legacy Build System**.
2. For Xcode 13.0++, you need to select **File** > **Workspace Settings** > **Do not show a diagnostic issue about build system deprecation**.

[](id:que2)
### Question 2. What should I do if the error "Xcode 12.X compilation: Building for iOS Simulator, but the linked and embedded framework '.framework'..." occurs when I compile my iOS project after importing the resources?

Go to **Build Settings** > **Build Options**, change **Validate Workspace** to **Yes**, and click **Run**.
>? If you change **Validate Workspace** back to **No** after compilation, you can still run your project successfully.

[](id:que3)
### Question 3. What should I do if the filter settings don't take effect?
Check the value you set (value range: 0-100). The effect may not be obvious if the value is too small.

[](id:que4)
### Question 4. What should I do if a `dSYM` generation error occurs when I compile the iOS demo project?
```
PhaseScriptExecution CMake\ PostBuild\ Rules build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh
    cd /Users/zhenli/Downloads/xmagic_s106
    /bin/sh -c /Users/zhenli/Downloads/xmagic_s106/build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh

Command /bin/sh failed with exit code 1
```
- Cause: Failed to sign `libpag.framework` and `Masonary.framework` again.
- Solution:
  1. Open `demo/copy_framework.sh`.
  2. Use the following command to check the absolute path of the local `cmake`. Replace `$(which cmake)` with the absolute path of `cmake`.
```
which cmake
```
  3. Replace all `Apple Development: ......` with your own signature.
