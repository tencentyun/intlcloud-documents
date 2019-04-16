## 機能説明

このAPIは、既存のインデックスタスクを変更するために使用されます。

## リクエスト

### リクエスト例

```
PUT /index HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
  "topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
  "effective": true,
  "rule": {
    "full_text": {
      "case_sensitive": false,
      "tokenizer": "{^&%"
    },
    "key_value": {
      "case_sensitive": false,
      "keys": ["age","name"],
      "types": ["long","text"],
      "tokenizers": ["","-"]
    }
  }
}

```

### リクエストライン

```
PUT /index
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名        |  タイプ  | 場所  |必須項目 |      意味                                      |
|--------------|--------|------|--------|-----------------------------------------------|
| topic_id     | string | body | はい      |変更するindexが属するtopic id                      |
| effective    | bool   | body | はい      |indexの切り替え状態                                |
| rule         | object | body | いいえ      |インデックス規則。effectiveがtrueの場合に必要です               |


規則に関する説明：

|  フィールド名     |  タイプ  | 必須項目 |        意味                    |
|------------|--------|---------|-------------------------------|
| full_text  | object | いいえ      | フルテキストインデックス関連構成              |
| key_value  | object | いいえ      | kvインデックス関連構成|
> **注：**
>
> ruleを設定するときは、full_textとkey_valueの少なくとも一方を指定する必要があります。

full_textに関する説明：

|  フィールド名     |  タイプ  | 必須項目 |        意味                    |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | はい      | テーブル名の大文字と小文字を区別するかどうかを指定します              |
| tokenizer | string | いいえ      | フルテキストインデックスの区切り文字              |

key_valueに関する説明：

|  フィールド名     |  タイプ  | 必須項目 |        意味                    |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | はい      | テーブル名の大文字と小文字を区別するかどうかを指定します              |
| keys | array(string) | はい      | インデックス付けが必要なkeyの名前            |
| types| array(string) | はい      | インデックス付けが必要なkeyに対応するタイプです。1対1対応、現時点では、```long double text```がサポットされます |
| tokenizers| array(string) | いいえ      | 上記のkeyに対応する区切り文字です。1対1対応、```text```タイプのみ適用可能で、他のタイプは空の文字列です  |

## 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0

```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### 応答パラメータ

なし

## エラーコード

詳細については、[エラーコード](https://cloud.tencent.com/document/product/614/12402)を参照してください。

