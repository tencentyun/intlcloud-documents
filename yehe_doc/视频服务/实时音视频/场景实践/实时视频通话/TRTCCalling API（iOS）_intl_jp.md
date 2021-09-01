TRTCCalling はTencent CloudのTRTCとIM を組み合わせたサービスで、1v1と多人数のビデオ/音声通話をサポートします。TRTCCalling はTencent Cloudの2つのクローズドソース SDKに依存する1つのオープンソースの Classで、具体的な実装プロセスについては、[Real-Time Video Call（iOS）](https://intl.cloud.tencent.com/document/product/647/36065)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低レイテンシーのオーディオビデオ通話コンポーネントとして使用しています。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047)を使用しシグナリングメッセージを送信、処理しています。


<h2 id="TRTCCalling">TRTCCalling API 概要</h2>

### SDK 基本関数

| API                             | 説明                                             |
| ------------------------------- | ------------------------------------------------ |
| [shareInstance](#shareinstance) | コンポーネントシングルトン。                                       |
| [addDelegate](#adddelegate)     | イベントコールバックを設定します。                                   |
| [login](#login)                 | コンポーネントインターフェースへのログイン、すべての機能を使用するためには、まずログインする必要があります。 |
| [logout](#logout)               | コンポーネントインターフェースからログアウト。ログアウト後にダイヤル操作はできません。         |


### 通話操作に関連するインターフェース関数

| API                     | 説明           |
| ----------------------- | -------------- |
| [call](#call)           | 1対1通話に招待します。 |
| [groupCall](#groupcall) | グループ通話に招待します。 |
| [accept](#accept)       | 現在の通話を受信します。 |
| [reject](#reject)       | 現在の通話を拒否します。 |
| [hangup](#hangup)       | 現在の通話を終了します。 |

### プッシュプルストリームに関連するインターフェース関数

| API                                 | 説明                                         |
| ----------------------------------- | -------------------------------------------- |
| [startRemoteView](#startremoteview) | リモートユーザーのカメラのデータを指定の UIViewにレンダリングします。 |
| [stopRemoteView](#stopremoteview)   | リモートデータのレンダリングを停止します。                           |

### 音声ビデオ制御に関連するインターフェース関数

| API                           | 説明                                   |
| ----------------------------- | -------------------------------------- |
| [openCamera](#opencamera)     | カメラを起動し、指定の UIView にレンダリングします。 |
| [switchCamera](#switchcamera) | 前後カメラを切り替えます。                       |
| [closeCamara](#closecamara)   | カメラを終了します。                           |
| [setMicMute](#setmicmute)     | ローカルオーディオキャプチャをミュートにします。                     |
| [setHandsFree](#sethandsfree) | ハンズフリーを設定します。                             |

<h2 id="TRTCCallingDelegate">TRTCCallingDelegate API 概要</h2>

### 一般的なイベントコールバック

| API                 | 説明       |
| ------------------- | ---------- |
| [onError](#onerror) | エラーのコールバック。 |

### 招待者のコールバック

| API                       | 説明             |
| ------------------------- | ---------------- |
| [onReject](#onreject)     | 通話拒否時のコールバック。   |
| [onNoResp](#onnoresp)     | 相手方の応答がない場合のコールバック。 |
| [onLineBusy](#onlinebusy) | 通話中である場合のコールバック。   |

### 被招待者のコールバック

| API                                   | 説明                 |
| ------------------------------------- | -------------------- |
| [onInvited](#oninvited)               | 通話に招待された場合のコールバック。     |
| [onCallingCancel](#oncallingcancel)   | 現在の通話をキャンセルする場合のコールバック。 |
| [onCallingTimeOut](#oncallingtimeout) | 現在の通話がタイムアウトした場合のコールバック。   |

### 一般的なコールバック

| API                                                          | 説明                       |
| ------------------------------------------------------------ | -------------------------- |
| [onGroupCallInviteeListUpdate](#ongroupcallinviteelistupdate) | グループ通話招待リスト更新のコールバック。     |
| [onUserEnter](#onuserenter)                                  | ユーザーが通話に参加した場合のコールバック。         |
| [onUserLeave](#onuserleave)                                  | ユーザーが通話から退出した場合のコールバック。         |
| [onUserAudioAvailable](#onuseraudioavailable)                | ユーザーがオーディオアップストリームを開始したかどうかのコールバック。 |
| [onUserVideoAvailable](#onuservideoavailable)                | ユーザーがビデオアップストリームを開始したかどうかのコールバック。 |
| [onUserVoiceVolume](#onuservoicevolume)                      | ユーザー通話音量のコールバック。         |
| [onCallEnd](#oncallend)                                      | 通話終了時のコールバック。             |

## SDK 基本関数

### shareInstance

shareInstance は TRTCCalling のコンポーネントシングルトンです。

```Objective-C
/// Singletonオブジェクト
+ (TRTCCalling *)shareInstance;
```


### addDelegate

[TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36065) イベントコールバック、TRTCCallingDelegateを介して [TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36065) の各種ステータス通知を受け取ることができます。

```Objective-C
/// TRTCCallingDelegateを設定してコールバック
/// @param delegate コールバックインスタンス
- (void)addDelegate:(id<TRTCCallingDelegate>)delegate;
```

### login

コンポーネントにログインします。

```Objective-C
typedef void(^CallingActionCallback)(void);
typedef void(^ErrorCallback)(int code, NSString *des);

/// インターフェースにログイン
/// @param sdkAppID SDK ID、Tencent Cloudコンソールで取得することができます
/// @param userID ユーザーID
/// @param userSig ユーザー署名
/// @param success 成功時のコールバック
/// @param failed 失敗時のコールバック
- (void)login:(UInt32)sdkAppID
         user:(NSString *)userID
      userSig:(NSString *)userSig
      success:(CallingActionCallback)success
       failed:(ErrorCallback)failed
NS_SWIFT_NAME(login(sdkAppID:user:userSig:success:failed:));
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                  | 意味                                                         |
| -------- | --------------------- | ------------------------------------------------------------ |
| sdkAppID | UInt32                | TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】> アプリケーション情報でSDKAppIDを表示できます。 |
| user     | String                | 現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。|
| userSig  | String                | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法 ](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
| success  | CallingActionCallback | ログイン成功のコールバック。                                               |
| failed   | ErrorCallback         | ログイン失敗のコールバック。                                               |

### logout

コンポーネントからログアウトします。

```Objective-C
/// インターフェースからログアウト
/// @param success 成功時のコールバック
/// @param failed 失敗時のコールバック
- (void)logout:(CallingActionCallback)success
        failed:(ErrorCallback)failed
NS_SWIFT_NAME(logout(success:failed:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ                  | 意味           |
| ------- | --------------------- | -------------- |
| success | CallingActionCallback | ログアウト成功時のコールバック。 |
| failed  | ErrorCallback         | ログアウト失敗時のコールバック。 |


## 通話操作に関連するインターフェース関数

### call

1対1通話の招待、現在通話中でも引き続き他のユーザーの招待をコールできます。

```Objective-C
/// 1v1通話開始インターフェース
/// @param userID 被招待者ID
/// @param type 通話タイプ：ビデオ/音声
- (void)call:(NSString *)userID
        type:(CallType)type
NS_SWIFT_NAME(call(userID:type:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ     | 意味                  |
| ------ | -------- | --------------------- |
| userID | String   | ユーザー IDを呼び出します。         |
| type   | CallType | 通話タイプ：ビデオ/音声。 |

### groupCall

IM グループが通話に招待すると、被招待者は `onInvited`の コールバックを受け取ります。現在通話中でもこの関数をコールして引き続き他のユーザーを通話に招待することができ、また通話中のユーザーも `onGroupCallInviteeListUpdate` のコールバックを受け取ることができます。

```Objective-C
/// 多人数の通話を開始
/// @param userIDs 被招待者IDリスト
/// @param type 通話タイプ:ビデオ/音声
/// @param groupID グループID、オプションパラメータ
- (void)groupCall:(NSArray *)userIDs
             type:(CallType)type
          groupID:(NSString * _Nullable)groupID
NS_SWIFT_NAME(groupCall(userIDs:type:groupID:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ     | 意味                  |
| ------- | -------- | --------------------- |
| userIDs | [String] | 招待 ID リスト。        |
| type    | CallType | 通話タイプ：ビデオ/音声。 |
| groupID | String   | グループ ID。               |



### accept

現在の通話を受信します。被招待者として `onInvited` のコールバックを受け取った場合は、この関数をコールして通話に応答することができます。

```Objective-C
/// 現在の通話を受信
- (void)accept;
```



### reject

現在の通話を拒否します。被招待者として `onInvited`のコールバックを受け取った場合は、この関数をコールして電話を拒否することができます。

```Objective-C
/// 現在の通話を拒否
- (void)reject;
```



### hangup

現在の通話を終了します。通話中である場合は、この関数をコールして通話を終了できます。

```Objective-C
/// 自発的に通話を終了
- (void)hangup;
```


## プッシュプルストリームに関連するインターフェース関数

### startRemoteView

リモートユーザーのカメラのデータを指定の UIView にレンダリングします。

```Objective-C
///リモートユーザーのビデオレンダリングを開始
- (void)startRemoteView:(NSString *)userId view:(UIView *)view
NS_SWIFT_NAME(startRemoteView(userId:view:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                 |
| ------ | ------ | -------------------- |
| userId | String | リモートユーザー ID。        |
| view   | UIView | ビデオ画面をロードするウィジェット。 |


### stopRemoteView

リモートデータのレンダリングを停止します。

```Objective-C
///リモートユーザーのビデオレンダリングを終了
- (void)stopRemoteView:(NSString *)userId
NS_SWIFT_NAME(stopRemoteView(userId:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味          |
| ------ | ------ | ------------- |
| userId | String | リモートユーザー ID。 |

## 音声ビデオ制御に関連するインターフェース関数

### openCamera

カメラを起動し、指定の UIView にレンダリングします。

```Objective-C
///CCDカメラを起動
- (void)openCamera:(BOOL)frontCamera view:(UIView *)view
NS_SWIFT_NAME(openCamera(frontCamera:view:));
```

パラメータは下表に示すとおりです。

| パラメータ        | タイプ   | 意味                                          |
| ----------- | ------ | --------------------------------------------- |
| frontCamera | Bool   | true：フロントカメラを起動します。false：CCDリアカメラを起動します。 |
| view        | UIView | ビデオ画面をロードするウィジェット。                          |

### switchCamera

前後カメラを切り替えます。

```Objective-C
///カメラの切り替え
- (void)switchCamera:(BOOL)frontCamera;
```

パラメータは下表に示すとおりです。

| パラメータ        | タイプ | 意味                                              |
| ----------- | ---- | ------------------------------------------------- |
| frontCamera | Bool | true：フロントカメラに切り替えます。false：リアカメラに切り替えます。 |

### closeCamara

カメラを終了します。

```Objective-C
///カメラを終了
- (void)closeCamara;
```

### setMicMute

ローカルオーディオキャプチャをミュートにします。

```Objective-C
///ミュート操作
- (void)setMicMute:(BOOL)isMute;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ | 意味                                  |
| ------ | ---- | ------------------------------------- |
| isMute | Bool | true：マイクの終了、false：マイクの起動。 |

### setHandsFree

ハンズフリーを起動します。

```Objective-C
///ハンズフリー操作
- (void)setHandsFree:(BOOL)isHandsFree;
```

パラメータは下表に示すとおりです。

| パラメータ        | タイプ | 意味                              |
| ----------- | ---- | --------------------------------- |
| isHandsFree | Bool | true：ハンズフリーを起動、false：ハンズフリーを終了。 |

## TRTCCallingDelegateイベントコールバック

## 一般的なイベントコールバック

### onError

エラーのコールバック。

>?SDK リカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

```Objective-C
/// sdk内にエラー発生 | sdk error
/// - Parameters:
///   - code: エラーコード
///   - msg: エラーメッセージ
-(void)onError:(int)code msg:(NSString * _Nullable)msg
NS_SWIFT_NAME(onError(code:msg:));

```

パラメータは下表に示すとおりです。

| パラメータ | タイプ    | 意味       |
| ---- | ------- | ---------- |
| code | Int     | エラーコード。   |
| msg  | String? | エラー情報。 |


## 招待者のコールバック

### onReject

通話拒否時のコールバック。

```Objective-C
/// 通話拒否時のコールバック-招待者のみが通知を受け取り、他のユーザーは onUserEnterを使用する必要があります |
/// reject callback only worked for Sponsor, others should use onUserEnter)
/// - Parameter uid: userid
-(void)onReject:(NSString *)uid
NS_SWIFT_NAME(onReject(uid:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ   | 意味             |
| ---- | ------ | --------------- |
| uid  | String | 拒否したユーザーの ID。 |

### onNoResp

相手方が応答しない場合のコールバック。

```Objective-C
/// 応答しない場合のコールバック-招待者のみが通知を受け取り、他のユーザーは onUserEnterを使用する必要があります|
/// no response callback only worked for Sponsor, others should use onUserEnter)
/// - Parameter uid: userid
-(void)onNoResp:(NSString *)uid
NS_SWIFT_NAME(onNoResp(uid:));

```

パラメータは下表に示すとおりです。

| パラメータ | タイプ   | 意味               |
| ---- | ------ | ----------------- |
| uid  | String | 応答しないユーザーの ID。 |

### onLineBusy

通話中である場合のコールバック。

```Objective-C
/// 通話中である場合のコールバック-招待者のみが通知を受け取り、他のユーザーは onUserEnterを使用する必要があります |
/// linebusy callback only worked for Sponsor, others should use onUserEnter
/// - Parameter uid: userid
-(void)onLineBusy:(NSString *)uid
NS_SWIFT_NAME(onLineBusy(uid:));

```

パラメータは下表に示すとおりです。

| パラメータ | タイプ   | 意味             |
| ---- | ------ | --------------- |
| uid  | String | 通話中であるユーザーの ID。 |

## 被招待者のコールバック

### onInvited

通話に招待された場合のコールバック。

```Objective-C
/// 通話に招待された場合のコールバック | invitee callback
/// - Parameter userIds: 招待リスト (invited list)
-(void)onInvited:(NSString *)sponsor
         userIds:(NSArray<NSString *> *)userIds
     isFromGroup:(BOOL)isFromGroup
        callType:(CallType)callType
NS_SWIFT_NAME(onInvited(sponsor:userIds:isFromGroup:callType:));
```

パラメータは下表に示すとおりです。

| パラメータ        | タイプ     | 意味                   |
| ----------- | -------- | --------------------- |
| sponsor     | String   | 発信者のID。         |
| userIds     | [String] | 招待 ID リスト。        |
| isFromGroup | Bool     | 多人数の通話への招待かどうか。    |
| callType    | CallType | 通話タイプ：音声/ビデオ。 |

### onCallingCancel

現在の通話がキャンセルされた場合のコールバック。被招待者がリクエストを処理しない場合、招待者がキャンセル後にこのコールバックを受け取ります。

```Objective-C
/// 現在の通話がキャンセルされた場合のコールバック | current call had been canceled callback
-(void)onCallingCancel:(NSString *)uid
NS_SWIFT_NAME(onCallingCancel(uid:));
```



### onCallingTimeOut

現在の通話がタイムアウトした場合のコールバック。

```Objective-C
/// 通話がタイムアウトした場合のコールバック | timeout callback
-(void)onCallingTimeOut;
```

## 一般的なコールバック

### onGroupCallInviteeListUpdate

グループ通話招待リスト更新のコールバック。

```Objective-C
/// グループ通話招待リスト更新のコールバック | update current inviteeList in group calling
/// - Parameter userIds: 招待リスト | inviteeList
-(void)onGroupCallInviteeListUpdate:(NSArray *)userIds
NS_SWIFT_NAME(onGroupCallInviteeListUpdate(userIds:));
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ     | 意味            |
| ------- | -------- | -------------- |
| userIds | [String] | 招待 ID リスト。 |

### onUserEnter

ユーザーが通話に参加した場合のコールバック。

```Objective-C
/// 通話に参加する場合のコールバック | user enter room callback
/// - Parameter uid: userid
-(void)onUserEnter:(NSString *)uid
NS_SWIFT_NAME(onUserEnter(uid:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ   | 意味              |
| ---- | ------ | ----------------- |
| uid  | String | 通話に参加するユーザー ID。 |

### onUserLeave

ユーザーが通話から退出した場合のコールバック。

```Objective-C
/// 通話から退出する場合のコールバック | user leave room callback
/// - Parameter uid: userid
-(void)onUserLeave:(NSString *)uid
NS_SWIFT_NAME(onUserLeave(uid:));
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ   | 意味               |
| ---- | ------ | ----------------- |
| uid  | String | 通話から退出するユーザー ID。 |

### onUserAudioAvailable

ユーザーがオーディオアップストリームを開始したかどうかのコールバック。

```Objective-C
/// ユーザーが音声アップリンクを開始したかどうかのコールバック | is user audio available callback
/// - Parameters:
///   - uid: ユーザーID | userID
///   - available: 有効か | available
-(void)onUserAudioAvailable:(NSString *)uid available:(BOOL)available
NS_SWIFT_NAME(onUserAudioAvailable(uid:available:));

```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味                |
| --------- | ------ | ------------------ |
| uid       | String | 通話するユーザー ID。      |
| available | Bool   | ユーザーの音声が使用可能かどうか。 |

### onUserVideoAvailable

ユーザーがビデオアップストリームを開始したかどうかのコールバック。通知を受け取った後、ユーザーは`startRemoteView`をコールしてリモートビデオを レンダリングすることができます。

```Objective-C
/// ユーザーがビデオアップリンクを開始したかどうかのコールバック | is user video available callback
/// - Parameters:
///   - uid: ユーザーID | userID
///   - available: 有効か | available
-(void)onUserVideoAvailable:(NSString *)uid available:(BOOL)available
NS_SWIFT_NAME(onUserVideoAvailable(uid:available:));

```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ   | 意味                |
| --------- | ------ | ------------------ |
| uid       | String | 通話するユーザー ID。      |
| available | Bool   | ユーザービデオが使用可能かどうか。 |


### onUserVoiceVolume

ユーザーの通話音量のコールバック。

```Objective-C
/// ユーザーの音量のコールバック
/// - Parameter uid: ユーザーID | userID
/// - Parameter volume: 話し手の音量、 数値範囲0 - 100
-(void)onUserVoiceVolume:(NSString *)uid volume:(UInt32)volume
NS_SWIFT_NAME(onUserVoiceVolume(uid:volume:));
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                             |
| ------ | ------ | ------------------------------- |
| uid    | String | 通話するユーザー ID。                   |
| volume | UInt32 | 通話者の音量、数値範囲0 - 100。 |

### onCallEnd

通話終了時のコールバック。

```Objective-C
/// 通話終了 | end callback
-(void)onCallEnd;
```
