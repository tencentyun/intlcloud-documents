## 機能説明

このAPIはログセットを変更するために使用されます。

## リクエスト

### リクエスト例

```
PUT /logset HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{"logset_id": "xxxx-xx-xx-xx-xxxxxxx","logset_name": "testname","period": 15}
```

### リクエストライン

```
PUT /logset
```

### リクエストヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### リクエストパラメータ

| フィールド名        |  タイプ  | 場所  | 必須項目 |      意味                       |
|--------------|--------|------|---------|--------------------------------|
| logset_id    | string | body | はい      |変更するログセットのID                |
| logset_name  | string | body | いいえ      |ログセットの名、重複できません             |
| period       | int    | body | いいえ      |ログセットの保存期間、単位は日、最大は90日    |

> **注：**
>
logset_nameとperiodの少なくとも一方を提供する必要があります。

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

