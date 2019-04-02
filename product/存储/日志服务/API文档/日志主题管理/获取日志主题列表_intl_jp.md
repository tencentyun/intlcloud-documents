## 機能説明

このAPIは、ログトピック関連情報のリストを取得するために使用されます。

## リクエスト

### リクエスト例

```
GET /topics?logset_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
```

### リクエストライン

```
GET /topics
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名    | タイプ   | 場所  | 必須項目 | 意味             |
| --------- | ------ | ----- | ---- | ---------------- |
| logset_id | string | query | はい   | 照合するlogset id |

## 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "topics": [
    {
    "logset_id": "xxxx-xx-xx-xx-xxxxxxxx",
    "topic_id": "xxxx-xx-xx-xx-yyyyyyyy",
    "topic_name": "testname",
    "path": "/abc/log/test.log",
    "wild_path":"/data/nginx/log/**/access.log",
    "collection": true,
    "index": true,
    "log_type": "delimiter_log",
    "extract_rule": {
          "time_key": "date",
          "time_format": "%Y-%m-%d %H:%M:%S",
          "delimiter": "|",
          "log_regex": ".*",
          "beginning_regex": "^",
          "keys": ["date","","content"],
          "filter_keys": [],
          "filter_regex": []
      },
    "create_time": "2017-08-08 12:12:12"
    }
  ]
}
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### 応答パラメータ

| フィールド名 | タイプ      | 必須項目 |意味             |
| ------ | --------- | ---- | ---------------- |
| topics | JsonArray | はい   | ログトピック関連情報配列 |

TopicInfoのフォーマットは次のとおりです：

| フィールド名        | タイプ       |必須項目 | 意味                                                         |
| ------------- | ---------- | ---- | ------------------------------------------------------------ |
| logset_id     | string     | はい   | ログセットのID                                                  |
| topic_id      | string     | はい   | ログトピックのID                                                |
| topic_name    | string     | はい   | ログトピックの名前                                               |
| path          | string     | はい   | 古いバージョンのログファイルのパス                                             |
| wild_path     |	string     | いいえ   | ワイルドカードを使用した新しいログ収集パスです。/\*\*/でファイルディレクトリとファイル名を区切って、新旧のパスが同時に存在することはできません  |
| collection    | bool       | はい   | コレクションを有効にするかどうか                                                 |
| index         | bool       | はい   | インデックスを有効にするかどうか                                                 |
| log_type     | string     | はい   | 収集されたログタイプについては、`json_log`がjsonフォーマットのログを表し、`delimiter_log`が区切り記号フォーマットのログを表し、`minimalist_log`がミニマリストのログを表し、`egex_log`、`multiline_log`が複数行のログを表し、`fullregex_log`が完全な正規表現を表します |
| extract_rule  | JsonObject | はい   | 抽出規則                                                     |
| machine_group | JsonObject | いいえ   | サーバーグループ関連情報の収集                                               |
| create_time   | string     | いいえ   | 作成時間                                                     |

extract_ruleのフォーマットは次のとおりです：

| time_key          | タイプ              | 必須項目 | 意味                                                        |
| --------------- | ----------------- | -------- | ----------------------------------------------------------- |
| time_key        | string            | いいえ       | 時間フィールドのkey名前です。                                           |
| time_format     | string            | いいえ       | 時間のフォーマットです。C言語の`strftime`関数を参照してください |
| delimiter       | string            | いいえ       | 区切り記号タイプログに対応する区切り記号                                      |
| log_regex       | string            | いいえ       | 複数行のログタイプに対応するログ全体のマッチング規則                             |
| beginning_regex | string            | いいえ       | 複数行のログタイプに対応する行頭のマッチング規則                                |
| keys            | JsonArray(string) | いいえ       | 抽出された各フィールドのkey名前                                     |
| filter_keys     | JsonArray(string) | いいえ       | ログをフィルタリングする必要があるkeyです                                           |
| filter_regex    | JsonArray(string) | いいえ       | filter_keysで指定されたキーに対応する値です。値の数はfilter_keysの数と同じです。1対1対応です        |

## エラーコード

詳細については、[エラーコード](https://cloud.tencent.com/document/product/614/12402)を参照してください。

