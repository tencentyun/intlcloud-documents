## 機能説明

このAPIは、指定された配送ポリシーの詳細を取得するために使用されます。

## リクエスト

### リクエスト例

```
GET /shipper?shipper_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
```

### リクエストライン

```
GET /shipper
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名     | タイプ   | 場所  | 必須項目 | 意味             |
| ---------- | ------ | ----- | -------- | ---------------- |
| shipper_id | string | query | はい       | 照合するshipper idです |

## 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "shipper_id": "xxxx-xx-xx-xx-xxxxxxxx",
  "topic_id": "yyyy-yy-yy-yy-yyyyyyyy",
  "bucket": "test-1250000001",
  "prefix": "test",
  "shipper_name": "myname",
  "interval": 300,
  "max_size": 256,
  "effective": true,
  "filter_rules": [{
    "key": "",
    "regex": "",
    "value": ""
  }],
  "partition": "%Y%m%d",
    "compress": {
        "format": "none"
    },
    "content": {
        "format": "json",
    },
  "create_time": "2017-12-12 12:12:12"
}
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### 応答パラメータ

| フィールド名       | タイプ   | 必須項目 | 意味                                             |
| ------------ | ------ | -------- | ------------------------------------------------ |
| shipper_id   | string | はい       | 配信のIDです                                        |
| topic_id     | string | はい       | 配信規則が属するtopic idです                           |
| bucket       | string | はい       | ログが配送されるbucketアドレスです                                 |
| prefix       | string | はい       | ログが配信されるプレフィックスディレクトリです                                   |
| shipper_name | string | はい       | 配信規則の名前です                                   |
| interval     | int    | はい       | 配信間隔です。単位：秒                          |
| max_size     | int    | はい       | 配信するファイルの最大サイズです。単位：MB                      |
| effective    | bool   | はい       | 有効かどうか                                         |
| filter_rules | array  | はい       | 配信されるログをフィルタリングするための規則です                               |
| create_time  | string | はい       | 配信されるログの作成時間です                               |
| partition    | string | いいえ       | ログを配信するためのパーティション規則です。`strftime`は時間フォーマットの表現を定義するために使うことができます             |
| compress     | object | はい       | 配信されるログの圧縮構成です                               |
| content      | object | はい       | 配信されるログのフォーマット構成です                           |

filter_rulesのフォーマットは次のとおりです：

| フィールド名       | タイプ   | 必須項目 | 意味                                               |
| ------ | ------ | -------- | -------------------------------------------------- |
| key    | string | はい       | 比較用のkeyです。`__CONTENT__`が全文を意味します               |
| regex  | string |  はい       | 比較コンテンツを抽出するために使用する正規表現です                           |
| value  | string | はい       | 上記のregexを使用して抽出されたコンテンツと比較するために使用される値です。規則が一致している場合は、この規則が起動されます |

compressのフォーマットは次のとおりです：

| フィールド名        | タイプ       |必須項目 | 意味                                       |
| ------ | ------ | -------- | ------------------------------------------ |
| format | string | はい   | 圧縮フォーマットです。`gzip`、`lzop`と`none`（圧縮しない）がサポットされます |

contentのフォーマットは次のとおりです：

| フィールド名        | タイプ       |必須項目 | 意味                        |
| -------- | ------ | -------- | --------------------------- |
| format   | string | はい       | コンテンツフォーマットです。`json`、`csv`がサポートされます |
| csv_info | object | いいえ       | コンテンツフォーマットが`csv`の場合は返します       |

csv_infoのフォーマットは次のとおりです：

| フィールド名             | タイプ          | 必須項目 | 意味                                             |
| ------------------ | ------------- | -------- | ------------------------------------------------ |
| print_key          | bool          | はい       | csvファイルにkeyの最初の行を書き込むかどうかを示します                               |
| keys               | array（string） | はい       | 各列keyの名前です                                    |
| delimiter          | string        | はい       | 各フィールド間の区切り記号                                 |
| escape_char        | string        | はい       | フィールドに区切り記号が含まれている場合は、エスケープ文字でこのフィールドを囲む必要があります |
| non_existing_field | string        | はい       | 存在しないか無効な、上記で指定したフィールドに値を入力するために使用されます           |

### エラーコード

詳細については、[エラーコード](https://cloud.tencent.com/document/product/614/12402)を参照してください。

