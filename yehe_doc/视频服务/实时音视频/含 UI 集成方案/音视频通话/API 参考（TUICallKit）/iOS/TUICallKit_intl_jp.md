## TUICallKit APIの概要

TUICallKit APIはオーディオビデオ通話コンポーネントの**UIインターフェース付き**のものです。TUICallKit APIを使用することで、WeChatのようなオーディオビデオ通話シーンをシンプルなインターフェースでスピーディーに実現できます。より詳細なアクセス手順については、[TUICallKitクイックアクセス](https://www.tencentcloud.com/document/product/647/50992)をご参照ください。

## APIの概要

| API                                                          | 説明                                                   |
| ------------------------------------------------------------ | -------------------------------- |
| [createInstance](#createinstance) | TUICallKitインスタンスの作成（シングルトンモード） |
| [setSelfInfo](#setselfinfo) | ユーザーのニックネーム、プロフィール画像の設定             |
| [call](#call) | 1v1通話の開始                    |
| [groupCall](#groupcall) | グループ通話の開始                     |
| [joinInGroupCall](#joiningroupcall) | 現在のグループ通話に自主的に参加         |
| [setCallingBell](#setcallingbell) | カスタム着信音の設定               |
| [enableMuteMode](#enablemutemode) | ミュートモードのオン/オフ                |
| [enableFloatWindow](#enablefloatwindow) | フローティングウィンドウ機能のオン/オフ              |

## APIの詳細

### createInstance

TUICallKitのシングルトンを作成します。

```objectivec
- (instancetype)createInstance;
```

### setSelfInfo

ユーザーニックネーム、プロフィール画像を設定します。ユーザーニックネームは500バイト以内、ユーザープロフィール画像はURL形式でなければなりません。

```objectivec
- (void)setSelfInfo:(NSString * _Nullable)nickname avatar:(NSString * _Nullable)avatar succ:(TUICallSucc)succ fail:(TUICallFail)fail
```

| パラメータ     | タイプ     | 意味           |
| -------- | -------- | -------------- |
| nickName | NSString | ターゲットユーザーのニックネーム |
| avatar   | NSString | ターゲットユーザーのプロフィール画像 |

### call

電話をかけます（1v1通話）

```objectivec
- (void)call:(NSString *)userId callMediaType:(TUICallMediaType)callMediaType;
```

パラメータは下表に示すとおりです。

| パラメータ          | タイプ             | 意味                                   |
| ------------- | ---------------- | -------------------------------------- |
| userId        | NSString         | ターゲットユーザーのuserId                      |
| callMediaType | TUICallMediaType | 通話のメディアタイプ。ビデオ通話、音声通話など |

### groupCall

グループ通話を開始します。注意：グループ通話を使用する前にIMグループを作成する必要があります。作成済みの場合は無視してください。

```objectivec
- (void)groupCall:(NSString *)groupId userIdList:(NSArray<NSString *> *)userIdList callMediaType:(TUICallMediaType)callMediaType;
```

| パラメータ          | タイプ             | 意味                                   |
| ------------- | ---------------- | -------------------------------------- |
| groupId       | NSString         | 今回のグループ通話のグループID                    |
| userIdList    | NSArray          | ターゲットユーザーのuserIdリスト                 |
| callMediaType | TUICallMediaType | 通話のメディアタイプ。ビデオ通話、音声通話など |

### joinInGroupCall

グループ通話を開始します。注意：グループ通話を使用する前にIMグループを作成する必要があります。作成済みの場合は無視してください。

```objectivec
- (void)joinInGroupCall:(TUIRoomId *)roomId groupId:(NSString *)groupId callMediaType:(TUICallMediaType)callMediaType;
```

| パラメータ          | タイプ             | 意味                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId   | 今回の通話のオーディオビデオルームID。現在は数字のルームナンバーのみサポートしています。文字列のルームナンバーは今後のバージョンでサポート予定です |
| groupId       | NSString         | 今回のグループ通話のグループID                                          |
| callMediaType | TUICallMediaType | 通話のメディアタイプ。ビデオ通話、音声通話など                       |

### setCallingBell

カスタム着信音を設定します。 ここではローカルファイルアドレスのみ渡すことができます。このファイルディレクトリにアプリケーションがアクセスできることを確認する必要があります。

着信音を設定後、デバイスにバインドします。ユーザーを変更しても着信音はそのまま有効です。

デフォルトの着信音に戻したい場合は、`filePath`にnullを渡します。

```objectivec
- (void)setCallingBell:(NSString *)filePath;
```

### enableMuteMode

ミュートモードをオン/オフします。

```objc
- (void)enableMuteMode:(BOOL)enable;
```

### enableFloatWindow

フローティングウィンドウ機能をオン/オフします。デフォルトでは`false`で、通話画面の左上隅のフローティングウィンドウボタンは非表示になっており、trueに設定すると表示されます。

```objc
- (void)enableFloatWindow:(BOOL)enable;
```