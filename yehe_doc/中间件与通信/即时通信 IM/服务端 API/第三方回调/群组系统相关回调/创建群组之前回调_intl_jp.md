## 機能説明

Appバックグラウンドは、このコールバックを使用して、ユーザーのグループを作成するリクエストをバックグラウンドで拒否できるなど、ユーザーのグループを作成するリクエストをリアルタイムで確認できます。

## 注意事項

- コールバックを有効にするには、コールバックURLを構成し、このコールバックプロトコルに対応するスイッチをオンにする必要があります。構成方法の詳細については、[サードパーティのコールバック構成](https://intl.cloud.tencent.com/document/product/1047/34520)ドキュメントをご参照ください。
- コールバックの方向は、IMバックグラウンドからAppバックグラウンドへのHTTP POSTリクエストを開始することです。
- Appバックグラウンドは、コールバックリクエストを受け取った後、リクエストURLのパラメータSDKAppIDが独自のSDKAppIDであるかどうかを確認する必要があります。
- その他のセキュリティ関連事項については、[サードパーティコールバック概要：セキュリティに関する考慮事項](https://intl.cloud.tencent.com/document/product/1047/34354)ドキュメントをご参照ください。

## コールバックをトリガーするシナリオ

- Appユーザーは、クライアントを通じてグループを作成します
- App管理者は、REST APIを通じてグループを作成します

## コールバックの発生時間

IMバックグラウンドでグループを作成する準備が整う前。

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
| CallbackCommand | Group.CallbackBeforeCreateGroupに固定します                  |
| contenttype     | 固定値はJSONです                                             |
| ClientIP        | クライアントIP、形式はたとえば127.0.0.1です                  |
| OptPlatform     | クライアントプラットフォーム、値の選択は、[サードパーティコールバック概要：コールバックプロトコル](https://intl.cloud.tencent.com/document/product/1047/34354)のパラメータOptPlatformの意味を参照します |

### リクエストパッケージの事例

```
{
    "CallbackCommand": "Group.CallbackBeforeCreateGroup", // コールバックコマンド
    "Operator_Account": "leckie", // オペレーター
    "Owner_Account": "leckie", // グループマスター
    "Type": "Public", // グループタイプ
    "Name": "MyFirstGroup", // グループ名
    "CreateGroupNum": 123, //このユーザーが作成した類似グループの数
    "MemberList": [ // 初期メンバーリスト
        {
            "Member_Account": "bob"
        },
        {
            "Member_Account": "peter"
        }
    ],
    "EventTime":"1670574414123"//ミリ秒レベル、イベントトリガーのタイムスタンプ
}
```

### リクエストパッケージフィールドの説明

| オブジェクト     | 概要    | 機能                                                         |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | コールバックコマンド                                         |
| Operator_Account | String  | グループ作成要求を開始したオペレーターUserID                 |
| Owner_Account    | String  | 作成がリクエストされたグループのグループマスターUserID       |
| Type             | String  | グループメッセージを生成する[グループタイプ概要](https://intl.cloud.tencent.com/document/product/1047/33529)、たとえばPublic |
| Name             | String  | 作成がリクエストされたグループ名                             |
| CreateGroupNum   | Integer | このユーザーが作成した類似グループの数                       |
| MemberList       | Array   | 作成がリクエストされたグループの初期化メンバーリスト         |
| EventTime        | Integer | イベントトリガーのミリ秒レベルのタイムスタンプ               |

### レスポンスパッケージの事例

#### 作成の許可

ユーザーがグループを作成することは許可されます。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // 作成は許可されます
}
```

#### 作成の拒否

ユーザーがグループを作成することは許可されていません。グループは作成されず、呼び出し元にエラーコード`10016`が返されます。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 1 // 作成は拒否されます
}
```

### レスポンスパッケージフィールドの説明

| フィールド   | タイプ  | 属性 | 説明                                                         |
| ------------ | ------- | ---- | ------------------------------------------------------------ |
| ActionStatus | String  | 必須 | リクエスト処理の結果、OKは処理が成功したことを意味し、FAILは失敗を意味します |
| ErrorCode    | Integer | 必須 | エラーコード。0は作成を許可、1は作成を拒否することを意味します。業務が独自のエラーコードを使用してユーザーのグループ作成を拒否したい場合は、エラーコードErrorCodeおよびErrorInfoをクライアントに渡します。エラーコードErrorCodeを[10100, 10200]の範囲内に設定してください |
| ErrorInfo    | String  | 必須 | エラーメッセージ                                             |

## 参考

- [サードパーティのコールバック概要](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API：[グループの作成](https://intl.cloud.tencent.com/document/product/1047/34895)
