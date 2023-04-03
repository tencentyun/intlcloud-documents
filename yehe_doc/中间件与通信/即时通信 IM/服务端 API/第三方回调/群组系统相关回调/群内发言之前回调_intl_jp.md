## 機能説明

Appバックグラウンドは、このコールバックを使用して、ユーザーのグループメッセージをリアルタイムで確認でき、以下を含みます：
-  グループメッセージをリアルタイムで記録します（たとえば、ログの記録、他のシステムへの同期など）。
-  グループで発言するユーザーのリクエストをブロックします。
>! メッセージのプレコールバックはデフォルトで2秒のタイムアウトになり、調整することはお勧めしません。プレコールバックを使用して内容審査を処理すると、プレコールバック全体がタイムアウトする場合があります。内容審査が必要な場合は、内容コールバックを使用してください。

## 注意事項

-  コールバックを有効にするには、コールバックURLを構成し、このコールバックプロトコルに対応するスイッチをオンにする必要があります。構成方法の詳細については、[サードパーティのコールバック構成](https://intl.cloud.tencent.com/document/product/1047/34520)ドキュメントをご参照ください。
-  コールバックの方向は、IMバックグラウンドからAppバックグラウンドへのHTTP POSTリクエストを開始することです。
- Appバックグラウンドは、コールバックリクエストを受け取った後、リクエストURLのパラメータSDKAppIDが独自のSDKAppIDであるかどうかを確認する必要があります。
- その他のセキュリティ関連事項については、[サードパーティコールバック概要：セキュリティに関する考慮事項](https://intl.cloud.tencent.com/document/product/1047/34354)ドキュメントをご参照ください。

## コールバックをトリガーするシナリオ

-  Appユーザーは、クライアントを通じてグループメッセージを送信します。
-  App管理者は、REST APIを通じてグループメッセージを送信します。

## コールバックの発生時間

IMバックグラウンドがグループメッセージをグループメンバーに送信する前。

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
| SdkAppid        | アプリケーション作成時にIMコンソールで割り当てられたSDKAppID |
| CallbackCommand | Group.CallbackBeforeSendMsgに固定します                      |
| contenttype     | 固定値はJSONです                                             |
| ClientIP        | クライアントIP、形式はたとえば127.0.0.1です                  |
| OptPlatform     | クライアントプラットフォーム、値の選択は、[サードパーティコールバック概要：コールバックプロトコル](https://intl.cloud.tencent.com/document/product/1047/34354)のパラメータOptPlatformの意味を参照します |

### リクエストパッケージの事例

```
{
    "CallbackCommand": "Group.CallbackBeforeSendMsg", // コールバックコマンド
    "GroupId": "@TGS#2J4SZEAEL", // グループID
    "Type": "Community", // グループタイプ
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
    "TopicId":"@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_TestTopic",// トピックID、このオプションは、トピックをサポートするコミュニティにのみ適用されます
    "EventTime":"1670574414123"//ミリ秒レベル、イベントトリガーのタイムスタンプ		
}
```

### リクエストパッケージフィールドの説明

| フィールド       | タイプ  | 説明                                                         |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | コールバックコマンド                                         |
| GroupId          | String  | グループメッセージを生成するグループID                       |
| Type             | String  | グループメッセージを生成する[グループタイプ概要](https://intl.cloud.tencent.com/document/product/1047/33529)、たとえばPublic |
| From_Account     | String  | メッセージの送信者UserID                                     |
| Operator_Account | String  | リクエストの開始者UserID、管理者によるリクエストかどうかを認識するために使用できます |
| Random           | Integer | メッセージリクエストの32ビットの乱数                         |
| OnlineOnlyFlag   | Integer | オンラインメッセージは1、そうでない場合は0となります。ライブブロードキャストグループの場合はこの属性を無視し、デフォルト値の0とします。 |
| MsgBody          | Array   | メッセージ内容。具体的には、[メッセージ形式の説明](https://intl.cloud.tencent.com/document/product/1047/33527)をご参照ください |
| CloudCustomData  | String  | メッセージカスタムデータ（クラウドに保存され、対向側に送信され、プログラムをアンインストールして再インストールした後にプルできます） |
| TopicId          | String  | トピックID、このオプションが使用可能な場合、トピック内の発言を意味します。このオプションは、トピックをサポートするコミュニティにのみ適用されます |
| EventTime        | Integer | イベントトリガーのミリ秒レベルのタイムスタンプ               |

### レスポンスパッケージの事例

#### 発言の許可

送信するメッセージの内容を変更せずにユーザーの発言が許可されます。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // 0は発言が許可されることを意味します
}
```

#### 発言の禁止

ユーザーの発言は許可されていません。このメッセージは送信されず、呼び出し元にエラーコード`10016`が返されます。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 1 // 1は発言が拒否されることを意味します
}
```

#### サイレントに破棄

ユーザーの発言は許可されていません。このメッセージは送信されませんが、呼び出し元に成功が返され、メッセージが送信されたと呼び出し元に思わせます。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 2 // 2はサイレントに破棄することを意味します
}
```

#### メッセージ内容の変更

次のレスポンス事例は、ユーザーが送信したグループメッセージを変更する（カスタムメッセージを追加する）ことです。IMバックグラウンドは、変更後のメッセージを送信します。Appバックグラウンドは、この機能に基づいて、ユーザーが送信したメッセージに、たとえばユーザーレベル、タイトルなど、特別な内容を追加できます。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0, // 0である必要があります。この方法でのみ、変更後のメッセージを正常に送信できます
    "MsgBody": [ // App変更後のメッセージ、存在しない場合はユーザーが送信したメッセージがデフォルトで使用されます
        {
            "MsgType": "TIMTextElem", // テキスト
            "MsgContent": {
                "Text": "red packet"
            }
        },
        {
            "MsgType": "TIMCustomElem", // カスタムメッセージ
            "MsgContent": {
                "Desc": "CustomElement.MemberLevel", // 説明
                "Data": "LV1" // データ
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

### レスポンスパッケージフィールドの説明

| フィールド      | タイプ  | 属性       | 説明                                                         |
| --------------- | ------- | ---------- | ------------------------------------------------------------ |
| ActionStatus    | String  | 必須       | リクエスト処理の結果、OKは処理が成功したことを意味し、FAILは失敗を意味します |
| ErrorCode       | Integer | 必須       | エラーコード。0は発言が許可され、1は発現が拒否され、2はサイレントに破棄することを意味します。業務が発言を拒否したいと同時に、エラーコードErrorCodeおよびErrorInfoをクライアントに渡した場合は、エラーコードErrorCodeを[10100, 10200]の範囲内に設定してください |
| ErrorInfo       | String  | 必須       | エラーメッセージ                                             |
| MsgBody         | Array   | オプション | App変更後のメッセージボディ。Instant Messagingバックグラウンドは、変更後のメッセージをグループに送信します。具体的な形式については、[メッセージ形式の説明](https://intl.cloud.tencent.com/document/product/1047/33527)をご参照ください |
| CloudCustomData | String  | オプション |                                                              |


## 参考

- [サードパーティのコールバック概要](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API：[グループでの普通メッセージの送信](https://intl.cloud.tencent.com/document/product/1047/34959)
