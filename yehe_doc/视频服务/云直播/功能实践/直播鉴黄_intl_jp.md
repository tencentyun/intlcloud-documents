
LVBのポルノ検出をアクティブにするには、まずLVBスクリーンキャプチャ機能をアクティブにする必要があります。[LVBコンソール](https://intl.cloud.tencent.com/zh/document/product/267/31072) またはLVBスクリーンキャプチャポルノ検出APIを介してアクティブにすることができます。ここでは、主にLVBスクリーンキャプチャポルノ検出APIを介したLVBポルノ検出機能の実現方法について説明します。

## LVBポルノ検出のアクティブ化
LVBポルノ検出は、LVBスクリーンキャプチャに基づくため、LVBポルノ検出のアクティブ化には、LVBスクリーンキャプチャ機能のアクティブ化が必要です。具体的な操作は次のとおりです。

### 1. ポルノ検出機能を付帯するLVBスクリーンキャプチャテンプレートの作成
[CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834)を呼び出し、PornFlag = 1の設定で、ポルノ検出機能を付帯するLVBスクリーンキャプチャテンプレートを作成します。

### 2. ポルノ検出機能を付帯するLVBスクリーンキャプチャルールの作成
[CreateLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30835)を呼び出し、ポルノ検出機能を付帯するLVBスクリーンキャプチャルールを作成するには、第1ステップで作成したLVBスクリーンキャプチャテンプレートIDをポルノ検出が必要なライブストリーミングAppId、DomainName、AppName、StreamNameに関連付けます。

### 3. LVBを開始し、ポルノ検出を開始
ポルノ検出機能を付帯するLVBスクリーンキャプチャルールを作成した後、新たに開始するLVBでは自動的にポルノ検出機能が開始されます。現在ライブストリーミング中のストリームに、LVBのポルノ検出を開始したい場合は、ライブストリーミングを停止、再開して、この機能の開始を有効にする必要があります。

## LVBポルノ検出結果の取得
LVBポルノ検出機能をアクティブにした後、ポルノ検出コールバックテンプレートで登録するコールバックドメイン名を設定すれば、LVBバックエンドからポルノ検出結果がコールバックされます。
>! デフォルトでは疑わしい結果に対してのみコールバックを行い、通常の結果にはコールバックを行いません。

### 1. LVBポルノ検出コールバックテンプレートの作成
[CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815)を呼び出し、PornCensorshipNotifyUrl パラメータをお客様のドメイン名として設定し、LVBポルノ検出コールバックテンプレートを作成します。
### 2. LVBポルノ検出コールバックルールの作成

[CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816)を呼び出し、ポルノ検出機能を付帯するLVBスクリーンキャプチャルールを作成するには、直前のステップで作成したLVBスクリーンキャプチャテンプレートID をポルノ検出のコールバックが必要なライブストリーミングAppId、DomainName、AppNameに関連付けます。

### 3. ポルノ検出結果の取得
LVBのバックエンドは、HTTP POSTリクエストを介して登録されたドメイン名にポルノ検出結果を送信します。ポルノ検出結果はJSON 形式でHTTP Bodyに保存されます。ライブストリーミングがポルノであるかどうかは、typeフィールドのみで判断できます。
>!画像の`type`を使用してポルノ画像かどうかを判断することを推奨しますが、検出システムの判断は100%の精度を保証できないため、少数ながらポルノの疑いがあると識別された画像の識別結果が正しくない場合があります。したがって目視による再確認を行うことをお勧めします。  

#### 完全なプロトコルは次のとおりです。
| **パラメータ** | **入力必須の有無** | **データタイプ** | **説明**                                                     |
| --- | --- | --- | --- |
| tid | 入力必須 | Number | 予備警告ポリシーID、ビデオコンテンツの予備警告：20001 |
| streamId | オプション | String | ストリーム名 |
| channelId | オプション | string | チャネルID |
| img | 入力必須 | string | 予備警告画像リンク |
| type | 入力必須 | Array | 画像タイプ、 0 ：通常の画像、 1 ：ポルノ画像、 2 ：セクシー画像、 3 ：政治関連画像、 4 ：違法な画像、 5 ：テロ関連画像 、6 - 9 ：その他画像 |
| confidence | 入力必須 | Number | ポルノ信頼度、範囲 0-100；normalScore、 hotScore、 pornScore の総合スコア |
| normalScore | 入力必須 | Number | 画像がノーマルな画像である評点 |
| hotScore | 入力必須 | Number | 画像がセクシー画像である評点 |
| pornScore | 入力必須 | Number | 画像がポルノ画像である評点 |
| level | オプション | Number | 画像のレベル |
| ocrMsg | オプション | string | 画像のOCR識別情報（該当する場合） |
| screenshotTime | 入力必須 | Number | スクリーンキャプチャ時間 |
| sendTime | 入力必須 | Number | リクエスト送信時間、UNIXタイムスタンプ |
| abductionRisk | オプション | Array | AbductionRisk構造を含む配列 |
| faceDetails | オプション| Array | 人の顔の属性faceDetailの構造を含む配列 |
| gameDetails | オプション| Object |  ゲームの詳細情報  |
| polityScore | オプション| Number | 画像が政治関連である評点|
| illegalScore |  オプション| Number  | 画像が違法である評点 |
| terrorScore  | オプション| Number  | 画像がテロ関連である評点|
| similarScore  | オプション| Number | 画像の類似度の評点|
| stream_param  | オプション| String | プッシュパラメータ |
| app  | オプション| String | プッシュドメイン名 |
| appid  | オプション| Number | 業務ID  |
| appname  | オプション| String | プッシュpathパス  |



#### AbductionRisk の紹介：

| **パラメータ** | **入力必須の有無** | **データタイプ** | **説明** |
| --- | --- | --- | --- |
| level | 入力必須 | Number  | リスクレベルの範囲0 - 4、数字が大きいほどリスクも高くなり、3と4は悪意を表しますので、対処することをお勧めします |
| type | 入力必須 | Number | リスクタイプ、20002：ポルノ  |

#### faceDetail説明：
| **パラメータ名** | **入力必須の有無** | **タイプ** | **説明** |
| --- | --- | --- | --- |
| gender | オプション| Number | 性別 [0(female) - 100(male)] |
| age | オプション| Number | 年齢 |
| expression | オプション| Number | 微笑 [0(normal) - 50(smile) - 100(laugh)] |
| beauty | オプション| Number | 魅力 [0 - 100] |
| x | オプション| Number | FaceBox左上角 x |
| y | オプション| Number | FaceBox左上角 y |
| width | オプション| Number | FaceBox幅 |
| height | オプション| Number | FaceBox高さ |

#### gameDetails説明：
| **パラメータ名** | **入力必須の有無** | **タイプ** | **説明** |
| --- | --- | --- | --- |
| battlegrounds | オプション | Object | BATTLEGROUNDSの情報 |
| gameList | オプション| Array | ゲームリスト |

#### gameList説明：

| **パラメータ名** | **入力必須の有無** | **タイプ** | **説明** |
| --- | --- | --- | --- |
| name | オプション| String | ゲーム名 |
| confidence | オプション| Number | 確率 |


#### リクエスト例
HTTP Body：
```
{
    "ocrMsg":"",
		
    "type":[2],
		
    "confidence":0,
		
    "normalScore":2,
		
    "hotScore":97,
		
    "pornScore":0,
		
    "screenshotTime":1575513174,
		
    "level":0,
		
    "img":"http://test-10000.cos.ap-shanghai.myqcloud.com/2019-12-05/teststream-screenshot-10-32-54-960x540.jpg",
		
    "abductionRisk":[ ],
		
    "faceDetails":[ ],
		
    "sendTime":1575513176,
		
    "illegalScore":0,
		
    "polityScore":0,
		
    "similarScore":0,
		
    "terrorScore":0,
		
    "tid":20001,
		
    "streamId":"teststream",
		
    "channelId":"teststream",
		
    "stream_param":"txSecret=40f38f69f574fd51126c421a3d96c374&txTime=5DEBEC80",
		
    "app":"testlive.myqcloud.com",
		
    "appname":"live",
		
    "appid":10000
}  
```

## LVBポルノ検出の停止

LVBポルノ検出を停止するには、スクリーンキャプチャルールを削除するか、またはスクリーンキャプチャテンプレートを変更します。すべての削除と変更操作は新たなLVBの対してのみ有効です。すでに開始されているLVBにつき、ポルノ検出を停止したい場合は、ライブストリーミングを停止、再開して、この機能の停止を有効にする必要があります。

### 1. ポルノ検出スクリーンキャプチャルールの削除による停止

[DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833)を呼び出し、テンプレート IDを介してDomainName、 AppName、StreamNameの対応するLVBスクリーンキャプチャ仕様を削除します。

### 2. ポルノ検出スクリーンキャプチャテンプレートの削除または修正による停止

[ModifyLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30828)を呼び出し、LVBテンプレートのポルノ検出表示を0に修正します。