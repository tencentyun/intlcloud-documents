## SDKへのアクセス

SDKのダウンロード、接続、認証、Demoクイックスタートについては、[Tencent Effectの独立した統合](https://intl.cloud.tencent.com/document/product/1143/45384)をご参照ください。

## アバター制作素材の準備

現在Tencentでは、SDKと共にいくつかのアバター制作、着せ替え素材をご提供しています。素材はSDKの解凍後の`MotionRes/avatarRes`ディレクトリ内にあります。他の動的エフェクト素材と同様に、プロジェクトのassetsディレクトリにcopyする必要があります
![](https://qcloudimg.tencent-cloud.cn/raw/f712ea1424c224b5cac36403c4c218bf.png)

## アバター制作フローとSDKインターフェース
<table>
<tr>
	<th style="text-align:center">アバター制作フロー</th>
	<th style="text-align:center">写真撮影によるアバター制作のフロー</th>
</tr>
<tr>
	<td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/8dab03ae9b380cca30b7fb1408a82bdd.jpg" width=650></td>
	<td style="text-align:center"><img src="https://qcloudimg.tencent-cloud.cn/raw/8fe57503adf3f4f269de09edc178459f.jpg" width=550></td>
</tr>
</table>


XMagicApiのロードデータ、アバター制作、エクスポート設定、写真撮影アバター制作インターフェースの詳細は次のとおりです。

### 1. Avatarソースデータ取得インターフェース（getAvatarConfig）

```swift
+ (NSDictionary <NSString *, NSArray *>* _Nullable)getAvatarConfig:(NSString * _Nullable)resPath exportedAvatar:(NSString *_Nullable)exportedAvatar;
```

- **入力パラメータ**：
	- resPath：Avatar素材のスマートフォン上の絶対パスです。例：`/var/mobile/Containers/Data/Application/C82F1F7A-01A1-4404-8CF6-131B26B4DA1A/Library/Caches/avatarMotionRes.bundle/avatar_v2.0_male`。
	- exportedAvatar：ユーザーが前回のアバター制作後に保存したデータであり、JSON形式の文字列です。初めて使用する場合またはユーザーがそれまでに保存したことがない場合、この値はnilとなります。
- **出力パラメータ**：
	NSDictionaryの形式で返します。dictionaryのkeyはデータのcategoryです。詳細についてはTEDefineクラスをご覧ください。dictionaryのvalueはこのcategory下のすべてのデータです。アプリケーション層でこのdictionaryを取得した後、必要に応じて希望のUIスタイルを表示します。

### 2. Avatar素材ロードインターフェース（loadAvatar）
```swift
- (void)loadAvatar:(NSString * _Nullable)resPath exportedAvatar:(NSString * _Nullable)exportedAvatar;
```
- **入力パラメータ**：
	- resPath：avatar素材のスマートフォン上の絶対パスです。例：`/var/mobile/Containers/Data/Application/C82F1F7A-01A1-4404-8CF6-131B26B4DA1A/Library/Caches/avatarMotionRes.bundle/avatar_v2.0_male`。
	- exportedAvatar：ユーザーが前回のアバター制作後に保存したデータであり、json形式の文字列です。初めて使用する場合またはユーザーがそれまでに保存したことがない場合、この値はnilとなります。
- **出力パラメータ**：
NSDictionaryの形式で返します。dictionaryのkeyはデータのcategoryです。詳細についてはTEDefineクラスをご覧ください。dictionaryのvalueはこのcategory下のすべてのデータです。アプリケーション層でこのdictionaryを取得した後、必要に応じて希望のUIスタイルを表示します。

### 3. アバター制作、着せ替えインターフェース（updateAvatar）

```swift
- (void)updateAvatar:(NSArray<AvatarData *> *_Nonnull)avatarDataList;
```

呼び出すと現在の素材のプレビューキャラクターをリアルタイムに更新します。1つのAvatarDataオブジェクトは1つのアトミック設定であり（髪型変更など），一度に複数のアトミック設定を渡すことができます（髪型と髪色の両方を変更するなど）。このインターフェースは渡されるAvatarDataの有効性をチェックし、有効なものはSDKに設定し、無効なデータにはcallbackを返します。
- 例えば髪型の変更を要求しているのに、髪のモデルファイル（AvatarDataのvalueフィールド内に設定）がローカルに見つからない場合、このAvatarDataは無効と判断されます。
- また例えば、瞳マップの変更を要求しているのに、マップファイル（AvatarDataのvalueフィールド内に設定）がローカルに見つからない場合、このAvatarDataは無効と判断されます。

### 4. アバター制作設定エクスポートインターフェース（exportAvatar）

```swift
+ (NSString *_Nullable)exportAvatar:(NSArray <AvatarData *>*_Nullable)avatarDataList;
```

ユーザーがアバターを制作する際、AvatarDataのselectedステータスまたはブレンドシェイプ値を変更する場合があります。制作完了後、新しいフルAvatarDataリストを渡すとJSON文字列をエクスポートできます。この文字列はローカルに保存することも、サーバーにアップロードすることもできます。
このエクスポートされた文字列には2つの用途があります。
- 次回再びXMagicの**loadAvatar**インターフェースでこのAvatar素材をダウンロードする際、このJSON文字列を**exportedAvatar**として設定すると、ユーザーが前回作成したキャラクターをプレビューで表示することができます。
- 上記のように、getAllAvatarDataを呼び出す際にこのパラメータを渡すことで、Avatarソースデータ内の選択状態およびブレンドシェイプ値を変更できるようにする必要があります。


### 5. 写真撮影アバター制作インターフェース（createAvatarByPhoto）
このインターフェースにはネットワーク接続が必要です。

```swift
+ (void)createAvatarByPhoto:(NSString * _Nullable)photoPath avatarResPaths:(NSArray <NSString *>* _Nullable)avatarResPaths isMale:(BOOL)isMale success:(nullable void (^)(NSString *_Nullable matchedResPath, NSString *_Nullable srcData))success failure:(nullable void (^)(NSInteger code, NSString *_Nullable msg))failure;
```

- **photoPath**：写真のパスです。顔が確実に画面の中央に位置するようにしてください。画面内に含まれる顔は1つだけにすることをお勧めします。複数の顔がある場合、SDKはその中の1つを選択します。写真の短辺は500px以上を推奨します。これより小さいと認識効果に影響する可能性があります。
- **avatarResPaths**：複数のAvatar素材セットを渡すことができます。SDKは写真の分析結果に基づいて、最も適した素材のセットを選択し、自動的にアバター制作を行います。
>! 現在は1セットのみをサポートしています。複数のセットを渡した場合、SDKは最初の1セットのみを使用します。

- **isMale**：男性かどうか。この属性は現在使用されていませんが、今後SDKが最適化される場合を考え、正確に渡すことをお勧めします。
- **success**：成功のコールバックです。 matchedResPathはマッチした素材パス、srcDataはマッチ結果です。上記で述べたexportAvatarインターフェースが返すものは同じ意味となります。
- **failure**：失敗のコールバックです。codeはエラーコード、msgはエラーメッセージです。

### 6. ダウンロードした設定ファイルを対応するフォルダ内に配置する（addAvatarResource）

```swift
+ (void)addAvatarResource:(NSString * _Nullable)rootPath category:(NSString * _Nullable)category filePath:(NSString * _Nullable)filePath completion:(nullable void (^)(NSError * _Nullable error, NSArray <AvatarData *>* _Nullable avatarList))completion;
```

このインターフェースは主にAvatarパーツの動的ダウンロードのシナリオに用いられます。例としては、Avatar素材内に10種類の髪型があり、その後1種類の髪型をクライアントに動的に送信したい場合、ダウンロード完了後に圧縮パッケージを取得してからこのインターフェースを呼び出し、圧縮パッケージのパスをSDKに渡します。SDKはこの圧縮パッケージを解析し、対応するcategoryディレクトリ下に保存します。getAllAvatarDataインターフェースを次に呼び出す際、SDKは新たに追加されたこのデータを解析することができます。

パラメータの説明：
- **rootPath**：Avatar素材のルートディレクトリです。例えば`/var/mobile/Containers/Data/Application/C82F1F7A-01A1-4404-8CF6-131B26B4DA1A/Library/Caches/avatarMotionRes.bundle/avatar_v2.0_male`などです。
- **category**：ダウンロードしたこの設定のカテゴリーです。
- **zipFilePath**：ダウンロードしたZIPパッケージを保存するローカルアドレスです。
- **completion**: 結果のコールバックです。errorはエラーメッセージ、avatarListは解析したavatarデータ配列を表します。

### 7. カスタムイベントの送信
カスタムイベントを送信します。例：顔がない場合のアイドル状態の表示の有効化。
```swift
- (void)sendCustomEvent:(NSString * _Nullable)eventKey eventValue:(NSString * _Nullable)eventValue;
```
- **eventKey**：カスタムイベントのkeyです。TEDefineのAvatarCustomEventKeyを参照できます。
- **eventValue**：カスタムイベントのvalueです。 JSON文字列であり、例えば`@{@"enabel" : @(YES)}をjson文字列に変換するか、または@"{\\"enable\\" : true}"`を直接書き込みます。

### 8. AvatarDataの呼び出し
これらのインターフェースのコアはすべてAvatarDataクラスです。その主な内容は次のとおりです。
```
/// @brief アバター制作設定タイプ
@interface AvatarData : NSObject
/// 例えば、輪郭、目の微調整などです。TEDefineでは標準のcategoryを定義し、それでニーズを満たせない場合はcategory文字列をカスタマイズすることもできます。既存のものと競合しなければそれでよく、空にすることはできません
@property (nonatomic, copy) NSString * _Nonnull category;
// 具体的な各itemまたは各微調整項目を識別します。例えば各眼鏡にはすべて個々のidがあり、各微調整項目にもすべて個々のidがあります。空にすることはできません
@property (nonatomic, copy) NSString * _Nonnull Id;
// selectorタイプまたはAvatarDataTypeSlider値タイプ
@property (nonatomic, assign) AvatarDataType type;
/// selectorタイプの場合は、現在選択されているものの有無を表します
@property (nonatomic, assign) BOOL isSelected;

/// 顔、目、髪、トップス、靴などの体のある部位を制作します。値の設定方法については公式ドキュメントをご参照ください
@property (nonatomic, copy) NSString * _Nonnull entityName;
/// entityNameに対してどの操作(action)を実行するかを表します。 ルールについては公式ドキュメントをご参照ください
@property (nonatomic, copy) NSString * _Nonnull action;
/// entityNameに対して実行するactionの具体的な値を表します。 ルールについては公式ドキュメントをご参照ください
@property (nonatomic, copy) NSDictionary * _Nonnull value;
@end
```

1つのAvatarDataオブジェクトは1つのアトミック設定です（髪型変更、 頬の調整など）。
<table>
<tr>
	<th style="text-align:center">髪型変更</th>
	<th style="text-align:center">頬の調整</th>
</tr>
<tr>
	<td><img src="https://qcloudimg.tencent-cloud.cn/raw/6c7cf2b3775fef1d72d2b95b19af878c.png"></td>
	<td><img src="https://qcloudimg.tencent-cloud.cn/raw/9c4699e9cf0f361a728b76aa34b6486a.png"></td>
</tr>
</table>

- アバター制作の際、データがselectorタイプの場合は、AvatarDataのselectedフィールドを変更します。例えばA、B、C、Dという4種類の眼鏡があり、Aをデフォルトで選択している場合、Aのselectedはtrue、B、C、Dはfalseとなります。ユーザーが眼鏡Bを選択した場合、それはBのselectedをtrueにし、A、C、Dをfalseにすることになります。
- アバター制作の際、データがsliderタイプの場合は、AvatarDataのvalueフィールドを変更します。valueフィールドはJsonObjectであり、その中にはいくつかのkey-valueペアがあります。key-valueの中のvalueをスライダーの値に変更するだけです。

## AvatarDataの高度な説明（参考）
AvatarDataはSDKが素材ルートディレクトリのcustom_configsディレクトリから自動的に解析してアプリケーション層に返します。通常はAvataDataを手動で構築する必要はありません。
AvatarDataの中で、アバター制作において重要な役割を果たすものは[entityName](entityName)、[action](#action)，[value](#value)の3つのフィールドです。これら3つのフィールドの値は、SDKが素材設定を解析する際に自動的に入力されます。多くの場合、この3つのフィールドの意味を理解する必要はありませんが、UI層で表示する際、スライダータイプの場合は、value内のブレンドシェイプkey-valueを解析し、UIの操作と対応させる必要があります。

[](id:entityName)
### entityNameフィールド
アバター制作の際は、どの部位（顔、目、髪、トップス、靴など）を制作するかを明確に指定する必要があります。entityNameフィールドはこれらの体の部位の名前を記述するためのものです。TencentのDemo素材の場合、TencentEffectStudioで素材プロジェクト（xxx.studio）を開くと、このようなリストが表示されます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/06a4860a9b6f1b1cf3350d0dfbfbd68b.png" width=300>
リスト内の各項目がそれぞれ体の部位に対応しています。**命名する際は、その命名がstudioプロジェクトにおいてグローバルで一意であることを確実にする必要があります**。

[](id:action)
### actionフィールド
actionフィールドはentityNameに対してどの操作（action）を実行するかを表します。SDK内では5種類のactionを定義しています。各actionの意味およびvalueの要件は次のとおりです。

| action         | 意味                                                         | value要件                                                    |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| changeColor    | 現在のマテリアルの色を変更します。基本色、放射光色などの色属性が含まれます           | JsonObjectタイプ。入力必須です。下記参照 |
| changeTexture  | 現在のマテリアルのマップを変更します。色のテクスチャマップ、金属の粗さのテクスチャマップ、AOテクスチャマップ、法線テクスチャマップ、放射光テクスチャマップなどが含まれます | JsonObjectタイプ。入力必須です。下記参照 |
| shapeValue     | blendShape値を変更します。通常、顔の細部のブレンドシェイプの微調整に用いられます | JsonObjectタイプ。このうちkeyはブレンドシェイプ名、valueはfloatタイプの値です。入力必須です。下記参照  |
| replace        | サブモデルの置き換え（眼鏡、髪型、衣服などの置き換えなど） | JsonObjectタイプ。内部には新しいサブモデルの3D変換情報、モデルパス、マテリアルパスを記述しています。現在の位置にあるサブモデルを非表示にしたい場合はnullを使用します。下記参照 |
| basicTransform | 位置、回転、ズームを調整します。通常はカメラの遠近、角度の調整に用いることで、モデルの全身と半身アングルの切り替えを実現します | JsonObjectタイプ。入力必須です。下記参照 |

[](id:value)
### valueフィールド
<dx-tabs>
::: actionがchangeColorであるシナリオ
[](id:changeColor)
**設定例**：

```swift
{
		"key": "baseColorFactor",
        "value": [43, 26, 23, 255],
		"subMeshIndex":0,
		"materialIndex":0
}
```
- **key**：入力必須です。現在のマテリアルの色を変更します。基本色、放射光色、その他のカスタム色などの色属性が含まれます。

<br>keyが具体的にどの値をとるかは、現在そのマテリアルを使用しているshaderに関連します。上記のスクリーンキャプチャで使用しているのは内蔵のlit_fadeというshaderであり、そこで定義する基本色の名前はbaseColorFactor、放射光色はemissiveFactorであるため、keyの値はそのどちらかとします。また、マテリアルファイルをテキスト形式で直接開くことも、その中で各色のkey値を確認することもできます。例えばここで使用しているのは`hair.fmaterial`というマテリアルファイルであり、TEStudioプロジェクトディレクトリで見つけて開きます。その内容は次のとおりです。<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/374363dc75275181e05d02a05bb6c2dd.png" width=500>
- **value**：入力必須です。4つの値はそれぞれRGBAです。
- **subMeshIndexおよびmaterialIndex**：[](id:subMeshIndex)任意入力です。このフィールドに入力しない場合、SDKではデフォルト値の0をとります。
	TEStudioでは、Mesh(1つのサブモデルであると理解することができます。例：眼鏡、髪、顔)には一般的にサブMeshは設定されておらず、なおかつ1つのMeshには1つのマテリアルしか存在しません。下図をご覧ください。<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/6c4b6de62f37fb58e74d25ec8b01eaa4.png" width=300>
	<br>一部の比較的複雑なMeshには複数のサブMeshが存在する場合があり、1つのMeshが複数のマテリアルを持つこともあります。下図をご覧ください。<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/736b84897bb2e784ac0a3d0085591829.png" width=300>
	<br>このため、changeColorを行いたい場合は、どのマテリアルのcolorをchangeしたいのかを明確に指示する必要があります。subMeshIndexとmaterialIndexは具体的なマテリアル位置の特定に用います。この2つのindexの値を決定するには、素材プロジェクトディレクトリ下のtemplate.jsonを開き、現在のmeshを見つけ、subMeshConfigs属性を確認する必要があります。例えば“hair”を検索するとhairの設定の位置を特定でき、次のようなsubMesh設定を確認することができます。
	<img src="https://qcloudimg.tencent-cloud.cn/raw/85e39b3f3492b2aed27a67bbd3394c60.png" width=500>
	<br>その後、subMeshIndexとmaterialIndexを組み合わせることで、具体的なマテリアルの位置を特定することができます。
	:::
	::: actionがchangeTextureであるシナリオ
	[](id:changeTexture)
	**設定例**：
```swift
{
	"switchKey": "baseColorEnableTexture",
	"switchValue": true,
	"key": "baseColorMap",
	"value": "0622-1/Images/face_tex_base_3.png",
	"subMeshIndex":0,
	"materialIndex":0,
	"textureOptions": {
            "wrapS": "REPEAT",
            "wrapT": "REPEAT",
            "magFilter": "LINEAR",
            "minFilter": "LINEAR_MIPMAP_LINEAR",
            "sRGB": false,
            "mipmap": true,
            "samplerType": "SAMPLER_2D"
         }
}
```

- **switchKeyおよびswitchValue**：入力必須です。マップを表示するかどうかを制御します。switchValueがfalseの場合はマップテクスチャを設定しないことを表し、この場合は他のフィールドに入力しなくても結構です。switchKeyの値とkeyの値は組み合わせて使用する必要があります。
- **keyおよびvalue**：switchValueがtrueの場合、これら2つのフィールドは入力必須です。valueの値はマップファイルの素材ルートディレクトリに対する相対パス（設定例をご覧ください）、もしくはスマートフォン上の絶対パスとします。
>? [action ==  changeColor](#changeColor)の場合のkey値の説明と同様に、switchKeyとkeyはmaterialが使用しているshaderに関連します。例えばTEStudio内の内蔵shaderの「色テクスチャ」のオンオフおよび値に対応するのは、ここのbaseColorEnableTextureとbaseColorMapです。AOテクスチャ、法線テクスチャなどのフィールドも同様です。Tencentの公式アバター制作素材ではshaderのカスタマイズも提供しており、リップマップのオンオフ、顔ステッカーのオンオフなどを追加しています。
>- マテリアルファイルはテキスト形式で直接開くことができ、その中で各マップのswitchKeyおよびkey値を確認できます。例えばDemoの素材の中のface_mainで使用するマテリアルファイルface.fmaterialを開くと、次の内容を確認することができます。
><img src="https://qcloudimg.tencent-cloud.cn/raw/0fa0653a62172412aba16b64d1bc172f.png" width=500>
>- <br>何かのマップを変更したい場合は、そのマップに対応する値をswitchKeyとkeyの2つのフィールドに入力します。

- **subMeshIndexおよびmaterialIndex**：任意入力です。このフィールドに入力しない場合、SDKではデフォルト値の0をとります。詳細な説明については[action ==  changeColor](#subMeshIndex)の説明をご参照ください。
- **textureOptions**：任意入力です。マップ解析パラメータです。マップの展開およびレンダリングのスタイルを決定します。特別な設定が必要な場合を除き、このフィールドへの入力はお勧めしません。
:::
::: actionがshapeValueであるシナリオ
[](id:shapeValue)
**設定例**
```
{
	"chin_length": 0.0,
	"cheek_width": 0.0,
	"chin_width": 0.0
}
```
それぞれブレンドシェイプ名とブレンドシェイプ値です。ブレンドシェイプ名については[素材設計仕様](https://doc.weixin.qq.com/doc/w3_ALoA-gYYAAgV0MAAbjtQfO4EWXhI9?scode=AJEAIQdfAAoU7K9sLCAGMA3QZFAAg&version=4.0.19.6020&platform=win)をご参照ください。ブレンドシェイプ値は-1.0～1.0の間の値とします。
:::
::: actionがreplaceであるシナリオ
[](id:replace)
action == replaceの場合のvalueフィールドにはサブモデルの3D変換情報、モデルパス、マテリアルパスを記述しています。各モデルのこれらの情報は素材ルートディレクトリのtemplate.jsonから見つけることができます。
**設定例**：
```
{
	"position": {
		"x": -0.424766392,
		"y": -29.969169617,
		"z": -25.769769669
	},
	"rotation": {
		"x": 0,
		"y": 0,
		"z": 0
	},
	"scale": {
		"x": 1,
		"y": 1,
		"z": 1
	},
	"meshResourceKey": "meshFolder/glass_A.fmesh",
	"subMeshConfigs": [{
		"materialResourceKeys": ["/sdcard/xmagic_res/glass_red.fmaterial"]
	}，{
		"materialResourceKeys": ["/sdcard/xmagic_res/test1.fmaterial","/sdcard/xmagic_res/test2.fmaterial"]
	}]
}
```
- **position、rotation、scale**：モデルの位置、回転、ズーム属性をそれぞれ記述したものです。任意入力です。入力しない場合はデフォルト値を使用します。positionのデフォルト値は0,0,0、rotationのデフォルト値は0,0,0、scaleのデフォルト値は1,1,1です。
>! rotationの単位は角度であり、例えば45度の場合は45と入力します。これは素材template.json内のeEulerフィールドの値に対応します。
- **meshResourceKey**：入力必須です。モデルのmeshファイルのパスを記述したものです。パスはmeshファイルの素材ルートディレクトリに対する相対パス（設定例をご覧ください）とすることも、ファイルのスマートフォン上の絶対パスとすることもできます。
-  **subMeshConfigs**：入力必須です。[subMeshIndexおよびmaterialIndex](#subMeshIndex)についての説明のように、1つのmeshには複数のsubMeshを含めることができ、1つのsubMeshにも複数のマテリアルを含めることができます。subMeshConfigsフィールドの設定はmeshとマテリアルのバインド関係です。materialResourceKeys内の値はmaterialファイルの素材ルートディレクトリに対する相対パス（設定例をご覧ください）とすることも、ファイルのスマートフォン上の絶対パスとすることもできます。
:::
::: actionがbasicTransformであるシナリオ
**設定例**：
```swift
{
	"position": {
		"x": -0.424766392,
		"y": -29.969169617,
		"z": -25.769769669
	},
	"rotation": {
		"x": 0,
		"y": 0,
		"z": 0
	},
	"scale": {
		"x": 1,
		"y": 1,
		"z": 1
	}
}
```
位置、回転、ズームの調整に用います。通常はカメラの遠近、角度の調整に用いることで、モデルの全身と半身アングルの切り替えを実現します。position、rotation、scaleフィールドの説明については、[actionがreplaceであるシナリオ](#replace)をご参照ください。
:::
</dx-tabs>

## Avatar制作・着せ替えデータの設定

Avatar属性設定はresourcesフォルダ下に配置します（パス：`素材/custom_configs/resources`）。
![](https://qcloudimg.tencent-cloud.cn/raw/fcc5d2d5173afe13008b8369c63b1a32.png)

これらの設定ファイルは自動生成されるため、通常は手動で設定する必要はありません。自動生成の方法は次のとおりです。
設計者はTencentEffectStudioを使用してキャラクターのセットを設計後、Tencentの提供するresource_generator_guiというapp（現在はMacOSプラットフォームのみサポートしています）を実行するだけでこの設定を自動生成できます。詳細については[設計仕様](https://doc.weixin.qq.com/doc/w3_ALoA-gYYAAgV0MAAbjtQfO4EWXhI9?scode=AJEAIQdfAAoU7K9sLCAGMA3QZFAAg&version=4.0.19.6020&platform=win)をご参照ください。



