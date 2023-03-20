### SDKを手動で統合後、QCloudCOSXMLEndPointインスタンスのregionNameを設定すると、エラー「[__NSCFConstantString matchesRegularExpression:]: unrecognized selector sent to instance xxx」がスローされましたが、どのように対処すればよいですか。

**原因**：matchesRegularExpressionはNSStringのカテゴリーが提供するメソッドです。Objective-Cリンカーはメソッドごとにシンボルテーブルを生成することはなく、クラスについてのみシンボルテーブルを生成します。SDKは静的ライブラリであり、静的ライブラリ内ですでに存在するクラスのカテゴリーが定義されている場合は、システムがそのクラスはすでに存在すると判断し、クラスとクラスのカテゴリーのコードを統合しないため、最終的に実行可能なコードの中にカテゴリー内のメソッドがない状態になります。

**対処方法**：
1. target>Build Settings>All>Other Linker Flagsに`-Objc`および`-all_load`の2つのパラメータを追加します。
2. `-ObjC`は静的ライブラリのクラスとカテゴリーをすべて最終的に実行可能なファイルの中にロードしますが、ライブラリ内にカテゴリーだけがあり、クラスがない場合、そのパラメータは失効するため、`-all_load`が必要です。このパラメータは見つかったすべてのターゲットファイルを実行可能なファイルに加えます。
3. 上記の方法でもこのエラーが解決しない場合は、bitcodeの無効化をお試しください。

### SDKを統合してリクエストを送信すると、「デフォルトのOCRサービス設定が設定されていません。設定してからこのメソッドを呼び出してください。または、Keyが'xxx'のOCRサービス設定として設定されていません。設定してからこのメソッドを呼び出してください」というエラーがスローされましたが、どのように対処すればよいですか。

**原因**：SDKのすべてのリクエストは1つのQCloudCOSXMLServeiceおよびQCloudCOSTransferMangerServiceに依存しています（アップロードの高度なインターフェースはそのインスタンスに依存）。リクエスト送信前に対応するserviceを登録していない場合に、このエラーがスローされます。

**対処方法**：次のコードによって、リクエストに必要なserviceインスタンスを登録し、このインスタンスがリクエスト送信前に確実に存在するようにします。

```iOS
    QCloudServiceConfiguration *configuration = [QCloudServiceConfiguration new];
    configuration.appID = "AppId";
    configuration.signatureProvider = self;
    QCloudCOSXMLEndPoint *endpoint = [[QCloudCOSXMLEndPoint alloc] init];
    endpoint.regionName = @"region";
    endpoint.useHTTPS = YES;
    configuration.endpoint = endpoint;

    [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
    [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];
```

### SDKの統合後に、「デフォルトのCOSXMLServiceがすでに存在します。新たな設定がある場合は、registerCOSXMLWithConfiguration:withKey:によって再登録してください」というエラーがスローされましたが、どのように対処すればよいですか。

**原因**：SDKでは、COSXMLServiceインスタンスごとに対応する設定が異なります（設定情報については関連の属性を参照可能）。例えば、regionNameがap-guangzhouとap-beijingという2つの異なる設定の場合、2つの異なるserviceを登録する必要があります。ap-guangzhouを使用してあるserviceに登録した後、そのregionをap-guangzhouに変更して再登録を行った場合、このエラーがトリガーされます。

**対処方法**：
1. デフォルトのserviceは`registerDefaultCOSXMLWithConfiguration：`によって行われます。keyを指定する必要はありません。
2. 次のコードによって新たなserviceを登録します。
```iOS
//登録が必要なkeyが存在するかどうかを判断します
    if(![QCloudCOSXMLService hasServiceForKey:@"登録が必要なkey"]){
    //存在しなければ新たなserviceを登録します
        [QCloudCOSXMLService registerCOSXMLWithConfiguration:configuration withKey:@"登録が必要なkey"]
    }
```

