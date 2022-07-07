このドキュメントでは、主に、ルーム内の他のユーザーのオーディオビデオストリームのサブスクリプション方法、つまり、他のユーザーのオーディオビデオの再生方法を紹介します。以下のドキュメントでは、便宜上、「ルーム内の他のユーザー」をまとめて「リモートユーザー」と呼びます。
![](https://qcloudimg.tencent-cloud.cn/raw/9b0ed566818d885be845b9bafb35b57c.png)

## 呼び出しガイド

[](id:step1)
### 手順1：事前手順の完了

[SDKのプロジェクトへのインポート](https://intl.cloud.tencent.com/document/product/647/35092)を参照して、SDKのインポートおよびApp権限の設定を完了します。

[](id:step2)
### 手順2：サブスクリプションモードの設定（非必須）
TRTCCloudの**setDefaultStreamRecvMode**インターフェースを呼び出して、サブスクリプションモードを設定できます。TRTCは2つのサブスクリプションモードを提供します：
- 自動サブスクリプション：SDKは、ユーザー側で追加の動作を実行することなく、リモートユーザーの音声を自動的に再生します。これは、SDKのデフォルトの動作です。
- 手動サブスクリプション：SDKはリモートユーザーの音声を自動的にプルして再生しません。音声の再生をトリガーするには、手動で**muteRemoteAudio(userId, false)**を呼び出してください。
>! SDKのデフォルトの動作は、自動サブスクリプションであるので、setDefaultStreamRecvModeを呼び出さなくても問題ないことに注意してください。ただし、手動サブスクリプションに設定した場合は、setDefaultStreamRecvModeがenterRoomの前に呼び出された場合にのみ有効であることに注意してください。


[](id:step3)
### 手順3：TRTCの入室
[入室](https://intl.cloud.tencent.com/document/product/647/47645)を参照して現在のユーザーが入室します。正常に入室した後のみ、他のユーザーのオーディオビデオストリームをサブスクリプションできます。


[](id:step4)
### 手順4：オーディオストリームの再生
インターフェイスmuteRemoteAudio("denny"，true)を呼び出すことにより、リモートユーザーdennyの音声をミュートできます。次に、インターフェイスmuteRemoteAudio("denny"，false)を呼び出すことにより、リモートユーザーdennyのミュートを解除できます。

<dx-codeblock>
::: Android  Java
// Mute user with id denny
mCloud.muteRemoteAudio("denny", true);
// Unmute user with id denny
mCloud.muteRemoteAudio("denny", false);
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// Mute user with id denny
[self.trtcCloud muteRemoteAudio:@"denny" mute:YES];
// Unmute user with id denny
[self.trtcCloud muteRemoteAudio:@"denny" mute:YES];
:::
::: Windows  C++
// Mute user with id denny
trtc_cloud_->muteRemoteAudio("denny", true);
// Unmute user with id denny
trtc_cloud_->muteRemoteAudio("denny", false);
:::
</dx-codeblock>


[](id:step5)
### 手順5：ビデオストリームの再生

#### 1. 再生の開始と停止（startRemoteView + stopRemoteView）
インターフェースstartRemoteViewを呼び出すことにより、リモートユーザーのビデオ画面を再生できますが、ユーザーのビデオ画面を運ぶためのレンダリングコントロールとして使用されるビューオブジェクトをSDKに渡す必要があることが前提です。

startRemoteViewの最初のパラメータはリモートユーザーのuserId、2番目のパラメータはリモートユーザーのストリームタイプ、3番目のパラメータは渡す必要のあるviewオブジェクトです。2番目のパラメータstreamType（ストリームタイプ）には、次の3つのオプション値があります。
- TRTCVideoStreamTypeBig：ユーザーのビッグストリーム画面です。通常、ユーザーのカメラ画面を送信するために使用されます。
- TRTCVideoStreamTypeSub：ユーザーのサブストリーム画面です。通常、ユーザーの画面共有の画面を送信するために使用されます。
- TRTCVideoStreamTypeSmall：ビッグストリーム画像を基準にしたユーザーの低解像度の小さな画面です。リモートユーザーが「デュアルチャネルエンコーディング（enableEncSmallVideoStream）」を有効にした場合にのみ、ユーザーの低解像度画面を再生できます。また、同時に、ビッグストリーム画面と低解像度の小さな画面の両方から1つのみ選択できます。

stopRemoteViewインターフェースを呼び出すことにより、1つのリモートユーザーのビデオの再生を停止できます。また、stopAllRemoteViewインターフェースを介してすべてのリモートユーザーのビデオの再生を停止できます。

<dx-codeblock>
::: Android java
// dennyのカメラ画面（「ビッグストリーム」と呼ばれる）を再生します
mCloud.startRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG，cameraView);
// dennyの画面共有画面（「サブストリーム」と呼ばれる）を再生します
mCloud.startRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_SUB，screenView);
// 低解像度画面（ビッグストリームと低解像度の両方から1つのみ選択できる）を再生します
mCloud.startRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_SMALL，cameraView);
// dennyのカメラ画面の再生を停止します
mCloud.stopRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG，cameraView);
// すべてのビデオ画面の再生を停止します
mCloud.stopAllRemoteView();
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// dennyのカメラ画面（「ビッグストリーム」と呼ばれる）を再生します
[self.trtcCloud startRemoteView:@"denny" streamType:TRTCVideoStreamTypeBig view:cameraView];
// dennyの画面共有画面（「サブストリーム」と呼ばれる）を再生します
[self.trtcCloud startRemoteView:@"denny" streamType:TRTCVideoStreamTypeSub view:screenView];
// 低解像度画面（ビッグストリームと低解像度の両方から1つのみ選択できる）を再生します
[self.trtcCloud startRemoteView:@"denny" streamType:TRTCVideoStreamTypeSmall view:cameraView];
// dennyのカメラ画面の再生を停止します
[self.trtcCloud stopRemoteView:@"denny" streamType:TRTCVideoStreamTypeBig view:cameraView];
// すべてのビデオ画面の再生を停止します
[self.trtcCloud stopAllRemoteView];
:::
::: Windows  C++
// dennyのカメラ画面（「ビッグストリーム」と呼ばれる）を再生します
trtc_cloud_->startRemoteView("denny", liteav::TRTCVideoStreamTypeBig, (liteav::TXView)(hWnd));
// dennyの画面共有画面（「サブストリーム」と呼ばれる）を再生します
trtc_cloud_->startRemoteView("denny", liteav::TRTCVideoStreamTypeSub, (liteav::TXView)(hScreenWnd));
// 低解像度画面（ビッグストリームと低解像度の両方から1つのみ選択できる）を再生します
trtc_cloud_->startRemoteView("denny", liteav::TRTCVideoStreamTypeSmall, (liteav::TXView)(hWnd));
// dennyのカメラ画面の再生を停止します
trtc_cloud_->stopRemoteView("denny", liteav::TRTCVideoStreamTypeBig);
// すべてのビデオ画面の再生を停止します
trtc_cloud_->stopAllRemoteView();
:::
</dx-codeblock>

