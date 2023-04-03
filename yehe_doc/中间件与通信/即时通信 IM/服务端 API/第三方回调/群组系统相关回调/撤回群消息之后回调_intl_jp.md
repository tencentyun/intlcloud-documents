## 機能説明

Appバックグラウンドは、このコールバックを使用して、ユーザーのグループチャットメッセージの撤回アクションをリアルタイムで確認できます。

## 注意事項

- コールバックを有効にするには、コールバックURLを構成し、このコールバックプロトコルに対応するスイッチをオンにする必要があります。構成方法の詳細については、[サードパーティのコールバック構成](https://intl.cloud.tencent.com/document/product/1047/34520)ドキュメントをご参照ください。
- コールバックの方向は、IMバックグラウンドからAppバックグラウンドへのHTTP POSTリクエストを開始することです。
- Appバックグラウンドは、コールバックリクエストを受け取った後、リクエストURLのパラメータSDKAppIDが独自のSDKAppIDであるかどうかを確認する必要があります。
- その他のセキュリティ関連事項については、[サードパーティコールバック概要：セキュリティに関する考慮事項](https://intl.cloud.tencent.com/document/product/1047/34354)ドキュメントをご参照ください。

## コールバックをトリガーするシナリオ

- Appユーザーは、クライアントを通じてグループチャットメッセージを撤回します。
- App管理者は、REST APIを通じてグループチャットメッセージを撤回します。

## コールバックの発生時間

グループチャットメッセージの撤回に成功した後。

## インターフェースの説明

### リクエストURLの事例

次の事例のApp構成のコールバックURLは`https://www.example.com`です。
**事例：**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### リクエストパラメータの説明

| パラメータ      | 説明                                                         |
| --------------- | ------------------------------------------------------------ |
| https           | リクエストプロトコルはHTTPS、リクエスト方式はPOSTです        |
| www.example.com | コールバックURL                                              |
| SdkAppid        | アプリケーション作成時にIMコンソールでアサインされたSDKAppID |
| CallbackCommand | Group.CallbackAfterRecallMsgに固定します                     |
| contenttype     | 固定値はJSONです                                             |
| ClientIP        | クライアントIP、形式はたとえば127.0.0.1です                  |
| OptPlatform     | クライアントプラットフォーム、値の選択は、[サードパーティコールバック概要：コールバックプロトコル](https://intl.cloud.tencent.com/document/product/1047/34354)のパラメータOptPlatformの意味を参照します |

### リクエストパッケージの事例

```
{
    "CallbackCommand":"Group.CallbackAfterRecallMsg", // コールバックコマンド
    "Operator_Account":"admin", // オペレーター
    "Type":"Community", // グループタイプ
    "GroupId":"1213456", // グループID
    "MsgSeqList":[ // 撤回メッセージMsgSeqリスト           
        {"MsgSeq":130}
    ],
    "TopicId":"@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_TestTopic",// トピックID、このオプションは、トピックをサポートするコミュニティにのみ適用されます
    "EventTime":"1670574414123"//ミリ秒レベル、イベントトリガーのタイムスタンプ		
}
```

### リクエストパッケージフィールドの説明

| オブジェクト     | 概要    | 機能                                                         |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | コールバックコマンド                                         |
| Operator_Account | String  | グループチャットメッセージを撤回するオペレーターUserID       |
| Type             | String  | グループメッセージを生成する[グループタイプ概要](https://intl.cloud.tencent.com/document/product/1047/33529)、たとえばPublic |
| GroupId          | String  | グループID                                                   |
| MsgSeqList       | Array   | 撤回メッセージMsgSeqリスト                                   |
| TopicId          | String  | トピックID、このオプションが使用可能な場合、トピック内のメッセージが撤回されたことを意味します。このオプションは、トピックをサポートするコミュニティにのみ適用されます。 |
| EventTime        | Integer | イベントトリガーのミリ秒レベルのタイムスタンプ               |

### レスポンスパッケージの事例

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // コールバック結果を無視します
}
```

### レスポンスパッケージフィールドの説明

| フィールド   | タイプ  | 属性 | 説明                                                         |
| ------------ | ------- | ---- | ------------------------------------------------------------ |
| ActionStatus | String  | 必須 | リクエスト処理の結果、OKは処理が成功したことを意味し、FAILは失敗を意味します |
| ErrorCode    | Integer | 必須 | エラーコード、ここで0を入力すると、レスポンス結果を無視できることを意味します |
| ErrorInfo    | String  | 必須 | エラーメッセージ                                             |

## 参考

- [サードパーティのコールバック概要](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API：[グループメッセージの撤回](https://intl.cloud.tencent.com/document/product/1047/34965)
