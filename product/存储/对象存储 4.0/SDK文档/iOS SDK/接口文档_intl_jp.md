APIドキュメントでは、あなたが既に初期化プロセスを完了したとします。APIドキュメントでは、詳細なAPIリストをリストし、かつ例を挙げて使い方を説明します。照合するとき、Command+Fを使って照合したいAPIを検索し、APIの簡単な説明を閲覧し、コード例をあなたのプロジェクトにコピーし実行します。    

> ?より多くの機能が必要であれば、または返されたパラメータの意味が分からなければ、コードの注釈を見ることをおすすめします。3本指で軽くタップか、Force-touchで強く押すまたはマウスを変数の上に移動し、Control+Command+Dを押すことでコメントを確認します。

## よく見られる操作のベストプラクティス

この節で、最もよく見られる操作のベストプラクティスを説明しますが、それらの前提はクイックスタートに記載される初期化を完了したことです。

### ファイルのアップロード

クイックスタート中の[ファイルをアップロードする](https://cloud.tencent.com/document/product/436/11280#step---2-.E4.B8.8A.E4.BC.A0.E6.96.87.E4.BB.B6)を参考してください。

### ファイルをアップロードするときの一時停止/再開

1 MB以上のファイルの場合、SDKは、マルチパートアップロードを使用してアップロードを行います。すなわち、ファイルを複数の1 MBの断片ファイルに分けて、並行して（最大並列数は4）アップロードします。アップロードした各断片ファイルがアプリケーションサーバーに保存されます。それがアップロードするときの一時停止/再開の基礎です。    

マルチパートアップロードプロセスにおいて、マルチパートアップロードの初期化が完了後、またはアップロードをキャンセルすると、アップロードを再開するためのresumeDataを生成します。このresumetDataからアップロードリクエストを再生成し、そしてこのアップロードリクエストを使用してアップロードを続くことができ、進捗の累計を表示します。以下のResumeDataの取得例を参照してください。

```objective-C
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
//···アップロードパラメータを設定する
put.initMultipleUploadFinishBlock = ^(QCloudInitiateMultipartUploadResult * multipleUploadInitResult, QCloudCOSXMLUploadObjectResumeData resumeData) {
	//マルチパートアップロードを初期化した後にこのblockをコールバックします。ここでresumeDataを取得し、resumeDataにより1つのマルチパートアップロード用リクエストを生成します
	QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
};

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];

//···初期化完了かつアップロード未完了前
NSError* error;
//これは呼び出しを手動でキャンセルし、resumeDataを生成する例です
resumeData = [put cancelByProductingResumeData:&error];
if (resumeData) {
QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
 }
 //生成されるアップロード再開用リクエストは直接アップロードに使用されます
 [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:request];

```

注意すべきことは、マルチパートアップロードの動作原理に従い、1つの断片ファイルをアップロードした後、アプリケーションサーバーがこの断片ファイルを記録し、進捗を累計することができます。次の場合一時停止/再開はできなく、改めてアップロードプロセスを開始します。

- アップロードするファイルが1 MB以下で、マルチパートアップロードが実行されていません。
- アップロードにQCloudCOSXMLUploadObjectRequestクラスを使用せず、簡単なアップロードAPIを使用します。
- resumeDataの生成をキャンセルするとき、マルチパートアップロードの初期化が完了していません（アップロードの初期化を完了後のコールバックが呼び出されていない）。

### ファイルのダウンロード

クイックスタート中の[ファイルをダウンロードする](https://cloud.tencent.com/document/product/436/11280#3.-.E4.B8.8B.E8.BD.BD.E6.96.87.E4.BB.B6)を参照してください。

### ファイルのコピー

#### 説明

まずはQCloudCOSXMLCopyObjectRequestオブジェクトを初期化し、次はQCloudCOSTransferMangerServiceのCopyObjectメソッドを呼び出します。大きなファイルの場合、マルチパートコピーでコピーを行います。このプロセスは、ユーザーに反映することはしません。  

、> !クロスオリジンレプリケーションの場合、ここで使用するtransferManagerが所属するregionは、ターゲットバケットが所属するregionでなければなりません。

#### 例

```objective-c
QCloudCOSXMLCopyObjectRequest* request = [[QCloudCOSXMLCopyObjectRequest alloc] init];
request.bucket = @"ターゲットBucket";
request.object = @"ターゲットファイル名";
request.sourceBucket = @"ファイルの元Bucket。パブリック読取であるか、または当該アカウントは権限があります";
request.sourceObject = @"ソースのファイル名";
request.sourceAPPID = @"ソースのAPPID";
request.sourceRegion= @"ソースの産業園";
[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    //完了後コールバック
    if (nil == error) {
      //成功
    }
}];
//クロスオリジンレプリケーションの場合、ここで使用するtransferManagerが所属するregion は、ターゲットバケットが所属するregionでなければなりません
[[QCloudCOSTransferMangerService defaultCOSTransferManager] CopyObject:request];
```

## Service操作

### すべてのBucket - Get Serviceをリストする

Get Service APIは、リクエスト者の名配下のすべてのストレージスペースリスト（Bucket list）を取得するために使用されます。

#### 返された結果QCloudListAllMyBucketsResultパラメータの説明

| パラメータ名 | 記述               | タイプ          |
| -------- | ------------------ | ------------- |
| owner    | バケット保有者の情報 | QCloudOwner * |
| buckets  | すべてのbucket情報   | NSArray<QCloudBucket*> *    |

#### 例

```objective-c
QCloudGetServiceRequest* request = [[QCloudGetServiceRequest alloc] init];
[request setFinishBlock:^(QCloudListAllMyBucketsResult* result, NSError* error) {
//完了後の処理をコールバック
}];
[[QCloudCOSXMLService defaultCOSXML] GetService:request];
```

### 署名済みURLの生成と使用

SDKまたはサーバーでは、アップロード、ダウンロードまたはその他の操作に使用される1つの署名済みURLを生成できます。

#### 手順説明

1. QCloudGetPresignedURLRequestインスタンスを生成します。
2. 必要な情報（リクエストのBucket、Object、HTTPMethodなど）を入力します。
3. URLを使用するときにHTTPベッダまたはパラメータを追加するには、署名済みURLを生成するときに、QCloudGetPresignedURLRequestに対応するメソッドを呼び出す必要があります。
4. QCloudCOSXMLService中のgetPresignedURLを呼び出し、リクエストを送信し、結果から署名済みURLを取得します。

#### QCloudGetPresignedURLRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| ----------- | ------------------------------------------------------------ | --------- | ---- |
| bucket      | 署名済みリクエストのBucket                                      | NSString* | はい   |
| object      | 署名済みリクエストを使用するObject。オブジェクトキー（Key）は、バケットでのオブジェクトの唯一の識別子。例えば、オブジェクトのアクセスドメイン名bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpgでは、オブジェクトキーは、doc1/pic1.jpg。より詳細な記述について、[オブジェクト記述](https://cloud.tencent.com/document/product/436/13324)を参照してください | NSString* | はい   |
| HTTPMethod  | 署名済みURLを使用するリクエストのHTTPメソッド。有効値（大文字と小文字を区別する）：@"GET",@"PUT",@"POST",@"DELETE" | NSString* | はい   |
| contentType | 事前署名付きURLを使用するリクエストにこのヘッダが含まれた場合、ここで設定できます          | NSString* | いいえ   |
| contentMD5 | 事前署名付きURLを使用するリクエストにこのヘッダーが含まれた場合、ここで設定できます          | NSString* | いいえ   |

**注意：** 署名済みURLから生成されるリクエストのヘッダー、またはURLパラメータを設定するには、以下のメソッドにより設定します。    

```objective-c
/**
 署名済みリクエストのヘッダーを追加する

 @param value HTTP headerの値
 @param requestHeader HTTP headerのkey
 */
- (void)setValue:(NSString * _Nullable)value forRequestHeader:(NSString * _Nullable)requestHeader;

/**
 署名済みリクエストのURLパラメータを追加する

 @param value パラメータの値
 @param requestParameter パラメータのkey
 */
- (void)setValue:(NSString * _Nullable)value forRequestParameter:(NSString *_Nullable)requestParameter;
```

#### 事前署名付きURLの取得例

```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];
getPresignedURLRequest.bucket = self.bucket;
getPresignedURLRequest.HTTPMethod = @"GET";
getPresignedURLRequest.object = @"testUploadWithPresignedURL";
[getPresignedURLRequest setFinishBlock:^(QCloudGetPresignedURLResult * _Nonnull result, NSError * _Nonnull error) {
if (nil == error) {
 NSString* presignedURL = result.presienedURL;
}
}
[[QCloudCOSXMLService defaultCOSXML] getPresignedURL:getPresignedURLRequest];

```

#### 事前署名付きURLの使用例

ここで、事前署名付きURLを使用しダウンロードする例を示します。

```objective-C
NSMutableURLRequest* request = [[NSMutableURLRequest alloc] initWithURL:[NSURL URLWithString:@"署名済みURL"]];
request.HTTPMethod = @"GET";
request.HTTPBody = [@"ファイル内容" dataUsingEncoding:NSUTF8StringEncoding];
[[[NSURLSession sharedSession] downloadTaskWithRequest:request completionHandler:^(NSURL * _Nullable location, NSURLResponse * _Nullable response, NSError * _Nullable error) {
    NSInteger statusCode = [(NSHTTPURLResponse*)response statusCode];
}] resume];
```

## バケット操作

### bucketの作成

#### 方法のプロトタイプ

COSを使用し始めるとき、オブジェクトの使用と管理を容易にするため、指定したアカウントに1つのBucketを作成する必要があります。Bucket所属の地域を指定します。Bucketを作成するユーザーは、デフォルトでBucketの保有者です。Bucketを作成するときにアクセス権限を指定しないと、デフォルトでプライベート（private）読取・書込権限です。具体的な手順は以下のとおりです。    

1. QCloudPutBucketRequestをインスタンス化し、必要なパラメータを入力します。
2. QCloudCOSXMLServiceオブジェクト中のPutBucketメソッドを呼び出しリクエストを送信します。
3. コールバックされたfinishBlock中のoutputObjectから具体的な内容を取得します。

#### QCloudPutBucketRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket            | 作成するバケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。注意：バケット名は、数字と小文字アルファベットからなり、長さが40文字以下とします。さもなければ、作成が失敗します | NSString * | はい   |
| accessControlList | BucketのACL属性を定義します。有効値：private、public-read-write、public-read；デフォルト値：private | NSString * | いいえ   |
| grantRead         | 認証対象者に読取権限を付与します。フォーマット： id=" ",id=" "、サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"  そのうち、OwnerUinは、ルートアカウントのID、SubUinは、サブアカウントのIDを示します | NSString * | いいえ   |
| grantWrite        | 認証対象者に書込権限を付与します。フォーマットは上記に同じです。                             | NSString * | いいえ   |
| grantFullControl  | 認証対象者に読取・書込権限を付与します。フォーマットは上記に同じです。                             | NSString * | いいえ   |

#### 例

```objective-c
QCloudPutBucketRequest* request = [QCloudPutBucketRequest new];
request.bucket = @"bucketname-appid"; //additional actions after finishing
[request setFinishBlock:^(id outputObject, NSError* error) {

}];
[[QCloudCOSXMLService defaultCOSXML] PutBucket:request];
```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。

### バケット内容をリスクする

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudGetBucketRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudGetBucketRequestをインスタンス化し、必要なパラメータを入力します。    
2. QCloudCOSXMLServiceオブジェクト中のGetBucketメソッドを呼び出しリクエストを送信します。    
3. コールバックされたfinishBlock 中のQCloudListBucketResultから具体的な内容を取得します。   

#### QCloudGetBucketRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| ------------ | ------------------------------------------------------------ | ---------- | ---- |
| bucket       | バケット名。[COS V5コンソール ](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット： &lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |
| prefix       | プレフィックスのマッチング。返されたファイルのプレフィックスアドレスの設定に使用されます                         | NSString * | いいえ   |
| delimiter    | 境界記号は区切り記号で、Prefixがあれば、Prefixからdelimiterまでの同じパスを同じ種類にし、Common Prefixと定義します。そしてすべてのCommon Prefixを一覧表示します。Prefixがなければ、パスから開始します。それを終了記号として理解できます。末尾がAであるという結果を希望する場合、delimiterをAに設定すればよい。 | NSString * | いいえ   |
| encodingType | 戻り値の符号化方式を決めます。選択可能な値：url                            | NSString * | いいえ   |
| marker       | デフォルトではUTF-8のバイナリ順でエントリを一覧表示します。すべての一覧表示されるエントリはmarkerから開始します  | NSString * | いいえ   |
| maxKeys      | 単回返される最大エントリ数。デフォルトは1000                             | int        | いいえ   |

#### 例

```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
request.bucket = @“testBucket-123456789”;
request.maxKeys = 1000;
[request setFinishBlock:^(QCloudListBucketResult * result, NSError*   error) {
//additional actions after finishing
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。

### バケットのACL（Access Control List）を取得する

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudGetBucketACLRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1.QCloudGetBucketACLRequestをインスタンス化し、ACL取得用バケットを入力します。    
2. QCloudCOSXMLServiceオブジェクト中のGetBucketACLメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlock 中のQCloudACLPolicyから具体的な内容を取得します。    

#### QCloudGetBucketACLRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | バケット名、[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt; 。例えば testBucket-1253653367 | NSString * | はい   |

#### 返された結果QCloudACLPolicyパラメータの説明

| パラメータ名 | 記述               | タイプ          |
| -------- | ---------------------------------- | ---------------- |
| owner    | バケット保有者の情報                 | QCloudACLOwner * |
| accessControlList     | 認証対象者と権限の情報 | QCloudAccessControlList *        |

#### 例

```objective-c
QCloudGetBucketACLRequest* getBucketACl   = [QCloudGetBucketACLRequest new];
getBucketACl.bucket = @"testbucket-123456789";
[getBucketACl setFinishBlock:^(QCloudACLPolicy * _Nonnull result, NSError * _Nonnull error) {
   //QCloudACLPolicyにBucketのACL情報が含まれます。
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketACL:getBucketACl];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。

### バケットのACL（Access Control List）を設定する

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudPutBucketACLRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudPutBucketACLRequestをインスタンス化し、設定するバケットを入力し、設定値の権限タイプによりそれぞれパラメータを入力します。    
2. QCloudCOSXMLServiceオブジェクト中のPutBucketACLメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから、設定が成功であるかどうかを取得し、設定した後の追加動作を実行します。   

#### QCloudPutBucketACLRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket            | バケット名。[COSV5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;、例えば testBucket-1253653367 | NSString * | はい   |
| accessControlList | ObjectのACL属性を定義します。有効値：private、public-read-write、public-read。デフォルト値：private | NSString * | いいえ   |
| grantRead         | 認証対象者に読取権限を付与します。フォーマット： id=" ",id=" "；<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"  <br>そのうち、OwnerUinはルートアカウントのID、SubUinはサブアカウントのIDを示します | NSString * | いいえ   |
| grantWrite        | 認証対象者に書込権限を付与します。フォーマットは上記に同じです。                             | NSString * | いいえ   |
| grantFullControl  | 認証対象者に読取・書込権限を付与します。フォーマットは上記に同じです。                             | NSString * | いいえ   |

#### 例

```objective-c
QCloudPutBucketACLRequest* putACL = [QCloudPutBucketACLRequest new];
NSString* appID = @“あなたのAPPID”;
NSString *ownerIdentifier = [NSString stringWithFormat:@"qcs::cam::uin/%@:uin/%@", appID, appID];
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",ownerIdentifier];
putACL.grantFullControl = grantString;
putACL.bucket = @“testBucket-123456789”;
[putACL setFinishBlock:^(id outputObject, NSError *error) {
//error occucs if error != nil
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketACL:putACL];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。

### バケットのCORS（クロスオリジンアクセス）設定を取得する

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudGetBucketCORSRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudGetBucketCORSRequestをインスタンス化し、CORSを取得するバケットを入力します。    
2. QCloudCOSXMLServiceオブジェクト中のGetBucketCORSメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから結果を取得します。結果がQCloudCORSConfigurationオブジェクトにカプセル化されます。このオブジェクトのrules属性は配列です。配列に一連のQCloudCORSRuleが格納されます。具体的なCORS設定がQCloudCORSRuleオブジェクトにカプセル化されます。   

#### QCloudGetBucketCORSRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | バケット名、[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt; 。例えば testBucket-1253653367 | NSString * | はい   |

#### 返された結果QCloudCORSConfigurationパラメータの説明

| パラメータ名 | 記述               | タイプ          |
| -------- | ------------------------------------------------ | ----------------------------------- |
| rules    | CORS配列を格納します。配列内容は、QCloudCORSRuleインスタンスです | NSArray&lt;CloudCORSRule`*`&gt; `*` |

#### QCloudCORSRuleパラメータの説明

| パラメータ名 | 記述               | タイプ          |
| ------------- | ------------------------------------------------------------ | ------------------------------ |
| identifier    | 構成規則のID                                                | NSString *                     |
| allowedMethod | 許可されるHTTP操作。列挙値：GET、PUT、HEAD、POST、DELETE       | NSArray&lt;NSString`*`&gt;`*`  |
| allowedOrigin | 許可されるアクセス元。ワイルドカード*をサポートします。フォーマット：プロトコル://ドメイン名[:ポート]、例えば：`http://www.qq.com` | NSString *                     |
| allowedHeader | OPTIONSリクエストを送信するときにサーバーに対し、次のリクエストがどのようなカスタマイズしたHTTPリクエストヘッダーを使用できるかを通知します。ワイルドカード*をサポートします | NSArray&lt;NSString`*`&gt; `*` |
| maxAgeSeconds | OPTIONSリクエストの結果を取得する有効期間を設定します     | int                            |
| exposeHeader  | ブラウザがサーバーから受信されるカスタムヘッダー情報を設定します      | NSString *                     |

#### 例

```objective-c
QCloudGetBucketCORSRequest* corsReqeust = [QCloudGetBucketCORSRequest new];
corsReqeust.bucket = @"testBucket-123456789";
[corsReqeust setFinishBlock:^(QCloudCORSConfiguration * _Nonnull result, NSError * _Nonnull error) {
   //CORS設定がresultにカプセル化されます。
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketCORS:corsReqeust];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### バケットのCORS（クロスオリジンアクセス）を設定する

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudPutBucketCORSRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudPutBucketCORSRequestをインスタンス化、バケットを設定し、必要なCORSをQCloudCORSRuleに追加します。複数のCORS設定があれば、複数のQCloudCORSRuleを1つのNSArrayに入れ、この配列をQCloudCORSConfigurationのrules属性に入力し、requestに格納します。    
2. QCloudCOSXMLServiceオブジェクト中のPutBucketCORSメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから設定が成功であるかどうか（errorは空であるか）を取得し、設定後の追加動作を実行します。   

#### QCloudPutBucketCORSRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| ----------------- | ------------------------------------------------------------ | ------------------------- | ---- |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット： &lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |
| corsConfiguration | CORSの具体的なパラメータを格納します                                       | QCloudCORSConfiguration * | はい   |

#### QCloudCORSConfigurationパラメータの説明

| パラメータ名 | 記述               | タイプ          |
| -------- | ------------------------------------------------ | -------------------------------- |
| rules    | CORS配列を格納します。配列内容は、QCloudCORSRuleインスタンスです | NSArray&lt;QCloudCORSRule`*` > * |

#### QCloudCORSRuleパラメータの説明

| パラメータ名 | 記述               | タイプ          |
| ------------- | ------------------------------------------------------------ | ---------------------------- |
| identifier    | 構成規則のID                                                | NSString *                     |
| allowedMethod | 許可されるHTTP操作。列挙値：GET、PUT、HEAD、POST、DELETE       | NSArray &lt;NSString`*`> *   |
| allowedOrigin | 許可されるアクセス元。ワイルドカード*をサポートします。フォーマット：プロトコル://ドメイン名[:ポート]、例えば：`http://www.qq.com` | NSString *                     |
| allowedHeader | OPTIONSリクエストを送信するときにサーバーに対し、次のリクエストがどのようなカスタマイズしたHTTPリクエストヘッダーを使用できるかを通知します。ワイルドカード*をサポートします | NSArray &lt;NSString `*` > * |
| maxAgeSeconds | OPTIONSリクエストの結果を取得する有効期間を設定します     | int                            |
| exposeHeader  | ブラウザがサーバーから受信されるカスタムヘッダー情報を設定します      | NSString *                     |

#### 例

```objective-c
QCloudPutBucketCORSRequest* putCORS = [QCloudPutBucketCORSRequest new];
QCloudCORSConfiguration* cors = [QCloudCORSConfiguration new];

QCloudCORSRule* rule = [QCloudCORSRule new];
rule.identifier = @"sdk";
rule.allowedHeader = @[@"origin",@"host",@"accept",@"content-type",@"authorization"];
rule.exposeHeader = @"ETag";
rule.allowedMethod = @[@"GET",@"PUT",@"POST", @"DELETE", @"HEAD"];
rule.maxAgeSeconds = 3600;
rule.allowedOrigin = @"*";
cors.rules = @[rule];
putCORS.corsConfiguration = cors;
putCORS.bucket = @"testBucket-123456789";
[putCORS setFinishBlock:^(id outputObject, NSError *error) {
    if (!error) {
      //success
  }
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketCORS:putCORS];
```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### バケットの地域情報の取得Get Bucket Location

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudGetBucketLocationRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudGetBucketLocationRequestをインスタンス化し、Bucket名を入力します。    
2. QCloudCOSXMLServiceオブジェクト中のGetBucketLocationメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから具体的な内容を取得します。   

#### QCloudGetBucketLocationRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |

#### 返された結果QCloudBucketLocationConstraintパラメータの説明

| パラメータ名 | 記述               | タイプ          |
| ------------------ | -------------------- | --------- |
| locationConstraint | Bucketが所属する地域を説明します | NSString* |

#### 例

```objective-c
QCloudGetBucketLocationRequest* locationReq = [QCloudGetBucketLocationRequest new];
locationReq.bucket = @"testBucket-123456789";
 __block QCloudBucketLocationConstraint* location;
[locationReq setFinishBlock:^(QCloudBucketLocationConstraint * _Nonnull result, NSError * _Nonnull error) {
       location = result;
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketLocation:locationReq];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### バケットCORS設定の削除

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudDeleteBucketCORSRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudDeleteBucketCORSRequestをインスタンス化し、必要なパラメータを入力します。    
2. QCloudCOSXMLServiceオブジェクトのメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから具体的な内容を取得します。   

#### QCloudDeleteBucketCORSRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |

#### 例

```objective-c
QCloudDeleteBucketCORSRequest* deleteCORS = [QCloudDeleteBucketCORSRequest new];
deleteCORS.bucket = @"testBucket-123456789";
[deleteCORS setFinishBlock:^(id outputObject, NSError *error) {
   //success if error == nil
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketCORS:deleteCORS];
```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### Bucket中の実行しているマルチパートアップロードを照合List Bucket Multipart Uploads

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudListBucketMultipartUploadsRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudListBucketMultipartUploadsRequestをインスタンス化し、必要なパラメータを入力します。例えば、返された結果のプレフィックス、符号化方式など。    
2. QCloudCOSXMLServiceオブジェクト中のListBucketMultipartUploadsメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから具体的な内容を取得します。   

#### QCloudListBucketMultipartUploadsRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| -------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |
| prefix         | 限定返されたObject keyは、Prefixをプレフィックスとする必要があります。注意：prefixで照合するとき、返されたkeyにPrefixが含まれます | NSString * | いいえ   |
| delimiter    | 境界記号は区切り記号で、Prefixがあれば、Prefixからdelimiterまでの同じパスを同じ種類にし、Common Prefixと定義します。そしてすべてのCommon Prefixを一覧表示します。Prefixがなければ、パスから開始します。それを終了記号として理解できます。末尾がAであるという結果を希望する場合、delimiterをAに設定すればよい。 | NSString * | いいえ   |
| encodingType | 戻り値の符号化方式を決めます。選択可能な値：url                            | NSString * | いいえ   |
| keyMarker      | 一覧表示するエントリがこのkey値から開始します                                      | NSString * | いいえ   |
| uploadIDMarker | 一覧表示するエントリがこのUploadId値から開始します                                 | int        | いいえ   |
| maxUploads     | 最大返されたmultipart数を設定します。合法値は1～1000です                | int        | いいえ   |

#### 返された結果QCloudListMultipartUploadsResultパラメータの説明

| パラメータ名 | 記述               | タイプ          |
| ------------ | ------------------------------------------------------------ | ---------- |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * |
| prefix         | 限定返されたObject keyは、Prefixをプレフィックスとする必要があります。注意：prefixで照合するとき、返されたkeyにPrefixが含まれます | NSString * |
| delimiter    | 境界記号は区切り記号で、Prefixがあれば、Prefixからdelimiterまでの同じパスを同じ種類にし、Common Prefixと定義します。そしてすべてのCommon Prefixを一覧表示します。Prefixがなければ、パスから開始します | NSString * |
| encodingType | 戻り値の符号化方式を決めます。選択可能な値：url                            | NSString * |
| keyMarker    | 一覧表示するエントリがこのkey値から開始します                | NSString * |
| maxUploads   | 最大返されたmultipart数を設定します。合法値は1～1000です                 | int        |
| uploads      | アップロードしたすべてのパート情報                                       | NSArray*   |

#### 例

```objecitve-c
QCloudListBucketMultipartUploadsRequest* uploads = [QCloudListBucketMultipartUploadsRequest new];
uploads.bucket = @"testBucket-123456789";
uploads.maxUploads = 100;
__block NSError* resulError;
__block QCloudListMultipartUploadsResult* multiPartUploadsResult;
[uploads setFinishBlock:^(QCloudListMultipartUploadsResult* result, NSError *error) {
    multiPartUploadsResult = result;
    localError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] ListBucketMultipartUploads:uploads];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。返されたエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコードを含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### BucketにHead Bucketが存在するかどうかを照合

Head Bucketリクエストにより、このBucketが存在するかどうか、アクセス権限があるかどうかを確認できます。Headの権限がReadと一致します。このBucketが存在する場合、200を返します。このBucketにアクセス権限がなければ、403を返します。このBucketが存在しない場合、404を返します。    

#### QCloudHeadBucketRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |

#### 例

```objective-c
 QCloudHeadBucketRequest* request = [QCloudHeadBucketRequest new];
 request.bucket = @"testBucket-123456789";
 [request setFinishBlock:^(id outputObject, NSError* error) {
     //完了後コールバックを設定します。errorがなければ、正常にbucketにアクセスできます。errorがあれば、error codeとmessasgeから具体的な失敗原因を取得します。
 }];
 [[QCloudCOSXMLService defaultCOSXML] HeadBucket:request];
```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。

### Put Bucket Lifecycle

COSを使用すると、ユーザーはライフサイクル構成でバケット内のオブジェクトのライフサイクルを管理できます。ライフサイクル構成には、一連のオブジェクト規則に適用される1つ以上の規則セットが含まれます（各規則はCOSのために一つの操作を定義します）。
これらの操作は、次の2つのタイプに分けられます：

- 変換操作：オブジェクトを別のストレージタイプに変換する時間を定義します。例えば、オブジェクト作成後30日、それをSTANDARD_IA（IA、低頻度アクセスに適用）ストレージタイプに変換することを選択できます。
- 期限切れ操作：Objectの期限切れ時間を指定します。COSは自動でユーザーのために期限切れのObjectを削除します。

Put Bucket Lifecycleは、バケットのために新しいライフサイクル構成を作成するように使用されます。もしこのバケットにはライフサイクルが構成されている場合、このAPIを使用して新しい構成を作成すると同時に、元の構成が上書きされます。

#### パラメータ説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| --------- | ------------------------------------------------------------ | ----------------------------- | ---- |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |
| lifeCycle | ライフサイクル構成                                                 | QCloudLifecycleConfiguration* | はい   |

#### QCloudLifecycleConfigurationパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| -------- | ------------------ | ------------------------------- | ---- |
| rules    | 規則記述集合の配列 | NSArray<QCloudLifecycleRule*> * | はい   |

#### QCloudLifecycleRuleパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| ------------------------------ | ------------------------------------------------- | --------------------------------------------- | ---- |
| identifier                     | 唯一の規則を識別します。長さは255文字以内        | NSString*                                     | はい   |
| filter                         | Filterは、規則の影響を受けるObject集合を記述します             | QCloudLifecycleRuleFilter*                    |      |
| status                         | 規則が有効になっているかどうかを示します。列挙値：Enabled、Disabled       | QCloudLifecycleStatue                         | はい   |
| abortIncompleteMultipartUpload | マルチパートアップロードの実行を保持する最大時間を設定します                | QCloudLifecycleAbortIncompleteMultipartUpload | いいえ   |
| transition                     | 規則変換属性。オブジェクトがいつStandard_IAに変換されるなど | QCloudLifecycleTransition*                    | いいえ   |
| expiration                     | 規則期限切れ属性                                      | QCloudLifecycleExpiration*                    | いいえ   |
| noncurrentVersionExpiration    | 非カレントバージョンオブジェクト期限がいつ切れるかを明確にします                        | QCloudLifecycleExpiration*                    | いいえ   |
| noncurrentVersionTransition    | 非カレントバージョンオブジェクトがいつSTANDARD_IAに変換されるなどを明確にします | QCloudNoncurrentVersionExpiration*            | いいえ   |

#### 例

```objective-c
QCloudPutBucketLifecycleRequest* request = [QCloudPutBucketLifecycleRequest new];
request.bucket = @"bucket名を入力します";
__block QCloudLifecycleConfiguration* configuration = [[QCloudLifecycleConfiguration alloc] init];
QCloudLifecycleRule* rule = [[QCloudLifecycleRule alloc] init];
rule.identifier = @"identifier";
rule.status = QCloudLifecycleStatueEnabled;
QCloudLifecycleRuleFilter* filter = [[QCloudLifecycleRuleFilter alloc] init];
filter.prefix = @"0";
rule.filter = filter;

QCloudLifecycleTransition* transition = [[QCloudLifecycleTransition alloc] init];
transition.days = 100;
transition.storageClass = QCloudCOSStorageStandarIA;
rule.transition = transition;
request.lifeCycle = configuration;
request.lifeCycle.rules = @[rule];
[request setFinishBlock:^(id outputObject, NSError* error) {
   //完了後コールバックの設定
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketLifecycle:request];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### Get Bucket Lifecycle

#### 返された結果QCloudLifecycleConfigurationパラメータの説明

Put Bucket Lifecycle API中のQCloudLifecycleConfigurationと一致します。

#### 例

```objective-c
QCloudGetBucketLifecycleRequest* request = [QCloudGetBucketLifecycleRequest new];
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(QCloudLifecycleConfiguration* result,NSError* error) {
    //完了後コールバックの設定
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketLifecycle:request];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### Delete Bucket Lifecycle

#### 返された結果QCloudLifecycleConfigurationパラメータの説明

Put Bucket Lifecycle API中のQCloudLifecycleConfigurationと一致します。

#### 例

```objective-c
QCloudDeleteBucketLifeCycleRequest* request = [[QCloudDeleteBucketLifeCycleRequest alloc ] init];
request.bucket = @"testBucket-123456789";
 [request setFinishBlock:^(QCloudLifecycleConfiguration* result, NSError* error) {
 //完了後コールバックの設定
}];
 [[QCloudCOSXMLService defaultCOSXML] DeleteBucketLifeCycle:request];
```

### <span id="pbv">Put Bucket Versioning</span>   

Put Bucket Versioning APIは、バケットを有効または無効にするバージョンコントロール機能を実現します。不可逆的なAPIであり、有効にするとキャンセルすることはできません。

#### QCloudPutBucketVersioningRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| ------------- | ------------------------------------------------------------ | ------------------------------------ | ---- |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |
| configuration | バージョンコントロールの具体的な情報                                           | QCloudBucketVersioningConfiguration* | はい   |

#### QCloudBucketVersioningConfigurationパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| -------- | ------------------------------------------- | ------------------------------- | ---- |
| status   | バージョンが有効になっていることを示します。列挙値：Suspended\Enabled | QCloudCOSBucketVersioningStatus | はい   |

#### 例

```objective-c
QCloudPutBucketVersioningRequest* request = [[QCloudPutBucketVersioningRequest alloc] init];
request.bucket = @"testBucket-123456789";
QCloudBucketVersioningConfiguration* configuration = [[QCloudBucketVersioningConfiguration alloc] init];
request.configuration = configuration;
configuration.status = QCloudCOSBucketVersioningStatusEnabled;
[request setFinishBlock:^(id outputObject, NSError* error) {
   //完了後コールバックの設定
 }];
 [[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。

### Get Bucket Versioning  

#### 返された結果QCloudBucketVersioningConfigurationパラメータの説明

| パラメータ名 | 記述               | タイプ          |
| -------- | ------------------------------------------- | ------------------------------- |
| status   | バージョンが有効になっていることを示します。列挙値：Suspended\Enabled | QCloudCOSBucketVersioningStatus |

#### 例

```objective-c
QCloudGetBucketVersioningRequest* request = [[QCloudGetBucketVersioningRequest alloc] init];
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(QCloudBucketVersioningConfiguration* result, NSError* error) {
   //完了後コールバックの設定
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketVersioning:request];
```

### Put Bucket Replication  

Put Bucket Replicationリクエストはバージョン管理を有効にしたバケットにレプリケーション構成を追加するために使用します。バケットにレプリケーション構成が既にある場合は、このリクエストは既存の構成を置き換えます。    

#### QCloudPutBucketReplicationRequestパラメータ説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| ------------ | ------------------------------------------------------------ | ------------------------------------ | ---- |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |
| configuration | すべてのオリジン間構成情報をを説明します                                       | QCloudBucketReplicationConfiguration* | はい   |



> !このAPIバケットを使用するには、バージョン管理を有効にする必要があります。バージョン管理について、[Put Bucket Versioning](#pbv)を参照してください。



#### 返された結果  パラメータの説明

#### 例

```objective-c
QCloudPutBucketReplicationRequest* request = [[QCloudPutBucketReplicationRequest alloc] init];
request.bucket = @"source-bucket";
QCloudBucketReplicationConfiguation* configuration = [[QCloudBucketReplicationConfiguation alloc] init];
configuration.role = [NSString identifierStringWithID:@"uin" :@"uin"];
QCloudBucketReplicationRule* rule = [[QCloudBucketReplicationRule alloc] init];
rule.identifier = @"identifier";
rule.status = QCloudQCloudCOSXMLStatusEnabled;

QCloudBucketReplicationDestination* destination = [[QCloudBucketReplicationDestination alloc] init];
//qcs:id/0:cos:[region]:appid/[AppId]:[bucketname]
NSString* destinationBucket = @"destinationBucket";
NSString* region = @"destinationRegion"
destination.bucket = [NSString stringWithFormat:@"qcs:id/0:cos:%@:appid/%@:%@",@"region",@"appid",@"destinationBucket"];
rule.destination = destination;
configuration.rule = @[rule];
request.configuation = configuration;
[request setFinishBlock:^(id outputObject, NSError* error) {
     //完了後コールバックの設定
}];
 [[QCloudCOSXMLService defaultCOSXML] PutBucketRelication:request];
```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。

### Get Bucket Replication

Get Bucket Replication APIはバケット中のユーザーによるクロスオリジンレプリケーション構成情報を読み取るようにリクエストします。

#### 返された結果QCloudBucketReplicationConfigurationパラメータの説明

| パラメータ名 | 記述               | タイプ          |
| -------- | ------------------------------------------------------------ | --------------------------------------- |
| role     | 送信者の身元識別。フォーマット：qcs::cam::uin/<OwnerUin>:uin/<SubUin> | NSString*                               |
| rule     | 具体的な構成情報。最大1000個までとします。すべてのポリシーを1つの対象バケットに指定します | NSArray<QCloudBucketReplicationRule*> * |

#### QCloudBucketReplicationRuleパラメータの説明

| パラメータ名 | 記述               | タイプ          |
| ----------- | -------------------------------------------------------- | ----------------------------------- |
| status      | Ruleが有効になっているかどうかを示します                                       | QCloudQCloudCOSXMLStatus            |
| identifier  | 具体的なrule名を示します                                 | NSString*                           |
| prefix      | プレフィックスのマッチングポリシー。重複することはできません。重複の場合エラーを返します。プレフィックスに一致するルートディレクトリは空です | NSString*                           |
| destination | 対象バケット情報                                           | QCloudBucketReplicationDestination* |

#### 例

```objective-c
QCloudGetBucketReplicationRequest* request = [[QCloudGetBucketReplicationRequest alloc] init];
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(QCloudBucketReplicationConfiguation* result, NSError* error) {
    //完了後コールバックの設定
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketReplication:request];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### Delete Bucket Replication  

Delete Bucket Replication APIはバケット中のユーザーによるオリジン間コピー構成を削除するようにリクエストします。

#### パラメータ説明

#### 返された結果  パラメータの説明

#### 例

```objective-c
QCloudDeleteBucketReplicationRequest* request = [[QCloudDeleteBucketReplicationRequest alloc] init];
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(id outputObject, NSError* error) {
   //完了後コールバックの設定
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketReplication:request];
```

## ファイル操作

COSでは、各ファイルは1つのObject（オブジェクト）です。ファイルへの操作は、オブジェクトへの操作に相当します。

### 簡易アップロード（Put Object）

簡易アップロードは、小ファイル（20MB以下）に限られます。簡易アップロードは、メモリからファイルをアップロードすることをサポートします。

>!現在のアクセスポリシーのエントリは1000条に限られており、オブジェクトACL制御が不要な場合、アップロードする前に設定しないでください。デフォルトでバケット権限を受け継ぎます。

#### QCloudPutObjectRequestパラメータの説明

| パラメータ名 | 説明                     | タイプ                   | 必須 |
| ----------------------------- | ------------------------------------------------------------ | --------------------- | ---- |
| Object     |オブジェクトキー（Key）は、バケットでのオブジェクトの唯一の識別子。例えば、オブジェクトのアクセスドメイン名bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpgでは、オブジェクトキーは、doc1/pic1.jpg。より詳細な記述について、[オブジェクト記述](https://cloud.tencent.com/document/product/436/13324)を参照してください | NSString* | はい   |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい  |
| body                          | ファイルがディスクに格納された場合、ここはアップロードするファイルのパスであり、NSURL * タイプ変数を入力します。ファイルがメモリに格納された場合、ここにファイル2進数データを含むNSData * タイプ変数を入力します | BodyType              | はい   |
| storageClass                  |オブジェクトのストレージレベル                                               | QCloudCOSStorageClass | はい   |
| cacheControl       | RFC 2616で定義されるキャッシュポリシー                                     | NSString *            | いいえ   |
| contentDisposition            | RFC 2616で定義されるファイル名                                     | NSString *            | いいえ   |
| expect                        | expect=@"100-Continue"を使用するとき、サーバーからの確認を受信した後、リクエスト内容を送信します | NSString *            | いいえ   |
| expires                       | RFC 2616で定義される期限切れ時間                                     | NSString *            | いいえ   |
| initMultipleUploadFinishBlock | このrequestによりマルチパートアップロードのリクエストが発生した場合、マルチパートアップロード初期化後、このblockによりコールバックします。このコールバックされるblockから分割した後のbucket、 key、 uploadID、およびアップロードが失敗した後にアップロードを再開するためのResumeDataを取得します。 | block                 | いいえ   |
| accessControlList  | ObjectのACL属性を定義します。有効値：private、public-read-write、public-read。デフォルト値：private | NSString *            | いいえ   |
| grantRead         | 認証対象者に読取権限を付与します。フォーマット： id=" ",id=" "、サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"  そのうち、OwnerUinは、ルートアカウントのID、SubUinは、サブアカウントのIDを示します | NSString * | いいえ   |
| grantWrite        | 認証対象者に書込権限を付与します。フォーマットは上記に同じです。                             | NSString * | いいえ   |
| grantFullControl  | 認証対象者に読取・書込権限を付与します。フォーマットは上記に同じです。                             | NSString * | いいえ   |

#### 例    

```objective-C
QCloudPutObjectRequest* put = [QCloudPutObjectRequest new];
put.object = @"object-name";
put.bucket = @"bucket-12345678";
put.body =  [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];
[put setFinishBlock:^(id outputObject, NSError *error) {
   //完了後コールバック
  if (nil == error) {
   //成功
   }
   }];
[[QCloudCOSXMLService defaultCOSXML] PutObject:put];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### オブジェクトのACL（Access Control List）を照合

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudGetObjectACLRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudGetObjectACLRequestをインスタンス化し、バケット名、照合するオブジェクト名を入力します。    
2. QCloudCOSXMLServiceオブジェクト中のGetObjectACLメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから取得されたQCloudACLPolicyオブジェクトからカプセル化されたACLの具体的な情報を取得します。   

#### QCloudGetObjectACLRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | バケット名、[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt; 。例えば testBucket-1253653367 | NSString * | はい   |
| object   |オブジェクトキー（Key）は、バケットでのオブジェクトの唯一の識別子。例えば、オブジェクトのアクセスドメイン名bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpgでは、オブジェクトキーは、doc1/pic1.jpg。より詳細な記述について、[オブジェクト記述](https://cloud.tencent.com/document/product/436/13324)を参照してください | NSString* | はい   |

#### 例

```objective-c
request.bucket = self.aclBucket;
request.object = @"オブジェクト名";
request.bucket = @"testBucket-123456789"
__block QCloudACLPolicy* policy;
[request setFinishBlock:^(QCloudACLPolicy * _Nonnull result, NSError * _Nonnull error) {
     policy = result;
}];
[[QCloudCOSXMLService defaultCOSXML] GetObjectACL:request];
```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。

### オブジェクトのACL（Access Control List）を設定

現在のアクセスポリシーエントリは1000件までとします。オブジェクトACLのコントロールが必要とされない場合、設定しないでください。デフォルトでBucket権限が継承されます。

#### 方法のプロトタイプ

オブジェクト操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudPutObjectACLRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudPutObjectACLRequestをインスタンス化し、バケット名、さらに必要なパラメータ（権限付与に関する具体的な情報など）を入力します。    
2. QCloudCOSXMLServiceオブジェクトのメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから設定された完了状況を取得します。errorは空であれば、設定が成功します。   

#### QCloudPutObjectACLRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |
| object            |オブジェクト名                                                       | NSString * | はい   |
| accessControlList | ObjectのACL属性を定義します。有効値：private、public-read-write、public-read。デフォルト値：private | NSString * | いいえ   |
| grantRead         | 認証対象者に読取権限を付与します。フォーマット： id=" ",id=" "；<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"  <br>そのうち、OwnerUinはルートアカウントのID、SubUinはサブアカウントのIDを示します | NSString * | いいえ   |
| grantWrite        | 認証対象者に書込権限を付与します。フォーマットは上記に同じです。                             | NSString * | いいえ   |
| grantFullControl  | 認証対象者に読取・書込権限を付与します。フォーマットは上記に同じです。                             | NSString * | いいえ   |

#### 例

```objective-c
QCloudPutObjectACLRequest* request = [QCloudPutObjectACLRequest new];
request.object = @"ACLのオブジェクト名を設定する必要があります";
request.bucket = @"testBucket-123456789";
NSString *ownerIdentifier = [NSString stringWithFormat:@"qcs::cam::uin/%@:uin/%@",self.appID, self.appID];
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",ownerIdentifier];
request.grantFullControl = grantString;
__block NSError* localError;
[request setFinishBlock:^(id outputObject, NSError *error) {
     localError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] PutObjectACL:request];
```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### ファイルのダウンロード

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1.インスタンス化し、必要なパラメータを入力します。    
2. QCloudCOSXMLServiceオブジェクトのメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから具体的な内容を取得します。   

#### パラメータ説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| -------------------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |
| object            |オブジェクト名                                                       | NSString * | はい   |
| range                      | RFC 2616で定義される指定ファイルのダウンロード範囲。単位はバイト（bytes）     | NSString * | いいえ   |
| ifModifiedSince            | ファイルの変更時間が指定時間より遅い場合、ファイル内容を返します。さもなければ412 (not modified)を返します | NSString * | いいえ   |
| responseContentType        | レスポンスヘッダー中のContent-Typeパラメータを設定します                           | NSString * | いいえ   |
| responseContentLanguage    | レスポンスヘッダー中のContent-Languageパラメータを設定します                     | NSString * | いいえ   |
| responseContentExpires     | レスポンスヘッダー中のContent-Expiresパラメータを設定します                        | NSString * | いいえ   |
| responseCacheControl       | レスポンスヘッダー中のCache-Controlパラメータを設定します                          | NSString * | いいえ   |
| responseContentDisposition | レスポンスヘッダー中のContent-Dispositionパラメータを設定します。                  | NSString * | いいえ   |
| responseContentEncoding    | レスポンスヘッダー中のContent-Encodingパラメータを設定します                       | NSString * | いいえ   |

#### 例

```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];
//ダウンロード用パスURLを設定します。設定された場合、ファイルが指定パスにダウンロードされます。このパラメータが設定されていない場合、ファイルがメモリにダウンロードされ、finishBlockのoutputObjectに格納されます。
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
request.object = @“あなたのObject-Key”;
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(id outputObject, NSError *error) {
    //additional actions after finishing
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload, int64_t totalBytesExpectedToDownload) {
   //ダウンロード中の進捗
}];
[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### Objectのクロスオリジンアクセス構成のプリフライトリクエスト

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudOptionsObjectRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudOptionsObjectRequestをインスタンス化し、設定するオブジェクト名、バケット名、シミュレートクロスオリジンアクセスリクエストhttpメソッドと、シミュレートクロスオリジンアクセスに許可されるアクセス元を入力します。    
2. QCloudCOSXMLServiceオブジェクトのメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから具体的な内容を取得します。   

#### QCloudOptionsObjectRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| -------------------------- | ------------------------------------------------------------ | --------------------------- | ---- |
| object   |オブジェクトキー（Key）は、バケットでのオブジェクトの唯一の識別子。例えば、オブジェクトのアクセスドメイン名bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpgでは、オブジェクトキーは、doc1/pic1.jpg。より詳細な記述について、[オブジェクト記述](https://cloud.tencent.com/document/product/436/13324)を参照してください | NSString* | はい   |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |
| accessControlRequestMethod | シミュレートクロスオリジンアクセスのHTTPメソッド                                   | NSArray&lt;NSString`*`> *   | はい   |
| origin                     | シミュレートクロスオリジンアクセスで許可されるアクセス元。ワイルドカード*をサポートします。フォーマット：プロトコル://ドメイン名[:ポート]、例えば：`http://www.qq.com` | NSString *                  | はい   |
| allowedHeader              | OPTIONSリクエストを送信するときにサーバーに対し、次のリクエストがどのようなカスタマイズしたHTTPリクエストヘッダーを使用できるかを通知します。ワイルドカード*をサポートします | NSArray&lt;NSString `*` > * | いいえ   |

#### 例

```objective-c
QCloudOptionsObjectRequest* request = [[QCloudOptionsObjectRequest alloc] init];
request.bucket =@"バケット名";
request.origin = @"*";
request.accessControlRequestMethod = @"get";
request.accessControlRequestHeaders = @"host";
request.object = @"オブジェクト名";
__block id resultError;
[request setFinishBlock:^(id outputObject, NSError* error) {
     resultError = error;
 }];

[[QCloudCOSXMLService defaultCOSXML] OptionsObject:request];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### 単一オブジェクトの削除

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudDeleteObjectRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudDeleteObjectRequestをインスタンス化し、必要なパラメータを入力します。    
2. QCloudCOSXMLServiceオブジェクトのメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから具体的な内容を取得します。   

#### QCloudDeleteObjectRequestパラメータの説明

| パラメータ名 | タイプ                                                         | 必須       | 記述 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| object   |オブジェクトキー（Key）は、バケットでのオブジェクトの唯一の識別子。例えば、オブジェクトのアクセスドメイン名bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpgでは、オブジェクトキーは、doc1/pic1.jpg。より詳細な記述について、[オブジェクト記述](https://cloud.tencent.com/document/product/436/13324)を参照してください | NSString* | はい   |
| bucket   | バケット名、[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt; 。例えば testBucket-1253653367 | NSString * | はい   |

#### 例

```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
deleteObjectRequest.bucket = @"testBucket-123456789";
deleteObjectRequest.object = @"オブジェクト名";
__block NSError* resultError;
[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    resultError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### 複数オブジェクトの削除

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudDeleteMultipleObjectRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudDeleteMultipleObjectRequestをインスタンス化し、必要なパラメータを入力します。    
2. QCloudCOSXMLServiceオブジェクトのメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから具体的な内容を取得します。   

#### QCloudDeleteMultipleObjectRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| ------------- | ------------------------------------------------------------ | ------------------ | ---- |
| object   |オブジェクトキー（Key）は、バケットでのオブジェクトの唯一の識別子。例えば、オブジェクトのアクセスドメイン名bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpgでは、オブジェクトキーは、doc1/pic1.jpg。より詳細な記述について、[オブジェクト記述](https://cloud.tencent.com/document/product/436/13324)を参照してください | NSString* | はい   |
| deleteObjects | 一括削除する複数オブジェクトの情報をカプセル化します                           | QCloudDeleteInfo * | はい   |

#### QCloudDeleteInfoパラメータ説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| -------- | -------------------------- | ----------------------------------------- | ---- |
| objects  | オブジェクト情報を削除する配列を格納します | NSArray&lt;QCloudDeleteObjectInfo `*` > * | はい   |

#### QCloudDeleteObjectInfoパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| key   |オブジェクトキー（Key）は、バケットでのオブジェクトの唯一の識別子。例えば、オブジェクトのアクセスドメイン名bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpgでは、オブジェクトキーは、doc1/pic1.jpg。より詳細な記述について、[オブジェクト記述](https://cloud.tencent.com/document/product/436/13324)を参照してください | NSString* | はい   |

#### 例

```objective-c
QCloudDeleteMultipleObjectRequest* delteRequest = [QCloudDeleteMultipleObjectRequest new];
delteRequest.bucket = @"testBucket-123456789";

QCloudDeleteObjectInfo* deletedObject0 = [QCloudDeleteObjectInfo new];
deletedObject0.key = @"第1のオブジェクト名";

QCloudDeleteObjectInfo* deleteObject1 = [QCloudDeleteObjectInfo new];
deleteObject1.key = @"第2のオブジェクト名";

QCloudDeleteInfo* deleteInfo = [QCloudDeleteInfo new];
deleteInfo.quiet = NO;
deleteInfo.objects = @[ deletedObject0,deleteObject2];
delteRequest.deleteObjects = deleteInfo;
__block NSError* resultError;
[delteRequest setFinishBlock:^(QCloudDeleteResult* outputObject, NSError *error) {
      localError = error;
      deleteResult = outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。



### マルチパートアップロードの初期化

#### 方法のプロトタイプ

バケット操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudInitiateMultipartUploadRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudInitiateMultipartUploadRequestをインスタンス化し、必要なパラメータを入力します。    
2. QCloudCOSXMLServiceオブジェクト中のInitiateMultipartUploadメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから具体的な内容を取得します。   

#### パラメータ説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| ------------------ | ------------------------------------------------------------ | --------------------- | ---- |
| Object             | アップロードファイル（オブジェクト）のファイル名であり、オブジェクトのkeyです。オブジェクトキー（Key）は、バケットでのオブジェクトの唯一の識別子。例えば、オブジェクトのアクセスドメイン名bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpgでは、オブジェクトキーは、doc1/pic1.jpg。より詳細な記述について、[オブジェクト記述](https://cloud.tencent.com/document/product/436/13324)を参照してください | NSString* | はい   |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |
| cacheControl       | RFC 2616で定義されるキャッシュポリシー                                     | NSString *            | いいえ   |
| contentDisposition            | RFC 2616で定義されるファイル名                                     | NSString *            | いいえ   |
| expect             | `expect=@"100-continue" `を使用するとき、サーバーからの確認を受信した後、リクエスト内容を送信します | NSString *            | いいえ   |
| expires                       | RFC 2616で定義される期限切れ時間                                     | NSString *            | いいえ   |
| storageClass       |オブジェクトのストレージレベル                                               | QCloudCOSStorageClass | いいえ   |
| accessControlList  | ObjectのACL属性を定義します。有効値：private、public-read-write、public-read。デフォルト値：private | NSString *            | いいえ   |
| grantRead          | 認証対象者に読取権限を付与します。フォーマット： id=" ",id=" "；<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"  <br>そのうち、OwnerUinはルートアカウントのID、SubUinはサブアカウントのIDを示します | NSString *            | いいえ   |
| grantWrite        | 認証対象者に書込権限を付与します。フォーマットは上記に同じです。                             | NSString * | いいえ   |
| grantFullControl  | 認証対象者に読取・書込権限を付与します。フォーマットは上記に同じです。                             | NSString * | いいえ   |

#### 例

```objective-c
QCloudInitiateMultipartUploadRequest* initrequest = [QCloudInitiateMultipartUploadRequest new];
initrequest.bucket = @"testBucket-123456789";
initrequest.object = @"オブジェクト名";
__block QCloudInitiateMultipartUploadResult* initResult;
[initrequest setFinishBlock:^(QCloudInitiateMultipartUploadResult* outputObject, NSError *error) {
    initResult = outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] InitiateMultipartUpload:initrequest];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。

### オブジェクトmeta情報の取得

#### 方法のプロトタイプ

ファイル操作を行う前、ヘッダファイルQCloudCOSXML/QCloudCOSXML.hをインポートする必要があります。その前に前文のSTEP-1初期化操作を完了する必要があります。1つのQCloudHeadObjectRequestインスタンスを生成し、次は必要な追加制限条件を入力し、内容を取得します。具体的な手順は以下のとおりです。    

1. QCloudHeadObjectRequestをインスタンス化し、必要なパラメータを入力します。    
2. QCloudCOSXMLServiceオブジェクト中のHeadObjectメソッドを呼び出し、リクエストを送信します。    
3. コールバックされたfinishBlockから具体的な内容を取得します。   

#### QCloudHeadObjectRequestパラメータの説明

| パラメータ名    | 記述                                                         | タイプ      | 必須 |
| --------------- | ------------------------------------------------------------ | ---------- | ---- |
| Object   |オブジェクトキー（Key）は、バケットでのオブジェクトの唯一の識別子。例えば、オブジェクトのアクセスドメイン名bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpgでは、オブジェクトキーは、doc1/pic1.jpg。より詳細な記述について、[オブジェクト記述](https://cloud.tencent.com/document/product/436/13324)を参照してください | NSString* | はい   |
| bucket       | バケット名。[COS V5コンソール](https://console.cloud.tencent.com/cos5/bucket)から確認できます。フォーマット：&lt;bucketName&gt;-&lt;APPID&gt;。例えば testBucket-1253653367 | NSString * | はい   |
| ifModifiedSince            | ファイルの変更時間が指定時間より遅い場合、ファイル内容を返します。さもなければ304 (not modified)を返します | NSString * | はい   |

#### 例

```objective-c
QCloudHeadObjectRequest* headerRequest = [QCloudHeadObjectRequest new];
headerRequest.object = @“オブジェクト名”;
headerRequest.bucket = @"testBucket-123456789";

   __block id resultError;
[headerRequest setFinishBlock:^(NSDictionary* result, NSError *error) {
      resultError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] HeadObject:headerRequest];

```

#### エラーコードの返しについて

SDKリクエストに失敗した場合、返されたerrorは空ではなく、エラーコード、エラー記述、その他のデバッグに使用される必要な情報を含み、開発者が速やかに問題を解決することに役立ちます。

返されるエラーコード（返されたerrorにカプセル化される）は、デバイス自体からネットワーク原因などで返されたエラーコード、およびCOSから返されたエラーコード含みます。

- デバイス自体からネットワーク原因で発生したエラーコードは、四桁の負の数です。例えば、-1001。このようなエラーコードはアップル社によって定義されるものです。NSURLError.hヘッダファイルの定義、または[アップル社公式ドキュメント説明](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)を参照してください。
- COSから返されたエラーコードは、HTTPのステータスコードに基づいて生成されたもので、つまり404、503など。そのようなエラーコードについて、COS公式ドキュメントの[エラーコードについて]( https://cloud.tencent.com/document/product/436/7730)を参照し、解決策を求めます。

## カスタムヘッダーの追加

カスタムヘッダを追加する必要があれば、カスタムヘッダーを使用できます。カスタムヘッダを追加したクラスにはcustomHeaders属性が含まれます。

```objective-c
@property (strong, nonatomic) NSMutableDictionary* customHeaders;
```

この属性内のすべてのキー値ペアについて、対応する形式でリクエストを構築するHTTPベッダーに追加されます。

## サーバー暗号化

アップロードするオブジェクトを暗号化する必要があれば、暗号化方式をサポートします

### 暗号鍵がcosによって保管されるサーバーによる保護データの暗号化（SSE-COS）

COSを使用することにより、データをデータセンターに書き込むときに自動的に暗号化することが可能になり、このデータを取り出すときに自動的に復号化します。現時点でCOSのマスタ暗号鍵を用いてデータをAES-256暗号化します。

iOS SDKは、-(void)setCOSServerSideEncyptionメソッドを呼び出すことにより実現します。

```objective-c
[request setCOSServerSideEncyption];
```

### 客先からの暗号鍵のサーバーによる保護データの暗号化（SSE-C）

iOS sdkは、-(void)setCOSServerSideEncyptionWithCustomerKey:(NSString *)customerKeyメソッドを呼び出すことにより実現します。
  注意：

1. この暗号化を実行するサービスは、HTTPSリクエストを使用する必要があります。「[HTTPSサービスを有効にする](#https)」節を参照してください。
2. customerKey：ユーザーが提供する暗号鍵。32バイトの文字列を受け取ります。英数字、文字列の組み合せがサポートされますが、中国語がサポートされません
3.アップロードしたソースファイルがこのメソッドを呼び出した場合、QCloudCOSXMLDownloadObjectRequest、QCloudHeadObjectRequest、QCloudCOSXMLUploadObjectRequest、QCloudCOSXMLUploadObjectRequestを使用してソースオブジェクト操作を行うときにもこのメソッドを呼び出す必要があります。

```objective-c
NSString *customKey = @"123456qwertyuioplkjhgfdsazxcvbnm";
[put setCOSServerSideEncyptionWithCustomerKey:customKey];
```

## <span id="https">HTTPSサービスの有効化</span>

iOS SDKは、HTTPSリクエストをサポートします。QCloudServiceConfiguration構成オブジェクトを初期化するとき、そのendpointのuseHTTPSをYESに設定すればよい

```objective-c
QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
configuration.appID = kAppID;
configuration.signatureProvider = self;
QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
endpoint.regionName = kRegion;
endpoint.useHTTPS = YES;
configuration.endpoint = endpoint;
[QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
[QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];
}
```
