VODは、iOSプラットフォームでビデオをアップロードするシナリオ向けに、iOSアップロードSDKを提供しています。アップロードのフローについては、[クライアントからのアップロードガイド](https://intl.cloud.tencent.com/document/product/266/33921) をご参照ください。

## ソースコードのダウンロード
1. [クリックしてダウンロード](https://liteav.sdk.qcloud.com/download/ugc/LiteAVSDK_UGC_Upload_iOS.zip) して、iOSアップロードDemoとソースコードをダウンロードします。
2. ダウンロードした圧縮パッケージを解凍すると、TXUGCUploadDemoディレクトリが表示されます。アップロードソースコードは、`TXUGCUploadDemo/upload`ディレクトリにあります。

## アップロードライブラリとソースコードの統合

1. ソースコードディレクトリ`TXUGCUploadDemo/upload`をプロジェクトディレクトリにコピーします。
2. 動的ライブラリ`QCloudCore.framework`、`QCloudCOSXML.framework`（`TXUGCUploadDemo/upload/COSSDK/`ディレクトリにあります）をプロジェクトにインポートし、次の依存ライブラリを追加します。
    ```
    1. CoreTelephony.framework
    2. Foundation.framework
    3. SystemConfiguration.framework
    4. libc++.tbd
    ``` 
3. Build Settingsにおいて、Other Linker Flagsを設定し、パラメータ`-ObjC`を追加します。

##  シンプルアップロード

#### アップロードオブジェクトの初期化

```objc
TXUGCPublish *_videoPublish = [[TXUGCPublish alloc] initWithUserID:@"upload_video_userid"];
```

#### アップロードオブジェクトのコールバックの設定

```objc
_videoPublish.delegate = self;
```

```objc
#pragma mark - TXVideoPublishListener

- (void)onPublishProgress:(NSInteger)uploadBytes totalBytes:(NSInteger)totalBytes {
    self.progressView.progress = (float)uploadBytes/totalBytes;
    NSLog(@"onPublishProgress [%ld/%ld]", uploadBytes, totalBytes);
}

- (void)onPublishComplete:(TXPublishResult*)result {
    NSString *string = [NSString stringWithFormat:@"アップロード完了、エラーコード[%d]，メッセージ[%@]", result.retCode, result.retCode == 0? result.videoURL: result.descMsg];
    [self showErrorMessage:string];
    NSLog(@"onPublishComplete [%d/%@]", result.retCode, result.retCode == 0? result.videoURL: result.descMsg);
}
```

#### アップロードパラメータの作成

```objc
TXPublishParam *publishParam = [[TXPublishParam alloc] init];

publishParam.signature  = @"業務バックエンドで生成された署名";
publishParam.videoPath  = @"ビデオファイルへのパス";
```
> `signature`の計算ルールについては、[クライアントからのアップロード署名 ](https://intl.cloud.tencent.com/document/product/266/33922)をご参照ください。

#### アップロードの呼び出し

```objc
[_videoPublish publishVideo:publishParam];
```
>?
>- アップロード方法は、ファイルのサイズに応じて、通常アップロードとマルチパートアップロードが自動的に選択されます。マルチパートアップロードの各手順を気にすることなく、マルチパートアップロードを行うことができます。
>- 指定されたサブアプリケーションにアップロードする必要がある場合は、[サブアプリケーションシステム-クライアントからのアップロード](https://intl.cloud.tencent.com/document/product/266/33987)をご参照ください。

## 高度な機能
#### カバーの付加

アップロードパラメータに画像を追加します。

```objc
TXPublishParam *publishParam = [[TXPublishParam alloc] init];
publishParam.signature  = @"業務バックエンドで生成された署名";
publishParam.coverPath = @"カバー画像ファイルへのパス";
publishParam.videoPath  = @"ビデオファイルへのパス";
```

#### アップロードのキャンセルと再開

アップロードをキャンセルするには、 `canclePublish`インターフェースを呼び出します。

```objc
[_videoPublish canclePublish];
```

アップロードを再開するには、同じアップロードパラメータを使用し（ビデオパスとカバーパスは変更されません）`TXUGCPublish`の`publishVideo`を再度呼び出します。

#### 中断からの再開

VODはビデオのアップロード中、中断からの再開をサポートします。アップロードが予期せず終了した場合に、中断ポイントからアップロードを再開できるため、アップロード時間を短縮できます。

中断からの再開の有効時間は1日です。つまり、ビデオのアップロードが中断しても、1日以内に同じビデオを再度アップロードすると、中断したポイントからアップロードすることができます。1日を超えると、デフォルトでビデオ全体が再度アップロードされます。

アップロードパラメータの`enableResume`は、中断からの再開のスイッチであり、デフォルトで有効になっています。


## 画像とメディアのアップロード

```objc
// オブジェクトの作成
TXUGCPublish *_imagePublish = [[TXUGCPublish alloc] initWithUserID:@"upload_image_userid"];

// コールバックの設定
_imagePublish.mediaDelegate = self;

// アップロードパラメータの作成
TXMediaPublishParam *publishParam = [[TXMediaPublishParam alloc] init];
publishParam.signature  = @"業務バックエンドで生成された署名";
publishParam.mediaPath = @"画像ファイルへのパス";

// 画像またはメディアファイルをアップロードします
[_imagePublish publishMedia:publishParam];

```


## ビデオアップロードインターフェースの説明

アップロードオブジェクトの初期化：`TXUGCPublish::initWithUserID`

| パラメータ名   | パラメータの説明               | タイプ        | 入力必須   |
| ------ | ------------------ | --------- | ---- |
| userID | userID。ユーザーを区別するために使用されます。 | NSString | いいえ    |

アップロードの開始：`TXUGCPublish.publishVideo`

| パラメータ名  | パラメータの説明 | タイプ              | 入力必須   |
| ----- | ---- | --------------- | ---- |
| param | パラメータを公開します。 | TXPublishParam | はい    |

アップロードパラメータ：`TXPublishParam`

| パラメータ名         | パラメータの説明                               | タイプ        | 入力必須   |
| ------------ | ---------------------------------- | --------- | ---- |
| signature    | [クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922)。 | NSString* | はい    |
| videoPath    | ローカルビデオファイルパス。                           | NSString* | はい    |
| coverPath    |ローカルカバー画像へのパス。これは設定しなくてもかまいません。                 | NSString*  | いいえ    |
| fileName     | Tencent Cloudにアップロードされたビデオファイル名です。空のままの場合、デフォルトでローカルファイル名が使用されます。 | NSString*  | いいえ    |
| enableResume | 中断ポイントからの再開の有効無効を指定。デフォルトでは有効になっています。                  | BOOL      | いいえ    |
| enableHttps  | HTTPSの有効無効を指定。デフォルトでは無効になっています。                    | BOOL      | いいえ    |


アップロードコールバックの設定：`TXUGCPublish.delegate`

| メンバー変数名   | 変数の説明        | タイプ                     | 入力必須   |
| -------- | ----------- | ---------------------- | ---- |
| delegate | アップロードの進行状況と結果のコールバックを監視します。 | TXVideoPublishListener | はい    |


アップロード進行状況のコールバック：`onPublishProgress`

| 変数名        | 変数の説明     | タイプ        |
| ----------- | -------- | --------- |
| uploadBytes | アップロード済みのバイト数。 | NSInteger |
| totalBytes  | 合計バイト数。     | NSInteger |

アップロード結果のコールバック：`onPublishComplete`

| 変数名   | 変数の説明 | タイプ               |
| ------ | ---- | ---------------- |
| result | アップロード結果。 | TXPublishResult |

アップロードイベントのコールバック：`onPublishEvent`

| 変数名   | 変数の説明 | タイプ               |
| ------ | ---- | ---------------- |
| evt | デバッグ情報を出力するためのイベント。 | NSDictionary |

アップロード結果：`TXPublishResult`

| メンバー変数名   | 変数の説明      | タイプ        |
| -------- | --------- | --------- |
| retCode  | エラーコード。       | int       |
| descMsg  | アップロード失敗のエラー説明。 | NSString |
| videoId  | VODビデオファイルID。  | NSString |
| videoURL | ビデオストレージアドレス。    | NSString |
| coverURL | カバーストレージアドレス。    | NSString |

事前アップロード：`TXUGCPublishOptCenter.prepareUpload`
    
| パラメータ名  | パラメータの説明                                     | タイプ   | 入力必須 |
| --------- | -------------------------------------------- | ------ | ---- |
| signature | [クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922)。 | NSString | はい   |


#### エラーコード

SDKは、`TXVideoPublishListener`インターフェースを介してビデオのアップロードのステータスを監視します。従って、`TXPublishResult`の`retCode`を使用して、ビデオの公開状況を確認することができます。

| エラーコード  | TVCCommonにおいて対応する定数           | 意味              |
| :--: | :---------------------------- | :-------------- |
|  0   | TVC_OK                        | アップロードに成功しました。            |
| 1001 | TVC_ERR_UGC_REQUEST_FAILED         |  アップロードリクエストが失敗しました。通常、クライアントの署名が期限切れまたは無効になっており、Appに別の署名を再申請する必要があります。                 |
| 1002 | TVC_ERR_UGC_PARSE_FAILED      | リクエスト情報の解析に失敗しました。        |
| 1003 | TVC_ERR_VIDEO_UPLOAD_FAILED   | ビデオのアップロードに失敗しました。          |
| 1004 | TVC_ERR_COVER_UPLOAD_FAILED   | カバーのアップロードに失敗しました。          |
| 1005 | TVC_ERR_UGC_FINISH_REQ_FAILED | アップロード終了リクエストに失敗しました。        |
|  1006 | TVC_ERR_UGC_FINISH_RSP_FAILED | アップロード終了の応答に失敗しました。        |



## 画像とメディアのアップロードインターフェースの説明

アップロードオブジェクトの初期化：`TXUGCPublish::initWithUserID`

| パラメータ名   | パラメータの説明               | タイプ        | 入力必須   |
| ------ | ------------------ | --------- | ---- |
| userID | userID。ユーザーを区別するために使用されます。 | NSString | いいえ    |

アップロードの開始：`TXUGCPublish.publishMedia`

| パラメータ名  | パラメータの説明 | タイプ              | 入力必須   |
| ----- | ---- | --------------- | ---- |
| param | パラメータを公開します。 | TXMediaPublishParam | はい    |

アップロードパラメータ：`TXMediaPublishParam`

| パラメータ名         | パラメータの説明                               | タイプ        | 入力必須   |
| ------------ | ---------------------------------- | --------- | ---- |
| signature    | [クライアントからのアップロード署名](https://cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/266/33922)。 | NSString* | はい    |
| mediaPath    | ローカル画像/メディアファイルパス。                           | NSString* | はい    |
| fileName     | Tencent Cloudにアップロードされた画像/メディアファイル名です。空のままの場合、デフォルトでローカルファイル名が使用されます。  | NSString*  | いいえ    |
| enableResume | 中断ポイントからの再開の有効無効を指定。デフォルトでは有効になっています。                  | BOOL      | いいえ    |
| enableHttps  | HTTPSの有効無効を指定。デフォルトでは無効になっています。                    | BOOL      | いいえ    |


アップロードコールバックの設定：`TXUGCPublish.TXMediaPublishListener`

| メンバー変数名   | 変数の説明        | タイプ                     | 入力必須   |
| -------- | ----------- | ---------------------- | ---- |
| mediaDelegate | アップロードの進行状況と結果のコールバックを監視します。 | TXMediaPublishListener | はい    |


アップロード進行状況のコールバック：`onMediaPublishProgress`

| 変数名        | 変数の説明     | タイプ        |
| ----------- | -------- | --------- |
| uploadBytes | アップロード済みのバイト数。 | NSInteger |
| totalBytes  | 合計バイト数。     | NSInteger |

アップロード結果のコールバック：`onMediaPublishComplete`

| 変数名   | 変数の説明 | タイプ               |
| ------ | ---- | ---------------- |
| result | アップロード結果。 | TXMediaPublishResult |

アップロードイベントのコールバック：`onMediaPublishEvent`

| 変数名   | 変数の説明 | タイプ               |
| ------ | ---- | ---------------- |
| evt | デバッグ情報を出力するためのイベント。 | NSDictionary |

アップロード結果：`TXMediaPublishResult`

| メンバー変数名   | 変数の説明      | タイプ        |
| -------- | --------- | --------- |
| retCode  | エラーコード。       | int       |
| descMsg  | アップロード失敗のエラー説明。 | NSString |
| mediaId  | 画像/メディアファイルID。  | NSString |
| mediaURL | 画像/メディアストレージアドレス。    | NSString |

事前アップロード：`TXUGCPublishOptCenter.prepareUpload`
    
| パラメータ名  | パラメータの説明                                     | タイプ   | 入力必須 |
| --------- | -------------------------------------------- | ------ | ---- |
| signature | [クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922)。 | NSString | はい   |


#### エラーコード

SDKは、`TXMediaPublishListener`インターフェースを介して画像/メディアのアップロードのステータスを監視します。従って、`TXMediaPublishResult`の`retCode`を使用して、画像/メディアの状況を確認することができます。

| エラーコード  | TVCCommonにおいて対応する定数           | 意味              |
| :--: | :---------------------------- | :-------------- |
|  0   | MEDIA_PUBLISH_RESULT_OK                        | アップロードに成功しました。            |
| 1001 | MEDIA_PUBLISH_RESULT_UPLOAD_REQUEST_FAILED    | アップロードリクエストが失敗しました。通常、クライアントの署名が期限切れまたは無効になっており、Appに別の署名を再申請する必要があります。         |
| 1002 | MEDIA_PUBLISH_RESULT_UPLOAD_RESPONSE_ERROR      | リクエスト情報の解析に失敗しました。        |
| 1003 | MEDIA_PUBLISH_RESULT_UPLOAD_VIDEO_FAILED   | 画像/メディアのアップロードに失敗しました。           |
| 1005 | MEDIA_PUBLISH_RESULT_PUBLISH_REQUEST_FAILED | アップロードリクエストの終了に失敗しました。        |
| 1006 | MEDIA_PUBLISH_RESULT_PUBLISH_RESPONSE_ERROR |アップロード終了の応答に失敗しました。        |





