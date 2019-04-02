## 機能説明

このAPIは、配信構成を削除するために使用されます。

## リクエスト

### リクエスト例

```
DELETE /shipper?shipper_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```
### リクエストライン

```
DELETE /shipper
```
### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名        |  タイプ  | 場所  | 必須項目 |      意味                       |
|--------------|--------|------|---------|--------------------------------|
| shipper_id   | string | query| はい      |削除する配信構成のidです                  |

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

