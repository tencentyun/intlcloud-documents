## 機能説明

アプリのバックグラウンドでは、このコールバックを介してグループメンバーの参加に関するメッセージをリアルタイムで確認できます。メンバーがグループに参加したことがアプリのバックグラウンドに通知されたときに、アプリはそれに応じて必要なデータ同期を実行できます。

## 注意事項

- コールバックを有効にするには、コールバックURLを設定し、このコールバックプロトコルに対応するスイッチをオンにする必要があります。設定方法の詳細については、[サードパーティコールバックの設定](https://intl.cloud.tencent.com/document/product/1047/34520)ドキュメントをご参照ください。
- コールバックの方向は、IMバックグラウンドからアプリバックグラウンドへHTTP POSTリクエストを送信するようになっています。
- アプリのバックグラウンドがコールバックリクエストを受信した後、リクエストURLのパラメータSDKAppIDが自分のSDKAppIDであるかどうかを確認する必要があります。
- その他のセキュリティ関連事項については、[サードパーティコールバックの概要：セキュリティに関する考慮事項](https://intl.cloud.tencent.com/document/product/1047/34354)ドキュメントをご参照ください。

## このコールバックをトリガーする可能性のあるシナリオ

- アプリユーザーがクライアントでグループへの参加を自主的に申請した後、申請が承認された場合。
- アプリユーザーがクライアントで他のメンバーをグループに招待した後、そのメンバーがグループに正常に参加した場合。
- アプリ管理者がREST APIでユーザーをグループに追加した場合。

## コールバックの発生時間

- ユーザーがグループへの参加を申請し、グループに正常に参加した後。
- ユーザーが他のメンバーから招待され、グループに参加した後。
- アプリ管理者がREST APIでユーザーをグループに追加した後。

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
| CallbackCommand | CallbackAfterNewMemberJoinという固定値が適用されます         |
| contenttype     | JSONという固定値が適用されます                               |
| ClientIP        | クライアントIP。形式の例：127.0.0.1                          |
| OptPlatform     | クライアントプラットフォーム。値の詳細については、[サードパーティコールバックの概要：コールバックプロトコル](https://intl.cloud.tencent.com/document/product/1047/34354)にあるOptPlatformのパラメータの意味をご参照ください |

### リクエストパケットの例

```
{
    "CallbackCommand": "Group.CallbackAfterNewMemberJoin", // コールバックコマンド
    GroupId": "@TGS#2J4SZEAEL",
    "Type": "Public", // グループタイプ
    "JoinType": "Apply", // グループへの参加方法：Apply（グループへの参加を申請）、Invited（招待を受けてグループに参加）
    "Operator_Account": "leckie", // 操作者メンバー
    "NewMemberList": [ // グループに参加した新しいメンバーのリスト
        {
            "Member_Account": "jared"
        },
        {
            "Member_Account": "tommy"
        }
    ],
    "EventTime":"1670574414123"//ミリ秒レベル、イベントのトリガータイムスタンプ		
}
```

### リクエストパケットフィールドの説明

| フィールド       | タイプ  | 説明                                                         |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | コールバックコマンド                                         |
| GroupId          | String  | 他のユーザーを追加するループID                               |
| Type             | String  | 作成がリクエストされた[グループタイプの概要](https://intl.cloud.tencent.com/document/product/1047/33529)。例：Public |
| JoinType         | String  | グループへの参加方法：Apply（グループへの参加を申請）、Invited（招待を受けてグループに参加） |
| Operator_Account | String  | リクエスト操作者のUserID。                                   |
| NewMemberList    | Array   | グループに参加した新しいメンバーのUserIDの集合               |
| EventTime        | Integer | イベントがトリガーされるミリ秒レベルのタイムスタンプ         |

### レスポンスパケットの例

アプリのバックグラウンドでデータを同期した後、レスポンスパケットを返します。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // レスポンス結果を無視
}
```

### レスポンスパケットフィールドの説明

| フィールド   | タイプ  | 属性 | 説明                                                         |
| ------------ | ------- | ---- | ------------------------------------------------------------ |
| ActionStatus | String  | 必須 | リクエスト処理の結果。OKは処理に成功したことを意味し、FAILは失敗したことを意味します |
| ErrorCode    | Integer | 必須 | エラーコード。0はレスポンス結果の無視を許可することを意味します |
| ErrorInfo    | String  | 必須 | エラー情報                                                   |

## 参照情報

- [サードパーティコールバックの概要](https://intl.cloud.tencent.com/document/product/1047/34354)
- [グループメンバーが離れた後のコールバック](https://intl.cloud.tencent.com/document/product/1047/34373)
- [ライブストリーミングオンライン状態のコールバック](https://intl.cloud.tencent.com/document/product/1047/48734)
- REST API：[グループメンバーの追加](https://intl.cloud.tencent.com/document/product/1047/34921)
