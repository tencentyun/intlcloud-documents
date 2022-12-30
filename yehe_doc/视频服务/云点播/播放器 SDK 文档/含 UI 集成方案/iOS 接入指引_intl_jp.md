## 製品概要

Tencent Cloud View Cube iOSプレーヤーコンポーネントは、Tencent Cloudによるオープンソースのプレーヤーコンポーネントです。簡単な数行のコードで、Tencent Videoのような強力な再生機能を備えることができます。画面の縦横切り替え、解像度の選択、ジェスチャー、ミニウィンドウなどの基本機能を備えるほか、ビデオキャッシュ、ソフトウェア/ハードウェアデコードの切り替え、倍速再生などの特殊機能もサポートしています。システムのプレーヤーよりも、サポートする形式が多く、互換性に優れ、機能もより強力です。同時に、トップ画面の秒速起動、低遅延などの優位性、ならびにビデオサムネイルなどの高度な機能も備えています。

プレーヤーコンポーネントでは業務上の個別のニーズを満たせない場合で、なおかつお客様にある程度の開発経験がおありの場合は、Player+を統合し、プレーヤーインターフェースおよび再生機能のカスタム開発を行うことも可能です。

## 準備作業
1. [VOD](https://intl.cloud.tencent.com/product/vod)関連サービスを有効化します。未登録のユーザーはアカウントを登録し、[無料試用](https://intl.cloud.tencent.com/login)できます。
2. Xcodeをダウンロードします。すでにダウンロードしている場合は、この手順をスキップして、App Storeに移動し、ダウンロードとインストールを実行できます。
3. Cocoapodsをダウンロードします。すでにダウンロードしている場合は、この手順をスキップして、[Cocoapods公式サイト](https://cocoapods.org/)に移動し、ガイドに従ってインストールできます。

## このドキュメントから把握できること
- [Tencent Cloud View Cube iOSプレーヤーコンポーネントの統合方法](#step1)
- [プレイヤーの作成・使用方法](#step3)

## 統合の準備
[](id:step1)
### 手順1：プロジェクトのダウンロード
Tencent Cloud View Cube iOSプレーヤーのプロジェクトアドレスは、[LiteAVSDK/Player_iOS](https://github.com/LiteAVSDK/Player_iOS)です。

Tencent Cloud View Cube iOSプレーヤーコンポーネントプロジェクトのダウンロードは、 **[プレーヤーコンポーネントZIPパッケージのダウンロード](#zip)**、または**[Gitコマンドでのダウンロード](#git)**のいずれかの方法で行えます。
<dx-tabs>
::: プレーヤーコンポーネントZIPパッケージのダウンロード[](id:zip)
次のプレーヤーコンポーネントZIPパッケージを直接ダウンロードできます。ページの**Code** > **Download ZIP**をクリックしてダウンロードしてください
![](https://qcloudimg.tencent-cloud.cn/raw/a38a9995bfe13d645bcd1d2e5242a297.png)
:::
::: Gitコマンドのダウンロード[](id:git)
1. まず、Gitがコンピュータにインストールされていることを確認します。インストールされていない場合は、[Gitのインストールチュートリアル](https://git-scm.com/downloads)を参照し、インストールしてください。
2. 次のコマンドを実行し、プレーヤーコンポーネントのプロジェクトコードをローカルにcloneします。
```shell
git clone git@github.com:tencentyun/SuperPlayer_iOS.git
```
   以下のメッセージが表示されたら、プロジェクトコードがローカルにcloneされました。
```shell
'SuperPlayer_iOS'に複製中...
remote: Enumerating objects: 2637, done.
remote: Counting objects: 100% (644/644), done.
remote: Compressing objects: 100% (333/333), done.
remote: Total 2637 (delta 227), reused 524 (delta 170), pack-reused 1993
オブジェクトの受信中：100% (2637/2637)、571.20 MiB | 3.94 MiB/s、完了。
deltaの処理中：100% (1019/1019)、完了。
```
プロジェクトをダウンロードして、プロジェクトソースコードを解凍した後のディレクトリは以下のとおりです。
<table>
<thead><tr><th>ファイル名</th><th>機能</th></tr></thead>
<tbody>
<tr><td>SDK</td>
<td>プレーヤーを保存するframework静的ライブラリ</td>
</tr><tr>
<td>Demo</td><td>Super Playerを保存するDemo</td>
</tr><tr>
<td>App</td><td>アプリケーションのエントリーインターフェース</td>
</tr><tr>
<td>SuperPlayerDemo</td><td>Super Player Demo</td>
</tr><tr><td>SuperPlayerKit</td><td>Super Playerコンポーネント</td>
</tr></tbody></table>
:::
</dx-tabs>

[](id:step2)
### 手順2：統合ガイド
この手順は、プレーヤーを統合する方法をユーザーにガイドするために使用されます。ユーザーは、**[Cocoapods統合](#cocoapods)**または**[SDKの手動ダウンロード](#manual)**を使用して現在のプロジェクトにインポートすることをお勧めします。
<dx-tabs>
::: Cocoapods統合[](id:cocoapods)
1. このプロジェクトはCocoapodsのインストールをサポートしています。次のコードをPodfileに追加するだけでよいです。
（1）Pod方式で直接SuperPlayerを統合します
```objective-c
pod 'SuperPlayer
```
  Player版に依存する必要がある場合は、podfileファイルに以下の依存関係を追加することができます。
```objective-c
pod 'SuperPlayer/Player'
```
Player_Premium版に依存する必要がある場合は、podfileファイルに以下の依存関係を追加することができます。

```objective-c
pod 'SuperPlayer/Player_Premium'  
```

プロフェッショナル版に依存する必要がある場合は、podfileファイルに以下の依存関係を追加することができます

```objective-c
pod 'SuperPlayer/Professional'
```

2. `pod install`または`pod update`を実行します。

:::
::: SDKの手動ダウンロード[](id:manual)
1. SDK + Demo開発パッケージをダウンロードします。Tencent Cloud View Cube iOSプレーヤーのプロジェクトは、[LiteAVSDK/Player_iOS](https://github.com/LiteAVSDK/Player_iOS)です。
2. `TXLiteAVSDK_Player_Premium.framework`をプロジェクトにインポートし、`Do Not Embed`にチェックを入れます。
3.Demo/TXLiteAVDemo/SuperPlayerKit/SuperPlayerを自身のプロジェクトディレクトリ下にコピーします。
4. SuperPlayerが依存するサードパーティライブラリにはAFNetworking、SDWebImage、Masonry、TXLiteAVSDK_Playerが含まれます
 1. 手動でTXLiteAVSDK_Playerを統合する場合は、必要なシステムライブラリとlibraryを追加する必要があります。
<b>システムFrameworkライブラリ</b>：MetalKit, ReplayKit, SystemConfiguration, CoreTelephony, VideoToolbox, CoreGraphics, AVFoundation, Accelerate, MobileCoreServices, ,VideoToolbox
<b>システムLibraryライブラリ:</b> libz, libresolv,  libiconv, libc++, libsqlite3
具体的な手順は以下を[ご参照](https://www.tencentcloud.com/document/product/266/49669)ください。カスタム開発 - VODシナリオ - アクセスドキュメント - SDK統合 ステップ1 - 手動でSDKを統合する
さらにTXLiteAVSDK_Playerファイル下のTXFFmpeg.xcframeworkと TXSoundTouch.scframeworkを動的ライブラリの方式で次の図に示すように追加してください。
![](https://qcloudimg.tencent-cloud.cn/raw/5834caae21d3413522c7d51d4b3b57b0.png)
 2. Podを使用した方式でTXLiteAVSDK_Playerを統合する場合は、ライブラリを追加する必要はありません。


:::
</dx-tabs>

[](id:step3)
### 手順3：プレーヤー機能の使用
この手順は、ユーザーがプレーヤーを作成・使用し、プレーヤーでビデオを再生できるようにガイドするのに使用されます。

1. **プレーヤーの作成：**[](id:usePlayer)
プレーヤーのメインクラスは、`SuperPlayerView`です。作成後すぐにビデオを再生できます。
```xml
// ヘッダーファイルの導入
#import <SuperPlayer/SuperPlayer.h>

// プレーヤーの作成  
_playerView = [[SuperPlayerView alloc] init];
// イベントを受信するための、プロキシの設定
_playerView.delegate = self;
// 親Viewの設定。_playerViewがholderViewの下に自動的に追加されます
_playerView.fatherView = self.holderView;
```

2. **License権限承認の設定**
すでに関連するLicense権限承認を取得している場合は、[Tencent Cloud View Cubeコンソール](https://console.cloud.tencent.com/vcube)にて、License URLおよびLicense Keyを取得する必要があります。

License権限承認を取得していない場合は、先に<a href="https://cloud.tencent.com/document/product/881/74588">ビデオ再生License</a>をご参照の上、関連の権限承認を取得する必要があります。
<br>License情報を取得後、SDKの関連インターフェースを呼び出す前に、次のインターフェースでLicenseを初期化します。`- [AppDelegate application:didFinishLaunchingWithOptions:]` に以下の設定を行うことをお勧めします。
```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<取得したlicenseUrl>";
    NSString * const licenceKey = @"<取得したkey>";
        
    //TXLiveBaseは"TXLiveBase.h"ヘッダーファイルの中にあります
    [TXLiveBase setLicenceURL:licenceURL key:licenceKey]; 
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}
```

3.  **ビデオの再生：**
このステップは、ビデオ再生の方法についてユーザーにご説明するためのものです。Tencent Cloud View Cube iOSプレーヤーコンポーネントは[VOD FileId](#fileid)または[URLを使用](#url)する再生をサポートしています。 **FileIdの統合**を選択して、より拡充された機能を利用することをお勧めします。
<dx-tabs>
::: VOD FileIdによる再生[](id:fileid)
ビデオFileIdは、通常、ビデオのアップロード後にサーバーから返されます。

1. クライアントからビデオが公開されると、サーバーがFileIdをクライアントに返します。
2. サーバーからのビデオアップロード時、アップロード確認の通知に対応するFileIdが含まれています。
ファイルがすでにTencent Cloudに存在する場合は、[メディア資産管理](https://console.cloud.tencent.com/vod/media)にアクセスし、該当するファイルをさがして、FileIdを確認できます。下図のように、IDのところにFileIdが表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/f089346e01ab8e44e42f28c965809b9c.png)

<dx-alert infotype="notice">
1. FileIdを使用して再生する場合は、初めにAdaptive-HLS(10)トランスコードテンプレートを使用してビデオのトランスコードを行うか、またはプレーヤーコンポーネントの署名psignを使用して再生するビデオを指定する必要があります。これらを行わないと、ビデオ再生が失敗する可能性があります。トランスコードのチュートリアルおよび説明については [プレーヤーコンポーネントを使用したビデオ再生](https://intl.cloud.tencent.com/document/product/266/38098)を、psign生成のチュートリアルについては[psignチュートリアル](https://intl.cloud.tencent.com/document/product/266/38099)をそれぞれご参照ください。
2. FileIdを使用して再生する際に「no v4 play info」エラーが表示された場合は、上記の問題が存在する可能性があることを示しているため、上記のチュートリアルに従って調整することをお勧めします。また、ソースビデオの再生リンクを直接取得し、[URLによる再生](#url) 方式で再生することもできます。
3. **トランスコードを行っていないソースビデオを再生すると、互換性がない場合がありますので、トランスコードをご使用後にビデオを再生することをお勧めします。**
</dx-alert>

<dx-codeblock>
:::  java
//リンク不正アクセス防止を有効にせずに再生を行い、その途中で「no v4 play info」エラーが表示された場合は、Adaptive-HLS(10)トランスコードテンプレートを使用してビデオのトランスコードを行うか、またはソースビデオの再生リンクを直接取得し、url方式で再生することをお勧めします。

SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329071;// AppIdを設定
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710173650"; // FileIdを設定
// psignはプレーヤーの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://intl.cloud.tencent.com/document/product/266/38099
model.videoId.pSign = @"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
[_playerView playWithModelNeedLicence:model];
:::
</dx-codeblock>
:::
::: URLによる再生[](id:url)
```java
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.videoURL = @"http://your_video_url.mp4";   // ビデオ再生urlを設定
[_playerView playWithModelNeedLicence:model];
```
:::
</dx-tabs>
- **再生の終了：**[](id:exitPlayer)
プレーヤーが不要な時には、`resetPlayer`を呼び出してプレーヤー内部の状態を消去し、メモリをリリースします。
```java
[_playerView resetPlayer];
```

これで、Tencent Cloud View Cube iOSプレーヤーコンポーネントの作成、ビデオ再生、再生終了機能の統合が完了しました。

[](id:moreFeature)
## 機能の使用[](id:moreFeature)

### 1. 全画面再生

プレーヤーコンポーネントは全画面再生をサポートしています。全画面再生のシーンでは、同時に画面ロック、ジェスチャーによる音量と明るさの制御、弾幕、スクリーンショット、解像度の切り替えなどの機能設定がサポートされます。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント**で体験できます。画面右下隅の**全画面**をクリックすると、全画面再生画面に進むことができます。


ウィンドウ再生モードでは、次のインターフェースを呼び出すことで全画面再生モードに入ることができます。

```objective-c
- (void)superPlayerFullScreenChanged:(SuperPlayerView *)player {
  //ここで、ユーザーは全画面表示に切り替えた後のロジックをカスタマイズできます
}
```

#### 全画面再生インターフェースの機能概要


<dx-tabs>
::: ウィンドウモードに戻る[](id:window)
**戻る**ボタンでウィンドウ再生モードに戻ることができます。クリックすると、SDKが全画面切り替えのロジックを処理した後にトリガーされるプロキシメソッドは次のとおりです。

```objective-c
// 戻るイベント
- (void)superPlayerBackAction:(SuperPlayerView *)player;
左上隅の戻るボタンをクリックするとトリガーされます
// 全画面変更通知
- (void)superPlayerFullScreenChanged:(SuperPlayerView *)player;
```
:::
::: 画面ロック[](id:screenlock)
画面ロック操作により、ユーザーは没入的な再生状態に入ることができます。クリックした後にSDK自身によって処理され、コールバックがありません。

```objective-c
// ユーザーは、次のインターフェースを介して画面をロックするかどうかを制御できます
@property(nonatomic, assign) BOOL isLockScreen;
```
:::
::: 弾幕[](id:barrage)
弾幕機能をオンにすると、ユーザーが送信したテキストが画面に表示されます。

ここで、SPDefaultControlViewオブジェクトを取得し、プレーヤーviewの初期化時にSPDefaultControlViewの弾幕ボタンのイベントを設定します。弾幕の内容と弾幕viewは、ユーザー自身でカスタマイズする必要があります。詳細については、SuperPlayerDemoの下のCFDanmakuView、CFDanmakuInfo、およびCFDanmakuをご参照ください。

```objective-c
SPDefaultControlView *dv = (SPDefaultControlView *)**self**.playerView.controlView;
[dv.danmakuBtn addTarget:**self** action:**@selector**(danmakuShow:) forControlEvents:UIControlEventTouchUpInside];
```

CFDanmakuView：弾幕のプロパティは初期化時に構成します。

```objective-c
// 以下のプロパティはすべて構成する必要があります--------
// 弾幕動画の時間
@property(nonatomic, assign) CGFloat duration;
// 中央上部/下部の弾幕動画の時間
@property(nonatomic, assign) CGFloat centerDuration;
// 弾幕の弾道の高さ
@property(nonatomic, assign) CGFloat lineHeight;
// 弾幕の弾道間の間隔
@property(nonatomic, assign) CGFloat lineMargin;

// 弾幕の弾道の最大行数
@property(nonatomic, assign) NSInteger maxShowLineCount;

// 弾幕の弾道の中央上部/下部の最大行数
@property(nonatomic, assign) NSInteger maxCenterLineCount;
```
:::
::: スクリーンショット[](id:screenshot)
プレーヤーコンポーネントは再生中にその時点のビデオフレームを切り取ることができる機能をご提供します。画像を保存して共有することができます。スクリーンショットボタンをクリックすると、SDKの内部で処理が行われ、スクリーンショットが成功したかどうかのコールバックは行われません。スクリーンショットした画像のディレクトリはスマートフォンのアルバムとなります。
:::
::: 解像度の切り替え[](id:resolution)
ユーザーは、HD、SD、UHDなど、ニーズに応じて異なるビデオ再生の解像度を選択できます。クリック後にトリガーされる解像度viewの表示と解像度オプションのクリック操作は、コールバックなしでSDK内部によってに処理されます。
:::
</dx-tabs>


### 2. フローティングウィンドウによる再生

プレーヤーコンポーネントはフローティングウィンドウによるミニウィンドウ再生をサポートしています。アプリケーション内の他のページに切り替えてもビデオ再生が中断しない機能です。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント**で体験できます。画面左上隅の**戻る**をクリックすると、フローティングウィンドウ再生機能を体験できます。

<img src="https://qcloudimg.tencent-cloud.cn/raw/e8a774cb9833f2de45fc1cf3cc928ee4.png" style="zoom:25%;" />



```objective-c
// 画面が縦向きになっており、再生中である場合、戻るボタンをクリックすると、インターフェースがトリガーされます
[SuperPlayerWindowShared setSuperPlayer:self.playerView];
[SuperPlayerWindowShared show];
// フローティングウィンドウをクリックして、ウィンドウによってトリガーされたコードインターフェースが返されます
SuperPlayerWindowShared.backController = self;
```

### 3. ビデオカバー

プレーヤーコンポーネントはユーザーによるビデオカバーのカスタマイズをサポートしています。これはユーザーがビデオの最初のフレーム画面の再生コールバックを受信する前の表示に用いられます。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **カバーカスタマイズのデモンストレーション**ビデオで体験できます。


* プレーヤーコンポーネントを自動再生モード`PLAY_ACTION_AUTO_PLAY`に設定すると、ビデオが自動再生されます。このとき、ビデオの最初のフレームをロードするまでの間はカバーが表示されます。
* プレーヤーコンポーネントを手動再生モード`PLAY_ACTION_MANUAL_PLAY`に設定すると、ユーザーが**再生**をクリックしなければ再生が開始されません。**再生**をクリックするまでの間はカバーが表示されます。**再生**をクリックした後、ビデオの最初のフレームをロードするまでの間もカバーが表示されます。

ビデオカバーは、ネットワークURLアドレスまたはローカルFileアドレスの使用をサポートしています。使用方法については、下記のガイドをご参照ください。FileIDでビデオを再生する場合は、VODでビデオカバーを直接構成できます。

```objective-c
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
SuperPlayerVideoId *videoId = [SuperPlayerVideoId new];
videoId.fileId = @"8602268011437356984"; 
model.appId = 1400329071;
model.videoId = videoId;
//再生モードは、自動再生モード：PLAY_ACTION_AUTO_PLAYまたは手動再生モード：PLAY_ACTION_MANUAL_PLAYに設定できます
model.action  = PLAY_ACTION_MANUAL_PLAY; 
//カバーのアドレスをネットワークのurlアドレスに設定する場合、coverPictureUrlを設定しなければ、VODコンソールが設定したカバーが自動的に使用されます
model.customCoverImageUrl = @"http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/cc1e28208602268011087336518/MXUW1a5I9TsA.png"; 
[self.playerView playWithModelNeedLicence:model];
```

### 4. ビデオリストによるカルーセル

プレーヤーコンポーネントはビデオリストの繰り返し再生をサポートしています。ビデオリストを指定すると、次のようになります。

* リスト内のビデオを順番に繰り返し再生することをサポートし、再生プロセス中に次のビデオを自動的に再生すること、および次のビデオに手動で切り替えることをサポートします。
* リストにある最後のビデオの再生が終了すると、リスト内にある最初のビデオは自動的に再生されます。

機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **ビデオリストの繰り返し再生のデモンストレーション**ビデオで体験できます。



```objective-c
//手順1：カルーセルデータのNSMutableArrayの構成
NSMutableArray *modelArray = [NSMutableArray array];
SuperPlayerModel *model = [SuperPlayerModel new];
SuperPlayerVideoId *videoId = [SuperPlayerVideoId new];
videoId.fileId = @"8602268011437356984"; 
model.appId = 1252463788;
model.videoId = videoId;
[modelArray addObject:model];

model = [SuperPlayerModel new];
videoId = [SuperPlayerVideoId new];
videoId.fileId = @"4564972819219071679";
model.appId = 1252463788;
model.videoId = videoId;
[modelArray addObject:model];

//手順2：SuperPlayerViewのカルーセルインターフェースの呼び出し
[self.playerView playWithModelListNeedLicence:modelArray isLoopPlayList:YES startIndex:0];
```

```objective-c
(void)playWithModelListNeedLicence:(NSArray *)playModelList isLoopPlayList:(BOOL)isLoop startIndex:(NSInteger)index;
```

インターフェースパラメータの説明

| パラメータ名         | タイプ   | 説明                                   |
| ------------- | --------- | --------- |
| playModelList | NSArray * | データリストのカルーセル    |
| isLoop        | Boolean   | 繰り返すかどうか      |
| index         | NSInteger | 再生を開始したビデオのインデックス |


### 5、ピクチャーインピクチャー機能

ピクチャーインピクチャー（PictureInPicture）はiOS 9でリリースされていますが、以前はiPad上でしか使用できませんでした。iPhoneでピクチャーインピクチャーを使用するにはiOS 14にアップデートすれば使用することができます。
現在Tencent Cloudプレーヤーはアプリケーション内およびアプリケーション外のピクチャーインピクチャー機能をサポートし、ユーザーのニーズを満たすことができます。使用するにはバックグラウンドモードを開く必要があります。ステップは次のとおりです。XCodeで対応するTarget -> Signing & Capabilities -> Background Modesを選択し、「Audio, AirPlay, and Picture in Picture」にチェックを入れます。
![](https://qcloudimg.tencent-cloud.cn/raw/116e1e741f80d810502221fd143d8434.png)



ピクチャーインピクチャー機能を使用したサンプルコードの例：																								

```objective-c
// ピクチャーインピクチャーに進む
 if (![TXVodPlayer isSupportPictureInPicture]) {
    return;
 }
 [_vodPlayer enterPictureInPicture];

// ピクチャーインピクチャーを終了する
[_vodPlayer exitPictureInPicture];
```

### 6、ビデオのプレビュー

プレーヤーコンポーネントはビデオプレビュー機能をサポートしています。これは非VIPプレビューなどのシーンに適用でき、開発者は異なるパラメータを渡してビデオのプレビュー時間、プロンプト情報、プレビュー終了画面などを制御することができます。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **プレビュー機能のデモンストレーション**ビデオで体験できます。



```objective-c
 //ステップ1：プレビューmodelの作成
 TXVipWatchModel *model = [[TXVipWatchModel alloc] init];
 model.tipTtitle = @"15秒のプレビューが可能、VIPをアクティブ化すると完全なビデオを視聴可能";
 model.canWatchTime = 15;
 //ステップ2：プレビューmodelの設定
 self.playerView.vipWatchModel = model;
 //手順3：メソッドの呼び出しによるトライアル視聴機能のデモンストレーション
 [self.playerView showVipTipView];
```

  TXVipWatchModelタイプのパラメータの説明：

| パラメータ名         | タイプ   | 説明                                   |
| ------------ | -------- | --------- |
| tipTtitle    | NSString | トライアル視聴のヒント情報    |
| canWatchTime | float    | トライアル視聴時間の長さ（単位：秒） |

### 7、動的ウォーターマーク

プレーヤーコンポーネントは再生画面での、不規則に動くテキストウォーターマークの追加をサポートし、不正録画を効果的に防止します。ウォーターマークは全画面再生モードおよびウィンドウ再生モードのどちらでも表示でき、開発者はウォーターマークのテキスト、文字サイズ、色を変更することができます。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **動的ウォーターマークのデモンストレーション**ビデオで体験できます。



```objective-c
//手順1：ビデオのソース情報modelの作成
SuperPlayerModel *  playermodel   = [SuperPlayerModel new];
//ビデオソースのその他の情報の追加
//手順2：ダイナミックウォーターマークmodelの作成
DynamicWaterModel *model = [[DynamicWaterModel alloc] init];
//手順3：ダイナミックウォーターマークデータの設定
model.dynamicWatermarkTip = @"shipinyun";
model.textFont = 30;
model.textColor = [UIColor colorWithRed:255.0/255.0 green:255.0/255.0 blue:255.0/255.0 alpha:0.8];
playermodel.dynamicWaterModel = model;
//手順4：メソッドの呼び出しによるダイナミックウォーターマークのデモンストレーション
[self.playerView playWithModelNeedLicence:playermodel];
```

DynamicWaterModelタイプのパラメータの説明：

| パラメータ名         | タイプ   | 説明                                   |
| ------------------- | -------- | ------ |
| dynamicWatermarkTip | NSString | ウォーターマークのテキスト情報 |
| textFont            | CGFloat  | テキストサイズ   |
| textColor           | UIColor  | テキストの色   |

### 8. 動画のダウンロード

ユーザーがネットワークに接続している状態でビデオをキャッシュした場合、ネットワークに接続していない状態でもビデオを視聴することができます。またオフラインキャッシュしたビデオはクライアント内だけで視聴でき、ローカルへのダウンロードはできないため、ダウンロードしたビデオの違法配信を効果的に防止し、ビデオのセキュリティを保護することができます。
Tencent Cloud View Cube App > プレーヤー > プレーヤーコンポーネント > オフラインキャッシュ（全画面）のデモンストレーションビデオで、全画面視聴モードを使用して体験できます。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/rUaM578_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_1669772078943.png" style="zoom: 500%;" />

VideoCacheView（キャッシュ選択リストビュー）は、対応する解像度のビデオを選択してダウンロードするために使用します。左上隅で解像度を選択し、ダウンロードしたいビデオオプションをクリックし、チェックマークが表示された場合はダウンロードを開始したことを表します。下のvideo download listボタンをクリックすると、VideoDownloadListViewのあるActivityにリダイレクトします。

```objective-c
// ステップ1：キャッシュ選択リストビューの初期化
//@property (nonatomic, strong) VideoCacheView *cacheView;
_cacheView = [[VideoCacheView alloc] initWithFrame:CGRectZero];
_cacheView.hidden = YES;
[self.playerView addSubview:_cacheView];

// ステップ2：再生中のビデオオプションの設定
[_cacheView setVideoModels:_currentPlayVideoArray currentPlayingModel:player.playerModel];

// video download listボタンのクリックイベント
- (UIButton *)viewCacheListBtn;
```

```objective-c
- (void)setVideoModels:(NSArray *)models currentPlayingModel:(SuperPlayerModel *)currentModel;
```

インターフェースパラメータの説明

| パラメータ名           | タイプ         | 説明                     |
| ---------------- | ------------ | ------------------------ |
| models           | NSArray      | ダウンロードリストのビデオデータモデル   |
| SuperPlayerModel | currentModel | 現在再生中のビデオデータモデル |

VideoCacheListView（ビデオダウンロードリスト）には、現在ダウンロード中およびダウンロードが完了したビデオのリストViewが表示されます。クリックすると、現在ダウンロード中の場合はダウンロードが一時停止します。ダウンロード一時停止中の場合はダウンロードを再開します。ダウンロードが完了している場合はジャンプして再生します。

<img src="http://1400155958.vod2.myqcloud.com/facd87c8vodcq1400155958/a69c6b2c387702307128674240/wt31IYPsdQoA.jpg" style="zoom: 33%;" />



```objective-c
// データを追加します。データはTXVodDownloadManager#getDownloadMediaInfoListインターフェースから取得します
NSArray<TXVodDownloadMediaInfo *> *array = [[[TXVodDownloadManager shareInstance] getDownloadMediaInfoList] mutableCopy];
for (TXVodDownloadMediaInfo *info in array) {
    VideoCacheListModel *model = [[VideoCacheListModel alloc] init];
    model.mediaInfo = info;
    [self.videoCacheArray addObject:model];
}

// リストの項目はクリックして再生、長押しで削除などの操作をサポートしています
- (void)longPress:(UILongPressGestureRecognizer *)longPress;  // 長押し
```

### 9、スプライトイメージおよびキーモーメント情報

#### キーモーメント情報

プログレスバーの重要な位置に文字説明を追加し、ユーザーがクリックするとキーモーメント位置の文字情報を表示できるようにすることで、現在の位置のビデオ情報を素早く把握することができます。ビデオ情報をクリックすると、キーモーメント情報の位置をseekすることができます。

Tencent Cloud View Cube App > プレーヤー > プレーヤーコンポーネント > Tencent Cloudビデオで、全画面視聴モードを使用して体験できます。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/Qc3t442_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16697206995071%20%281%29.png)

#### スプライトイメージ

ユーザーがプログレスバーのドラッグまたは早送り操作を行う際に、ビデオのサムネイルを確認して指定の場所のビデオ内容をすぐに把握できるようにしています。サムネイルプレビューはビデオのスプライトイメージをベースにして実現します。VODコンソールでビデオファイルのスプライトイメージを生成するか、またはスプライトイメージファイルを直接生成することができます。
Tencent Cloud View Cube App > プレーヤー > プレーヤーコンポーネント > Tencent Cloudビデオで、全画面視聴モードを使用して体験できます。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/Ii2h727_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16697206895960%20%281%29.png)

```objective-c
// ステップ1：playWithModelNeedLicenceプレーヤーでビデオを再生した場合のみ、onPlayEventコールバックからスプライトイメージおよびキーモーメント情報データを取得できます
[self.playerView playWithModelNeedLicence:playerModel];

// ステップ2: playWithModelNeedLicenceでVOD_PLAY_EVT_GET_PLAYINFO_SUCCコールバックイベントからキーフレームとスプライトイメージの情報を取得します
NSString *imageSpriteVtt = [param objectForKey:VOD_PLAY_EVENT_IMAGESPRIT_WEBVTTURL]?:@"";
NSArray<NSString *> *imageSpriteList = [param objectForKey:VOD_PLAY_EVENT_IMAGESPRIT_IMAGEURL_LIST];
NSArray<NSURL *> *imageURLs = [self convertImageSpriteList:imageSpriteList];
[self.imageSprite setVTTUrl:[NSURL URLWithString:imageSpriteVtt] imageUrls:imageURLs];

// ステップ3: 取得したキーモーメント情報およびスプライトイメージを画面に表示します
if (self.isFullScreen) {
   thumbnail = [self.imageSprite getThumbnail:draggedTime];
}
if (thumbnail) {
   [self.fastView showThumbnail:thumbnail withText:timeStr];
}
```



## Demo体験

より完全な機能を体験するには、プロジェクトDemoを直接実行するか、QRコードをスキャンしてモバイルDemoであるTencent Cloud View Cube　Appをダウンロードしてください。

### プロジェクトDemoの実行

1. Demoディレクトリで、コマンドライン`pod update`を実行して、`TXLiteAVDemo.xcworkspace`ファイルを再度生成します。
2. プロジェクトをダブルクリックして開き、証明書を変更して、本番環境での実行を選択します。
3. Demoが正常に実行された後、**プレーヤー** > **プレーヤーコンポーネント**と進むと、プレーヤーの機能を体験できます。

[](id:qrcode)
### Tencent Cloud View Cube App

**Tencent Cloud View Cube App** > **プレーヤー**で、より多くのプレーヤーコンポーネント機能を体験できます。
Appのアップグレードやメンテナンス中も、Demoソースコードは引き続き正常に使用できます。
