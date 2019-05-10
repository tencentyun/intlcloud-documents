##　概要

この文章では、リクエストがエラーの場合、返されたエラーコードと対応するエラーメッセージを紹介します。

## エラーメッセージの戻りフォーマット

### 戻りヘッダー

Content-Type：application/xml

対応HTTPステータスコード：3XX、4XX、5XX

### 返し内容

**文法フォーマット**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<Error>
  <Code>[エラーコード]</Code>
  <Message>[エラーメッセージ]</Message>
  <Resource>[リソースアドレス]</Resource>
  <RequestId>[リクエストID]</RequestId>
  <TraceId>[エラーID]</TraceId>
</Error>
```
<style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

**要素説明**

| 要素名称      | 説明                                       | タイプ        |
| --------- | ---------------------------------------- | --------- |
| Error     | すべてのエラーメッセージが含まれています。                               | Container |
| Code      | エラーコードは、唯一のエラー条件とエラーシナリオを特定するために使用されます。        | String    |
| Message   | 具体的なエラーメッセージが含まれています。                               | String    |
| Resource  | リソースアドレス：バケットアドレスまたはオブジェクトアドレス。                 | String    |
| RequestId | リクエストが送信されるとき、サーバーはリクエストのために唯一のIDを自動的に生成します。request-idは、問題が発生したときにCOSが問題をより迅速に特定するのに役立ちます。 | String    |
| TraceId   | リクエストにエラーがある場合、サーバーはこのエラーのために唯一のIDを自動的に生成します。trace-idは、問題が発生したときにCOSが問題をより迅速に特定するのに役立ちます。リクエストにエラーがある場合、trace-idはrequest-idに1つずつ対応します。 | String    |

## エラーコードリスト

**3XXタイプエラー**

| エラーコード               | 説明                                       | HTTPステータスコード               |
| ----------------- | ---------------------------------------- | --------------------- |
| PermanentRedirect | リソースの位置は恒久的に変更されています。正しい新場所にリダイレクトするには、HTTP Locationを使用してください | 301 Moved Permanently |
| TemporaryRedirect | リソースの位置は一時的に変更されています。正しい新場所にリダイレクトするには、HTTP Locationを使用してください | 302 Moved Temporarily |
| Redirect          | 一時リダイレクト                                    | 307 Moved Temporarily |
| TemporaryRedirect | DNSアップデート中は、一時的にリダイレクトされます                        | 307 Moved Temporarily |

**4XXタイプエラー**

| エラーコード                                 | 説明                                | HTTPステータスコード                             |
| ----------------------------------- | --------------------------------- | ----------------------------------- |
| InvalidSHA1Digest                        | リクエスト内容sha1検証は不正です                        | 400 Bad Request  |
| NoSuchUpload                        |	マルチパートアップロードとき、指定されたuploadidが存在していません                    | 400 Bad Request  |
| InvalidPart                         |  パートが欠落しています                                       | 400 Bad Request  |
| InvalidPartOrder                      | マルチパートアップロードの番号が連続していません                               | 400 Bad Request  |
| ObjectNotAppendable                  | 指定されたファイルが追加できません                               | 400 Bad Request  |
| AppendPositionErr                     | ファイル長さと追加された位置が一致していません                 | 400 Bad Request  |
| NoSuchVersion                        | 指定されたバージョンが存在していません                                   | 400 Bad Request  |
| NoLifecycle                          | ライフサイクルが存在していません                                   | 400 Bad Request  |
| PreconditionFailed                   | 前提条件のマッチング失敗                                  | 400 Bad Request  |
| UnexpectedContent                    | リクエストは関連内容をサポートしません                                | 400 Bad Request  |
| MultiBucketNotSupport                 | 地域間コピーは1つだけのターゲットバケットを設定できます                    | 400 Bad Request  |
| NotSupportedStorageClass              | 指定されたストレージタイプが不正です                              | 400 Bad Request  |
| BadDigest                           | 提供されたx-cos-SHA-1値はサーバーで取得されたファイルSHA-1値と一致しません | 400 Bad Request                     |
| EntityTooSmall                      | アップロードされたファイルサイズが必要な最低限サイズより小さくなっています。これはマルチパートアップロードでよく発生します          | 400 Bad Request                     |
| EntityTooLarge                      | アップロードされたファイルサイズが必要な最大限サイズを超えています                   | 400 Bad Request                     |
| ImcompleteBody                      | リクエストされた実際の内容長さは指定されたConent-Lengthとは一致していません            | 400 Bad Request                     |
| IncorrectNumberOfFilesInPostRequest | Postリクエストでは、一度に1つのファイルしかアップロードできません                 | 400 Bad Request                     |
| InlineDataTooLarge                  | インラインデータサイズが必要な最大値を超えています                    | 400 Bad Request                     |
| InvalidArgument                     | リクエストパラメータが不正です                   | 400 Bad Request                     |
| InvalidBucketName                   | バケット名称は不正です                       | 400 Bad Request                     |
| InvalidDigest                       | x-cos-SHA-1値は不正です                   | 400 Bad Request                     |
| InvalidPart                         | パート欠落またはSectionIDエラー                 | 400 Bad Request                     |
| InvalidPolicyDocunment              | ポリシー構成ファイルが不正です                         | 400 Bad Request                     |
| InvalidURI                          | URIが不正です                            | 400 Bad Request                     |
| KeyTooLong                          | カスタマイズヘッダーが長すぎます                            | 400 Bad Request                     |
| MalformedACLError                   | 説明されたACLポリシーはXML文法と一致していません                  | 400 Bad Request                     |
| MalformedPOSTRequest                | 該当POSTリクエストのボディ内容は不正です         | 400 Bad Request                     |
| MalformedXML                        | ボディのXMLフォーマットはXML文法と一致していません                 | 400 Bad Request                     |
| MaxMessageLengthExceeded            | リクエストは長すぎます                              | 400 Bad Request                     |
| MaxPostPreDataLengthExceededError   | 該当POSTリクエストのデータプレフィックスが長すぎます。これはマルチパートアップロードでよく発生します            | 400 Bad Request                     |
| MatadataTooLarge                    | メタデータサイズが必要な最大サイズを超えています                     | 400 Bad Request                     |
| MissingRequestBodyError             | リクエストボディ欠落                          | 400 Bad Request                     |
| MissingSecurityHeader               | 必要なヘッダー欠落                        | 400 Bad Request                     |
| MissingContentMD5             | リクエストヘッダーにはContent-MD5が不足です                         | 400 Bad Request                     |
| MissingAppid                  |   リクエストヘッダーにはAppidが不足です  | 400 Bad Request                     |
| MissingHost                   |  リクエストヘッダーにはHostが不足です    | 400 Bad Request                     |
| RequestIsNotMultiPartContent        | PostリクエストContent-Typeが不正です            | 400 Bad Request                     |
| RequestTimeOut                      | データの読み取りがタイムアウト、ネットワークが遅すぎるか、同時アップロードが大きすぎるかを確認します          | 400 Bad Request           |
| TooManyBucket                       | バケット数は200制限を超えています                       | 400 Bad Request                     |
| UnexpectedContent                   | リクエストは関連内容をサポートしません                         | 400 Bad Request                     |
| UnresolvableGrantByUID              | 提供されたUIDが存在していません                         | 400 Bad Request                     |
| UserKeyMustBeSpecified              | バケットに対するPost操作は明確なパスを指定する必要があります           | 400 Bad Request                     |
| ExpiredToken                       | 署名列は期限切れです                                 | 403 Forbidden                       |
| AccessDenied                        | 署名や権限が正しくありません。アクセスが拒否されます                 | 403 Forbidden                       |
| AccountProblem                     | 利用中のアカウントが今回の操作を拒否しました                       | 403 Forbidden                       |
| InvaildAccessKeyId                  | AccessKeyが存在していません                      | 403 Forbidden                       |
| InvalidObjectState                  | リクエスト内容はオブジェクト属性と一致していません                  | 403 Forbidden                       |
| InvalidSecurity                     | 署名列が不正です                            | 403 Forbidden                       |
| RequestTimeTooSkewed                | リクエスト時間が権限の有効期間を超えました                      | 403 Forbidden                       |
| SignatureDoesNotMatch               | 提供された署名は規則に適合しません                  | 403 Forbidden                       |
| NoSuchBucket                        | 指定されたバケットが存在していません                      | 404 Not Found                       |
| NoSuchUpload                        | 指定されたマルチパートアップロードが存在していません                        | 404 Not Found                       |
| NoSuchBucket                        | 指定されたバケットポリシーが存在していません                      | 404 Not Found                       |
| MethodMotAllowed                    | このリソースはHTTP方法をサポートしません                     | 405 Method Not Allowed              |
| BucketAlreadyExists                 | CreateBucketが指定されたBucketNameがすでに使用されていますので、新しいBucketNameを選択してください               | 409 Conflict                        |
| BucketNotEmpty                      | DeleteBucket前に、ファイルと未完成のマルチパートアップロードタスクを削除してください                    | 409 Conflict                        |
| InvalidBucketState                  | バケットの状態は、操作リクエストと競合します。例えば、マルチバージョン管理と地域間コピーの競合など                 | 409 Conflict                        |
| OperationAborted                    | 指定されたリソースはこのような操作をサポートしていないか、ファイル転送が不完全で破損しているため、ダウンロード時にこのエラーコードが報告されます          | 409 Conflict   |
| MissingContentLength                | Header Content-Length欠落           | 411 Length Required                 |
| PreconditionFailed                  | 前提条件のマッチング失敗                          | 412 Precondition                    |
| InvalidRange                        | リクエストのファイル範囲は不正です                        | 416 Requested Range Not Satisfiable |



**5XXタイプエラー**

| エラーコード                | 説明               | HTTPステータスコード                 |
| ------------------ | ---------------- | ----------------------- |
| InternalErrror     | サーバーの内部エラー          | 500 Internal Server     |
| NotImplemented     | ヘッダーには処理できない方法が存在しています | 501 Not Implemented     |
| ServiceUnavailable | サーバー内部エラー、再試行してください   | 503 Service Unavailable |
| SlowDown           | アクセス頻度を減らしてください          | 503 Slow Down           |

**他のタイプエラー**

| エラーコード                     | 説明         | HTTPステータスコード |
| ----------------------- | ---------- | ------- |
| InvaildAddressingHeader | 匿名ロールを使用してアクセスする必要があります | N/A     |


