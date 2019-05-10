## 機能説明

このAPIは、指定された基準に従ってログのコンテンツを検索するために使用されます。

### リクエスト例

```
GET /searchlog?logset_id=xxxx-xx-xx-xx-xxxxxxxx&topic_ids=xxxx,xxxx&start_time=2017-08-22%2010%3A10%3A10&end_time=2017-08-23%2010%3A10%3A10&query=&limit=10&context= HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### リクエストライン

```
GET /searchlog
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名         |  タイプ  | 場所  |必須項目 |      意味                                          |
|---------------|--------|------|--------|---------------------------------------------------|
| logset_id     | string | query| はい      |照合するlogset id                                   |
| topic_ids     | string | query| はい      |照合するtopic idの組合せ、`,`で区切られます                         |
| start_time    | string | query| はい      |照合するログの開始時刻、フォーマット：YYYY-mm-dd HH：MM：SS       |
| end_time      | string | query| はい      |照合するログの終了時刻、フォーマット：YYYY-mm-dd HH：MM：SS       |
| query         | string | query| はい      |照合するコンテンツ                                         |
| limit         | int    | query| はい      |一度に返されるログの数、一度に返される最大数は`100`です          |
| context       | string | query| いいえ      |使用するためにもっとロードし、最後に返されたコンテキスト値をトランスペアレント伝送し、後続のログコンテンツを取得します |
| sort          | string | query| いいえ      |asc（昇順）またはdesc（降順）の時間順に並べ替え、デフォルトではdesc        |

## 応答

### 応答例

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 53

{
    "context": "abcdefg",
    "listover": false,
    "results": [
    {
        "timestamp": "2017-07-14 20:43:00",
        "topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
        "topic_name": "xxxxxxx",
        "content": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    },
    {
        "timestamp": "2017-07-14 20:42:00",
        "topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
        "topic_name": "xxxxxxx",
        "content": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    }
    ]
}
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### 応答パラメータ

|  フィールド名      |  タイプ                | 必須項目 |        意味                    |
|-------------|----------------------|---------|-------------------------------|
| context     | string               | はい      | 後続のコンテンツをロードするためのコンテキスト        |
| listover    | bool                 | はい      | すべての検索結果が返されるかどうか          |
| results     | JsonArray（LogObject） | はい      | ログコンテンツ情報                    |

LogObjectのフォーマットは次のとおりです：

|  フィールド名     |  タイプ  | 必須項目 |        意味                    |
|------------|--------|---------|-------------------------------|
| topic_id   | string | はい      | ログが属するtopic id             |
| topic_name | string | はい      | ログトピックの名前                  |
| timestamp  | string | はい      | ログ時間                       |
| content    | string | はい      | ログコンテンツ                      |

## エラーコード

詳細については、[エラーコード](https://cloud.tencent.com/document/product/614/12402)を参照してください。

