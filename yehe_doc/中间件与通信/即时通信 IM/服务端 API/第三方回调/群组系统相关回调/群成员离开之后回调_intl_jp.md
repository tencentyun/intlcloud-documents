## 機能説明

アプリのバックグラウンドでは、このコールバックを介して、ユーザーがグループから退出する状況をリアルタイムで確認できます。これには、ユーザーのグループ退出の、リアルタイムでの記録（ログの記録、他のシステムとの同期など）が含まれます。

## 注意事項

- コールバックを有効にするには、コールバックURLを設定し、このコールバックプロトコルに対応するスイッチをオンにする必要があります。設定方法の詳細については、[サードパーティコールバックの設定](https://intl.cloud.tencent.com/document/product/1047/34520)ドキュメントをご参照ください。
- コールバックの方向は、IMバックグラウンドからアプリバックグラウンドへHTTP POSTリクエストを送信するようになっています。
- アプリのバックグラウンドがコールバックリクエストを受信した後、リクエストURLのパラメータSDKAppIDが自分のSDKAppIDであるかどうかを確認する必要があります。
- その他のセキュリティ関連事項については、[サードパーティコールバックの概要：セキュリティに関する考慮事項](https://intl.cloud.tencent.com/document/product/1047/34354)ドキュメントをご参照ください。

## このコールバックをトリガーする可能性のあるシナリオ

- アプリユーザーがクライアントでグループから退出する。
- アプリユーザーがクライアントで他のグループメンバーを強制退出させる。
- アプリ管理者がREST APIでグループメンバーを削除する。

## コールバックの発生時間

ユーザーがグループから自主的に退出した、またはグループの所有者/管理者によってグループから強制退出させた後。

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
| https           | リクエストプロトコルはHTTPS、リクエストメソッドはPOSTです。  |
| www.example.com | コールバックURL。                                            |
| SdkAppid        | アプリケーションの作成時にIMコンソールで割り当てられたSDKAppID |
| CallbackCommand | Group.CallbackAfterMemberExitという固定値が適用されます      |
| contenttype     | JSONという固定値が適用されます                               |
| ClientIP        | クライアントIP。形式の例：127.0.0.1                          |
| OptPlatform     | クライアントプラットフォーム。値の詳細については、[サードパーティコールバックの概要：コールバックプロトコル](https://intl.cloud.tencent.com/document/product/1047/34354)にあるOptPlatformのパラメータの意味をご参照ください。 |

### リクエストパケットの例

```
{
    "CallbackCommand": "Group.CallbackAfterMemberExit", // コールバックコマンド
    "GroupId": "@TGS#2J4SZEAEL", // グループID
    "Type": "Public", // グループタイプ
    "ExitType": "Kicked", // メンバーの退出の形：Kicked-強制退出、Quit-自分がグループから退出
    "Operator_Account": "leckie", // 操作者
    "ExitMemberList": [ // グループを退出したメンバーのリスト
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
| GroupId          | String  | グループメッセージが生成されるグループID                     |
| Type             | String  | グループメッセージが生成される[グループタイプの概要](https://intl.cloud.tencent.com/document/product/1047/33529)。例：Public |
| ExitType         | String  | メンバーの退出方法：Kickedはグループオーナーに強制退出させたこと、Quitは自分からグループを退出することを意味します |
| Operator_Account | String  | グループ退出者のUserID                                       |
| ExitMemberList   | Array   | グループを退出したメンバーのリスト                           |
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
-[新しいメンバーによるグループ参加後のコールバック](https://intl.cloud.tencent.com/document/product/1047/34372)
- [ライブストリーミングオンライン状態のコールバック](https://intl.cloud.tencent.com/document/product/1047/48734)
- REST API：[グループメンバーの削除](https://intl.cloud.tencent.com/document/product/1047/34949)
