## 一時キーの説明

一時キーは、Security Token Service（STS）が提供する一時アクセスのための証明書です。一時キーはTmpSecretId、TmpSecretKey、Tokenの3つの部分から成ります。パーマネントキーと異なり、一時キーには次のような特徴があります。
-	有効期間が短く（30分～36時間）、パーマネントキーを開示する必要がないため、アカウント漏洩のリスクが低くなります。
-	一時キーを取得する際、policyパラメータを渡して一時的な権限を設定することで、使用者の権限の範囲をさらに限定することができます。

このため、一時キーはフロントエンドの直接転送などの、一時的な権限承認のシーンに適します。信頼性の低いユーザーに対しては、パーマネントキーではなく一時キーを発行することで、安全性を高めることができます。

## 一時キーの取得

一時キーは、当社のご提供するCOS STS SDK方式で取得するか、またはSTSのクラウドAPI方式によって直接取得することができます。
詳細については、[一時キーの生成および使用ガイド](https://intl.cloud.tencent.com/document/product/436/14048)をご参照ください。

## 一時キーの権限

一時キーを申請する前に、Cloud Access Management（CAM）ユーザー（Tencent Cloudルートアカウントまたはサブアカウント）を取得しておく必要があります。Policyパラメータを設定することで、一時キーに一時ポリシーを追加して使用者の権限を制限することができます。
- policyパラメータを設定しない場合、取得した一時キーはCAMユーザーと同等の権限を有します。
- policyパラメータを設定した場合、取得した一時キーの権限は、CAMユーザーの権限をベースにして、さらにpolicyで設定した範囲内に制限されます。

例えば、「A」がCAMユーザーの従来の権限を表し、「B」がpolicyパラメータによって一時キーに設定した権限を表すとした場合、「A」と「B」の共通部分が一時キーの最終的に有効な権限となります。

下図のように、CAMユーザー権限とpolicyの一時権限の共通部分が有効な権限です。
![](https://qcloudimg.tencent-cloud.cn/raw/60982ace7d24b98f97210e674fd373a9.png)


下図のように、policyがCAMユーザー権限の範囲内にある場合は、policyが有効な権限となります。
![](https://qcloudimg.tencent-cloud.cn/raw/03b30ed344faa1a9e28a6210810866d1.png)

## 一時キーを使用したCOSアクセス

![](https://qcloudimg.tencent-cloud.cn/raw/0127017176d6014ec8957f47d4858666.png)
一時キーにはSecretId、SecretKey、Tokenが含まれます。各ルートアカウントおよびサブアカウントはいずれも複数の一時キーを生成することができます。パーマネントキーと異なり、一時キーの有効期間は30分から36時間しかありません。一時キーはフロントエンドの直接転送などの、一時的な権限承認のシーンに適します。信頼性の低いユーザーに対しては、パーマネントキーではなく一時キーを発行することで、安全性を高めることができます。詳細については、[一時キーの生成および使用ガイド](https://intl.cloud.tencent.com/document/product/436/14048)および[フロントエンドの直接転送に用いる一時キーの使用ガイド](https://intl.cloud.tencent.com/document/product/436/35265)をご参照ください。

- APIリクエストの送信
パーマネントキーと同じように、一時キーによっても署名を生成することができます。リクエストヘッダーにAuthorizationを入力することで、署名リクエストを作成します。COSはリクエストを受信すると、署名が有効か、および一時キーが有効期間内かどうかをチェックします。
署名アルゴリズムの説明については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)をご参照ください。COSは署名生成ツールもご提供しており、SDKで署名を生成することもできます。[SDKの署名実装](https://intl.cloud.tencent.com/document/product/436/7778#sdk-.E7.AD.BE.E5.90.8D.E5.AE.9E.E7.8E.B0)をご参照ください。
- SDKツールの使用
SDKツールをインストールすると、一時キーを使用してユーザーのID情報を初期化できるほか、一時キー（SecretId、SecretKey、Token）を使用してCOSClientを初期化し、署名を生成せずに、SDKを使用して直接アップロード、ダウンロードなどの操作を行うことができるようになります。一時キーの生成については一時キーの生成および使用ガイドをご参照ください。

Java SDKについては次の例をご参照ください。その他の言語のdemoについては、[SDKの概要](https://intl.cloud.tencent.com/document/product/436/6474)をご参照ください。

```
// 1 取得した一時キー (tmpSecretId、tmpSecretKey、sessionToken)を渡します
String tmpSecretId = "SECRETID";
String tmpSecretKey = "SECRETKEY";
String sessionToken = "TOKEN";
BasicSessionCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// 2 bucketのリージョンを設定します。COSリージョンの略称についてはhttps://cloud.tencent.com/document/product/436/6224をご参照ください
// clientConfigにはregion、https(デフォルトではhttp)、タイムアウト、プロキシなどを設定するsetメソッドが含まれます。ご利用にあたっては、ソースコードまたはよくあるご質問のJava SDKのパートをご参照ください
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// 3 cosクライアントを生成します
COSClient cosClient = new COSClient(cred, clientConfig);
```

## 一時キーのユースケース

一時キーは主に第三者に対しCOSへの一時的なアクセス権限を承認するために用いられます。例えば、ユーザーがクライアントAppを開発し、データをCOSバケットに保存したとします。この場合、パーマネントキーを直接Appクライアント上に置くことはセキュリティ上問題がありますが、クライアントに対してはアップロード・ダウンロードの権限を承認する必要があります。このようなケースでは一時キーを使用することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/0b37dd8a160a065efe68c0fbeea09c3b.png)

上の図のように、ユーザーがAppクライアントを開発し、ユーザーのサーバー上にパーマネントキーを保存し、一時キーを使用してフロントエンド直接転送を行うには次のいくつかの手順が必要です。
1.	Appクライアントからユーザーサーバーに、データアップロード・ダウンロード用の一時キーをリクエストします。
2.	ユーザーサーバーはパーマネントキーのIDを使用して、STSサーバーに一時キーを申請します。
3.	STSサーバーはユーザーサーバーに一時キーを返します。
4.	ユーザーサーバーは一時キーをAppクライアントに送信します。
5.	Appクライアントは一時キーを使用して署名リクエストを生成し、COSに対しデータのアップロード・ダウンロードをリクエストします。

一時キーはフロントエンドデータの直接転送のユースケースに適しています。次のベストプラクティスをご参照の上、一時キーをご利用ください。
- [Web端末直接転送の実践](https://intl.cloud.tencent.com/document/product/436/9067)
- [ミニプログラム直接転送の実践](https://intl.cloud.tencent.com/document/product/436/30934)
- [モバイルアプリケーション直接転送の実践](https://intl.cloud.tencent.com/document/product/436/30618)

