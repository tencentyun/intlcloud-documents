CSSのポルノ検出をアクティブ化するには、まずCSSスクリーンキャプチャ機能をアクティブにする必要があります。[CSSコンソール](https://intl.cloud.tencent.com/document/product/267/31072) またはCSSスクリーンキャプチャポルノ検出APIを使用しアクティブにすることができます。本書では、CSSスクリーンキャプチャポルノ検出APIを使用し、CSSポルノ検出機能を実装する方法を説明します。


## 注意事項
COS Bucketへのアクセス権限がパブリック読取りで、Bucketにポルノ、政治及びその他の禁令違反に関するスクリーンキャプチャが存在する場合、COS Bucketからこれらの画像を削除し、COS Bucketが禁止され利用に支障が出ることを回避することをお勧めします。

## CSSポルノ検出のアクティブ化
CSSポルノ検出は、CSSスクリーンキャプチャに基づくため、CSSポルノ検出のアクティブ化には、CSSスクリーンキャプチャ機能のアクティブ化が必要です。具体的な操作は次のとおりです。

### 1. ポルノ検出機能付きCSSスクリーンキャプチャテンプレートの作成
[CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834)を呼び出し、PornFlag = 1を設定することによって、ポルノ検出機能を備えたCSSスクリーンキャプチャテンプレートを作成します。

### 2. ポルノ検出機能付きCSSスクリーンキャプチャルールの作成
[CreateLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30835)を呼び出し、ポルノ検出機能付きCSSスクリーンキャプチャルールを作成し、ステップ1で作成したCSSスクリーンキャプチャテンプレートIDをポルノ検出が必要なライブストリーミングAppId、DomainName、AppName、StreamNameに関連付けます。

### 3. CSSを開始し、ポルノ検出を開始
ポルノ検出機能付きCSSスクリーンキャプチャルールを作成した後、新たに開始するCSSではポルノ検出機能が有効になります。現在ライブストリーミング中のストリームに対して、CSSのポルノ検出を有効にするには、ライブストリーミングを停止し再開する必要があります。

## CSSポルノ検出結果の取得
CSSポルノ検出機能をアクティブにした後、ポルノ検出コールバックテンプレートで登録したコールバックドメイン名を設定すれば、CSSバックエンドからポルノ検出結果がコールバックされます。
>! デフォルトでは疑わしい結果に対してのみコールバックを行い、通常の結果にはコールバックを行いません。

### 1. CSSポルノ検出コールバックテンプレートの作成
[CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815)を呼び出し、PornCensorshipNotifyUrlパラメータにご利用のドメイン名を設定し、CSSポルノ検出コールバックテンプレートを作成します。
### 2. CSSポルノ検出コールバックルールの作成

[CreateLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30816)を呼び出し、ポルノ検出機能付きCSSスクリーンキャプチャルールを作成し、前のステップで作成したCSSスクリーンキャプチャテンプレートIDをポルノ検出が必要なライブストリーミングAppId、DomainName、AppNameに関連付けます。

### 3. ポルノ検出結果の取得
CSSのバックエンドは、HTTP POSTリクエストを介して登録されたドメイン名にポルノ検出結果を送信します。ポルノ検出結果はJSON形式でHTTP Bodyに保存されます。typeフィールドのみでライブストリーミングにポルノ関連のコンテンツがあるかを判断できます。
>!画像の`type`を使用してポルノ画像かどうかを判断することを推奨しますが、検出システムの判断が100%正しいことを保証できないため、ポルノ疑い有無の認識が正確でない場合もございます。したがって、目視による再確認を行うことをお勧めします。  

#### 完全なプロトコルは次のとおりです：
| パラメータ        | 入力必須の有無        | データタイプ         | 説明        |
| -------- | -------- | -------- | -------- |
| streamId    | オプション     | String | ストリーム名     |
| channelId      | オプション     | string   | チャネルID      |
| img     | 入力必須     | string   | 警告画像リンク      |
| type    | 入力必須     | Array    | 検出結果で優先度が最も高い悪意のあるタグに対応する分類値のことです。具体的な意味については、パラメータlabelによって返される補足説明をご参照ください |
| score       | 入力必須     | Array    | typeに対応する評価点数   |
| ocrMsg      | オプション     | string   | 画像のOCR認識情報（該当する場合）       |
| suggestion     | 入力必須     | string   | 推奨値。選択可能な値： <ul style="margin:0"><li/>Block：ブロック<li/>Review：レビュー待ち<li/>Pass：正常</ul> |
| label       | 入力必須     | string   | このフィールドは、検出結果(LabelResults)において優先度が最も高い悪意のあるタグを返すために使用され、モデルが推奨するレビュー結果を表します。業務上のニーズに応じて、不正タイプと推奨値を処理することをお勧めします |
| subLabel    | 入力必須     | string   | このフィールドは、検出結果でヒットした最も優先度が高い悪意のあるタグのサブタグ名を返すために使用されます。例えば、ポルノ--性行為。サブタグがヒットされなかった場合は、空の文字列が返されます |
| labelResults   | オプション     | [Array of LabelResult](#labelresult)   | このフィールドは、分類モデルによってヒットした悪意のあるタグの詳細な識別結果を返すために使用されます。これには、ポルノや広告など好ましくない、安全ではない、または不適切なコンテンツタイプの識別結果が含まれます<br>注意：**このフィールドは、有効な値を取得できなかったことを意味するnullを返す場合があります** |
| objectResults  | オプション     | [Array of ObjectResult](#objectresult) | このフィールドは、オブジェクト検出モデルの詳細な検出結果を返すために使用されます。これには、エンティティ、広告ロゴ、2次元コードなどのコンテンツでヒットしたタグ名、タグスコア、座標情報、シーンの識別結果、推奨操作といったコンテンツの識別情報が含まれます。詳細な戻り値の情報については、対応するデータ構造(ObjectResults)の説明をご参照ください<br> 注意：**このフィールドは、有効な値を取得できなかったことを意味するnullを返す場合があります** |
| ocrResults     | オプション     | [Array of OcrResult](#ocrresult)    | このフィールドは、OCRテキスト識別の詳細な検出結果を返すために使用されます。これには、テキスト座標情報、テキスト識別結果、推奨操作といったコンテンツの識別情報が含まれます。詳細な戻り値の情報については、対応するデータ構造(ObjectResults)の説明をご参照ください<br> 注意：**このフィールドは、有効な値を取得できなかったことを意味するnullを返す場合があります** |
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
| Suggestion | String      | 現在の悪意のあるタグに対する後続操作の提案を返します。 判定結果が得られた後の戻り値はシステムが推奨する後続操作を表示します。業務上のニーズに応じて、各不正のタイプと推奨値に対処することをお勧めします。戻り値：<ul style="margin:0"><li/>Block：ブロックを推奨<li/>Review ：手動レビューを推奨<li/>Pass：承認を推奨</ul> |
| label | String      | このフィールドは、検出結果に対応する悪意のあるタグを返すために使用されます |
|| SubLabel   | String | サブタグ名|
| Score      | Integer | このタグモデルでヒットしたスコア    |
| Details    | Array of [LabelDetailItem](#labeldetailitem) | 分類モデルでヒットしたサブタグの詳細な結果     |

#### LabelDetailItem

分類モデルでヒットしたサブタグの結果。

| 名称 | タイプ | 説明|
| -------- | -------- | ----- |
| Id    | Integer  | 番号   |
| Name     | String   | サブタグ名     |
| Score    | Integer  | サブタグスコア。値の範囲は0ポイント～100ポイント|

#### ObjectResult

エンティティの検出結果の詳細。

| 名称   | タイプ    | 説明     |
| ---------- | --------------------- | --------------------- |
| Scene      | String   | 2次元コード、ロゴ、画像OCRのシーンなど、エンティティによって識別されたエンティティシーンの結果を返します。 |
| Suggestion | String   | 現在の悪意のあるタグに対する後続操作の提案を返します。判定結果が得られた後の戻り値は、システムが推奨する後続操作を表します。業務上のニーズに応じて、それぞれの不正タイプと推奨値を処理することをお勧めします。 戻り値：<ul style="margin:0"><li/>Block：ブロックを推奨<li/>Review ：手動レビューを推奨<li/>Pass：承認を推奨</ul> |
| label | String   | このフィールドは、検出結果に対応する悪意のあるタグを返すために使用されます |
| SubLabel   | String      | サブタグ名 |
| Score    | Integer | 該当するシーンモデルでヒットするサブタグのスコア。値の範囲は0ポイント～100ポイント|
| Names      | Array of String    | エンティティ名リスト |
| Details    | Array of [ObjectDetail](#objectdetail) | エンティティ検出結果の詳細 |

#### ObjectDetail

エンティティ検出結果の詳細で、検出シーンがエンティティ、広告ロゴ、2次元コードである場合、モデル検出対象フレームのタグ名、タグ値、タグスコアおよび検出フレームの位置情報を表します。

| 名称     | タイプ     | 説明    |
| -------- | -------- | -------- |
| Id    | Integer    | このパラメータは、識別や区別を容易にするために、識別されたオブジェクトのIDを返すために使用されます    |
| Name     | String     | このパラメータは、ヒットしたエンティティタグを返すために使用されます   |
| Value    | String     | このパラメータは、対応するエンティティタグに対応する値またはコンテンツを返すために使用されます。例えば、タグが2次元コード(QrCode)の場合、このフィールドは識別された2次元コードに対応するURLアドレスになります |
| Score    | Integer    | このパラメータは、対応するエンティティタグのスコアを返すために使用され、値は0～100です。例えば、QrCode 99は、対応する識別コンテンツが2次元コードシーンタグにヒットする確率が非常に高いことを意味します |
| Location | [Location](#location) | このフィールドは、エンティティ検出フレームの座標位置（左上隅のxy座標、長さと幅、回転角度）を返すために使用され、エンティティの関連情報の素早い特定を容易にします |

#### Location

座標。

| 名称     | タイプ     | 説明    |
| -------- | -------- | ---------------- |
| X     | Float    | 左上隅の横座標     |
| Y     | Float    | 左上隅の縦座標     |
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
| SubLabel   | String      | サブタグ名 |
| Score    | Integer | 該当するシーンモデルでヒットするサブタグのスコア。値の範囲は0ポイント～100ポイント|
| Text    | String | テキストコンテンツ |
| Details    | Array of [OcrTextDetail](#ocrtextdetail) | OCR 結果の詳細 |

#### OcrTextDetail
OCRテキスト結果の詳細です。

| 名称 | タイプ     | 説明  |
| -------- | --------------- | --------------- |
| Text     | String     | OCRで識別されたテキストコンテンツを返します（OCRで識別できるテキストの上限は** 5000バイト**です）。 |
| label | String     | このフィールドは、検出結果に対応する悪意のあるタグを返すために使用されます |
| Keywords | Array of String | このタグでヒットしたキーワード |
| Score    | Integer      | このタグモデルでヒットするスコア。値の範囲は0ポイント～100ポイント |
| Location | [Location](#location) | OCR テキスト座標位置 |

#### LibResult
ブラック/ホワイトライブラリ結果の詳細です。

| 名称   | タイプ    | 説明     |
| ---------- | ------------------ | ------------------ |
| Scene      | String      | モデルのシーン識別結果を表します。デフォルト値はSimilarです。    |
| Suggestion | String      | 後続操作の提案を返します。判定結果が得られた後の戻り値は、システムが推奨する後続操作を表します。業務上のニーズに応じて、それぞれの不正タイプと推奨値を処理することをお勧めします。戻り値：<ul style="margin:0"><li/>Block：ブロックを推奨<li/>Review ：手動レビューを推奨<li/>Pass：承認を推奨</ul> |
| label | String      | このフィールドは、検出結果に対応する悪意のあるタグを返すために使用されます |
| SubLabel   | String      | サブタグ名 |
| Score      | Integer     | 画像検索モデル認識スコア。値の範囲は0ポイント～100ポイント |
| Details    | Array of [ObjectDetail](#objectdetail) | ブラック/ホワイトライブラリ結果の詳細 |

#### LibDetail
カスタマイズコーパス/ブラック/ホワイトライブラリの詳細です。

| 名称     | タイプ     | 説明    |
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
        "appid":10000,
        "event_type": 317,
        "sign": "ac920c3e66**********78cf1b5de2c63",
        "t": 1615860427
}
:::
</dx-codeblock>

## CSSポルノ検出の無効化

CSSポルノ検出を無効にするには、スクリーンキャプチャルールを削除するか、スクリーンキャプチャテンプレートを変更する必要があります。削除と変更は新たなCSSに対してのみ有効です。すでに開始されているCSSに対して、ポルノ検出を無効にする場合、ライブストリーミングを停止し、再開する必要があります。

### 1. ポルノ検出スクリーンキャプチャルールの削除による無効化

[DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833)を呼び出し、テンプレートIDでDomainName、 AppName、StreamNameに対応するCSSスクリーンキャプチャルールを削除します。

### 2. ポルノ検出スクリーンキャプチャテンプレートの削除または変更による無効化

[ModifyLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30828)を呼び出し、CSSテンプレートのポルノ検出タグを0に変更します。