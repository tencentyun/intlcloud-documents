JSON iOS SDKとXML SDKのドキュメントを詳しく比較すると、単なる増分アップデートではないことがわかります。XML iOS SDKは、アーキテクチャ、使いやすさ、およびセキュリティが大幅に向上し、かつ使いやすさ、ロバスト性、および伝送パフォーマンスが大幅に改善されました。XML iOS SDKにアップグレードする場合は、以下のガイドに従ってSDKのアップグレードを完成してください。

## 機能比較

下記のグラフに、JSON SDKとXML SDKの主な機能の比較を示します。

| 機能       | XML SDK         | JSON SDK                         |
| -------- | :------------: | :------------------:    |
| ファイルアップロード | ローカルファイル、2進数データ、マルチパートアップロードをサポートします<br>デフォルトでアップロードを上書きします<br>アップロードモードをスマート判断します<br>簡単なアップロードは最大5GBをサポートします<br>マルチパートアップロードは最大48.82TB（50,000GB）をサポートします | ローカルのファイルのアップロードのみをサポートします<br>上書きを選択できます<br>簡単またはマルチパートアップロードのどちらかを手動で選択します<br>簡単なアップロードは最大20MBをサポートします<br>マルチパートアップロードは最大64GBをサポートします |
| ファイルの削除 | 一括削除をサポートします | 単一ファイルの削除のみをサポートします |
| バケット基本操作 | バケットの作成<br>バケットの取得<br>バケットの削除   | サポートしません |
| バケットACL操作 | バケットACLを設定します<br>バケットACLの設定を取得します<br>バケットACLの設定を削除します   | サポートしません |
| バケットライフサイクル | バケットライフサイクルを作成します<br>バケットライフサイクルを取得します<br>バケットライフサイクルを削除します | サポートしません |
| ディレクトリ操作 | APIを独立に提供しません   | ディレクトリを作成します<br>ディレクトリを照合します<br>ディレクトリを削除します |

## アップグレード手順
以下の5つのステップに従いiOS SDKをアップグレードしてください。

**1. iOS SDKのアップデート**
cocoapodsまたはパッケージされたダイナミックライブラリをダウンロードすることによりSDKを統合します。ここで、cocoapodsによるインポートをお勧めします。
- ** Cocoapodsによるインポート（推奨）**  
Podfile ファイルに使用されます。
```
  pod 'QCloudCOSXML'
```

