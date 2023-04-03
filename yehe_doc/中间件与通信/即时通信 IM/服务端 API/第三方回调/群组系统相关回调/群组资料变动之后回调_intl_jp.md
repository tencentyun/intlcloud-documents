## 機能説明
Appバックグラウンドは、このコールバックを使用して、変更グループ情報のリアルタイム記録（ログの記録、他のシステムへの同期など）など、グループ情報（グループ名、グループ概要、グループ通知、グループプロファイルフォト）の変更をリアルタイムで確認できます。

## 注意事項

- コールバックを有効にするには、コールバックURLを構成し、このコールバックプロトコルに対応するスイッチをオンにする必要があります。構成方法の詳細については、[サードパーティのコールバック構成](https://intl.cloud.tencent.com/document/product/1047/34520)ドキュメントをご参照ください。
- コールバックの方向は、IMバックグラウンドからAppバックグラウンドへのHTTP POSTリクエストを開始することです。
- Appバックグラウンドは、コールバックリクエストを受け取った後、リクエストURLのパラメータSDKAppIDが独自のSDKAppIDであるかどうかを確認する必要があります。
- その他のセキュリティ関連事項については、[サードパーティコールバック概要：セキュリティに関する考慮事項](https://intl.cloud.tencent.com/document/product/1047/34354)ドキュメントをご参照ください。

## コールバックをトリガーするシナリオ

### コールバックをトリガーする内容

グループ情報には、[グループの基本情報](https://intl.cloud.tencent.com/document/product/1047/33529)および[グループディメンションカスタムフィールド](https://intl.cloud.tencent.com/document/product/1047/33529)が含まれます。
現在、グループの基本情報のグループ名、グループ概要、グループ通知、およびグループプロファイルフォトURLが変更された後にこのコールバックをトリガーする場合があります。その他のグループの基本情報は、変更後に一時的にトリガーされません。

### コールバックをトリガーする方法

- Appユーザーは、クライアントを通じてグループ情報を変更します。
- App管理者は、REST APIを通じてグループ情報を変更します。

## コールバックの発生時間

グループの基本情報が変更された後。

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
| CallbackCommand | Group.CallbackAfterGroupInfoChangedに固定されます            |
| contenttype     | 固定値はJSONです                                             |
| ClientIP        | クライアントIP、形式は例えば127.0.0.1です                    |
| OptPlatform     | クライアントプラットフォーム、値の選択は、[サードパーティコールバック概要：コールバックプロトコル](https://intl.cloud.tencent.com/document/product/1047/34354)のパラメータOptPlatformの意味を参照します |

### リクエストパッケージの事例

```
{
    "CallbackCommand": "Group.CallbackAfterGroupInfoChanged", // コールバックコマンド
    "GroupId" : "@TGS#2J4SZEAEL",
    "Type": "Public", // グループタイプ
    "Operator_Account": "leckie", // オペレーター
    "Notification": "NewNotification", // 変更後のグループ通知
    "EventTime":"1670574414123"//ミリ秒レベル、イベントトリガーのタイムスタンプ		
}
```



### リクエストパッケージフィールドの説明

| フィールド       | タイプ  | 説明                                                         |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | コールバックコマンド                                         |
| GroupId          | String  | グループ情報が変更されたグループID                           |
| Type             | String  | グループ情報が変更されたグループ[グループタイプ概要](https://intl.cloud.tencent.com/document/product/1047/33529)、たとえばPublic |
| Operator_Account | String  | オペレーターUserID                                           |
| Name             | String  | 変更後のグループ名                                           |
| Introduction     | String  | 変更後のグループ概要                                         |
| Notification     | String  | 変更後のグループ通知                                         |
| FaceUrl          | String  | 変更後のグループプロファイルフォトURL                        |
| EventTime        | Integer | イベントトリガーのミリ秒レベルのタイムスタンプ               |

### レスポンスパッケージの事例

Appバックグラウンドでグループ情報の変更情報を記録した後、コールバックレスポンスパッケージを送信します。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0  // レスポンス結果を無視します
}
```

### レスポンスパッケージフィールドの説明

| オブジェクト | 概要    | 機能 | 機能                                                         |
| ------------ | ------- | ---- | ------------------------------------------------------------ |
| ActionStatus | String  | 必須 | リクエスト処理の結果、OKは処理が成功したことを意味し、FAILは失敗を意味します。 |
| ErrorCode    | Integer | 必須 | エラーコード、0はレスポンス結果を無視できることを意味します  |
| ErrorInfo    | String  | 必須 | エラーメッセージ                                             |

## 参考

- [サードパーティのコールバック概要](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API：[グループの基本情報の変更](https://intl.cloud.tencent.com/document/product/1047/34962)
