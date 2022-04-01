## Preparations for Integration

1. Download and unzip the [demo package](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/iOS/2.4.1vcube/TRTC-API-Example.zip) and import the xMagic module (`bundle`, `XmagicIconRes`, and `Xmagic` folders) from the demo project into your actual project.
2. Import `libpag.framework`, `Masonry.framework`, `XMagic.framework`, and `YTCommonXMagic.framework` in the SDK directory.
3. For the framework signature, select **General** and set **Masonry.framework** and **libpag.framework** to **Embed & Sign**.
4. Replace the `Bundle ID` with the one under the obtained trial license.

## SDK API Integration 

- For steps [1](#step1)–[2](#step2), see the `viewDidLoad` and `buildBeautySDK` methods of the `ThirdBeautyViewController` class in the demo project. The `application` method of the `AppDelegate` class performs xMagic authentication.
- For steps [4](#step4)–[7](#step7), see the instance code of the `ThirdBeautyViewController` and `BeautyView` classes in the demo project.

### Step 1. Initialize authorization[](id:step1)

1. Add the following authentication code to the `didFinishLaunchingWithOptions` of the `AppDelegate` in the project, where the `LicenseURL` and `LicenseKey` are the authorization information obtained at Tencent Cloud official website as instructed in [License Guide](https://intl.cloud.tencent.com/document/product/1143/45380):
```
[TXLiveBase setLicenceURL:LicenseURL key:LicenseKey];
```
2. xMagic authentication: set the `URL` and `KEY` in the initialization code of the relevant business module to trigger the license download. Avoid downloading it just before use. You can also trigger the download in the `didFinishLaunchingWithOptions` method of the `AppDelegate`. Here, `LicenseURL` and `LicenseKey` are the information generated in the console when the license is bound.
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
</tr>
<tr>
<td>-3</td>
<td>Download failed. Check the network settings.</td>
</tr>
<tr>
<td>-4</td>
<td>The Tencent Effect SDK authorization information read from the local system is empty, which may be caused by an I/O failure.</td>
</tr>
<tr>
<td>-5</td>
<td>The content of read VCUBE TEMP license file is empty, which may be caused by an I/O failure.</td>
</tr>
<tr>
<td>-6</td>
<td>The JSON field in the `v_cube.license` file is incorrect. Contact Tencent Cloud for assistance.</td>
</tr>
<tr>
<td>-7</td>
<td>Signature verification failed. Contact Tencent Cloud for assistance.</td>
</tr>
<tr>
<td>-8</td>
<td>Decryption failed. Contact Tencent Cloud for assistance.</td>
</tr>
<tr>
<td>-9</td>
<td>The JSON field in the `TELicense` field is incorrect. Contact Tencent Cloud for assistance.</td>
</tr>
<tr>
<td>-10</td>
<td>The Tencent Effect SDK authorization information parsed online is empty. Contact Tencent Cloud for assistance.</td>
</tr>
<tr>
<td>-11</td>
<td>Failed to write the Tencent Effect SDK authorization information to the local file, which may be caused by an I/O failure.</td>
</tr>
<tr>
<td>-12</td>
<td>Failed to download and failed to parse local assets.</td>
</tr>
<tr>
<td>-13</td>
<td>Authentication failed.</td>
</tr>
<tr>
<td>Others</td>
<td>Contact Tencent Cloud for assistance.</td>
</tr>
</tbody></table>

### Step 2. Set the SDK material resource path[](id:step2)

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

### Step 5. Perform rendering[](id:step5)
In the video frame callback API, construct and pass `YTProcessInput` to the SDK for rendering. You can refer to `ThirdBeautyViewController` in the demo.
```objectivec
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
        if(gSafeInset.bottom > 0.0){  // Adaptive to full screen
            make.bottom.mas_equalTo(self.view.mas_bottom).mas_offset(0);
        } else {
            make.bottom.mas_equalTo(self.view.mas_bottom).mas_offset(-10);
        }
    }];
    _vBeauty.hidden = YES;
});
```

