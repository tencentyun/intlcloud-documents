
## SDK内蔵インターフェースのエラーコード
例：`https://webar.qcloud.com/sdk/verify`などの `webar.qcloud.com/sdk/xxx`インターフェースのエラーコードがあります。
Responseの返送構造：

```js
{
    "Code": xxx,
    "Message": "xxx"
}
```


### 成功 
 Codeが0の場合は成功を表します。データがある場合、Dataには対応するデータがあります。

```json
{
    Code: 0,
    Data:{...}
}
```


### 認証エラー
 Codeの100 -- 104は認証エラーです。response Statusは401です。
```json
{
  "100":{
    zh: "認証パラメータがありません"
  },
  "101":{
    zh: "signatureタイムアウト"
  },
  "102":{
    zh: "ユーザーが見つかりません"
  },
  "103":{
    zh: "signatureエラー"
  },
  "104":{
    zh: "refererまたはWeChatAppIdがマッチングしません"
  }
}
 

```

### 入力パラメータエラー
Code = -2は入力パラメータ検証エラーです。Messageに対応する説明があります。

```json

{
    "Code": -2,
    "Message": "LicenseKeyフィールドは文字列である必要があります"
}
```

### 業務検証エラー
Code > 1000は業務検証エラーです。Messageに対応する説明があります：

```json
{
    "Code": 2007,
    "Message": "この項目は存在しません"
}
```

### 不明なエラー
Code = -1は不明なエラーです。
```json
{
    "Code": -1,
    "Message": "不明なエラー"
}
```
