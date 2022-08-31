## 準備作業
1. [VOD](https://intl.cloud.tencent.com/product/vod)関連サービスのアクティブ化を行います。アカウント登録がないユーザーは、アカウントを登録して[トライアル](https://intl.cloud.tencent.com/login)を行うことができます。
2. Xcodeをダウンロードします。ダウンロード済みの場合はこのステップを省略できます。ダウンロードとインストールはApp Storeで行えます。
3. Cocoapodsをダウンロードします。ダウンロード済みの場合はこのステップを省略できます。[Cocoapods公式サイト](https://cocoapods.org/)に進み、ガイドに従ってインストールすることができます。

## ここでは次の内容について知ることができます
* iOSプレーヤーSDKの統合方法
* プレーヤーSDKを使用したVOD再生方法
* プレーヤーSDKの基本機能を使用して、より多くの機能を実装する方法

## SDKの統合
[](id:step1)

### ステップ1：SDK開発キットのダウンロード
<dx-tabs>
::: Cocoapodsによる統合[](id:cocoapods)
PodメソッドによるTXLiteAVSDK_Playerの直接統合：
```objective-c
 pod 'TXLiteAVSDK_Player'
```
特定のバージョンを指定する必要がある場合は、podfileファイルに以下の依存関係を追加することができます。
```objective-c
 pod 'TXLiteAVSDK_Player', '~> 10.3.11513'
```

:::
::: SDKの手動ダウンロード[](id:manual)

1. [最新バージョン](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_iOS_latest.zip)のSDK + Demo開発キットをダウンロードします。
2. SDK/TXLiteAVSDK_Player.frameworkを統合するプロジェクトに追加し、`Do Not Embed`にチェックを入れます。
3. プロジェクトTargetの-ObjCを設定する必要があります。設定しない場合、SDKのクラスがロードされないので、Crashが発生することがあります。
```objective-c
Xcodeを開き、-> 対応するTargetを選択し、-> "Build Setting" Tabを選択し、-> "Other Link Flag"を検索して、-> "-ObjC"を入力します
```
2. 適切なライブラリファイルを追加します（SDKディレクトリ内）
 **TXFFmpeg.xcframework**：.xcframeworkファイルをプロジェクトに追加し、「General - Frameworks, Libraries, and Embedded Content」の「Embed&Sign」に設定します。また、「Project Setting - Build Phases - Embed Frameworks」で検査を行い、オプション「Code Sign On Copy」を下図のようにチェックを入れた状態にします。
 **TXSoundTouch.xcframework**：.xcframeworkファイルをプロジェクトに追加し、「General - Frameworks, Libraries, and Embedded Content」の「Embed&Sign」に設定します。また、「Project Setting - Build Phases - Embed Frameworks」で検査を行い、オプション「Code Sign On Copy」を下図のようにチェックを入れた状態にします。<br>
 <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/b226decc76c33eff8c3f5b4cc4246bea.png" />
<br>
また、Xcodeの「Build Settings - Search Paths」に切り替えて、「Framework Search Paths」に上記Frameworkにあるパスを追加します。

<b>MetalKit.framework</b>：Xcodeを開き、「project setting - Build  Phases - Link Binary With Libraries」に切り替え、左下隅の記号「+」を選択して「MetalKit」と入力し、下図のようにプロジェクトに追加します。<br>
<img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/8ab7576dcc8bbe7b36396955ca06b186.png" />
<br>
<img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/8480798e5ba897077ed3cef8ebc12f2e.png" />
<br>

<b>ReplayKit.framework</b>：Xcodeを開き、「project setting - Build  Phases - Link Binary With Libraries」に切り替え、左下隅の記号「+」を選択して「ReplayKit」と入力し、下図のようにプロジェクトに追加します。<br>
<img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/aa07f3d4963ee703505a14a743f61a68.png" />
<img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/12491d4a64aa6df44e6a966e80ca54de.png" />
<br>

同じ方法で、以下のシステムライブラリも追加します。

<br><b>システムFrameworkライブラリ</b>：SystemConfiguration, CoreTelephony, VideoToolbox, CoreGraphics, AVFoundation, Accelerate, MobileCoreServices<br>
<b>システムLibraryライブラリ:</b> libz, libresolv,  libiconv, libc++, libsqlite3

<h4>ピクチャーインピクチャー機能</h4>

ピクチャーインピクチャー機能を使用する必要がある場合は、下図の方法で設定してください。不要な場合は無視してかまいません。
<br>
1、iOSのピクチャーインピクチャー（Picture-In-Picture）を使用するには、SDKをバージョン10.3以上にアップグレードしてください
<br>
2、ピクチャーインピクチャー機能を使用する場合、バックグラウンドモードを開く必要があります。XCodeは対応するTarget -> Signing & Capabilities -> Background Modesを選択し、図のように「Audio, AirPlay, and Picture in Picture」にチェックを入れます。
<br>
<img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/116e1e741f80d810502221fd143d8434.png" />
<br>
:::
</dx-tabs>




​        

[](id:step2)

### ステップ2：Playerの作成

ビデオクラウドSDKのTXVodPlayerモジュールは、オンデマンド再生機能を実装する役割を果たします。

```objectivec
TXVodPlayer *_txVodPlayer = [[TXVodPlayer alloc] init];
[_txVodPlayer setupVideoWidget:_myView insertIndex:0]
```

[](id:step3)

### ステップ3：レンダリングView

次に、プレーヤー内のビデオ画面を表示する場所を探します。iOSシステムではviewを基本的なインターフェースのレンダリング単位として使用するため、viewを用意してレイアウトを調整するだけで済みます。

```objectivec
[_txVodPlayer setupVideoWidget:_myView insertIndex:0]
```

内部的な原理でいえば、プレーヤーは提供したview（サンプルコードでは\_myView）に直接画面をレンダリングするのではなく、このviewの上にOpenGLレンダリングのためのサブビュー（subView）を作成します。

レンダリング画面のサイズを調整したい場合は、一般的なviewのサイズと位置を調整するだけで、SDKはビデオ画面をviewのサイズと位置に合わせてリアルタイムで調整します。

![](https://qcloudimg.tencent-cloud.cn/raw/235b2e8e6fc3eb328ba05a4c5d251da7.jpg)

**アニメーション化の方法**
 viewのアニメーション化は比較的自由に行えますが、ここでアニメーションによって変更されるターゲット属性は、frameの属性ではなくtransformの属性であることにご注意ください。

```objectivec
[UIView animateWithDuration:0.5 animations:^{
     _myView.transform = CGAffineTransformMakeScale(0.3, 0.3); // 1/3縮小
 }];
```

[](id:step4)

### ステップ4：再生の起動

TXVodPlayerは2種類の再生モードをサポートしており、ニーズに応じて選択することができます。

<dx-tabs>
::: URL方式による方法
  TXVodPlayerは内部で自動的に再生プロトコルを認識しますので、再生URLをstartPlay関数に渡すだけで完了です。
```objectivec
NSString* url = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
[_txVodPlayer startPlay:url];
```
:::
::: fileId方式による方法
```objectivec
TXPlayerAuthParams *p = [TXPlayerAuthParams new];
p.appId = 1252463788;
p.fileId = @"4564972819220421305";
[_txVodPlayer startPlayWithParams:p];
```
[メディア資産管理](https://console.cloud.tencent.com/vod/media)で対応するファイルを検索することができます。クリックしてファイルを開き、右側のビデオ詳細でfileIdを確認することができます。
fileId方式で再生する場合、プレーヤーはバックグラウンドに実際の再生アドレスをリクエストします。この時点でネットワークの異常やfileIdが存在しない場合、`PLAY_ERR_GET_PLAYINFO_FAIL`イベントを受信します。逆に、`PLAY_EVT_GET_PLAYINFO_SUCC`を受信した場合、リクエストが成功したことを意味します。
:::
</dx-tabs>

### ステップ5：再生終了

再生終了時に現在のUIを終了する場合は、必ず**removeVideoWidget**を使用してviewコントロールを破棄してください。この操作をしない場合、メモリリークや画面のちらつきといった問題が発生します。

```objectivec
// 再生の停止
[_txVodPlayer stopPlay];
[_txVodPlayer removeVideoWidget]; // viewコントロールの破棄を忘れずに
```

## 基本機能の使用
### 1、再生の制御

#### 再生開始

```objective-c
// 再生開始
[_txVodPlayer startPlay:url];
```

#### 再生一時停止

```objective-c
// 再生一時停止
[_txVodPlayer pause];
```

#### 再生再開

```objective-c
// 再生再開
[_txVodPlayer resume];
```

#### 再生終了

```objective-c
// 再生終了
[_txVodPlayer stopPlay];
```

#### 進捗の調整（Seek）

ユーザーがプログレスバーをドラッグすると、seekを呼び出して指定した位置から再生を開始することができます。プレーヤーSDKは正確なseekをサポートします。

```objective-c
int time = 600; // intタイプのとき、単位は秒
// 進捗の調整
[_txVodPlayer seek:time];
```

#### 指定した時間からの再生

startPlayを最初に呼び出す前に、指定した時間からの再生がサポートされています。

```objective-c
float startTimeInMS = 600; // 単位：ミリ秒
[_txVodPlayer setStartTime:startTimeInMS];  // 再生開始時間の設定
[_txVodPlayer startPlay:url];
```


### 2、画面調整
- **view：サイズと位置**
画面のサイズや位置を変えるには、setupVideoWidgetのパラメータviewのサイズと位置を直接調整すれば、SDKはビデオ画面をviewのサイズと位置に追従させ、リアルタイムで調整します。
- **setRenderMode：全体に表示または適応**
<table>
<tr><th>オプション値</th><th>意味</th></tr>
<tr>
<td>RENDER_MODE_FILL_SCREEN</td>
<td>画像をアスペクト比を維持したまま画面全体に表示し、余分な部分をトリミングします。このモードでは画面に黒枠が残りませんが、一部の領域がトリミングされるため、完全に表示されない場合があります。</td>
</tr><tr>
<td>RENDER_MODE_FILL_EDGE</td>
<td>画像は、アスペクト比を維持したまま、最も長い辺に合わせてスケーリングされます。スケーリングされた幅と高さは表示領域を超えることなく中央に表示され、画面に黒枠が残る場合があります。</td>
</tr></table>
- **setRenderRotation：画面の回転**
<table>
<tr><th>オプション値</th><th>意味</th></tr>
<tr>
<td>HOME_ORIENTATION_RIGHT</td>
<td>homeは右側</td>
</tr><tr>
<td>HOME_ORIENTATION_DOWN</td>
<td>homeは下</td>
</tr><tr>
<td>HOME_ORIENTATION_LEFT</td>
<td>homeは左側</td>
</tr><tr>
<td>HOME_ORIENTATION_UP</td>
<td>homeは上</td>
</tr></table>




### 3、可変速再生
VODプレーヤーは可変速再生をサポートしており、インターフェース`setRate`を通じてオンデマンド再生レートを設定することにより、0.5X、1.0X、1.2X、2Xなどの高速再生と低速再生をサポートしています。


 ```objectivec
// 1.2倍速再生に設定
[_txVodPlayer setRate:1.2]; 
// ...
// 再生開始
[_txVodPlayer startPlay:url];
 ```

### 4、ループ再生

```objective-c
// ループ再生の設定
[_txVodPlayer setLoop:true];
// 現在のループ再生ステータスの取得
[_txVodPlayer loop];
```

### 5、ミュート設定

```objective-c
// ミュートの設定です。trueはミュートオン、falseはミュートオフを表します
[_txVodPlayer setMute:true];
```

### 6、スクリーンキャプチャ

**snapshot**を呼び出すと、現在のビデオを1つのフレームとしてキャプチャできます。この機能は、現在のCSSストリームのビデオ画面のみをキャプチャします。現在のUI全体をキャプチャする必要がある場合は、iOSシステムAPIを呼び出して実行してください。


### 7、ロール画像広告
プレーヤーSDKは、広告宣伝用として、インターフェースへのロール画像の追加をサポートしています。実装方法は以下のとおりです。
* `autoPlay`をNOにすると、この時点でプレーヤーは正常にロードされますが、ビデオはすぐに再生を開始しません。
* プレーヤーがロードされてからビデオが始まる前に、プレーヤーのインターフェースでロール画像広告を確認することができます。
* 広告の表示終了条件に達したら、resumeインターフェースでビデオ再生を開始します。

### 8,HTTP-REF
TXVodPlayConfigのheadersは、URLがコピーされるのを防ぐためによく使われるRefererフィールド（Tencent Cloudは、よりセキュアな署名のリンク不正アクセス防止方式を提供できます）や、クライアントのID情報を検証するためのCookieフィールドなど、HTTPリクエストヘッダーの設定に使用することができます。
### 9、ハードウェアアクセラレーション
Blu-rayレベル(1080p)の画質の場合、ソフトウェアデコードだけではスムーズな再生は困難です。そのため、ゲームのライブストリーミングがメインのシナリオでは、一般的にハードウェアアクセラレーションをオンにすることをお勧めします。

ソフトウェアデコードとハードウェアデコードを切り替えるには、切り替える前に**stopPlay**、切り替えた後に**startPlay**を行う必要があります。この操作をしない場合、より深刻な画面の揺れや歪みといった問題が発生します。

```objectivec
[_txVodPlayer stopPlay];
_txVodPlayer.enableHWAcceleration = YES;
[_txVodPlayer startPlay:_flvUrl type:_type];
```

### 10、解像度の設定
SDKは、hlsのマルチビットレート形式をサポートしており、ユーザーが異なるビットレートの再生ストリームを切り替えるときに便利です。PLAY_EVT_PLAY_BEGINイベントを受信した後、以下の方法でマルチビットレートアレイを取得することができます
```objectivec
NSArray *bitrates = [_txVodPlayer supportedBitrates]; //マルチビットレートアレイの取得
```

再生中は、`-[TXVodPlayer setBitrateIndex:]`を通じていつでもビットレートを切り替えることができます。切り替え中、別のストリームのデータを再度プルするため、若干のタイムラグが発生します。SDKは、Tencent Cloudのマルチビットレートファイルに最適化されているため、ラグが発生することなく切り替えが可能です。
### 11、ビットレートストリーミングアダプティブ
SDKは、HLSのマルチビットレートアダプティブをサポートしています。関連機能をオンにすると、プレーヤーが現在の帯域幅に基づいて再生に最適なビットレートを動的に選択することが可能です。`PLAY_EVT_PLAY_BEGIN`イベントを受信した後、以下の方法でビットレートストリーミングアダプティブをオンにすることができます。
```objectivec
[_txVodPlayer setBitrateIndex:-1]; //indexパラメータは-1で渡されます
```
再生中はいつでも`-[TXVodPlayer setBitrateIndex:]`で別のビットレートに切り替えることができ、切り替えた後はビットレートストリーミングアダプティブはオフになります。

### 12、再生進捗のリスニング

VOD再生中の進捗情報には、**ロード進捗**と**再生進捗**という2種類があります。現在、SDKはこれら2つの進捗をイベント通知という形でリアルタイムに通知しています。イベント通知の詳細については、[イベントリスニング](#listening)をご参照ください。


```objective-c
-(void) onPlayEvent:(TXVodPlayer *)player event:(int)EvtID withParam:(NSDictionary*)param {
    if (EvtID == PLAY_EVT_PLAY_PROGRESS) {
            // ロードの進行状況です。単位は秒、小数点以下はミリ秒です
            float playable = [param[EVT_PLAYABLE_DURATION] floatValue];
                [_loadProgressBar setValue:playable];
                
            // 再生の進行状況です。単位は秒、小数点以下はミリ秒です
            float progress = [param[EVT_PLAY_PROGRESS] floatValue];
                [_seekProgressBar setValue:progress];
                
            // ビデオの総尺です。単位は秒、小数点以下はミリ秒です
            float duration = [param[EVT_PLAY_DURATION] floatValue];
            // 表示時間の設定などに使用できます
    }
}
```


### 13、再生インターネット速度のリスニング

[イベントリスニング](#listening)を使用すると、ビデオの再生時にラグが発生した際、その時点のネットワーク速度を表示することができます。

* `onNetStatus`の`NET_SPEED`で現在のネットワーク速度を取得します。具体的な使用方法については、[ステータスフィードバック（onNetStatus）](#status)をご参照ください。
* `PLAY_EVT_PLAY_LOADING`イベントをリスニングした後に、現在のネットワーク速度を表示します。
* `PLAY_EVT_VOD_LOADING_END`イベントを受信した後、現在のネットワーク速度を表示するviewを非表示にします。

### 14、ビデオ解像度の取得

プレーヤーSDKはURL文字列を介してビデオを再生します。URLそのものにはビデオ情報は含まれません。関連情報を取得するには、クラウドサーバーにアクセスしてビデオ情報をロードする必要があるため、SDKはビデオ情報をイベント通知としてのみお客様のアプリケーションに送信します。詳細については、[イベントリスニング](#listening)をご参照ください。

**解像度情報**
<dx-tabs>
::: 方法1
`onNetStatus`の`VIDEO_WIDTH`と`VIDEO_HEIGHT`により、ビデオの幅と高さを取得します。具体的な使用方法については、[ステータスフィードバック（onNetStatus）](#status)をご参照ください。
:::
::: 方法2
`-[TXVodPlayer width]`と`-[TXVodPlayer height]`を直接呼び出すと、現在の幅と高さを取得できます。
:::
</dx-tabs>

### 15、再生バッファサイズ

通常のビデオ再生時に、事前にネットワークからバッファするデータの最大サイズを制御します。設定されていない場合は、プレーヤーのデフォルトのバッファポリシーに従って、スムーズな再生が確保されます。

```java
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setMaxBufferSize:10];  // 再生時の最大バッファサイズです。単位：MB
[_txVodPlayer setConfig:_config];  // configを_txVodPlayerに渡します
```

### 16、ビデオローカルキャッシュ[](id:cache)
UGSVのビデオ再生シナリオでは、ビデオファイルのローカルキャッシュは非常に重要な機能です。一般ユーザーにとっては、一度視聴したビデオを再度視聴する際にトラフィックを消費しないことが望ましいからです。

- **サポートされている形式：**SDKは、HLS(m3u8)とMP4という2種類の一般的なオンデマンド形式のキャッシュ機能をサポートしています。
- **オンのタイミング：**SDKは、デフォルトではキャッシュ機能がオンになりませんので、ユーザーの再生率が高くないシナリオでは、この機能をオンにすることはお勧めしません。
- **オンにする方法：**この機能をオンにするには、ローカルキャッシュディレクトリとキャッシュサイズという2つのパラメータを設定する必要があります
```objectivec
//再生エンジンのグローバルキャッシュディレクトリの設定
NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
NSString *documentsDirectory = [paths objectAtIndex:0];
NSString *preloadDataPath = [documentsDirectory stringByAppendingPathComponent:@"/preload"];
if (![[NSFileManager defaultManager] fileExistsAtPath:preloadDataPath]) {
     [[NSFileManager defaultManager] createDirectoryAtPath:preloadDataPath
                               withIntermediateDirectories:NO
                                                attributes:nil
                                                     error:&error];
[TXPlayerGlobalSetting setCacheFolderPath:preloadDataPath];
//再生エンジンのキャッシュサイズの設定
[TXPlayerGlobalSetting setMaxCacheSize:200];
// ...
// 再生開始
[_txVodPlayer startPlay:playUrl];                            
```

>? TXVodPlayConfig#setMaxCacheItemsインターフェースで設定された旧バージョンは廃止されているため、非推奨です。

## 高度な機能の使用

### 1、ビデオのプリ再生

#### ステップ1：ビデオのプリ再生・使用

UGSV再生シナリオでは、プリロード機能がスムーズな視聴に大変役立ちます。現在のビデオを視聴中に、次に再生するビデオのURLをバックグラウンドでロードし、ユーザーが実際に次のビデオに切り替えたときに、最初からロードする必要がなく、すぐに再生することができます。

ビデオのプリ再生は、秒単位で開けるという効果を発揮しますが、ある程度のパフォーマンスオーバーヘッドがあります。業務にたくさんのビデオプリロードのニーズがある場合、[ビデオのプリダウンロード](#download)と併用することをお勧めします。

これは、ビデオ再生中のシームレスな切り替えを後押しする技術で、TXVodPlayerのisAutoPlayスイッチを使って、この機能を実装することができます。具体的な方法は以下のとおりです。
<img src="https://qcloudimg.tencent-cloud.cn/raw/b2bd645f29af403bf2740156aee44092.jpg" width=850px>

```objectivec
// ビデオAの再生：isAutoPlayがYESに設定されている場合、startPlayの呼び出しにより、直ちにビデオのロードと再生が開始されます
NSString* url_A = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f10.mp4";
_player_A.isAutoPlay = YES;
[_player_A startPlay:url_A];

// ビデオAを再生すると同時に、ビデオBをプリロードします。これは、isAutoPlayをNOに設定すると行われます
NSString* url_B = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
_player_B.isAutoPlay = NO;
[_player_B startPlay:url_B];
```

ビデオAの再生が終了し、自動的に（またはユーザーが手動で）ビデオBに切り替えたとき、resume関数を呼び出し、すぐに再生できるようにします。

>! autoPlayをfalseに設定した後、resumeを呼び出す前にビデオBの準備ができていることを確認する必要があります。すなわち、ビデオBのPLAY_EVT_VOD_PLAY_PREPARED（2013、プレーヤーは再生可能状態）イベントをリスニングした後に呼び出す必要があります。

```objectivec
-(void) onPlayEvent:(TXVodPlayer *)player event:(int)EvtID withParam:(NSDictionary*)param
{
    // ビデオAの再生が終了すると、そのままビデオBの再生が始まるので、シームレスな切り替えが可能です
    if (EvtID == PLAY_EVT_PLAY_END) {
            [_player_A stopPlay];
            [_player_B setupVideoWidget:mVideoContainer insertIndex:0];
            [_player_B resume];
        }
}
```

#### ステップ2：ビデオのプリ再生・バッファの設定

- バッファを大きめに設定すると、ネットワークの変動に対応しやすくなり、スムーズな再生という目的を達成できます。

- バッファを小さめに設定すると、トラフィックの消費を抑えることができます。 

##### プリ再生バッファサイズ

このインターフェースは、プリロードシナリオ（ビデオ再生が開始され、playerのAutoPlayがfalseに設定される前）向けで、最大バッファサイズを制御するために使用されます。

```objective-c
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setMaxPreloadSize:(2)];;  // プリ再生の最大バッファサイズです。単位はMBで、業務の状況に応じてトラフィックを節約するように設定します
[_txVodPlayer setConfig:_config];  // configを_txVodPlayerに渡します
```

##### 再生バッファサイズ 

通常のビデオ再生時に、事前にネットワークからバッファするデータの最大サイズを制御します。設定されていない場合は、プレーヤーのデフォルトのバッファポリシーに従って、スムーズな再生が確保されます。

```objective-c
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setMaxBufferSize:10];  // 再生時の最大バッファサイズです。単位：MB
[_txVodPlayer setConfig:_config];  // configを_txVodPlayerに渡します
```

### 2、ビデオのプリダウンロード[](id:download)
プレーヤーインスタンスを作成する必要がなく、ビデオコンテンツの一部があらかじめダウンロードされています。そのためプレーヤーを使用すると、ビデオの再生速度がアップし、より良い再生エクスペリエンスを提供することができます。

再生サービスを利用する前に、[ビデオキャッシュ](#cache)が設定されていることを確認してください。
>?
>- TXPlayerGlobalSettingはグローバルキャッシュ設定インターフェースです。以前のTXVodConfigのキャッシュ設定インターフェースは廃止されています。
>- グローバルキャッシュのディレクトリとサイズの設定は、プレーヤーのTXVodConfigで構成されるキャッシュ設定よりも優先されます。

ユースケース：

```objective-c
//再生エンジンのグローバルキャッシュディレクトリの設定
NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
NSString *documentsDirectory = [paths objectAtIndex:0];
NSString *preloadDataPath = [documentsDirectory stringByAppendingPathComponent:@"/preload"];
if (![[NSFileManager defaultManager] fileExistsAtPath:preloadDataPath]) {
     [[NSFileManager defaultManager] createDirectoryAtPath:preloadDataPath 
      												 withIntermediateDirectories:NO 
      																					attributes:nil 
      																							 error:&error]; //Create folder
}
[TXPlayerGlobalSetting setCacheFolderPath:preloadDataPath];

//再生エンジンのキャッシュサイズの設定
[TXPlayerGlobalSetting setMaxCacheSize:200];
NSString *m3u8url = "http://****";
int taskID = [[TXVodPreloadManager sharedManager] startPreload:m3u8url 
 																									 preloadSize:10 
 																					 preferredResolution:1920*1080 
 																											delegate:self];


//プリダウンロードのキャンセル
[[TXVodPreloadManager sharedManager] stopPreload:taskID];
```

### 3、ビデオのダウンロード
ビデオをダウンロードすると、ユーザーがインターネットに接続している状態でビデオをダウンロードした場合、インターネットに接続していない状態でもビデオを視聴することができます。また同時に、プレーヤーSDKはローカル暗号化機能を提供しており、ダウンロードしたローカルビデオは暗号化された状態のまま、指定されたプレーヤーでのみ復号し再生することができるので、ダウンロードしたビデオの違法配信を効果的に防止し、ビデオのセキュリティを保護することができます。

HLSストリームメディアはローカルに直接保存できないため、ローカルファイルを再生することによるHLSのオフライン再生ができません。この問題については、`TXVodDownloadManager`ベースのビデオダウンロード方式によって、HLSをオフラインで再生することが可能です。

> ! 
> - `TXVodDownloadManager`は展示店では、MP4とFLV形式のファイルのキャッシュをサポートしておらず、HLS形式ファイルのみサポートしています。
>- プレーヤーSDKは、MP4およびFLV形式のローカルファイルの再生をサポートしています。
[](id:offline1)
#### ステップ1：準備作業

`TXVodDownloadManager`は単一のインスタンスとして設計されているので、複数のダウンロードオブジェクトを作成することはできません。使い方は以下のとおりです。

```objective-c
TXVodDownloadManager *downloader = [TXVodDownloadManager shareInstance];
[downloader setDownloadPath:"<ダウンロード先のディレクトリを指定してください>"];
```

[](id:offline2)
#### ステップ2：ダウンロードの開始
ダウンロードを開始するには、URLとfileidという2つの方法があります。
<dx-tabs>
::: URL方式
ダウンロードアドレスを渡すだけで完了です。
```objective-c
[downloader startDownloadUrl:@"http://1253131631.vod2.myqcloud.com/26f327f9vodgzp1253131631/f4bdff799031868222924043041/playlist.m3u8"]
```
:::
::: fileid方式
fileidによるダウンロードでは、少なくともappIdとfileIdを渡す必要があります。
```objective-c
TXPlayerAuthParams *auth = [TXPlayerAuthParams new];
auth.appId = 1252463788;
auth.fileId = @"4564972819220421305";
TXVodDownloadDataSource *dataSource = [TXVodDownloadDataSource new];
dataSource.auth = auth;
[downloader startDownload:dataSource];
```
:::
</dx-tabs>


[](id:offline3)
#### ステップ3：タスク情報 

タスク情報を受信する前に、コールバックdelegateを設定する必要があります。

```objective-c
downloader.delegate = self;
```

受信する可能性のあるタスクコールバックは、以下のとおりです。
<table><thead>
<tr><th width="55%">コールバック情報</th><th>意味</th></tr>
</thead>
<tbody><tr>
<td>-[TXVodDownloadDelegate onDownloadStart:]</td>
<td>タスクの開始、SDKがダウンロードを開始したことを示します</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadProgress:]</td>
<td>タスクの進捗です。SDKはダウンロード中にこのインターフェースを頻繁にコールバックするので、ここで進捗の表示を更新することができます</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadStop:]</td>
<td>タスクの停止です。<code>stopDownload</code>を呼び出してダウンロードを停止すると、停止が成功したことを示すこのメッセージが表示されます</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadFinish:]</td>
<td>ダウンロードの完了です。このコールバックを受信すると、すべてのダウンロードが完了したことを意味します。この時点で、ダウンロードしたファイルはTXVodPlayerで再生することができます</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadError:errorMsg:]</td>
<td>ダウンロードエラーです。ダウンロード中にネットワークが切断されると、このインターフェースがコールバックされると同時にダウンロードタスクが停止されます。すべてのエラーコードについては、<code>TXDownloadError</code></td>をご参照ください
</tr>
</tbody></table>

downloaderは複数のタスクを同時にダウンロードできるので、コールバックインターフェースには`TXVodDownloadMediaInfo`オブジェクトが含まれます。お客様は、URLやdataSourceにアクセスしてダウンロード元を特定したり、ダウンロードの進捗やファイルサイズなどの情報を取得したりできます。

[](id:offline4)
#### ステップ4：ダウンロードの中断

ダウンロードを停止するには、`-[TXVodDownloadManager stopDownload:]`メソッドを呼び出してください。パラメータは、`-[TXVodDownloadManager sartDownloadUrl:]`によって返されるオブジェクトです。**SDKは、中断からの再開をサポート**しています。ダウンロードディレクトリが変更されていない場合、同じファイルの次のダウンロードは最後に停止したところから再び開始されます。

再ダウンロードが不要な場合は、`-[TXVodDownloadManager deleteDownloadFile:]`メソッドを呼び出してファイルを削除し、ストレージ容量を解放してください。

### 4、暗号化再生

ビデオ暗号化方式は、主にオンライン教育など、ビデオの著作権保護が必要なシナリオで使用されています。ビデオソースを暗号化する場合、プレーヤーを変更するだけでなく、ビデオソース自体を暗号化・トランスコードする必要があり、バックエンドとエンドポイントという両方の開発エンジニアが関わる必要が出てきます。詳細については、[ビデオ暗号化ソリューション](https://intl.cloud.tencent.com/document/product/266/38131)をご参照ください。

### 5、プレーヤーの設定 

statPlayを呼び出す前に、setConfigによってプレーヤーのパラメータを設定することができます。例としては、プレーヤーの接続タイムアウト時間の設定、プログレスコールバック間隔の設定、キャッシュファイル数の設定などです。TXVodPlayConfigがサポートするパラメータの詳細については、[基本設定インターフェース](https://intl.cloud.tencent.com/document/product/266/47844)をクリックしてご参照ください。使用例は、以下のとおりです。

```java
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setEnableAccurateSeek:true];  // 正確にseekするかどうかを設定します。デフォルトはtrueです
[_config setMaxCacheItems:5];  // キャッシュファイル数を5に設定します
[_config setProgressInterval:200];  // プログレスコールバック間隔を設定します。単位はミリ秒です
[_config setMaxBufferSize:50];  // 最大プリロードサイズ、単位はMBです
[_txVodPlayer setConfig:_config];  // configを_txVodPlayerに渡します
```

##### 再生開始時の解像度の指定

 HLSのマルチビットレートのビデオソースを再生する場合、ビデオストリームの解像度情報があらかじめわかっていれば、再生開始前にビデオ解像度を優先的に指定して再生することができます。プレーヤーは、再生開始時に希望する解像度以下のストリームを探すため、再生開始後にsetBitrateIndexによって希望するビットレートストリーミングに切り替える必要はありません。

```java
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
// 入力パラメータは、ビデオの幅と高さの積（幅×高さ）で、カスタム値として渡すことができます
[_config setPreferredResolution:720*1280];
[_txVodPlayer setConfig:_config];  // configを_txVodPlayerに渡します
```

##### 再生進捗コールバック時間間隔の設定

```objective-c
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setProgressInterval:200];  // プログレスコールバック間隔を設定します。単位はミリ秒です
[_txVodPlayer setConfig:_config];  // configを_txVodPlayerに渡します
```

[](id:listening)

## プレーヤーイベントのリスニング
TXVodPlayListenerリスナーをTXVodPlayerオブジェクトにバインドすると、onPlayEvent（イベント通知）とonNetStatus（ステータスフィードバック）を介して、アプリケーションに情報を同期させることができます。

### イベント通知（onPlayEvent）

#### 再生イベント
| イベントID               |   数値  |  意味の説明                 |
| :-------------------  |:-------- |  :------------------------ |
|PLAY_EVT_PLAY_BEGIN    |  2004|  ビデオ再生の開始 |
|PLAY_EVT_PLAY_PROGRESS |  2005|  ビデオ再生の進行状況です。現在の再生の進行状況、ロードの進行状況および全体の長さを通知します     |
|PLAY_EVT_PLAY_LOADING  |  2007|  ビデオ再生をloading中です。再開できれば、その後にLOADING_ENDイベントが発生します|
|PLAY_EVT_VOD_LOADING_END   |  2014|  ビデオ再生loadingを終了します。ビデオは引き続き再生されます|
| VOD_PLAY_EVT_SEEK_COMPLETE | 2019 | Seekの完了です。バージョン10.3からサポートしています|

#### イベント終了
| イベントID               |   数値  |  意味の説明                |
| :-------------------  |:-------- |  :------------------------ |
|PLAY_EVT_PLAY_END      |  2006|  ビデオ再生を終了します   |
|PLAY_ERR_NET_DISCONNECT |  -2301  |  ネットワーク接続が切断され、かつ複数回再接続しても再開できません。これ以上のリトライを行うには、ご自身で再生を再起動してください |
|PLAY_ERR_HLS_KEY       | -2305 | HLS復号keyの取得に失敗しました |

#### 警告イベント
以下のイベントは、SDK内のイベントをお知らせするためにのみ使用されるため、無視してかまいません。

| イベントID                 |    数値  |  意味の説明                    |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | 現在のビデオフレームのデコードに失敗しました  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | 現在のオーディオフレームのデコードに失敗しました  |
| PLAY_WARNING_RECONNECT           |  2103  | ネットワーク接続が切断されましたが、自動再接続が開始されました（再接続が3回を超えると、PLAY_ERR_NET_DISCONNECTが直接スローされます）|
| PLAY_WARNING_HW_ACCELERATION_FAIL|  2106  | ハードウェアデコードの開始に失敗しました。ソフトウェアデコードを使用してください   |


#### 接続イベント
この他、サーバーへの接続に関するイベントもいくつかあります。主にサーバー接続時間の測定や統計を行うために使用されます。

| イベントID                     |    数値  |  意味の説明                    |
| :-----------------------  |:-------- |  :------------------------ |
| PLAY_EVT_VOD_PLAY_PREPARED     |  2013    | プレーヤーは再生可能状態です。autoPlayがfalseに設定されている場合、再生を開始するにはこのイベントを受信した後にresumeを呼び出す必要があります
| PLAY_EVT_RCV_FIRST_I_FRAME|  2003    | ネットワークが最初のレンダリング可能なビデオデータパッケージ（IDR）を受信しました  |

#### 画面イベント
以下のイベントは、画面変更情報の取得に使用されます。

| イベントID                     |    数値  |  意味の説明                    |
| :-----------------------  |:-------- |  :------------------------ |
| PLAY_EVT_CHANGE_RESOLUTION|  2009    | ビデオ解像度の変更               |
| PLAY_EVT_CHANGE_ROATION   |  2011    | MP4ビデオの回転角度 |


#### ビデオ情報イベント
| イベントID                     |    数値  |  意味の説明                    |
| :-----------------------  |:-------- |  :------------------------ |
|PLAY_EVT_GET_PLAYINFO_SUCC   | 2010 | 再生ファイル情報の取得に成功しました |

fileId方式によって再生し、リクエストが成功した場合、SDKはいくつかの情報を上位レイヤーに通知します。PLAY_EVT_GET_PLAYINFO_SUCCイベントを受信後、paramを解析することでビデオ情報を取得できます。

|   ビデオ情報                   |  意味の説明                   |
| :------------------------  |  :------------------------ |
| EVT_PLAY_COVER_URL     | ビデオカバーアドレス |
| EVT_PLAY_URL  | ビデオ再生アドレス |
| EVT_PLAY_DURATION | ビデオ時間 |

```objective-c
-(void) onPlayEvent:(TXVodPlayer *)player event:(int)EvtID withParam:(NSDictionary*)param
{
    if (EvtID == PLAY_EVT_VOD_PLAY_PREPARED) {
        //プレーヤーが準備が完了したイベントを受信すると、この時点でpause、resume、getWidth、getSupportedBitratesなどのインターフェースを呼び出すことができます
    } else if (EvtID == PLAY_EVT_PLAY_BEGIN) {
        // 再生開始イベントの受信
    } else if (EvtID == PLAY_EVT_PLAY_END) {
        // 開始終了イベントの受信
    }
}
```

[](id:status)

### ステータスフィードバック（onNetStatus）
ステータスフィードバックは、0.5秒ごとに1回トリガーされますが、プッシャーの現在のステータスをリアルタイムにフィードバックすることが目的です。車のダッシュボードのように、SDK内の状況の一部を具体的に教えてくれるので、現在のビデオ再生状況などを把握することができます。
<table>
<thead><tr><th>評価パラメータ</th><th>意味の説明</th></tr><tr>
<td>CPU_USAGE</td><td>現在の瞬間的なCPU使用率</td>
</tr><tr>
<td>VIDEO_WIDTH</td><td>ビデオ解像度 - 幅</td>
</tr><tr>
<td>VIDEO_WIDTH</td><td>ビデオ解像度 - 高さ</td>
</tr><tr>
<td>NET_SPEED</td><td>現在のネットワークデータ受信速度</td>
</tr><tr>
<td>VIDEO_FPS</td><td>現在のストリームメディアのビデオフレームレート</td>
</tr><tr>
<td>VIDEO_BITRATE</td><td>現在のストリームメディアのビデオビットレートです。単位はkbps</td>
</tr><tr>
<td>AUDIO_BITRATE</td><td>現在のストリームメディアのオーディオビットレートです。単位はkbps</td>
</tr><tr>
<td>V_SUM_CACHE_SIZE</td><td>バッファ(jitterbuffer)サイズです。現在のバッファの長さは0で、ラグから遠くないことを意味しています</td>
</tr><tr>
<td>SERVER_IP</td><td>接続先サーバーIP</td>
</tr></table>
onNetStatusによるビデオ再生プロセスにおける取得情報の例：
```objective-c
- (void)onNetStatus:(TXVodPlayer *)player withParam:(NSDictionary *)param {
    //現在のCPU使用率の取得
    float cpuUsage = [[param objectForKey:@"CPU_USAGE"] floatValue];
    //ビデオ幅の取得
    int videoWidth = [[param objectForKey:@"VIDEO_WIDTH"] intValue];
    //ビデオ高さの取得
    int videoHeight = [[param objectForKey:@"VIDEO_HEIGHT"] intValue];
    //リアルタイムレートの取得
    int  speed = [[param objectForKey:@"NET_SPEED"] intValue];
    //現在のストリームメディアのビデオフレームレートの取得
    int fps = [[param objectForKey:@"VIDEO_FPS"] intValue];
    //現在のストリームメディアのビデオビットレートを取得します。単位はkbps
    int videoBitRate = [[param objectForKey:@"VIDEO_BITRATE"] intValue];
    //現在のストリームメディアのオーディオビットレートを取得します。単位はkbps
    int audioBitRate = [[param objectForKey:@"AUDIO_BITRATE"] intValue];
    //バッファ(jitterbuffer)サイズを取得します。現在のバッファの長さは0で、ラグから遠くないことを意味しています
    int jitterbuffer = [[param objectForKey:@"V_SUM_CACHE_SIZE"] intValue];
    //接続されているサーバーのIPアドレスの取得
    NSString *ip = [param objectForKey:@"SERVER_IP"];
}
```

## シナリオ化機能

### 1、SDKベースのDemoコンポーネント

Tencent Cloudは、プレーヤーSDKをベースとして以下のような[プレーヤーコンポーネント](https://intl.cloud.tencent.com/document/product/266/33976)を開発しました。品質モニタリング、ビデオ暗号化、超高速HD(TESHD)、解像度切り替え、ミニウィンドウ再生などの機能を一体化し、あらゆるオンデマンド(VOD)、ライブストリーミング再生のシナリオに対応します。完備された機能をパッケージ化するとともに、上位層のUIを提供することで、市場で人気を博す各種ビデオアプリに引けを取らない再生ソフトウェアを短時間で作成することができます。

### 2、オープンソースGithub

Tencent Cloudは、プレーヤーSDKをベースとして、没入型ビデオプレーヤーコンポーネント、ビデオFeedストリーム、マルチプレーヤー再利用コンポーネントなどを開発しました。今後はバージョンアップを重ねながら、ユーザーシナリオに基づいたコンポーネントをご提供していく予定です。[Player_iOS](https://github.com/LiteAVSDK/Player_iOS)からダウンロードし、体験することができます。
