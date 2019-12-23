## API説明
このAPI（GetFederationToken）は、統合身元の一時的アクセス認証情報を取得するために使用されます。
リクエストドメイン名：

```
sts.api.qcloud.com
```

## 入力パラメータ
以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

|フィールド|必須項目|タイプ|説明|
| ------------ | ------------ | ------------ | ------------ |
|name|はい|String|統合身元ユーザーのニックネーム|
|policy|はい|String|ポリシーの説明</br>**注意：**</br>1. policyはurlencodeを実行する必要があります（GET方法でクラウドAPIをリクエストする場合、リクエストを送信する前に、すべてのパラメータをクラウドAPI仕様に従ってもう一度urlencodeする必要があります。</br>2. ポリシー構文は[CAMポリシー構文](https://intl.cloud.tencent.com/document/product/598/10603)を参照してください。</br>3. ポリシーにprincipal要素を含めることはできません。|
|durationSeconds|いいえ|Int|一時的証明書の有効期間を指定します。単位は秒、デフォルトは1800秒、最大有効期間は7200秒です|

## 出力パラメータ

| フィールド  | タイプ  | 説明  |
| ------------ | ------------ | ------------ |
|  credentials | [credentials](#dataStructure)  | オブジェクトにtoken、tmpSecretId、tmpSecretKeyトライアドが含まれています  |
|  expiredTime | Int  | 証明書の無効時間、秒までの正確なUnixタイムスタンプを返します  |

<span id="dataStructure"></span>
## Credentialsデータ構造

| フィールド  | タイプ  | 説明  |
|---------|---------|---------|
| token | String | token 値 |
| tmpSecretId | String | 一時的セキュリティ証明書ID |
| tmpSecretKey | String | 一時的セキュリティ証明書Key |

## 例
### 入力

```
https://sts.api.qcloud.com/v2/index.php?Action=GetFederationToken&name=nickName&policy=%7b%22version%22%3a%222.0%22%2c%22statement%22%3a%5b%7b%22action%22%3a%5b%22name%2fqcisa%3aGetInfoByFields%22%5d%2c%22resource%22%3a%5b%22qcs%3a%3aqcisa%3a%3auin%2f90000000000%3aqcisa%2fbigCustomerDetail%22%2c%22qcs%3a%3aqcisa%3a%3auin%2f90000000000%3aqcisa%2fuserDetail%22%2c%22qcs%3a%3aqcisa%3a%3auin%2f90000000000%3aqcisa%2fauthDetail%22%5d%2c%22effect%22%3a%22allow%22%7d%5d%7d&durationSeconds=1800&<共通リクエストパラメータ>
```

### 出力

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "credentials": {
            "sessionToken": "9586a03c55b6cc088fb63461e88b4d4b5ceaeebf3",
            "tmpSecretId": "AKIDTs591htUbXKwmQryzpTvBF7nHZgdOlvv",
            "tmpSecretKey": "xjJhtujMq8E8tTcfbTFuRq8JMI7pQtHY"
        },
        "expiredTime": 1494309923
    }
}
```

