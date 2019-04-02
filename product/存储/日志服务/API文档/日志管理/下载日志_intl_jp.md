## 機能説明

このAPIはカーソルを使用してログをダウンロードするために使用されます。

## リクエスト

### リクエスト例

```
GET /log?topic_id=xxxxxxxx-xxxx-xxxx-xxxx&cursor=xxxxxx&count=10 HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
```

### リクエストライン

```
GET /log
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名        |  タイプ  | 場所  |必須項目 |      意味                                      |
|--------------|--------|------|--------|-----------------------------------------------|
| topic_id     | string | query| はい     |ログトピックのID                                     |
| cursor       | string | query| はい     |API「ログカーソルの取得」を介して取得されたカーソル                 |
| count        | string | query| はい     |ダウンロードするログの数、最大1000                      |

## 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Type: application/x-protobuf
Content-Length: 23
x-cls-cursor: xxxxxx
x-cls-count:10

<LogGroupListのコンテンツはpdのフォーマットとしてパッケージ化されています>
```

### 応答ヘッダー

| Header名              |      意味                       |
|------------------------|--------------------------------|
| x-cls-cursor           |次回ログをダウンロードするために使用できる現在のログカーソル  |
| x-cls-count            |現在のリクエストに対してダウンロードされたログの数           |

### 応答パラメータ

LogGroupListオブジェクトのパッケージ化されたコンテンツを返します。pbファイルの説明については、 [構造化ログのアップロード](https://cloud.tencent.com/document/product/614/16873) APIを参照してください。

## エラーコード

[エラーコード](https://cloud.tencent.com/document/product/614/12402)ドキュメントを参照してください。

