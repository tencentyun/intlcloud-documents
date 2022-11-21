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

```objectivec
- (TUICallEngine *)createInstance;
```

### destroyInstance

TUICallEngineのシングルトンを破棄します。

```objectivec
- (void)destroyInstance;
```

### init

関数を初期化します。すべての機能を使用する前にこの関数を呼び出し、通話サービス認証を含む初期化操作を完了させてください。

```objectivec
- (void)init:(NSString *)sdkAppID userId:(NSString *)userId userSig:(NSString *)userSig succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ               | 意味                                                         |
| -------- | ------------------ | ------------------------------------------------------------ |
| sdkAppID | int                | **TRTCコンソール** > [**アプリケーション管理**](https://console.tencentcloud.com/trtc/app) > **アプリケーション情報**でSDKAppIDを確認できます |
| userId   | String             | 現在のユーザーID。文字列タイプでは、アルファベット（a-z および A-Z）、数字（0-9）、ハイフン（-）、アンダーバー（_）のみ使用できます |
| userSig  | String             | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、 [UserSigの計算、使用方法](https://www.tencentcloud.com/document/product/647/35166)をご参照ください |
| callback | TUIDefine.Callback | 初期化コールバック。`onSuccess`は初期化に成功したことを表します                        |

### addObserver

このコールバックインターフェースを追加すると、この応答を通じて`TUICallObserver`関連のイベントコールバックを監視できます。

```objectivec
- (void)addObserver:(id<TUICallObserver>)observer;
```

### removeObserver

コールバックインターフェースを削除します。

```objectivec
- (void)removeObserver:(id<TUICallObserver>)observer;
```

### call

電話をかけます（1v1通話）

```objectivec
- (void)call:(TUIRoomId *)roomId userId:(NSString *)userId callMediaType:(TUICallMediaType)callMediaType params:(TUICallParams *)params succ:(TUICallSucc)succ fail:(TUICallFail)fail
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ             | 意味                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId   | 今回の通話のオーディオビデオルームID。現在は数字のルームナンバーのみサポートしています。文字列のルームナンバーは今後のバージョンでサポート予定です |
| userId        | NSString         | ターゲットユーザーのuserId                                            |
| callMediaType | TUICallMediaType | 通話のメディアタイプ。ビデオ通話、音声通話など                       |
| params        | TUICallParams    | 通話パラメータ拡張フィールド。例：カスタムコンテンツのオフラインプッシュ                   |

### groupCall

グループ通話を開始します。注意：グループ通話を使用する前にIMグループを作成する必要があります。作成済みの場合は無視してください。

```objectivec
- (void)groupCall:(TUIRoomId *)roomId groupId:(NSString *)groupId userIdList:(NSArray <NSString *> *)userIdList callMediaType:(TUICallMediaType)callMediaType params:(TUICallParams *)params succ:(TUICallSucc)succ fail:(TUICallFail)fail
```

| パラメータ          | タイプ             | 意味                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId   | 今回の通話のオーディオビデオルームID。現在は数字のルームナンバーのみサポートしています。文字列のルームナンバーは今後のバージョンでサポート予定です |
| groupId       | NSString         | 今回のグループ通話のグループID                                          |
| userIdList    | NSArray          | ターゲットユーザーのuserIdリスト                                       |
| callMediaType | TUICallMediaType | 通話のメディアタイプ。ビデオ通話、音声通話など                       |
| params        | TUICallParams    | 通話パラメータ拡張フィールド。例：カスタムコンテンツのオフラインプッシュ                   |

### accept

現在の通話を受信します。着呼側として`onCallReceived()`のコールバックを受信した場合は、この関数を呼び出して通話に応答することができます。

```objectivec
- (void)accept:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### reject

現在の通話を拒否します。着呼側として`onCallReceived()`のコールバックを受信した場合は、この関数を呼び出して通話を拒否することができます。

```objectivec
- (void)reject:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### ignore

現在の通話を無視します。着呼側として`onCallReceived()`のコールバックを受信した場合は、この関数を呼び出して通話を無視することができ、このとき発呼側は`onUserLineBusy`のコールバックを受信します。備考：業務内にライブストリーミング、ミーティングなどのシーンがある場合、ライブストリーミング/ミーティング中の場合もこの関数を呼び出して通話を無視することができます。

```objectivec
- (void)ignore:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### hangup

現在の通話を終了します。通話中である場合は、この関数を呼び出して通話を終了できます。

```objectivec
- (void)hangup:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### inviteUser

今回のグループ通話にユーザーを招待します。ユースケース：グループ通話中のユーザーが自主的に他の人を招待する場合に使用します。

