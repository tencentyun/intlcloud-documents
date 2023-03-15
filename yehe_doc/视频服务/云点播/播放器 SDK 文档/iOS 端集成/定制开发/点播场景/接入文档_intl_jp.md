## 準備作業
1. [VOD](https://intl.cloud.tencent.com/product/vod)関連サービスを有効化します。未登録のユーザーはアカウントを登録し、[無料試用](https://intl.cloud.tencent.com/login)できます。
2. Xcodeをダウンロードします。すでにダウンロードしている場合は、この手順をスキップして、App Storeに移動し、ダウンロードとインストールを実行できます。
3. Cocoapodsをダウンロードします。すでにダウンロードしている場合は、この手順をスキップして、[Cocoapods公式サイト](https://cocoapods.org/)に移動し、ガイドに従ってインストールできます。

## このドキュメントから把握できること
* iOSプレーヤーSDKを統合する方法
* プレーヤーSDKを使ったオンデマンド再生の方法
* プレーヤーSDKの基盤となる機能を使用したり多くの機能の実現方法

## SDKの統合
[](id:step1)

### ステップ1：SDK開発パッケージをダウンロード
<dx-tabs>
::: Cocoapods統合[](id:cocoapods)
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

### ステップ2：SDKへのアクセス環境の設定

お客様がより高品質かつ安全でコンプライアンスに則ったビジネスを展開し、各国・地域の規制の要求事項を満たすよう、Tencent Cloudは2つのSDKアクセス環境を提供します。グローバルユーザにサービスを提供している場合、以下のインターフェースでグローバルアクセス環境を設定することをお勧めします。

```objective-c
// グローバルユーザにサービスを提供している場合、SDKアクセス環境にグローバルアクセス環境を設定してください
[TXLiveBase setGlobalEnv:"GDPR"]
```

[](id:step3)

### ステップ3：License権限承認の設定

すでに関連するLicense権限承認を取得している場合は、[Tencent Cloud View Cubeコンソール](https://console.cloud.tencent.com/vcube)にて、License URLおよびLicense Keyを取得する必要があります。
License権限承認を取得していない場合は、先に[ビデオ再生License](https://cloud.tencent.com/document/product/881/74588) をご参照の上、関連する権限承認を取得してください。

License情報を取得後、SDKの関連インターフェースを呼び出す前に、次のインターフェースでLicenseを初期化します。`- [AppDelegate application:didFinishLaunchingWithOptions:]` に以下の設定を行うことをお勧めします。

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<取得したlicenseUrl>";
    NSString * const licenceKey = @"<取得したkey>";

    //TXLiveBaseは"TXLiveBase.h"ヘッダーファイルの中にあります
    [TXLiveBase setLicenceURL:licenceURL key:licenceKey]; 
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}
```

[](id:step4)

### ステップ4：Playerの作成

ビデオクラウドSDKのTXVodPlayerモジュールは、オンデマンド再生機能の実装を行います。

```objectivec
TXVodPlayer *_txVodPlayer = [[TXVodPlayer alloc] init];
[_txVodPlayer setupVideoWidget:_myView insertIndex:0]
```

[](id:step5)

### ステップ5：レンダリングView

次はプレーヤーのビデオ画面を表示する場所を探します。iOSでは基本的なインターフェースのレンダリング単位としてviewが使われていますので、viewを用意してレイアウトを調整するだけで済みます。

```objectivec
[_txVodPlayer setupVideoWidget:_myView insertIndex:0]
```

内部原理的には、プレーヤーは提供されたview（サンプルコードの\_myView）に画面を直接レンダリングするのではなく、このviewの上にOpenGLレンダリング用のサブビュー(subView)を作成します。

レンダリングされた画面のサイズを変更する場合は、一般的なviewのサイズと位置を変更するだけでいい。SDKでは、ビデオ画面がviewのサイズと位置に合わせてリアルタイムで調整されます。

![](https://qcloudimg.tencent-cloud.cn/raw/235b2e8e6fc3eb328ba05a4c5d251da7.jpg)

**アニメーションの作り方**
 viewをアニメートするのは自由ですが、ここのアニメーションで変更するターゲット属性はframe属性ではなくtransform属性であることに注意してください。

```objectivec
[UIView animateWithDuration:0.5 animations:^{
     _myView.transform = CGAffineTransformMakeScale(0.3, 0.3); // 1/3のサイズに缩小
 }];
```

[](id:step6)

### ステップ6：再生を開始

TXVodPlayerは2つの再生モードをサポートしており、必要に応じて選択できます。

<dx-tabs>
::: URL方式
  TXVodPlayerは内部で再生プロトコルを自動的に認識するので、再生URLをstartPlay関数に渡すだけでよいです。
```objectivec
NSString* url = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
[_txVodPlayer startPlay:url];
```
:::
::: fileId方式
```objectivec
TXPlayerAuthParams *p = [TXPlayerAuthParams new];
p.appId = 1252463788;
p.fileId = @"4564972819220421305";
[_txVodPlayer startPlayWithParams:p];
```
[メディア資産管理](https://console.cloud.tencent.com/vod/media)で対応するファイルを見つけます。クリックして、右側のビデオ詳細でfileIdを確認することができます。
fileId方式で再生すると、プレーヤーはリアルな再生アドレスをバックグラウンドにリクエストします。この時点でfileIdが存在しない場合は、`PLAY_ERR_GET_PLAYINFO_FAIL`イベントが受信され、そうでない場合は、リクエストが成功したことを示す`PLAY_EVT_GET_PLAYINFO_SUCC`が受信されます。
:::
</dx-tabs>

### ステップ7：再生の終了

再生の終了時に現在のUIを終了する場合は、**removeVideoWidget**を使用してviewコントロールを破棄してください。破棄しないと、メモリリークやスプラッシュスクリーンの問題が発生します。

```objectivec
// 再生の停止
[_txVodPlayer stopPlay];
[_txVodPlayer removeVideoWidget]; // viewコントロールを破棄することを忘れないでください
```

## 基本機能の使用
### 1、再生コントロール

#### 再生の開始

```objective-c
// 再生の開始
[_txVodPlayer startPlay:url];
```

#### 再生の一時停止

```objective-c
// 再生の一時停止
[_txVodPlayer pause];
```

#### 再生の再開

```objective-c
// 再生の再開
[_txVodPlayer resume];
```

#### 再生の終了

```objective-c
// 再生の終了
[_txVodPlayer stopPlay];
```

#### 再生位置の調整(Seek)

ユーザーが再生バーをドラッグすると、seekを呼び出して指定された位置から再生を開始することができ、プレーヤーSDKは正確なseekをサポートします。

```objective-c
int time = 600; // int型の場合、単位を秒とします
/// 再生位置の調整
[_txVodPlayer seek:time];
```

#### 指定された時間から再生します

startPlayが初回呼び出されるまでは、指定された時間からの再生がサポートされています。

```objective-c
float startTimeInSecond = 60; // 単位：秒
[_txVodPlayer setStartTime:startTimeInSecond];  // 再生開始時間の設定
[_txVodPlayer startPlay:url];
```


### 2、画面調整
- **view：サイズと位置**
画面のサイズと位置を変更する場合は、setupVideoWidgetのパラメータviewのサイズと位置を直接変更すると、SDKはビデオ画面を自分のviewのサイズと位置に合わせてリアルタイムで調整することができます。
- **setRenderMode：並べて表示または画像のサイズに合わせる**
<table>
<tr><th>選択可能な値</th><th>意味</th></tr>
<tr>
<td>RENDER_MODE_FILL_SCREEN</td>
<td>画像を拡大や縮小せず、画面のいっぱいに広げられ、はみ出した部分が切れます。このモードでは画面に黒い隙間はありませんが、画像の一部が切れて表示されない場合があります。</td>
</tr><tr>
<td>RENDER_MODE_FILL_EDGE</td>
<td>画像の最も長い辺に合わせて縦横の比率を保って拡大・縮小します。拡大・縮小後の幅と高さが表示領域を超えず、中央に表示されます。また画面に黒い隙間が残る場合があります。</td>
</tr></table>
- **setRenderRotation：画面回転**
<table>
<tr><th>選択可能な値</th><th>意味</th></tr>
<tr>
<td>HOME_ORIENTATION_RIGHT</td>
<td>homeは右にあります</td>
</tr><tr>
<td>HOME_ORIENTATION_DOWN</td>
<td>homeは下にあります</td>
</tr><tr>
<td>HOME_ORIENTATION_LEFT</td>
<td>homeは左にあります</td>
</tr><tr>
<td>HOME_ORIENTATION_UP</td>
<td>homeは上にあります</td>
</tr></table>




### 3、速度を変えて再生します
VODプレーヤーは可変速再生をサポートしています。インターフェース`setRate`を使用してオンデマンド再生速度を設定します。0.5X、1.0X、1.2X、2Xなどの高速再生と低速再生をサポートしています。


 ```objectivec
// 1.2倍の再生速度を設定します
[_txVodPlayer setRate:1.2]; 
// ...
// 再生の開始
[_txVodPlayer startPlay:url];
 ```

### 4、ループ再生

```objective-c
// ループ再生の設定
[_txVodPlayer setLoop:true];
// 現在のループ再生状態を取得します
[_txVodPlayer loop];
```

### 5、ミュート設定

```objective-c
// ミュートを設定します。ミュートをオンにする場合はtrue、ミュートをオフにする場合はfalse
[_txVodPlayer setMute:true];
```

### 6、スクリーンショット

**snapshot**を呼び出すことにより、現在のビデオから1つのフレーム画像をキャプチャすることができます。この機能は、現在のライブストリームのビデオ画面のみをキャプチャします。現在のインターフェース全体をキャプチャする必要がある場合は、iOSのシステムAPIを呼び出してください。


### 7、ピクチャ挿入広告
プレーヤーSDKは、広告宣伝などのためにインターフェースにピクチャを挿入することをサポートします。実現方式は次のとおりです。
* `autoPlay'をNOにすると、プレーヤーは正常にロードされますが、ビデオはすぐに再生を開始しません。
* ビデオはプレーヤーでロードされた後、再生が開始されていない間は、プレーヤーのインターフェースで画像広告が表示されます。
* 広告表示終了条件が満たされたら、resumeインターフェースを使用してビデオ再生を開始します。

### 8、HTTP-REF
TXVodPlayConfigのheadersは、URLがあちこちにコピーされないようにするよく使われているRefererフィールド（Tencent Cloudは、より安全な署名の盗難防止用チェーンスキームを提供します）や、クライアントのID情報を検証するためのCookieフィールドなど、HTTPリクエストヘッダを設定するために使用されます。
### 9、ハードウェア・アクセラレーション
ブルーレイ（1080p）レベルの画質については、単にソフトウェアデコードを使用してスムーズな再生体験を得るのが難しいので、ゲームのライブ配信を中心としたシーンでは、ハードウェア・アクセラレーションをオンにすることをお勧めします。

ソフトウェアデコードとハードウェアデコードを切り替えるには、切り替えの前に**stopPlay**を実行して、切り替えの後に**startPlay**を実行する必要があります。そうしないと、画面のちらつき問題が発生します。

```objectivec
[_txVodPlayer stopPlay];
_txVodPlayer.enableHWAcceleration = YES;
[_txVodPlayer startPlay:_flvUrl type:_type];
```

### 10、シャープネスの設定
SDKはhlsのマルチビットレート形式をサポートしており、ユーザーは異なるビットレートの再生ストリームを簡単に切り替えることができます。PLAY_EVT_PLAY_BEGINイベントを受信した後、マルチビットレート配列は以下の方法で取得することができます
```objectivec
NSArray *bitrates = [_txVodPlayer supportedBitrates]; //マルチビットレート配列を取得します
```

再生中はいつでも`-[TXVodPlayer setBitrateIndex:]`でビットレートを切り替えることができます。切り替え中は、別のストリームのデータを再び引き取るため、少しカクカクすることがあります。SDKはTencent Cloudのマルチビットレートファイル向けに最適化され、ラグなしで切り替えることができます。
### 11、アダプティブビットレートストリーミング
SDKはHLSのアダプティブビットレートストリーミングをサポートし、関連機能をオンにすると、プレーヤーは現在の帯域幅に最適なビットレートを動的に選択して再生することができます。`PLAY_EVT_PLAY_BEGIN`イベントを受信した後、以下の方法でアダプティブビットレートストリーミングをオンにすることができます：
```objectivec
[_txVodPlayer setBitrateIndex:-1]; //indexパラメータに-1を渡します
```
再生中はいつでも`-[TXVodPlayer setBitrateIndex:]`で他のビットレートを切り替えることができます。切り替えた後、アダプティブビットレートストリーミングもオフにされます。

###12、再生位置のリスニング

オンデマンド再生位置情報には、**ロードの進行状況**と**再生位置**の2種類があります。SDKでは、この2つの進行状況をイベント通知としてリアルタイムで通知しています。イベント通知の詳細については、[イベントリスニング](#listening)をご参照ください。


```objective-c
-(void) onPlayEvent:(TXVodPlayer *)player event:(int)EvtID withParam:(NSDictionary*)param {
    if (EvtID == PLAY_EVT_PLAY_PROGRESS) {
            // ロードの進行状況（秒単位、小数部はミリ秒）
            float playable = [param[EVT_PLAYABLE_DURATION] floatValue];
                [_loadProgressBar setValue:playable];
                
            // 再生位置（秒単位、小数部はミリ秒）
            float progress = [param[EVT_PLAY_PROGRESS] floatValue];
                [_seekProgressBar setValue:progress];
                
            // ビデオの長さ（秒単位、小数部はミリ秒）
            float duration = [param[EVT_PLAY_DURATION] floatValue];
            // 時間表示の設定などに使用されます
    }
}
```


### 13、再生ネットワーク速度のリスニング

[イベントリスニング](#listening)を使用すると、ビデオがカクカクするときに現在のネットワーク速度を表示できます。

* 現在のネットワーク速度は`onNetStatus`の`NET_SPEED`を使用して取得されます。具体的な使用方法については[ステータスフィードバック(onNetStatus)](#status)をご参照ください。
* `PLAY_EVT_PLAY_LOADING`イベントを受信した後、現在のネットワーク速度を表示します。
* `PLAY_EVT_VOD_LOADING_END`イベントを受信した後、現在のネットワーク速度を表示するviewを非表示にします。

### 14、ビデオ解像度の取得

プレーヤーSDKは、URL文字列を通じて映像を再生します。URL自身に映像情報が含まれていません。関連情報を取得するには、クラウド上のサーバーにアクセスして関連ビデオ情報をロードする必要があります。したがって、SDKはイベント通知としてのみビデオ情報をアプリケーションに送信できます。詳細は[イベントリスニング](#listening)をご参照ください。

**解像度情報**
<dx-tabs>
::: 方法1
`onNetStatus`の`VIDEO_WIDTH`と`VIDEO_HEIGHT`を通じてビデオの幅と高さを取得します。具体的な使用方法については[ステータスフィードバック(onNetStatus)](#status)をご参照ください。
:::
::: 方法2
直接`-[TXVodPlayer width]`と`-[TXVodPlayer height]`を呼び出して現在の幅と高さを取得します。
:::
</dx-tabs>

### 15、再生バッファサイズ

通常の映像再生時にネットワークから予めバッファリングされる最大データサイズをコントロールします。設定されていない場合は、スムーズな再生を確保するため、プレーヤーのデフォルトのバッファポリシーが適用されます。

```java
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setMaxBufferSize:10];  // 再生時の最大バッファサイズ。単位：MB
[_txVodPlayer setConfig:_config];  // config を _txVodPlayerに渡す
```

### 16、ビデオのローカルキャッシュ[](id：cache)
短いビデオ再生シーンでは、ビデオファイルのローカルキャッシュは非常に必要な機能であり、一般的なユーザーにとっては、一度見たビデオを再視聴するときに、もう1度トラフィックを消費しないでください。

- **対応形式：**SDKは、一般的なオンデマンド形式であるHLS(m3u8)およびMP4の2つのキャッシュ機能をサポートしています。
- **オンにするタイミング：**SDKでは、デフォルトでキャッシュ機能がオンにされません。また、ユーザのレビュー率が高くないシーンでは、この機能をオンにすることを推奨するものでもありません。
-**オンにする方法：**この機能をオンにするには、ローカルキャッシュディレクトリとキャッシュサイズの2つのパラメータを設定してください。
```objectivec
//再生エンジンのグローバルキャッシュディレクトリを設定します
NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
NSString *documentsDirectory = [paths objectAtIndex:0];
NSString *preloadDataPath = [documentsDirectory stringByAppendingPathComponent:@"/preload"];
if (![[NSFileManager defaultManager] fileExistsAtPath:preloadDataPath]) {
     [[NSFileManager defaultManager] createDirectoryAtPath:preloadDataPath
                               withIntermediateDirectories:NO
                                                attributes:nil
                                                     error:&error];
[TXPlayerGlobalSetting setCacheFolderPath:preloadDataPath];
//再生エンジンのキャッシュサイズを設定します
[TXPlayerGlobalSetting setMaxCacheSize:200];
// ...
// 再生の開始
[_txVodPlayer startPlay:playUrl];                            
```

>?古いバージョンでは、TXVodPlayConfig#setMaxCacheItemsインターフェースを使用して設定され、すでに廃止されたため、使用は推奨されていません。

## 高級機能使用

### 1、ビデオのプリプレイ

#### ステップ1：ビデオプリプレイの使用

短いビデオ再生シーンでは、プリロード機能がスムーズな再生の体験に役立ちます。現在のビデオを視聴している間に、再生する次のビデオURLをバックグラウンドでロードします。これにより、ユーザーが実際に次のビデオに切り替えたときに、最初からロードする必要はなくなり、すぐに再生することが可能になります。

ビデオをプリプレイすると、素早い再生の効果が得られますが、パフォーマンスのオーバーヘッドが必要です。業務で同時にビデオをプリロードする必要がある場合は、[ビデオのプリダウンロード](#download)と組み合わせて使用することをお勧めします。

これは、ビデオ再生のシームレスな切り替えを実現するための技術的なサポートですT。TXVodPlayerのisAutoPlayを使用してこの機能を実装できます。具体的な使い方は次のとおりです：
<img src="https://qcloudimg.tencent-cloud.cn/raw/b2bd645f29af403bf2740156aee44092.jpg" width=850px>

```objectivec
// ビデオAの再生: isAutoPlayisAutoPlayがYesに設定されている場合、startPlayを呼び出すとすぐにビデオのロードと再生を開始します
NSString* url_A = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f10.mp4";
_player_A.isAutoPlay = YES;
[_player_A startPlay:url_A];

// ビデオAを再生しながら、isAutoPlayをNoに設定してビデオBをプリロードします
NSString* url_B = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
_player_B.isAutoPlay = NO;
[_player_B startPlay:url_B];
```

ビデオAの再生が終了し、自動的に（あるいはユーザーが手動で）ビデオBに切り替えたときに、resume関数を呼び出すとすぐに再生できます。

>! autoPlayがfalseに設定されている場合、resumeを呼び出す前に、ビデオBの準備が完了していることを確認する必要があります。つまり、ビデオBのPLAY_EVT_VOD_PLAY_PREPARED（2013。プレーヤー準備が完了し、再生可能になりました）イベントを受信した後に呼び出されます。

```objectivec
-(void) onPlayEvent:(TXVodPlayer *)player event:(int)EvtID withParam:(NSDictionary*)param
{
    // ビデオAの再生が終了した時点で、ビデオBの再生を直接開始することで、シームレスに切り替えることができます
    if (EvtID == PLAY_EVT_PLAY_END) {
            [_player_A stopPlay];
            [_player_B setupVideoWidget:mVideoContainer insertIndex:0];
            [_player_B resume];
        }
}
```

#### ステップ2：ビデオプリプレイのバッファー設定

- バッファを大きく設定することで、ネットワークの揺らぎに対応し、スムーズな再生を実現することができます。

- バッファを小さく設定すると、トラフィックの消費を抑えることができます。 

##### プリプレイバッファサイズ

このインターフェースは、プリロードシーン（ビデオの再生開始前で、playerのAutoPlayがfalseに設定されている場合）で、再生開始前の段階での最大バッファサイズを制御するために使用されます。

```objective-c
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setMaxPreloadSize:(2)];;  // プリプレイ時の最大バッファサイズ。単位：MB。業務状況に応じてトラフィックを節約するように設定します
[_txVodPlayer setConfig:_config];  // config を _txVodPlayerに渡す
```

##### プリプレイバッファサイズ 

通常の映像再生時にネットワークから予めバッファリングされる最大データサイズをコントロールします。設定されていない場合は、スムーズな再生を確保するため、プレーヤーのデフォルトのバッファポリシーが適用されます。

```objective-c
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setMaxBufferSize:10];  // 再生時の最大バッファサイズ。単位：MB
[_txVodPlayer setConfig:_config];  // config を _txVodPlayerに渡す
```

### 2、動画のプリダウンロード[](id:download)
プレーヤーのインスタンスを作成する必要がなく、ビデオの一部のコンテンツを事前にダウンロードすると、プレーヤを使用するときに、ビデオの再生開始速度が速くなり、より良い再生体験を提供できます。

再生サービスを使用する前に、[ビデオキャッシュ](#cache)が設定されていることを確認してください。
>?
>- TXPlayerGlobalSettingはグローバルキャッシュ設定インターフェースであり、従来のTXVodConfigのキャッシュ設定インターフェースは破棄されます。
>- グローバルキャッシュディレクトリとサイズの設定は、プレーヤーのTXVodConfigに設定されたキャッシュ設定よりも優先されます。

ユースケース：

```objective-c
//再生エンジンのグローバルキャッシュディレクトリを設定します
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

//再生エンジンのキャッシュサイズを設定します
[TXPlayerGlobalSetting setMaxCacheSize:200];
NSString *m3u8url = "http://****";
int taskID = [[TXVodPreloadManager sharedManager] startPreload:m3u8url 
 																									 preloadSize:10 
 																					 preferredResolution:1920*1080 
 																											delegate:self];


//事前ダウンロードをキャンセルします
[[TXVodPreloadManager sharedManager] stopPreload:taskID];
```

### 3. 動画のダウンロード
ビデオのダウンロードは、ネットワークが存在する状態でビデオをダウンロードし、そしてネットワークが存在しない環境で視聴することをサポートします。また、プレーヤーSDKはローカル暗号化能力を提供しており、ダウンロード後のローカルビデオは暗号化されたままであり、ビデオの復号化と再生には指定されたプレーヤーが必要であり、ダウンロードのビデオの違法な伝播を効果的に防止し、ビデオの安全を保護することができます。

HLSストリーミングメディアはローカルに直接保存できないので、ローカルファイルを再生することでHLSのオフライン再生を実現することもできません。この問題については、`TXVodDownloadManager'に基づくビデオダウンロードスキームを使用してHLSのオフライン再生を行うことができます。

> ! 
> -  `TXVodDownloadManager`は、MP4およびFLV形式のファイルのキャッシュを現在のところサポートしておらず、HLS形式のファイルのキャッシュのみをサポートします。
> - プレーヤーSDKは、MP4及びFLV形式のローカルファイル再生をサポートしています。
[](id:offline1)
#### ステップ1：準備作業

`TXVodDownloadManager`は単一のインスタンスとして設計されているので、複数のダウンロードオブジェクトを作成することはできません。使い方は次のとおりです：

```objective-c
TXVodDownloadManager *downloader = [TXVodDownloadManager shareInstance];
[downloader setDownloadPath:"<ダウンロードディレクトリを指定>"];
```

[](id:offline2)
#### ステップ2：ダウンロード開始
ダウンロード開始の2つの方式：URLとfileid。
<dx-tabs>
::: URL方式
ダウンロードアドレスを渡すだけでよいです。
```objective-c
[downloader startDownloadUrl:@"http://1253131631.vod2.myqcloud.com/26f327f9vodgzp1253131631/f4bdff799031868222924043041/playlist.m3u8"]
```
:::
::: fileid方式
Fileidのダウンロードには、少なくともappIdとfileIdを渡してください。
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

タスク情報を受信する前に、コールバックdelegateを設定してください。

```objective-c
downloader.delegate = self;
```

受信可能なタスクコールバックは次のとおりです：
<table><thead>
<tr><th width="55%">コールバック情報</th><th>意味</th></tr>
</thead>
<tbody><tr>
<td>-[TXVodDownloadDelegate onDownloadStart:]</td>
<td>タスク開始。SDKのダウンロードが開始されたことを意味します</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadProgress:]</td>
<td>タスクの進行状況。ダウンロード中にSDKが頻繁にこのインターフェースにコールバックします。ここで進行状況の表示を更新できます</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadStop:]</td>
<td>タスクが停止しました。<code>stopDownload</code>呼び出してダウンロードを停止した場合、このメッセージが表示されると、正常に停止したことを意味します</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadFinish:]</td>
<td>ダウンロードが完了しました。このコールバックを受信すると、すべてがダウンロードされたことを意味します。この場合、ダウンロードしたファイルをTXVodPlayerで再生できます</td>
</tr>
<tr>
<td>-[TXVodDownloadDelegate onDownloadError:errorMsg:]</td>
<td>ダウンロードエラー。ダウンロード中にネットワークが切断されると、このインターフェースがコールバックされ、同時にダウンロードタスクが停止します。すべてのエラーコードは<code>TXDownloadError</code>をご参照ください</td>
</tr>
</tbody></table>

downloaderは複数のタスクを同時にダウンロードできるので、コールバックインターフェースには`TXVodDownloadMediaInfo`オブジェクトが用意されています。URLやdataSourceにアクセスしてダウンロード元を判断し、同時にダウンロードの進行状況やファイルサイズなどの情報を得ることができます。

[](id:offline4)
#### ステップ4：ダウンロードの中断

ダウンロードを停止するには、`-[TXVodDownloadManager stopDownload:]`メソッドを呼び出してください。パラメータは`-[TXVodDownloadManager sartDownloadUrl:]`から返されたオブジェクトです。**SDKは一時停止/再開をサポートしています。**ダウンロードディレクトリが変更されていない場合、同じファイルの次回のダウンロードは、前回停止した場所から再開されます。

再ダウンロードする必要がない場合は、`-[TXVodDownloadManager deleteDownloadFile:]`メソッドを呼び出してファイルを削除し、ストレージを解放してください。

### 4、暗号化して再生します

ビデオ暗号化スキームは主にオンライン教育など、ビデオ著作権の保護が必要なシーンで使用されています。ビデオリソースを暗号化して保護するには、プレーヤーを改造するだけでなく、ビデオソース自体を暗号化してトランスコードしてください。また、それらの作業にはバックグラウンド及び端末開発のエンジニアが参加する必要があります。詳細については、[ビデオ暗号化ソリューション](https://intl.cloud.tencent.com/document/product/266/38131)をご参照ください。

###5、プレーヤーの設定 

statPlayを呼び出す前に、setConfigを使用してプレーヤーのパラメータ設定を行うことができます。例えば、プレーヤー接続タイムアウト時間、進行状態のコールバック間隔、キャッシュファイル数などの設定が可能です。TXVodPlayConfigでサポートされている詳細な設定パラメータについては、[基本設定インターフェース](https://intl.cloud.tencent.com/document/product/266/47844)をご参照ください。ユースケース：

```java
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setEnableAccurateSeek:true];  // 正確なseekを実行するかどうかを設定します。デフォルトはtrueです
[_config setMaxCacheItems:5];  // キャッシュファイル数を5に設定します
[_config setProgressInterval:200];  // 再生位置のコールバック間隔をミリ秒単位で設定します
[_config setMaxBufferSize:50];  // 最大プリロードサイズ（単位MB）
[_txVodPlayer setConfig:_config];  // config を _txVodPlayerに渡す
```

##### 再生開始時に解像度を指定します

 マルチビットレートのHLSビデオソースを再生します。ビデオストリームの解像度情報を事前に知っていれば、再生開始前に再生するビデオ解像度を優先的に指定することができます。プレーヤーは、好みの解像度以下のストリームを探して再生を開始します。再生後は、setBitrateIndexを使用して必要なビットレートストリームに切り替える必要はありません。

```java
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
// 渡すパラメータはビデオの幅と高さの積（幅*高さ）です。カスタマイズした値を渡すことができます
[_config setPreferredResolution:720*1280];
[_txVodPlayer setConfig:_config];  // config を _txVodPlayerに渡す
```

##### 再生位置のコールバック間隔を設定します

```objective-c
TXVodPlayConfig *_config = [[TXVodPlayConfig alloc]init];
[_config setProgressInterval:200];  // 再生位置のコールバック間隔をミリ秒単位で設定します
[_txVodPlayer setConfig:_config];  // config を _txVodPlayerに渡す
```

[](id:listening)

## プレーヤーイベント監視
TXVodPlayerオブジェクトにTXVodPlayリスナーをバインドすることができます。つまり、onPlayEvent（イベント通知）とonNetStatus（ステータスフィードバック）を使用してアプリケーションと情報を同期できます。

### イベント通知（onPlayEvent）

#### 再生イベント
| イベントID                 |    数値  |  意味説明                |
| :-------------------  |:-------- |  :------------------------ |
|PLAY_EVT_PLAY_BEGIN    |  2004|  ビデオ再生開始 |
|PLAY_EVT_PLAY_PROGRESS |  2005|  ビデオ再生位置。現在の再生位置、ロードの進行状態と全体時間を通知します     |
|PLAY_EVT_PLAY_LOADING  |  2007|  ビデオ再生のloading。再開可能な場合、その後にLOADING_ENDイベントが発生します|
|PLAY_EVT_VOD_LOADING_END   |  2014|  ビデオ再生loadingが終了し、ビデオが引き続き再生します|
| VOD_PLAY_EVT_SEEK_COMPLETE | 2019 | Seekの完了です。バージョン10.3からサポートしています|

#### 終了イベント
| イベントID                 |    数値  |  意味説明                |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_EVT_PLAY_END       | 2006  | ビデオ再生終了                                           |
|PLAY_ERR_NET_DISCONNECT |  -2301  |  ネットワーク接続が切断され、何度も再接続しても回復できません。さらにリトライしたければ、手動で再起動後再生してください |
| PLAY_ERR_HLS_KEY        | -2305 | HLS復号キーの取得に失敗しました                                  |

#### 警告イベント
これらのイベントは、SDK内のイベントの一部を知らせるためだけに使用されていますが、気にしなくてもかまいません。

| イベントID                 |    数値  |  意味説明                |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | 現在のビデオフレームのデコードに失敗しました  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | 現在のオーディオフレームのデコードに失敗しました  |
| PLAY_WARNING_RECONNECT           |  2103  | ネットワーク接続が切断され、自動再接続が有効にされています（再接続回数が3回を超えるとPLAY_ERR_NET_DISCONNECTがスローされます）|
| PLAY_WARNING_HW_ACCELERATION_FAIL|  2106  | ハードウェアデコードの開始に失敗しました。ソフトウェアデコードを使用してください   |


#### 接続イベント
またいくつのサーバー接続イベントは主にサーバー接続時間の測定と統計に使用されます。

| イベントID                 |    数値  |  意味説明                |
| :-----------------------  |:-------- |  :------------------------ |
| PLAY_EVT_VOD_PLAY_PREPARED | 2013 | プレーヤーの再生準備が完了し、再生可能状態です。autoPlayがfalseに設定されている場合、このイベントを受信してからresumeを呼び出すと再生を開始します |
| PLAY_EVT_RCV_FIRST_I_FRAME | 2003 | ネットワークが最初のレンダリング可能なビデオパケット（IDR）を受信しました                      |

#### 画面イベント
次のイベントは、画面の変更情報を取得するために使用されます。

| イベントID                 |    数値  |  意味説明                |
| :-----------------------  |:-------- |  :------------------------ |
| PLAY_EVT_CHANGE_RESOLUTION|  2009    | ビデオ解像度の変更               |
| PLAY_EVT_CHANGE_ROATION   |  2011    | MP4 ビデオ回転角度 |


#### ビデオ情報イベント
| イベントID                 |    数値  |  意味説明                |
| :-----------------------  |:-------- |  :------------------------ |
|PLAY_EVT_GET_PLAYINFO_SUCC   | 2010 | 正常に再生ファイル情報を取得しました |

再生はfileId方式を使用し、リクエストが成功した場合、SDKは上位層にリクエスト情報を通知します。PLAY_EVT_GET_PLAYINFO_SUCCイベントを受信した後、paramを解析してビデオ情報を取得することができます。

| ビデオメッセージ              | 意味説明     |
| :------------------------  |  :------------------------ |
| EVT_PLAY_COVER_URL     | ビデオタイトル画像アドレス |
| EVT_PLAY_URL  | ビデオ再生アドレス |
| EVT_PLAY_DURATION | ビデオの長さ |

```objective-c
-(void) onPlayEvent:(TXVodPlayer *)player event:(int)EvtID withParam:(NSDictionary*)param
{
    if (EvtID == PLAY_EVT_VOD_PLAY_PREPARED) {
        // プレーヤーの準備ができているイベントを受信しました。この時点で、pause、resume、getWidth、getSupportedBitratesなどのインターフェースを呼び出すことができます
    } else if (EvtID == PLAY_EVT_PLAY_BEGIN) {
        // 再生開始イベントを受信しました
    } else if (EvtID == PLAY_EVT_PLAY_END) {
        // 開始終了イベントを受信しました
    }
}
```

[](id:status)

### ステータスのフィードバック（onNetStatus）
ステータスフィードバックは0.5秒ごとにトリガされ、現在のプッシャ状態をリアルタイムでフィードバックすることを目的としています。これは自動車のダッシュボードのように、現在のSDK内部の特定の状況を知らせることができ、現在のビデオ再生の状態などを理解できるようになります。
<table>
<tr><th>評価パラメータ</th><th>意味説明</th></tr><tr>
<td>CPU_USAGE</td><td>現在の瞬時CPU使用率</td>
</tr><tr>
<td>VIDEO_WIDTH</td><td>ビデオ解像度 - 幅</td>
</tr><tr>
<td>VIDEO_HEIGHT</td><td>ビデオ解像度 - 高さ</td>
</tr><tr>
<td>NET_SPEED</td><td>現在のネットワークデータの受信速度</td>
</tr><tr>
<td>VIDEO_FPS</td><td>現在のストリーミングメディアのビデオフレームレート</td>
</tr><tr>
<td>VIDEO_BITRATE</td><td>現在のストリーミングメディアのビデオビットレート（kbps単位）</td>
</tr><tr>
<td>AUDIO_BITRATE</td><td>現在のストリーミングメディアのオーディオビットレート（kbps単位）</td>
</tr><tr>
<td>V_SUM_CACHE_SIZE</td><td>バッファ（jitterbuffer）のサイズ。バッファの現在の長さは0であれば、カクカクする可能性が高いことを意味します</td>
</tr><tr>
<td>SERVER_IP</td><td>接続されたサーバーIP</td>
</tr></table>
onNetStatusからビデオ再生プロセス情報を取得する例：
```objective-c
- (void)onNetStatus:(TXVodPlayer *)player withParam:(NSDictionary *)param {
    //現在のCPU使用率を取得します
    float cpuUsage = [[param objectForKey:@"CPU_USAGE"] floatValue];
    // ビデオ幅の取得
    int videoWidth = [[param objectForKey:@"VIDEO_WIDTH"] intValue];
    // ビデオの高さの取得
    int videoHeight = [[param objectForKey:@"VIDEO_HEIGHT"] intValue];
    //リアルタイムレートを取得
    int  speed = [[param objectForKey:@"NET_SPEED"] intValue];
    //現在のストリーミングメディアのビデオフレームレートを取得します
    int fps = [[param objectForKey:@"VIDEO_FPS"] intValue];
    //現在のストリーミングメディアのビデオビットレート（kbps単位）を取得します
    int videoBitRate = [[param objectForKey:@"VIDEO_BITRATE"] intValue];
    //現在のストリーミングメディアのオーディオビットレート（kbps単位）を取得します
    int audioBitRate = [[param objectForKey:@"AUDIO_BITRATE"] intValue];
    //バッファ（jitterbuffer）のサイズを取得します。バッファの現在の長さは0であれば、カクカクする可能性が高いことを意味します
    int jitterbuffer = [[param objectForKey:@"V_SUM_CACHE_SIZE"] intValue];
    //連続したサーバーののIPアドレスを取得します
    NSString *ip = [param objectForKey:@"SERVER_IP"];
}
```

##  シーン化機能

### 1、SDKベースのDemoコンポーネント

Tencent CloudはプレーヤーSDKに基づき、品質監視、動画暗号化、超高速HD、シャープネス切り替え、小窓再生などの機能を一体化した、すべてのオンデマンド、ライブ再生シーンに対応する[プレーヤーコンポーネント](https://intl.cloud.tencent.com/document/product/266/33976)を開発しました。完全な機能を実装し、上位UIを提供することで、市販されているさまざまなビデオアプリに匹敵する再生ソフトウェアを短期間で構築することができます。

### 2、オープンソースGithub

Tencent CloudはプレーヤーSDKに基づき、没入型ビデオプレーヤーコンポーネント、ビデオFeedストリーム、複数プレーヤーに再利用可能なコンポーネントなどを開発しており、リリースに伴い、ユーザーシナリオに基づくコンポーネントをより多く提供していきます。[Player_iOS](https://github.com/LiteAVSDK/Player_iOS)でダウンロードして体験いただけます。
