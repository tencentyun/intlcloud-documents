## 機能説明

Appバックグラウンドは、このコールバックを使用して、グループメッセージが正常に送信されたことをAppバックグラウンドに通知し、Appがそれに応じて必要なデータ同期を実行するなど、ユーザーのグループメッセージをリアルタイムで確認できます。

## 注意事項

-  コールバックを有効にするには、コールバックURLを構成し、このコールバックプロトコルに対応するスイッチをオンにする必要があります。構成方法の詳細については、[サードパーティのコールバック構成](https://intl.cloud.tencent.com/document/product/1047/34520)ドキュメントをご参照ください。
-  コールバックの方向は、IMバックグラウンドからAppバックグラウンドへのHTTP POSTリクエストを開始することです。
- Appバックグラウンドは、コールバックリクエストを受け取った後、リクエストURLのパラメータSDKAppIDが独自のSDKAppIDであるかどうかを確認する必要があります。
- その他のセキュリティ関連事項については、[サードパーティコールバック概要：セキュリティに関する考慮事項](https://intl.cloud.tencent.com/document/product/1047/34354)ドキュメントをご参照ください。

## コールバックをトリガーするシナリオ

-  Appユーザーは、クライアントを通じてグループメッセージを送信します。
-  App管理者は、REST APIを通じてグループメッセージを送信します。

## コールバックの発生時間

グループメッセージの送信に成功した後。

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
| CallbackCommand | Group.CallbackAfterSendMsgに固定します                       |
| contenttype     | 固定値はJSONです                                             |
| ClientIP        | クライアントIP、形式はたとえば127.0.0.1です                  |
| OptPlatform     | クライアントプラットフォーム、値の選択は、[サードパーティコールバック概要：コールバックプロトコル](https://intl.cloud.tencent.com/document/product/1047/34354)のパラメータOptPlatformの意味を参照します |

### リクエストパッケージの事例

```
{
    "CallbackCommand": "Group.CallbackAfterSendMsg", // コールバックコマンド
    "GroupId": "@TGS#2J4SZEAEL", // グループID
    "Type": "Public", // グループタイプ
    "From_Account": "jared", // 送信者
    "Operator_Account":"admin", // リクエストの送信者
    "Random": 123456, // 乱数
    "MsgSeq": 123, // メッセージ番号
    "MsgTime": 1490686222, // メッセージの時間
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
| MsgSeq           | Integer | メッセージのシーケンス番号、メッセージの一意の識別子<br>グループチャットメッセージはMsgSeqを使用してソートされます。MsgSeqの値が大きいほど、メッセージが遅くなります |
| MsgTime          | Integer | メッセージが送信されたときのタイムスタンプ。バックグラウンドServer時間に対応します |
| OnlineOnlyFlag   | Integer | オンラインメッセージは1、そうでない場合は0となります。ライブブロードキャストグループの場合はこの属性を無視し、デフォルト値の0とします。 |
| MsgBody          | Array   | メッセージボディ。具体的には、[メッセージ形式の説明](https://intl.cloud.tencent.com/document/product/1047/33527)をご参照ください |
| CloudCustomData  | String  | メッセージカスタムデータ（クラウドに保存され、対向側に送信され、プログラムをアンインストールして再インストールした後にプルできます） |
| TopicId          | String  | トピックID、このオプションが使用可能な場合、トピック内の発言を意味します。このオプションは、トピックをサポートするコミュニティにのみ適用されます |
| EventTime        | Integer | イベントトリガーのミリ秒レベルのタイムスタンプ               |

### レスポンスパッケージの事例

Appバックグラウンドでデータ同期を実行した後、コールバックレスポンスパッケージを送信します。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 //コールバック結果を無視します
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
- REST API：[グループでの普通メッセージの送信](https://intl.cloud.tencent.com/document/product/1047/34959)
