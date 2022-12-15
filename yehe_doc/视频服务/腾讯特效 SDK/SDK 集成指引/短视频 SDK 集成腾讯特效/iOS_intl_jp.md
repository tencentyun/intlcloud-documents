## 統合の準備[](id:ready)

1. [Demoパッケージ](https://intl.cloud.tencent.com/document/product/1143/45374)をダウンロードして解凍し、Demoプロジェクトの`demo/XiaoShiPin/`ディレクトリ下のxmagickitフォルダをご自身のプロジェクトのpodfileファイルと同じレベルのディレクトリ下にコピーします。
2. Podfileファイル内に以下の依存関係を追加します。その後、`pod install`コマンドを実行すると、インポートが完了します。
```
pod 'xmagickit', :path => 'xmagickit/xmagickit.podspec'
```
3. Bundle IDを、テスト用に申請した権限と同じものに変更します。

### 開発者環境要件
- 開発ツールXCode11以降：App Storeまたは[アドレスのダウンロード](https://developer.apple.com/xcode/resources/)をクリックします。
- 推奨実行環境：
  - デバイス要件：iPhone 5およびそれ以上。iPhone 6およびそれ以下はフロントカメラのサポートは最大720pとし、1080pはサポートしていません。
  - システム要件：iOS 12.0およびそれ以降のバージョン。


## SDKインターフェースの統合 [](id:step)
### 手順1：権限の初期化 [](id:step1)
プロジェクトのAppDelegateのdidFinishLaunchingWithOptionsに次のコードを追加します。このうちLicenseURL、LicenseKeyはTencent Cloud公式サイトに権限承認を申請した際の情報とします。
```objectivec
[TXUGCBase setLicenceURL:LicenseURL key:LicenseKey];

[TELicenseCheck setTELicense:LicenseURLkey:LicenseKey completion:^(NSInteger authresult, NSString * _Nonnull errorMsg) {
              if (authresult == TELicenseCheckOk) {
                   NSLog(@"認証成功");
               }else{
                   NSLog(@"認証失敗");
               }
       }];
```
**認証errorCodeの説明**：

| エラーコード                            | 説明                                               |
| :----- | :------------------------------------------------------ |
| 0      | 成功。Success                                           |
| -1     | 入力パラメータが無効です（例：URLまたはKEYが空など）。          |
| -3     | ダウンロードの段階で失敗しました。ネットワークの設定を確認してください                            |
| -4     | ローカルから読み取ったTE権限承認情報が空です。IOの失敗による可能性があります        |
| -5     | 読み取ったVCUBE TEMP Licenseファイルの内容が空です。IOの失敗による可能性があります |
| -6     | v_cube.licenseファイルのJSONフィールドが正しくありません。Tencent Cloudチームに連絡して処理を依頼してください |
| -7     | 署名の検証に失敗しました。Tencent Cloudチームに連絡して処理を依頼してください   |
| -8     | 復号に失敗しました。Tencent Cloudチームに連絡して処理を依頼してください   |
| -9     | TELicenseフィールド内のJSONフィールドが正しくありません。Tencent Cloudチームに連絡して処理を依頼してください |
| -10    | ネットワークから解析したTE権限承認情報が空です。Tencent Cloudチームに連絡して処理を依頼してください  |
| -11    | TE権限承認情報をローカルファイルに書き込む際に失敗しました。IOの失敗による可能性があります      |
| -12    | ダウンロードに失敗しました。ローカルassetの解析も失敗しました       |
| -13    | 認証に失敗しました                                                |
| その他   | Tencent Cloudチームに連絡して処理を依頼してください  |


### 手順2：SDK素材リソースパスの設定 [](id:step2)

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

### 手順3：ログおよびイベント監視の追加[](id:step3)
```objectivec
// Register log
[self.beautyKit registerSDKEventListener:self];
[self.beautyKit registerLoggerListener:self withDefaultLevel:YT_SDK_ERROR_LEVEL];
```

### 手順4：各種美顔効果の設定[](id:step4)
```objectivec
- (int)configPropertyWithType:(NSString *_Nonnull)propertyType withName:(NSString *_Nonnull)propertyName withData:(NSString*_Nonnull)propertyValue withExtraInfo:(id _Nullable)extraInfo;
```

### 手順5：レンダリング処理の実施[](id:step5)
UGSVの前処理フレームコールバックインターフェースで、YTProcessInputを作成してtextureIdをSDKに渡し、レンダリング処理を行います。

```
 [self.xMagicKit process:inputCPU withOrigin:YtLightImageOriginTopLeft withOrientation:YtLightCameraRotation0]
```

### 手順6：SDKの一時停止/再開[](id:step6)

```objectivec
[self.beautyKit onPause];
[self.beautyKit onResume];
```

### 手順7：レイアウトにSDK美顔パネルを追加 [](id:step7)
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