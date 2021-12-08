
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
| ---------- | ---------- | ---------- | --------------------------- |
| streamId | オプション     | String | ストリーム名 |
| channelId | オプション     | string | チャネルID |
| img | 入力必須     | string | 予備警告画像リンク |
| type | 入力必須      | Array | 検出結果（labelResults）において対応する**優先度が最も高い悪意のあるタグ**を返し、モデルが推奨する審査結果を表示します。業務のニーズに応じて、不正のタイプと推奨値ごとに対処することをお勧めします。戻り値：<ul style="margin:0"><li/>0：正常<li/>1：ポルノ<li/>6：罵詈雑言<li/>8：広告<li/>2-5、7：その他の不快、安全ではないまたは不適切と感じるコンテンツタイプ</ul> |
| score | 入力必須     | Array | type 対応する評点 |
| hotScore                    | 入力必須     | Number | 画像がセクシー画像である評点 |
| pornScore | 入力必須     |Number | 画像がポルノ画像である評点 |
| illegalScore | 入力必須     | Number | 画像が違法である評点 |
| polityScore | 入力必須     | Number | 画像が政治関連である評点|
| terrorScore  | 入力必須     | Number | 画像がテロ関連である評点 |
| abuseScore | 入力必須     | Number | 画像が罵詈雑言関連である評点 |
| teenagerScore | 入力必須    | Number | 画像が青少年に不適切である評点 |
| adScore | 入力必須     | Number | 画像がadScore関連である評点 |
| ocrMsg | オプション    | string | 画像のOCR識別情報（該当する場合） |
| suggestion | 入力必須     | string | 推奨値。値はオプション：<ul style="margin:0"><li/>Block：ブロック<li/>Review：レビュー待ち<li/>Pass：正常</ul>     |
| label | 入力必須      | string                | 検出結果（labelResults）において対応する**優先度が最も高い悪意のあるタグ**を返し、モデルが推奨する審査結果を表示します。業務のニーズに応じて、不正のタイプと推奨値ごとに対処することをお勧めします。戻り値：<ul style="margin:0"><li/>Normal：正常<li/>Porn：ポルノ<li/>Abuse：罵詈雑言<li/>Ad：広告<li/>Custom：その他の不快、安全でないまたは不適切と感じるコンテンツタイプ</ul> |
| subLabel | 入力必須     | string | サブタグ名、サブタグがヒットしない場合は、空の文字列が返されます              |
| labelResults | オプション     | Array of [LabelResult](#labelresult)  | ポルノ、セクシー、暴力、違法不正などのレビュー結果を含む、分類検出モデルのレビュー結果 |
| objectResults | オプション     | Array of [ObjectResult](#objectresult) | 政治団体、広告ロゴ、2次元コードなどのレビュー情報を含む、エンティティ検出モデルのレビュー結果 |
| ocrResults | オプション     | Array of [OcrResult](#ocrresult) | OCRテキスト関連情報を含む、OCRテキストレビュー結果、およびテキストレビュー結果の詳細 |
| libResults | オプション     | Array of [LibResult](#libresult) | リスクライブラリのレビュー結果 |
| screenshotTime | 入力必須     | Number | スクリーンキャプチャ時間 |
| sendTime | 入力必須     | Number | リクエスト送信時間、UNIXタイムスタンプ |
| similarScore  | オプション     | Number | 画像の類似度の評点|
| stream_param  | オプション     | String | プッシュパラメータ|
| app  | オプション     | String | プッシュドメイン名 |
| appid  | オプション     | Number | 業務ID  |
| appname  | オプション     |String | プッシュpathパス  |

 

#### LabelResult
分類モデルのヒット結果。

| 名称   | タイプ                 |  説明                                                     |
| ---------- | ------------------------ | ------------------------ |
| Scene      | String                                       | 広告、ポルノ、有害なコンテンツのシーンなど、モデルによって識別されたシーンの結果を返します。     |
| Suggestion | String                                        |現在の悪意のあるタグに対する後続操作の提案を返します。 判定結果が得られた後の戻り値はシステムが推奨する後続操作を表示します。業務上のニーズに応じて、各不正のタイプと推奨値に対処することをお勧めします。 戻り値：<ul style="margin:0"><li/>Block：ブロックを推奨<li/>Review ：手動レビューを推奨<li/>Pass：承認を推奨</ul> |
| Label      | String                                       | 検出結果に対応する悪意のあるタグを返します。戻り値：<ul style="margin:0"><li/>Normal：正常<li/>Porn：ポルノ<li/>Abuse：罵詈雑言<li/>Ad：広告<li/>Custom：その他の不快、安全でないまたは不適切と感じるコンテンツタイプ</ul> |
| SubLabel   | String | サブタグ名                                                   |
| Score      | Integer | このタグモデルでヒットするスコア                                        |
| Details    | Array of [LabelDetailItem](#labeldetailitem) | 分類モデルでヒットするサブタグの詳細な結果                                   |

#### LabelDetailItem

分類モデルでヒットするサブタグの結果。

| 名称   | タイプ               | 説明                |
| -------- | -------- | --------------------------- |
| Id       | Integer  | 番号                        |
| Name     | String   | サブタグ名                  |
| Score    | Integer  | サブタグスコア。値の範囲は0ポイント～100ポイント|


#### ObjectResult

エンティティの検出結果の詳細。

| 名称   | タイプ              | 説明              |
| ---------- | --------------------- | --------------------- |
| Scene      | String                                 | 2次元コード、logo、画像OCRのシーンなど、エンティティによって識別されたエンティティシーンの結果を返します。 |
| Suggestion | String                                |現在の悪意のあるタグに対する後続操作の提案を返します。 判定結果が得られた後の戻り値はシステムが推奨する後続操作を表示します。業務上のニーズに応じて、各不正のタイプと推奨値に対処することをお勧めします。 戻り値：<ul style="margin:0"><li/>Block：ブロックを推奨<li/>Review ：手動レビューを推奨<li/>Pass：承認を推奨</ul> |
| Label      | String                                 | 検出結果に対応する悪意のあるタグを返し、モデルが推奨する審査結果を表示します。業務のニーズに応じて、不正のタイプと推奨値ごとに対処することをお勧めします。戻り値：<ul style="margin:0"><li/>Normal：正常<li/>Porn：ポルノ<li/>Abuse：罵詈雑言<li/>Ad：広告<li/>Custom：その他の不快、安全でないまたは不適切と感じるコンテンツタイプ</ul> |
| SubLabel   | String             | サブタグ名 |
| Score    | Integer | 該当するシーンモデルでヒットするサブタグのスコア。値の範囲は0ポイント～100ポイント|
| Names      | Array of String       | エンティティ名リスト |
| Details    | Array of [ObjectDetail](#objectdetail) | エンティティ検出結果の詳細 |

#### ObjectDetail

エンティティ検出結果の詳細で、検出シーンが政治団体、政治関係者、広告ロゴ、2次元コードおよび顔の属性である場合、モデル検出対象フレームのタグ名、タグ値、タグスコアおよび検出フレームの位置情報を表示します。

| 名称 | タイプ | 説明                    |
| -------- | -------- | -------- |
| Id       | Integer  | 番号  |
| Name     | String   | タグ名  |
| Value    | String   | タグ値：<ul style="margin:0"><li/>シーンがAdである場合は、URLアドレスを表示します。例えばNameがQrCodeであれば、Value値は`http//abc.com/aaa`です<br><li/>シーンが FaceAttributeである場合は、顔の属性情報を表示します。例えばNameがAgeであれば、Value値は`18`です</ul>|
| Score    | Integer  | スコア。値の範囲は0ポイント～100ポイント |
| Location | [Location](#location) | 検出フレーム座標 |

#### Location

座標。

| 名称      | タイプ     | 説明    |
| -------- | -------- | ---------------- |
| X        | Float    | 左上隅の横軸     |
| Y        | Float    | 左上隅の縦軸     |
| Width    | Float    | 幅             |
| Height   | Float    | 高さ             |
| Rotate   | Float    | 検出フレームの回転角度 |

#### OcrResult

OCR検出結果の詳細です。

| 名称   | タイプ               | 説明                |
| ---------- | ---------------------- | ---------------------- |
| Scene      | String                                   | 認識シーンを表示します。デフォルト値はOCR（画像OCR認識）です。              |
| Suggestion | String                                       | 最も優先度の高い悪意のあるタグに対応する後続操作の提案を返します。 判定結果が得られた後の戻り値はシステムが推奨する後続操作を表示します。業務上のニーズに応じて、各不正と推奨値に対処することをお勧めします。 戻り値：<ul style="margin:0"><li/>Block：ブロックを推奨<li/>Review ：手動レビューを推奨<li/>Pass：承認を推奨</ul> |
| Label      | String                                   | OCR検出結果に対応する優先度が最も高い悪意のあるタグを返し、モデルが推奨する審査結果を表示します。業務のニーズに応じて、不正のタイプと推奨値ごとに対処することをお勧めします。戻り値：<ul style="margin:0"><li/>Normal：正常<li/>Porn：ポルノ<li/>Abuse：罵詈雑言<li/>Ad：広告<li/>Custom：その他の不快、安全でないまたは不適切と感じるコンテンツタイプ</ul> |
| SubLabel   | String             | サブタグ名 |
| Score    | Integer | 該当するシーンモデルでヒットするサブタグのスコア。値の範囲は0ポイント～100ポイント|
| Text       | String | テキストコンテンツ |
| Details    | Array of [OcrTextDetail](#ocrtextdetail) | OCR 結果の詳細 |


#### OcrTextDetail
OCRテキスト結果の詳細です。

| 名称 | タイプ        | 説明                                                     |
| -------- | --------------- | --------------- |
| Text     | String                | OCRで認識されたテキストコンテンツを返します（OCRテキスト認識の上限は** 5000バイト以内**です） |
| Label    | String                | 検出結果に対応する悪意のあるタグを返します。戻り値：<ul style="margin:0"><li/>Normal：正常<li/>Porn：ポルノ<li/>Abuse：罵詈雑言<li/>Ad：広告<li/>Custom：その他の不快、安全でないまたは不適切と感じるコンテンツタイプ</ul> |
| Keywords | Array of String | このタグでヒットしたキーワード |
| Score    | Integer        | 該当するタグモデルでヒットするスコア。値の範囲は0ポイント～100ポイント |
| Location | [Location](#location) | OCR テキスト座標位置 |


#### LibResult
ブラック/ホワイトライブラリ結果の詳細です。

| 名称   | タイプ           | 説明                                                     |
| ---------- | ------------------ | ------------------------------------------------------------ |
| Scene      | String                           | モデルのシーン認識結果を表示します。デフォルト値はSimilarです。                 |
| Suggestion | String                                       | 後続操作の提案を返します。 判定結果が得られた後の戻り値はシステムが推奨する後続操作を表示します。業務上のニーズに応じて、各不正と推奨値に対処することをお勧めします。 戻り値：<ul style="margin:0"><li/>Block：ブロックを推奨<li/>Review ：手動レビューを推奨<li/>Pass：承認を推奨</ul> |
| Label      | String                           | 検出結果に対応する悪意のあるタグを返します。戻り値：<ul style="margin:0"><li/>Normal：正常<li/>Porn：ポルノ<li/>Abuse：罵詈雑言<li/>Ad：広告<li/>Custom：その他の不快、安全でないまたは不適切と感じるコンテンツタイプ</ul> |
| SubLabel   | String             | サブタグ名 |
| Score    | Integer            | 画像検索モデル認識スコア。値の範囲は0ポイント～100ポイント |
| Details    | Array of [ObjectDetail](#objectdetail) | ブラック/ホワイトライブラリ結果の詳細 |

#### LibDetail
カスタマイズコーパス/ブラック/ホワイトライブラリの詳細です。

| 名称   | タイプ                 |  説明                                                     |
| -------- | -------- | ------------------------------------------------------------ |
| Id       | Integer  | 番号                                                         |
| ImageId  | String   | 画像 ID                                                       |
| Label   | String  | 検出結果に対応する悪意のあるタグを返します。戻り値：<ul style="margin:0"><li/>Normal：正常<li/>Porn：ポルノ<li/>Abuse：罵詈雑言<li/>Ad：広告<li/>Custom：その他の不快、安全でないまたは不適切と感じるコンテンツタイプ</ul> |
| Tag      | String   | カスタマイズタグ                                                   |
| Score    | Integer  |モデル認識スコア。値の範囲は0ポイント～100ポイント                               |



#### リクエスト例
<dx-codeblock>
::: HTTPbody  json
{
        "ocrMsg": "",
        "type": [1],
        "socre": 99,
        "hotScore": 0,
        "pornScore": 99,
        "screenshotTime": 1610640000,
        "level": 0,
        "img": "http://1.1.1.1/download/porn/test.jpg",
        "abductionRisk": [],
        "faceDetails": [],
        "sendTime": 1615859827,
        "illegalScore": 0,
        "polityScore": 0,
        "similarScore": 0,
        "terrorScore": 0,
        "abuseScore": 0,
        "teenagerScore": 0,
        "adScore": 0,
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
