## 機能説明

このAPIは、サーバーグループを変更するために使用されます。

## リクエスト

### リクエスト例

```
PUT /machinegroup HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{"group_id": "xxxx-xx-xx-xx-xxxxxxx", "group_name": "testname", "ips": ["10.10.10.10", "10.10.10.11"]}
```

### リクエストライン

```
PUT /machinegroup
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名        |  タイプ  | 場所  | 必須項目 |      意味                       |
|--------------|--------|------|---------|--------------------------------|
| group_id     | string | body | はい      |変更するサーバーグループのID                |
| group_name   | string | body | いいえ      |サーバーグループの名、重複できません             |
| ips          | JsonArray| body | いいえ      |サーバーグループ下のIPリスト|


>!Group_nameとipsの少なくとも一方を提供する必要があります。

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

[エラーコード](https://cloud.tencent.com/document/product/614/12402)ドキュメントを参照してください。


