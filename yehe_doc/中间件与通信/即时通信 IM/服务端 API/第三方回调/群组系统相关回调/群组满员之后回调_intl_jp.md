## 機能説明

Appバックグラウンドは、このコールバックを使用して、ユーザーがグループに参加できるために、非アクティブなグループメンバーを削除するなど、グループ満員のダイナミックをリアルタイムで確認できます。

## 注意事項

- コールバックを有効にするには、コールバックURLを構成し、このコールバックプロトコルに対応するスイッチをオンにする必要があります。構成方法の詳細については、[サードパーティのコールバック構成](https://intl.cloud.tencent.com/document/product/1047/34520)ドキュメントをご参照ください。
- コールバックの方向は、IMバックグラウンドからAppバックグラウンドへのHTTP POSTリクエストを開始することです。
- Appバックグラウンドは、コールバックリクエストを受け取った後、リクエストURLのパラメータSDKAppIDが独自のSDKAppIDであるかどうかを確認する必要があります。
- その他のセキュリティ関連事項については、[サードパーティコールバック概要：セキュリティに関する考慮事項](https://intl.cloud.tencent.com/document/product/1047/34354)ドキュメントをご参照ください。

## コールバックをトリガーするシナリオ

- Appユーザーは、クライアント申請を通じてグループに参加します。
- Appユーザーは、クライアント招待を通じてグループに参加します。
- App管理者は、REST APIを通じてグループメンバーを追加します。

## コールバックの発生時間

新しいメンバーが参加した後にグループ満員になったか、またはグループ満員になったため新しいメンバーの参加に失敗した後。

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
| SdkAppid        | アプリケーション作成時にIMコンソールでアサインされたSDKAppID |
| CallbackCommand | Group.CallbackAfterGroupFullに固定されます                   |
| contenttype     | 固定値はJSONです                                             |
| ClientIP        | クライアントIP、形式はたとえば127.0.0.1です                  |
| OptPlatform     | クライアントプラットフォーム、値の選択は、[サードパーティコールバック概要：コールバックプロトコル](https://intl.cloud.tencent.com/document/product/1047/34354)のパラメータOptPlatformの意味を参照します |

### リクエストパッケージの事例

```
{
    "CallbackCommand": "Group.CallbackAfterGroupFull", // コールバックコマンド
    "GroupId": "@TGS#2J4SZEAEL", // グループID
    "EventTime":"1670574414123"//ミリ秒レベル、イベントトリガーのタイムスタンプ		
}
```

### リクエストパッケージフィールドの説明

| フィールド      | タイプ  | 説明                                           |
| --------------- | ------- | ---------------------------------------------- |
| CallbackCommand | String  | コールバックコマンド                           |
| GroupId         | String  | 満員のグループID                               |
| EventTime       | Integer | イベントトリガーのミリ秒レベルのタイムスタンプ |

### レスポンスパッケージの事例

Appバックグラウンドでグループ満員情報を記録した後、コールバックレスポンスパッケージを送信します。

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // レスポンス結果を無視します
}
```

### レスポンスパッケージフィールドの説明

| フィールド   | タイプ  | 属性 | 説明                                                         |
| ------------ | ------- | ---- | ------------------------------------------------------------ |
| ActionStatus | String  | 必須 | リクエスト処理の結果、OKは処理が成功したことを意味し、FAILは失敗を意味します |
| ErrorCode    | Integer | 必須 | エラーコード、0はレスポンス結果を無視できることを意味します  |
| ErrorInfo    | String  | 必須 | エラーメッセージ                                             |


## 参考

- [サードパーティのコールバック概要](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API：[グループメンバーの削除](https://intl.cloud.tencent.com/document/product/1047/34949)
- REST API：[グループメンバーの追加](https://intl.cloud.tencent.com/document/product/1047/34921)
