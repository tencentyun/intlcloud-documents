## 機能説明

このAPIは、指定されたインデックスポリシーの詳細を取得するために使用されます。

## リクエスト

### リクエスト例

```
GET /index?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### リクエストライン

```
GET /index
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

|| フィールド名         |  タイプ  | 場所  |必須項目 |      意味                  |
|---------------|--------|-------|---------|---------------------------|
| topic_id      | string | query | はい      |照合するindexが属するtopic id    |

### 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 153

{
  "topic_id": "yyyy-yy-yy-yy-yyyyyyyy",
  "effective": true,
  "rule": {
    "full_text": {
      "case_sensitive": false
    },
    "key_value": {
      "case_sensitive": false,
      "keys": ["age","name"],
      "types": ["long","text"]
    }
  }
}
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### 応答パラメータ

|  フィールド名     |  タイプ  | 必須項目 |        意味                    |
|------------|--------|---------|-------------------------------|
| topic_id   | string | はい      | インデックス規則が属するtopic id          |
| effective  | bool   | はい      | 有効かどうか                       |
| rule       | object | いいえ      | インデックス規則。effectiveがtrueの場合に返します|

規則に関する説明：

|  フィールド名     |  タイプ  | 必須項目 |        意味                    |
|------------|--------|---------|-------------------------------|
| full_text  | object | いいえ      | フルテキストインデックス関連構成              |
| key_value  | object | いいえ      | kvインデックス関連構成|

full_textに関する説明：

|  フィールド名     |  タイプ  | 必須項目 |        意味                    |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | はい      | テーブル名の大文字と小文字を区別するかどうかを指定します              |

key_valueに関する説明：

|  フィールド名     |  タイプ  | 必須項目 |        意味                    |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | はい      | テーブル名の大文字と小文字を区別するかどうかを指定します              |
| keys | array(string) | はい      | インデックス付けが必要なkeyの名前              |
| types| array(string) | はい      | 上記のkeyに対応するタイプです。1対1対応、現時点では、```long double text```がサポットされます  |

## エラーコード

詳細については、[エラーコード](https://cloud.tencent.com/document/product/614/12402)を参照してください。