```objectivec
- (void)inviteUser:(NSArray<NSString *> *)userIdList params:(TUICallParams *)params succ:(void(^)(NSArray <NSString *> *userIdList))succ fail:(TUICallFail)fail
```

| パラメータ       | タイプ          | 意味                                       |
| ---------- | ------------- | ------------------------------------------ |
| userIdList | NSArray       | ターゲットユーザーのuserIdリスト                     |
| params     | TUICallParams | 通話パラメータ拡張フィールド。例：カスタムコンテンツのオフラインプッシュ |

### joinInGroupCall

今回のグループ通話に自主的に参加します。ユースケース：グループ内のユーザーが今回のグループ通話に自主的に参加する場合に使用します。

```objectivec
- (void)joinInGroupCall:(TUIRoomId *)roomId groupId:(NSString *)groupId callMediaType:(TUICallMediaType)callMediaType succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

| パラメータ          | タイプ             | 意味                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId   | 今回の通話のオーディオビデオルームID。現在は数字のルームナンバーのみサポートしています。文字列のルームナンバーは今後のバージョンでサポート予定です |
| groupId       | NSString         | 今回のグループ通話のグループID                                          |
| callMediaType | TUICallMediaType | 通話のメディアタイプ。ビデオ通話、音声通話など                       |

### switchCallMediaType

ビデオ通話を音声通話へ切り替えます。

```objectivec
- (void)switchCallMediaType:(TUICallMediaType)newType;
```

| パラメータ          | タイプ             | 意味                                   |
| ------------- | ---------------- | -------------------------------------- |
| callMediaType | TUICallMediaType | 通話のメディアタイプ。ビデオ通話、音声通話など |

### startRemoteView

ビデオ画面に表示するViewオブジェクトを設定します

```objectivec
- (void)startRemoteView:(NSString *)userId videoView:(TUIVideoView *)videoView onPlaying:(void(^)(NSString *userId))onPlaying onLoading:(void(^)(NSString *userId))onLoading onError:(void(^)(NSString *userId, int code, NSString *errMsg))onError;
```

| パラメータ      | タイプ         | 意味              |
| --------- | ------------ | ----------------- |
| userId    | NSString     | ターゲットユーザーのuserId |
| videoView | TUIVideoView | レンダリング対象のビュー      |

### stopRemoteview

リモートユーザーのビデオデータのサブスクリプションを停止します。

```objectivec
- (void)stopRemoteView:(NSString *)userId;
```

| パラメータ   | タイプ     | 意味              |
| ------ | -------- | ----------------- |
| userId | NSString | ターゲットユーザーのuserId |

### openCamera

カメラをオンにする

```objectivec
- (void)openCamera:(TUICallCamera)camera videoView:(TUIVideoView *)videoView succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

| パラメータ      | タイプ          | 意味             |
| --------- | ------------- | ---------------- |
| camera    | TUICallCamera | フロントカメラ/リアカメラ |
| videoView | TUIVideoView  | レンダリング対象のビュー     |

### closeCamera

カメラをオフにします。

```objectivec
- (void)closeCamera;
```

### switchCamera

フロント/リアカメラを切り替えます。

```objectivec
- (void)switchCamera:(TUICallCamera)camera;
```

| パラメータ   | タイプ          | 意味             |
| ------ | ------------- | ---------------- |
| camera | TUICallCamera | フロントカメラ/リアカメラ |

### openMicrophone

マイクをオンにします

```objectivec
- (void)openMicrophone:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### closeMicrophone

マイクをオフにします。

```objectivec
- (void)closeMicrophone;
```

### selectAudioPlaybackDevice

オーディオ再生デバイスを選択します。 現在はヘッドホン、スピーカーをサポートしています。通話のシーンでは、このインターフェースを使用してハンズフリーモードのオン/オフが行えます。

```objectivec
- (void)selectAudioPlaybackDevice:(TUIAudioPlaybackDevice)device;
```

| パラメータ   | タイプ                   | 意味        |
| ------ | ---------------------- | ----------- |
| device | TUIAudioPlaybackDevice | ヘッドホン/スピーカー |

### setSelfInfo

ユーザーニックネーム、プロフィール画像を設定します。ユーザーニックネームは500バイト以内、ユーザープロフィール画像はURL形式でなければなりません。

```objectivec
- (void)setSelfInfo:(NSString * _Nullable)nickName avatar:(NSString * _Nullable)avatar succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### enableMultiDeviceAbility

TUICallEngineのマルチデバイスログインモードをオン/オフします （プレミアム版パッケージのみサポート）

```objectivec
- (void)enableMultiDeviceAbility:(BOOL)enable succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```