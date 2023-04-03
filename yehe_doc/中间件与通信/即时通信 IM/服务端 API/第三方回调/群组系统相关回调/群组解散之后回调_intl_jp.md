## 機能説明

アプリのバックグラウンドでは、このコールバックを介して、グループ解散のリアルタイム記録（ログの記録、他のシステムとの同期など）をリアルタイムで確認できます。

## 注意事項

- コールバックを有効にするには、コールバックURLを設定し、このコールバックプロトコルに対応するスイッチをオンにする必要があります。設定方法の詳細については、[サードパーティコールバックの設定](https://intl.cloud.tencent.com/document/product/1047/34520)ドキュメントをご参照ください。
- コールバックの方向は、IMバックグラウンドからアプリバックグラウンドへHTTP POSTリクエストを送信するようになっています。
- アプリのバックグラウンドがコールバックリクエストを受信した後、リクエストURLのパラメータSDKAppIDが自分のSDKAppIDであるかどうかを確認する必要があります。
- その他のセキュリティ関連事項については、[サードパーティコールバックの概要：セキュリティに関する考慮事項](https://intl.cloud.tencent.com/document/product/1047/34354)ドキュメントをご参照ください。

## このコールバックをトリガーする可能性のあるシナリオ

- アプリユーザーがクライアントでグループを解散する。
- アプリ管理者がREST APIでグループを解散する。

## コールバックの発生時間

グループ解散後。

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
| CallbackCommand | 固定値：Group.CallbackAfterGroupDestroyed。                  |
| contenttype     | JSONという固定値が適用されます                               |
| ClientIP        | クライアントIP。形式の例：127.0.0.1                          |
| OptPlatform     | クライアントプラットフォーム。値の詳細については、[サードパーティコールバックの概要：コールバックプロトコル](https://intl.cloud.tencent.com/document/product/1047/34354)にあるOptPlatformのパラメータの意味をご参照ください |

### リクエストパケットの例

```
{
    "CallbackCommand": "Group.CallbackAfterGroupDestroyed", // コールバックコマンド
    GroupId": "@TGS#2J4SZEAEL", 
    "Type": "Public", // グループタイプ
    "Owner_Account": "leckie", // グループオーナー
    "Name": "MyFirstGroup", // グループ名
    "MemberList" : [ //解散されたグループ内のメンバー
        {
            "Member_Account": "leckie"
        },
        {
            "Member_Account": "peter"
        },
        {
            "Member_Account": "bob"
        }
    ],
    "EventTime":"1670574414123"//ミリ秒レベル、イベントのトリガータイムスタンプ		
}
```

### リクエストパケットフィールドの説明

| フィールド      | タイプ  | 説明                                                         |
| --------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand | String  | コールバックコマンド                                         |
| GroupId         | String  | 解散されたグループID                                         |
| Type            | String  | 解散されたグループの[グループタイプの概要](https://intl.cloud.tencent.com/document/product/1047/33529)。例：Public |
| Owner_Account   | String  | グループオーナーのUserID                                     |
| MemberList      | Array   | 解散されたグループのメンバーリスト。コミュニティはこのフィールドを返しません |
| EventTime       | Integer | イベントがトリガーされるミリ秒レベルのタイムスタンプ         |

### レスポンスパケットの例

アプリのバックグラウンドがグループの解散情報を記録した後、コールバックのレスポンスパケットを送信します。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### レスポンスパケットフィールドの説明

| フィールド   | タイプ  | 属性 | 説明                                                         |
| ------------ | ------- | ---- | ------------------------------------------------------------ |
| ActionStatus | String  | 必須 | リクエスト処理の結果。OKは処理に成功したことを意味し、FAILは失敗したことを意味します |
| ErrorCode    | Integer | 必須 | エラーコード。0に設定することをお勧めします。このコールバックは、グループ解散後にユーザーに通知するために使用されます。ユーザーのエラーコード値は、グループ解散の通常のプロセスには影響しません |
| ErrorInfo    | String  | 必須 | エラー情報                                                   |

## 参照情報

- [サードパーティコールバックの概要](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API：[グループの解散](https://intl.cloud.tencent.com/document/product/1047/34896)
