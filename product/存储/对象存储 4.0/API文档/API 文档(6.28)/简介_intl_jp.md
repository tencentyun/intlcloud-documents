Tencent Cloud COSは、軽量で接続状態のないAPIであるXML APIを使用しています。このAPIを呼び出すことで、HTTP/HTTPSを介して直接リクエストを送信し、および応答を受け入れ、Tencent Cloud COSのアプリケーションサーバーとの対話を実現します。

さまざまなデータ転送フレームワークが使用されているため、COSはクラウドAPIに依存しないAPIと独立したSDKを提供します。COSの[API操作リスト](https://cloud.tencent.com/document/product/436/10111)に直接アクセスして参照するか、または、COSの[SDKリスト](https://cloud.tencent.com/document/product/436/6474)にアクセスして、必要なSDKをダウンロードします。クラウドAPIのガイドおよび対応するSDKには、COSの操作機能が含まれていません。

>!
>- COSの利用可能な地域（Region）の詳細については、[地域およびアクセスドメイン名](https://cloud.tencent.com/document/product/436/6224)ドキュメントを参照してください。 
>- APIまたはSDKを使用してリクエストを開始する前に、[リクエストの作成概要](https://cloud.tencent.com/document/product/436/31315)ドキュメントを読んで、アクセスを開始したドメイン名、セキュリティ認証の概念、およびプライベート/パブリックネットワークのアクセスチェックなどの情報を理解することをお勧めします。
>- COSはXMLおよびJSONという2つの異なるバージョンのAPIがあり、2つのバージョンのAPIプロトコルは同じではありませんが、アクセスデータは相互運用可能です。
>- Tencent Cloudは、XML APIを使用することをお勧めします。JSON APIの履歴バージョンでは、2018年以降に発行する新機能は提供されなくなります。

## 用語情報
本文に現れる主な概念と用語：
<style rel="stylesheet">
table th:nth-of-type(1) {
width: 150px;	
}
table th:nth-of-type(2) {
width:550px;	
}
</style>

|名称|	説明|
|---|---|
| APPID	|開発者がCOSサービスにアクセスするときに所有するユーザーディメンションの一意のリソース識別子。これはリソースを識別するために使用されます|
| SecretId | ID認証用の開発者所有のプロジェクト識別ID|
| SecretKey	| 開発者所有のプロジェクトID暗号鍵|
| Bucket|	 COSにあるデータを保存するためのコンテナ|
| Object|	 COSに保存されている具体的なファイルは、ストレージの基本エンティティです|
| Region|	ドメイン名の地域情報。列挙値については、ap-beijing、ap-hongkong、eu-frankfurtなどの[利用可能な地域](https://cloud.tencent.com/document/product/436/6224)のドキュメントを参照してください |
| ACL |	アクセス制御リスト（Access Control List）は特定のバケットまたはオブジェクトのアクセス制御情報のリストを指します|
| CORS | CORS（Cross-Origin Resource Sharing）は、<br>リクエストが発信されたリソースのドメインは、該当リクエストが指向するリソースのドメインにあるHTTPリクエストとは異なります|
| Multipart Uploads |マルチパートアップデート、Tencent cloud COSサービスはファイルをアップロードするためのマルチパートアップロードモードを提供します|

## クイックスタート

Tencent Cloud COS APIを使用するには、次のステップを実行する必要があります：

1. Tencent Cloud COSサービスを購入します
2. Tencent Cloud [COSコンソール](https://console.cloud.tencent.com/cos5)で1つのバケットを作成します
2. CAMコンソールの[クラウドAPI暗号鍵](https://console.cloud.tencent.com/capi)ページにアクセスして、APPID、SecretId、SecretKey内容を取得します
2. リクエスト署名アルゴリズムプログラムを作成します（またはあらゆる種類のサーバーSDKを使用します）
3. 署名を計算し、APIを呼び出して操作を実行します

## 履歴バージョンAPI
[履歴バージョンAPI概要](https://cloud.tencent.com/document/product/436/6052)を確認してください。

