## 機能説明

このAPIは、既存の配送タスクを変更するために使用されます。このAPIを使用するときは、CLSに手動で指定されたバケットへの書き込み権限を付与する必要があります。



### リクエスト例

```
 PUT /shipper HTTP/1.1
 Host: <Region>.cls.myqcloud.com
 Authorization: <AuthorizationString>
 Content-Type: application/json
 
 {
   "shipper_id": "xxxx-xx-xx-xx-xxxxxxxx",
   "bucket": "test-1250000001",
   "prefix": "test",
   "shipper_name": "myname",
   "interval": 300,
   "max_size": 256,
   "effective": true,
   "partition": "%Y%m%d",
     "compress": {
         "format": "none"
     },
     "content": {
         "format": "json",
     },
   "filter_rules": [{
     "key": "",
     "regex": "",
     "value": ""
   }]
 }
```



## リクエストライン

```
PUT /shipper
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名       | タイプ   | 場所  | 必須項目 | 意味                                                         |
| ------------ | ------ | ---- | ---- | ------------------------------------------------------------ |
| shipper_id   | string | body | はい   | 変更されたShipperのIDです                                         |
| bucket       | string | body | いいえ   | Shipperが配信した新しいbucketです。フォーマット：{bucketName}  -  {appid}        |
| prefix       | string | body | いいえ   | Shipperが配信した新しいディレクトリのプレフィックスです                                   |
| shipper_name | string | body | いいえ   | 配信規則の名前です                                               |
| interval     | int    | body | いいえ   | 配信間隔です。単位：秒、デフォルトは300、範囲は60 ~ 3600です           |
| max_size     | int    | body | いいえ   | 配信されるファイルの最大値です。単位：MB、デフォルトは256、範囲は100 ~ 10240です      |
| effective    | bool   | body | いいえ   | Shipperの切り替え状態です                                           |
| filter_rules | array  | body | いいえ   | 配信されるログをフィルタリングするための規則です。規則に一致するログが配信されます。規則間の関係は`and`です。規則の数は5に制限されています。配列を空のままにした場合、すべてのログはフィルタリングされずに配信されます |
| partition    | string | body | いいえ   | ログを配信するためのパーティション規則です。`strftime`は時間フォーマットの表現を定義するために使うことができます             |
| compress     | object | body | はい   | 配信されるログの圧縮構成です                                           |
| content      | object | body | はい   | 配信されるログのフォーマット構成です                                       |

Ruleのフォーマットは次のとおりです：

| フィールド名        | タイプ       |必須項目 | 意味                                                  |
| ------ | ------ | ---- | ----------------------------------------------------- |
| key    | string | はい   | 比較用のkeyです。`__CONTENT__`が全文を意味します                 |
| regex  | string | はい   | 比較コンテンツを抽出するために使用する正規表現です                              |
| value  | string | はい   | 上記のregexを使用して抽出されたコンテンツと比較するために使用される値です。規則が一致している場合は、この規則が起動されます |

compressのフォーマットは次のとおりです：

| フィールド名        | タイプ       |必須項目 | 意味                                       |
| ------ | ------ | ---- | ------------------------------------------ |
| format | string | はい   | 圧縮フォーマットです。`gzip`、`lzop`と`none`（圧縮しない）がサポットされます |

contentのフォーマットは次のとおりです：

| フィールド名        | タイプ       |必須項目 | 意味                        |
| -------- | ------ | -------- | --------------------------- |
| format   | string | はい       | コンテンツフォーマットです。`json`、`csv`がサポートされます |
| csv_info | object | いいえ       | コンテンツフォーマットが`csv`の場合は設定します       |

csv_infoのフォーマットは次のとおりです：

| フィールド名             | タイプ          | 必須項目 | 意味                                             |
| ------------------ | ------------- | -------- | ------------------------------------------------ |
| print_key          | bool          | はい       | csvファイルにkeyの最初の行を書き込むかどうかを示します                               |
| keys               | array（string） | はい       | 各列keyの名前です                                    |
| delimiter          | string        | はい       | 各フィールド間の区切り記号                                 |
| escape_char        | string        | はい       | フィールドに区切り記号が含まれている場合は、エスケープ文字でこのフィールドを囲む必要があります |
| non_existing_field | string        | はい       | 存在しないか無効な、上記で指定したフィールドに値を入力するために使用されます           |

>!次のうち少なくとも1つを提供する必要があります：bucket、prefix、shipper_name、interval、max_size、effective、filter_rules、compress。

## 応答

### 応答例

```
 HTTP/1.1 200 OK
 Content-Type: application/json
 Content-Length: 0
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### 応答パラメータ
なし

## エラーコード

詳細については、[エラーコード](https://cloud.tencent.com/document/product/614/12402)を参照してください。

