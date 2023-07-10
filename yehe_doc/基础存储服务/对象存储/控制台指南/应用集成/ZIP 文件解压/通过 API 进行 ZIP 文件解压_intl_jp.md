## 準備作業

1. ZIPファイルの解凍機能は、Serverless Cloud Function（SCF）を介して実装されています。 使用する前に、COSコンソールの[ZIPファイルの解凍](https://console.cloud.tencent.com/cos5/application/cosGunzipApi)で**ZIPファイルの解凍**関数を作成する必要があります。作成ガイドについては、[ZIPファイルの解凍](https://intl.cloud.tencent.com/document/product/436/45163)をご参照ください。
2. 関数を作成したら、関数リストのアクションバーの**使用ガイド**に従って、関数パラメータの設定を完了します。設定が必要な具体的な関数パラメータについては、下記をご参照ください。形式は**JSON文字列**です。
 - SCF認証を選択する関数の場合、SCFが提供する[実行関数(Invoke)インターフェース](https://intl.cloud.tencent.com/document/product/583/17243)を呼び出して、SCFを実行する必要があります。そのうちClientContextパラメータは、JSON形式で渡されます。[関数パラメータの設定例](#1)をご参照ください。
 - 認証免除を選択した関数の場合、対応するAPI Gatewayに直接HTTPリクエストを行うことで関数を呼び出すことができます。


<span id=1></span>
## 関数パラメータの設定例

>? 実際に使用する際は、コードからコメントを削除する必要があります。
>

```plaintext
{
    "bucket": "examplebucket-1250000000",    // ZIPパッケージを保存するソースバケット
    "region": "ap-guangzhou",         // ZIPパッケージを保存するソースバケットが配置されているリージョン
    "key": "example.zip",              //  ZIPパッケージ名
    "targetBucket": "examplebucket-1250000000",    // 解凍生成物を最終的に配布するターゲットバケット
    "targetRegion": "ap-guangzhou",         // 解凍生成物を最終的に配布するターゲットバケットが配置されているリージョン
    "targetPrefix": "target/",              // 解凍生成物を最終的に配布するプレフィックス
}
```

パラメータの説明は次のとおりです。

| パラメータ名       | パラメータの説明                   | タイプ   | 入力必須かどうか |
| ------------ | ------------------------------------------------------------ | ------ | -------- |
| bucket       | ZIPパッケージが保存されているソースバケットで、命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式である必要があります。例：examplebucket-1250000000 | String | はい       |
| region       | ZIPパッケージのソースバケットが配置されているリージョンです。列挙値については、[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください | String | はい       |
| key          | ZIPパッケージ名（Object名）、バケット内のオブジェクトの一意の識別子です。詳細については、[オブジェクトの概要](https://intl.cloud.tencent.com/document/product/436/13324)をご参照ください | String | はい       |
| targetBucket | 解凍生成物を最終的に配布するターゲットバケットで、命名形式はBucketName-APPIDです。ここに入力するバケット名は、この形式である必要があります。例：examplebucket-1250000000 | String | はい       |
| targetRegion | 解凍生成物を最終的に配布するターゲットバケットが配置されているリージョンです。列挙値については、[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください | String | はい       |
| targetPrefix | 解凍生成物を最終的に配布するプレフィックスで、指定されたディレクトリへ配布しスラッシュ/で終了します。デフォルトまたは空の文字列は、ルートパスへの配布と見なされます | String | いいえ       |

## 関数応答結果の例
```plaintext
{
    "code": 0,
    "message": "cos gunzip file success",
    "data": {
        "Bucket": "examplebucket-1250000000",
        "Region": "ap-guangzhou"
    }
}
```

応答パラメータの説明は次のとおりです。

| パラメータ名  | パラメータの説明                                                      | タイプ             |
| ------- | ------------------------------------------------------------ | ---------------- |
| code    | ビジネスエラーコード。0の場合は実行に成功し、それ以外の場合は実行に失敗します          | Number           |
| message | 実行結果のテキスト記述、nullの可能性があります                              | String           |
| data    | 実行成功の情報です。実行が成功した場合は、解凍生成物が最終的に配布されるターゲットバケットの情報が含まれます | Object           |
| error   | 実行のエラー情報です。実行が成功した場合はnullになります                          | Object or String |

## 実際の例

### 事例1：*.zipファイルの解凍

#### パラメータ設定

```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "example.zip",
  "targetBucket": "examplebucket-1250000000",
  "targetRegion": "ap-guangzhou",
  "targetPrefix": "target/"
}
```

#### 解凍生成物の最終的な場所

```plaintext
target/example.txt
```
