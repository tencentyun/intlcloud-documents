CSS ポルノ検出では、ライブストリーミング中にポルノ関係の疑いのある画面をリアルタイムで切り取ってイメージにし、さらに生成した画像をCOSの中に保存します。ポルノ検出コールバックはライブストリーミングのポルノ検出画像情報のプッシュに用いられ、これには問題画像が属するタイプ、レベル評価、スクリーンキャプチャの時間などが含まれます。コールバックテンプレートの中でポルノ検出コールバックメッセージの受信サーバーアドレスを設定し、本テンプレートとプッシュドメイン名をバインドする必要があります。ライブストリーミングがポルノ検出イベントをトリガーした後、Tencent Cloud CSSのバックエンドがポルノ関連画像情報をお客様が設定した受信サーバーにコールバックします。

ここでは、主にポルノ検出コールバックイベントがトリガーされた後、Tencent Cloudバックエンドがユーザーに送信するコールバックメッセージ通知のフィールドについてご説明します。

## 注意事項
- このドキュメントを読む前に、Tencent Cloud CSSによるコールバック機能の設定方法とコールバックメッセージの受信方法についてご理解下さると幸いです。詳細については、[イベント通知の受信方法](https://intl.cloud.tencent.com/document/product/267/38080)をご参照ください。
- CSSポルノ検出は、デフォルトでは疑わしい結果に対してのみコールバックを行い、通常の結果にはコールバックを行いません。
- 画像の [type](#type)を利用してポルノ画像に対する評定を行う場合、検出システムの判定を100%の精度にすることはできないため、時折判定が誤っていることもあります。よって、実際のユースケースに応じて、人による二次確認を実施することをお勧めします。

## スクリーンキャプチャイベントのパラメータ説明
### イベントタイプパラメータ

| イベントタイプ | フィールド設定値の説明           |
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
| ---------- | ---------- | ---------- | --------------------------- |
| streamId | オプション     | String | ストリーム名 |
| channelId | オプション     | string | チャネルID |
| img | 入力必須     | string | 予備警告画像リンク |
| type | 入力必須      | Array | 検出結果（labelResults）において対応する優先度が最も高い悪意のあるタグを返し、モデルが推奨する審査結果を表示します。業務のニーズに応じて、不正のタイプと推奨値ごとに対処することをお勧めします。戻り値は数字で以下のようになります：<ul style="margin:0"><li/>0：正常<li/>1-8：それぞれ次のパラメータでhotScoreからadScoreまでのさまざまなタイプの順序を表わします。1-ポルノ、6-罵詈雑言、8-広告、その他以下同様</ul> |
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
| label | 入力必須     | string                | パラメータtypeに対して返すタイプ値の補足テキスト説明です。戻り値**0**の補足説明はNormal、戻り値が**6**の場合の補足説明はAbuse、戻り値が**8**の場合の補足説明はAdなど |
| subLabel | 入力必須     | string | サブタグ名、サブタグがヒットしない場合は、空の文字列が返されます              |
| labelResults | オプション     | Array of [LabelResult](#labelresult)  | ポルノ、セクシー、暴力、違法不正などのレビュー結果を含む、分類検出モデルのレビュー結果 |
| objectResults | オプション     | Array of [ObjectResult](#objectresult) | 政治団体、広告ロゴ、2次元コードなどのレビュー情報を含む、エンティティ検出モデルのレビュー結果 |
| ocrResults | オプション     | Array of [OcrResult](#ocrresult) | OCRテキスト関連情報を含む、OCRテキストレビュー結果、およびテキストレビュー結果の詳細 |
| libResults | オプション     | Array of [LibResult](#libresult) | リスクライブラリのレビュー結果 |
| screenshotTime | 入力必須     | Number | スクリーンキャプチャ時間 |
| sendTime | 入力必須     | Number | リクエスト送信時間、UNIXタイムスタンプ |
| similarScore  | オプション     | Number | 画像の類似度の評点|
| stream_param  | オプション     | String | プッシュパラメータ
| app  | オプション     | String | プッシュドメイン名 |
| appid  | オプション     | Number | 業務ID  |
| appname  | オプション     |String | プッシュpathパス  |

 

#### LabelResult
分類モデルのヒット結果。

| 名称   | タイプ                 |  説明                                                     |
| ---------- | ------------------------ | ------------------------ |
| Scene      | String                                       | 広告、ポルノ、有害なコンテンツのシーンなど、モデルによって識別されたシーンの結果を返します。     |
| Suggestion | String                                        |現在の悪意のあるタグに対する後続操作の提案を返します。 判定結果が得られた後の戻り値はシステムが推奨する後続操作を表示します。業務上のニーズに応じて、各不正のタイプと推奨値に対処することをお勧めします。 戻り値：<ul style="margin:0"><li/>Block：ブロックを推奨<li/>Review ：手動レビューを推奨<li/>Pass：承認を推奨</ul> |
| label | String                                       | コールバックメーセッジパラメータtypeに対して返すタイプ値の補足テキスト説明です。戻り値が**0**の場合の補足説明はNormal、戻り値が**6**の場合の補足説明はAbuse、戻り値が**8**の場合の補足説明はAdなど |
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
| label | String                                 | コールバックメーセッジパラメータtypeに対して返すタイプ値の補足テキスト説明です。戻り値が**0**の場合の補足説明はNormal、戻り値が**6**の場合の補足説明はAbuse、戻り値が**8**の場合の補足説明はAdなど |
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
| label | String                                   | コールバックメーセッジパラメータtypeに対して返すタイプ値の補足テキスト説明です。戻り値が**0**の場合の補足説明はNormal、戻り値が**6**の場合の補足説明はAbuse、戻り値が**8**の場合の補足説明はAdなど |
| SubLabel   | String             | サブタグ名 |
| Score    | Integer | 該当するシーンモデルでヒットするサブタグのスコア。値の範囲は0ポイント～100ポイント|
| Text       | String | テキストコンテンツ |
| Details    | Array of [OcrTextDetail](#ocrtextdetail) | OCR 結果の詳細 |


#### OcrTextDetail
OCRテキスト結果の詳細です。

| 名称 | タイプ        | 説明                                                     |
| -------- | --------------- | --------------- |
| Text     | String                | OCRで認識されたテキストコンテンツを返します（OCRテキスト認識の上限は** 5000バイト以内**です） |
| label | String                | コールバックメーセッジパラメータtypeに対して返すタイプ値の補足テキスト説明です。戻り値が**0**の場合の補足説明はNormal、戻り値が**6**の場合の補足説明はAbuse、戻り値が**8**の場合の補足説明はAdなど |
| Keywords | Array of String | このタグでヒットしたキーワード |
| Score    | Integer        | 該当するタグモデルでヒットするスコア。値の範囲は0ポイント～100ポイント |
| Location | [Location](#location) | OCR テキスト座標位置 |


#### LibResult
ブラック/ホワイトライブラリ結果の詳細です。

| 名称   | タイプ           | 説明                                                     |
| ---------- | ------------------ | ------------------------------------------------------------ |
| Scene      | String                           | モデルのシーン認識結果を表示します。デフォルト値はSimilarです。                 |
| Suggestion | String                                       | 後続操作の提案を返します。 判定結果が得られた後の戻り値はシステムが推奨する後続操作を表示します。業務上のニーズに応じて、各不正と推奨値に対処することをお勧めします。 戻り値：<ul style="margin:0"><li/>Block：ブロックを推奨<li/>Review ：手動レビューを推奨<li/>Pass：承認を推奨</ul> |
| label | String                           | コールバックメーセッジパラメータtypeに対して返すタイプ値の補足テキスト説明です。戻り値が**0**の場合の補足説明はNormal、戻り値が**6**の場合の補足説明はAbuse、戻り値が**8**の場合の補足説明はAdなど |
| SubLabel   | String             | サブタグ名 |
| Score    | Integer            | 画像検索モデル認識スコア。値の範囲は0ポイント～100ポイント |
| Details    | Array of [ObjectDetail](#objectdetail) | ブラック/ホワイトライブラリ結果の詳細 |

#### LibDetail
カスタマイズコーパス/ブラック/ホワイトライブラリの詳細です。

| 名称   | タイプ                 |  説明                                                     |
| -------- | -------- | ------------------------------------------------------------ |
| Id       | Integer  | 番号                                                         |
| ImageId  | String   | 画像ID                                                       |
| label | String  | コールバックメーセッジパラメータtypeに対して返すタイプ値の補足テキスト説明です。戻り値が**0**の場合の補足説明はNormal、戻り値が**6**の場合の補足説明はAbuse、戻り値が**8**の場合の補足説明はAdなど |
| Tag      | String   | カスタマイズタグ                                                   |
| Score    | Integer  |モデル認識スコア。値の範囲は0ポイント～100ポイント                               |



### コールバックメッセージの例
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







