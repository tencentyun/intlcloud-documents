## Preparations for Integration

### Developer environment requirements

- Xcode 11 or higher: download on App Store or [here](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/iOS/2.4.1.18/demo.zip).
- Recommended runtime environment:
  - Device requirements: iPhone 5 or later. iPhone 6 and older models support up to 720p for front camera.
  - System requirements: iOS 10.0 or higher.

### C/C++ layer development environment

Xcode uses the C++ environment by default.

<table>
<tr><th>Type</th><th>Dependent Library</th></tr>
<tr>
<td>System dependent library</td>
<td><ul style="margin:0">
<li/>AVFoundation
<li/>Accelerate
<li/>AssetsLibrary
<li/>CoreML
<li/>JavaScriptCore
<li/>CoreFoundation
<li/>MetalPerformanceShaders
<li/>CoreTelephony
<li/>libc++.tbd
</ul></td>
</tr>
<tr>
<td>Built-in library</td>
<td><ul style="margin:0">
<li/>YTCommon (static authentication library)
<li/>XMagic (static beauty filter library)
<li/>libpag (dynamic video decoding library)
</ul></td>
</tr>
</table>

## Resource Import
### Resources
- Required resource package: `LightCore.bundle`
- Keying feature package: `LightSegmentPlugin.bundle`
- Gesture feature package: `LightHandPlugin.bundle`
- 3D feature package: `Light3DPlugin.bundle`

### Method to import
- **Method 1**: add the resources as project resources.
- **Method 2**: if you need to specify the path `initWithRenderSize:assetsDict: (XMagic)`, you can configure each resource path through `assetsDict`.

### Permission configuration
Add permission descriptions in the `Info.plist` file; otherwise, the app will crash on iOS 10. Grant the camera access in **Privacy - Camera Usage Description** to allow the app to use the camera.

## Integration Steps

