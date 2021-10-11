TRTCCalling はTencent CloudのTRTCとIM を組み合わせたサービスで、1v1と多人数のビデオ通話をサポートします。TRTCCallingはTencent Cloudの2つのクローズドソースSDKに依存する1つのオープンソースのClassです。具体的な実装プロセスについては、[Real-Time Video Call（Android）](https://intl.cloud.tencent.com/document/product/647/36066)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のオーディオビデオ通話コンポーネントとして使用します。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047)をシグナリング情報の送信と処理に使用します。


<h2 id="TRTCCalling">TRTCCalling API概要</h2>

### SDK基本関数

| API                                             | 説明                                                         |
| ----------------------------------------------- | ------------------------------------------------ |
| [sharedInstance](#sharedinstance)               | コンポーネントシングルトン。                                       |
| [destroySharedInstance](#destroysharedinstance) | コンポーネントシングルトンを破棄します。                                   |
| [addDelegate](#adddelegate)                     | イベントコールバックを追加します。                                   |
| [removeDelegate](#removedelegate)               | コールバックインターフェースを削除します。                                   |
| [destroy](#destroy)                             | 関数の破棄。このインスタンスを実行する必要がなくなった場合は、このインターフェースをコールしてください。   |
| [login](#login)                                 | コンポーネントインターフェースへのログイン。すべての機能を使用するためには、まずログインする必要があります。 |
| [logout](#logout)                               | コンポーネントインターフェースからログアウト。ログアウト後にダイヤル操作はできません。         |


### 通話操作に関連するインターフェース関数

| API                     | 説明           |
| ----------------------- | -------------- |
| [call](#call)           | 1対1通話に招待します。 |
| [groupCall](#groupcall) | グループチャット通話に招待します。 |
| [accept](#accept)       | 現在の通話を受信します。 |
| [reject](#reject)       | 現在の通話を拒否します。 |
| [hangup](#hangup)       | 現在の通話を終了します。 |

### プッシュプルストリームに関連するインターフェース関数

| API                                 | 説明                                                   |
| ----------------------------------- | ------------------------------------------------------ |
| [startRemoteView](#startremoteview) | リモートユーザーのカメラデータを指定のTXCloudVideoViewにレンダリングします。 |
| [stopRemoteView](#stopremoteview)   | リモートデータのレンダリングを停止します。                                     |

### 音声ビデオ制御に関連するインターフェース関数

| API                           | 説明                                             |
| ----------------------------- | ------------------------------------------------ |
| [openCamera](#opencamera)     | カメラを起動し、指定のTXCloudVideoViewにレンダリングします。 |
| [switchCamera](#switchcamera) | フロント/リアカメラを切り替えます。                       |
| [closeCamara](#closecamara)   | カメラを終了します。                           |
| [setMicMute](#setmicmute)     | ローカルオーディオキャプチャをミュートにします。                               |
| [setHandsFree](#sethandsfree) | ハンズフリーを設定します。                                       |

<h2 id="TRTCCallingDelegate">TRTCCallingDelegate API概要</h2>

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
| [onGroupCallInviteeListUpdate](#ongroupcallinviteelistupdate) | グループチャット招待リスト更新のコールバック。     |
| [onUserEnter](#onuserenter)                                  | ユーザーが通話に参加した場合のコールバック。         |
| [onUserLeave](#onuserleave)                                  | ユーザーが通話から退出した場合のコールバック。         |
| [onUserAudioAvailable](#onuseraudioavailable)                | ユーザーがオーディオアップストリームを開始したかどうかのコールバック。 |
| [onUserVideoAvailable](#onuservideoavailable)                | ユーザーがビデオアップストリームを開始したかどうかのコールバック。 |
| [onUserVoiceVolume](#onuservoicevolume)                      | ユーザー通話音量のコールバック。         |
| [onCallEnd](#oncallend)                                      | 通話終了時のコールバック。             |

## SDK基本関数

### sharedInstance

shareInstanceはTRTCCallingのコンポーネントシングルトンです。

```java
public static ITRTCCalling sharedInstance(Context context);
```

### destroySharedInstance

コンポーネントシングルトンを廃棄します。

```java
public static void destroySharedInstance();
```

### destroy

関数の廃棄。このインスタンスを実行する必要がなくなった場合は、このインターフェースをコールしてください。

```java
void destroy();
```

### addDelegate

[TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36066)イベントコールバック。TRTCCallingDelegateを介して[TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36066)の各種ステータス通知を受け取ることができます。

```java
public abstract void addDelegate(TRTCCallingDelegate delegate);
```

>?TRTCCallingDelegateはTRTCCallingのプロキシコールバックです。

### removeListener

コールバックインターフェースを削除します。

```java
void removeDelegate(TRTCCallingDelegate listener);
```

### login

コンポーネントにログインします。

```java
void login( int sdkAppId,
            final String userId, 
            String userSign, 
            final ActionCallBack callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppID | int         | TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】> アプリケーション情報でSDKAppIDを確認できます。 |
| user     | String         | 現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。 |
| userSig  | String         |Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |
| callback | ActionCallBack | ログイン時のコールバック、`onSuccess`はログインに成功したことを意味します。                         |

### logout

コンポーネントからログアウトします。

```java
void logout(final ActionCallBack callBack);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                 |
| -------- | -------------- | ------------------------------------ |
| callback | ActionCallBack | ログアウト時のコールバック、`onSuccess`はログアウトに成功したことを意味します。 |

## 通話操作に関連するインターフェース関数

### call

1対1通話の招待、現在通話中でも引き続き他のユーザーの招待をコールできます。

```java
void call(String userId, int type);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                             |
| ------ | ------ | -------------------------------- |
| userID | String   | ユーザーIDを呼び出します。         |
| type   | int    | 1は音声通話、2はビデオ通話を意味します。 |

### groupCall

IMグループが通話に招待すると、被招待者は`onInvited()`の コールバックを受け取ります。現在通話中でもこの関数をコールして引き続き他のユーザーを通話に招待することができ、また通話中のユーザーも`onGroupCallInviteeListUpdate`()のコールバックを受け取ることができます。

```java
void groupCall(List<String> userIdList, int type, String groupId);
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ               | 意味                             |
| ---------- | ------------------ | -------------------------------- |
| userIdList | List<String> | 招待IDリスト。                   |
| type       | int                | 1は音声通話、2はビデオ通話を意味します。 |
| groupId    | String             | グループID。                          |



### accept

現在の通話を受信します。被招待者として`onInvited()`のコールバックを受け取った場合は、この関数を呼び出して通話に応答することができます。

```java
void accept();
```



### reject

現在の通話を拒否します。被招待者として`onInvited()`のコールバックを受け取った場合は、この関数を呼び出して電話を拒否することができます。

```java
void reject();
```



### hangup

現在の通話を終了します。通話中である場合は、この関数を呼び出して通話を終了できます。

```java
void hangup();
```


## プッシュプルストリームに関連するインターフェース関数

### startRemoteView

リモートユーザーのカメラデータを指定のTXCloudVideoViewにレンダリングします。

```java
void startRemoteView(String userId, TXCloudVideoView txCloudVideoView);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ             | 意味                  |
| ------ | ---------------- | -------------------- |
| userId | String           | リモートユーザーID。        |
| txCloudVideoView   | TXCloudVideoView | ビデオ画像をロードするウィジェット。 |


### stopRemoteView

リモートデータのレンダリングを停止します。

```java
void stopRemoteView(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味           |
| ------ | ------ | ------------- |
| userId | String | リモートユーザーID。 |

## 音声ビデオ制御に関連するインターフェース関数

### openCamera

カメラを起動し、指定のTXCloudVideoViewにレンダリングします。

```java
void openCamera(boolean isFrontCamera, TXCloudVideoView txCloudVideoView);
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ             | 意味                                                 |
| ------------- | ---------------- | --------------------------------------------------- |
| isFrontCamera | boolean          | trueはフロントカメラの起動を、falseはリアカメラの起動を意味します。 |
| txCloudVideoView   | TXCloudVideoView | ビデオ画像をロードするウィジェット。                                |

### switchCamera

フロント/リアカメラを切り替えます。

```java
void switchCamera(boolean isFrontCamera);
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ    | 意味                                                     |
| ------------- | ------- | ------------------------------------------------------- |
| isFrontCamera | boolean | trueはフロントカメラへの切り替えを、falseはリアカメラへの切り替えを意味します。 |

### closeCamara

カメラをオフにします。

```java
void closeCamera();
```

### setMicMute

ローカルオーディオキャプチャをミュートにします。

```java
void setMicMute(boolean isMute);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                                        |
| ------ | ------- | ------------------------------------------- |
| isMute | boolean | trueはマイクの終了を、falseはマイクの起動を意味します。 |

### setHandsFree

リモートの音声をミュートにします。

```java
void setHandsFree(boolean isHandsFree);
```

パラメータは下表に示すとおりです。

| パラメータ        | タイプ    | 意味                                    |
| ----------- | ------- | --------------------------------------- |
| isHandsFree | boolean | trueはハンズフリーの起動を、falseはハンズフリーの終了を意味します。 |

## TRTCCallingDelegateイベントコールバック

## 一般的なイベントコールバック

### onError

エラーのコールバック。

>? SDKリカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

```java
void onError(int code, String msg);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ   | 意味       |
| ---- | ------ | ---------- |
| code | int    | エラーコード。   |
| msg  | String | エラー情報。 |


## 招待者のコールバック

### onReject

通話拒否時のコールバック。

```java
void onReject(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味            |
| ------ | ------ | --------------- |
| userId | String | 拒否したユーザーのID。 |

### onNoResp

相手方が応答しない場合のコールバック。

```java
void onNoResp(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味              |
| ------ | ------ | ----------------- |
| userId | String | 応答しないユーザーのID。 |

### onLineBusy

通話中である場合のコールバック。

```java
void onLineBusy(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味            |
| ------ | ------ | --------------- |
| userId | String | 通話中のユーザーのID。 |

## 被招待者のコールバック

### onInvited

通話に招待された時のコールバック。

```java
void onInvited(String sponsor, List<String> userIdList, boolean isFromGroup, int callType);
```

パラメータは下表に示すとおりです。

| パラメータ        | タイプ               | 意味                             |
| ----------- | ------------------ | -------------------------------- |
| sponsor     | String             | 発信者のID。                    |
| userIdList     | List&lt;String&gt; | 自分以外の招待IDのリスト。         |
| isFromGroup | boolean            | 多人数の通話への招待かどうか。               |
| callType        | int                | 1は音声通話、2はビデオ通話を意味します。 |

### onCallingCancel

現在の通話がキャンセルされた場合のコールバック。被招待者がリクエストを処理しない場合、招待者がキャンセル後にこのコールバックを受け取ります。

```java
void onCallingCancel();
```



### onCallingTimeOut

現在の通話がタイムアウトした場合のコールバック。

```java
void onCallingTimeout();
```

## 一般的なコールバック

### onGroupCallInviteeListUpdate

グループチャット招待リスト更新のコールバック。

```java
void onGroupCallInviteeListUpdate(List<String> userIdList);
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ               | 意味           |
| ---------- | ------------------ | -------------- |
| userIdList | List<String> | 招待IDリスト。 |

### onUserEnter

ユーザーが通話に参加した場合のコールバック。

```java
void onUserEnter(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味              |
| ------ | ------ | ----------------- |
| userId | String | 通話に参加したユーザーのID。 |

### onUserLeave

ユーザーが通話から退出した場合のコールバック。

```java
void onUserLeave(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味              |
| ------ | ------ | ----------------- |
| userId | String | 通話から離脱したユーザーのID。 |

### onUserAudioAvailable

ユーザーがオーディオアップストリームを開始したかどうかのコールバック。

```java
void onUserAudioAvailable(String userId, boolean available);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| userId    | String  | 通話するユーザーID。      |
| available | boolean | ユーザーの音声が使用可能かどうか。 |

### onUserVideoAvailable

ユーザーがビデオアップストリームを開始したかどうかのコールバック。通知を受け取った後、ユーザーは`startRemoteView`をコールしてリモートビデオを レンダリングすることができます。

```java
void onUserVideoAvailable(String userId, boolean available);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| userId    | String  | 通話するユーザーID。      |
| available | boolean | ユーザーのビデオが使用可能かどうか。 |


### onUserVoiceVolume

ユーザーの通話音量のコールバック。

```java
void onUserVoiceVolume(Map<String, Integer> volumeMap);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                       | 意味                                                         |
| --------- | -------------------------- | ------------------------------------------------------------ |
| volumeMap | Map<String, Integer> | ボリュームメーター。各useridに応じて、対応するボリュームレベルを取得できます。最小ボリュームは0、最大ボリュームは100です。 |

### onCallEnd

通話終了時のコールバック。

```java
void onCallEnd();
```
