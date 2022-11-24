## TUICallObserver APIの概要

TUICallObserverはTUICallEngineに対応するコールバックイベントクラスです。このコールバックによって、関心のあるコールバックイベントを監視することができます。

## コールバックイベントの概要

| API                                                          | 説明                       |
| ------------------------------------------------------------ | -------------------------- |
| [onError](#onerror) | 通話中のエラーコールバック         |
| [onCallReceived](#oncallreceived) | 通話リクエストのコールバック             |
| [onCallCancelled](#oncallcancelled) | 通話キャンセルのコールバック             |
| [onCallBegin](#oncallbegin) | 通話接続のコールバック             |
| [onCallEnd](#oncallend) | 通話終了のコールバック             |
| [onCallMediaTypeChanged](#oncallmediatypechanged) | 通話メディアタイプ変更発生のコールバック |
| [onUserReject](#onuserreject) | xxxxユーザーによる通話拒否のコールバック    |
| [onUserNoResponse](#onusernoresponse) | xxxxユーザーの応答なしのコールバック      |
| [onUserLineBusy](#onuserlinebusy) | xxxxユーザーが通話中である場合のコールバック        |
| [onUserJoin](#onuserjoin) | xxxxユーザーの通話参加のコールバック    |
| [onUserLeave](#onuserleave) | xxxxユーザーの通話からの退出のコールバック   |
| [onUserVideoAvailable](#onuservideoavailable) | xxxユーザーのビデオストリームの有無のコールバック |
| [onUserAudioAvailable](#onuseraudioavailable) | xxxユーザーのオーディオストリームの有無のコールバック |
| [onUserVoiceVolumeChanged](#onuservoicevolumechanged) | 全ユーザーの音量レベルフィードバックのコールバック |
| [onUserNetworkQualityChanged](#onusernetworkqualitychanged) | 全ユーザーのネットワーク品質フィードバックのコールバック |

## コールバックイベントの詳細

### onError

エラーのコールバック。

>? SDKリカバリー不能なエラーは必ず監視し、状況に応じてユーザーに適切なインターフェースプロンプトを表示します。

```java
void onError(int code, String msg);
```

パラメータは下表に示すとおりです。

| パラメータ | タイプ   | 意味     |
| ---- | ------ | -------- |
| code | int    | エラーコード   |
| msg  | String | エラー情報 |

### onCallReceived

新しい通話リクエストコールバックを受信します。着呼側が受信します。このイベントを監視することで、通話応答画面を表示するかどうかを決定できます。

```java
void onCallReceived(String callerId, List<String> calleeIdList, String groupId, 
                    TUICallDefine.MediaType callMediaType);
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ                    | 意味                                   |
| ------------- | ----------------------- | -------------------------------------- |
| callerId      | String                  | 発呼側ID（招待者）                      |
| calleeIdList  | List                    | 着呼側IDリスト（被招待者）               |
| groupId       | String                  | グループ通話ID                            |
| callMediaType | TUICallDefine.MediaType | 通話のメディアタイプ。ビデオ通話、音声通話など |

### onCallCancelled

今回の通話が発呼側からキャンセルされたことを表します（キャンセルの原因は発呼側の自主的なキャンセル、または通話タイムアウトによるキャンセルの両方の可能性があります）。着呼側が受信します。このイベントを監視することで、未応答通話などに類似した表示ロジックを実現できます。

```java
void onCallCancelled(String callerId);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味          |
| -------- | ------ | ------------- |
| callerId | String | キャンセルしたユーザーのID |

### onCallBegin

通話接続を表します。発呼側と着呼側がどちらも受信できます。このイベントを監視することで、クラウドレコーディング、コンテンツ審査などのフローを開始できます。

```java
void onCallBegin(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType, TUICallDefine.Role callRole);
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ                    | 意味                                                         |
| ------------- | ----------------------- | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId  | 今回の通話のオーディオビデオルームID。現在は数字のルームナンバーのみサポートしています。文字列のルームナンバーは今後のバージョンでサポート予定です |
| callMediaType | TUICallDefine.MediaType | 通話のメディアタイプ。ビデオ通話、音声通話                           |
| callRole      | TUICallDefine.Role      | ロール。列挙タイプ：発呼側、着呼側                                   |

### onCallEnd

通話の終了を表します。発呼側と着呼側がどちらも受信できます。このイベントを監視することで、通話時間、通話タイプなどの情報を表示したり、クラウドのレコーディングフローを停止したりすることができます。

```java
void onCallEnd(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType, TUICallDefine.Role callRole, long totalTime);
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ                    | 意味                                                         |
| ------------- | ----------------------- | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId  | 今回の通話のオーディオビデオルームID。現在は数字のルームナンバーのみサポートしています。文字列のルームナンバーは今後のバージョンでサポート予定です |
| callMediaType | TUICallDefine.MediaType | 通話のメディアタイプ。ビデオ通話、音声通話                           |
| callRole      | TUICallDefine.Role      | ロール。列挙タイプ：発呼側、着呼側                                   |
| totalTime     | long                    | 今回の通話時間                                               |

>! クライアントのイベントは一般的にすべて、プロセスキルなどの異常イベントに伴って消失します。通話時間の監視によって料金計算などのロジックを完成させたい場合は、REST APIを使用してこの種のフローを完成させることをお勧めします。

### onCallMediaTypeChanged

通話のメディアタイプに変更が発生したことを表します。

```java
void onCallMediaTypeChanged(TUICallDefine.MediaType oldCallMediaType,TUICallDefine.MediaType newCallMediaType);
```

パラメータは下表に示すとおりです。

| パラメータ             | タイプ                    | 意味         |
| ---------------- | ----------------------- | ------------ |
| oldCallMediaType | TUICallDefine.MediaType | 変更前の通話タイプ |
| newCallMediaType | TUICallDefine.MediaType | 変更後の通話タイプ |

### onUserReject

通話が拒否された場合のコールバックです。1v1通話では、発呼側のみが拒否のコールバックを受信します。グループ通話では、すべての被招待者がこのコールバックを受信することができます。

```java
void onUserReject(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味          |
| ------ | ------ | ------------- |
| userId | String | 拒否したユーザーのID |

### onUserNoResponse

相手方が応答しない場合のコールバック。

```java
void onUserNoResponse(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味            |
| ------ | ------ | --------------- |
| userId | String | 応答しないユーザーのID |

### onUserLineBusy

通話中である場合のコールバック。

```java
void onUserLineBusy(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味          |
| ------ | ------ | ------------- |
| userId | String | 通話中のユーザーのID |

### onUserJoin

今回の通話に参加したユーザーがいる場合のコールバック。

```java
void onUserJoin(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                  |
| ------ | ------ | --------------------- |
| userId | String | 現在の通話に参加したユーザーのID |

### onUserLeave

今回の通話から退出したユーザーがいる場合のコールバック。

```java
void onUserLeave(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                  |
| ------ | ------ | --------------------- |
| userId | String | 現在の通話から退出したユーザーのID |

### onUserVideoAvailable

ユーザーがビデオアップストリームを開始したかどうかのコールバック。

```java
void onUserVideoAvailable(String userId, boolean isVideoAvailable);
```

パラメータは下表に示すとおりです。

| パラメータ             | タイプ    | 意味             |
| ---------------- | ------- | ---------------- |
| userId           | String  | 通話ユーザーID      |
| isVideoAvailable | boolean | ユーザーのビデオが使用可能かどうか |

### onUserAudioAvailable

ユーザーがオーディオアップストリームを開始したかどうかのコールバック。

```java
void onUserAudioAvailable(String userId, boolean isAudioAvailable);
```

パラメータは下表に示すとおりです。

| パラメータ             | タイプ    | 意味             |
| ---------------- | ------- | ---------------- |
| userId           | String  | ユーザーID          |
| isAudioAvailable | boolean | ユーザーのオーディオが使用可能かどうか |

### onUserVoiceVolumeChanged

ユーザーの通話音量のコールバック。

```java
void onUserVoiceVolumeChanged(Map<String, Integer> volumeMap);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                 | 意味                                                         |
| --------- | -------------------- | ------------------------------------------------------------ |
| volumeMap | Map< String, Integer> | ボリュームメーター。各useridにつき、対応するユーザーの音量レベルを取得できます。音量の最小値は0、最大値は100です |

### onUserNetworkQualityChanged

ユーザーのネットワーク品質のコールバック。

```java
void onUserNetworkQualityChanged(List<TUICallDefine.NetworkQualityInfo> networkQualityList);
```

パラメータは下表に示すとおりです。

| パラメータ               | タイプ | 意味                                                     |
| ------------------ | ---- | -------------------------------------------------------- |
| networkQualityList | List | ネットワーク状態。各userIdにつき、対応するユーザーの現在のネットワーク品質を取得できます |
