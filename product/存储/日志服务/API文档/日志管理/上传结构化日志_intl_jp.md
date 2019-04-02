## 機能説明

このAPIは、指定されたログトピックにログをアップロードするために使用されます。

## リクエスト

### リクエスト例

```
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf

<LogGroupListのコンテンツはpdのフォーマットとしてパッケージ化されています>
```
#### PB説明ファイル

```
package cls;
message Log
{
    message Content
    {
        required string key   = 1;
        required string value = 2;
    }
    required int64   time     = 1; // UNIX Time Format
    repeated Content contents = 2;
}
message LogGroup
{
    repeated Log    logs        = 1;
    optional string contextFlow = 2; //コンテキストの一貫性を保つために使用されるUID
    optional string filename    = 3; //ファイル名
    optional string source      = 4; //ログソース、通常はサーバーIPです。
}
message LogGroupList
{
    repeated LogGroup logGroupList = 1;
}
```

### リクエストライン

```
POST /structuredlog
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名        |  タイプ  | 場所  |必須項目 |      意味                                      |
|--------------|--------|------|--------|-----------------------------------------------|
| topic_id     | string | query| はい     |ログに報告されたログトピック ID                            |
| logGroupList | message|  pb | はい     |ログコンテンツ関連                                     |

LogGroupの説明：

| フィールド名        |      意味                                      |
|--------------|-----------------------------------------------|
| logs         |ログコンテンツ                                        |
| contextFlow  |コンテキストの一貫性を保つために使用されるUID                                |
| filename     |ファイル名                                          |
| source       |ログソース、通常はサーバーIPです。                          |

Log説明：

| フィールド名        |      意味                                      |
|--------------|-----------------------------------------------|
| time         |ログ時間、UNIXタイムスタンプ（秒単位）。一部の言語ではミリ秒単位の時間が返されるので、変換する必要があることに注意してください。 |
| contents     |ログコンテンツ                                        |

コンテンツの説明：

| フィールド名        |      意味                                      |
|--------------|-----------------------------------------------|
| key          |フィールドのキー、```_```で始めることができません                    |
| value        |フィールドの値                                        |

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