[](id:step1)
### Step 1. Prepare the signature
For the framework signature, select **General** and set **Masonry.framework** and **libpag.framework** to **Embed & Sign**.
[](id:step2)
### Step 2. Authenticate
1. Apply for a license and get the `LicenseURL` and `LicenseKEY` as instructed in [License Guide](https://intl.cloud.tencent.com/document/product/1143/45380).
> ! Under normal circumstances, as long as the app is successfully connected to the internet once, the authentication process can be completed, so you **don't need** to put the license file in the project directory. However, if your app needs to use the SDK features when it is never connected to the internet, you can download the license file and put it in the project directory. In this case, the license file must be named `v_cube.license`.
2. Set the `URL` and `KEY` in the initialization code of the relevant business module to trigger the license download. Avoid downloading it just before use. You can also trigger the download in the `didFinishLaunchingWithOptions` method of the `AppDelegate`. Here, `LicenseURL` and `LicenseKey` are the information generated in the console when the license is bound.
```
[TELicenseCheck setTELicense:LicenseURL key:LicenseKey completion:^(NSInteger authresult, NSString * _Nonnull errorMsg) {
       if (authresult == TELicenseCheckOk) {
            NSLog(@"Authentication succeeded");
        } else {
            NSLog(@"Authentication failed");
        }
    }];
```
**Authentication `errorCode` description:**
<table>
<thead>
<tr>
<th>Error Code</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td>Success.</td>
</tr>
<tr>
<td>-1</td>
<td>The input parameter is invalid; for example, the `URL` or `KEY` is empty.</td>
</tr><tr>
<td>-3</td>
<td>Download failed. Check the network settings.</td>
</tr><tr>
<td>-4</td>
<td>The Tencent Effect SDK authorization information read from the local system is empty, which may be caused by an I/O failure.</td>
</tr><tr>
<td>-5</td>
<td>The content of read VCUBE TEMP license file is empty, which may be caused by an I/O failure.</td>
</tr><tr>
<td>-6</td>
<td>The JSON field in the `v_cube.license` file is incorrect. Contact Tencent Cloud for assistance.</td>
</tr><tr>
<td>-7</td>
<td>Signature verification failed. Contact Tencent Cloud for assistance.</td>
</tr><tr>
<td>-8</td>
<td>Decryption failed. Contact Tencent Cloud for assistance.</td>
</tr><tr>
<td>-9</td>
<td>The JSON field in the `TELicense` field is incorrect. Contact Tencent Cloud for assistance.</td>
</tr><tr>
<td>-10</td>
<td>The Tencent Effect SDK authorization information parsed online is empty. Contact Tencent Cloud for assistance.</td>
</tr><tr>
<td>-11</td>
<td>Failed to write the Tencent Effect SDK authorization information to the local file, which may be caused by an I/O failure.</td>
</tr><tr>
<td>-12</td>
<td>Failed to download and failed to parse local assets.</td>
</tr><tr>
<td>-13</td>
<td>Authentication failed.</td>
</tr><tr>
<td>Others</td>
<td>Contact Tencent Cloud for assistance.</td>
</tr>
</tbody></table>

[](id:step3)
### Step 3. Load the SDK (XMagic.framework)
The following is the lifecycle of using Tencent Effect SDK:
1. Load beauty filter resources.
```
NSDictionary *assetsDict = @{@"core_name":@"LightCore.bundle",
	@"root_path":[[NSBundle mainBundle] bundlePath]
};
```
2. Initialize Tencent Effect SDK.
```
initWithRenderSize:assetsDict: (XMagic)
self.beautyKit = [[XMagic alloc] initWithRenderSize:previewSize assetsDict:assetsDict];
```
3. Tencent Effect SDK processes each frame of data and returns the processing results.
```
process: (XMagic)
```
```
// Pass in frame data at the camera callback
- (void)captureOutput:(AVCaptureOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection;

// Get the raw data and process the rendering information for each frame
- (void)mycaptureOutput:(AVCaptureOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)inputSampleBuffer fromConnection:(AVCaptureConnection *)connection originImageProcess:(BOOL)originImageProcess;

// Use the CPU to process the data
- (YTProcessOutput*)processDataWithCpuFuc:(CMSampleBufferRef)inputSampleBuffer;

// Use the GPU to process the data
- (YTProcessOutput*)processDataWithGpuFuc:(CMSampleBufferRef)inputSampleBuffer;

// Data processing API of Tencent Effect SDK
/// @param input: input the data to be processed
/// @return: output the processed data
- (YTProcessOutput* _Nonnull)process:(YTProcessInput * _Nonnull)input;
```
4. Release Tencent Effect SDK.
```
deinit (XMagic)
// Make a call where SDK resources need to be released
[self.beautyKit deinit]
```

> ?After completing the above steps, you can control the display timing and other device environment parameters as needed.

## FAQs

[](id:que1)
### Question 1. What should I do in case of the compilation error "unexpected service error: build aborted due to an internal error: unable to write manifest to-xxxx-manifest.xcbuild': mkdir(/data, S_IRWXU | S_IRWXG | S_IRWXO): Read-only file system (30):"?

1. Go to **File** > **Project settings** > **Build System** and select **Legacy Build System**.
2. For Xcode 13.0++, you need to select **File** > **Workspace Settings** > **Do not show a diagnostic issue about build system deprecation**.

[](id:que2)
### Question 2. What should I do if "Building for iOS Simulator, but the linked and embedded framework '.framework'..." is reported during compilation by Xcode 12.X after resources are imported on iOS?

Go to **Build Settings** > **Build Options**, change **Validate Workspace** to **Yes**, and click **Run**.
> ?  Note that the execution will also be normal if you change **Validate Workspace** from **Yes** to **No** after the compilation is completed.

[](id:que3)
### Question 3. What should I do if the filter settings don't take effect?
Check whether the value is set properly (value range: 0–100). You may have set too small a value so the effect is not obvious.

[](id:que4)
### Question 4. What should I do if an error is reported when `dSYM` is generated during demo compilation on iOS?
```
PhaseScriptExecution CMake\ PostBuild\ Rules build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh
    cd /Users/zhenli/Downloads/xmagic_s106
    /bin/sh -c /Users/zhenli/Downloads/xmagic_s106/build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh

Command /bin/sh failed with exit code 1
```
- Cause: failed to sign `libpag.framework` and `Masonary.framework` again.
- Solution:
	1. Open `demo/copy_framework.sh`.
	2. Use the following command to check the absolute path of the local `cmake` and replace `$(which cmake)` with it.
```
which cmake
```
3. Replace all `Apple Development: ......` with your own signature.
