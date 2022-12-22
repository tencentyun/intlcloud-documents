AvatarはTencent Effectの機能の一部であるため、先にTencent Effect美顔エフェクトSDKを統合してからAvatar素材をロードする必要があります。Tencent Effect美顔エフェクトSDKを接続していない場合は、[Tencent Effectの独立した統合 >](https://intl.cloud.tencent.com/document/product/1143/45384)を参照して理解し、統合を行うことができます。

## ステップ1：Avatar素材の準備
1. Tencent Effect SDKを統合します。
2. 対応するDemoプロジェクトを公式サイトからダウンロードし、解凍します。
3. Demo内の`BeautyDemo/bundle/avatarMotionRes.bundle`素材ファイルをご自身のプロジェクトにコピーします。

## ステップ2：Demoインターフェースの接続
### アクセス方法
1. プロジェクトではBeautyDemoと同じAvatar操作インターフェースを使用します。
2. Demo内の`BeautyDemo/Avatar`フォルダ下のすべてのクラスをプロジェクトにコピーし、次のコードを追加すれば完了です。
```objective-c
	 AvatarViewController *avatarVC = [[AvatarViewController alloc] init];
	 avatarVC.modalPresentationStyle = UIModalPresentationFullScreen;
	 avatarVC.currentDebugProcessType = AvatarPixelData; // 画像またはテクスチャId方式
	 [self presentViewController:avatarVC animated:YES completion:nil];
```

## Demoインターフェースの説明

#### 1. Demo UI[](id:demoui)
<img src="https://qcloudimg.tencent-cloud.cn/raw/1b25592a83e2e7f38ded001ca8c0b93b.png" style="zoom:66%;" />

#### 2. 実現方法
操作パネルデータはJSONファイルの解析によって取得したものです。Demo内のこのファイルを`BeautyDemo/Avatar/`ディレクトリに配置します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/7ae4858642c7dedcba05514a2ffed06a.png" style="zoom:100%;" />
- **JSON構造とUIパネルの対応関係**
	- headは最初のiconで選択した内容です。
<img src="https://qcloudimg.tencent-cloud.cn/raw/6547824e221494545e5353e8dce5e1cc.png" style="zoom:67%;" />
	- subTabsは右側の第2階層メニューに対応します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/0cb8236d813fc9ec278b7026063a7b88.png" style="zoom:67%;" />
	- itemsは右側の第3階層メニューに対応します。<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/2ad79a0d0efcb34cc5c1816975badfd8.png" style="zoom:67%;" />
- **パネル解析で得られたデータをSDKインターフェースで取得したAvatarオブジェクトデータにバインドします**
下図の上半分はSDKが取得したavatarディクショナリ（keyはcategor、valueはavatar配列）、下半分はパネルのデータです。パネルのオプションをクリックすると、パネルの第2階層タイトルからcategory（**赤枠で表示**）を取得し、このcetogoryによってSDKが返すavatarディクショナリ内で対応するavatarData配列を取得できます。パネルの第3階層タイトルからID（**青枠で表示**）を取得し、このIDによってavatarData配列の中で対応するavatarDataオブジェクトにマッチさせ、このオブジェクトをSDKのupdateAvatarに渡してアバター制作を完了することができます。<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/c908600561bded5e9f2ba20b5cde0029.png" style="zoom: 43%;" />

<img src="https://qcloudimg.tencent-cloud.cn/raw/2de257429b7abaa5e21923c292dd5c9a.png" style="zoom: 43%;" />

#### 3. タイトルのアイコン/文字の変更
[Demo UI](#demoui)画像に示すJSONファイルを変更します。例えば**ヘッダー**に表示するiconを変更するには、下図の赤枠内のiconUrlとcheckedIconUrlを変更します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/58e042d3fb8cb0588062dde318063a5e.png" style="zoom:57%;" />

## ステップ3：アバター制作機能のカスタマイズ
`BeautyDemo/Avatar/Controller`内の**AvatarViewController**関連コードを参照できます。
>? インターフェースの説明については[Avatar SDKの説明](https://www.tencentcloud.com/document/product/1143/51287)をご参照ください。

1. xmagicオブジェクトを作成し、Avatarデフォルトテンプレートを設定します。
```objectivec
- (void)buildBeautySDK {

	CGSize previewSize = CGSizeMake(kPreviewWidth, kPreviewHeight);
	NSString *beautyConfigPath = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) lastObject];
	beautyConfigPath = [beautyConfigPath stringByAppendingPathComponent:@"beauty_config.json"];
	NSFileManager *localFileManager=[[NSFileManager alloc] init];
	BOOL isDir = YES;
	NSDictionary * beautyConfigJson = @{};
	if ([localFileManager fileExistsAtPath:beautyConfigPath isDirectory:&isDir] && !isDir) {
			NSString *beautyConfigJsonStr = [NSString stringWithContentsOfFile:beautyConfigPath encoding:NSUTF8StringEncoding error:nil];
			NSError *jsonError;
			NSData *objectData = [beautyConfigJsonStr dataUsingEncoding:NSUTF8StringEncoding];
			beautyConfigJson = [NSJSONSerialization JSONObjectWithData:objectData                                                           options:NSJSONReadingMutableContainers
																															 error:&jsonError];
	}
	NSDictionary *assetsDict = @{@"core_name":@"LightCore.bundle",
															 @"root_path":[[NSBundle mainBundle] bundlePath],
															 @"tnn_"
															 @"beauty_config":beautyConfigJson
	};
	// Init beauty kit
	self.beautyKit = [[XMagic alloc] initWithRenderSize:previewSize assetsDict:assetsDict];
	// Register log
	[self.beautyKit registerSDKEventListener:self];
	[self.beautyKit registerLoggerListener:self withDefaultLevel:YT_SDK_ERROR_LEVEL];

	// 素材ファイルに対応するパスを渡すとavatarデフォルトキャラクターをロードできます
	AvatarGender gender = self.genderBtn.isSelected ? AvatarGenderFemale : AvatarGenderMale;
	NSString *bundlePath = [self.resManager avatarResPath:gender];
	[self.beautyKit loadAvatar:bundlePath exportedAvatar:nil];

}
```
2. 素材のAvatarソースデータを取得します。
```objectivec
@implementation AvatarViewController
_resManager = [[AvatarResManager alloc] init];
NSDictionary *avatarDict = self.resManager.getMaleAvatarData;
@end


@implementation AvatarResManager

- (NSDictionary *)getMaleAvatarData
{
	if (!_maleAvatarDict) {
			NSString *resDir = [self avatarResPath:AvatarGenderFemale];
			NSString *savedConfig = [self getSavedAvatarConfigs:AvatarGenderMale];
			// sdkインターフェースで素材ソースデータを解析します
			_maleAvatarDict = [XMagic getAvatarConfig:resDir exportedAvatar:savedConfig];
	}
	return _maleAvatarDict;
}
@end
```
3. アバター制作操作を行います。
```objectivec
// sdkインターフェースで解析した素材ソースデータから必要なキャラクターのavatarオブジェクトを取得し、sdkに渡します
NSMutableArray *avatars = [NSMutableArray array];
// avatarConfigはsdkインターフェースgetAvatarConfig:exportedAvatar:から取得したavatarオブジェクトの1つです
[avatars addObject:avatarConfig];
// アバター制作/着せ替えインターフェース。呼び出すと現在の素材で表現されるキャラクターをリアルタイムに更新します
[self.beautyKit updateAvatar:avatars];
```
4. アバター制作文字列のエクスポート：
現在のAvatar設定のオブジェクトを文字列としてエクスポートし、カスタム保存できます。
```objectivec
- (BOOL)saveSelectedAvatarConfigs:(AvatarGender)gender
{
	NSMutableArray *avatarArr = [NSMutableArray array];
	NSDictionary *avatarDict = gender == AvatarGenderMale ? _maleAvatarDict : _femaleAvatarDict;
	// 1、選択したavatarオブジェクトをトラバースして探します
	for (NSArray *arr in avatarDict.allValues) {
			for (AvatarData *config in arr) {
					if (config.type == AvatarDataTypeSelector) {
							if (config.isSelected) {
									[avatarArr addObject:config];
							}
					}else{
							[avatarArr addObject:config];
					}
			}
	}
	// 2、sdkインターフェースを呼び出し、選択したavatarオブジェクトを文字列としてエクスポートします
	NSString *savedConfig = [XMagic exportAvatar:avatarArr.copy];
	if (savedConfig.length <= 0) {
			return NO;
	}
	NSError *error;
	NSString *fileName = [self getSaveNameWithGender:gender];
	NSString *savePath = [_saveDir stringByAppendingPathComponent:fileName];
	// ディレクトリが存在するかどうかを判断し、存在しない場合はディレクトリを作成します
	BOOL isDir;
	if (![[NSFileManager defaultManager] fileExistsAtPath:_saveDir isDirectory:&isDir]) {
			[[NSFileManager defaultManager] createDirectoryAtPath:_saveDir withIntermediateDirectories:YES attributes:nil error:nil];
	}
	// 3、エクスポートした文字列をサンドボックスに書き込み、次回取り出して使用できるようにします
	[savedConfig writeToFile:savePath atomically:YES encoding:NSUTF8StringEncoding error:&error];
	if (error) {
			return NO;
	}
	return YES;
}
```
5. バーチャル背景とリアル背景を切り替えます。
```objectivec
- (void)bgExchangeClick:(UIButton *)btn
{
	btn.selected = !btn.isSelected;
	NSDictionary *avatarDict = self.resManager.getFemaleAvatarData;
	NSArray *array = avatarDict[@"background_plane"];
	AvatarData *selConfig;
	// 背景も実際にはavatarオブジェクトの1つです。categoryはbackground_planeであり、背景を置き換えることはすなわち異なるavatarオブジェクトを設定することになります
	for (AvatarData *config in array) {
			if ([config.Id isEqual:@"none"]) {
					if (btn.selected) {
							selConfig = config;
							break;
					}
			}else{
					selConfig = config;
			}
	}
	[self.beautyKit updateAvatar:@[selConfig]];
}
```