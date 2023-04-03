## 機能説明

アプリのバックグラウンドでは、このコールバックを介してグループメンバーが他のユーザーをグループに招待するリクエストをリアルタイムで確認できます。アプリのバックグラウンドで、グループメンバーが他のユーザーをグループに直接招待するリクエストをブロックすることも可能です。

## 注意事項

- コールバックを有効にするには、コールバックURLを設定し、このコールバックプロトコルに対応するスイッチをオンにする必要があります。設定方法の詳細については、[サードパーティコールバックの設定](https://intl.cloud.tencent.com/document/product/1047/34520)ドキュメントをご参照ください。
- コールバックの方向は、IMバックグラウンドからアプリバックグラウンドへHTTP POSTリクエストを送信するようになっています。
- アプリのバックグラウンドがコールバックリクエストを受信した後、リクエストURLのパラメータSDKAppIDが自分のSDKAppIDであるかどうかを確認する必要があります。
- その他のセキュリティ関連事項については、[サードパーティコールバックの概要：セキュリティに関する考慮事項](https://intl.cloud.tencent.com/document/product/1047/34354)ドキュメントをご参照ください。

## このコールバックをトリガーする可能性のあるシナリオ

- アプリユーザーがクライアントで他のユーザーをグループに招待するリクエストを送信した場合。
- アプリ管理者がREST APIでユーザーをグループに追加した場合。

## コールバックの発生時間

IMバックグラウンドがターゲットユーザーをグループに追加する前（リレーションシップチェーンホスティングが存在し、アプリがIMでフレンドシップ検証を設定している場合、コールバックがフレンドシップ検証の承認後に発生します）。

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
| CallbackCommand | Group.CallbackBeforeInviteJoinGroupという固定値が適用されます |
| contenttype     | JSONという固定値が適用されます                               |
| ClientIP        | クライアントIP。形式の例：127.0.0.1                          |
| OptPlatform     | クライアントプラットフォーム。値の詳細については、[サードパーティコールバックの概要：コールバックプロトコル](https://intl.cloud.tencent.com/document/product/1047/34354)にあるOptPlatformのパラメータの意味をご参照ください |


### リクエストパケットの例

```
 {
    "CallbackCommand": "Group.CallbackBeforeInviteJoinGroup",
    "GroupId": "@TGS#2J4SZEAEL",
    "Type": "Public",
    "Operator_Account": "leckie",
    "DestinationMembers": [
        {
            "Member_Account": "jared"
        },
        {
            "Member_Account": "leckie"
        }
    ],
    "EventTime":"1670574414123"//ミリ秒レベル、イベントのトリガータイムスタンプ		
}
```

### リクエストパケットフィールドの説明

| フィールド         | タイプ  | 説明                                                         |
| ------------------ | ------- | ------------------------------------------------------------ |
| CallbackCommand    | String  | コールバックコマンド                                         |
| GroupId            | String  | 他のユーザーを追加するループID                               |
| Type               | String  | 作成がリクエストされた[グループタイプの概要](https://intl.cloud.tencent.com/document/product/1047/33529)。例：Public |
| Operator_Account   | String  | リクエスト操作者のUserID                                     |
| DestinationMembers | Array   | グループに招待するUserIDの集合                               |
| EventTime          | Integer | イベントがトリガーされるミリ秒レベルのタイムスタンプ         |

### レスポンスパケットの例
#### ユーザー全員のグループ参加の許可

アプリのバックグラウンドで、すべてのリクエストに関連するすべてのユーザーのグループ参加を許可します。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // グループへの参加リクエストの処理の続行を許可することを示す
}
```

#### 一部のメンバーのグループ参加のブロック

アプリのバックグラウンドで一部のユーザーをグループに招待するリクエストを拒否し、RefusedMembers_AccountでこれらのIdentifierを返します。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "RefusedMembers_Account": [ // 参加を拒否したユーザーのリスト
        "jared"
    ]
}
```

### レスポンスパケットフィールドの説明

| フィールド             | タイプ  | 属性 | 説明                                                         |
| ---------------------- | ------- | ---- | ------------------------------------------------------------ |
| ActionStatus           | String  | 必須 | リクエスト処理の結果。OKは処理に成功したことを意味し、FAILは失敗したことを意味します |
| ErrorCode              | Integer | 必須 | エラーコード。0はグループへの参加リクエストの処理の続行を許可することを示します。1はそのリクエストを拒否することを示します。サービスニーズに応じて、エラーコードを指定してユーザーのグループへの参加を拒否する必要がある場合は、エラーコード「ErrorCode」と「ErrorInfo」をクライアントに送信し、エラーコード「ErrorCode」を[10100,10200]の範囲内にある値に設定してください |
| ErrorInfo              | String  | 必須 | エラー情報                                                   |
| RefusedMembers_Account | Array   | 任意 | 参加を拒否したユーザーIDの集合                               |

## 参照情報

- [サードパーティコールバックの概要](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API：[グループメンバーの追加](https://intl.cloud.tencent.com/document/product/1047/34921)
