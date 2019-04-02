## 機能説明

このAPIは、指定されたログトピックの下にあるログカーソルを取得し、かつダウンロードするために使用されます。

## リクエスト

### リクエスト例

```
GET /cursor?topic_id=xxxxxxxx-xxxx-xxxx-xxxx&start=2017-12-28%2014%3A13%3A00 HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### リクエストライン

```
GET /cursor
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名        |  タイプ  | 場所  |必須項目 |      意味                                      |
|--------------|--------|------|--------|-----------------------------------------------|
| topic_id     | string | query| はい     |ログトピックのID                                     |
| start        | string | query| はい     |ログの開始時刻、数分から正確です。フォーマット：YYYY-mm-dd HH:MM:SS  |

## 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 23

{
    "cursor": "1212ssssxxxxxx"
}
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### 応答パラメータ

|  フィールド名      |  タイプ                | 必須項目 |        意味                    |
|-------------|----------------------|---------|-------------------------------|
| cursor      | string               | はい      | カーソル                           |

## エラーコード

詳細については、[エラーコード](https://cloud.tencent.com/document/product/614/12402)を参照してください。

