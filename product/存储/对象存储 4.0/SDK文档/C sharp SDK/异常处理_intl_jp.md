## 概要

SDK APIを呼び出してCOSサービスをリクエストすることが失敗した場合、システムはCosClientException（クライアント異常）またはCosServerException（サーバー異常）をスローします。
- CosClientExceptionは、クライアントがCOSサーバーと正常に対話できないことによって引き起こされます。例えば、クライアントがサーバーに接続できず、サーバーから返されたデータを解決できず、ローカルファイルの読み取りにIO異常が発生したなどです。
- CosServerExceptionは、クライアントがCOSサーバーと正常に対話しますが、COSリソースの操作が失敗したことを表します。例えば、クライアントが存在しないバケットにアクセスし、存在しないファイルを削除し、ある操作を実行する権限がないなどです。


## クライアント異常

CosClientExceptionはSystem.ApplicationExceptionから統合され、使用方法はSystem.ApplicationExceptionと同じであり、同時に追加のメンバーerrorCodeを添加し、以下に示すとおりです：

|メンバー|説明|タイプ|
| ---- | ---- | ---- |
|errorCode|クライアントエラーコード、例えば、10000はパラメータ検証が失敗したことを表します|int|



## サーバー異常

CosServerExceptionは、サーバーから返されたステータスコード、requesttid、エラーの詳細などを含みます。異常をキャプチャした後、必要なトラブルシューティング要因を含む異常全体を印刷することをお勧めします。以下は、異常メンバー変数の説明です：

| メンバー   | 説明 | タイプ |
| ------------ | ---------------------------------------- | --------- |
| requestId    | リクエストIDであり、リクエストを表すために使用され、トラブルシューティングに非常に重要です。| string    |
| statusCode   | 応答のステータスコードであり、4xxはクライアントによるリクエストの失敗を指し、5xxはサーバー異常による失敗です。詳細については、[COSエラー情報](https://cloud.tencent.com/document/product/436/7730)を参照してください。 | string    |
| errorCode | リクエストが失敗した時にボディにより返されたError Code、詳細については、[COSエラーメッセージ](https://cloud.tencent.com/document/product/436/7730)を参照してくだい| string |
| errorMessage | リクエストが失敗した時にボディにより返されたError Message、詳細については、[COSエラーメッセージ](https://cloud.tencent.com/document/product/436/7730)を参照してくだい| string |


