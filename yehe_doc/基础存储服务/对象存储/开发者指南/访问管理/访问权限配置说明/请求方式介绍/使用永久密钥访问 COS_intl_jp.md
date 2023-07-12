## 背景の説明

RESTful APIによって、Cloud Object Storage（COS）に対しHTTP匿名リクエストまたはHTTP署名リクエストを送信することができます。匿名リクエストは一般的に、静的ウェブサイトのホスティングなどの、パブリックアクセスを必要とするケースに用いられます。そのほかの大多数のケースでは署名リクエストが必要となります。

署名リクエストは匿名リクエストより、署名値を1つ多く持っています。署名はキー（SecretId/SecretKey）およびリクエスト情報を暗号化して生成した文字列をベースとしたものです。SDKは署名を自動計算しますので、お客様はユーザー情報の初期化の際にキーを設定しさえすれば、署名の計算について気にする必要はありません。RESTful APIを通じて送信するリクエストには、署名アルゴリズムに基づいて計算した署名を追加する必要があります。

## パーマネントキーの取得

パーマネントキーはCAMコンソールの[APIキー管理](https://console.cloud.tencent.com/cam/capi)ページで取得できます。パーマネントキーにはSecretIdとSecretKeyが含まれ、アカウントの永続的なIDを表します。有効期限はありません。
- SecretId：APIを呼び出した人のID識別に用いられます。
- SecretKey：署名文字列の暗号化およびサーバーによる署名文字列の検証に用いられるキーです。


## パーマネントキーを使用したCOSアクセス

### APIリクエストによるCOSアクセス

APIリクエストを使用する場合、プライベートバケットの場合は必ず署名リクエストを使用しなければなりません。パーマネントキーで署名を生成し、Authorizationヘッダーに追加することで、署名リクエストを作成できます。リクエストをCOSに送信すると、COSは署名とリクエストが一致しているかを検証します。

>? 署名生成のアルゴリズムは複雑なため、SDKを直接使用してリクエストを送信することで、このプロセスを省略することをお勧めします。
>

1. パーマネントキーによる署名生成
署名アルゴリズムの説明については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)のドキュメントをご参照ください。COSは署名生成ツールもご提供しており、SDKで署名を生成することもできます。[SDKの署名実装](https://intl.cloud.tencent.com/document/product/436/7778#sdk-.E7.AD.BE.E5.90.8D.E5.AE.9E.E7.8E.B0)をご参照ください。ご自身でプログラムを作成して署名を生成することも可能ですが、署名アルゴリズムは複雑なため、通常その方法は推奨されません。
2. Authorizationヘッダーの入力
APIリクエストを送信する際、署名を標準Http Authorizationヘッダーに入力します。次はGetObjectリクエストの例です。
```
GET /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: q-sign-algorithm=sha1&q-ak=SecretId&q-sign-time=KeyTime&q-key-time=KeyTime&q-header-list=HeaderList&q-url-param-list=UrlParamList&q-signature=Signature
```

### SDKツールによるCOSアクセス

1. パーマネントキーによるID情報の初期化
SDKツールのインストールが完了した後、最初にユーザーのID情報の初期化が必要です。ルートアカウントまたはサブアカウントのパーマネントキー（SecretIdおよびSecretKey）を入力します。
2. SDKを直接使用するCOSリクエスト
初期化すると、SDKツールを使用してアップロード・ダウンロードなどの基本操作を直接行うことができるようになります。SDKツールがお客様の代わりにキーによって署名を生成し、COSにリクエストを送信するため、APIリクエストのようにご自身で署名を生成する必要はありません。

例えば、Java SDKのコードは次のようになります。その他の言語のdemoについては、[SDKの概要](https://intl.cloud.tencent.com/document/product/436/6474)のクイックスタートドキュメントをご参照ください。
```
// 1 ユーザーID情報（secretId、secretKey）を初期化します。
// SECRETIDおよびSECRETKEYについてはCAMコンソールhttps://console.cloud.tencent.com/cam/capiで確認および管理を行ってください
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 2 bucketのリージョンを設定します。COSリージョンの略称についてはhttps://cloud.tencent.com/document/product/436/6224をご参照ください
// clientConfigにはregion、https(デフォルトではhttp)、タイムアウト、プロキシなどを設定するsetメソッドが含まれます。使用にあたってはソースコードまたはよくあるご質問のJava SDKのパートを参照できます。
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// ここではhttpsプロトコルの設定と使用を推奨します
// バージョン5.6.54からは、デフォルトでhttpsを使用します
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3 cosクライアントを生成します。
COSClient cosClient = new COSClient(cred, clientConfig);

```


