
CSSのポルノ検出をアクティブ化するには、まずCSSスクリーンキャプチャ機能をアクティブにする必要があります。[CSSコンソール](https://intl.cloud.tencent.com/document/product/267/31072)  またはCSSスクリーンキャプチャポルノ検出APIを介してアクティブにすることができます。本ページでは、主にCSSスクリーンキャプチャポルノ検出APIを介したCSSポルノ検出機能の実現方法について説明します。

## CSSポルノ検出のアクティブ化
CSSポルノ検出は、CSSスクリーンキャプチャに基づくため、CSSポルノ検出のアクティブ化には、CSSスクリーンキャプチャ機能のアクティブ化が必要です。具体的な操作は次のとおりです。

### 1. ポルノ検出機能を付帯するCSSスクリーンキャプチャテンプレートの作成
[CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834)を呼び出し、PornFlag = 1と設定することによって、ポルノ検出機能を備えたCSSスクリーンキャプチャテンプレートを作成します。

### 2. ポルノ検出機能を付帯するCSSスクリーンキャプチャルールの作成
[CreateLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30835)を呼び出し、ポルノ検出機能を付帯するCSSスクリーンキャプチャルールを作成するには、第1ステップで作成したCSSスクリーンキャプチャテンプレートIDをポルノ検出が必要なライブストリーミングAppId、DomainName、AppName、StreamNameに関連付けます。

### 3. CSSを開始し、ポルノ検出を開始
ポルノ検出機能を付帯するCSSスクリーンキャプチャルールを作成した後、新たに開始するCSSでは自動的にポルノ検出機能が開始されます。現在ライブストリーミング中のストリームに、CSSのポルノ検出を開始したい場合は、ライブストリーミングを停止、再開して、この機能の開始を有効にする必要があります。

## CSSポルノ検出結果の取得
CSSポルノ検出機能をアクティブにした後、ポルノ検出コールバックテンプレートで登録するコールバックドメイン名を設定すれば、CSSバックエンドからポルノ検出結果がコールバックされます。
>! デフォルトでは疑わしい結果に対してのみコールバックを行い、通常の結果にはコールバックを行いません。

### 1. CSSポルノ検出コールバックテンプレートの作成
[CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815)を呼び出し、PornCensorshipNotifyUrl パラメータをお客様のドメイン名として設定し、CSSポルノ検出コールバックテンプレートを作成します。
### 2. CSSポルノ検出コールバックルールの作成

[CreateLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30816)を呼び出し、ポルノ検出機能を付帯するCSSスクリーンキャプチャルールを作成するには、直前のステップで作成したCSSスクリーンキャプチャテンプレートIDをポルノ検出が必要なライブストリーミングAppId、DomainName、AppNameに関連付けます。

### 3. ポルノ検出結果の取得
CSSのバックエンドは、HTTP POSTリクエストを介して登録されたドメイン名にポルノ検出結果を送信します。ポルノ検出結果はJSON 形式でHTTP Bodyに保存されます。ライブストリーミングがポルノであるかどうかは、typeフィールドのみで判断できます。
>!画像の`type`を使用してポルノ画像かどうかを判断することを推奨しますが、検出システムの判断は100%の精度を保証できないため、ポルノ疑い有無の認識が正確でない場合もございます。したがって目視による再確認を行うことをお勧めします。  

#### 完全なプロトコルは次のとおりです。
| パラメータ        | 入力必須の有無        | データタイプ         | 説明        |
| -------- | -------- | -------- | -------- |
| streamId    | オプション     | String | ストリーム名     |
| channelId      | オプション     | string   | チャネルID      |
| img     | 入力必須     | string   | 予備警告画像リンク      |
| type    | 入力必須     | Array    | 検出結果で優先度が最も高い悪意のあるタグに対応する分類値のことです。具体的な意味については、パラメータlabelによって返される補足テキストの説明を参照することができます |
| score       | 入力必須     | Array    | type 対応する評点   |
| ocrMsg      | オプション     | string   | 画像のOCR認識情報（該当する場合）       |
| suggestion     | 入力必須     | string   | 推奨値。値はオプション： <ul style="margin:0"><li/>Block：ブロック<li/>Review：レビュー待ち<li/>Pass：正常</ul> |
| label       | 入力必須     | string   | このフィールドは、検出結果(LabelResults)において対応する優先度が最も高い悪意のあるタグを返すために使用され、モデルが推奨するレビュー結果を表します。業務上のニーズに応じて、それぞれの不正タイプと推奨値を処理することをお勧めします |
| subLabel    | 入力必須     | string   | このフィールドは、検出結果でヒットした最も優先度が高い悪意のあるタグの下にあるサブタグの名前を返すために使用されます。例えば、ポルノ--性行為で、サブタグがヒットしない場合は、空の文字列が返されます |
| labelResults   | オプション     | [Array of LabelResult](#labelresult)   | このフィールドは、分類モデルによってヒットした悪意のあるタグの詳細な識別結果を返すために使用されます。これには、ポルノや広告といった好ましくない、安全ではない、または不適切なコンテンツタイプの識別結果が含まれます<br>注意：**このフィールドは、有効な値が取得できなかったことを意味するnullを返す場合があります** |
| objectResults  | オプション     | [Array of ObjectResult](#objectresult) | このフィールドは、オブジェクト検出モデルの詳細な検出結果を返すために使用されます。これには、エンティティ、広告ロゴ、2次元コードなどのコンテンツでヒットしたタグ名、タグスコア、座標情報、シーン識別結果、推奨される操作といったコンテンツ識別情報が含まれます。詳細な戻り値の情報については、対応するデータ構造(ObjectResults)の説明をご参照ください<br> 注意：**このフィールドは、有効な値が取得できなかったことを意味するnullを返す場合があります** |
| ocrResults     | オプション     | [Array of OcrResult](#ocrresult)    | このフィールドは、OCRテキスト識別の詳細な検出結果を返すために使用されます。これには、テキスト座標情報、テキスト識別結果、推奨される操作といったコンテンツ識別情報が含まれます。詳細な戻り値の情報については、対応するデータ構造(ObjectResults)の説明をご参照ください<br> 注意：**このフィールドは、有効な値が取得できなかったことを意味するnullを返す場合があります** |
| libResults     | オプション     | [Array of LibResult](#libresult)    | リスクライブラリのレビュー結果  |
| screenshotTime | 入力必須     | Number | スクリーンキャプチャ時間 |
| sendTime    | 入力必須     | Number | リクエスト送信時間、UNIXタイムスタンプ |
| stream_param  | オプション     | String | プッシュパラメータ |
| app     | オプション     | String | プッシュドメイン名 |
| appid       | オプション     | Number | 業務ID |
| appname     | オプション     | String | プッシュpathパス |

 

#### LabelResult
分類モデルのヒット結果。

| 名称   | タイプ  | 説明    |
| ---------- | ------------------------ | ------------------------ |
| Scene      | String      | 広告、ポルノ、有害なコンテンツのシーンなど、モデルによって識別されたシーンの結果を返します。     |
| Suggestion | String      | 現在の悪意のあるタグに対する後続操作の提案を返します。 判定結果が得られた後の戻り値はシステムが推奨する後続操作を表示します。業務上のニーズに応じて、各不正のタイプと推奨値に対処することをお勧めします。 戻り値：<ul style="margin:0"><li/>Block：ブロックを推奨<li/>Review ：手動レビューを推奨<li/>Pass：承認を推奨</ul> |
| label | String      | このフィールドは、検出結果に対応する悪意のあるタグを返すために使用されます |
|| SubLabel   | String | サブタグ名|
| Score      | Integer | このタグモデルでヒットするスコア    |
| Details    | Array of [LabelDetailItem](#labeldetailitem) | 分類モデルでヒットするサブタグの詳細な結果     |

#### LabelDetailItem

分類モデルでヒットするサブタグの結果。

| 名称 | タイプ | 説明|
| -------- | -------- | ----- |
| Id    | Integer  | 番号   |
| Name     | String   | サブタグ名     |
| Score    | Integer  | サブタグスコア。値の範囲は0ポイント～100ポイント|


#### ObjectResult

エンティティの検出結果の詳細。

| 名称   | タイプ              | 説明              |
| ---------- | --------------------- | --------------------- |
| Scene      | String   | 2次元コード、ロゴ、画像OCRのシーンなど、エンティティによって識別されたエンティティシーンの結果を返します。 |
| Suggestion | String   | 現在の悪意のあるタグに対する後続操作の提案を返します。判定結果が得られた後の戻り値は、システムが推奨する後続操作を表します。業務上のニーズに応じて、それぞれの不正タイプと推奨値を処理することをお勧めします。 戻り値：<ul style="margin:0"><li/>Block：ブロックを推奨<li/>Review ：手動レビューを推奨<li/>Pass：承認を推奨</ul> |
| label | String   | このフィールドは、検出結果に対応する悪意のあるタグを返すために使用されます |
| SubLabel   | String             | サブタグ名 |
| Score    | Integer | 該当するシーンモデルでヒットするサブタグのスコア。値の範囲は0ポイント～100ポイント|
| Names      | Array of String    | エンティティ名リスト |
| Details    | Array of [ObjectDetail](#objectdetail) | エンティティ検出結果の詳細 |

#### ObjectDetail

エンティティ検出結果の詳細で、検出シーンがエンティティ、広告ロゴ、2次元コードである場合、モデル検出対象フレームのタグ名、タグ値、タグスコアおよび検出フレームの位置情報を表します。

| 名称     | タイプ     | 説明    |
| -------- | -------- | -------- |
| Id    | Integer    | このパラメータは、識別や区別を容易にするために、識別されたオブジェクトのIDを返すために使用されます    |
| Name     | String     | このパラメータは、ヒットのエンティティタグを返すために使用されます   |
| Value    | String     | このパラメータは、対応するエンティティタグに対応する値またはコンテンツを返すために使用されます。例えば、タグが2次元コード(QrCode)の場合、このフィールドは識別された2次元コードに対応するURLアドレスになります |
| Score    | Integer    | このパラメータは、対応するエンティティタグのスコアを返すために使用され、値は0～100です。例えば、QrCode 99は、対応する識別コンテンツが2次元コードシーンタグにヒットする確率が非常に高いことを意味します |
| Location | [Location](#location) | このフィールドは、エンティティ検出フレームの座標位置（左上隅のxy座標、長さと幅、回転角度）を返すために使用され、エンティティの関連情報の素早い配置を容易にします |

#### Location

座標。

| 名称      | タイプ     | 説明    |
| -------- | -------- | ---------------- |
| X     | Float    | 左上隅の横軸     |
| Y     | Float    | 左上隅の縦軸     |
| Width    | Float    | 幅      |
| Height   | Float    | 高さ      |
| Rotate   | Float    | 検出フレームの回転角度 |

#### OcrResult

OCR検出結果の詳細です。

| 名称   | タイプ  | 説明   |
| ---------- | ---------------------- | ---------------------- |
| Scene      | String     | 識別シーンを表します。デフォルト値はOCR（画像OCR認識）です。    |
| Suggestion | String     | 優先度が最も高い悪意のあるタグに対応する後続操作の提案を返します。判定結果が得られた後の戻り値は、システムが推奨する後続操作を表します。業務上のニーズに応じて、それぞれの不正タイプと推奨値を処理することをお勧めします。 戻り値：<ul style="margin:0"><li/>Block：ブロックを推奨<li/>Review ：手動レビューを推奨<li/>Pass：承認を推奨</ul> |
| label | String     | このフィールドは、検出結果に対応する悪意のあるタグを返すために使用されます |
| SubLabel   | String             | サブタグ名 |
| Score    | Integer | 該当するシーンモデルでヒットするサブタグのスコア。値の範囲は0ポイント～100ポイント|
| Text    | String | テキストコンテンツ |
| Details    | Array of [OcrTextDetail](#ocrtextdetail) | OCR 結果の詳細 |


#### OcrTextDetail
OCRテキスト結果の詳細です。

| 名称 | タイプ     | 説明  |
| -------- | --------------- | --------------- |
| Text     | String     | OCRで識別されたテキストコンテンツを返します（OCRテキスト識別の上限は** 5000バイト以内**です） 。 |
| label | String     | このフィールドは、検出結果に対応する悪意のあるタグを返すために使用されます |
| Keywords | Array of String | このタグでヒットしたキーワード |
| Score    | Integer      | 該当するタグモデルでヒットするスコア。値の範囲は0ポイント～100ポイント |
| Location | [Location](#location) | OCR テキスト座標位置 |


#### LibResult
ブラック/ホワイトライブラリ結果の詳細です。

| 名称   | タイプ    | 説明     |
| ---------- | ------------------ | ------------------ |
| Scene      | String      | モデルのシーン識別結果を表します。デフォルト値はSimilarです。    |
| Suggestion | String      | 後続操作の提案を返します。判定結果が得られた後の戻り値は、システムが推奨する後続操作を表します。業務上のニーズに応じて、それぞれの不正タイプと推奨値を処理することをお勧めします。 戻り値：<ul style="margin:0"><li/>Block：ブロックを推奨<li/>Review ：手動レビューを推奨<li/>Pass：承認を推奨</ul> |
| label | String      | このフィールドは、検出結果に対応する悪意のあるタグを返すために使用されます |
| SubLabel   | String      | サブタグ名 |
| Score      | Integer     | 画像検索モデル認識スコア。値の範囲は0ポイント～100ポイント |
| Details    | Array of [ObjectDetail](#objectdetail) | ブラック/ホワイトライブラリ結果の詳細 |

#### LibDetail
カスタマイズコーパス/ブラック/ホワイトライブラリの詳細です。

| 名称      | タイプ     | 説明    |
| -------- | -------- | ------------------ |
| Id    | Integer  | 番号    |
| ImageId  | String   | 画像ID    |
| label | String  | このフィールドは、検出結果に対応する悪意のあるタグを返すために使用されます |
| Tag      | String   | カスタムタグ|
| Score    | Integer  |モデル認識スコア。値の範囲は0ポイント～100ポイント    |



#### コールバックメッセージの例
<dx-codeblock>
::: HTTPbody  json
{
        "ocrMsg": "",
        "type": [1],
        "socre": 99,
        "screenshotTime": 1610640000,
        "level": 0,
        "img": "http://1.1.1.1/download/porn/test.jpg",
        "abductionRisk": [],
        "faceDetails": [],
        "sendTime": 1615859827,
        "suggestion": "Block",
        "label": "Porn",
        "subLabel": "PornHigh",
        "labelResults": [{
                "HitFlag": 0,
                "Scene": "Illegal",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }, {
                "HitFlag": 1,
                "Scene": "Porn",
                "Suggestion": "Block",
                "Label": "Porn",
                "SubLabel": "PornHigh",
                "Score": 99,
                "Details": [{
                        "Id": 0,
                        "Name": "PornHigh",
                        "Score": 99
                }, {
                        "Id": 1,
                        "Name": "WomenChest",
                        "Score": 99
                }]
        }, {
                "HitFlag": 0,
                "Scene": "Sexy",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "Terror",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }],
        "objectResults": [{
                "HitFlag": 0,
                "Scene": "QrCode",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "MapRecognition",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "PolityFace",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }],
        "ocrResults": [{
                "HitFlag": 0,
                "Scene": "OCR",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Text": "",
                "Details": []
        }],
        "streamId": "teststream",
        "channelId": "teststream",
        "stream_param": "txSecret=40f38f69f574fd51126c421a3d96c374&txTime=5DEBEC80",
        "app": "5000.myqcloud.com",
        "appname": "live",
        "appid": 10000,
        "event_type": 317,
        "sign": "ac920c3e66**********78cf1b5de2c63",
        "t": 1615860427
}
:::
</dx-codeblock>



## CSSポルノ検出の停止

CSSポルノ検出を停止するには、スクリーンキャプチャルールを削除するか、またはスクリーンキャプチャテンプレートを変更します。削除と変更操作は新たなCSSの対してのみ有効です。すでに開始されているCSSにつき、ポルノ検出を停止したい場合は、ライブストリーミングを停止、再開して、この機能の停止を有効にする必要があります。

### 1. ポルノ検出スクリーンキャプチャルールの削除による停止

[DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833)を呼び出し、テンプレートIDを介してDomainName、 AppName、StreamNameに対応するCSSスクリーンキャプチャ仕様を削除します。

### 2. ポルノ検出スクリーンキャプチャテンプレートの削除または修正による停止

[ModifyLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30828)を呼び出し、CSSテンプレートのポルノ検出表示を0にします。
