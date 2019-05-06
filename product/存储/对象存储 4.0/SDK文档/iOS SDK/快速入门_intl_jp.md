## 開発準備

### SDKの取得 

- COSのiOS SDKアドレス：[XML iOS SDK](https://github.com/tencentyun/qcloud-sdk-ios.git)。   
- パッケージされたFrameworkフォーマットのSDKをダウンロードするには、[realease](https://github.com/tencentyun/qcloud-sdk-ios/releases)から必要なバージョンを選択しダウンロードを行います。
- その他の例についてDemo：[ XML iOS  SDK Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples.git)を参照してください。
- COS XMLバージョンの進化について、[XML iOS  SDK  ChangeLog](https://github.com/tencentyun/qcloud-sdk-ios/blob/master/CHANGELOG.md)を参照してください。

### 開発準備

- SDKは、iOS 8.0以降のバージョンのOSをサポートします。
- 携帯電話はネットワーク（GPRS、3GまたはWi-Fiネットワークなど）があります。
- [COS V5コンソール](https://console.cloud.tencent.com/cos5)からAPPID、SecretId、SecretKeyを取得します。

> ?本書に記載されるSecretID、SecretKey、Bucketなどの名前の意味と取得方法について[COS用語情報](https://cloud.tencent.com/document/product/436/7751)を参照してください。

### SDKの構成

#### SDKのインポート

cocoapodsまたはパッケージされたダイナミックライブラリをダウンロードすることによりSDKを統合します。ここで、cocoapodsによるインポートをお勧めします。

- ** Cocoapodsによるインポート（推奨）**  
  Podfile ファイルに使用されます。

```
  pod 'QCloudCOSXML'
```

- **パッケージされたダイナミックライブラリによるインポート（手動統合方式）**  
  下図のように、**QCloudCOSXML.framework、QCloudCore.frameworkとlibmtasdk.a**をプロジェクトにドラッグします。
  ![](https://main.qcloudimg.com/raw/ce990d8871293daec0aa434f28b152e6.png)  
  依存ライブラリを追加します。

> 1. CoreTelephony
> 2. Foundation
> 3. SystemConfiguration
> 4. libc++.tbd

### プロジェクトの構成

Build SettingsにOther Linker Flagsを設定し、以下のパラメータを追加します。

```shell
-ObjC
-all_load
```

以下の通りです。
![パラメータ構成](https://main.qcloudimg.com/raw/2736ab0172191942e41e3268838a1e88.png)

> !
> - Tencent Cloud COS XML iOSのSDKは、HTTPプロトコルを採用します。iOSでの実行を確保するには、HTTP伝送を有効にする必要があります。
>   以下の2つの方式でHTTP伝送を有効にします。
>  - **手動設定方式**
>   info.plistプロジェクトファイルにApp Transport Security Settingsタイプを追加し、App Transport Security SettingsにAllow Arbitrary Loadsタイプ（Boolean）を追加し、値をYESに設定します。
>  - **コード設定方式**
>   SDKを組み込んだAppのinfo.plistに以下のコードを追加できます。
> ```
>  <key>NSAppTransportSecurity</key>
> <dict>
> <key>NSExceptionDomains</key>
> <dict>
> 	<key>myqcloud.com</key>
> 	<dict>
> 		<key>NSIncludesSubdomains</key>
> 		<true/>
> 		<key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
> 		<true/>
> 	</dict>
> </dict>
> </dict>
> ```
>
> - また、SDKにMobile Tencent Analytics（MTA）機能が導入されています。この機能を無効にするには、以下の方式で設定してください。
>  - ヘッダファイル` #import <QCloudCore/MTAConfig.h>`をインポートします
>  - デフォルトのcosxmlサービスを登録した後、次のコードを追加します。
>   `[TACMTAConfig getInstance].statEnable = NO;`

### 初期化  

SDK機能を使用する前には、必要なヘッダファイルをインポートし、初期化操作を行う必要があります。
SDKをアップロードするためのヘッダファイルを導入します。

```objective-c
QCloudCore.h,    
QCloudCOSXML/QCloudCOSXML.h
```

> !
>
> 1. SDKを使用する前、まずは1つのデフォルトのクラウドサービス構成オブジェクトQCloudServiceConfigurationをインスタンス化し、次はQCloudCOSXMLServiceとQCloudCOSTransferManagerServiceオブジェクトをインスタンス化します。  
> 2. QCloudServiceConfigurationが変更された場合、`registerCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration withKey:(NSString*)key`を使って新しいQCloudCOSTransferManagerServiceを登録できます。ただし、デフォルトのQCloudCOSTransferManagerServiceは1つしかありません。

#### 方法のプロトタイプ

QCloudServiceConfigurationオブジェクトのインスタンス化：

```
 QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
 configuration.appID = @""//プロジェクトID;
```

QCloudCOSXMLServiceオブジェクトのインスタンス化：

```
+ (QCloudCOSXMLService*) registerDefaultCOSXMLWithConfiguration:(QCloudServiceConfiguration*)configuration;
```

QCloudCOSTransferManagerServiceオブジェクトのインスタンス化：

```
+ (QCloudCOSTransferMangerService*) registerDefaultCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration;
```

#### QCloudServiceConfigurationパラメータの説明

| パラメータ名 | 説明                     | タイプ                   | 必須 |
| -------- | ------------------------ | ---------------------- | ---- |
| appID    | プロジェクトID、すなわちAPPID。      | NSString *             | いいえ   |
| endpoint | endpoint関連情報を構成します。 | QCloudCOSXMLEndPoint * | はい   |

#### QCloudCOSXMLEndPointパラメータの説明

| パラメータ名 | 説明                     | タイプ                   | 必須 |
| ----------- | -------------------------------- | ---------- | ---- |
| regionName  | サービスが所属する地域。                 | NSString * | はい   |
| serviceName | ドメイン名。デフォルトは：myqcloud.com       | NSString * | いいえ   |
| useHTTPS    | HTTPSサービスを使用するかどうか。デフォルトはNO。 | BOOL       | いいえ   |
| suffix    | カスタムhttp://bucketname.suffixをサポートします | NSString       | いいえ   |


#### 初期化例
下例で使用されるappID、 SecretId、 SecretKeyなどは、[COS v5コンソール](https://console.cloud.tencent.com/cos5)から取得されます。

```objective-c
//AppDelegate.m

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
     QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
     configuration.appID = @"*****";
     configuration.signatureProvider = self;
     QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
     endpoint.regionName = @"ap-beijing";//サービス地域名。使用可能な地域について注釈を参考してください
     configuration.endpoint = endpoint;
     [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
     [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];
}
```

## クイックスタート

ここで示されているアップロードとダウンロードの基本プロセスの詳細について、[XML iOS SDK Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples)を参照してください。具体的なAPIの使い方について、Demoのユニットテストファイルを参照してください。

> !このステップの前に[Tencent Cloudコンソール](https://console.cloud.tencent.com/cos4/secret)にCOS業務のAPPIDを申請する必要があります。

### 初期化

> !QCloudServiceConfigurationのsignatureProviderオブジェクトは、QCloudSignatureProviderプロトコルを実現する必要があります。

#### 参考例ステップ1

```objective-c
//AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
	configuration.appID = @"*****";
	configuration.signatureProvider = self;
	QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
	endpoint.regionName = @"ap-beijing";//サービス地域名。使用可能な地域について注釈を参考してください
	configuration.endpoint = endpoint;
	[QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
	[QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];
}
```

#### 参考例ステップ2

```objective-c
//AppDelegate.m
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
//署名プロセスの実現について、サーバーにて署名を実現するプロセスをおすすめします。具体的には、次の章「署名の生成」を参照してください。
}
```

### ファイルのアップロード

自社業務のBucketを申請したとします。実際的に、SDKのすべてのリクエストがRequestクラスに対応します。そのリクエストを生成し、適切な属性を設定した後、リクエストをQCloudCOSTransferMangerServiceオブジェクトに渡すと、その動作を完了できます。そのうち、requestのbodyに、アップロードするファイルのローカルのURL（NSURL\* タイプ）を入力します。    

アップロードファイルのAPIは、署名を用いて身元認証を行い、送信したリクエストは、初期化ときに指定した、QCloudSignatureProviderプロトコルに従うオブジェクトに対し、署名リクエストを自動的に行います。署名の生成について、次の章[署名の生成](#.E7.94.9F.E6.88.90.E7.AD.BE.E5.90.8D)を参照してください。

> !URLに対応するファイルがアップロードしているときに変更されることはできません。さもなければ、エラーが発生します。

#### 例

```objective-c
    QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
    NSURL* url = [NSURL fileURLWithPath:@"filePathString"] /*ファイルのURL*/;
    put.object = @"ファイル名.jpg";
    put.bucket = @"test-123456789";
    put.body =  url;
    [put setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent, int64_t totalBytesExpectedToSend) {
        NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent, totalBytesExpectedToSend);
    }];
    [put setFinishBlock:^(id outputObject, NSError* error) {

    }];
    [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
```

#### QCloudCOSXMLUploadObjectRequestパラメータの説明

| パラメータ名 | 説明                     | タイプ                   | 必須 |
| ----------------------------- | ------------------------------------------------------------ | --------------------- | ---- |
| Object     |オブジェクトキー（Key）は、バケットでのオブジェクトの唯一の識別子。例えば、オブジェクトのアクセスドメイン名bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpgでは、オブジェクトキーは、doc1/pic1.jpg。より詳細な記述について、[オブジェクト記述](https://cloud.tencent.com/document/product/436/13324)を参照してください | NSString* | はい   |
| bucket                        | バケット名、[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt; 。例えば testBucket-1253653367 | NSString * | はい   |
| body                          | アップロードするファイルのパス。NSURL * タイプ変数を入力します                   | BodyType              | はい   |
| storageClass                  |オブジェクトのストレージレベル                                               | QCloudCOSStorageClass | はい   |
| cacheControl       | RFC 2616で定義されるキャッシュポリシー                                     | NSString *            | いいえ   |
| contentDisposition            | RFC 2616で定義されるファイル名                                     | NSString *            | いいえ   |
| expect                        | expect=@"100-Continue"を使用するとき、サーバーからの確認を受信した後、リクエスト内容を送信します | NSString *            | いいえ   |
| expires                       | RFC 2616で定義される期限切れ時間                                     | NSString *            | いいえ   |
| initMultipleUploadFinishBlock | このrequestによりマルチパートアップロードのリクエストが発生した場合、マルチパートアップロード初期化後、このblockによりコールバックします。このコールバックされるblockから分割した後のbucket、 key、 uploadID、およびアップロードが失敗した後にアップロードを再開するためのResumeDataを取得します | block                 | いいえ   |
| accessControlList  | ObjectのACL属性を定義します。有効値：private、public-read-write、public-read。デフォルト値：private | NSString *            | いいえ   |
| grantRead         | 認証対象者に読取権限を付与します。フォーマット： id=" ",id=" "、サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"  そのうち、OwnerUinは、ルートアカウントのID、SubUinは、サブアカウントのIDを示します | NSString * | いいえ   |
| grantWrite        | 認証対象者に書込権限を付与します。フォーマットは上記に同じです                             | NSString * | いいえ   |
| grantFullControl  | 認証対象者に読取・書込権限を付与します。フォーマットは上記に同じです                             | NSString * | いいえ   |

### ファイルのダウンロード

#### 例

```objective-c
  QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];
  //ダウンロード用パスURLを設定します。設定された場合、ファイルは指定パスにダウンロードされます
  request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
  request.object = @“お使いのObject-Key”;
  request.bucket = @"test-123456789";
  [request setFinishBlock:^(id outputObject, NSError \*error) {
    //additional actions after finishing
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload, int64_t totalBytesExpectedToDownload) {
	 //ダウンロード中の進捗
	}];
[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

## 署名の生成

SDKのリクエストは署名が必要です。それによりアクセスするユーザーの身元を確認できます。アクセスのセキュリティを確保します。署名が正しくない場合、ほとんどのCOSのサービスにアクセスできず、403エラーを返します。SDKで署名が生成されます。各リクエストは、QCloudServiceConfigurationオブジェクト中のsignatureProviderオブジェクトに対し、署名の生成をリクエストします。署名を生成するオブジェクトをsignatureProviderに最初段階で付与します。署名を生成するオブジェクトは、QCloudSignatureProviderプロトコルに従い、署名生成メソッドを以下の方法で実現します。

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields* )fileds    
                     request:(QCloudBizHTTPRequest* )request    
                  urlRequest:(NSURLRequest* )urlRequst    
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
```

### CAMシステムを導入し、一時的な署名（推奨）を実現します

ローカルは恒久的なSecretIdとSecretKeyを用いて署名生成用APIを提供したが、恒久的なSecretIdとSecretKeyをローカルに保存することは危ない行為であり、漏えいが発生し不必要な損失を引き起こしやすいため、セキュリティの視点から、サーバーにて署名プロセスを実現することをおすすめします。

>!サーバー時間を署名の開始時間として返すことを強くおすすめします。それがユーザーの携帯電話のローカル時間の偏差が大きくて署名が正しくなることを避けます。

署名プロセス全体を実現するには、自分の署名サーバー内にTencent CloudのCAM（Cloud Access Manager）を導入することをお勧めします。

![CAM署名導入配置図](http://ericcheung-1253653367.cosgz.myqcloud.com/Logical%20View.png)      

署名サーバーにCAMシステムを導入するには、[モバイルアプリケーション直接送信実践](/document/product/436/9068)を参照してください。

署名サーバーにCAMシステムを導入した後、クライアントが署名サーバーに署名を要求するとき、署名サーバーがCAMシステムに一時的な証明書を要求します。その後にクライアントに返します。CAMシステムは、恒久的なSecretIdとSecretKeyを用いて一時的なSecret IDを生成します。Secret Keyと一時的なTokenを用いて署名を生成します。それは最大限にセキュリティを向上させます。端末はそれらの一時暗号鍵情報を受信した後、それらで1つのQCloudCredentialオブジェクトを構築し、そしてこのQCloudCredentailオブジェクトを用いてQCloudAuthentationCreatorを生成します。最後にこのCreatorを用いて署名情報が含まれるQCloudSignatureオブジェクトを生成します。具体的な操作について、下例を参照してください。

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    /*署名サーバーに一時的なSecret ID、Secret Key、Tokenを要求します*/
    QCloudCredential* credential = [QCloudCredential new];
    credential.secretID = @"CAMシステムから取得される一時的なSecret ID";
    credential.secretKey = @"CAMシステムから取得される一時的なSecret Key";
    credential.token = @"CAMシステムから返されたToken。セッションIDです"
    /*サーバー時間を署名の開始時間として返すことを強くおすすめします。それがユーザーの携帯電話のローカル時間の偏差が大きくて署名が正しくなることを避けます */
    credential.startDate = /*返されるサーバー時間*/
    credential.expiretionDate	 = /*署名期限切れ時間*/
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
    QCloudSignature* signature =  [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}

```

### 端末で永続暗号鍵を使って署名を生成します（非推奨）

>!端末で永続暗号鍵を使って署名を生成することをおすすめしません。データを漏えいするおそれがあります。

サンプルコードは以下のとおりです。

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{

    QCloudCredential* credential = [QCloudCredential new];
    credential.secretID = @"恒久的なSecretID";
    credential.secretKey = @"永続SecretKey";
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
    QCloudSignature* signature =  [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}

```

### 足場ツールによる非同期署名の管理

このステップで、署名を生成し正常にSDKのAPIを使用するようになっています。一時的な署名を容易に実現し、サーバーからtempSecretKeyなどの一時的な署名に必要な情報を取得するため、足場ツールを提供します。上記コードを用いて署名を生成できますが、足場ツールのQCloudCredentailFenceQueueを用いて一時的な署名を取得できます。QCloudCredentailFenceQueueがフェンスメカニズムを提供します。つまり、QCloudCredentailFenceQueueを用いて署名を取得する場合、署名を取得する必要のあるすべてのリクエストは署名完了後実行しますので、非同期プロセスの自己管理を省略します。   
QCloudCredentailFenceQueueを使用するには、1つのインスタンスを生成する必要があります。

```objective-c
//AppDelegate.m
//AppDelegateは、QCloudCredentailFenceQueueDelegateプロトコルに従う必要があります
//
- (BOOL)application:(UIApplication * )application didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {
    // init step
    self.credentialFenceQueue = [QCloudCredentailFenceQueue new];
    self.credentialFenceQueue.delegate = self;
    return YES;
}
```

そしてQCloudCredentailFenceQueueクラスの呼び出しはQCloudCredentailFenceQueueDelegateに従い、プロトコルで定義されるメソッドを実現します。

```objective-c
- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
```

QCloudCredentailFenceQueueを使って署名を取得するとき、署名が必要とされるSDKのすべてのリクエストは、このプロトコルで定義されるメソッドにより署名に必要なパラメータを取得し有効な署名を生成した後に実行されます。下の例を参照してください。

```objective-c
//AppDelegate.m
- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
{
   QCloudCredential* credential = [QCloudCredential new];
   //ここで、プロセスを同期し、サーバーから一時的な署名に必要なsecretID、secretKey、expirationDate、tokenパラメータを取得できます
   credential.secretID = @"****";
   credential.secretKey = @"****";
   /*サーバー時間を署名の開始時間として返すことを強くおすすめします。それがユーザーの携帯電話のローカル時間の偏差が大きくて署名が正しくなることを避けます */ 
   credential.startDate =[NSDate dateWithTimeIntervalSince1970:@"返されるサーバー時間"]
   credential.experationDate = [NSDate dateWithTimeIntervalSince1970:1504183628];
   credential.token = @"****";
   QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
   continueBlock(creator, nil);
}
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    [self.credentialFenceQueue performAction:^(QCloudAuthentationCreator *creator, NSError *error) {
        if (error) {
            continueBlock(nil, error);
        } else {
            QCloudSignature* signature =  [creator signatureForData:urlRequst];
            continueBlock(signature, nil);    
        }
    }];
}
```

以上、提供される足場ツールを用いて一時的な署名を生成できます。もちろん、具体的な署名プロセスを手動で実現することもできます。

## 簡易SDKの使用ガイドブック

アップロードとダウンロード機能のみを使用し、SDKのサイズに高く要求するユーザーには、アップロードとダウンロード機能のみを備える簡易SDKを提供します。パッケージの増分は完全バージョンの半分のサイズしかありません。  

簡易SDKは、CocoapodsのSubspec機能により実現されています。そのため、現時点でCocoapods統合により簡易SDKを統合します。簡易SDKを使用するにはPodfileに以下の内容を追加します。

```
pod 'QCloudCOSXML/Transfer'
```

> !Mobile Lineのユーザーにとって、TACStorageを**使用しない**場合のみ、簡易SDKを使用できます。また、[Cocoapods](https://github.com/CocoaPods/Specs)の公式ソースは、**すべてのソースの前に**（Podfileの第1行目に入れることをおすすめ）入れる必要があります。他のユーザーは、この説明を無視してください。

簡易SDKには、QCloudCOSXML.hヘッダファイルが含まれません。そのかわりに、初期化するときに以下のヘッダファイルをインポートする必要があります。

```
#import <QCloudCOSXML/QCloudCOSXMLTransfer.h>
#import <QCloudCore/QCloudCore.h>
```

簡易SDKの初期化プロセス、アップロード・ダウンロードのAPIは、完全SDKと一致します。

