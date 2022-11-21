## TUICallEngine APIの概要

TUICallEngine APIはオーディオビデオ通話コンポーネントの**UIインターフェースがない**ものです。TUICallKitのインタラクションではニーズを満たせない場合はこのインターフェースを使用し、パッケージのインタラクションをカスタマイズすることができます。

## APIの概要

| API                                                          | 説明                                                        |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](#createinstance) | TUICallEngineインスタンスの作成（シングルトンモード）                         |
| [destroyInstance](#destroyinstance) | TUICallEngineインスタンスの破棄（シングルトンモード）                         |
| [init](#init) | オーディオビデオ通話基本機能の認証完了                                |
| [addObserver](#addobserver) | イベントコールバックの追加                                                |
| [removeObserver](#removeobserver) | コールバックインターフェースの削除                                                |
| [call](#call) | 1v1通話の開始                                               |
| [groupCall](#groupcall) | グループ通話の開始                                                |
| [accept](#accept) | 通話応答                                                    |
| [reject](#reject) | 通話拒否                                                    |
| [hangup](#hangup) | 通話終了                                                    |
| [ignore](#ignore) | 通話を無視                                                    |
| [inviteUser](#inviteuser) | グループ通話中に他の人を招待                                |
| [joinInGroupCall](#joiningroupcall) | 現在のグループ通話に自主的に参加                                    |
| [switchCallMediaType](#switchcallmediatype) | 通話メディアタイプの切り替え。ビデオ通話からオーディオ通話への切り替えなど                    |
| [startRemoteView](#startremoteview) | リモートユーザービデオストリームのサブスクリプション開始                                      |
| [stopRemoteView](#stopremoteview) | リモートユーザービデオストリームのサブスクリプション停止                                      |
| [openCamera](#opencamera) | カメラの起動                                                  |
| [closeCamera](#closecamera) | カメラの終了                                                   |
| [switchCamera](#switchcamera) | フロント/リアカメラの切り替え                                              |
| [openMicrophone](#openmicrophone) | マイクをオンにする                                                  |
| [closeMicrophone](#closemicrophone) | マイクをオフにする                                                  |
| [selectAudioPlaybackDevice](#selectaudioplaybackdevice) |  オーディオ再生デバイスの選択（ヘッドホン/スピーカー）                             |
| [setSelfInfo](#setselfinfo) | ユーザーのニックネーム、プロフィール画像の設定                                        |
| [enableMultiDeviceAbility](#enablemultideviceability) | TUICallEngineのマルチデバイスログインモードのオン/オフ （プレミアム版パッケージのみサポート） |

## APIの詳細

### createInstance

TUICallEngineのシングルトンを作成します。

```java
TUICallEngine createInstance(Context context)
```

### destroyInstance

TUICallEngineのシングルトンを破棄します。

```java
void destroyInstance();
```

### init

関数を初期化します。すべての機能を使用する前にこの関数を呼び出し、通話サービス認証を含む初期化操作を完了させてください。

```java
void init(int sdkAppId, String userId, String userSig, TUICommonDefine.Callback callback)
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ                     | 意味                                                         |
| -------- | ------------------------ | ------------------------------------------------------------ |
| sdkAppId | int                      | **TRTCコンソール** > [**アプリケーション管理**](https://console.tencentcloud.com/trtc/app) > **アプリケーション情報**でSDKAppIDを確認できます |
| userId   | String                   | 現在のユーザーID。文字列タイプでは、アルファベット（a-z および A-Z）、数字（0-9）、ハイフン（-）、アンダーバー（_）のみ使用できます |
| userSig  | String                   | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、 [UserSigの計算、使用方法](https://www.tencentcloud.com/document/product/647/35166)をご参照ください |
| callback | TUICommonDefine.Callback | 初期化コールバック。`onSuccess`は初期化に成功したことを表します                        |

### addObserver

このコールバックインターフェースを追加すると、この応答を通じて`TUICallObserver`関連のイベントコールバックを監視できます。

```java
void addObserver(TUICallObserver observer);
```

### removeObserver

コールバックインターフェースを削除します。

```java
void removeObserver(TUICallObserver observer);
```

### call

電話をかけます（1v1通話）。

```java
void call(TUICommonDefine.RoomId roomId, String userId, TUICallDefine.MediaType callMediaType,
          TUICallDefine.CallParams params, TUICommonDefine.Callback callback);
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ                     | 意味                                                         |
| ------------- | ------------------------ | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId   | 今回の通話のオーディオビデオルームID。現在は数字のルームナンバーのみサポートしています。文字列のルームナンバーは今後のバージョンでサポート予定です |
| userId        | String                   | ターゲットユーザーのuserId                                            |
| callMediaType | TUICallDefine.MediaType | 通話のメディアタイプ。例：ビデオ通話、音声通話など                     |
| params        | TUICallDefine.CallParams | 通話パラメータ拡張フィールド。例：カスタムコンテンツのオフラインプッシュ                   |

### groupCall

グループ通話を開始します。注意：グループ通話を使用する前にIMグループを作成する必要があります。作成済みの場合は無視してください。

```java
void groupCall(TUICommonDefine.RoomId roomId, String groupId, List<String> userIdList,    
               TUICallDefine.MediaType callMediaType, TUICallDefine.CallParams params,                               
               TUICommonDefine.Callback callback);
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ                     | 意味                                                         |
| ------------- | ------------------------ | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId   | 今回の通話のオーディオビデオルームID。現在は数字のルームナンバーのみサポートしています。文字列のルームナンバーは今後のバージョンでサポート予定です |
| groupId       | String                   | 今回のグループ通話のグループID                                          |
| userIdList    | List                     | ターゲットユーザーのuserIdリスト                                       |
| callMediaType | TUICallDefine.MediaType | 通話のメディアタイプ。例：ビデオ通話、音声通話など                     |
| params        | TUICallDefine.CallParams | 通話パラメータ拡張フィールド。例：カスタムコンテンツのオフラインプッシュ                   |

### accept

現在の通話を受信します。着呼側として`onCallReceived()`のコールバックを受信した場合は、この関数を呼び出して通話に応答することができます。

```java
void accept(TUICommonDefine.Callback callback);
```

### reject

現在の通話を拒否します。着呼側として`onCallReceived()`のコールバックを受信した場合は、この関数を呼び出して通話を拒否することができます。

```java
void reject(TUICommonDefine.Callback callback);
```

### ignore

現在の通話を無視します。着呼側としてonCallReceived()のコールバックを受信した場合は、この関数を呼び出して通話を無視することができ、このとき発呼側はonUserLineBusyのコールバックを受信します。

備考：業務内にライブストリーミング、ミーティングなどのシーンがある場合、ライブストリーミング/ミーティング中の場合もこの関数を呼び出して通話を無視することができます。

```java
void ignore(TUICommonDefine.Callback callback);
```

### hangup

現在の通話を終了します。通話中である場合は、この関数を呼び出して通話を終了できます。

```java
void hangup(TUICommonDefine.Callback callback);
```

### inviteUser

今回のグループ通話にユーザーを招待します。

ユースケース：グループ通話中のユーザーが自主的に他の人を招待する場合に使用します。

```java
void inviteUser(List<String> userIdList, TUICallDefine.CallParams params, 
                TUICommonDefine.ValueCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ                     | 意味                                       |
| ---------- | ------------------------ | ------------------------------------------ |
| userIdList | List                     | ターゲットユーザーのuserIdリスト                     |
| params     | TUICallDefine.CallParams | 通話パラメータ拡張フィールド。例：カスタムコンテンツのオフラインプッシュ |

### joinInGroupCall

今回のグループ通話に自主的に参加します。

ユースケース：グループ内のユーザーが今回のグループ通話に自主的に参加する場合に使用します。

```java
void joinInGroupCall(TUICommonDefine.RoomId roomId, String groupId, 
                     TUICallDefine.MediaType callMediaType, TUICommonDefine.Callback callback);
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ                    | 意味                                                         |
| ------------- | ----------------------- | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId  | 今回の通話のオーディオビデオルームID。現在は数字のルームナンバーのみサポートしています。文字列のルームナンバーは今後のバージョンでサポート予定です |
| groupId       | String                  | 今回のグループ通話のグループID                                          |
| callMediaType | TUICallDefine.MediaType | 通話のメディアタイプ。ビデオ通話、音声通話など                       |

### switchCallMediaType

ビデオ通話を音声通話へ切り替えます。

```java
void switchCallMediaType(TUICallDefine.MediaType callMediaType);
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ                    | 意味                                   |
| ------------- | ----------------------- | -------------------------------------- |
| callMediaType | TUICallDefine.MediaType | 通話のメディアタイプ。ビデオ通話、音声通話など |

### startRemoteView

リモートユーザーのビデオデータのサブスクリプションを開始します。このインターフェースはsetRenderViewの後に呼び出します。

```java
void startRemoteView(String userId, TUIVideoView videoView, TUICommonDefine.PlayCallback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ         | 意味              |
| --------- | ------------ | ----------------- |
| userId    | String       | ターゲットユーザーのuserId |
| videoView | TUIVideoView | レンダリング対象のビュー      |

### stopRemoteView

リモートユーザーのビデオデータのサブスクリプションを停止します。

```java
void stopRemoteView(String userId);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味              |
| ------ | ------ | ----------------- |
| userId | String | ターゲットユーザーのuserId |

### openCamera

カメラをオンにする

```java
void openCamera(TUICommonDefine.Camera camera, TUIVideoView videoView, TUICommonDefine.Callback callback);
```

パラメータは下表に示すとおりです。

| パラメータ      | タイプ                   | 意味             |
| --------- | ---------------------- | ---------------- |
| camera    | TUICommonDefine.Camera | フロントカメラ/リアカメラ |
| videoView | TUIVideoView           | レンダリング対象のビュー     |

### closeCamera

カメラをオフにします。

```java
void closeCamera();
```

### switchCamera

フロント/リアカメラを切り替えます。

```java
void switchCamera(TUICommonDefine.Camera camera);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ                   | 意味             |
| ------ | ---------------------- | ---------------- |
| camera | TUICommonDefine.Camera | フロントカメラ/リアカメラ |

### openMicrophone

マイクをオンにします

```java
void openMicrophone(TUICommonDefine.Callback callback);
```

### closeMicrophone

マイクをオフにします。

```java
void closeMicrophone();
```

### selectAudioPlaybackDevice

オーディオ再生デバイスを選択します。 現在はヘッドホン、スピーカーをサポートしています。通話のシーンでは、このインターフェースを使用してハンズフリーモードのオン/オフが行えます。

```java
void selectAudioPlaybackDevice(TUICommonDefine.AudioPlaybackDevice device);
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ                                | 意味        |
| ------ | ----------------------------------- | ----------- |
| device | TUICommonDefine.AudioPlaybackDevice | ヘッドホン/スピーカー |

### setSelfInfo

ユーザーニックネーム、プロフィール画像を設定します。ユーザーニックネームは500バイト以内、ユーザープロフィール画像はURL形式でなければなりません。

```java
void setSelfInfo(String nickname, String avatar, TUICommonDefine.Callback callback);
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味                   |
| -------- | ------ | ---------------------- |
| nickname | String | ユーザーニックネーム               |
| avatar   | String | ユーザープロフィール画像（形式はURL） |

### enableMultiDeviceAbility

TUICallEngineのマルチデバイスログインモードをオン/オフします （プレミアム版パッケージのみサポート）。

```java
void enableMultiDeviceAbility(boolean enable, TUICommonDefine.Callback callback);
```