- **パッケージされたダイナミックライブラリによるインポート（手動統合方式）**  
[Release](https://github.com/tencentyun/qcloud-sdk-ios/releases)から必要なバージョンを選択しダウンロードします  
下図のように、**QCloudCOSXML.framework、QCloudCore.frameworkとlibmtasdk.a**をプロジェクトにドラッグします。
![](https://main.qcloudimg.com/raw/14c8f5773ea19bc681b7f862dd6384fb.png)  

	依存ライブラリを追加します。
> - CoreTelephony
> - Foundation
> - SystemConfiguration
> - libc++.tbd

**プロジェクト構成**
上記手順を完了した後、Build SettingsにOther Linker Flagsを設定し、下記パラメータを追加します。
```shell
-ObjC
-all_load
```

以下の通りです。
![パラメータ構成](https://main.qcloudimg.com/raw/3bee5d2c3cb7e7f80b94c5f6bbe2ce5e.png)

**2. SDK認証方式の変更**

JSON SDKでは、アプリケーションサーバーで自分で署名を計算し、クライアントに返してそれを使用する必要があります。XML SDKは、新しい認証アルゴリズムを採用します。アプリケーションサーバーで一時暗号鍵（STS）ソリューションを導入することを強くお勧めします。このソリューションでは、署名計算プロセスを理解する必要はなく、サーバーでCAMを導入し、取得した一時暗号鍵をクライアントに返してSDKに設定するだけで、SDKが暗号鍵を管理して署名を計算します。一時暗号鍵は一定期間後に自動的に無効になり、永続暗号鍵は漏洩されません。
また、異なる粒度でアクセス権限を制御することもできます。具体的な手順について、[モバイルアプリケーション直接送信の実践](https://cloud.tencent.com/document/product/436/9068)および[一時暗号鍵の生成と使用ガイド](https://cloud.tencent.com/document/product/436/14048)を参照してください。

それでもアプリケーションサーバーを使用して手動で署名を計算してから、クライアントに戻って使用する方式の場合は、署名アルゴリズムが変更されたことに注意してください。署名は単一の署名と複数の署名を区別しなくなりましたが、署名の有効期間の設定によってセキュリティを確保します。署名をアップデートするには、[XMLリクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください。

**3. SDKの初期化方式の変更**

XML SDKの初期化APIに一部変化があります。

- `QCloudCOSXMLService`が`COSClient`に取って代わりますが、両者の役割が同じです。また、より多くの情報を構成するための`QCloudServiceConfiguration`を追加しました。
- 有効な暗号鍵を提供するためには、初期化するときに1つの暗号鍵の提供者`QCloudAuthentationV5Creator`をインスタンス化する必要があります。一時暗号鍵をお勧めします。

**JSON SDKの初期化方式は下記のとおりです：**

```
COSClient *client= [[COSClient alloc] initWithAppId:appId withRegion:@“sh”];
```

**XML SDKの初期化方式は下記のとおりです：**
>?サンプルコードには一時暗号鍵を使って署名を取得することを示します。サーバー時間を署名の開始時間として返すことを強くお勧めします。それがユーザーの携帯電話のローカル時間の偏差が大きくて署名が正しくなることを避けます

```
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
  /*サーバー時間を署名の開始時間として返すことを強くお勧めします。それがユーザーの携帯電話のローカル時間の偏差が大きくて署名が正しくなることを避けます*/
   credential.startDate = /*返さえるサーバー時間*/
   credential.expiretionDate	 = /*署名期限切れ時間*/
   QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
   QCloudSignature* signature =  [creator signatureForData:urlRequst];
   continueBlock(signature, nil);

}

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


**4. バケット名称とAvailability Zoneの略称を変更します**

XML SDKのバケット名称とAvailability Zoneの略称はJSON SDKのものとは異なるため、ユーザーは対応して変更する必要があります。


**バケット**
XML SDKバケット名は、ユーザーカスタム文字列とAPPIDからなり、両者はハイフン「-」で繋ぎます。例えば、`exampleobject-1250000000`、そのうち、`exampleobject`はユーザーカスタム文字列で、`1250000000`はAPPIDです。

>?APPIDは、Tencent Cloudアカウントのタグの1つで、クラウドリソースを関連づけます。ユーザーがTencent Cloudアカウントを申請した後、システムは、自動的にユーザーに1つのAPPIDを割り当てます。[Tencent Cloudコンソール](https://console.cloud.tencent.com/)の【アカウント情報】でAPPIDを確認できます。

バケットを設定するとき、以下のサンプルコードを参照してください：
```
NSString *bucket = "exampleobject-1250000000";
```

**バケットのAvailability Zoneの略称Region**
XML SDKバケットの使用可能な地域の略称が変更されました。次のグラフには、各地域のJSON SDKとXML SDKでの対応関係を示します。

| 地域       | XML SDK地域略称         | JSON SDK地域略称                         |
| -------- | ------------ | ---------------------------------------- |
| 北京1区（華北） | ap-beijing-1 | tj |
| 北京       | ap-beijing   | bj |
| 上海（華東）   | ap-shanghai  | sh |
| 広州（華南）   | ap-guangzhou | gz |
| 成都（西南）   | ap-chengdu   | cd |
| 重慶       | ap-chongqing | 無し |
| シンガポール      | ap-singapore | sgp |
| 香港       | ap-hongkong  | hk |
| トロント      | na-toronto   | ca |
| フランクフルト     | eu-frankfurt | ger |
| ムンバイ       | ap-mumbai    | 無し |
| ソウル       | ap-seoul     | 無し |
| シリコンバレー       | na-siliconvalley     | 無し |
| バージニア       | na-ashburn     | 無し |
| バンコク       | ap-bangkok     | 無し |
| モスクワ       | eu-moscow     | 無し |

初期化するとき、バケットが所属する地域の略語を`QCloudServiceConfiguration`の`regionName`に設定してください。

```
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

**5. APIの変更**

XML SDKにアップグレードした後、ある操作用APIは変化がありました。実際のニーズに応じて適切に変更してください。SDKを容易に使用するためにカプセル化をしています。具体的には参考例と[APIドキュメント](https://cloud.tencent.com/document/product/436/12258)を参照してください。

API変化は以下の3点があります：

**1）独立のディレクトリAPIがありません**

XML SDKでは、単独ディレクトリAPIを提供しません。COS自体は、フォルダとディレクトリの概念がありません。COSは、アップロードオブジェクトproject/a.txtのために1つのprojectフォルダを作成するわけがありません。ユーザーの使用習慣にあわせるよう、オブジェクトをコンソールに格納します。COS browserなどグラフィカルツールでは、「フォルダ」と「ディレクトリ」の表示方式をシミュレートします。キー値がproject/、内容が空白のオブジェクトを作成することで実現されます。表示方式について従来フォルダをシミュレートします。

例えば：オブジェクトproject/doc/a.txtをアップロードし、区切り記号/で「フォルダ」の展開方式をシミュレートします。そして、コンソールに「フォルダ」projectとdocが表示されます。そのうち、docはprojectの次の階層の「フォルダ」にあり、a.txtファイルも含まれます。

したがって、適用シナリオが単にファイルをアップロードするだけの場合は、まずフォルダを作成せずに直接アップロードすることができます。

適用シナリオにフォルダの概念があり、フォルダを作成する機能を提供する必要がある場合は、パスが '/'で終わる0KBファイルをアップロードできます。こうすれば、`GetBucket`APIを呼び出すときにこのようなファイルをフォルダとして使うことができます。


**2）QCloudCOSTransferMangerService**

XML SDKでは、簡単なアップロード（レプリケーション）かマルチパートアップロード（レプリケーション）のどちらかをスマート判断できる操作をカプセル化しました。`QCloudCOSTransferMangerService`という名前を付けます。また、APIの設計と伝送性能を最適化しました。そのまま使用することをお勧めします。`QCloudCOSTransferMangerService`の主な特性は以下のとおりです。

* 一時停止/再開アップロードをサポートします。
* ファイルのサイズにより簡単なアップロード（コピー）かマルチパートアップロード（コピー）のどちらかをスマート判断できます。

`QCloudCOSTransferMangerService`を使ってアップロードを行うサンプルコード：

```
  QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
  NSURL* url = /*ファイルのURL*/;
  put.object = @"ファイル名.jpg";
  put.bucket = @"exampleobject-1250000000";
  put.body =  url;
  [put setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent, int64_t totalBytesExpectedToSend) {
      NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent, totalBytesExpectedToSend);
  }];
  [put setFinishBlock:^(id outputObject, NSError* error) {

  }];
  [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];

```
`QCloudCOSTransferMangerService`を使ってファイルをアップロードするときにの一時停止/再開のサンプルコード：

```
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
  //•••アップロードパラメータを設定する
  put.initMultipleUploadFinishBlock = ^(QCloudInitiateMultipartUploadResult * multipleUploadInitResult, QCloudCOSXMLUploadObjectResumeData resumeData) {
	//マルチパートアップロードを初期化した後にこのblockをコールバックします。ここでresumeDataを取得し、resumeDataにより1つのマルチパートアップロード用リクエストを生成します
	 QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
  };

  [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
  //•••初期化完了かつアップロード未完了前
  NSError* error;
  //これは呼び出しを手動でキャンセルし、resumeDataを生成する例です
  resumeData = [put cancelByProductingResumeData:&error];
  if (resumeData) {
    QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
  }
  //生成されるアップロード再開用リクエストは直接アップロードに使用されます
  [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:request];

```
>!マルチパートアップロードの動作原理に従い、1つのパートをアップロードした後のみ、アプリケーションサーバーがこのパートを記録し、次のパートをアップロードします。次の場合一時停止/再開をせず、改めてアップロードプロセスを開始します。
 - アップロードするファイルが1 MB以下で、マルチパートアップロードが実行されていません。
 - アップロードにQCloudCOSXMLUploadObjectRequestクラスを使用せず、簡単なアップロードAPIを使用しました。
 - resumeDataの生成をキャンセルするとき、マルチパートアップロードの初期化が完了していません（アップロードの初期化を行うためのコールバックが呼び出されていません）。

**3）新規追加されたAPI**

XML SDKには以下の新しいAPIを追加しました。場合により呼び出すことができます。
* バケットの操作、例えば、QCloudPutBucketRequest、QCloudGetBucketRequest、QCloudListBucketRequestなど。
* バケットACLの操作、例えば、QCloudPutBucketACLRequest、QCloudGetBucketACLRequestなど。
* バケットライフサイクルの操作、例えば、PQCloudutBucketLifecycleRequest、QCloudGetBucketLifecycleRequestなど。

具体的には[iOS SDK APIドキュメント](https://cloud.tencent.com/document/product/436/12258)を参照してください。