### SDKの統合後の実行で、プロキシ「- (void)signatureWithFields:(QCloudSignatureFields *)fileds request:urlRequest:compelete:」が呼び出せませんが、どのように対処すればよいですか。

**原因**：このプロキシメソッドはキー/署名を取得するメソッドであり、キーの有効性を最大限に保証するため（署名の呼び出しが早すぎると期限切れになりやすい）、SDKはリクエスト送信前、すなわち`task resume`の前でなければ呼び出しを行いません。

**対処方法**：
1. このプロキシメソッドが存在するクラスがリクエスト送信前に破棄されないようご確認ください。このプロキシメソッドを1つのシングルトンクラス内に実装することをお勧めします。
2. `QCloudServiceConfigurationインスタンスを作成した後`、その`signatureProvider`、例えば`configuration.signatureProvider = self(selfは実装するプロキシメソッドが存在するクラス)`などを設定したかどうか。
3. 上記のどちらにも問題がない場合は、リクエストが送信されているかどうかをチェックしてください。

### SDKはキャッシュとキーを再利用できますか。キーが期限切れとなった後、新たなキーを再度リクエストするにはどうすればよいですか。

SDKはQCloudCredentailFenceQueueを提供してキーのキャッシュと再利用を実現します。具体的な使用方法については、[クイックスタート](https://intl.cloud.tencent.com/document/product/436/11280)のドキュメントをご参照ください。

### SDKの高度なインターフェース「QCloudCOSXMLUploadObjectRequest」から、エラー「このタイプのbodyの設定はサポートしていません。サポートしているタイプはNSData、QCloudFileOffsetBody、NSURLです」というエラーがスローされましたが、どのように対処すればよいですか。

SDKは現時点で次の3タイプのbodyの設定のみをサポートしています。
1. NSURL：ファイルのローカルパスであり、`[NSURL fileURLWithPath:@"ファイルのローカルにおけるパス"]`によってURLを初期化します。
2. NSData：バイナリーデータ。
3. QCloudFileOffsetBody：パートのbodyであり、開発者は通常、このタイプに関心を払う必要はありません。SDKの高度なインターフェース内で使用するbodyタイプです。

### SDKの高度なインターフェース「QCloudCOSXMLUploadObjectRequest」によってシステムフォトライブラリ内のビデオまたはファイルをアップロードする際に、中断からの再開に失敗し、「The specified Content-Length is zero」というエラーが発生しましたが、どのように対処すればよいですか。

SDKはサンドボックス内のファイルのアップロード続行のみサポートしています。中断からの再開機能を使用する必要がある場合は、先にファイルをサンドボックスに移動してください。

### SDKを統合後、アップロードインターフェースを呼び出してアップロードしたファイルのサイズがローカルのファイルと一致しませんが、どのように対処すればよいですか。

bodyを設定した後にローカルファイルに変更が生じていないことをご確認ください。例えばファイルの圧縮中や、書き込みが完了する前にアップロードインターフェースを呼び出してアップロードをトリガーした場合などは、SDKはその時点のファイルサイズを基準としてマルチパートアップロードを行うため、cosにアップロードされたファイルとローカルファイルのサイズが一致しないことが起こります。

### SDKを統合後、アップロードインターフェースを呼び出した際に、「入力されたbodyのURLはローカルURLではありません。確認してから使用してください」というエラーが発生しましたが、どのように対処すればよいですか。

**対処方法：**
URLは必ずfile://で始めてください。次の2つの方法で初期化することができます。
1. `[NSURL URLWithString:@"file:////var/mobile/Containers/Data/Application/DBPF7490-D5U8-4ABF-A0AF-CC49D6A60AEB/Documents/exampleobject"]`
2. `[NSURL fileURLWithPath:@"/var/mobile/Containers/Data/Application/DBPF7490-D5U8-4ABF-A0AF-CC49D6A60AEB/Documents/exampleobject"]`


### SDKを統合後、アップロードインターフェースを呼び出し、アップロードに成功したファイルのサイズが0でした。どのように対処すればよいですか。

**対処方法：**
1. アップロードパスがファイルのシステムフォトライブラリのパスであった場合は、このファイルの読み取り権限の有無を確認してください。例えば、`file:///var/mobile/Media/DCIM/101APPLE/`というパスは直接アクセスすることはできず、Photosフレームワーク内のrequestメソッドによって写真を取得する必要があります。
2. AppにiOS11との互換性が必要な場合は、フォトライブラリのビデオをアップロードする際に、`[[PHImageManager defaultManager] requestPlayerItemForVideo:asset options:option resultHandler:^(AVPlayerItem *playerItem, NSDictionary *info) {
    //適時にファイルをサンドボックスに移動またはplayerItemを保存
    }];`のメソッドを呼び出してplayerItemを取得してから保存するか、またはこのコールバックでアップロードしたいファイルをAppのサンドボックスに移動します。iOS11のplayerItemが破棄されるとファイルの読み取り権限は失効するため、アップロードしたファイルのサイズは0になります。
3. アップロードするファイルがAppのサンドボックス内のファイルの場合、アップロードするファイルが、例えば` /var/mobile/Containers/Data/Application/0BFBB3FE-0FD0-46CB-ADDE-DDE08F6D62C3/tmp/`などのサンドボックスのtmpフォルダに入っていないかをチェックしてください。このディレクトリ下のファイルはシステムによって随時クリーンアップされるため、アップロードしたいファイルを安全なディレクトリに移動することで、ファイルがアップロード中にクリーンアップされないようにしてください。サンドボックスに関するその他の説明については、[File System Basics](https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/FileSystemOverview/FileSystemOverview.html)をご参照ください。

### SDKを統合後、高度なインターフェースを使用してアップロードした際、「アップロード中のMD5検証がローカルと一致しません。ローカルファイルにアップロードの過程で変化が生じていないかを確認してください。マルチパートアップロードの過程では、各パートのアップロードが完了するごとに、そのパートのMD5とローカルパートのMD5が一致するかを検証し、一致しなければエラーとします」と表示されましたが、どのように対処すればよいですか。

**原因：**このエラーは1MBより大きいファイルをアップロードする場合に発生します。1MBを超えるファイルをSDKでアップロードする際は、ファイルをいくつかの1MBのファイルに分けてマルチパートアップロードを行います。各パートのアップロードが完了した後、バックエンドから返されるetagとローカルファイルのパートを比較し、不一致が発見された場合はこのエラーがスローされます。

**対処方法：**ファイルがアップロードの過程で変更されていないかチェックしてください。


### SDKにCDNアクセラレーションドメイン名を使用してアクセスすることはできますか。

できます。ご使用のプログラミング言語に応じて、対応するSDKドキュメントを参照して操作を行ってください。

### SDKでリクエストのタイムアウト時間を設定するにはどうすればよいですか。

**対処方法：**SDK 5.7.0以降では、リクエストのタイムアウト時間のカスタマイズをサポートしています。次の方法で設定できます。
1. `QCloudServiceConfiguration *config = [QCloudServiceConfiguration new]`を初期化します。
2. configの`timeoutInterval`属性を設定すれば完了です。例えば`configの.timeoutInterval = 30;`などに設定します。


### COS iOS SDKにcrashが発生しましたが、どのように対処すればよいですか。

現在のバージョンが最新バージョンかどうかチェックしてください。旧バージョンであれば、最新のSDKのバージョンにアップグレードすることをお勧めします。最新バージョンのiOS SDKについては、[qcloud-sdk-ios](https://github.com/tencentyun/qcloud-sdk-ios)をご参照ください。

### 「Undefined symbols for architecture arm64: "_ne10 init dsp", referenced from:」クラスのエラーにはどのように対処すればよいですか。

[コンパイルエラー：Undefined symbols for architecture arm64](https://github.com/LiteAVSDK/Player_iOS/issues/277)をご参照ください。
