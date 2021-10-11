TRTCMeetingは、Tencent CloudのTRTCおよびIMサービスを基に組み合わせたコンポーネントで、以下の機能をサポートしています。
- キャスターがミーティングルームを作成し、参加者はルームナンバーを入力した後にミーティングに参加します。
- 参加者の間で画面共有を行います。
- 各種のテキストメッセージとカスタムメッセージの送信をサポートします。

TRTCMeetingは、1つのオープンソースのClassであり、Tencent Cloudの2つのクローズドソースのSDKに依存しています。具体的な実現プロセスは、[多人数ビデオミーティング(Android)](https://intl.cloud.tencent.com/document/product/647/37283)をご参照ください。
- TRTC SDK： [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) を低遅延のビデオミーティングのコンポーネントとして使用します。
- IM SDK：[IM SDK](https://intl.cloud.tencent.com/document/product/1047)のMeetingRoomを利用して、ミーティング中のチャットルームの機能を実現します。


<h2 id="TRTCMeeting">TRTCMeeting API概要</h2>

### SDK基本関数

| API | 説明 |
|-----|-----|
| [sharedInstance](#sharedinstance)               | シングルトンオブジェクトを取得します。                                       |
| [destroySharedInstance](#destroysharedinstance) | シングルトンオブジェクトを破棄します。 |
| [setDelegate](#setdelegate) | イベントコールバックを設定します。|
| [setDelegateHandler](#setdelegatehandler) | イベントコールバックが設定されているスレッドです。 |
| [login](#login) | ログイン。|
| [logout](#logout) | ログアウト。|
| [setSelfProfile](#setselfprofile) | 個人情報を修正します。|

### ミーティングルームに関するインターフェース関数

| API | 説明 |
|-----|-----|
| [createMeeting](#createmeeting) | ルームの作成（キャスターが呼び出し）。|
| [destroyMeeting](#destroymeeting) | ルームの破棄（キャスターが呼び出し）。|
| [enterMeeting](#entermeeting) | 入室（参加者が呼び出し）。|
| [leaveMeeting](#leavemeeting) | 退室（参加者が呼び出し）。|

### リモートユーザーに関するインターフェース
| API | 説明 |
|-----|-----|
| [getUserInfoList](#getuserinfolist) | ルーム内の全メンバーのリストを取得します。enterMeeting()の成功後に呼び出しが有効となります。|
| [getUserInfo](#getuserinfo) | ルーム内の指定メンバーの詳細情報を取得します。enterMeeting()の成功後に呼び出しが有効となります。|
| [startRemoteView](#startremoteview) | 指定メンバーのリモートビデオ画面を再生します。|
| [stopRemoteView](#stopremoteview) | リモートビデオ画面の再生を停止します。 |
| [setRemoteViewFillMode](#setremoteviewfillmode) | ユーザーIDと設定に基づくリモート画像のレンダリングモード。 |
| [setRemoteViewRotation](#setremoteviewrotation) | リモート画像の時計回りの回転角度を設定します。 |
| [muteRemoteAudio](#muteremoteaudio) | リモートの指定参加者の音声をミュートにします。 |
| [muteRemoteVideoStream](#muteremotevideostream) | 指定参加者のビデオストリームを非表示にします。 |

### ローカルのビデオ操作インターフェース

| API | 説明 |
|-----|-----|
| [startCameraPreview](#startcamerapreview) | ローカルビデオのプレビュー画面を立ち上げます。|
| [stopCameraPreview](#stopcamerapreview) | ローカルのビデオキャプチャおよびプレビューを停止します。|
| [switchCamera](#switchcamera) | フロント/リアカメラを切り替えます。 |
| [setVideoResolution](#setvideoresolution) | 解像度の設定。 |
| [setVideoFps](#setvideofps) | フレームレートの設定。|
| [setVideoBitrate](#setvideobitrate) | ビットレートの設定。|
| [setLocalViewMirror](#setlocalviewmirror) | ローカル画面のミラーモードのプレビューを設定します。|

### ローカルのオーディオ操作インターフェース

| API | 説明 |
|-----|-----|
| [startMicrophone](#startmicrophone) | マイクの集音開始。|
| [stopMicrophone](#stopmicrophone) | マイクの集音停止。|
| [setAudioQuality](#setaudioquality) | 音質の設定。|
| [muteLocalAudio](#mutelocalaudio) | ローカル音声のミュート起動。|
| [setSpeaker](#setspeaker) | スピーカーの起動設定 。|
| [setAudioCaptureVolume](#setaudiocapturevolume) | マイクの集音音量設定。|
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | 再生音量の設定。|
| [startFileDumping](#startfiledumping) | 録音の開始。|
| [stopFileDumping](#stopfiledumping) | 録音の停止。|
| [enableAudioEvaluation](#enableaudioevaluation) | 音量レベルリマインダを有効にします。|

### スクリーンキャプチャのインターフェース

| API | 説明 |
|-----|-----|
| [startScreenCapture](#startscreencapture) | 画面共有を開始。 |
| [stopScreenCapture](#stopscreencapture) | 画面キャプチャの停止。|
| [pauseScreenCapture](#pausescreencapture) | 画面共有の一時停止。|
| [resumeScreenCapture](#resumescreencapture) | 画面共有のリカバー。|

### 美顔フィルタに関するインターフェース関数

| API | 説明 |
|-----|-----|
| [getBeautyManager](#getbeautymanager) | 美顔管理オブジェクト[TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager)を取得します。|

### 共有に関するインターフェース

| API | 説明 |
|-----|-----|
| [getLiveBroadcastingURL](#getlivebroadcastingurl) | CDN共有のリンク先を取得します。|

### メッセージ送信関連インターフェース関数

| API | 説明 |
|-----|-----|
| [sendRoomTextMsg](#sendroomtextmsg) | ルーム内でのテキストメッセージのブロードキャストでは、通常、チャットに使用します。|
| [sendRoomCustomMsg](#sendroomcustommsg) | カスタマイズ（シグナリング）メッセージを送信します。|


<h2 id="TRTCMeetingDelegate">TRTCMeetingDelegate API概要</h2>

### 一般的なイベントコールバック

| API | 説明 |
|-----|-----|
| [onError](#onerror) | エラーのコールバック。|

### ミーティングルームのイベントコールバック

| API | 説明 |
|-----|-----|
| [onRoomDestroy](#onroomdestroy) | ミーティングルームが破棄された時のコールバック。|
| [onNetworkQuality](#onnetworkquality)     | ネットワーク状態のコールバック。   |
| [onUserVolumeUpdate](#onuservolumeupdate) | ユーザー通話音量のコールバック。|

### 参加者入退室のイベントコールバック

| API | 説明 |
|-----|-----|
| [onUserEnterRoom](#onuserenterroom) | 新しい参加者の入室の通知を受信します。|
| [onUserLeaveRoom](#onuserleaveroom) | 参加者の退室の通知を受信します。|

### 参加者の音声・ビデオのイベントコールバック

| API | 説明 |
|-----|-----|
| [onUserVideoAvailable](#onuservideoavailable) | 参加者のカメラ・オン/オフの通知。|
| [onUserAudioAvailable](#onuseraudioavailable) | 参加者のマイク・オン/オフの通知。|


### メッセージイベントのコールバック

| API | 説明 |
|-----|-----|
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | テキストメッセージの受信。|
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | カスタムメッセージの受信。|

### スクリーンキャプチャのイベントコールバック

| API                                                 | 説明          |
| --------------------------------------------------- | -------------- |
| [onScreenCaptureStarted](#onscreencapturestarted) | スクリーンキャプチャ開始の通知。 |
| [onScreenCapturePaused](#onscreencapturepaused)   | スクリーンキャプチャ一時停止のコールバック。 |
| [onScreenCaptureResumed](#onscreencaptureresumed) | スクリーンキャプチャ再開のコールバック。 |
| [onScreenCaptureStoped](#onscreencapturestoped)   | スクリーンキャプチャ停止のコールバック。 |

## SDK基本関数

[](id:sharedInstance)
### sharedInstance

[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37283)シングルトンオブジェクトを取得します。
```java
 public static synchronized TRTCMeeting sharedInstance(Context context);
```
パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| context | Context | Androidコンテキスト。内部ではApplicationContextに変換してシステムAPIの呼び出しに使用します |



### destroySharedInstance

[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37283)シングルトンオブジェクトを破棄します。
>?インスタンスを破棄すると、外部キャッシュのTRTCMeeting インスタンスは再利用できなくなります。あらためて[sharedInstance](#sharedInstance)を呼び出し、新しいインスタンスを取得する必要があります。

```java
public static void destroySharedInstance();
```

### setDelegate

[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37283)のイベントコールバック。TRTCMeetingDelegate を介して、[TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37283) の各種ステータスの通知を取得できます。
```java
public abstract void setDelegate(TRTCMeetingDelegate delegate);
```

>?setDelegateはTRTCMeetingのプロキシコールバックです。   

### setDelegateHandler

イベントコールバックが配置されているスレッドを設定します。
```java
public abstract void setDelegateHandler(Handler handler);
```
パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| handler | Handler | TRTCMeetingの中の各種状態の通知のコールバックは、このhandlerによって通知されます。setDelegateと混用しないでください。 |

### login

ログイン。
```java
public abstract void login(int sdkAppId,
	 String userId, String userSig,
	 TRTCMeetingCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| sdkAppId | int |  TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】> アプリケーション情報の中でSDKAppIDを確認できます。 |
| user     | String | 現在のユーザーID、文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。|
| userSig  | String         |Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
| callback | ActionCallback | ログインのコールバック。成功時にcodeは0になります。 |


### logout

ログアウト。
```java
public abstract void logout(TRTCMeetingCallback.ActionCallback callback);
```
パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| callback | ActionCallback | ログアウトのコールバック。成功時にcodeは0になります。 |

   

### setSelfProfile

個人情報の修正。
```java
public abstract void setSelfProfile(String userName, String avatarURL, TRTCMeetingCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味       |
|-----|-----|-----|
| userName  | String         | ニックネーム。                              |
| avatarURL | String         | プロフィール画像のアドレス。                          |
| callback | ActionCallback | 個人情報設定のコールバック。成功時のcodeは0です。 |

   


## ミーティングルームに関するインターフェース関数
### createMeeting

ミーティングの作成（キャスターの呼び出し）。
```java
public abstract void createMeeting(int roomId, TRTCMeetingCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| roomId | int | ミーティングルームIDは、ご自身でアサインし、一元管理する必要があります。 |
| callback | ActionCallback | ルームの作成結果のコールバック。成功時にcodeは0になります。 |

キャスターの通常の呼び出しフローは以下のとおりです。 
1. 【キャスター】`createMeeting()`を呼び出し、ミーティングを作成します。ミーティングルーム作成の成功の有無が、 ActionCallbackでキャスターに通知されます。
2. 【キャスター】`startCameraPreview()`を呼び出し、カメラのプレビューを起動します。この時美顔パラメータを調整できます。 
3. 【キャスター】`startMicrophone()`を呼び出し、マイクキャプチャを起動します。

   

### destroyMeeting

ミーティングルームを破棄します（キャスターが呼び出し）。キャスターは、ミーティング作成後、この関数を呼び出してミーティングを破棄できます。
```java
public abstract void destroyMeeting(int roomId, TRTCMeetingCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| roomId | int | ミーティングルームIDは、ご自身でアサインし、一元管理する必要があります。 |
| callback | ActionCallback | ルームの破棄結果のコールバック。成功時にcodeは0になります。 |


### enterMeeting

ミーティングに参加します（参加者が呼び出し）。
```java
public abstract void enterMeeting(int roomId, TRTCMeetingCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| roomId | int | ミーティングルームID。 |
| callback | ActionCallback | 入室結果のコールバック。成功時にcodeは0になります。 |


参加者がミーティングに参加する通常の呼び出しフローは以下のとおりです。 
1. 【参加者】`enterMeeting`を呼び出し、roomIdを渡すと、ミーティングルームに参加できます。
2. 【参加者】`startCameraPreview()`を呼び出して、カメラのプレビューを起動し、`startMicrophone()`を呼び出し、マイクキャプチャを起動します。
3. 【参加者】`onUserVideoAvailable`のイベントを受信します。`startRemoteView(userId)`を呼び出し、メンバーのuserIdを渡して再生を開始します
   

### leaveMeeting

ミーティングから退出します（参加者が呼び出し）。
```java
public abstract void leaveMeeting(TRTCMeetingCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| callback | ActionCallback | 退室結果のコールバック。成功時にcodeは0になります。 |


## リモートユーザーに関するインターフェース

### getUserInfoList

ルーム内の全メンバーのリストを取得します。enterMeeting()の成功後に呼び出しが有効となります。


```java
public abstract void getUserInfoList(TRTCMeetingCallback.UserListCallback userListCallback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userListCallback | UserListCallback | ユーザーの詳細情報のコールバック。 |


### getUserInfo

ルーム内の指定メンバーの詳細情報を取得します。enterMeeting()の成功後に呼び出しが有効となります。
```java
public abstract void getUserInfo(String userId, TRTCMeetingCallback.UserListCallback userListCallback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | ユーザーID。|
| userListCallback | UserListCallback | ユーザーの詳細情報のコールバック。 |


### startRemoteView

指定メンバーのリモートビデオ画面を再生します。`onUserVideoAvailable()`がtrueのコールバックの時、このインターフェースを呼び出します。
```java
public abstract void startRemoteView(String userId, TXCloudVideoView view, final TRTCMeetingCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | 再生が必要なユーザーのID。|
| view | TXCloudVideoView | ビデオ画像をロードするviewウィジェット。|
| callback | ActionCallback | 操作コールバック。|

### stopRemoteView

リモートビデオ画面の再生を停止します。`onUserVideoAvailable()`がfalseのコールバックの時、このインターフェースを呼び出します。
```java
public abstract void stopRemoteView(String userId, final TRTCMeetingCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | 再生停止が必要なユーザーのID|
| callback | ActionCallback | 操作コールバック。|

### setRemoteViewFillMode

ユーザーidと設定に基づくリモート画像のレンダリングモード。
```java
public abstract void setRemoteViewFillMode(String userId, int fillMode);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | ユーザーID。|
| fillMode | int  | FILLまたはFITモード。デフォルト値：フィル（FILL）。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f)をご参照ください。|



### setRemoteViewRotation

リモート画像の時計回りの回転角度を設定します。
```java
public abstract void setRemoteViewRotation(String userId, int rotation);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                            |
|-----|-----|-----|
| userId | String | ユーザーID。 |
| rotation | int  | 時計回りの回転角度。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a87fd1307871debc7c051de4878eb6d69)をご参照ください。 |



### muteRemoteAudio

リモートの音声をミュートにします。
```java
public abstract void muteRemoteAudio(String userId, boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                            |
|-----|-----|-----|
| userId | String | ユーザーID。 |
| mute | boolean | true：ミュート起動、false：ミュート停止。|

   

### muteRemoteVideoStream

指定参加者のビデオストリームを非表示にします。
```java
public abstract void muteRemoteVideoStream(String userId, boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                            |
|-----|-----|-----|
| userId | String | ユーザーID。 |
| mute | boolean | true：非表示；false：非表示の解除。|


​      

## ローカルのビデオ操作インターフェース
### startCameraPreview

ローカルビデオのプレビュー画面を立ち上げます。
```java
public abstract void startCameraPreview(boolean isFront, TXCloudVideoView view);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| isFront | boolean | true：フロントカメラ；false：リアカメラ。 |
| view | TXCloudVideoView | ビデオ画像をロードするウィジェット。 |

   

### stopCameraPreview

ローカルのビデオキャプチャおよびプレビューを停止します。
```java
public abstract void stopCameraPreview();
```

   

### switchCamera

フロント/リアカメラを切り替えます。
```java
public abstract void switchCamera(boolean isFront);
```
パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| isFront | boolean | 前後カメラを切り替えます。true：フロントカメラ；false：リアカメラ。 |


### setVideoResolution

解像度の設定

```java
public abstract void setVideoResolution(int resolution);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| resolution | int | ビデオの解像度。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#aa3b72c532f3ffdf64c6aacab26be5f87)をご参照ください。 |



### setVideoFps

フレームレートの設定
```java
public abstract void setVideoFps(int fps);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| fps | int | ビデオキャプチャのフレームレート。 |

>?【推奨する値】 15fpsまたは20fps。5fps以下ではラグ感が顕著。10fps以下では軽微なラグ感があります。20fps以上は高すぎて浪費になります（映画のフレームレートは24fps）。


### setVideoBitrate

ビットレートの設定
```java
public abstract void setVideoBitrate(int bitrate);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| bitrate | int | ビットレート。SDKは、目標ビットレートに応じてエンコードを行い、ネットワークの状態が良くない場合のみ、ビデオビットレートを動的に引き下げます。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html)をご参照ください。 |

>? 【推奨する値】本TRTCVideoResolutionの各クラスに注記する最適ビットレートをご参照ください。これをもとにより高いレートに適宜調整することも可能です。例えば、TRTC_VIDEO_RESOLUTION_1280_720に対応する目標ビットレートが1200kbpsであるならば、設定を1500kbpsにし、より鮮明な画像を得ることができます。



### setLocalViewMirror

ローカル画面のミラーモードのプレビューを設定します
```java
public abstract void setLocalViewMirror(int type);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| type | int | イメージモード。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa353b5cf5662c43252eb8e5132f041c1)をご参照ください。 |

## ローカルのオーディオ操作インターフェース

### startMicrophone

マイクの集音開始
```java
public abstract void startMicrophone();
```

### stopMicrophone

マイクの集音停止
```java
public abstract void stopMicrophone();
```

### setAudioQuality

音質の設定
```java
public abstract void setAudioQuality(int quality);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| quality | int | 音質。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)をご参照ください。 |


### muteLocalAudio

ローカルのオーディオのミュート/ミュート取り消し
```java
public abstract void muteLocalAudio(boolean mute);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| mute | boolean | ミュート/ミュート取り消し。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)をご参照ください。 |



### setSpeaker

スピーカーの起動設定
```java
public abstract void setSpeaker(boolean useSpeaker);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| useSpeaker | boolean | true:スピーカー false:ヘッドホン |



### setAudioCaptureVolume

マイクの集音音量設定
```java
public abstract void setAudioCaptureVolume(int volume);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| volume | int | 集音音量、0-100、 デフォルト100。 |


### setAudioPlayoutVolume

再生音量の設定
```java
public abstract void setAudioPlayoutVolume(int volume);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| volume | int | 再生音量、0-100、 デフォルト100。 |


### startFileDumping

録音の開始
```java
public abstract void startFileDumping(TRTCCloudDef.TRTCAudioRecordingParams trtcAudioRecordingParams);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| trtcAudioRecordingParams | TRTCCloudDef.TRTCAudioRecordingParams | 録音パラメータ。詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams)をご参照ください。 |

>? この方法で呼び出した後、 SDKは通話プロセスの中のすべての音声（ローカル音声、リモート音声、BGMなど）を1つのファイルにレコーディングします。ルームに参加しているか否かにかかわらず、このインターフェースを呼び出せば有効となります。exitMeetingを呼び出した時に録音中であれば、録音は自動的に停止します。

### stopFileDumping

録音の停止
```java
public abstract void stopFileDumping();
```

### enableAudioEvaluation

音量レベルリマインダを有効にします
```java
public abstract void enableAudioEvaluation(boolean enable);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| enable | boolean |  true オン false オフ。 |

>? 有効化すると、onUserVolumeUpdateの中でSDKの音量のボリュームに対する評価を取得できます。

## スクリーンキャプチャのインターフェース
### startScreenCapture

画面共有を開始。
```java
public abstract void startScreenCapture(TRTCCloudDef.TRTCVideoEncParam encParams, TRTCCloudDef.TRTCScreenShareParams screenShareParams);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| encParams | TRTCCloudDef.TRTCVideoEncParam | 画面共有時のエンコードパラメータを設定します。上記の推奨設定を採用することをお勧めします。encParamsにnullを指定した場合、startScreenCaptureを呼び出す前のエンコードパラメータ設定が使用されます。 |
| screenShareParams | TRTCCloudDef.TRTCScreenShareParams | 画面共有の特殊なレイアウト設定については、その中のfloatingViewの設定を推奨します。一方で、Appがシステムから強制排除されるのを回避でき、もう一方で、ユーザーのプライバシー保護にも役立ちます。 |

>? 詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)をご参照ください。 |

### stopScreenCapture

画面キャプチャの停止。
```java
public abstract void stopScreenCapture();
```

### pauseScreenCapture

画面共有の一時停止。
```java
public abstract void pauseScreenCapture();
```

### resumeScreenCapture

画面共有のリカバー。
```java
public abstract void resumeScreenCapture();
```

## 共有のインターフェース
### getLiveBroadcastingURL

CDN共有のリンク先を取得します。
```java
public abstract String getLiveBroadcastingURL();
```

戻り値は下表に示すとおりです。

| 戻り値 | タイプ | 意味 |
|-----|-----|-----|
| url  | String  | CDN共有のリンク先。 |

## 美顔フィルタに関するインターフェース関数
### getBeautyManager

美顔管理オブジェクト [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager)を取得します。
```java
public abstract TXBeautyManager getBeautyManager();
```

美顔管理では、次の機能を使用できます。
- 「美顔のスタイル」、「美白」、「肌色補正（血色・つや感）」、「デカ眼」、「顔痩せ」、「V顔」、「下あご」、「面長補正」、「小鼻」、「キラキラ目」、「白い歯」、「目の弛み除去」、「シワ除去」、「ほうれい線除去」などの美容効果を設定します。
- 「髪の生え際」、「眼と眼の距離」、「眼角度」、「唇の形」、「鼻翼」、「鼻の位置」、「唇の厚さ」、「顔の形」を調整します。
- 人の顔のスタンプ（素材）等のダイナミック効果を設定します。
- メイクアップを追加します。
- ジェスチャー認識を行います。


## メッセージ送信関連インターフェース関数
### sendRoomTextMsg

ルーム内でテキストメッセージを発信します。
```java
public abstract void sendRoomTextMsg(String message, TRTCMeetingCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味           |
|-----|-----|-----|
| message | String | テキストメッセージ。 |
| callback | ActionCallback | 送信結果のコールバック。|

   

### sendRoomCustomMsg

カスタマイズしたテキストメッセージを送信します。
```java
public abstract void sendRoomCustomMsg(String cmd, String message, TRTCMeetingCallback.ActionCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| cmd      | String         | コマンドワードは、開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。 |
| message | String | テキストメッセージ。 |
| callback | ActionCallback | 送信結果のコールバック。|

   

## TRTCMeetingDelegateイベントコールバック

## 一般的なイベントコールバック
### onError

エラーのコールバック。
>? SDKのリカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

```java
void onError(int code, String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ   | 意味       |
|-----|-----|-----|
| code   | int    | エラーコード。   |
| message | String | エラー情報。 |



## ルームイベントのコールバック
### onRoomDestroy

ルームが破棄された時のコールバック。キャスターがルームを退出する時、ルーム内の全ユーザーがこの通知を受信します。
```java
void onRoomDestroy(String roomId);
```

パラメータは下表に示すとおりです。

|パラメータ   | タイプ   | 意味      |
|-----|-----|-----|
| roomId | String | ルームID。 |

### onNetworkQuality

ネットワーク状態のコールバック。
```java
 void onNetworkQuality(TRTCCloudDef.TRTCQuality localQuality, List<TRTCCloudDef.TRTCQuality> remoteQuality);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| localQuality | TRTCCloudDef.TRTCQuality | アップストリームネットワークの品質。 |
| remoteQuality | List&lt;TRTCCloudDef.TRTCQuality&gt; | ダウンストリームのネットワーク品質。 |

>? 詳細については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#aba07d4191391dadef900422521f34e5b)をご参照ください。 |


### onUserVolumeUpdate

音量レベルリマインダを有効にして、各メンバーの音量を通知します
```java
void onUserVolumeUpdate(String userId, int volume);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                            |
|-----|-----|-----|
| userId | String | ユーザーID。 |
| volume | int | 音量の大きさ。値：0～100。 |



## 参加者入退室のイベントコールバック
### onUserEnterRoom

新しい参加者の入室の通知を受信します。
```java
void onUserEnterRoom(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | ルームの新たな参加者のユーザーID。 |


### onUserLeaveRoom

参加者の退室の通知を受信します。
```java
void onUserLeaveRoom(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| userId | String | 退室する参加者のユーザーID |


## 参加者の音声・ビデオのイベントコールバック
### onUserVideoAvailable

参加者のカメラ・オン/オフの通知。
```java
void onUserVideoAvailable(String userId, boolean available);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                            |
|-----|-----|-----|
| userId | String | ユーザーID。 |
| available | boolean | true：ユーザーがカメラをオンにします。false：ユーザーがカメラをオフにします。 |

   

### onUserAudioAvailable

参加者のマイク・オン/オフの通知。
```java
void onUserAudioAvailable(String userId, boolean available);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                            |
|-----|-----|-----|
| userId | String | ユーザーID。 |
| available | boolean | true：ユーザーがマイクをオンにします。false：ユーザーがマイクをオフにします。 |

   

## メッセージイベントのコールバック
### onRecvRoomTextMsg

テキストメッセージの受信。
```java
void onRecvRoomTextMsg(String message, TRTCMeetingDef.UserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| message | String | テキストメッセージ。|
| userInfo | TRTCMeetingDef.UserInfo | 送信者のユーザー情報。|

   

### onRecvRoomCustomMsg

カスタムメッセージの受信。
```java
void onRecvRoomCustomMsg(String cmd, String message, TRTCMeetingDef.UserInfo userInfo);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ | 意味 |
|-----|-----|-----|
| cmd | String | コマンドワード。開発者がカスタマイズします。主にさまざまなメッセージタイプを区別するために使用されます。|
| message | String | テキストメッセージ。|
| userInfo | TRTCMeetingDef.UserInfo | 送信者のユーザー情報。 |


## スクリーンキャプチャのイベントコールバック

### onScreenCaptureStarted

スクリーンキャプチャ開始の通知。

```java
void onScreenCaptureStarted();
```

### onScreenCapturePaused

スクリーンキャプチャ一時停止の通知。

```java
void onScreenCapturePaused();
```

### onScreenCaptureResumed

スクリーンキャプチャ再開の通知。

```java
void onScreenCaptureResumed();
```

### onScreenCaptureStoped

スクリーンキャプチャ停止の通知。

```java
void onScreenCaptureStopped(int reason);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                               |
| ------ | ---- | -------------------------------------------------- |
| reason | int  | 停止の理由。0：ユーザーの自発的な停止。1：その他アプリケーションに占有されたことによる停止。 |





