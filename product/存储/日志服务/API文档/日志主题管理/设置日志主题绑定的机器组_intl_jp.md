## 機能説明

このAPIは、ログトピックにバインディングされているサーバーグループ関連情報を設定するために使用されます。

## リクエスト

### リクエスト例

```
PUT /topic/machinegroup?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <Authorization String>
Content-Type: application/json
{  
	"machine_groups": ["xxxxxx-xx-xx-xx-yyyyyyyy"]
}
```

### リクエストライン

```
PUT /topic/machinegroup
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。 

### リクエストパラメータ

| フィールド名   | タイプ   | 場所  | 必須項目 | 意味            |
| -------------- | ----------------- | ----- | -------- | ---------------------------- |
| topic_id       | string            | query | はい        | 照合するログトピックID |
| machine_groups | JsonArray（string） | body  | はい       | ログトピックがバインディングされているサーバーグループID配列 |

## 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Length: 0
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。 

### 応答パラメータ

なし。

### エラーコード

[エラーコード](https://cloud.tencent.com/document/product/614/12402)ドキュメントを参照してください。

