## 背景

本文では、主にTencent CloudオブジェクトストレージCOSに基づいて、モバイルアプリケーションのファイル転送機能を迅速に実現する方法を説明します。サーバーにおいて、詳細を気にすることなく、アクセス暗号鍵を生成して管理するだけで、ファイルデータはTencent Cloud COSに保存できます。

## アーキテクチャ

クライアントアプリケーションの場合、永続暗号鍵をクライアントコードに配置すると、暗号鍵情報が漏洩しやすいだけでなく、ユーザーのアクセス権限に対する制御も不便になります。一時暗号鍵つきでリクエストすることをお勧めします。一時的にストレージリソースにアクセスすることをAppに許可し、永続暗号鍵を漏洩することができなくなります。暗号鍵の有効期限はユーザーが指定し、有効期限が切れると自動的に無効になります。

COSモバイル端末のSDK（Android/IOS）は、一時暗号鍵によるライセンス要求をサポートしており、アプリケーションサーバーで一時暗号鍵のサービスを構築するだけで、端末のCOSリクエストをシームレスに認証できます。

### アーキテクチャ図
全体的なアーキテクチャ図は次のようになります。
![CAMへのCOSアクセスアーキテクチャ図](http://mc.qcloudimg.com/static/img/b1e187a9ec129ffc766c07a733ef4dd6/image.jpg)

そのうち：

- ユーザークライアント：ユーザー携帯アプリ。
- COS：[Tencent Cloud COS](https://cloud.tencent.com/product/cos)で、Appによりアップロードされたデータを保存します。
- CAM：[Tencent Cloudアクセスマネジメント](https://cloud.tencent.com/product/cam)で、COSの一時暗号鍵の生成のために使われます。
- アプリケーションサーバー：ユーザー独自のアプリケーションサーバーであり、ここで一時暗号鍵を取得してアプリケーションAppに返すことに用いられます。

## 準備

### bucketの作成

[COSコンソール](https://console.cloud.tencent.com/cos5/bucket)でバケットを作成します。ニーズに応じて、バケットの権限をプライベート読み書きまたはパブリック読み取り・プライベート書き込みに設定します。

### 永続暗号鍵の取得

永続暗号鍵により一時暗号鍵が生成されます。[API暗号鍵の管理](https://console.cloud.tencent.com/cam/capi)にログインして取得してください。以下の内容が含まれています。

- SecretId
- SecretKey
- AppID

## 一時暗号鍵サービスの構築

セキュリティ上の理由から、署名に一時暗号鍵を使用するには、サーバーで一時暗号鍵サービスを構築し、クライアントで使用するためのAPIを提供する必要があります。具体的な構築手順については、[一時暗号鍵の生成と使用ガイド](https://cloud.tencent.com/document/product/436/14048)を参照してください。

>! 正式に配備する際に、サーバーにはサイト自身の権限検査を追加してください。

### 適切な権限の選択

最小権限の原則に従って、ニーズに応じてPolicyで一時暗号鍵の権限範囲を制御することをお勧めします。サーバーは完全な読み取り・書き込み権限を持つ暗号鍵を送信します。一旦攻撃されると、他のユーザーのデータが漏洩する可能性があります。具体的な構成方法は、[一時暗号鍵の生成と使用ガイド](https://cloud.tencent.com/document/product/436/14048)を参照してください。

## SDKの認証サービスへのアクセス

### Android

一時暗号鍵サービスを構築したら、SDKを認証サービスにアクセスする必要があります。SDKはリクエストの同時実行数を制御し、有効な暗号鍵をローカルにキャッシュし、鍵が期限切れになった後に再度リクエストするため、取得した暗号鍵を自分で管理する必要はありません。

#### 標準なレスポンダー認証

STS SDKから取得したJSONデータを一時暗号鍵サービスのレスポンダーとして直接使用する場合（cossignではこの方法が使用されています）、下記のコードでCOS SDKの認証クラスを作成できます。

```
CosXmlServiceConfig cosXmlServiceConfig = ...;

/**
 *認証サービスのurlアドレスの取得
 */
URL url = null; //アプリケーションサーバー承認サービスのURLアドレス
try {
    url = new URL("your_auth_server_url");
} catch (MalformedURLException e) {
    e.printStackTrace();
}

/**
 * {@link QCloudCredentialProvider}オブジェクトの初期化を通じて、SDKに一時暗号鍵を提供します。
 */
QCloudCredentialProvider credentialProvider = new SessionCredentialProvider(new HttpRequest.Builder<String>()
                .url(url)
                .method("GET")
                .build());

CosXmlService cosXmlService = new CosXmlService(this, cosXmlServiceConfig, credentialProvider);                
```
>?この方式では署名の開始時間は携帯電話のローカル時間であるため、携帯電話のローカル時間のずれが大きい（10分以上である）場合、署名エラーが発生する可能性があります。この場合、以下のカスタマイズレスポンダー認証を利用することになります。

#### カスタマイズレスポンダー認証

一時暗号鍵サービスのHTTP応答ボディをカスタマイズすること、ユーザー携帯の大きいなローカル時間ずれによる誤った署名を回避するため、端末からサーバーへ返した時間を署名の開始時間として使用すること、または、他のプロトコルを使って端末とサーバーの間で通信することなど、より柔軟性を取りたい場合は、`BasicLifecycleCredentialProvider`クラスを継承してその`fetchNewCredentials()`を実現することができます：

まず、1つの `MyCredentialProvider` クラスを定義します：

```java
public class MyCredentialProvider extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials() throws QCloudClientException {

        // まず、あなたの一時暗号鍵サーバーから署名情報を含む応答を取得します
        ....

        // それから応答を解析して暗号鍵情報を取得します
        String tmpSecretId = ...;
        String tmpSecretKey = ...;
        String sessionToken = ...;
        long expiredTime = ...;

        // サーバーへ返した時間は署名の開始時刻とします
        long beginTime = ...;

        // todo something you want

        // 最後一時暗号鍵情報オブジェクトを返した
        return new SessionQCloudCredentials(tmpSecretId, tmpSecretKey, sessionToken, beginTime, expiredTime);
    }
}
```
定義した`MyCredentialProvider`インスタンスを使用して、リクエストを承認します。

```
CosXmlServiceConfig cosXmlServiceConfig = ...;

/**
 * {@link QCloudCredentialProvider}オブジェクトの初期化を通じて、SDKに一時暗号鍵を提供します。
 */
QCloudCredentialProvider credentialProvider = new MyCredentialProvider();

CosXmlService cosXmlService = new CosXmlService(this, cosXmlServiceConfig, credentialProvider);   
```

完全なサンプルコードは、[Android COS Transfer](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransfer)を参照してください。

AndroidによるCOSへのファイルのアップロードとダウンロードの詳細については、[Android SDKクイックスタート](https://cloud.tencent.com/document/product/436/12159)を参照してください。

### iOS

一時署名の取得と管理を容易にするために、QCloudCredentailFenceQueueを提供します。QCloudCredentailFenceQueueはフェンスメカニズムを提供しています。つまり、QCloudCredentailFenceQueueを使用して署名を取得する場合、署名を取得する必要があるすべてのリクエストは署名完了後に実行するため、非同期プロセスを自分で管理する必要はなくなります。

QCloudCredentailFenceQueueを使用するには、1つのインスタンスを生成する必要があります。

```
 //AppDelegate.m
//AppDelegateはQCloudCredentailFenceQueueDelegateプロトコルに従う必要があります。
//
- (BOOL)application:(UIApplication * )application didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {
    // init step
    self.credentialFenceQueue = [QCloudCredentailFenceQueue new];
    self.credentialFenceQueue.delegate = self;
    return YES;
}

```

そしてQCloudCredentailFenceQueueクラスの呼び出しはQCloudCredentailFenceQueueDelegateに従い、プロトコルで定義されるメソッドを実現します。

```
 - (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
```

QCloudCredentailFenceQueueを使って署名を取得するとき、署名が必要とされるSDKのすべてのリクエストは、このプロトコルで定義されるメソッドにより署名に必要なパラメータを取得し有効な署名を生成した後に実行されます。下の例を参照してください。

```
- (void)fenceQueue:(QCloudCredentailFenceQueue *)queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock {
    QCloudHTTPRequest* request = [QCloudHTTPRequest new];
    request.requestData.serverURL = @“your sign service url”;//リクエストのURL

    [request setConfigureBlock:^(QCloudRequestSerializer *requestSerializer, QCloudResponseSerializer *responseSerializer) {
        requestSerializer.serializerBlocks = @[QCloudURLFuseWithURLEncodeParamters];
        responseSerializer.serializerBlocks = @[QCloudAcceptRespnseCodeBlock([NSSet setWithObjects:@(200), nil],nil),//リターンコードが200以外の場合はエラーを返すことを規定します。
                                                QCloudResponseJSONSerilizerBlock];//返されたデータをJSONフォーマットで解析します。
    }];

    [request setFinishBlock:^(id response, NSError *error) {
        if (error) {
            error = [NSError errorWithDomain:@"com.tac.test" code:-1111 userInfo:@{NSLocalizedDescriptionKey:@"一時暗号鍵が取得されていません。"}];
            continueBlock(nil, error);
        } else {
            QCloudCredential* crendential = [[QCloudCredential alloc] init];
            crendential.secretID = response[@"data"][@"credentials"][@"tmpSecretId"];
            crendential.secretKey = response[@"data"][@"credentials"][@"tmpSecretKey"];
            credential.startDate =[NSDate dateWithTimeIntervalSince1970:@"返されるサーバー時間"]
            crendential.experationDate = [NSDate dateWithTimeIntervalSinceNow:[response[@"data"][@"expiredTime"] intValue]];
            crendential.token = response[@"data"][@"credentials"][@"sessionToken"];;
            QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:crendential];
            continueBlock(creator, nil);

        }
    }];
    [[QCloudHTTPSessionManager shareClient] performRequest:request];
}
```

iOSによるCOSへのファイルのアップロードとダウンロード方法の詳細については、[iOS SDKクイックスタート]()を参照してください。


## ユーザー体験

### Android

<<<<<<< HEAD
[こちらへ](https://cos-terminal-resource-1253960454.cos.ap-shanghai.myqcloud.com/cos-transfer-practice.apk)をクリックすることで、またはAndroidスマホでQRコードをスキャンしてdemoを直接ダウンロードして体験できます。
=======
[こちらへ](https://cos-terminal-resource-1253960454.cos.ap-shanghai.myqcloud.com/cos-transfer-practice.apk)をクリックすることで、またはAndroidスマホでQRコードをスキャンしてdemoを直接ダウンロードして体験できます。
>>>>>>> parent of b3f10c0cd1... Revert "Merge branch 'master' of https://github.com/tencentyun/qcloud-documents"

![](https://cos-terminal-resource-1253960454.cos.ap-shanghai.myqcloud.com/cos-transfer-practice-download.png)

完全なコードは、[COS Android Demo](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransferPractice)を参照してください。

### iOS

iOSの完全なサンプルプロジェクトは、[COS iOS Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/OOTB-XML)を参照してください。

QCloudCOSXMLDemo/QCloudCOSXMLDemo/TestCommonDefine.hファイルを変更し、AppIDおよび一時暗号鍵を取得できる前に構成したアドレスを入力して、次のコマンドを実行します。

```sh
pod install
```

コマンドを実行した後、QCloudCOSXMLDemo.xcworkspaceを開くとDemo体験に入ります。
