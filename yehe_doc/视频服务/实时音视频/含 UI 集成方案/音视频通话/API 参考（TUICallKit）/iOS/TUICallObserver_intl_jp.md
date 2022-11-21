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

```objc
- (void)onError:(int)code message:(NSString * _Nullable)message;
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ     | 意味     |
| ------- | -------- | -------- |
| code    | int      | エラーコード   |
| message | NSString | エラー情報 |

### onCallReceived

新しい通話リクエストコールバックを受信します。着呼側が受信します。このイベントを監視することで、通話応答画面を表示するかどうかを決定できます。

```objc
- (void)onCallReceived:(NSString *)callerId calleeIdList:(NSArray<NSString *> *)calleeIdList groupId:(NSString * _Nullable)groupId callMediaType:(TUICallMediaType)callMediaType
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ             | 意味                                   |
| ------------- | ---------------- | -------------------------------------- |
| callerId      | NSString         | 発呼側ID（招待者）                      |
| calleeIdList  | NSArray          | 着呼側IDリスト（被招待者）               |
| groupId       | NSString         | グループ通話ID                            |
| callMediaType | TUICallMediaType | 通話のメディアタイプ。ビデオ通話、音声通話など |

### onCallCancelled

今回の通話が発呼側からキャンセルされたことを表します（キャンセルの原因は発呼側の自主的なキャンセル、または通話タイムアウトによるキャンセルの両方の可能性があります）。着呼側が受信します。このイベントを監視することで、未応答通話などに類似した表示ロジックを実現できます。

```objc
- (void)onCallCancelled:(NSString *)callerId;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ     | 意味          |
| -------- | -------- | ------------- |
| callerId | NSString | キャンセルしたユーザーのID |

### onCallBegin

通話接続を表します。発呼側と着呼側がどちらも受信できます。このイベントを監視することで、クラウドレコーディング、コンテンツ審査などのフローを開始できます。

```swift
- (void)onCallBegin:(TUIRoomId *)roomId callMediaType:(TUICallMediaType)callMediaType callRole:(TUICallRole)callRole;
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ             | 意味                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId   | 今回の通話のオーディオビデオルームID。現在は数字のルームナンバーのみサポートしています。文字列のルームナンバーは今後のバージョンでサポート予定です |
| callMediaType | TUICallMediaType | 通話のメディアタイプ。ビデオ通話、音声通話                           |
| callRole      | TUICallRole      | ロール。列挙タイプ：発呼側、着呼側                                   |

### onCallEnd

通話の終了を表します。発呼側と着呼側がどちらも受信できます。このイベントを監視することで、通話時間、通話タイプなどの情報を表示したり、クラウドのレコーディングフローを停止したりすることができます。

```swift
- (void)onCallEnd:(TUIRoomId *)roomId callMediaType:(TUICallMediaType)callMediaType callRole:(TUICallRole)callRole totalTime:(float)totalTime;
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ             | 意味                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId   | 今回の通話のオーディオビデオルームID。現在は数字のルームナンバーのみサポートしています。文字列のルームナンバーは今後のバージョンでサポート予定です |
| callMediaType | TUICallMediaType | 通話のメディアタイプ。ビデオ通話、音声通話                           |
| callRole      | TUICallRole      | ロール。列挙タイプ：発呼側、着呼側                                   |
| totalTime     | float            | 今回の通話時間                                               |

>! クライアントのイベントは一般的にすべて、プロセスキルなどの異常イベントに伴って消失します。通話時間の監視によって料金計算などのロジックを完成させたい場合は、REST APIを使用してこの種のフローを完成させることをお勧めします。

### onCallMediaTypeChanged

通話のメディアタイプに変更が発生したことを表します。

```swift
- (void)onCallMediaTypeChanged:(TUICallMediaType)oldCallMediaType newCallMediaType:(TUICallMediaType)newCallMediaType;
```

パラメータは下表に示すとおりです。

| パラメータ             | タイプ             | 意味         |
| ---------------- | ---------------- | ------------ |
| oldCallMediaType | TUICallMediaType | 変更前の通話タイプ |
| newCallMediaType | TUICallMediaType | 変更後の通話タイプ |

### onUserReject

通話が拒否された場合のコールバックです。1v1通話では、発呼側のみが拒否のコールバックを受信します。グループ通話では、すべての被招待者がこのコールバックを受信することができます。

```swift
- (void)onUserReject:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ     | 意味          |
| ------ | -------- | ------------- |
| userId | NSString | 拒否したユーザーのID |

### onUserNoResponse

相手方が応答しない場合のコールバック。

```swift
- (void)onUserNoResponse:(NSString *)userId;
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ     | 意味            |
| ------ | -------- | --------------- |
| userId | NSString | 応答しないユーザーのID |

### onUserLineBusy

通話中である場合のコールバック。

```swift
- (void)onUserLineBusy:(NSString *)userId;
```

### onUserJoin

今回の通話に参加したユーザーがいる場合のコールバック。

```swift
- (void)onUserJoin:(NSString *)userId;
```

### onUserLeave

今回の通話から退出したユーザーがいる場合のコールバック。

```swift
- (void)onUserLeave:(NSString *)userId;
```

### onUserAudioAvailable

ユーザーがオーディオアップストリームを開始したかどうかのコールバック。

```swift
- (void)onUserAudioAvailable:(NSString *)userId isAudioAvailable:(BOOL)isAudioAvailable;
```

パラメータは下表に示すとおりです。

| パラメータ             | タイプ     | 意味             |
| ---------------- | -------- | ---------------- |
| userId           | NSString | ユーザーID          |
| isAudioAvailable | BOOL     | ユーザーのオーディオが使用可能かどうか |

### onUserVideoAvailable

ユーザーがビデオアップストリームを開始したかどうかのコールバック。

```swift
- (void)onUserVideoAvailable:(NSString *)userId isVideoAvailable:(BOOL)isVideoAvailable;
```

パラメータは下表に示すとおりです。

| パラメータ             | タイプ     | 意味             |
| ---------------- | -------- | ---------------- |
| userId           | NSString | 通話ユーザーID      |
| isVideoAvailable | BOOL     | ユーザーのビデオが使用可能かどうか |

### onUserVoiceVolumeChanged

ユーザーの通話音量のコールバック。

```swift
- (void)onUserVoiceVolumeChanged:(NSDictionary <NSString *, NSNumber *> *)volumeMap;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                                  | 意味                                                         |
| --------- | ------------------------------------- | ------------------------------------------------------------ |
| volumeMap | NSDictionary <NSString *, NSNumber *> | ボリュームメーター。各useridに応じて、対応する音量レベルを取得できます。音量の最小値は0、最大値は100です |
| volumeMap | NSDictionary                          | ボリュームメーター。各userIdに応じて、対応する音量レベルを取得できます。音量の最小値は0、最大値は100です |

### onUserNetworkQualityChanged

ユーザーのネットワーク品質のコールバック。

```swift
- (void)onUserNetworkQualityChanged:(NSArray<TUINetworkQualityInfo *> *)networkQualityList;
```

パラメータは下表に示すとおりです。

| パラメータ               | タイプ    | 意味                                                     |
| ------------------ | ------- | -------------------------------------------------------- |
| networkQualityList | NSArray | ネットワーク状態。各userIdにつき、対応するユーザーの現在のネットワーク品質を取得できます |