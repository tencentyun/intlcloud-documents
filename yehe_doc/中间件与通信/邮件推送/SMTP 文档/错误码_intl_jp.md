## 入力パラメータ
| ドメイン名                        | 意味        | 備考                                                                                                                               |
| ------------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Bcc                       | Bccアドレス      | 現在サポートされていません                                                                                                                            |
| Cc                        | Ccアドレス      | 現在サポートされていません                                                                                                                            |
| Content-Transfer-Encoding | コンテンツ転送エンコード | 現在使用されていません。添付ファイル内容以外の他のコンテンツを暗号化する必要はありません                                                                                                    |
| Content-Type              | コンテンツタイプ     | 現在、text/plain; charset=UTF-8,text/html; charset=UTF-8 multipart/mixed, multipart/related とmultipart/alternativeのいずれかを渡す必要があります。それ以外を渡すとエラーが報告されます |
| Date                      | 日付と時刻     | 現在使用されていません                                                                                                                           |
| Delivered-To              | 送信アドレス      | 現在使用されていません                                                                                                                           |
| From                      | 送信者アドレス     | 渡す必要があります                                                                                                                               |
| Message-ID                | メッセージID     | 現在使用されていません                                                                                                                           |
| MIME-Version              | MIMEバージョン   | 現在使用されていません。渡さないか、1.0を渡します。そうでない場合、エラーが報告されます                                                                                                            |
| Received                  | 伝送パス      | 現在使用されていません                                                                                                                           |
| Reply-To                  | 返信アドレス      | 現在使用されていません                                                                                                                           |
| Return-Path               | 返信アドレス      | 現在使用されていません                                                                                                                           |
| Subject                   | 件名        | 渡す必要があります                                                                                                                               |
| To                        | 受信者アドレス     | 渡す必要があります                                                                                                                               |

### 添付ファイルパートのパラメータ（添付ファイルを送信する場合）
| ドメイン名                        | 意味        | 備考                             |
| ------------------------- | --------- | ------------------------------ |
| Content-Type              | コンテンツタイプ     | ファイルをapplication/octet-streamに渡すことをお勧めします  |
| Content-Transfer-Encoding | コンテンツ転送エンコード | 現在、base64の送信のみをサポートしており、それ以外を渡すとエラーが報告されます           |
| Content-Disposition       | コンテンツの配置方法   | 現在、attachmentの送信のみサポートしており、それ以外を渡すと添付ファイルが送信できなくなります |
| Content-ID                | コンテンツID    | 現在サポートされていません                         |
| Content-Location          | コンテンツの位置(パス) | 現在サポートされていません                          |
| Content-Base                | コンテンツベース    | 現在サポートされていません                         |

>?入力パラメータの検証要件は、概ね[送信インターフェース](https://intl.cloud.tencent.com/document/product/1084/39408)と同じです。これには、受信者のメールボックスの数、メール本文のサイズ、添付ファイルの形式、添付ファイルのサイズなどの制限が含まれます。

## リターンパラメータ
SMTPインターフェースにはリターンパラメータがなく、errメッセージのリターンのみをサポートしています。nilが返された場合、インターフェースのコールに成功したことを意味しますが、実際のメッセージの送信は必ずしも成功するとは限りません。メールの送信ステータスの取得については、[メール送信ステータスの取得](https://intl.cloud.tencent.com/document/product/1084/39502)をご参照ください。

## エラーコード
### システムレベルのエラー
1. bodyパートが1行で2000を超えるか、またはそれ以上の場合
`554 5.0.0 Error: transaction failed, blame it on the weather: smtp: too longer line in input stream`またはその他`too longer`のログが含まれます。
`write tcp *.*.*.*:60575->*.*.*.*:25: write: broken pipe`

2. 添付ファイルサイズが大きすぎる場合
添付ファイルが約9Mの場合、EOFが返されます。添付ファイルの合計サイズは8M未満で、メッセージ全体のサイズは10Mを超えないようにすることをお勧めします。超えた場合、コンテンツが切り捨てられ、base64デコードの失敗など、その他の異常なエラーが報告されます。
				
### ビジネスレベルのエラー
ビジネスエラーレポートの形式は次のとおりです。
`
554 5.0.0 Error: transaction failed, blame it on the weather: ##SES-response-json: {"Response":{"RequestId":"bee4e9fb-8127-48cc-b606-bbb1e801596b","QcloudError":{"Error":{"Code":"FailedOperation.MissingEmailContent.操作に失敗しました。送信コンテンツが足りません（TemplateDataとSimpleを同時に空にすることはできません)。
`
 `##SES-response-json:`の後は、送信インターフェースによって返される構造体の`json`形式です。フィールドの説明は次のとおりです。

| フィールド          | フィールドタイプ   | 意味    |
| ----------- | ------ | ----- |
| RequestId   | string | リクエストLD  | 
| QcloudError | stuct  | エラー構造体 | 

QcloudError:

| フィールド          | フィールドタイプ   | 意味    | 
| ----------- | ------ | ----- | 
| Code   | string | エラーコード  | 
| Message | string  | エラー情報 | 



一般的なビジネスエラーの説明は次のとおりです。

| エラーコード                                | エラーの説明                                                               | 備考                                    |
| ---------------------------------- | ------------------------------------------------------------------ | ------------------------------------- |
| FailedOperation                    | msg.From is null                                                   | 送信者が空です                                 |
| FailedOperation                    | msg.Subject is null                                                | 送信件名が空です                                |
| FailedOperation                    | msg.Body is null                                                   | 送信コンテンツが空です                                |
| FailedOperation                    | Content-Transfer-Encoding must in...                               | 添付ファイルのContent-Transfer-Encodingをチェックし、入力パラメータの説明をご参照ください |
| FailedOperation                    | Content-Type must in...                                            | HeaderのContent-Typeをチェックし、入力パラメータの説明をご参照ください         |
| FailedOperation                    | Mime-Version must in...                                            | HeaderのMime-Versionをチェックし、入力パラメータの説明をご参照ください         |
| FailedOperation                    | The email is too large. Remove some content...                     | 添付ファイル以外のメール本文は1M以下とします                     |
| FailedOperation                    | Incorrect attachment content. Make sure the base64 content is...   | 添付ファイルのコンテンツはbase64で暗号化されている必要があります                       |
| FailedOperation                    | The attachments are too large. Make sure they do not exceed the... | 1つの添付ファイルが5Mを超えています。またはすべての添付ファイルのサイズが10Mを超えています（具体的なサイズは調整される場合があります）      |
| RequestLimitExceeded.SmtpRateLimit | smtp sending frequency limit...                                    | SMTPコールレート制限をトリガーします                          |

### その他のビジネスエラー
エラーコードの説明は、[メールの送信](https://intl.cloud.tencent.com/document/product/1084/39408)をご参照ください。
