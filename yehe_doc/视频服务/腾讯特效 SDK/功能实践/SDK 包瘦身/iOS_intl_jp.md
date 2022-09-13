## リソースのダイナミックダウンロード
パッケージのサイズを抑えるため、SDKが必要とするモデルリソースとモーションリソースMotionRes（一部のベーシック版SDKにはモーションリソースがありません）をオンラインダウンロードに変更してください。ダウンロード後に、上記のファイルのパスをSDKに設定します。

1. 美顔リソースのZIPパッケージをクラウドにアップロードして、ダウンロードURLを生成します。例：`https://服务器地址/LightCore.bundle.zip`。
2. プロジェクトの中で生成されたURLからファイルをダウンロードして、サンドボックスに解凍します(例：サンドボックスパス`Document/Xmagic`）。ここまで操作すると、Document/XmagicフォルダーにSDKが必要とするリソースが揃っています。
![](https://qcloudimg.tencent-cloud.cn/raw/f90fe608cc12156a3b4b778f0ad4d969.png)   
3. SDKを初期化するとき、root_pathフィールドにステップ2のサンドボックスパスを渡します。
```objectivec
 NSDictionary *assetsDict = @{@"core_name":@"LightCore.bundle",
                              @"root_path":_filePath ,//_filePathはローカルにダウンロードされた美顔リソースが所在する親ディレクトリ:Ducument/Xmagicです。
                              @"tnn_"
                              @"beauty_config":beautyConfigJson
 };
 // Init beauty kit                                 @"root_path":Ducument/Xmagic,
 self.beautyKit = [[XMagic alloc] initWithRenderSize:_inputSize assetsDict:assetsDict];
```
4. 美顔パネルの各美顔エフェクトのアイコンを設定し、ダウンロードしたリソースファイルから該当するimageを取得します。
```objectivec
NSMutableArray *arrayModels = [NSMutableArray array];
for (NSDictionary* dict in motionArray) {
	BeautyCellModel* model = [BeautyCellModel beautyWithDict:dict];
	// Load default mainbundle path of motionres
	if ([model.title isEqualToString:NSLocalizedString(@"item_none_label",nil)]) {
		model.icon = [NSString stringWithFormat:@"%@/%@.png", [[NSBundle mainBundle] bundlePath], model.key];
		[arrayModels addObject:model];
	}else{
		if(_useNetResource && _filePath != nil){ //ネット上のリソースを使用する場合
			NSString *DirPath = [_filePath stringByAppendingPathComponent:@"2dMotionRes.bundle/"]; //美顔リソースの絶対パスを取得します
			model.icon = [NSString stringWithFormat:@"%@/%@/template.png", DirPath, model.key];
		}else{
			model.icon = [NSString stringWithFormat:@"%@/%@/template.png", [[NSBundle mainBundle] pathForResource:@"2dMotionRes" ofType:@"bundle"], model.key];
		}
		if ([fileManager fileExistsAtPath:model.icon]) {
			[arrayModels addObject:model];
		}
	}
}
```
5. 美顔エフェクトのパラメータの受け渡しを設定します（詳しくは[APIドキュメント](https://intl.cloud.tencent.com/document/product/1143/48646)をご参照ください）。

```objectivec
/// @brief 美顔の各エフェクトを設定します
/// @param propertyType エフェクトタイプ 文字列：beauty, lut, motion
/// @param propertyName エフェクト名
/// @param propertyValue エフェクトの値
/// @param extraInfo リザーブド拡張、オプションナル設定項目dictあり
/// @return 成功した場合は0、失敗した場合はその他を返します
/// @note 詳細説明
/**
| エフェクトタイプ | エフェクト名 | エフェクトの値 | 説明  | 備考 |
| :---- | :---- |:---- | :---- | :---- |
|  beauty  | 美顔id名 | 美顔エフェクトの強度値 |美顔タイプ設定インターフェース | なし |
|  lut  | フィルターのパス+フィルター名 | フィルターの強度値 | フィルタータイプ設定インターフェース | なし |
|  motion  | モーションパス名 | モーションパス | モーションタイプ設定インターフェース| **注意**：リソースにzipがある場合、入力モーションパスが書き込み可能なパスであることを確認してください。そうでなければ、appパッケージにパッケージングした場合、手動でunzipしないと使用できません |
**/
- (int)configPropertyWithType:(NSString *_Nonnull)propertyType withName:(NSString *_Nonnull)propertyName withData:(NSString*_Nonnull)propertyValue withExtraInfo:(id _Nullable)extraInfo;
```

## 例
### 美顔の各エフェクトを設定します
「美顔」と「美ボディ」のエフェクトは処理する必要はありません。SDKの内部では自動的にダウンロードしたリソースファイルを使用します。美顔配下の美白エフェクトを使用することを例として、SDKに渡したパラメーターを以下に示します：
```objectivec
[self.beautyKitRef configPropertyWithType:@"beauty" withName:@"beauty.whiten" withData:@"30" withExtraInfo:nil];
```
この場合、SDKに渡した各パラメーターの値は以下のとおりです：

| フィールド          | 値            |
| ------------- | ------------- |
| propertyType  | beauty        |
| propertyName  | beauty.whiten |
| propertyValue | 30            |
| extraInfo     | nil           |

### フィルターのエフェクトを設定します
keyを処理する必要があります。固有のローカル美顔リソースまたはネットからローカルにダウンロードした美顔リソースを使用できます。
```objectivec
NSString *key = [_model.lutIDs[index] path];
if (key != nil) {
    key = [@"lut.bundle/" stringByAppendingPathComponent:key];//フィルターエフェクト画像の相対パス
}
if(_useNetResource && _filePath != nil){ //ダウンロードした美顔リソースを使用する場合
    key = [_filePath stringByAppendingPathComponent:key];//エフェクト画像の絶対パスを生成します
}
[self.beautyKitRef configPropertyWithType:@"lut" withName:key withData:[NSString 
stringWithFormat:@"%f",value] withExtraInfo:nil];
```

### フィルター配下のホワイトニングエフェクトを設定します
ローカルリソースとネットワークリソースを使用する時に渡すパラメータの例を以下に示します：

| フィールド          | ローカルリソースを使用する時に渡すパラメータ | ネットワークリソースを使用する時に渡すパラメータ                                     | 備考     |
| ------------- | ------------------------ | ------------------------------------------------------------ | -------- |
| propertyType  | lut                      | lut                                                          |     -     |
| propertyName  | lut.bundle/n_baixi.png   | `/var/mobile/Containers/Data/Application/25C7D01A-73F6-4F1B-AEB6-5EE03A221D18/Documents/Xmagic/lut.bundle/n_baixi.png` | ファイルパス |
| propertyValue | 60.000000                | 60.000000                                                    |    -      |
| extraInfo     | null                     | null                                                         |      -    |

### モーション、メイク、分割エフェクトを設定します
propertyValueフィールドを処理する必要があります。固有のローカル美顔リソースまたはネットからローカルにダウンロードした美顔リソースを使用できます。
```objectivec
NSString *key = [_model.motionIDs[index] key];
        NSString *path = [_model.motionIDs[index] path];
        NSString *motionRootPath = path==nil?[[NSBundle mainBundle] pathForResource:@"MotionRes" ofType:@"bundle"]:path;
        if(_useNetResource && _filePath != nil){ //ダウンロードした美顔リソースを使用する場合
            motionRootPath = [_filePath stringByAppendingPathComponent:@"2dMotionRes.bundle"];//2dMotionResの絶対パスを生成します
        }
        [self.beautyKitRef configPropertyWithType:@"motion" withName:key withData:motionRootPath withExtraInfo:nil];
```

### 2Dモーション配下の可愛い落書きエフェクトを設定します
ローカルリソースとネットワークリソースを使用する時に渡すパラメータの例を以下に示します：

| フィールド          | ローカルリソースを使用する時に渡すパラメータ | ネットワークリソースを使用する時に渡すパラメータ                                     | 備考     |
| ------------- | ------------- | ------------- | -------- |
| propertyType  | motion | motion |        -  |
| propertyName  | video_keaituya | video_keaituya |       -   |
| propertyValue | `/private/var/containers/Bundle/Application/FD2D7912-E58E-4584-B7E4-8715B8D2338F/BeautyDemo.app/2dMotionRes.bundle` | `/var/mobile/Containers/Data/Application/25C7D01A-73F6-4F1B-AEB6-5EE03A221D18/Documents/Xmagic/2dMotionRes.bundle` | ファイルパス |
| extraInfo     | nil | nil |     -     |

