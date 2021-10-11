TRTCCallingはTencent CloudのTencent Real-Time Communication（TRTC）とIMを組み合わせたサービスで、1v1オーディオビデオ通話をサポートします。TRTCCallingは、Tencent Cloudの2つのクローズドソースSDKに依存する1つのオープンソースのClassです。具体的な実装プロセスについては、[Real-time Voice Call（Flutter）](https://intl.cloud.tencent.com/document/product/647/41692)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のオーディオビデオ通話コンポーネントとして使用します。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047)をシグナリング情報の送信と処理に使用します。


<h2 id="TRTCCalling">TRTCCalling API概要</h2>

### SDK基本関数

| API                                             | 説明                                                         |
| ----------------------------------------------- | ------------------------------------------------ |
| [sharedInstance](#sharedinstance)               | コンポーネントシングルトン。                                       |
| [destroySharedInstance](#destroysharedinstance) | コンポーネントシングルトンを廃棄します。                                   |
| [registerListener](#registerlistener)           | イベントコールバックを追加します。 |
| [unRegisterListener](#unregisterlistener)       | コールバックインターフェースを削除します。 |
| [destroy](#destroy)                             | 関数の廃棄。このインスタンスを実行する必要がなくなった場合は、このインターフェースをコールしてください。   |
| [login](#login)                                 | コンポーネントインターフェースへのログイン。すべての機能を使用するためには、まずログインする必要があります。 |
| [logout](#logout)                               | コンポーネントインターフェースからログアウト。ログアウト後にダイヤル操作はできません。         |


### 通話操作に関連するインターフェース関数

| API                     | 説明           |
| ----------------------- | -------------- |
| [call](#call)           | 1対1通話に招待します。 |
| [accept](#accept)       | 現在の通話を受信します。 |
| [reject](#reject)       | 現在の通話を拒否します。 |
| [hangup](#hangup)       | 現在の通話を終了します。 |


### オーディオ制御に関するインターフェース関数

| API                           | 説明                                             |
| ----------------------------- | ------------------------------------------------ |
| [setMicMute](#setmicmute)     | ローカルオーディオキャプチャをミュートにします。                                   |
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
| [onUserEnter](#onuserenter)                                  | ユーザーが通話に参加した場合のコールバック。         |
| [onUserLeave](#onuserleave)                                  | ユーザーが通話から退出した場合のコールバック。         |
| [onUserAudioAvailable](#onuseraudioavailable)                | ユーザーがオーディオアップストリームを開始したかどうかのコールバック。 |
| [onUserVoiceVolume](#onuservoicevolume)                      | ユーザー通話音量のコールバック。         |
| [onCallEnd](#oncallend)                                      | 通話終了時のコールバック。             |

## SDK基本関数

### sharedInstance

shareInstanceはTRTCCallingのコンポーネントシングルトンです。

```java
static Future<TRTCCalling> sharedInstance();
```

### destroySharedInstance

コンポーネントシングルトンを廃棄します。

```java
static void destroySharedInstance();
```

### destroy

関数の廃棄。このインスタンスを実行する必要がなくなった場合は、このインターフェースをコールしてください。

```java
void destroy();
```

### registerListener

[TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36066)イベントコールバック。TRTCCallingDelegateを介して[TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36066)の各種ステータス通知を受け取ることができます。

```java
void registerListener(VoiceListenerFunc func);
```


### unRegisterListener

コールバックインターフェースを削除します。

```java
void unRegisterListener(VoiceListenerFunc func);
```

### login

コンポーネントにログインします。

```java
Future<ActionCallback> login(int sdkAppId, String userId, String userSig);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ           | 意味                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppID | int         | TRTCコンソール >【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】> アプリケーション情報でSDKAppIDを確認できます。 |
| userId     | String         | 現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。 |
| userSig  | String         |Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 |

### logout

コンポーネントからログアウトします。

```java
Future<ActionCallback> logout();
```

## 通話操作に関連するインターフェース関数

### call

1対1通話の招待、現在通話中でも引き続き他のユーザーの招待をコールできます。

```java
Future<ActionCallback> call(String userId, int type);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                             |
| ------ | ------ | -------------------------------- |
| userID | String   | ユーザーIDを呼び出します。         |
| type   | int    | 1は音声通話、2はビデオ通話を意味します。 |

### accept

現在の通話を受信します。被招待者として`onInvited()`のコールバックを受け取った場合は、この関数を呼び出して通話に応答することができます。

```java
Future<ActionCallback> accept();
```

### reject

現在の通話を拒否します。被招待者として`onInvited()`のコールバックを受け取った場合は、この関数を呼び出して電話を拒否することができます。

```java
Future<ActionCallback> reject();
```

### hangup

現在の通話を終了します。通話中である場合は、この関数を呼び出して通話を終了できます。

```java
void hangup();
```


## オーディオ制御に関するインターフェース関数

### setMicMute

ローカルオーディオキャプチャをミュートにします。

```java
void setMicMute(bool isMute);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味                                        |
| ------ | ------- | ------------------------------------------- |
| isMute | bool | trueはマイクの終了を、falseはマイクの起動を意味します。 |

### setHandsFree

リモートの音声をミュートにします。

```java
void setHandsFree(bool isHandsFree);
```

パラメータは下表に示すとおりです。

| パラメータ        | タイプ    | 意味                                    |
| ----------- | ------- | --------------------------------------- |
| isHandsFree | bool | trueはハンズフリーの起動を、falseはハンズフリーの終了を意味します。 |

## TRTCCallingDelegateイベントコールバック

## 一般的なイベントコールバック

### onError

エラーのコールバック。

>? SDKリカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

パラメータは下表に示すとおりです。

| パラメータ | タイプ   | 意味       |
| ---- | ------ | ---------- |
| code | int    | エラーコード。   |
| msg  | String | エラー情報。 |


## 招待者のコールバック

### onReject

通話拒否時のコールバック。

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味            |
| ------ | ------ | --------------- |
| userId | String | 拒否したユーザーのID。 |

### onNoResp

相手方が応答しない場合のコールバック。

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味              |
| ------ | ------ | ----------------- |
| userId | String | 応答しないユーザーのID。 |

### onLineBusy

通話中である場合のコールバック。


パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味            |
| ------ | ------ | --------------- |
| userId | String | 通話中のユーザーのID。 |

## 被招待者のコールバック

### onInvited

通話に招待された時のコールバック。

パラメータは下表に示すとおりです。

| パラメータ        | タイプ               | 意味                             |
| ----------- | ------------------ | -------------------------------- |
| sponsor     | String             | 発信者のID。                    |
| userIds     | List&lt;String&gt; | 自分以外の招待IDのリスト。         |
| isFromGroup | bool          | 多人数の通話への招待かどうか。               |
| type        | int                | 1は音声通話、2はビデオ通話を意味します。 |

### onCallingCancel

現在の通話がキャンセルされた場合のコールバック。被招待者がリクエストを処理しない場合、招待者がキャンセル後にこのコールバックを受け取ります。


### onCallingTimeOut

現在の通話がタイムアウトした場合のコールバック。


## 一般的なコールバック

### onUserEnter

ユーザーが通話に参加した場合のコールバック。

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味              |
| ------ | ------ | ----------------- |
| userId | String | 通話に参加したユーザーのID。 |

### onUserLeave

ユーザーが通話から退出した場合のコールバック。

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味              |
| ------ | ------ | ----------------- |
| userId | String | 通話から離脱したユーザーのID。 |

### onUserAudioAvailable

ユーザーがオーディオアップストリームを開始したかどうかのコールバック。

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| userId    | String  | 通話するユーザーID。      |
| available | boolean | ユーザーのオーディオが使用可能かどうか。 |


### onUserVoiceVolume

ユーザーの通話音量のコールバック。

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                       | 意味                                                         |
| --------- | -------------------------- | ------------------------------------------------------------ |
| userVolumes | List | ディスカッション中のルームの全参加者の音量、値の範囲：0～100。 |
| totalVolume | int| すべてのリモート参加者の総音量。値の範囲：0～100。|

### onCallEnd

通話終了時のコールバック。
