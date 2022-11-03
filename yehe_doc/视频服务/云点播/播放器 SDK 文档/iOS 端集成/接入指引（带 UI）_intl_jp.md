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
  プロフェッショナル版に依存する必要がある場合は、podfileファイルに以下の依存関係を追加することができます
```objective-c
pod 'SuperPlayer/Professional'
```

2. `pod install`または`pod update`を実行します。

:::
::: SDKの手動ダウンロード[](id:manual)
1. SDK + Demo開発パッケージをダウンロードします。Tencent Cloud View Cube iOSプレーヤーのプロジェクトは、[LiteAVSDK/Player_iOS](https://github.com/LiteAVSDK/Player_iOS)です。
2. `TXLiteAVSDK_Player.framework`をプロジェクトにインポートし、`Do Not Embed`にチェックを入れます。
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

2.  **ビデオの再生：**
このステップは、ビデオ再生の方法についてユーザーにご説明するためのものです。Tencent Cloud View Cube iOSプレーヤーコンポーネントは[VOD FileId](#fileid)または[URLを使用](#url)する再生をサポートしています。 **FileIdの統合**を選択して、より拡充された機能を利用することをお勧めします。
<dx-tabs>
::: VOD FileIdによる再生[](id:fileid)
ビデオFileIdは、通常、ビデオのアップロード後にサーバーから返されます。

   1. クライアントからビデオが公開されると、サーバーがFileIdをクライアントに返します。
   2. サーバーからのビデオアップロード時、アップロードの確認の通知の中に対応するFileIdが含まれています。
ファイルがすでにTencent Cloudに存在する場合は、[メディア資産管理](https://console.cloud.tencent.com/vod/media)にアクセスし、該当するファイルをさがして、FileIdを確認できます。下図のように、IDのところにFileIdが表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/f089346e01ab8e44e42f28c965809b9c.png)

<dx-alert infotype="notice">
1. FileIdを使用して再生する場合は、初めにAdaptive-HLS(10)トランスコードテンプレートを使用してビデオのトランスコードを行うか、またはプレーヤーコンポーネントの署名psignを使用して再生するビデオを指定する必要があります。これらを行わないと、ビデオ再生が失敗する可能性があります。トランスコードのチュートリアルおよび説明については [プレーヤーコンポーネントを使用したビデオ再生](https://intl.cloud.tencent.com/document/product/266/38098)を、psign生成のチュートリアルについては[psignチュートリアル](https://intl.cloud.tencent.com/document/product/266/38099)をそれぞれご参照ください。
2. FileIdを使用して再生したときに「no v4 play info」エラーが発生した場合は、上記の問題が発生している可能性があるので、上記のチュートリアルに従って調整することをお勧めします。同時に、ソースビデオの再生リンクを直接取得し、[URLによる再生](#url)という方法で再生を実現することもできます。
3. **トランスコーディングを実行していないソースビデオは、再生中に互換性がないという問題が発生する可能性があります。トランスコーディングを実行したビデオを使用して再生することをお勧めします**。

<dx-codeblock>
:::  java
//リンク不正アクセス防止を有効にせずに再生している間に「no v4 play info」エラーが発生した場合は、Adaptive-HLS(10)トランスコーディングテンプレートを使用してビデオをトランスコーディングするか、ソースビデオの再生リンクを直接取得し、urlを介して再生することをお勧めします。

SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329071;// AppIdを設定
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710173650"; // FileIdを設定
//プライベートの暗号化再生にはpsignの入力が必要です。psignはプレーヤーコンポーネントの署名です。署名についての紹介および生成方法については、以下のリンクをご参照ください。https://intl.cloud.tencent.com/document/product/266/38099
//model.videoId.pSign = @"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
[_playerView playWithModelNeedLicence:model];
:::
</dx-codeblock>
:::
::: URLによる再生[](id:url)
```java
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.videoURL = @"http://your_video_url.mp4";   // 再生するビデオのurlを構成します
[_playerView playWithModelNeedLicence:model];
```
:::
</dx-tabs>
3. **再生の終了：**[](id:exitPlayer)
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

<img src="https://qcloudimg.tencent-cloud.cn/raw/e8a774cb9833f2de45fc1cf3cc928ee4.png" style="zoom:35%;" />



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
//カバーのアドレスをネットワークurlアドレスに設定します。coverPictureUrlが設定されていない場合、VODコンソールで設定したカバーが自動的に使用されます。
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
 //手順1：トライアル視聴modelの作成
 TXVipWatchModel *model = [[TXVipWatchModel alloc] init];
 model.tipTtitle = @"15秒トライアル視聴できます。VIPを有効化してビデオの完全版を視聴しましょう";
 model.canWatchTime = 15;
 //手順2：トライアル視聴modelの設定
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

## Demo体験

より完全な機能を体験するには、プロジェクトDemoを直接実行するか、QRコードをスキャンしてモバイルDemoであるTencent Cloud View Cube　Appをダウンロードしてください。

### プロジェクトDemoの実行

1. Demoディレクトリで、コマンドライン`pod update`を実行して、`TXLiteAVDemo.xcworkspace`ファイルを再度生成します。
2. プロジェクトをダブルクリックして開き、証明書を変更して、本番環境での実行を選択します。
3. Demoが正常に実行された後、**プレーヤー** > **プレーヤーコンポーネント**と進むと、プレーヤーの機能を体験できます。

[](id:qrcode)
### Tencent Cloud View Cube App

**Tencent Cloud View Cube App** > **プレーヤー**で、より多くのプレーヤーコンポーネント機能を体験できます。

<img src="https://qcloudimg.tencent-cloud.cn/raw/5c383bc7826d4f4835c9a7232cf9b50e.png" width="150">
