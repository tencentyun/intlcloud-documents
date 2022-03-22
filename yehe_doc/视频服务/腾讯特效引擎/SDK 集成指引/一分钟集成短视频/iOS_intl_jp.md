## 統合の準備[](id:ready)

1. [Demoパッケージ](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/iOS/2.4.1vcube/UGSV-API-Example.zip)をダウンロードして解凍し、Demoプロジェクトのxmagicモジュール（bundle、XmagicIconResの2つのフォルダ内のファイル、**Record** > **View**フォルダ内のファイル）を実際のプロジェクトにインポートします。
2. libディレクトリの中の`libpag.framework`、`Masonry.framework`、`XMagic.framework`および`YTCommonXMagic.framework`をインポートします。
3. framework署名の**General--> Masonry.framework**および**libpag.framework**で**Embed & Sign**を選択します。
4. Bundle IDを、テスト用に申請した権限と同じものに変更します。

## SDKインターフェースの統合 [](id:step)

- [ステップ1](#step1)および[ステップ2](#step2)については、DemoプロジェクトのUGCKitRecordViewControllerクラスのviewDidLoad、buildBeautySDKのメソッドを参照できます。
- [ステップ4](#step4)から[ステップ7](#step7)までは、DemoプロジェクトのUGCKitRecordViewController、BeautyViewクラスの関連インスタンスコードを参照できます。

### ステップ1：権限の初期化 [](id:step1)
1. プロジェクトのAppDelegateのdidFinishLaunchingWithOptionsに次のコードを追加します。このうちLicenseURL、LicenseKeyはTencent Cloud公式サイトに権限承認を申請した際の情報とします。[Licenseガイド](https://intl.cloud.tencent.com/document/product/1143/45380)をご参照ください。
```
[TXUGCBase setLicenceURL:LicenseURL key:LicenseKey];

[TELicenseCheck setTELicense:@"https://license.vod2.myqcloud.com/license/v2/1258289294_1/v_cube.license" key:@"3c16909893f53b9600bc63941162cea3" completion:^(NSInteger authresult, NSString * _Nonnull errorMsg) {
              if (authresult == TELicenseCheckOk) {
                   NSLog(@"認証成功");
               }else{
                   NSLog(@"認証失敗");
               }
       }];
```
2. 権限コードについてはDemo内のUGCKitRecordViewControllerクラスのviewDidLoad内の権限コードを参照できます。
```
NSString *licenseInfo = [TXUGCBase getLicenceInfo];
NSData *jsonData = [licenseInfo dataUsingEncoding:NSUTF8StringEncoding];
NSError *err = nil;
NSDictionary *dic = [NSJSONSerialization JSONObjectWithData:jsonData
options:NSJSONReadingMutableContainers error:&err];
NSString *xmagicLicBase64Str = [dic objectForKey:@"TELicense"];

//xmagic権限の初期化
int authRet = [XMagicAuthManager initAuthByString:xmagicLicBase64Str withSecretKey:@""];// withSecretKeyは空の文字列とし、内容を入力する必要はありません
NSLog(@"xmagic auth ret : %i", authRet);
NSLog(@"xmagic auth version : %@", [XMagicAuthManager getVersion]);
```

### ステップ2：SDK素材リソースパスの設定 [](id:step2)

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

### ステップ3：ログおよびイベント監視の追加[](id:step3)
```
// Register log
[self.beautyKit registerSDKEventListener:self];
[self.beautyKit registerLoggerListener:self withDefaultLevel:YT_SDK_ERROR_LEVEL];
```

### ステップ4：各種美顔効果の設定[](id:step4)

```
- (int)configPropertyWithType:(NSString *_Nonnull)propertyType withName:(NSString *_Nonnull)propertyName withData:(NSString*_Nonnull)propertyValue withExtraInfo:(id _Nullable)extraInfo;
```

### ステップ5：レンダリング処理の実施[](id:step5)
UGSVの前処理フレームコールバックインターフェースで、YTProcessInputを作成してtextureIdをSDKに渡し、レンダリング処理を行います。

```
 [self.xMagicKit process:inputCPU withOrigin:YtLightImageOriginTopLeft withOrientation:YtLightCameraRotation0]
```

### ステップ6：SDKの一時停止/再開[](id:step6)

```
[self.beautyKit onPause];
[self.beautyKit onResume];
```

### ステップ7：レイアウトにSDK美顔パネルを追加 [](id:step7)

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
	//美顔オプションインターフェース
	_vBeauty = [[BeautyView alloc] init];
	[self.view addSubview:_vBeauty];
	[_vBeauty mas_makeConstraints:^(MASConstraintMaker *make) {
		make.width.mas_equalTo(self.view);
		make.centerX.mas_equalTo(self.view);
		make.height.mas_equalTo(254);
		if(gSafeInset.bottom > 0.0){  // 全画面適用
			make.bottom.mas_equalTo(self.view.mas_bottom).mas_offset(0);
		}else{
			make.bottom.mas_equalTo(self.view.mas_bottom).mas_offset(-10);
		}
	}];
		_vBeauty.hidden = YES;
});
```
