## 機能説明

アプリのバックグラウンドでは、このコールバックを介して、以下に示すユーザーのグループメッセージの異常状況をモニタリングできます。
- 送信したメッセージのパラメータが間違っている（グループIDが存在しないなど）
- メッセージの送信頻度が上限を超えている
- メッセージの送信時にセキュリティ攻撃を受けた
- 送信者がミュートされているなど

## 注意事項

-  コールバックを有効にするには、コールバックURLを設定し、このコールバックプロトコルに対応するスイッチをオンにする必要があります。設定方法の詳細については、[サードパーティコールバックの設定](https://intl.cloud.tencent.com/document/product/1047/34520)ドキュメントをご参照ください。
-  コールバックの方向は、IMバックグラウンドからアプリバックグラウンドへHTTP POSTリクエストを送信するようになっています。
- アプリのバックグラウンドがコールバックリクエストを受信した後、リクエストURLのパラメータSDKAppIDが自分のSDKAppIDであるかどうかを確認する必要があります。
- その他のセキュリティ関連事項については、[サードパーティコールバックの概要：セキュリティに関する考慮事項](https://intl.cloud.tencent.com/document/product/1047/34354)ドキュメントをご参照ください。

## このコールバックをトリガーする可能性のあるシナリオ

-  アプリユーザーがクライアントでグループメッセージを送信する。
-  アプリ管理者がREST APIでグループメッセージを送信する。

## コールバックの発生時間

IMバックグラウンドがグループメッセージをグループメンバーに送信できなかった後。

## インターフェースの説明

### リクエストURLの例

以下の例のアプリ設定のコールバックURLは`https://www.example.com`です。
**例：**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### リクエストパラメータの説明

| パラメータ      | 説明                                                         |
| --------------- | ------------------------------------------------------------ |
| https           | リクエストプロトコルはHTTPS、リクエストメソッドはPOSTです    |
| www.example.com | コールバックURL                                              |
| SdkAppid        | アプリケーションの作成時にIMコンソールで割り当てられたSDKAppID |
| CallbackCommand | Group.CallbackSendMsgExceptionという固定値が適用されます     |
| contenttype     | JSONという固定値が適用されます                               |
| OptPlatform     | クライアントプラットフォーム。値の詳細については、[サードパーティコールバックの概要：コールバックプロトコル](https://intl.cloud.tencent.com/document/product/1047/34354)にあるOptPlatformのパラメータの意味をご参照ください |

### リクエストパケットの例

```
{
    "CallbackCommand": "Group.CallbackSendMsgException", // コールバックコマンド
    "GroupId": "@TGS#2J4SZEAEL", // グループID
    "Type": "Public", // グループタイプ
    "From_Account": "jared", // 送信者
    "Operator_Account":"admin", // リクエストの送信者
    "Random": 123456, // 乱数
    "OnlineOnlyFlag": 1, //オンラインメッセージは1、そうでない場合は0となります。ライブストリーミンググループの場合はこの属性を無視し、デフォルト値の0とします。
    "MsgBody": [ // メッセージボディです。TIMMessageのメッセージオブジェクトをご参照ください
        {
            "MsgType": "TIMTextElem", // テキスト
            "MsgContent": {
                "Text": "red packet"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data",
    "ErrorCode": 10023, // メッセージ異常のエラーコード
    "ErrorInfo": "msg count exceeds limit,please retry later", // メッセージ異常の詳細情報
    "EventTime":"1670574414123"//ミリ秒レベル、イベントのトリガータイムスタンプ		
}
```

### リクエストパケットフィールドの説明

| フィールド       | タイプ   | 説明                                                         |
| ---------------- | -------- | ------------------------------------------------------------ |
| CallbackCommand  | String   | コールバックコマンド                                         |
| GroupId          | String   | グループメッセージが生成されるグループID                     |
| Type             | String   | グループメッセージが生成される[グループタイプの概要](https://intl.cloud.tencent.com/document/product/1047/33529)。例：Public |
| From_Account     | String   | メッセージ送信者のUserID                                     |
| Operator_Account | String   | リクエスト送信者のUserID。管理者のリクエストかどうかを識別するために使用できます |
| Random           | Integer  | メッセージ送信リクエストにある32桁の乱数                     |
| OnlineOnlyFlag   | Integer  | オンラインメッセージ。値は1または0です。ライブストリーミンググループの場合はこの属性を無視し、デフォルト値の0に設定されています |
| MsgBody          | Array    | メッセージ内容。詳細については、[メッセージ形式の説明](https://intl.cloud.tencent.com/document/product/1047/33527)をご参照ください |
| CloudCustomData  | String   | メッセージカスタムデータ（クラウドに保存され、対向側に送信され、プログラムをアンインストールして再インストールした後にプルできます） |
| ErrorCode        | Interger | メッセージ異常のエラーコード。その他のエラーコードについては、[グループのエラーコード](https://intl.cloud.tencent.com/document/product/1047/34348)をご参照ください |
| ErrorInfo        | String   | メッセージ異常の詳細情報                                     |
| EventTime        | Integer  | イベントがトリガーされるミリ秒レベルのタイムスタンプ         |

### レスポンスパケットの例

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### レスポンスパケットフィールドの説明

| フィールド   | タイプ  | 属性 | 説明                                     |
| ------------ | ------- | ---- | ---------------------------------------- |
| ActionStatus | String  | 必須 | リクエスト処理の結果。入力する固定値：OK |
| ErrorCode    | Integer | 必須 | エラーコード。入力する固定値：0          |
| ErrorInfo    | String  | 必須 | エラー情報。固定値：空の文字列           |

## 参照情報

- [サードパーティコールバックの概要](https://intl.cloud.tencent.com/document/product/1047/34354)
-REST API：[グループ内での一般メッセージの送信](https://intl.cloud.tencent.com/document/product/1047/34959)
