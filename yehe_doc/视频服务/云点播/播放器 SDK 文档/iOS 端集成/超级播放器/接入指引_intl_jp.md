## 製品概要

Tencent Cloud View Cube iOS Super Playerは、Tencent Cloudによるオープンソースのプレーヤーコンポーネントです。簡単な数行のコードで、Tencent Videoのような強力な再生機能を備えることができます。画面の縦横切り替え、解像度の選択、ジェスチャー、ミニウィンドウなどの基本機能を備えるほか、ビデオキャッシュ、ソフトウェア/ハードウェアデコードの切り替え、倍速再生などの特殊機能もサポートしています。システムのプレーヤーと比べて、サポートする形式がより多く、互換性により優れ、機能もより強力です。同時に、トップ画面のインスタントブロードキャスティング、低遅延などの優位性、ならびにビデオサムネイルなどの高度な機能も備えています。


## 準備作業
1. [VOD](https://intl.cloud.tencent.com/product/vod)関連サービスを有効化します。未登録のユーザーはアカウントを登録し、[無料試用](https://intl.cloud.tencent.com/login)できます。
2. Xcodeをダウンロードします。すでにダウンロードしている場合は、この手順をスキップして、App Storeに移動し、ダウンロードとインストールを実行できます。
3. Cocoapodsをダウンロードします。すでにダウンロードしている場合は、この手順をスキップして、[Cocoapods公式サイト](https://cocoapods.org/)に移動し、ガイドに従ってインストールできます。

## このドキュメントから把握できること
- [Tencent Cloud View Cube iOS Super Playerの統合方法](#step1)
- [プレイヤーの作成・使用方法](#step3)

## 統合の準備
[](id:step1)
### 手順1：プロジェクトのダウンロード
Tencent Cloud View Cube iOS Super Playerのプロジェクトアドレスは、[SuperPlayer_iOS](https://github.com/LiteAVSDK/Player_iOS)です。

Tencent Cloud View Cube iOS Super Playerプロジェクトは、**[プレーヤーコンポーネントZIPパッケージのダウンロード](#zip)**または**[Gitコマンドのダウンロード](#git)**によりダウンロードできます。
<dx-tabs>
::: プレーヤーコンポーネントZIPパッケージのダウンロード[](id:zip)
画面の**Code** > **Download ZIP**をクリックして、プレーヤーコンポーネントZIPパッケージを直接ダウンロードすることができます。
![](https://qcloudimg.tencent-cloud.cn/raw/a38a9995bfe13d645bcd1d2e5242a297.png)
:::
::: Gitコマンドのダウンロード[](id:git)
1. まず、Gitがコンピュータにインストールされていることを確認します。インストールされていない場合は、[Gitのインストールチュートリアル](https://git-scm.com/downloads)を参照し、インストールしてください。
2. 以下のコマンドを実行し、Super Playerコンポーネントのプロジェクトコードをローカルにcloneします。
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
```xml
pod 'SuperPlayer'
```
2. `pod install`または`pod update`を実行します。
:::
::: SDKの手動ダウンロード[](id:manual)
1. SDK+Demo開発パッケージをダウンロードします。Tencent Cloud View Cube iOS Super Playerのプロジェクトアドレスは[SuperPlayer_iOS](https://github.com/LiteAVSDK/Player_iOS)です。
2. `TXLiteAVSDK_Player.framework`をプロジェクトにインポートし、`Do Not Embed`にチェックを入れます。
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
この手順は、ユーザーがビデオを再生できるようにガイドするのに使用されます。Tencent Cloud View Cube iOS Super Playerは、[VOD FileId](#fileid)または[URLの使用](#url)による再生をサポートしています。より完全な機能を利用するには、**FileIdの統合**を選択することをお勧めします。
<dx-tabs>
::: VOD FileIdによる再生[](id:fileid)
ビデオFileIdは、通常、ビデオのアップロード後にサーバーから返されます。

1. クライアントからビデオがリリースされると、サーバーがFileIdをクライアントに返します。
2. サーバーからのビデオアップロード時、アップロード確認の通知に対応するFileIdが含まれています。
ファイルがすでにTencent Cloudに存在する場合は、[メディア資産管理](https://console.cloud.tencent.com/vod/media)にアクセスし、該当するファイルをさがして、FileIdを確認できます。下図のように、IDのところにFileIdが表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/f089346e01ab8e44e42f28c965809b9c.png)
>!
>- FileIdを使用して再生する場合は、先にAdaptive-HLS(10)トランスコーディングテンプレートでビデオをトランスコーディングするか、Super Playerの署名psignで再生するビデオを指定する必要があります。そうしないと、ビデオの再生に失敗する可能性があります。トランスコーディングのチュートリアルと手順の詳細については、[Super Playerによるビデオ再生](https://intl.cloud.tencent.com/document/product/266/38098)をご参照ください。psignの生成チュートリアルの詳細ついては、[psignチュートリアル](https://intl.cloud.tencent.com/document/product/266/38099)をご参照ください。
>- FileIdを使用して再生したときに「no v4 play info」エラーが発生した場合は、上記の問題が発生している可能性があるので、上記のチュートリアルに従って調整することをお勧めします。同時に、ソースビデオの再生リンクを直接取得し、[URLによる再生](#url)という方法で再生を実現することもできます。
>- **トランスコーディングを実行していないソースビデオは、再生中に互換性がないという問題が発生する可能性があります。トランスコーディングを実行したビデオを使用して再生することをお勧めします。**

<dx-codeblock>
:::  java
//リンク不正アクセス防止を有効にせずに再生している間に「no v4 play info」エラーが発生した場合は、Adaptive-HLS(10)トランスコーディングテンプレートを使用してビデオをトランスコーディングするか、ソースビデオの再生リンクを直接取得し、urlを介して再生することをお勧めします。

SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329071;// AppIdを設定
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710173650"; // FileIdを設定
//プライベートの暗号化済みビデオを再生するには、psignの記入が必要となり、psignはSuper Playerの署名です。署名についての紹介および生成方法は、このリンク（https://intl.cloud.tencent.com/document/product/266/38099）をご参照ください。
//model.videoId.pSign = @"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
[_playerView playWithModel:model];
:::
</dx-codeblock>
:::
::: URLによる再生[](id:url)
```java
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.videoURL = @"http://your_video_url.mp4";   // 再生するビデオのurlを構成します
[_playerView playWithModel:model];
```
:::
</dx-tabs>
- **再生の終了：**[](id:exitPlayer)
プレーヤーが不要な時には、`resetPlayer`を呼び出してプレーヤー内部の状態を消去し、メモリをリリースします。
```java
[_playerView resetPlayer];
```

Tencent Cloud View Cube iOS Super Playerの作成、ビデオの再生、および再生の終了などの機能統合が完了しました。

[](id:moreFeature)
## 機能の使用[](id:moreFeature)

### 1. 全画面再生

Super Playerは全画面再生をサポートするほか、全画面再生シナリオでの画面ロック、音量と明るさのジェスチャー制御、弾幕、スクリーンショット、および解像度の切り替えなどの機能の設定を可能にします。機能の効果は、[**Tencent Cloud View Cube App**](#qrcode)>**Player**>**Super Player**で体験できます。インターフェースの右下隅にある**全画面表示**をクリックすると、全画面再生インターフェースを表示できます。



ウィンドウ再生モードでは、次のインターフェースを呼び出すことで全画面再生モードに入ることができます。

```objective-c
- (void)superPlayerFullScreenChanged:(SuperPlayerView *)player {
  //ここで、ユーザーは全画面表示に切り替えた後のロジックをカスタマイズできます
}
```


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
Super Playerは、再生中に各時点でのビデオフレームをキャプチャする機能を提供し、ユーザーは画像を保存して共有することができます。スクリーンショットボタンをクリックすると、SDK内部によって処理され、スクリーンショットの成功または失敗のコールバックはありません。キャプチャされた画像のディレクトリは携帯電話のアルバムです。
:::
::: 解像度の切り替え[](id:resolution)
ユーザーは、HD、SD、UHDなど、ニーズに応じて異なるビデオ再生の解像度を選択できます。クリック後にトリガーされる解像度viewの表示と解像度オプションのクリック操作は、コールバックなしでSDK内部によってに処理されます。
:::
</dx-tabs>


### 2. フローティングウィンドウによる再生

Super Playerは、フローティングウィンドウでのピクチャーインピクチャー再生をサポートします。これにより、他のアプリケーションに切り替えるときにビデオ再生機能を中断する必要がなくなります。機能の効果は、[**Tencent Cloud View Cube App**](#qrcode)>**Player**>**Super Player**で体験できます。インターフェースの左上隅にある**戻る**をクリックすると、フローティングウィンドウでの再生機能を体験できます。



```objective-c
// 画面が縦向きになっており、再生中である場合、戻るボタンをクリックすると、インターフェースがトリガーされます
[SuperPlayerWindowShared setSuperPlayer:self.playerView];
[SuperPlayerWindowShared show];
// フローティングウィンドウをクリックして、ウィンドウによってトリガーされたコードインターフェースが返されます
SuperPlayerWindowShared.backController = self;
```

### 3. ビデオカバー

Super Playerは、ユーザーによってカスタマイズされたビデオカバーをサポートし、ビデオカバーはビデオが最初のフレーム画面の再生コールバックを受信する前に表示するために使用されます。機能の効果は、[**Tencent Cloud View Cube App**](#qrcode)>**Player**>**Super Player**>**カスタムカバーのデモ**で体験できます。



*　Super Playerが自動再生モード`PLAY_ACTION_AUTO_PLAY`に設定されている場合、ビデオは自動的に再生され、このときにビデオの最初のフレームが読み込まれる前にカバーが表示されます。
* Super Playerが手動再生モード`PLAY_ACTION_MANUAL_PLAY`に設定されている場合、ユーザーが**再生**をクリックした後にのみビデオの再生が開始されます。カバーは、**再生**をクリックする前に表示され、**再生**をクリックしてからビデオの最初のフレームが読み込まれる前にも表示されます。

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
[self.playerView playWithModel:model] 
```

### 4. ビデオリストによるカルーセル

Super Playerは、ビデオリストによるカルーセルをサポートします。つまり、ビデオリストを指定すると、以下のことができます。

* リスト内のビデオを順番に繰り返し再生することをサポートし、再生プロセス中に次のビデオを自動的に再生すること、および次のビデオに手動で切り替えることをサポートします。
* リストにある最後のビデオの再生が終了すると、リスト内にある最初のビデオは自動的に再生されます。

機能の効果は、[**Tencent Cloud View Cube App**](#qrcode)>**Player**>**Super Player**>**ビデオリストによるカルーセルのデモ**で体験できます。



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
[self.playerView playWithModelList:modelArray isLoopPlayList:YES startIndex:0];
```

```objective-c
(void)playWithModelList:(NSArray *)playModelList isLoopPlayList:(BOOL)isLoop startIndex:(NSInteger)index;
```

インターフェースパラメータの説明

| パラメータ名         | タイプ   | 説明                                   |
| ------------- | --------- | --------- |
| playModelList | NSArray * | データリストのカルーセル    |
| isLoop        | Boolean   | 繰り返すかどうか      |
| index         | NSInteger | 再生を開始したビデオのインデックス |

### 5. ビデオのトライアル視聴

Super Playerは、ビデオのトライアル視聴機能をサポートし、VIPではないユーザーによるトライアル視聴などのシナリオに適用できます。開発者は、さまざまなパラメータを渡して、ビデオのトライアル視聴時間、ヒント情報、およびトライアル視聴終了インターフェースを制御できます。機能の効果は、[**Tencent Cloud View Cube App**](#qrcode)>**Player**>**Super Player**>**トライアル視聴のデモ**で体験できます。



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

### 6. ダイナミックウォーターマーク

Super Playerは、再生インターフェースに不規則に実行されるテキストウォーターマークを追加することをサポートし、無断録画を効果的に防止します。ウォーターマークは、全画面再生モードとウィンドウ再生モードの両方で表示でき、開発者はウォーターマークのテキスト、テキストサイズと色を変更できます。ウォーターマーク効果は、[**Tencent Cloud View Cube App**](#qrcode)>**Player**>**Super Player**>**ダイナミックウォーターマークのデモ**で体験できます。



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
[self.playerView playWithModel:playermodel];
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
3. Demoを正常に実行した後、**Player**>**Super Player**に移動して、プレーヤーの機能を体験できます。

[](id:qrcode)

### Tencent Cloud View Cube App

**Tencent Cloud View Cube App**>**Player**で、さらに多くのSuper Player機能を体験できます。

<img src="https://main.qcloudimg.com/raw/12c7da97cc910eda673cb19b66fc7cb3.png" width="150">
