## 製品概要

Tencent Cloud View Cube iOSプレーヤーコンポーネントは、Tencent Cloudによるオープンソースのプレーヤーコンポーネントです。簡単な数行のコードで、Tencent Videoのような強力な再生機能を備えることができます。画面の縦横切り替え、解像度の選択、ジェスチャー、ミニウィンドウなどの基本機能を備えるほか、ビデオキャッシュ、ソフトウェア/ハードウェアデコードの切り替え、倍速再生などの特殊機能もサポートしています。システムのプレーヤーよりも、サポートする形式が多く、互換性に優れ、機能もより強力です。同時に、トップ画面の秒速起動、低遅延などの優位性、ならびにビデオサムネイルなどの高度な機能も備えています。

プレーヤーコンポーネントでは業務上の個別のニーズを満たせない場合、お客様にある程度の開発経験がおありの場合は Player+を統合し、プレーヤーインターフェースおよび再生機能のカスタム開発を行うことも可能です。

## 準備作業
1. [VOD](https://intl.cloud.tencent.com/product/vod)関連サービスのアクティブ化を行います。アカウント登録がないユーザーは、アカウントを登録して[トライアル](https://intl.cloud.tencent.com/login)を行うことができます。
2. Xcodeをダウンロードします。ダウンロード済みの場合はこのステップを省略できます。ダウンロードとインストールはApp Storeで行えます。
3. Cocoapodsをダウンロードします。ダウンロード済みの場合はこのステップを省略できます。[Cocoapods公式サイト](https://cocoapods.org/)に進み、ガイドに従ってインストールすることができます。

## ここでは次の内容について知ることができます
- [Tencent Cloud View Cube iOSプレーヤーコンポーネントの統合方法](#step1)
- [プレーヤーの作成および使用方法](#step3)

## 統合の準備
[](id:step1)
### ステップ1：プロジェクトのダウンロード
Tencent Cloud View Cube iOSプレーヤーのプロジェクトアドレスは、[LiteAVSDK/Player_iOS](https://github.com/LiteAVSDK/Player_iOS)です。

Tencent Cloud View Cube iOSプレーヤーコンポーネントプロジェクトのダウンロードは、 **[プレーヤーコンポーネントZIPパッケージのダウンロード](#zip)**、または**[Gitコマンドでのダウンロード](#git)**のいずれかの方法で行えます。
<dx-tabs>
::: プレーヤーコンポーネントZIPパッケージのダウンロード[](id:zip)
次のプレーヤーコンポーネントZIPパッケージを直接ダウンロードできます。ページの**Code** > **Download ZIP**をクリックしてダウンロードしてください
![](https://qcloudimg.tencent-cloud.cn/raw/a38a9995bfe13d645bcd1d2e5242a297.png)
:::
::: Gitコマンドでのダウンロード[](id:git)
1. 初めに、コンピュータにGitがインストールされていることをご確認ください。インストールされていない場合は、[Gitインストールチュートリアル](https://git-scm.com/downloads)を参照してインストールすることができます。
2. 次のコマンドを実行し、プレーヤーコンポーネントのプロジェクトコードをローカルにcloneします。
```shell
git clone git@github.com:tencentyun/SuperPlayer_iOS.git
```
   次のメッセージが表示されると、プロジェクトコードのローカルへのcloneは成功です。
```shell
'SuperPlayer_iOS'にクローンしています...
remote: Enumerating objects: 2637, done.
remote: Counting objects: 100% (644/644), done.
remote: Compressing objects: 100% (333/333), done.
remote: Total 2637 (delta 227), reused 524 (delta 170), pack-reused 1993
オブジェクト受信のうち、100% (2637/2637), 571.20 MiB | 3.94 MiB/s, が完了しました
delta処理中: 100% (1019/1019), が完了しました
```
プロジェクトのダウンロード後、プロジェクトソースコードの解凍後のディレクトリは次のようになります。
<table>
<thead><tr><th>ファイル名</th><th>役割</th></tr></thead>
<tbody>
<tr><td>SDK</td>
<td>プレーヤーを保存するframework静的ライブラリ</td>
</tr><tr>
<td>Demo</td><td>Super Player Demoを保存</td>
</tr><tr>
<td>App</td><td>プログラムポータルインターフェース</td>
</tr><tr>
<td>SuperPlayerDemo</td><td>Super Player Demo</td>
</tr><tr><td>SuperPlayerKit</td><td>Super Playerコンポーネント</td>
</tr></tbody></table>
:::
</dx-tabs>

[](id:step2)
### ステップ2：ガイドの統合
このステップは、プレーヤーの統合方法についてユーザーにご説明するためのものです。**[Cocoapodsによる統合](#cocoapods)**または**[SDKの手動ダウンロード](#manual)**のどちらかを使用してから、現在のプロジェクトにインポートすることをお勧めします。
<dx-tabs>
::: Cocoapodsによる統合[](id:cocoapods)
1. 本プロジェクトはCocoapodsのインストールをサポートしています。次のコードをPodfileに追加するだけです。
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
具体的な手順は以下をご参照ください。カスタム開発 - VODシナリオ - アクセスドキュメント - SDK統合 ステップ1 - 手動でSDKを統合する
さらにTXLiteAVSDK_Playerファイル下のTXFFmpeg.xcframeworkと TXSoundTouch.scframeworkを動的ライブラリの方式で次の図に示すように追加してください。
![](https://qcloudimg.tencent-cloud.cn/raw/5834caae21d3413522c7d51d4b3b57b0.png)
 2. Podを使用した方式でTXLiteAVSDK_Playerを統合する場合は、ライブラリを追加する必要はありません。


:::
</dx-tabs>

[](id:step3)
### ステップ3：プレーヤー機能の使用
このステップは、プレーヤーの作成および使用、ならびにプレーヤーを使用してビデオ再生を行う方法についてユーザーにご説明するためのものです。

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
::: VOD FileIdからの再生[](id:fileid)
ビデオFileIdは、通常、ビデオのアップロード後にサーバーから返されます。

1. クライアントからビデオが公開されると、サーバーがFileIdをクライアントに返します。
2. サーバーからのビデオアップロード時、アップロードの確認の通知の中に対応するFileIdが含まれています。
ファイルがすでにTencent Cloudに存在する場合は、[メディア資産管理](https://console.cloud.tencent.com/vod/media)にアクセスし、該当するファイルをさがして、FileIdを確認できます。下図のように、IDのところにFileIdが表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/f089346e01ab8e44e42f28c965809b9c.png)
<dx-alert infotype="notice">
<li>FileId経由で再生する場合は、初めにAdaptive-HLS(10)トランスコードテンプレートを使用してビデオのトランスコードを行うか、またはプレーヤーコンポーネントの署名psignを使用して再生するビデオを指定する必要があります。これらを行わないと、ビデオ再生が失敗する可能性があります。トランスコードのチュートリアルおよび説明については [プレーヤーコンポーネントを使用したビデオ再生](https://intl.cloud.tencent.com/document/product/266/38098)を、psign生成のチュートリアルについては[psignチュートリアル](https://intl.cloud.tencent.com/document/product/266/38099)をそれぞれご参照ください。</li>
<li>FileId経由での再生の際に「no v4 play info」エラーが表示された場合は、上記の問題が存在する可能性があることを示しているため、上記のチュートリアルに従って調整することをお勧めします。また、ソースビデオの再生リンクを直接取得し、[URLによる再生](#url) 方式で再生することもできます。</li>
<li>**トランスコードを行っていないソースビデオを再生すると、互換性がない場合がありますので、トランスコードをご使用後にビデオを再生することをお勧めします。**</li></dx-alert>

<dx-codeblock>
:::  java
//リンク不正アクセス防止を有効にせずに再生を行い、その途中で「no v4 play info」エラーが表示された場合は、Adaptive-HLS(10)トランスコードテンプレートを使用してビデオのトランスコードを行うか、またはソースビデオの再生リンクを直接取得し、url方式で再生することをお勧めします。

SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329071;// AppIdを設定
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710173650"; // FileIdを設定
//プライベートの暗号化再生にはpsignの入力が必要です。psignはプレーヤーコンポーネントの署名です。署名についての紹介および生成方法については、以下のリンクをご参照ください。https://intl.cloud.tencent.com/document/product/266/38099
//model.videoId.pSign = @"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
[_playerView playWithModel:model];
:::
</dx-codeblock>
:::
::: URLを使用した再生[](id:url)
```java
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.videoURL = @"http://your_video_url.mp4";   // ビデオ再生urlを設定
[_playerView playWithModel:model];
```
:::
</dx-tabs>
- **再生の終了：**[](id:exitPlayer)
プレーヤーが不要な時には、`resetPlayer`を呼び出してプレーヤー内部の状態を消去し、メモリを解放します。
```java
[_playerView resetPlayer];
```

これで、Tencent Cloud View Cube iOSプレーヤーコンポーネントの作成、ビデオ再生、再生終了機能の統合が完了しました。

[](id:moreFeature)
## 機能の使用[](id:moreFeature)

### 1、全画面再生

プレーヤーコンポーネントは全画面再生をサポートしています。全画面再生のシーンでは、同時に画面ロック、ジェスチャーによる音量と明るさの制御、弾幕、スクリーンショット、解像度の切り替えなどの機能設定がサポートされます。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント**で体験できます。画面右下隅の**全画面**をクリックすると、全画面再生画面に進むことができます。



ウィンドウ再生モードでは、次のインターフェースを呼び出して全画面再生モードに進むことができます。

```objective-c
- (void)superPlayerFullScreenChanged:(SuperPlayerView *)player {
  //ユーザーはここで全画面切り替え後のロジックをカスタマイズできます
}
```

#### 


<dx-tabs>
::: ウィンドウモードに戻る[](id:window)
**戻る**によってウィンドウ再生モードに戻ることができます。クリック後にSDKが全画面切り替えのロジックを処理した後、トリガーするプロキシメソッドは次のとおりです。

```objective-c
// イベントを返す
- (void)superPlayerBackAction:(SuperPlayerView *)player;
左上隅の戻るボタンをクリックするとトリガーします
// 全画面変更通知
- (void)superPlayerFullScreenChanged:(SuperPlayerView *)player;
```
:::
::: 画面ロック[](id:screenlock)
画面ロック操作はユーザーが再生に集中したい場合に使用できます。クリックするとSDKが自動的に処理し、コールバックは行いません。

```objective-c
// ユーザーは次のインターフェースによって画面ロックの制御を行うことができます
@property(nonatomic, assign) BOOL isLockScreen;
```
:::
::: 弾幕[](id:barrage)
弾幕機能をオンにすると、画面上にユーザーの送信した文字を流すことができます。

ここでSPDefaultControlViewオブジェクトを取得し、プレーヤーviewの初期化の際にSPDefaultControlViewの弾幕ボタンにイベントを設定します。弾幕の内容および弾幕viewはユーザーご自身でカスタマイズする必要があります。詳細については、SuperPlayerDemoのCFDanmakuView、CFDanmakuInfo、CFDanmakuをご参照ください。

```objective-c
SPDefaultControlView *dv = (SPDefaultControlView *)**self**.playerView.controlView;
[dv.danmakuBtn addTarget:**self** action:**@selector**(danmakuShow:) forControlEvents:UIControlEventTouchUpInside];
```

CFDanmakuView：弾幕のプロパティの初期化時の設定。

```objective-c
// 次のプロパティはすべて設定必須です--------
// 弾幕アニメーション時間
@property(nonatomic, assign) CGFloat duration;
// 中央上部/下部弾幕アニメーション時間
@property(nonatomic, assign) CGFloat centerDuration;
// 弾幕の軌道の高さ
@property(nonatomic, assign) CGFloat lineHeight;
// 弾幕の軌道間の距離
@property(nonatomic, assign) CGFloat lineMargin;

// 弾幕の軌道の最大行数
@property(nonatomic, assign) NSInteger maxShowLineCount;

// 弾幕の軌道の中央上部/下部の最大行数
@property(nonatomic, assign) NSInteger maxCenterLineCount;
```
:::
::: スクリーンショット[](id:screenshot)
プレーヤーコンポーネントは再生中にその時点のビデオフレームを切り取ることができる機能をご提供します。画像を保存して共有することができます。スクリーンショットボタンをクリックすると、SDKの内部で処理が行われ、スクリーンショットが成功したかどうかのコールバックは行われません。スクリーンショットした画像のディレクトリはスマートフォンのアルバムとなります。
:::
::: 解像度の切り替え[](id:resolution)
ユーザーはニーズに応じて、HD、SD、FHDなどのビデオ再生の解像度を選択することができます。クリック後にトリガーされる解像度表示viewおよび解像度オプションのクリックはいずれもSDKの内部で処理され、コールバックは行われません。
:::
</dx-tabs>


### 2、フローティングウィンドウ再生

プレーヤーコンポーネントはフローティングウィンドウによるミニウィンドウ再生をサポートしています。アプリケーション内の他のページに切り替えてもビデオ再生が中断しない機能です。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント**で体験できます。画面左上隅の**戻る**をクリックすると、フローティングウィンドウ再生機能を体験できます。



```objective-c
// 縦画面かつ現在再生中の場合は、戻るボタンをクリックするとインターフェースがトリガーされます
[SuperPlayerWindowShared setSuperPlayer:self.playerView];
[SuperPlayerWindowShared show];
// フローティングウィンドウの戻るウィンドウをクリックするとトリガーされるコードインターフェース
SuperPlayerWindowShared.backController = self;
```

### 3、ビデオカバー

プレーヤーコンポーネントはユーザーによるビデオカバーのカスタマイズをサポートしています。これはユーザーがビデオの最初のフレーム画面の再生コールバックを受信する前の表示に用いられます。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **カバーカスタマイズのデモンストレーション**ビデオで体験できます。

* プレーヤーコンポーネントを自動再生モード`PLAY_ACTION_AUTO_PLAY`に設定すると、ビデオが自動再生されます。このとき、ビデオの最初のフレームをロードするまでの間はカバーが表示されます。
* プレーヤーコンポーネントを手動再生モード`PLAY_ACTION_MANUAL_PLAY`に設定すると、ユーザーが**再生**をクリックしなければ再生が開始されません。**再生**をクリックするまでの間はカバーが表示されます。**再生**をクリックした後、ビデオの最初のフレームをロードするまでの間もカバーが表示されます。

ビデオカバーはネットワークURLアドレスまたはローカルFileアドレスの使用をサポートしています。使用方法については下記のガイドをご参照ください。FileID方式でビデオを再生する場合は、VOD内で直接ビデオカバーを設定することができます。

```objective-c
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
SuperPlayerVideoId *videoId = [SuperPlayerVideoId new];
videoId.fileId = @"8602268011437356984"; 
model.appId = 1400329071;
model.videoId = videoId;
//再生モードは、自動再生モード`PLAY_ACTION_AUTO_PLAY`または手動再生モード`PLAY_ACTION_MANUAL_PLAY`に設定することができます。
model.action  = PLAY_ACTION_MANUAL_PLAY; 
//カバーのアドレスをネットワークのurlアドレスに設定する場合、coverPictureUrlを設定しなければ、VODコンソールが設定したカバーが自動的に使用されます
model.customCoverImageUrl = @"http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/cc1e28208602268011087336518/MXUW1a5I9TsA.png"; 
[self.playerView playWithModel:model] 
```

### 4、ビデオリストの繰り返し再生

プレーヤーコンポーネントはビデオリストの繰り返し再生をサポートしています。ビデオリストを指定すると、次のようになります。

* 再生リスト内のビデオを順序に従って繰り返し再生できます。再生中は次のビデオの自動再生と、次のビデオへの手動切り替えのどちらも行うことができます。
* リスト内の最後のビデオの再生が完了すると、リスト内の最初のビデオの再生を自動的に開始します。

機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **ビデオリストの繰り返し再生のデモンストレーション**ビデオで体験できます。



```objective-c
//ステップ1:繰り返し再生データのNSMutableArrayを作成
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

//ステップ2：SuperPlayerViewの繰り返し再生インターフェースを呼び出し
[self.playerView playWithModelList:modelArray isLoopPlayList:YES startIndex:0];
```

```objective-c
(void)playWithModelList:(NSArray *)playModelList isLoopPlayList:(BOOL)isLoop startIndex:(NSInteger)index;
```

インターフェースパラメータの説明

| パラメータ名           | タイプ        | 説明        |
| ------------- | --------- | --------- |
| playModelList | NSArray * | 繰り返し再生データリスト    |
| isLoop        | Boolean   | 繰り返すかどうか      |
| index         | NSInteger | 再生を開始するビデオのインデックス |


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
 model.tipTtitle = @「15秒のプレビューが可能、VIPをアクティブ化すると完全なビデオを視聴可能」。
 model.canWatchTime = 15;
 //ステップ2：プレビューmodelの設定
 self.playerView.vipWatchModel = model;
 //ステップ3：メソッドを呼び出してプレビュー機能を表示
 [self.playerView showVipTipView];
```

  TXVipWatchModelクラスのパラメータ説明：

| パラメータ名          | タイプ       | 説明        |
| ------------ | -------- | --------- |
| tipTtitle    | NSString | プレビュープロンプト情報    |
| canWatchTime | float    | プレビュー時間。単位は秒 |

### 7、動的ウォーターマーク

プレーヤーコンポーネントは再生画面での、不規則に動くテキストウォーターマークの追加をサポートし、不正録画を効果的に防止します。ウォーターマークは全画面再生モードおよびウィンドウ再生モードのどちらでも表示でき、開発者はウォーターマークのテキスト、文字サイズ、色を変更することができます。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **動的ウォーターマークのデモンストレーション**ビデオで体験できます。



```objective-c
//ステップ1：ビデオソース情報modelの作成
SuperPlayerModel *  playermodel   = [SuperPlayerModel new];
//ビデオソースのその他の情報を追加
//ステップ2：動的ウォーターマークmodelの作成
DynamicWaterModel *model = [[DynamicWaterModel alloc] init];
//ステップ3：動的ウォーターマークデータの設定
model.dynamicWatermarkTip = @"shipinyun";
model.textFont = 30;
model.textColor = [UIColor colorWithRed:255.0/255.0 green:255.0/255.0 blue:255.0/255.0 alpha:0.8];
playermodel.dynamicWaterModel = model;
//ステップ4：メソッドを呼び出して動的ウォーターマークを表示
[self.playerView playWithModel:playermodel];
```

DynamicWaterModelクラスのパラメータ説明：

| パラメータ名                 | タイプ       | 説明     |
| ------------------- | -------- | ------ |
| dynamicWatermarkTip | NSString | ウォーターマークのテキスト情報 |
| textFont            | CGFloat  | 文字サイズ   |
| textColor           | UIColor  | 文字の色   |

## Demo体験

さらに完全な機能は、プロジェクトのDemoを直接実行するか、または2次元コードをスキャンしてモバイル端末Demoをダウンロードし、Tencent Cloud View Cube Appで体験することができます。

### プロジェクトDemoの実行

1. Demoディレクトリでコマンドライン`pod update`を実行し、`TXLiteAVDemo.xcworkspace`ファイルを再作成します。
2. プロジェクトをダブルクリックし、証明書を変更して実機での実行を選択します。
3. Demoが正常に実行された後、**プレーヤー** > **プレーヤーコンポーネント**と進むと、プレーヤーの機能を体験できます。

[](id:qrcode)
### Tencent Cloud View Cube App

**Tencent Cloud View Cube App** > **プレーヤー**で、より多くのプレーヤーコンポーネント機能を体験できます。

<img src="https://qcloudimg.tencent-cloud.cn/raw/5c383bc7826d4f4835c9a7232cf9b50e.png" width="150">
