
CSSのポルノ検出をアクティブ化するには、まずCSSスクリーンキャプチャ機能をアクティブにする必要があります。[CSSコンソール](https://intl.cloud.tencent.com/document/product/267/31072)  またはCSSスクリーンキャプチャポルノ検出APIを介してアクティブにすることができます。本ページでは、主にCSSスクリーンキャプチャポルノ検出APIを介したCSSポルノ検出機能の実現方法について説明します。

## CSSポルノ検出のアクティブ化
CSSポルノ検出は、CSSスクリーンキャプチャに基づくため、CSSポルノ検出のアクティブ化には、CSSスクリーンキャプチャ機能のアクティブ化が必要です。具体的な操作は次のとおりです。

### 1. ポルノ検出機能を付帯するCSSスクリーンキャプチャテンプレートの作成
[CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834)を呼び出し、PornFlag = 1と設定することによって、ポルノ検出機能を備えたCSSスクリーンキャプチャテンプレートを作成します。

### 2. ポルノ検出機能を付帯するCSSスクリーンキャプチャルールの作成
[CreateLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30835)を呼び出し、ポルノ検出機能を付帯するCSSスクリーンキャプチャルールを作成するには、第1ステップで作成したCSSスクリーンキャプチャテンプレートIDをポルノ検出が必要なライブストリーミングAppId、DomainName、AppName、StreamNameにバインドします。

### 3. CSSを開始し、ポルノ検出を開始
ポルノ検出機能を付帯するCSSスクリーンキャプチャルールを作成した後、新たに開始するCSSでは自動的にポルノ検出機能が開始されます。現在ライブストリーミング中のストリームに、CSSのポルノ検出を開始したい場合は、ライブストリーミングを停止、再開して、この機能の開始を有効にする必要があります。

## CSSポルノ検出結果の取得
CSSポルノ検出機能をアクティブにした後、ポルノ検出コールバックテンプレートで登録するコールバックドメイン名を設定すれば、CSSバックエンドからポルノ検出結果がコールバックされます。
>! デフォルトでは疑わしい結果に対してのみコールバックを行い、通常の結果にはコールバックを行いません。

### 1. CSSポルノ検出コールバックテンプレートの作成
[CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815)を呼び出し、PornCensorshipNotifyUrl パラメータをお客様のドメイン名として設定し、CSSポルノ検出コールバックテンプレートを作成します。
### 2. CSSポルノ検出コールバックルールの作成

[CreateLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30816)を呼び出し、ポルノ検出機能を付帯するCSSスクリーンキャプチャルールを作成するには、直前のステップで作成したCSSスクリーンキャプチャテンプレートIDをポルノ検出が必要なライブストリーミングAppId、DomainName、AppNameにバインドします。

### 3. ポルノ検出結果の取得
CSSのバックエンドは、HTTP POSTリクエストを介して登録されたドメイン名にポルノ検出結果を送信します。ポルノ検出結果はJSON 形式でHTTP Bodyに保存されます。ライブストリーミングがポルノであるかどうかは、typeフィールドのみで判断できます。
>!画像の`type`を使用してポルノ画像かどうかを判断することを推奨しますが、検出システムの判断は100%の精度を保証できないため、ポルノ疑い有無の認識が正確でない場合もございます。したがって目視による再確認を行うことをお勧めします。  

#### 完全なプロトコルは次のとおりです。
| パラメータ | 入力必須の有無 | データタイプ | 説明 |
| --- | --- | --- | --- |
| tid | 入力必須 | Number | 予備警告ポリシーID、ビデオコンテンツの予備警告：20001 |
| streamId | オプション | String | ストリーム名 |
| channelId | オプション | string | チャネルID |
| img | 入力必須 | string | 予備警告画像リンク |
| type | 入力必須 | Array | 画像タイプ、0：通常の画像、1 - 5：不適切な画像 |
| confidence | 入力必須 | Number | ポルノ信頼度、範囲 0-100；normalScore、 hotScore、 pornScore の総合スコア |
| normalScore | 入力必須 | Number | 画像がノーマルな画像である評点 |
| hotScore | 入力必須 | Number | 画像がセクシー画像である評点 |
| pornScore | 入力必須 | Number | 画像がポルノ画像である評点 |
| level | オプション | Number | 画像のレベル |
| ocrMsg | オプション | string | 画像のOCR識別情報（該当する場合） |
| screenshotTime | 入力必須 | Number | スクリーンキャプチャ時間 |
| sendTime | 入力必須 | Number | リクエスト送信時間、UNIXタイムスタンプ |
| gameDetails | オプション| Object |  ゲームの詳細情報  |
| similarScore  | オプション| Number | 画像の類似度の評点|
| stream_param  | オプション| String | プッシュパラメータ |
| app  | オプション| String | プッシュドメイン名 |
| appid  | オプション| Number | 業務ID  |
| appname  | オプション| String | プッシュpathパス  |


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
HTTP Body:
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
            
    "sendTime":1575513176,
            
    "similarScore":0,
            
    "tid":20001,
            
    "streamId":"teststream",
            
    "channelId":"teststream",
            
    "stream_param":"txSecret=40f38f69f574fd51126c421a3d96c374&txTime=5DEBEC80",
            
    "app":"testlive.myqcloud.com",
            
    "appname":"live",
            
    "appid":10000
}  
```

## CSSポルノ検出の停止

CSSポルノ検出を停止するには、スクリーンキャプチャルールを削除するか、またはスクリーンキャプチャテンプレートを変更します。削除と変更操作は新たなCSSに対してのみ有効です。すでに開始されているCSSにつき、ポルノ検出を停止したい場合は、ライブストリーミングを停止、再開して、この機能の停止を有効にする必要があります。

### 1. ポルノ検出スクリーンキャプチャルールの削除による停止

[DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833)を呼び出し、テンプレートIDを介してDomainName、 AppName、StreamNameに対応するCSSスクリーンキャプチャ仕様を削除します。

### 2. ポルノ検出スクリーンキャプチャテンプレートの削除または修正による停止

[ModifyLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30828)を呼び出し、CSSテンプレートのポルノ検出表示を0にします。
