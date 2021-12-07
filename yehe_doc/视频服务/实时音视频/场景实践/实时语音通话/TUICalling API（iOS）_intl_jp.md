TUICallingは、Tencent CloudのTRTCとIMを組み合わせたサービスであり、1v1および多人数のビデオ通話をサポートしています。TUICallingはTencent Cloudの2つのクローズドソースSDKに依存するオープンソースのClassです。具体的な実装プロセスについては、[リアルタイム音声通話（iOS）](https://intl.cloud.tencent.com/document/product/647/36067)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のオーディオビデオ通話コンポーネントとして使用します。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047)をシグナリング情報の送信と処理に使用します。


## TUICalling API概要
[](id:TUICalling)

#### SDK 基本関数

| API                                             | 説明                                                         |
| ----------------------------------------------- | ------------------------------------------------ |
| [sharedInstance](#sharedinstance)               | コンポーネントシングルトン。                                       |
| [call](#call) | C2C通話に招待します。                                   |
| [receiveAPNSCalled](#receiveAPNSCalled)                     | 被招待者として着信に応答します。                                   |
| [setCallingListener](#setCallingListener)               | リスナーを設定します。                                   |
| [setCallingBell](#setCallingBell)                             | 着信音の設定（30s以内を推奨）   |
| [enableMuteMode](#enableMuteMode)                                 | ミュートモードをオンにします |
| [enableCustomViewRoute](#enableCustomViewRoute)                               | カスタムビューの有効化       |


## TUICallingListener API概要
[](id:TUICallingListener)

#### イベントコールバック

| API                 | 説明       |
| ------------------- | ---------- |
| [shouldShowOnCallView](#shouldShowOnCallView) | 呼び出された時の応答ページのプルリクエスト |
| [onCallStart](#onCallStart) | 呼び出し開始コールバック。発呼側、着呼側ともにトリガーされます |
| [onCallEnd](#onCallEnd) | 通話コールバック。発呼側、着呼側ともにトリガーされます |
| [onCallEvent](#onCallEvent) | 通話イベントコールバック |

## Type API概要
[](id:Type)

#### 通話タイプ
| enum                 | 説明       |
| ------------------- | ---------- |
| TUICallingTypeAudio | オーディオ通話 |
| TUICallingTypeVideo | ビデオ通話 |

## Role API概要
[](id:Role)

#### ユーザーロールタイプ
| enum                 | 説明       |
| ------------------- | ---------- |
| TUICallingRoleCall | 通話発信者（発呼側） |
| TTUICallingRoleCalled | 通話受信者（着呼側） |

## Event API概要
[](id:Event)

#### イベントタイプ
| enum                 | 説明       |
| ------------------- | ---------- |
| TUICallingEventCallStart | 通話開始 |
| TUICallingEventCallSucceed | 通話接続成功 |
| TUICallingEventCallEnd | 通話終了 |
| TUICallingEventCallFailed | 通話失敗 |

## SDK基本関数

### sharedInstance
[](id:sharedInstance)

shareInstanceはTUICallingManagerのコンポーネントシングルトンです。

```objc
+ (instancetype)shareInstance;
```

### call
[](id:call)

C2C通話に招待します。

```objc
- (void)call:(NSArray<NSString *> *)userIDs type:(TUICallingType)type;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| userIDs    | NSArray  | 通話ユーザーIDリスト      |
| type | TUICallingType | 通話タイプ：オーディオ/ビデオ |

### receiveAPNSCalled
[](id:receiveAPNSCalled)

被招待者として着信に応答します。

```objc
- (void)receiveAPNSCalled:(NSArray<NSString *> *)userIDs type:(TUICallingType)type;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| userIDs    | NSArray  | 通話ユーザーIDリスト      |
| type | TUICallingType | 通話タイプ：オーディオ/ビデオ |

### setCallingListener
[](id:setCallingListener)

リスナーを設定します。

```objc
- (void)setCallingListener:(id<TUICallingListerner>)listener;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| listener    | TUICallingListener  | TUIcallingコンポーネントリスナー   |

### setCallingBell
[](id:setCallingBell)

着信音を設定します（30s以内を推奨）。

```objc
- (void)setCallingBell:(NSString *)filePath;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| filePath    | NSString  | 着信音リソースパス   |

### enableMuteMode
[](id:enableMuteMode)

ミュートモードをオンにします。

```objc
- (void)enableMuteMode:(BOOL)enable;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| enable    | BOOL  | ミュートモード有効化の有無   |

### enableCustomViewRoute
[](id:enableCustomViewRoute)

カスタムビューをオンにします。
オンにすると、呼び出し/被呼び出し開始コールバックの中で、CallingViewControllerのインスタンスを受信します。開発者自身が表示方式を決定します。
>! フルスクリーン表示にする必要があります。そうしない場合、表示に異常が生じます。

```objc
- (void)enableCustomViewRoute:(BOOL)enable;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| enable    | BOOL  | カスタムビュー有効化の有無   |


## TUICallingListenerコールバック関数

### shouldShowOnCallView
[](id:shouldShowOnCallView)

呼び出された時の応答ページのプルリクエストに対する同意の有無。

```objc
- (BOOL)shouldShowOnCallView;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| 戻り値    | BOOL  |  同意の有無   |

### onCallStart
[](id:onCallStart)

呼び出し開始コールバック。発呼側、着呼側ともにトリガーされます。

```objc
 - (void)callStart:(NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role viewController:(UIViewController * _Nullable)viewController;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| userIDs    | NSArray  | 通話ユーザーIDリスト      |
| type | TUICallingType | 通話タイプ：オーディオ/ビデオ |
| role | TUICallingRole | ユーザーロールタイプ：発呼側/着呼側 |
| viewController | UIViewController | 通話ビューViewController  |

### onCallEnd
[](id:onCallEnd)

通話終了コールバック。発呼側、着呼側ともにトリガーされます。enableCustomViewRouteの設定がNOの時、このコールバックメソッドはトリガーされません。

```objc
 - (void)callEnd:(NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role totalTime:(CGFloat)totalTime;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| userIDs    | NSArray | 通話ユーザーIDリスト      |
| type | TUICallingType | 通話タイプ：オーディオ/ビデオ |
| role | TUICallingRole | ユーザーロールタイプ：発呼側/着呼側 |
| totalTime | CGFloat | 通話時間。単位：秒  |

### onCallEvent
[](id:onCallEvent)

通話イベントコールバック。enableCustomViewRouteの設定がNOの時、このコールバックメソッドはトリガーされません。

```objc
- (void)onCallEvent:(TUICallingEvent)event type:(TUICallingType)type role:(TUICallingRole)role message:(NSString *)message;
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| event    | TUICallingEvent  | 通話イベントタイプ。      |
| type | TUICallingType | 通話タイプ：オーディオ/ビデオ |
| role | TUICallingRole | ユーザーロールタイプ：発呼側/着呼側 |
| message | NSString | イベントの説明情報 |




