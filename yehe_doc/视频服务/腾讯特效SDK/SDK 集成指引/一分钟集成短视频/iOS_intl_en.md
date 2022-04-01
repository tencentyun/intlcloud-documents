## Preparations for Integration[](id:ready)

1. Download and unzip the [demo package](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/iOS/2.4.1vcube/UGSV-API-Example.zip) and import the xMagic module (files in the `bundle`, `XmagicIconRes`, and `Record > View` folders) from the demo project into your actual project.
2. Import `libpag.framework`, `Masonry.framework`, `XMagic.framework`, and `YTCommonXMagic.framework` in the `lib` directory.
3. For the framework signature, select **General** and set **Masonry.framework** and **libpag.framework** to **Embed & Sign**.
4. Replace the `Bundle ID` with the one under the obtained trial license.

## SDK API Integration[](id:step)

- For steps [1](#step1)–[2](#step2), see the `viewDidLoad` and `buildBeautySDK` methods of the `UGCKitRecordViewController` class in the demo project.
- For steps [4](#step4)–[7](#step7), see the instance code of the `UGCKitRecordViewController` and `BeautyView` classes in the demo project.

### Step 1. Initialize authorization[](id:step1)
1. Add the following code to the `didFinishLaunchingWithOptions` of the `AppDelegate` in the project, where the `LicenseURL` and `LicenseKey` are the authorization information obtained at Tencent Cloud official website as instructed in [License Guide](https://intl.cloud.tencent.com/document/product/1143/45380):
```
[TXUGCBase setLicenceURL:LicenseURL key:LicenseKey];

[TELicenseCheck setTELicense:@"https://license.vod2.myqcloud.com/license/v2/1258289294_1/v_cube.license" key:@"3c16909893f53b9600bc63941162cea3" completion:^(NSInteger authresult, NSString * _Nonnull errorMsg) {
              if (authresult == TELicenseCheckOk) {
                   NSLog(@"Authentication succeeded");
               } else {
                   NSLog(@"Authentication failed");
               }
       }];
```
2. For authorization code, see the `viewDidLoad` of the `UGCKitRecordViewController` class in the demo:
```
NSString *licenseInfo = [TXUGCBase getLicenceInfo];
NSData *jsonData = [licenseInfo dataUsingEncoding:NSUTF8StringEncoding];
NSError *err = nil;
NSDictionary *dic = [NSJSONSerialization JSONObjectWithData:jsonData
options:NSJSONReadingMutableContainers error:&err];
NSString *xmagicLicBase64Str = [dic objectForKey:@"TELicense"];

// Initialize the xMagic authorization
int authRet = [XMagicAuthManager initAuthByString:xmagicLicBase64Str withSecretKey:@""];// `withSecretKey` is an empty string and doesn't need to be filled in
NSLog(@"xmagic auth ret : %i", authRet);
NSLog(@"xmagic auth version : %@", [XMagicAuthManager getVersion]);
```

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
```
// Register log
[self.beautyKit registerSDKEventListener:self];
[self.beautyKit registerLoggerListener:self withDefaultLevel:YT_SDK_ERROR_LEVEL];
```

### Step 4. Configure beauty filter effects[](id:step4)

```
- (int)configPropertyWithType:(NSString *_Nonnull)propertyType withName:(NSString *_Nonnull)propertyName withData:(NSString*_Nonnull)propertyValue withExtraInfo:(id _Nullable)extraInfo;
```

### Step 5. Perform rendering[](id:step5)
In the short video preprocessing frame callback API, construct `YTProcessInput` and pass `textureId` to the SDK for rendering.

```
 [self.xMagicKit process:inputCPU withOrigin:YtLightImageOriginTopLeft withOrientation:YtLightCameraRotation0]
```

### Step 6. Pause/Resume the SDK[](id:step6)

```
[self.beautyKit onPause];
[self.beautyKit onResume];
```

### Step 7. Add the SDK beauty filter panel to the layout[](id:step7)

```
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