#### 2. 再生パラメータの設定（updateRemoteView + setRemoteRenderParams）

updateRemoteViewインターフェースを呼び出すことにより、再生中にviewオブジェクトを変更できます。これは、ビデオレンダリングコントロールを切り替えるときに役立ちます。
setRemoteRenderParamsを使用すると、画面の塗りつぶしモード、回転角度、イメージモードを設定できます。。
- 塗りつぶしモード：塗りつぶしまたは適応に分かれます。画面は2つのモードで元のアスペクト比を維持できます。その違いは、黒い境界線があるかどうかにあります。
- 回転角度：0度、90度、180度および270度など、4つの回転角度に設定できます。
- イメージモード：つまり、画面の左右のイメージモードです。

<dx-codeblock>
::: Android java
// dennyのビッグストリーム画面を小さなフローティングウィンドウに切り替えます（ミニウィンドウがminiFloatingViewである場合）
mCloud.updateRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG，miniFloatingView);

// リモートユーザーdennyのビッグストリーム画面を塗りつぶしモードに設定し、左右のイメージモードを有効にします
TRTCCloudDef.TRTCRenderParams param = new TRTCCloudDef.TRTCRenderParams();
param.fillMode   = TRTCCloudDef.TRTC_VIDEO_RENDER_MODE_FILL;
param.mirrorType   = TRTCCloudDef.TRTC_VIDEO_MIRROR_TYPE_DISABLE;
mCloud.setRemoteRenderParams("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG，param);
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// dennyのビッグストリーム画面を小さなフローティングウィンドウに切り替えます（ミニウィンドウがminiFloatingViewである場合）
[self.trtcCloud updateRemoteView:miniFloatingView streamType:TRTCVideoStreamTypeBig forUser:@"denny"];
// リモートユーザーdennyのビッグストリーム画面を塗りつぶしモードに設定し、左右のイメージモードを有効にします
TRTCRenderParams *param = [[TRTCRenderParams alloc] init];
param.fillMode     = TRTCVideoFillMode_Fill;
param.mirrorType   = TRTCVideoMirrorTypeDisable;
[self.trtcCloud setRemoteRenderParams:@"denny" streamType:TRTCVideoStreamTypeBig params:param];
:::
::: Windows  C++
// dennyのビッグストリーム画面を他のウィンドウに切り替えます（新しいウィンドウハンドルがnewViewである場合）
trtc_cloud_->updateRemoteView("denny", liteav::TRTCVideoStreamTypeBig, (liteav::TXView)(newView));

// リモートユーザーdennyのビッグストリーム画面を塗りつぶしモードに設定し、左右のイメージモードを有効にします
liteav::TRTCRenderParams param;
param.fillMode = TRTCVideoFillMode_Fill;
param.mirrorType = TRTCVideoMirrorType_Enable;
trtc_cloud_->setRemoteRenderParams("denny", TRTCVideoStreamTypeBig, param);
:::
</dx-codeblock>


[](id:step6)
### 手順6：ルーム内のリモートユーザーのオーディオビデオ状態の検知

手順4と手順5では、リモートユーザーへのオーディオビデオの再生を制御できますが、十分な情報がないと以下を知ることができません：
- 現在のルームのユーザーは誰ですか？
- カメラとマイクがオンになっているかどうか？

この問題を解決するために、SDKからのいくつかのイベントコールバックを監視してください：
**オーディオ状態変化通知（onUserAudioAvailable）**
リモートユーザーがマイクをオンまたはオフにしたときに、onUserAudioAvailable(userId，boolean)を監視することにより、この状態の変化を検知できます。

**ビデオ状態変化通知（onUserVideoAvailable）**
リモートユーザーがビデオ画面をオンまたはオフにしたときに、onUserVideoAvailable(userId，boolean)を監視することにより、この状態の変化を検知できます。
リモートユーザーが画面共有画面をオンまたはオフにしたときに、onUserSubStreamAvailable(userId，boolean)を監視することにより、この状態の変化を検知できます。

**ユーザーの入退室の通知（onRemoteUserEnter/LeaveRoom）**
リモートユーザーが現在のルームに入るとき、onRemoteUserEnterRoom(userId)を介してユーザーのuserIdを検知できます。リモートユーザーが現在のモードを離れるとき、onRemoteUserLeaveRoom(userId, reason)を介してこのユーザーのuserIdと離れる理由を検知できます。
>! 正確にいえば、onRemoteUserEnter/LeaveRoomは、キャスターをロール（role）とするユーザーの入退室通知のみを検知できます。このように設計する理由は、ルーム内のオンライン視聴者が多い場合に、頻繁に入退室する人がいるため、ルーム内のすべてのユーザーが他のユーザーの「シグナルストーム」によって攻撃されることを回避します。

これらのイベントコールバックを使用すると、ルームにいるユーザーと、カメラとマイクをオンにしたかどうかを知ることができます。次のサンプルコードを参照してください。このサンプルコードでは、mCameraUserList、mMicrophoneUserList、およびmUserListを使用してそれぞれ以下を個別に管理します。
- ルーム内のユーザー（正確にいえば、キャスターである）は誰ですか。
- カメラをオンにしたユーザーは誰ですか
- マイクをオンにしたユーザーは誰ですか

<dx-codeblock>
::: Android java
// リモートユーザーのビデオ状態の変化を検知し、カメラをオンにしたユーザーリストを更新します（mCameraUserList）
@Override
public void onUserVideoAvailable(String userId, boolean available) {
    available？mCameraUserList.add(userId) : mCameraUserList.remove(userId);
}

// リモートユーザーのオーディオ状態の変化を検知し、マイクをオンにしたユーザーリストを更新します（mMicrophoneUserList）
@Override
public void onUserAudioAvailable(String userId, boolean available) {
    available？mMicrophoneUserList.add(userId) : mMicrophoneUserList.remove(userId);
}

// リモートユーザーの入室通知を感知し、リモートユーザーリストを更新します（mUserList）
@Override
public void onRemoteUserEnterRoom(String userId) {
    mUserList.add(userId)；
}

// リモートユーザーの退室通知を感知し、リモートユーザーリストを更新します（mUserList）
@Override
public void onRemoteUserLeaveRoom(String userId，int reason) {
    mUserList.remove(userId)；
}
:::
::: iOS&Mac  ObjC
// リモートユーザーのビデオ状態の変化を検知し、カメラをオンにしたユーザーリストを更新します（mCameraUserList）
- (void)onUserVideoAvailable:(NSString *)userId available:(BOOL)available {
    if (available)  {
        [mCameraUserList addObject:userId];
    }else{
        [mCameraUserList removeObject:userId];
    }
}

// リモートユーザーのオーディオ状態の変化を検知し、マイクをオンにしたユーザーリストを更新します（mMicrophoneUserList）
- (void)onUserAudioAvailable:(NSString *)userId available:(BOOL)available{
    if (available)  {
        [mMicrophoneUserList addObject:userId];
    }else{
        [mMicrophoneUserList removeObject:userId];
    }
}

// リモートユーザーの入室通知を感知し、リモートユーザーリストを更新します（mUserList）
- (void)onRemoteUserEnterRoom:(NSString *)userId{
    [mUserList addObject:userId];
}

// リモートユーザーの退室通知を感知し、リモートユーザーリストを更新します（mUserList）
- (void)onRemoteUserLeaveRoom:(NSString *)userId reason:(NSInteger)reason{
    [mUserList removeObject:userId];
}
:::
::: Windows  C++
// リモートユーザーのビデオ状態の変化を検知し、カメラをオンにしたユーザーリストを更新します（mCameraUserList）
void onUserVideoAvailable(const char* user_id, bool available) {
    available ? mCameraUserList.push_back(user_id) : mCameraUserList.remove(user_id);
}

// リモートユーザーのオーディオ状態の変化を検知し、マイクをオンにしたユーザーリストを更新します（mMicrophoneUserList）
void onUserAudioAvailable(const char* user_id, bool available) {
    available ? mMicrophoneUserList.push_back(user_id) : mMicrophoneUserList.remove(user_id);
}

// リモートユーザーの入室通知を感知し、リモートユーザーリストを更新します（mUserList）
void onRemoteUserEnterRoom(const char* user_id) {
    mUserList.push_back(user_id);
}

// リモートユーザーの退室通知を感知し、リモートユーザーリストを更新します（mUserList）
void onRemoteUserLeaveRoom(const char* user_id, int reason) {
    mUserList.remove(user_id);
}
:::
</dx-codeblock>


## 拡張機能ガイド

### 1. 同じ「ミュート」ですが、その違いは何ですか？
サービスニーズの成長につれて、3種類の「ミュート」があり、それらはすべて「ミュート」と呼ばれますが、カウントの原則は完全に異なります。
- **1番目：再生側はオーディオストリームのサブスクリプションを停止します**
muteRemoteAudio("denny", true)関数を呼び出す場合、リモートユーザーdennyの音声を再生したくないことを意味し、このとき、SDKはdennyのオーディオデータストリームのプルを停止します。このモードでは、より多くのトラフィックを節約します。そのとき、dennyの音声をもう一度再生したい場合、SDKはオーディオデータのプルプロセスを再開する必要があるため、「ミュート」から「ミュート解除」への回復速度が遅くなります。

- **2番目：再生ボリュームをゼロに調整します**
サービスシーンでミュート切り替えの応答時間を短縮する必要がある場合、setRemoteAudioVolume("denny", 0)を使用して、リモートユーザーdennyの再生ボリュームをゼロに設定できます。このインターフェースにはネットワーク操作が含まれないため、応答速度が非常に速くなります。

- **3番目：リモートユーザーが自分でマイクをオフにします**
このドキュメントで説明されているすべての操作は、再生側の操作に対するものです。これらの操作の効果は、現在のユーザーにのみ有効です。たとえば、muteRemoteAudio("denny", true)を使用して、リモートユーザーdennyをミュートできますが、ルーム内の他のユーザーは依然として、dennyの音声を聞くことができます。
Dennyを完全に「シャットダウン」する場合、dennyのオーディオリリース動作に影響を与える必要があります。これについては、次のドキュメント[オーディオビデオストリームのリリース](https://intl.cloud.tencent.com/document/product/647/47634)で詳しく紹介します。
