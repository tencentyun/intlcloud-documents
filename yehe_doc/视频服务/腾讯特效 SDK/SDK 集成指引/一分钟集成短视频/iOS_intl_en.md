## Preparations[](id:ready)

1. Download and unzip the [demo package](https://intl.cloud.tencent.com/document/product/1143/45374). Import the `Xmagic` module (the files in `Bundle`, `XmagicIconRes`, and `Record > View` folders) into your project.
2. Import `libpag.framework`, `Masonry.framework`, `XMagic.framework`, and `YTCommonXMagic.framework` in the `lib` directory.
3. For the framework signature, select **General** and set **Masonry.framework** and **libpag.framework** to **Embed & Sign**.
4. Set `Bundle ID` to the bundle ID bound to the trial license.

### Developer environment requirements

- Xcode 11 or later: Download on App Store or [here](https://developer.apple.com/xcode/resources/).
- Recommended runtime environment:
  - Device requirements: iPhone 5 or later. iPhone 6 and older models support up to 720p for front camera.
  - System requirements: iOS 10.0 or later.

### C/C++ layer development environment

Xcode uses the C++ environment by default.

<table>
<tr><th>Type</th><th>Dependency Library</th></tr>
<tr>
<td>System dependent library</td>
<td><ul style="margin:0">
<li/>Accelerate
<li/>AssetsLibrary
<li/>AVFoundation
<li/>CoreFoundation
<li/>CoreML
<li/>JavaScriptCore
<li/>libc++.tbd
<li/>libmtasdk.a
<li/>libresolv.tbd
<li/>libsqlite3.tbd
<li/>MetalPerformanceShaders
</ul></td>
</tr>
<tr>
<td>Built-in library</td>
<td><ul style="margin:0">
<li/>YTCommon (static authentication library)
<li/>XMagic (static beauty filter library)
<li/>libpag (dynamic video decoding library)
<li/>Masonry (control layout library)
<li/>QCloudCore (object storage library)
<li/>QCloudCosXML (object storage library)
</ul></td>
</tr>
</table>

## SDK API Integration[](id:step)

- For steps [1](#step1)–[2](#step2), see the `viewDidLoad` and `buildBeautySDK` methods of the `UGCKitRecordViewController` class in the demo project.
- For steps [4](#step4)–[7](#step7), see the instance code of the `UGCKitRecordViewController` and `BeautyView` classes in the demo project.

### Step 1. Initiate authentication[](id:step1)
Add the following code to `didFinishLaunchingWithOptions` of `AppDelegate` (set `LicenseURL` and `LicenseKey` according to the authorization information you obtain from the Tencent Cloud website):
```objectivec
[TXUGCBase setLicenceURL:LicenseURL key:LicenseKey];

[TELicenseCheck setTELicense:@"https://license.vod2.myqcloud.com/license/v2/1258289294_1/v_cube.license" key:@"3c16909893f53b9600bc63941162cea3" completion:^(NSInteger authresult, NSString * _Nonnull errorMsg) {
              if (authresult == TELicenseCheckOk) {
                   NSLog(@"Authentication successful");
               } else {
                   NSLog(@"Authentication failed");
               }
       }];
```
**Authentication `errorCode` description:**

| Error Code | Description |
| :----- | :------------------------------------------------------ |
| 0 | Succeeded. |
| -1     | The input parameter is invalid; for example, the `URL` or `KEY` is empty.                      |
| -3     | Download failed. Check the network settings.                            |
| -4     | The Tencent Effect SDK authorization information read from the local system is empty, which may be caused by an I/O failure.        |
| -5     | The content of read VCUBE TEMP license file is empty, which may be caused by an I/O failure. |
| -6     | The JSON field in the `v_cube.license` file is incorrect. Contact Tencent Cloud for assistance. |
| -7     | Signature verification failed. Contact Tencent Cloud for assistance.                      |
| -8     | Decryption failed. Contact Tencent Cloud for assistance.                          |
| -9     | The JSON field in the `TELicense` field is incorrect. Contact Tencent Cloud for assistance. |
| -10    | The Tencent Effect SDK authorization information parsed online is empty. Contact Tencent Cloud for assistance.      |
| -11    | Failed to write the Tencent Effect SDK authorization information to the local file, which may be caused by an I/O failure.      |
| -12    | Failed to download and failed to parse local assets.                         |
| -13    | Authentication failed.                                                |
| Others   | Contact Tencent Cloud for assistance.                                    |


### Step 2. Set the path of SDK materials[](id:step2)

```objectivec
CGSize previewSize = [self getPreviewSizeByResolution:self.currentPreviewResolution];
NSString *beautyConfigPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) lastObject];
beautyConfigPath = [beautyConfigPath stringByAppendingPathComponent:@"beauty_config.json"];
NSFileManager *localFileManager=[[NSFileManager alloc] init];
BOOL isDir = YES;
NSDictionary * beautyConfigJson = @{};
if ([localFileManager fileExistsAtPath:beautyConfigPath isDirectory:&isDir] && !isDir) {
	NSString *beautyConfigJsonStr = [NSString stringWithContentsOfFile:beautyConfigPath encoding:NSUTF8StringEncoding error:nil];
	NSError *jsonError;
	NSData *objectData = [beautyConfigJsonStr dataUsingEncoding:NSUTF8StringEncoding];
	beautyConfigJson = [NSJSONSerialization JSONObjectWithData:objectData
											options:NSJSONReadingMutableContainers
											error:&jsonError];
}
NSDictionary *assetsDict = @{@"core_name":@"LightCore.bundle",
							@"root_path":[[NSBundle mainBundle] bundlePath],
							@"tnn_"
							@"beauty_config":beautyConfigJson
};
// Init beauty kit
self.beautyKit = [[XMagic alloc] initWithRenderSize:previewSize assetsDict:assetsDict];
```

### Step 3. Add the log and event listener[](id:step3)
```objectivec
// Register log
[self.beautyKit registerSDKEventListener:self];
[self.beautyKit registerLoggerListener:self withDefaultLevel:YT_SDK_ERROR_LEVEL];
```

### Step 4. Configure beauty filter effects[](id:step4)
```objectivec
- (int)configPropertyWithType:(NSString *_Nonnull)propertyType withName:(NSString *_Nonnull)propertyName withData:(NSString*_Nonnull)propertyValue withExtraInfo:(id _Nullable)extraInfo;
```

### Step 5. Render videos[](id:step5)
In the preprocessing frame callback, construct `YTProcessInput` and pass `textureId` to the SDK for rendering.

```
 [self.xMagicKit process:inputCPU withOrigin:YtLightImageOriginTopLeft withOrientation:YtLightCameraRotation0]
```

### Step 6. Pause/Resume the SDK[](id:step6)

```objectivec
[self.beautyKit onPause];
[self.beautyKit onResume];
```

### Step 7. Add the SDK beauty filter panel to the layout[](id:step7)
```objectivec
UIEdgeInsets gSafeInset;
#if __IPHONE_11_0 && __IPHONE_OS_VERSION_MAX_ALLOWED >= __IPHONE_11_0
if(gSafeInset.bottom > 0){
}
if (@available(iOS 11.0, *)) {
	gSafeInset = [UIApplication sharedApplication].keyWindow.safeAreaInsets;
} else
#endif
	{
		gSafeInset = UIEdgeInsetsZero;
	}

dispatch_async(dispatch_get_main_queue(), ^{
	// Beauty filter option UI
	_vBeauty = [[BeautyView alloc] init];
	[self.view addSubview:_vBeauty];
	[_vBeauty mas_makeConstraints:^(MASConstraintMaker *make) {
		make.width.mas_equalTo(self.view);
		make.centerX.mas_equalTo(self.view);
		make.height.mas_equalTo(254);
		if(gSafeInset.bottom > 0.0){  // Adapt to full-view screen
			make.bottom.mas_equalTo(self.view.mas_bottom).mas_offset(0);
		} else {
			make.bottom.mas_equalTo(self.view.mas_bottom).mas_offset(-10);
		}
	}];
		_vBeauty.hidden = YES;
});
```
