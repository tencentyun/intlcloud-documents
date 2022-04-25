TUICallingは、Tencent CloudのTRTCとIMを組み合わせたサービスであり、1v1および多人数のビデオ通話をサポートしています。TUICallingはTencent Cloudの2つのクローズドソースSDKに依存するオープンソースのClassです。具体的な実装プロセスについては、[リアルタイムビデオ通話（Android）](https://intl.cloud.tencent.com/document/product/647/36066)をご参照ください。

- TRTC SDK：[TRTC SDK](https://intl.cloud.tencent.com/document/product/647)を低遅延のオーディオビデオ通話コンポーネントとして使用します。
- IM SDK： [IM SDK](https://intl.cloud.tencent.com/document/product/1047)をシグナリング情報の送信と処理に使用します。

## TUICalling API概要

#### SDK 基本関数

| API                                                          | 説明                   |
| :----------------------------------------------------------- | :------------------------ |
| [sharedInstance](https://intl.cloud.tencent.com/document/product/647/43140) | コンポーネントシングルトン                  |
| [call](https://intl.cloud.tencent.com/document/product/647/43140) | C2C通話に招待              |
| [setCallingListener](https://intl.cloud.tencent.com/document/product/647/43140) | リスナーを設定              |
| [setCallingBell](https://intl.cloud.tencent.com/document/product/647/43140) | 着信音を設定（30秒以内を推奨） |
| [enableMuteMode](https://intl.cloud.tencent.com/document/product/647/43140) | ミュートモードをオンにする              |
| [enableCustomViewRoute](https://intl.cloud.tencent.com/document/product/647/43140) | カスタムビューをオンにする            |

## TUICallingListener API概要

#### イベントコールバック

| API                                                          | 説明                            |
| :----------------------------------------------------------- | :------------------------------- |
| [shouldShowOnCallView](https://intl.cloud.tencent.com/document/product/647/43140) | 呼び出されたときに応答画面のプルアップをリクエストします           |
| [onCallStart](https://intl.cloud.tencent.com/document/product/647/43140) | 呼び出し開始コールバック。発呼側、着呼側ともにトリガーされます |
| [onCallEnd](https://intl.cloud.tencent.com/document/product/647/43140) | 通話コールバック。発呼側、着呼側ともにトリガーされます     |
| [onCallEvent](https://intl.cloud.tencent.com/document/product/647/43140) | 通話イベントコールバック                     |

## Type API概要

#### 通話タイプ

| enum  | 説明     |
| :---- | :------- |
| AUDIO | オーディオ通話 |
| VIDEO | ビデオ通話 |

## Role API概要

#### ユーザーロールタイプ

| enum   | 説明               |
| :----- | :----------------- |
| CALL   | 通話発信者（発呼側） |
| CALLED | 通話受信者（着呼側） |

## Event API概要

#### イベントタイプ

| enum         | 説明         |
| :----------- | :----------- |
| CALL_START   | 通話開始     |
| CALL_SUCCEED | 通話接続成功 |
| CALL_END     | 通話終了     |
| CALL_FAILED  | 通話失敗     |

## SDK基本関数

### sharedInstance

shareInstanceはTUICallingのコンポーネントシングルトンです。

```java
public static TUICallingImpl sharedInstance();
```

### call

C2C通話に招待します。


```java
void call(String[] userIDs, Type type);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ            | 意味                |
| :------ | :-------------- | :------------------ |
| userIDs | String[]        | 通話ユーザーIDリスト    |
| type    | TUICalling.Type | 通話タイプ：オーディオ/ビデオ |

### setCallingListener
リスナーを設定します。


```java
void setCallingListener(TUICallingListener listener);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ               | 意味                  |
| :------- | :----------------- | :-------------------- |
| listener    | TUICallingListener  | TUIcallingコンポーネントリスナー   |

### setCallingBell

着信音を設定します(30s以内を推奨)。

```java
void setCallingBell(String filePath);
```



パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味         |
| :------- | :----- | :----------- |
| filePath    | String  | 着信音リソースパス   |

### enableMuteMode

ミュートモードをオンにします。

```java
void enableMuteMode(boolean enable);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味             |
| :----- | :------ | :--------------- |
| enable    | boolean  | ミュートモード有効化の有無   |

### enableCustomViewRoute

カスタムビューをオンにします。
オンにすると、呼び出し/被呼び出し開始コールバックの中で、CallingViewのインスタンスを受信します。開発者自身が表示方式を決定します。

>! フルスクリーンまたはスクリーンと同じ比率で表示する必要があります。そうしない場合、表示に異常が生じます。

```java
void enableCustomViewRoute(boolean enable);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味               |
| :----- | :------ | :----------------- |
| enable    | boolean  | カスタムビュー有効化の有無   |

## TUICallingListenerコールバック関数

### shouldShowOnCallView

呼び出された時の応答ページのプルリクエストに対する同意の有無。

```java
boolean shouldShowOnCallView();
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ    | 意味     |
| :----- | :------ | :------- |
| 戻り値    | boolean  |  同意の有無   |

### onCallStart

呼び出し開始コールバック。発呼側、着呼側ともにトリガーされます。

```java
 void onCallStart(String[] userIDs, TUICalling.Type type, TUICalling.Role role, View tuiCallingView);
```

パラメータは下表に示すとおりです。

| パラメータ           | タイプ            | 意味                                                         |
| :------------- | :-------------- | :----------------------------------------------------------- |
| userIDs        | String[]        | 通話ユーザーIDリスト。                                           |
| type           | TUICalling.Type | 通話タイプ：オーディオ/ビデオ                                          |
| role           | TUICalling.Role | ユーザーロールタイプ：発呼側/着呼側                                      |
| tuiCallingView | View            | 通話ビューView。enableCustomViewRouteの設定がfalseの時、viewはnullになります。 |

### onCallEnd

通話終了コールバック。発呼側、着呼側ともにトリガーされます。

```java
 void onCallEnd(String[] userIDs, TUICalling.Type type, TUICalling.Role role, long totalTime);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ            | 意味                    |
| :-------- | :-------------- | :---------------------- |
| userIDs   | String[]        | 通話ユーザーIDリスト        |
| type      | TUICalling.Type | 通話タイプ：オーディオ/ビデオ     |
| role      | TUICalling.Role | ユーザーロールタイプ：発呼側/着呼側 |
| totalTime | long            | 通話時間。単位：秒      |

### onCallEvent

通話イベントコールバック。

```java
void onCallEvent(TUICalling.Event event, TUICalling.Type type, TUICalling.Role role, String message);
```

パラメータは下表に示すとおりです。

| パラメータ    | タイプ             | 意味                    |
| :------ | :--------------- | :---------------------- |
| event   | TUICalling.Event | 通話イベントタイプ            |
| type    | TUICalling.Type  | 通話タイプ：オーディオ/ビデオ     |
| role    | TUICalling.Role  | ユーザーロールタイプ：発呼側/着呼側 |
| message | String           | イベントの説明情報          |