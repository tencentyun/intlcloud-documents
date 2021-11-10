## 製品概要

Tencent Cloud View Cube ios Super Player Adapterは、サードパーティのプレーヤーまたは自社開発のプレーヤーを使用して開放されたクラウドPAASリソースに接続を希望する顧客向けにVODのためのプレーヤープラグインを提供します。カスタムプレーヤー機能を必要とするユーザーにおいて一般的に使用されます。

[](id:sdkDownload)
## SDKのダウンロード

Tencent Cloud View Cube iOS Super Player Adapter SDKとDemoプロジェクトのダウンロードアドレスは[TXCPlayerAdapterSDK_iOS](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TXCPlayerAdapter/Release/1.0.0/TXCPlayerAdapterSDK_1.0.0_iOS.zip)です。 

## 対象となる読者

このドキュメントの内容の一部は、Tencent Cloud専用の機能となっていますので、使用前に、[Tencent Cloud](https://intl.cloud.tencent.com)関連サービスのアクティブ化を行ってください。アカウント登録がないユーザーは登録し、[無料試用](https://intl.cloud.tencent.com/login)が可能です。

[](id:guide)
## 統合ガイド

### 環境要件

HTTPリクエストのサポートを設定するには、プロジェクトのinfo.plistファイルに`AppTransport Security Settings->AllowArbitraryLoads`を追加し、設定をYESにする必要があります。

### コンポーネント依存

`GCDWebServer`コンポーネント依存を追加します。   

```objective-c
pod "GCDWebServer", "~> 3.0"
```

GCDWebServerは軽量のHTTPサーバーで、GCDを基にしてOS XおよびiOSで使用することができます。このライブラリはWebを基にしたファイルアップロードおよびWebDAV serverなどの拡張機能も実装しています。

### プレーヤーの使用

変数ステートメント。プレーヤーのメインクラスは`TXCPlayerAdapter`です。作成後すぐにビデオを再生できます。

FileIdは、通常、ビデオのアップロード後にサーバーから返されます。

1. クライアントからビデオが公開されると、サーバーがfileIdをクライアントに返します。
2. サーバーからのビデオアップロード時、アップロード確認の通知に対応するfileIdが含まれています。


ファイルがすでにTencent Cloudに存在する場合は、[メディア資産管理](https://console.cloud.tencent.com/vod/media)にアクセスし、対応するファイルを検索することができます。クリックしてファイルを開き、右側のビデオ詳細で関連パラメータを確認することができます。

```objective-c
NSInteger appId; ////appidをTencent Cloud VODで申請します
NSString *fileId;
//psignはSuper Playerの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://intl.cloud.tencent.com/document/product/266/38099
NSString *pSign = self.pSignTextView.text;
    
TXCPlayerAdapter *adapter = [TXCPlayerAdapter shareAdapterWithAppId:appId];
```

ビデオリクエスト情報と再生：

```objective-c
id<ITXCPlayerAssistorProtocol> assistor = [TXCPlayerAdapter createPlayerAssistorWithFileId:fileId pSign:pSign];
[assistor requestVideoInfo:^(id<ITXCPlayerAssistorProtocol> response, NSError *error) {
    if (error) {
        NSLog(@"create player assistor error : %@",error);
        [self.view makeToast:error.description duration:5.0 position:CSToastPositionBottom];
        return;
    }
    [weakSelf avplayerPlay:response]; //ビデオの再生
}];



- (void)avplayerPlay:(id<ITXCPlayerAssistorProtocol>)response
{
    AVPlayerViewController *playerVC = [[AVPlayerViewController alloc] init];
    self.playerVC = playerVC;
    TXCStreamingInfo *info = response.getStreamingInfo;
    AVPlayer *player = [[AVPlayer alloc] initWithURL:[NSURL URLWithString:info.playUrl]];
    playerVC.player = player;
    playerVC.title = response.getVideoBasicInfo.name;
    [self.navigationController pushViewController:playerVC animated:YES];
    
    [player addObserver:self forKeyPath:@"status" options:NSKeyValueObservingOptionNew context:nil];
}
```

使用後にPlayerを破棄します。

```objective-c
[TXCPlayerAdapter destroy];
```



## SDKインターフェースの説明

### Adatperの初期化
Adapterを初期化します。1回のみ。

**インターフェース**

```
+ (instancetype)shareAdapterWithAppId:(NSUInteger)appId;
```

**パラメータの説明**

appId：appidを入力します（サブアプリケーションを使用している場合はsubappidを入力）。

### Adatperの破棄
Adapterを破棄します。プロセス終了後に呼び出します。

**インターフェース**

```
+ (void)destroy;
```

### プレーヤー補助クラスの作成

プレーヤー補助クラスを介して再生fileId関連情報を取得し、DRM暗号化インターフェースなどを処置することができます。

**インターフェース**

```
+ (id<ITXCPlayerAssistorProtocol>)createPlayerAssistorWithFileId:(NSString *)fileId
                                                           pSign:(NSString *)pSign;
```

**パラメータの説明**

| パラメータ名 | タイプ   | 説明               |
| :----- | :----- | :----------------- |
| fileId | String | 再生したいビデオfileId |
| pSign  | String | Super Player署名     |

### ビデオ再生情報のリクエスト

このインターフェースでは、Tencent Cloud VODサーバーをリクエストし，ビデオ再生ストリーム情報などを取得することができます。

**インターフェース**

```objective-c
- (void)requestVideoInfo:(ITXCRequestVideoInfoCallback)completion;
```

**パラメータの説明**

| パラメータ名         | タイプ                         | 説明         |
| :------------- | :--------------------------- | :----------- |
| completion | ITXCRequestVideoInfoCallback | 非同期コールバック関数 |



### プレーヤー補助クラスの破棄

補助クラスを破棄し、プレーヤーを終了するか、または次のビデオ再生に切り替える時に呼び出します。

**インターフェース**

```
+ (void)destroyPlayerAssistor:(id<ITXCPlayerAssistorProtocol>)assistor;
```



### ビデオの基本情報を取得

ビデオ情報の取得を有効にするには、`id<ITXCPlayerAssistorProtocol>.requestVideoInfo`でコールバックする必要があります。

**インターフェース**

```
- (TXCVideoBasicInfo *)getVideoBasicInfo;
```

**パラメータの説明**

TXCVideoBasicInfoパラメータは次のとおりです。

| パラメータ名      | タイプ   | 説明                 |
| :---------- | :----- | :------------------- |
| name        | String | ビデオ名           |
| size        | Int    | ビデオサイズ。単位：byte |
| duration | Float | ビデオの長さ。単位：秒  |
| description | String | ビデオの説明             |
| coverUrl | String | ビデオカバー             |



### ビデオストリーム情報を取得

ビデオストリーム情報リストの取得を有効にするには、`id<ITXCPlayerAssistorProtocol>.requestVideoInfo`でコールバックする必要があります。

**インターフェース**

```
- (TXCStreamingInfo *)getStreamingInfo;
```

**パラメータの説明**

TXCStreamingInfoパラメータは次のとおりです。

| パラメータ名     | タイプ   | 説明                                                         |
| :--------- | :----- | :----------------------------------------------------------- |
| playUrl    | String | 再生URL                                                     |
| subStreams | List   | アダプティブビットレートストリーミングサブストリーム情報。タイプは[TXCSubStreamInfo](#TXCSubStreamInfo)です|

TXCSubStreamInfoパラメータは次のとおりです。[](id:TXCSubStreamInfo)

| パラメータ名         | タイプ   | 説明                                 |
| :------------- | :----- | :----------------------------------- |
| type           | String | サブストリームのタイプ。現在設定可能な値はvideoのみです |
| width          | Int    | サブストリームのビデオの幅。単位：px              |
| height         | Int    | サブストリームのビデオの高さ。単位：px               |
| resolutionName | String | プレーヤーで表示するサブストリームのビデオの仕様名       |

### キーフレームキーモーメント情報を取得

ビデオのキーフレームキーモーメント情報の取得を有効にするには、`id<ITXCPlayerAssistorProtocol>.requestVideoInfo`でコールバックする必要があります。

**インターフェース**

```
- (NSArray<TXCKeyFrameDescInfo *> *)getKeyFrameDescInfos;
```

**パラメータの説明**

TXCKeyFrameDescInfoパラメータは次のとおりです。

| パラメータ名     | タイプ   | 説明          |
| :--------- | :----- | :------------ |
| timeOffset | Float  | 1.1           |
| content    | String | 「オープニングスタート...」 |



### サムネイル情報を取得

サムネイル情報の取得を有効にするには、`id<ITXCPlayerAssistorProtocol>.requestVideoInfo`でコールバックする必要があります。

**インターフェース**

```
- (TXCImageSpriteInfo *)getImageSpriteInfo;
```

**パラメータの説明**

TCXImageSpriteInfo パラメータは次のとおりです。

| パラメータ名    | タイプ   | 説明                               |
| :-------- | :----- | :--------------------------------- |
| imageUrls | List   | サムネイルダウンロードURLアレイ。タイプはStringです |
| webVttUrl | String | サムネイルVTTファイルダウンロードURL            |
