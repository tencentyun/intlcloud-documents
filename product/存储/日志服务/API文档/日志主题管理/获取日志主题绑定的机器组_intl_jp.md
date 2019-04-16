## 機能説明

このAPIは、ログトピックにバインディングされているサーバーグループ関連情報を取得するために使用されます。

## リクエスト

### リクエスト例

```
GET /topic/machinegroup?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <Authorization String>
```

### リクエストライン

```
GET /topic/machinegroup
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。 

### リクエストパラメータ

| フィールド名   | タイプ   | 場所  | 必須項目 | 意味             |
| -------- | ------ | ----- | -------- | ---------------- |
|| topic_id | string | query | はい       | 照合するログトピックID |

## 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123
{
	"machine_groups": [
	{
		"group_id": "xxxx-xx-xx-xx-yyyyyyyy",
		"group_name": "testname"},    
		{"group_id": "xxxx-xx-xx-xx-zzzzzzzz", 
		"group_name": "testname1"}
	]
}
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。 

### 応答パラメータ

| フィールド名         | タイプ      | 必須項目 | 意味                     |
| -------------- | --------- | -------- | ------------------------ |
| machine_groups | JsonArray | はい       | ログトピックがバインディングされているサーバーグループ配列 |

machine_groupのフォーマットは次のとおりです：

| フィールド名     | タイプ   | 必須項目 | 意味         |
| ---------- | ------ | -------- | ------------ |
| group_id   | string | はい       | サーバーグループのID   |
| group_name | string | はい       | サーバーグループの名前 |

### エラーコード

[エラーコード](https://cloud.tencent.com/document/product/614/12402)ドキュメントを参照してください。

