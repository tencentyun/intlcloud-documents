CSSポルノ検出は、スクリーンキャプチャポルノ検出テンプレートで設定されたルールに従ってCSSストリームのスクリーンキャプチャを行い、画像を生成してCOSに保存するとともに、Pornfoundの識別機能によって不正な内容のある画像を識別します。ポルノ検出コールバックはライブストリーミングのポルノ検出画像情報のプッシュに用いられ、これには問題画像が属するタイプ、レベル評価、スクリーンキャプチャの時間などが含まれます。コールバックテンプレートの中でポルノ検出コールバックメッセージの受信サーバーアドレスを設定し、当該テンプレートとプッシュドメイン名を関連付ける必要があります。ライブストリーミングがポルノ検出イベントをトリガーした後、Tencent Cloud CSSのバックエンドがポルノ関連画像情報をお客様が設定した受信サーバーにコールバックします。

ここでは、主にポルノ検出コールバックイベントがトリガーされた後、Tencent Cloudバックエンドがユーザーに送信するコールバックメッセージ通知のフィールドについてご説明します。

## 注意事項
- このドキュメントを読む前に、Tencent Cloud CSSによるコールバック機能の設定方法とコールバックメッセージの受信方法についてご理解下さると幸いです。詳細については、[イベント通知の受信方法](https://intl.cloud.tencent.com/document/product/267/38080)をご参照ください。
- CSSポルノ検出は、デフォルトでは疑わしい結果に対してのみコールバックを行い、通常の結果にはコールバックを行いません。
- 画像の [type](#type)を利用してポルノ画像に対する評定を行う場合、検出システムの判定を100%の精度にすることはできないため、時折判定が誤っていることもあります。よって、実際のユースケースに応じて、人による二次確認を実施することをお勧めします。

## スクリーンキャプチャイベントのパラメータ説明
### イベントタイプパラメータ

| イベントタイプ | フィールド設定値の説明    |
| :------- | :------------- |
| CSSポルノ検出 | event_type = 317 |


### コールバック共通パラメータ

<table>
<tr><th>フィールド名</th><th>タイプ</th><th>説明</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>期限切れ時間、イベント通知サイン期限のUNIXタイムスタンプ。<ul style="margin:0"><li>Tencent Cloudからのメッセージ通知のデフォルトの期限切れ時間は10分です。メッセージ通知中の t 値が示す時間が期限に達した場合、この通知を無効と判断され、ネットワークのリプレイアタックを防止します。<li>t の形式は10進数UNIXタイムスタンプとなり、1970年1月1日（UTC/GMT 真夜中）から経過した秒数となります。</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>イベント通知セキュリティサイン sign = MD5（key + t）。<br>説明：Tencent Cloudが、暗号化 <a href="#key">key</a> と t で文字列を結合した後、MD5でsignの値を算出し、それを通知メッセージに入れます。お客様のバックエンドサーバーは、通知メッセージの受信後、同じアルゴリズムに基づきsignが正確か確認し、さらにメッセージが確実にTencent Cloudバックエンドから来たものかを確認することができます。</td>
</tr></table>

>? [](id:key)keyは、**イベントセンター>[CSSコールバック](https://console.cloud.tencent.com/live/config/callback)**の中のコールバックキーとなり、主に認証に使用します。お客様のデータ、情報のセキュリティ保護のため、入力することをお勧めします。

![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)




### コールバックメッセージのパラメータ
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



### コールバックメッセージの例
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








