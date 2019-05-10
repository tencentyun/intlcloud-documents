## 機能説明

このAPIは、ログトピックを変更するために使用されます。

## リクエスト

### リクエスト例

```
PUT /topic HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
  "topic_id": "xxxxxx-xx-xx-xx-xxxxxxxx",
  "topic_name": "testname",
  "path": "/data/nginx/log/access.log",
  "wild_path":"/data/nginx/log/**/access.log",
  "collection": false,
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
  }
}
```

### リクエストライン

```
PUT /topic
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名         |  タイプ  | 場所  |必須項目 | 意味                                                         |
| ------------ | ---------- | ---- | ---- | ------------------------------------------------------------ |
| topic_id     | string     | body | はい   | ログトピックのID                                                |
| topic_name   | string     | body | いいえ   | ログトピックの名前                                               |
| path         | string     | body | いいえ   | 古いバージョンのログトピックについて収集する必要があるログパスです                                   |
| wild_path    | string     | body | いいえ   | ワイルドカードを使用した新しいログ収集パスです。/\*\*/でファイルディレクトリとファイル名を区切って、新旧のパスが同時に存在することはできません       |
| collection   | bool       | いいえ   | コレクションを有効にするかどうか                                                 |
| log_type     | string     | body | いいえ   | 収集されたログタイプについては、`json_log`がjsonフォーマットのログをを表し、`delimiter_log`が区切り記号フォーマットのログを表し、`minimalist_log`がミニマリストのログを表し、`multiline_log`が複数行のログを表し、`fullregex_log`が完全な正規表現を表します |
| extract_rule | JsonObject | body | いいえ   | 抽出規則                                                     |

>!topic_name、path、group_id、collection、（log_type+extract_rule)の少なくとも一方を提供する必要があります。



extract_ruleのフォーマットは次のとおりです：

| フィールド名         |  タイプ              |必須項目 | 意味                                                         |
| --------------- | ----------------- | -------- | ------------------------------------------------------------ |
| time_key        | string            | いいえ       | 時間フィールドのkey名前です。time_keyとtime_formatがペアで現れる必要があります         |
| time_format     | string            | いいえ       | 時間のフォーマットです。C言語の`strftime`関数を参照してください  |
| delimiter       | string            | いいえ       | 区切り記号タイプログに対応する区切り記号です。`log_type`が`delimiter_log`である場合にのみ有効です |
| log_regex       | string            | いいえ       | ログ全体をマッチングする規則。`log_type`が`fullregex_log`である場合にのみ有効です      |
| beginning_regex | string            | いいえ       | 行頭のマッチング規則です。`log_type`が`multiline_log`または`regex_log`である場合にのみ有効です |
| keys            | JsonArray（string） | いいえ       | 抽出された各フィールドのkey名前です。空のkeyはこのフィールドを破棄することを意味します。`log_type`が`delimiter_log`である場合にのみ有効です。`json_log`のログにjson自分のkeyが使われます |
| filter_keys     | JsonArray（string） | いいえ       | ログをフィルタリングする必要があるkeyです。最大5つです                                   |
| filter_regex    | JsonArray（string） | いいえ       | filter_keysで指定されたキーに対応する値です。値の数はfilter_keysの数と同じです。1対1対応、規則にマッチングするログが収集されます |

## 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Length: 0
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### 応答パラメータ

なし

## エラーコード

詳細については、[エラーコード](https://cloud.tencent.com/document/product/614/12402)を参照してください。

