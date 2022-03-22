## 統合の準備

1. [Demoパッケージ](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/iOS/2.4.1vcube/TRTC-API-Example.zip)をダウンロードして解凍し、Demoプロジェクトのxmagicモジュール（bundle、XmagicIconRes、Xmagicフォルダ）を実際のプロジェクトにインポートします。
2. SDKディレクトリの中の`libpag.framework`、`Masonry.framework`、`XMagic.framework`、`YTCommonXMagic.framework`をインポートします。
3. framework署名の**General--> Masonry.framework**および**libpag.framework**で**Embed & Sign**を選択します。
4. Bundle IDを、テスト用に申請した権限と同じものに変更します。

## SDKインターフェースの統合 

- [ステップ1](#step1)および[ステップ2](#step2)については、DemoプロジェクトのThirdBeautyViewControllerクラスのviewDidLoad、buildBeautySDKのメソッドを参照できます。AppDelegateクラスのapplicationメソッドはXmagic認証を実行します。
- [ステップ4](#step4)から[ステップ7](#step7)までは、DemoプロジェクトのThirdBeautyViewController、BeautyViewクラスの関連インスタンスコードを参照できます。

### ステップ1：権限の初期化[](id:step1)

1. まず初めにプロジェクトのAppDelegateのdidFinishLaunchingWithOptionsに次の認証コードを追加します。このうちLicenseURLおよびLicenseKeyはTencent Cloud公式サイトに権限承認を申請した際の情報とします。[Licenseガイド](https://intl.cloud.tencent.com/document/product/1143/45380)をご参照ください。
```
[TXLiveBase setLicenceURL:LicenseURL key:LicenseKey];
```
2. Xmagicの認証：関連業務モジュールの初期化コードの中でURLとKEYを設定し、licenseのダウンロードをトリガーします。使用する直前になってダウンロードすることは避けてください。あるいはAppDelegateのdidFinishLaunchingWithOptionsメソッドでダウンロードをトリガーすることもできます。このうちLicenseURLとLicenseKeyはコンソールでLicenseをバインドした際に生成された権限承認情報です。
```
[TELicenseCheck setTELicense:LicenseURL key:LicenseKey completion:^(NSInteger authresult, NSString * _Nonnull errorMsg) {
       if (authresult == TELicenseCheckOk) {
            NSLog(@"認証成功");
        }else{
            NSLog(@"認証失敗");
        }
    }];
```
**認証errorCodeの説明**：
<table>
<thead>
<tr>
<th>エラーコード</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td>成功です。Success</td>
</tr>
<tr>
<td>-1</td>
<td>入力パラメータが無効です（例：URLまたはKEYが空など）</td>
</tr>
<tr>
<td>-3</td>
<td>ダウンロードの段階で失敗しました。ネットワークの設定を確認してください</td>
</tr>
<tr>
<td>-4</td>
<td>ローカルから読み取ったTE権限承認情報が空です。IOの失敗による可能性があります</td>
</tr>
<tr>
<td>-5</td>
<td>読み取ったVCUBE TEMP Licenseファイルの内容が空です。IOの失敗による可能性があります</td>
</tr>
<tr>
<td>-6</td>
<td>v_cube.licenseファイルのJSONフィールドが正しくありません。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
<tr>
<td>-7</td>
<td>署名の検証に失敗しました。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
<tr>
<td>-8</td>
<td>復号に失敗しました。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
<tr>
<td>-9</td>
<td>TELicenseフィールド内のJSONフィールドが正しくありません。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
<tr>
<td>-10</td>
<td>ネットワークから解析したTE権限承認情報が空です。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
<tr>
<td>-11</td>
<td>TE権限承認情報をローカルファイルに書き込む際に失敗しました。IOの失敗による可能性があります</td>
</tr>
<tr>
<td>-12</td>
<td>ダウンロードに失敗しました。ローカルassetの解析も失敗しました</td>
</tr>
<tr>
<td>-13</td>
<td>認証に失敗しました</td>
</tr>
<tr>
<td>その他</td>
<td>Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
</tbody></table>

### ステップ2：SDK素材リソースパスの設定[](id:step2)

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

```objectivec
 // Register log
[self.beautyKit registerSDKEventListener:self];
[self.beautyKit registerLoggerListener:self withDefaultLevel:YT_SDK_ERROR_LEVEL];
```

### ステップ4：各種美顔効果の設定[](id:step4)

```objectivec
- (int)configPropertyWithType:(NSString *_Nonnull)propertyType withName:(NSString *_Nonnull)propertyName withData:(NSString*_Nonnull)propertyValue withExtraInfo:(id _Nullable)extraInfo;
```

### ステップ5：レンダリング処理の実施[](id:step5)
ビデオフレームコールバックインターフェースで、YTProcessInputを作成してSDKに渡し、レンダリング処理を行います。DemoのThirdBeautyViewControllerを参照できます。
```objectivec
 [self.xMagicKit process:inputCPU withOrigin:YtLightImageOriginTopLeft withOrientation:YtLightCameraRotation0]
```

### ステップ6：SDKの一時停止/再開[](id:step6)

```objectivec
[self.beautyKit onPause];
[self.beautyKit onResume];
```

### ステップ7：レイアウトにSDK美顔パネルを追加[](id:step7)
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

