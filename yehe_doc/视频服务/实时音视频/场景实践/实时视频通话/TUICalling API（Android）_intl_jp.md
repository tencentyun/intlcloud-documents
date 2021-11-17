TUICallingは、Tencent CloudのTRTCとIMを組み合わせたサービスであり、1v1および多人数のビデオ通話をサポートしています。TUICallingはTencent Cloudの2つのクローズドソースSDKに依存するオープンソースのClassです。具体的な実装プロセスについては、[リアルタイムビデオ通話（Android）](https://intl.cloud.tencent.com/document/product/647/36066)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のオーディオビデオ通話コンポーネントとして使用します。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047)をシグナリング情報の送信と処理に使用します。


## TUICalling API概要
[](id:TUICalling)

#### SDK 基本関数

| API                                             | 説明                                                         |
| ----------------------------------------------- | ------------------------------------------------ |
| [sharedInstance](#sharedinstance)               | コンポーネントシングルトン                                     |
| [call](#call) | C2C通話に招待します                                   |
| [receiveAPNSCalled](#receiveAPNSCalled)                     | 被招待者として着信に応答します                                   |
| [setCallingListener](#setCallingListener)               | リスナーを設定します。                                   |
| [setCallingBell](#setCallingBell)                             | 着信音の設定（30s以内を推奨）   |
| [enableMuteMode](#enableMuteMode)                                 | ミュートモードをオンにします |
| [enableFloatWindow](#enableFloatWindow)                               | フローティングウィンドウをオンにします      |
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
| AUDIO | オーディオ通話 |
| VIDEO | ビデオ通話 |

## Role API概要
[](id:Role)

#### ユーザーロールタイプ
| enum                 | 説明       |
| ------------------- | ---------- |
| CALL | 通話発信者（発呼側） |
| CALLED | 通話受信者（着呼側） |

## Event API概要
[](id:Event)

#### イベントタイプ
| enum                 | 説明       |
| ------------------- | ---------- |
| CALL_START | 通話開始 |
| CALL_SUCCEED | 通話接続成功 |
| CALL_END | 通話終了 |
| CALL_FAILED | 通話失敗 |

## SDK基本関数

### sharedInstance
[](id:sharedInstance)

shareInstanceはTUICallingのコンポーネントシングルトンです。

```java
public static TUICallingManager sharedInstance();
```

### call
[](id:call)

C2C通話に招待します。

```java
void call(String[] userIDs, Type type);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| userIDs    | String[]  | 通話ユーザーIDリスト      |
| type | TUICalling.Type | 通話タイプ：オーディオ/ビデオ |

### receiveAPNSCalled
[](id:receiveAPNSCalled)

被招待者として着信に応答します。

```java
void receiveAPNSCalled(String[] userIDs, Type type);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| userIDs    | String[]  | 通話ユーザーIDリスト      |
| type | TUICalling.Type | 通話タイプ：オーディオ/ビデオ |

### setCallingListener
[](id:setCallingListener)

リスナーを設定します。

```java
void setCallingListener(TUICallingListener listener);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| listener    | TUICallingListener  | TUIcallingコンポーネントリスナー   |

### setCallingBell
[](id:setCallingBell)

着信音を設定します(30s以内を推奨)。

```java
void setCallingBell(String filePath);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| filePath    | String  | 着信音リソースパス   |

### enableMuteMode
[](id:enableMuteMode)

ミュートモードをオンにします。

```java
void enableMuteMode(boolean enable);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| enable    | boolean  | ミュートモード有効化の有無   |

### enableFloatWindow
[](id:enableFloatWindow)

フローティングウィンドウをオンにします。

```java
void enableFloatWindow(boolean enable);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| enable    | boolean  | フローティングウィンドウ有効化の有無   |

### enableCustomViewRoute
[](id:enableCustomViewRoute)

カスタムビューをオンにします。
オンにすると、呼び出し/被呼び出し開始コールバックの中で、CallingViewのインスタンスを受信します。開発者自身が表示方式を決定します。
>! フルスクリーンまたはスクリーンと同じ比率で表示する必要があります。そうしない場合、表示に異常が生じます。

```java
void enableCustomViewRoute(boolean enable);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| enable    | boolean  | カスタムビュー有効化の有無   |


## TUICallingListenerコールバック関数

### shouldShowOnCallView
[](id:shouldShowOnCallView)

呼び出された時の応答ページのプルリクエストに対する同意の有無。

```java
boolean shouldShowOnCallView();
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| 戻り値    | boolean  |  同意の有無   |

### onCallStart
[](id:onCallStart)

呼び出し開始コールバック。発呼側、着呼側ともにトリガーされます。

```java
 void onCallStart(String[] userIDs, TUICalling.Type type, TUICalling.Role role, View tuiCallingView);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| userIDs    | String[]  | 通話ユーザーIDリスト。      |
| type | TUICalling.Type | 通話タイプ：オーディオ/ビデオ |
| role | TUICalling.Role | ユーザーロールタイプ：発呼側/着呼側 |
| tuiCallingView | View | 通話ビューView。enableCustomViewRouteの設定がfalseの時、viewはnullになります。 |

### onCallEnd
[](id:onCallEnd)

通話終了コールバック。発呼側、着呼側ともにトリガーされます。

```java
 void onCallEnd(String[] userIDs, TUICalling.Type type, TUICalling.Role role, long totalTime);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| userIDs    | String[]  | 通話ユーザーIDリスト      |
| type | TUICalling.Type | 通話タイプ：オーディオ/ビデオ |
| role | TUICalling.Role | ユーザーロールタイプ：発呼側/着呼側 |
| totalTime | long | 通話時間。単位：秒 |

### onCallEvent
[](id:onCallEvent)

通話イベントコールバック。

```java
void onCallEvent(TUICalling.Event event, TUICalling.Type type, TUICalling.Role role, String message);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ    | 意味               |
| --------- | ------- | ------------------ |
| event    | TUICalling.Event  | 通話イベントタイプ      |
| type | TUICalling.Type | 通話タイプ：オーディオ/ビデオ |
| role | TUICalling.Role | ユーザーロールタイプ：発呼側/着呼側 |
| message | String | イベントの説明情報 |




