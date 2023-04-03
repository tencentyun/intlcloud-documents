## 機能説明

アプリのバックグラウンドでは、このコールバックを介してユーザーが作成したグループの情報をリアルタイムで確認できます。アプリのバックグラウンドにグループが正常に作成されたことが通知された場合、アプリのバックグラウンドでは、これに基づいてデータ同期などの操作を実行できます。

## 注意事項

- コールバックを有効にするには、コールバックURLを設定し、このコールバックプロトコルに対応するスイッチをオンにする必要があります。設定方法の詳細については、[サードパーティコールバックの設定](https://intl.cloud.tencent.com/document/product/1047/34520)ドキュメントをご参照ください。
- コールバックの方向は、IMバックグラウンドからアプリバックグラウンドへHTTP POSTリクエストを送信するようになっています。
- アプリのバックグラウンドがコールバックリクエストを受信した後、リクエストURLのパラメータSDKAppIDが自分のSDKAppIDであるかどうかを確認する必要があります。
- その他のセキュリティ関連事項については、[サードパーティコールバックの概要：セキュリティに関する考慮事項](https://intl.cloud.tencent.com/document/product/1047/34354)ドキュメントをご参照ください。

## このコールバックをトリガーする可能性のあるシナリオ

- アプリユーザーがクライアントでグループを正常に作成した場合。
- アプリ管理者がREST APIでグループを正常に作成した場合。

## コールバックの発生時間

グループを正常に作成した後。

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
| CallbackCommand | Group.CallbackAfterCreateGroupという固定値が適用されます     |
| contenttype     | JSONという固定値が適用されます                               |
| ClientIP        | クライアントIP。形式の例：127.0.0.1                          |
| OptPlatform     | クライアントプラットフォーム。値の詳細については、[サードパーティコールバックの概要：コールバックプロトコル](https://intl.cloud.tencent.com/document/product/1047/34354)にあるOptPlatformのパラメータの意味をご参照ください |

### リクエストパケットの例

```
 {
    "CallbackCommand": "Group.CallbackAfterCreateGroup", // コールバックコマンド
    GroupId": "@TGS#2J4SZEAEL",
    "Operator_Account": "group_root", // 操作者
    "Owner_Account": "leckie", // グループオーナー
    "Type": "Public", // グループタイプ
    "Name": "MyFirstGroup", // グループ名
    "MemberList": [ // 初期メンバーのリスト
        {
            "Member_Account": "bob"
        },
        {
            "Member_Account": "peter"
        }
    ],
    "UserDefinedDataList": [ //ユーザーのグループ作成時のカスタムフィールド
        {
            "Key": "UserDefined1",
            "Value": "hello"
        },
        {
            "Key": "UserDefined2",
            "Value": "world"
        }
    ],
    "EventTime":"1670574414123"//ミリ秒レベル、イベントのトリガータイムスタンプ		
}
```

### リクエストパケットフィールドの説明

| フィールド          | タイプ  | 説明                                                         |
| ------------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand     | String  | コールバックコマンド                                         |
| GroupId             | String  | 操作のグループID                                             |
| Operator_Account    | String  | グループを作成するリクエストを送信した操作者のUserID         |
| Owner_Account       | String  | 作成をリクエストするグループのグループオーナーのUserID       |
| Type                | String  | 作成がリクエストされた[グループタイプの概要](https://intl.cloud.tencent.com/document/product/1047/33529)。例：Public |
| Name                | String  | 作成をリクエストするグループの名前                           |
| MemberList          | Array   | 作成をリクエストするグループの初期メンバーリスト             |
| UserDefinedDataList | Array   | ユーザーがグループを作成するときのカスタムフィールド。このフィールドはデフォルトで使用されないため、有効にする必要があります。詳細については、[カスタムフィールド](https://www.tencentcloud.com/document/product/1047/33530#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5)をご参照ください |
| EventTime           | Integer | イベントがトリガーされるミリ秒レベルのタイムスタンプ         |

### レスポンスパケットの例

アプリのバックグラウンドでデータを同期した後、レスポンスパケットを送信します。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // コールバック結果を無視
}
```

### レスポンスパケットフィールドの説明

| フィールド   | タイプ  | 属性 | 説明                                                         |
| ------------ | ------- | ---- | ------------------------------------------------------------ |
| ActionStatus | String  | 必須 | リクエスト処理の結果。OKは処理に成功したことを意味し、FAILは失敗したことを意味します |
| ErrorCode    | Integer | 必須 | エラーコード。ここで、0はレスポンス結果の無視をすることを意味します |
| ErrorInfo    | String  | 必須 | エラー情報                                                   |

## 参照情報
- [サードパーティコールバックの概要](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API：[グループの作成](https://intl.cloud.tencent.com/document/product/1047/34895)
