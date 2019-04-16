## 機能説明

このAPIは、配信タスク情報のリストを取得するために使用されます。

## リクエスト

### リクエスト例

```
GET /tasks?shipper_id=xx-xx-xx-xxxx&start_time=2017-10-10+00%3A00%3A00&end_time=2017-10-10+23%3A59%3A59 HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
```

### リクエストライン

```
GET /tasks
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名        |  タイプ  | 場所  | 必須項目 |      意味                      |
|--------------|--------|------|---------|---------------------------------|
| shipper_id   | string | query| はい      |照合する配信規則idです                  |
| start_time   | string | query| はい      |照合の開始時刻です。過去3日間の照合をサポートします  |
| end_time     | string | query| はい      |照合の終了時刻です                     |

## 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "tasks": [
    {
      "task_id": "xxxxx-xx-xx-xx",
      "shipper_id": "xxxxx-xx-xx-xx",
      "topic_id": "xxxxx-xx-xx-xx",
      "range_start": "2017-10-17 10:10:10",
      "range_end": "2017-10-17 10:10:10",
      "start_time": "2017-10-17 10:10:10",
      "end_time": "2017-10-17 10:10:10",
      "status": "success",
      "message": "success",
    }
  ]
}
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### 応答パラメータ

|  フィールド名      |  タイプ     | 必須項目 |        意味                    |
|-------------|-----------|---------|-------------------------------|
| tasks       | JsonArray | はい      | 配信タスク情報配列です                |

TaskInfoのフォーマットは次のとおりです：

|  フィールド名     |  タイプ  | 必須項目 |        意味                    |
|------------|--------|---------|-------------------------------|
| task_id    | string | はい      | 配信タスクのIDです                |
| shipper_id | string | はい      | 配信規則のIDです                |
| topic_id | string | はい   | ログトピックのIDです                |
| range_start| string | はい      | 配信されたこのログのバッチの開始時刻です         |
| range_end  | string | はい      | 配信されたこのログのバッチの終了時刻です         |
| start_time | string | はい      | この配信タスクの開始時刻です           |
| end_time   | string | はい      | この配信タスクの終了時刻です           |
| status     | string | はい      | この配信タスクの結果：「success」、「running」、「failed」、「wait」 |
| message    | string | はい      | 結果の詳細な情報です                  |

## エラーコード

詳細については、[エラーコード](https://cloud.tencent.com/document/product/614/12402)を参照してください。

