本文書では、TRTCルームのオーディオビデオストリームをライブストリーミングCDNに公開（「転送/プッシュ」とも呼ばれる）して、互換性のある通常のライブプレーヤーで視聴する方法について説明します。

## 現在のユーザーのオーディオストリームとビデオストリームをライブストリーミングCDNに公開します

![](https://qcloudimg.tencent-cloud.cn/raw/f1df9ddcf6fbf206cb6e6b29af88ff31.png)
### 機能説明

TRTCCloudが提供するインターフェース**startPublishMediaStream**を使用することで、ルームにおける現在のユーザーのオーディオビデオストリームをライブストリーミングCDNに公開できます（「CDNへの公開」は「CDNへの転送/プッシュ」とも呼ばれます）。
このプロセスでは、TRTCのクラウドサーバーはオーディオビデオデータに対して二次トランスコーディング処理を実行するのではなく、オーディオビデオデータをライブストリーミングCDNサーバーに直接インポートするため、プロセス全体のコストが最も低くなります。
ただし、ルーム内の各オーディオビデオユーザーは、対応するCDNライブストリームを持っている必要があります。そのため、ルームに複数のユーザーのオーディオビデオストリームがある場合、視聴者は複数のライブプレーヤーを使用して視聴する必要があります。また、再生の進捗状況は、CDNライブストリーム間で大きく異なる可能性があります。

### 操作ガイド
以下のガイドに従って、ルームにいる現在のユーザーのオーディオビデオストリームをライブストリーミングCDNに公開することができます。
1. TRTCPublishTargetオブジェクトを作成し、TRTCPublishTargetオブジェクトのmodeパラメータに`TRTCPublishBigStreamToCdn`または`TRTCPublishSubStreamToCdn`を指定します。前者は現在のユーザーのメインチャネル画面（通常はカメラ）の公開、後者は現在のユーザーのサブチャネル画面（通常は画面共有）の公開を指します。
2. TRTCPublishTargetオブジェクトのcdnUrlListパラメータに1つまたは複数のCDNプッシュアドレスを指定します（標準CDNプッシュアドレスは通常、`rtmp://`をURLプレフィックスとして使用します）。指定したurlがTencent CloudのライブストリーミングCDNのプッシュアドレスである場合は、isInternalLineにtrueを設定する必要があります。そうでない場合は、falseを設定します。
3. このモードでは、トランスコーディングサービスが提供されていないため、インターフェースを呼び出す際に、`TRTCStreamEncoderParam`パラメータと`TRTCStreamMixingConfig`パラメータを指定しないでください。
4. startPublishMediaStreamインターフェースを呼び出し、onStartPublishMediaStreamを介してローカルAPIの呼び出しに成功したかどうかを監視します。成功した場合、onStartPublishMediaStreamのtaskIdは空白でない文字列を返します。
5. 公開を停止する必要がある場合は、stopPublishMediaStreamを呼び出し、onStartPublishMediaStreamを介して取得したtaskIdを渡してください。

### 参照コード

以下のコードは、現在のユーザーのオーディオビデオストリームをライブストリーミングCDNに公開する機能を実装します。

<dx-codeblock>
::: Java
```
// 現在のユーザーのオーディオビデオストリームをライブストリーミングCDNに公開します
TRTCCloudDef.TRTCPublishTarget target = new TRTCCloudDef.TRTCPublishTarget();
target.mode = TRTC_PublishBigStream_ToCdn;

TRTCCloudDef.TRTCPublishCdnUrl cdnUrl= new TRTCCloudDef.TRTCPublishCdnUrl();
cdnUrl.rtmpUrl = "rtmp://tencent/live/bestnews";
cdnUrl.isInternalLine = true;
target.cdnUrlList.add(cdnUrl);

mTRTCCloud.startPublishMediaStream(target, null, null);
```
:::
::: ObjC
```
// 現在のユーザーのオーディオビデオストリームをライブストリーミングCDNに公開します
TRTCPublishTarget* target = [[TRTCPublishTarget alloc] init];
target.mode = TRTCPublishBigStreamToCdn;

TRTCPublishCdnUrl* cdnUrl = [[TRTCPublishCdnUrl alloc] init];
cdnUrl.rtmpUrl = @"rtmp://tencent/live/bestnews";
cdnUrl.isInternalLine = YES;

NSMutableArray* cdnUrlList = [NSMutableArray new];
[cdnUrlList addObject:cdnUrl];
target.cdnUrlList = cdnUrlList;

[_trtcCloud startPublishMediaStream:target encoderParam:nil mixingConfig:nil];
```
:::
::: C++
```
// 現在のユーザーのオーディオビデオストリームをライブストリーミングCDNに公開します
TRTCPublishTarget target;
target.mode = TRTCPublishMode::TRTCPublishBigStreamToCdn;

TRTCPublishCdnUrl* cdn_url_list = new TRTCPublishCdnUrl[1];
cdn_url_list[0].rtmpUrl = "rtmp://tencent/live/bestnews";
cdn_url_list[0].isInternalLine = true;

target.cdnUrlList = cdn_url_list;
target.cdnUrlListSize = 1;

trtc->startPublishMediaStream(&target, nullptr, nullptr);
delete[] cdn_url_list;
```
:::
</dx-codeblock>


## 合成済みのオーディオビデオストリームをライブストリーミングCDNに公開します

![](https://qcloudimg.tencent-cloud.cn/raw/fa00298505bb8284bb5224b65cff4c6a.png)

### 機能の説明
TRTCルーム内の複数のユーザーのオーディオビデオストリームを1つのチャネルに合成し、合成後のオーディオビデオストリームをライブストリーミングCDNに公開する場合は、**startPublishMediaStream**インターフェースを呼び出して、ミクスストリーミングとトランスコーディングを制御する`TRTCStreamEncoderParam`パラメータと`TRTCStreamMixingConfig`パラメータを指定します。

1つのオーディオビデオストリームを合成してライブストリーミングCDNに公開するには、TRTCの複数のチャネルのオーディオビデオストリームをクラウドでデコードしてから、指定したミクスストリーミングパラメータ(`TRTCStreamMixingConfig`)によって合成を実行し、最後に指定したパラメータ(`TRTCStreamEncoderParam`)によって再エンコードする必要があるため、このモードでの転送/プッシュサービスは[トランスコーディング料金](https://intl.cloud.tencent.com/document/product/647/38929)が請求されます。

### 操作ガイド
以下のガイドに従って、ルームにいる複数のユーザーのオーディオビデオストリームを合成してライブストリーミングCDNに公開することができます。
1.TRTCPublishTargetオブジェクトを作成し、TRTCPublishTargetオブジェクトのmodeパラメータに`TRTCPublishMixStreamToCdn`を指定します。
2.TRTCPublishTargetオブジェクトのcdnUrlListパラメータに1つまたは複数のCDNプッシュアドレスを指定します（標準CDNプッシュアドレスは通常、`rtmp://`をURLプレフィックスとして使用します）。指定したurlがTencent CloudのライブストリーミングCDNのプッシュアドレスである場合は、isInternalLineにtrueを設定してください。そうでない場合は、falseを設定します。
3. パラメータ`TRTCStreamEncoderParam`を使用して、トランスコーディングされたオーディオビデオストリームのコーデックパラメータを設定します。
**ビデオコーデックパラメータ：**合成後の画面の解像度、フレームレート、ビットレート、エンコードのGOPを指定してください。そのうち、GOPに3s、FPSに15を設定することをお勧めします。ビットレートと解像度は対応関係があります。下表によく使用される解像度とそれに対応する推奨ビットレートを示します。
**オーディオコーデックパラメータ：**合成後のオーディオのコーデックフォーマット、コーデックビットレート、サンプリングレートとサウンドチャンネル数を指定してください。このステップでは、startLocalAudioを呼び出すときに2番目のパラメータAudioQualityに指定された音質タイプに応じて、パラメータを指定してください。

|videoEncodedWidth | videoEncodedHeight | videoEncodedFPS |  videoEncodedGOP |  videoEncodedKbps |
|:-------:|:-----:|:-------:|:------:|:------:|
| 640   | 360	    | 15 | 3 |  800kbps |
| 960   | 540	    | 15 | 3 | 1200kbps |
| 1280 | 720	   | 15 | 3 | 1500kbps |
| 1920 | 1080   | 15 | 3 | 2500kbps |

| TRTCAudioQuality | audioEncodedSampleRate | audioEncodedChannelNum | audioEncodedKbps | audioEncodedCodecType |
|---------|---------|---------|---------|---------|
| TRTCAudioQualitySpeech | 48000 | 1 | 50 | 0 |
| TRTCAudioQualityDefault | 48000 | 1 | 50 | 0 |
| TRTCAudioQualityMusic | 48000 | 2 | 60 | 2 |

4. パラメータ`TRTCStreamMixingConfig`を使用して、オーディオのミクスストリーミングパラメータと画面レイアウトモードを設定します。
オーディオのミクスストリーミングパラメータ(audioMixUserList)：デフォルトでは、空白のままでよいです。これは、ルーム内のすべてのオーディオが合成されることを意味します。ルーム内の一部のユーザーの音声を合成する場合にのみ、このパラメーターを指定してください。
**画面レイアウトパラメータ(videoLayoutList)**：画面のレイアウトは配列によって定義されます。配列における各TRTCVideoLayoutオブジェクトは、1つのエリアの位置、サイズ、背景色などを表します。TRTCVideoLayoutの**fixedVideoUser**フィールドを指定した場合、このlayoutオブジェクトで定義されたエリアに、常にあるユーザーの画面が表示されます。fixedVideoUserにnullを指定した場合、このエリアに画面が表示されるが、画面に表示されたユーザーは固定されておらず、TRTCミクスストリーミングサーバがルールに従って決めます。

> **例1：4名のユーザーの画面が1つの画面に合成して表示されています。1枚の画像を背景として使用しています**
> - layout1：ユーザーjerryのカメラ画面のサイズと位置を定義します。画面サイズは640x480です。画面は中央上部に配置されます。
> - 、layout2、layout3、layout4：具体的なユーザーIDが指定されていないため、TRTCは、特定のルールに従ってルームにおける3つのチャネルのユーザーの画面を選択し、これらの3つの位置に配置します。
![](https://qcloudimg.tencent-cloud.cn/raw/6530f7a07ef88f22ec9798d41f646b63.png) <br>

> **例2：4名のユーザーのカメラ画面と1つのチャネルの画面共有の画面が1つの画面に合成して表示されています**
> - layout1: ユーザーjerryが共有する画面のサイズと位置を定義します。画面サイズは1280x720で、埋め込みモードは黒枠が表示されることがあるFitモードで、背景の塗りつぶしは黒いです。画面は左側に配置されます。
> - layout2: ユーザーjerryのカメラ画面のサイズと位置を定義します。画面サイズは300x200で、埋め込みモードはFillモードです。画面は右上に配置されます。
> - 、layout3、layout4、layout5：具体的なユーザーIDが指定されていないため、TRTCは、特定のルールに従ってルームにおける3つのチャネルのユーザーの画面を選択し、これらの3つの位置に配置します。
![](https://qcloudimg.tencent-cloud.cn/raw/0cd5b07fb3e03e6a742f9c396c6ea241.png)

5. startPublishMediaStreamインターフェースを呼び出し、onStartPublishMediaStreamを介してローカルAPIの呼び出しに成功したかどうかを監視します。成功した場合、onStartPublishMediaStreamのtaskIdは空白でない文字列を返します。
6.ミクスストリーミングパラメータを変更する場合、たとえば、複数の画面のレイアウトモードを調整する場合は、ステップ5のtaskIdでupdatePublishMediaStream APIを呼び出し、新しいTRTCStreamMixingConfigパラメータを渡してください。転送/プッシュ中にTRTCStreamEncoderParamを変更すれば、CDNプレーヤーの安定性に影響しますので、変更しないことをお勧めします。
7. 公開アクションを停止する必要がある場合は、stopPublishMediaStreamを呼び出し、onStartPublishMediaStreamを介して取得したtaskIdを渡してください。

### 参照コード
以下のコードは、ルーム内の複数のユーザーのオーディオビデオストリームを合成してライブストリーミングCDNに公開する機能を備えています。

<dx-codeblock>
::: Java
```
// 公開モードをTRTC_PublishMixedStream_ToCdnに指定します
TRTCCloudDef.TRTCPublishTarget target = new TRTCCloudDef.TRTCPublishTarget();
target.mode = TRTC_PublishMixedStream_ToCdn;

// 公開するCDNのプッシュアドレスを指定します
TRTCCloudDef.TRTCPublishCdnUrl cdnUrl= new TRTCCloudDef.TRTCPublishCdnUrl();
cdnUrl.rtmpUrl = "rtmp://tencent/live/bestnews";
cdnUrl.isInternalLine = true;
target.cdnUrlList.add(cdnUrl);


// 合成後のオーディオビデオストリームの二次コーデックパラメータを設定します
TRTCCloudDef.TRTCStreamEncoderParam encoderParam 
    = new TRTCCloudDef.TRTCStreamEncoderParam();
encoderParam.videoEncodedWidth = 1280;
encoderParam.videoEncodedHeight = 720;
encoderParam.videoEncodedFPS = 15;
encoderParam.videoEncodedGOP = 3;
encoderParam.videoEncodedKbps = 1000;
encoderParam.audioEncodedSampleRate = 48000;
encoderParam.audioEncodedChannelNum = 1;
encoderParam.audioEncodedKbps = 50;
encoderParam.audioEncodedCodecType = 0;

// 画面のレイアウトパラメータを設定します
TRTCCloudDef.TRTCStreamMixingConfig mixingConfig =
      new TRTCCloudDef.TRTCStreamMixingConfig();
TRTCCloudDef.TRTCVideoLayout layout1 = new TRTCCloudDef.TRTCVideoLayout();
layout1.zOrder = 0;
layout1.x = 0;
layout1.y = 0;
layout1.width = 720;
layout1.height = 1280;
layout1.fixedVideoStreamType = TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_SUB;
layout1.fixedVideoUser.intRoomId = 1234;    
layout1.fixedVideoUser.userId = "mike"; 

TRTCCloudDef.TRTCVideoLayout layout2 = new TRTCCloudDef.TRTCVideoLayout();
layout2.zOrder = 0;
layout2.x = 1300;
layout2.y = 0;
layout2.width = 300;
layout2.height = 200;
layout2.fixedVideoStreamType = TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG;
layout2.fixedVideoUser.intRoomId = 1234;    
layout2.fixedVideoUser.userId = "mike"; 

TRTCCloudDef.TRTCVideoLayout layout3 = new TRTCCloudDef.TRTCVideoLayout();
layout3.zOrder = 0;
layout3.x = 1300;
layout3.y = 220;
layout3.width = 300;
layout3.height = 200;
layout3.fixedVideoStreamType = TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_SUB;
layout3.fixedVideoUser = null;

mixingConfig.videoLayoutList.add(layout1);
mixingConfig.videoLayoutList.add(layout2);
mixingConfig.videoLayoutList.add(layout3);
mixingConfig.audioMixUserList = null;

// ミクスストリーミングをリクエストします
mTRTCCloud.startPublishMediaStream(target, encoderParam, mixingConfig);
```
:::
::: ObjC
```
// 公開モードにTRTCPublishMixStreamToCdnを指定します
TRTCPublishTarget* target = [[TRTCPublishTarget alloc] init];
target.mode = TRTCPublishMixStreamToCdn;

// 公開するCDNのプッシュアドレスを指定します
TRTCPublishCdnUrl* cdnUrl = [[TRTCPublishCdnUrl alloc] init];
cdnUrl.rtmpUrl = @"rtmp://tencent/live/bestnews";
cdnUrl.isInternalLine = YES;

NSMutableArray* cdnUrlList = [NSMutableArray new];
[cdnUrlList addObject:cdnUrl];
target.cdnUrlList = cdnUrlList;

// 合成後のオーディオビデオストリームの二次コーデックパラメータを設定します
TRTCStreamEncoderParam* encoderParam = [[TRTCStreamEncoderParam alloc] init];
encoderParam.videoEncodedWidth = 1280;
encoderParam.videoEncodedHeight = 720;
encoderParam.videoEncodedFPS = 15;
encoderParam.videoEncodedGOP = 3;
encoderParam.videoEncodedKbps = 1000;
encoderParam.audioEncodedSampleRate = 48000;
encoderParam.audioEncodedChannelNum = 1;
encoderParam.audioEncodedKbps = 50;
encoderParam.audioEncodedCodecType = 0;

// 画面のレイアウトパラメータを設定します
TRTCStreamMixingConfig* config = [[TRTCStreamMixingConfig alloc] init];
NSMutableArray* videoLayoutList = [NSMutableArray new];
TRTCVideoLayout* layout1 = [[TRTCVideoLayout alloc] init];
layout1.zOrder = 0;
layout1.rect = CGRectMake(0, 0, 720, 1280);
layout1.fixedVideoStreamType = TRTCVideoStreamTypeSub;
layout1.fixedVideoUser.intRoomId = 1234;
layout1.fixedVideoUser.userId = @"mike";  

TRTCVideoLayout* layout2 = [[TRTCVideoLayout alloc] init];
layout2.zOrder = 0;
layout2.rect = CGRectMake(1300, 0, 300, 200);
layout2.fixedVideoStreamType = TRTCVideoStreamTypeBig;
layout2.fixedVideoUser.intRoomId = 1234;
layout2.fixedVideoUser.userId = @"mike"; 

TRTCVideoLayout* layout3 = [[TRTCVideoLayout alloc] init];
layout3.zOrder = 0;
layout3.rect = CGRectMake(1300, 220, 300, 200);
layout3.fixedVideoStreamType = TRTCVideoStreamTypeSub;
layout3.fixedVideoUser = nil;

[videoLayoutList addObject:layout1];
[videoLayoutList addObject:layout2];
[videoLayoutList addObject:layout3];
config.videoLayoutList = videoLayoutList;
config.audioMixUserList = nil;

// ミクスストリーミングをリクエストします
[_trtcCloud startPublishMediaStream:target encoderParam:encoderParam mixingConfig:config];
```
:::
::: C++
```
// 公開モードにTRTCPublishMixStreamToCdnを指定します
TRTCPublishTarget target;
target.mode = TRTCPublishMode::TRTCPublishMixStreamToCdn;

// 公開するCDNのプッシュアドレスを指定します
TRTCPublishCdnUrl* cdn_url = new TRTCPublishCdnUrl[1];
cdn_url[0].rtmpUrl = "rtmp://tencent/live/bestnews";
cdn_url[0].isInternalLine = true;
target.cdnUrlList = cdn_url;
target.cdnUrlListSize = 1;

// 合成後のオーディオビデオストリームの二次コーデックパラメータを設定します
TRTCStreamEncoderParam encoder_param;
encoder_param.videoEncodedWidth = 1280;
encoder_param.videoEncodedHeight = 720;
encoder_param.videoEncodedFPS = 15;
encoder_param.videoEncodedGOP = 3;
encoder_param.videoEncodedKbps = 1000;
encoder_param.audioEncodedSampleRate = 48000;
encoder_param.audioEncodedChannelNum = 1;
encoder_param.audioEncodedKbps = 50;
encoder_param.audioEncodedCodecType = 0;

// 画面のレイアウトパラメータを設定します
TRTCStreamMixingConfig config;
TRTCVideoLayout* video_layout_list = new TRTCVideoLayout[3];

TRTCUser* fixedVideoUser0 = new TRTCUser();
fixedVideoUser0->intRoomId = 1234;
fixedVideoUser0->userId = "mike"; 
video_layout_list[0].zOrder = 0;
video_layout_list[0].rect.left = 0;
video_layout_list[0].rect.top = 0;
video_layout_list[0].rect.right = 720;
video_layout_list[0].rect.bottom = 1280;
video_layout_list[0].fixedVideoStreamType =
      TRTCVideoStreamType::TRTCVideoStreamTypeSub;
video_layout_list[0].fixedVideoUser = fixedVideoUser0;  

TRTCUser* fixedVideoUser1 = new TRTCUser();
fixedVideoUser1->intRoomId = 1234;
fixedVideoUser1->userId = "mike"; 
video_layout_list[1].zOrder = 0;
video_layout_list[1].rect.left = 1300;
video_layout_list[1].rect.top = 0;
video_layout_list[1].rect.right = 300;
video_layout_list[1].rect.bottom = 200;
video_layout_list[1].fixedVideoStreamType =
      TRTCVideoStreamType::TRTCVideoStreamTypeBig;
video_layout_list[1].fixedVideoUser = fixedVideoUser1;

video_layout_list[2].zOrder = 0;
video_layout_list[2].rect.left = 1300;
video_layout_list[2].rect.top = 220;
video_layout_list[2].rect.right = 300;
video_layout_list[2].rect.bottom = 200;
video_layout_list[2].fixedVideoStreamType =
      TRTCVideoStreamType::TRTCVideoStreamTypeSub;
video_layout_list[2].fixedVideoUser = nullptr;

config.videoLayoutList = video_layout_list;
config.videoLayoutListSize = 3;
config.audioMixUserList = nullptr;

// ミクスストリーミングをリクエストします
trtc->startPublishMediaStream(&target, &encoder_param, &config);
delete fixedVideoUser0;
delete fixedVideoUser1;
delete[] video_layout_list;
```
:::
</dx-codeblock>

# よくある質問

1. CDNストリームの現在のステータスを監視できますか？ステータスが異常な場合はどうすればよいですか？
回答： `onCdnStreamStateChanged`コールバックを監視することで、最新のバックグラウンドタスクステータスを取得してコールバックを更新できます。詳細については、APIドキュメントをご参照ください。

2. 単一チャネルの転送/プッシュからミクスストリーミングの転送/プッシュに切り替えるには、手動で停止してから転送/プッシュタスクを再作成する必要がありますか？
回答：単一チャネルによるプッシュタスクからミクスストリーミングタスクに直接切り替えることができます。単一チャネルによるプッシュタスク`taskid`に対して、`updatePublishMediaStream`プッシュタスクの変更を実行すればよいです。プッシュリンクの安定性を確保するため、単一チャネルによるプッシュからミクスストリーミングによるプッシュに切り替えると、オーディオのみ、またはビデオのみのモードに切り替えることはできません。デフォルトでは、単一チャネルによるプッシュはオーディオビデオモードになっており、切り替え後のミクスストリーミングもオーディオビデオモードになっている必要があります。

3. ビデオのみでのミクスストリーミングを実現するにはどうすればよいですか？
回答：ミクスストリーミングの設定を構成するときは、 `TRTCStreamEncodeParam`でオーディオ関連のパラメータを設定せず、`TRTCStreamMixingConfig`で`audioMixUserList`を空白に設定してください。

4. ミクスストリーミング画面にウォーターマークを追加できますか？
回答：はい、`TRTCStreamMixingConfig`の`watermarkList`で設定できます。詳細については、APIドキュメントをご参照ください。

5. 教育関連の仕事をしていますので、教師のコンテンツ共有画面をミクスストリーミング、転送、プッシュする必要があります。画面上の共有コンテンツをミクスストリーミングすることはできますか？
回答：はい、できます。サブチャネルを使用してコンテンツ共有画面をプッシュしてから、教師のカメラ画面とコンテンツ共有画面を同じミクスストリーミングタスクに配置することをお勧めします。ミクスストリーミングのサブチャネルを設定する場合は、`TRTCVideoLayout`の`fixedVideoStreamType`を`TRTCVideoStreamTypeSub`に設定すればよいです。

6. プリセットのレイアウトモードで、オーディオストリームの合成を決定するにはどうすればよいですか？
回答：プリセットのレイアウトモードを使用すると、ミクスストリーミングのオーディオは、現在のルームのすべてのアップストリームオーディオから最大16チャネルのオーディオを選択して合成します。

## 関連料金
### 料金の計算
Cloud MixTranscodingでは、MCUクラスタに入力されたオーディオビデオストリームをデコードしてから、再エンコードして出力する必要があるため、追加のサービス料金が発生します。TRTCは、MCUクラスタを使用してCloud MixTranscodingを行ったユーザーに対し、追加の付加価値料金を請求します。Cloud MixTranscodingの料金は、トランスコーディングで入力された解像度とトランスコーディング時間に応じて請求されます。CDNへの転送/プッシュの料金は、毎月のピーク帯域幅に応じて請求されます。詳細については、[ミクスストリーミングと転送/プッシュの課金説明](https://intl.cloud.tencent.com/document/product/647/47631)をご参照ください。

### 料金の節約
クライアントのSDK APIベースのミクスストリーミングスキームで、バックエンドのミクスストリーミングタスクを停止する場合、以下のいずれかの条件を満たす必要があります：
- ミクスストリーミングタスクをリクエストした（つまり、 `startPublishMediaStream`を呼び出した）キャスターがルームから退出したこと
- `stopPublishMediaStream`を呼び出して、自らミクスストリーミングを停止したこと

その他の場合、TRTC Cloudは、ミクスストリーミングの状態を継続して維持するために最善を尽くします。従って、予期せぬミクスストリーミング料金が発生しないよう、ミクスストリーミングが不要な場合は、上記の方法でクラウドミクスストリーミングを可能な限り速やかに終了してください。
