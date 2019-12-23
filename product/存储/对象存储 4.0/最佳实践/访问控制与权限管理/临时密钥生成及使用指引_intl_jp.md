## 一時暗号鍵

一時暗号鍵は、CAM Cloud APIによって提供されるAPIを介して取得された権限が制限される暗号鍵です。<br>
 COS APIは、一時暗号鍵を使用して署名を計算でき、COS APIリクエストを開始するために使用されます。<br>
 COS APIリクエストを送信するときリクエスト例に一時暗号鍵の署名を含む必要があります。一時暗号鍵を取得するAPIによって返される情報内の3つのフィールドを使用する必要があります。3つのフィールドは下記のとおりです。
- `tmpSecretId`
- `tmpSecretKey`
- `sessionToken`

## 一時暗号鍵を使用する優位性

COSシナリオがWeb、iOS、Androidで使用されている場合、固定暗号鍵によって署名を計算する方式は権限を効果的に制御できず、同時に、永続暗号鍵をクライアントのコードに入れると、漏れるリスクが非常に高いです。一時暗号鍵の方式を採用すれば、権限制御問題を簡単かつ効果的に解決できます。
例えば、一時暗号鍵を申請するプロセスにおいて、権限ポリシー [policy](https://cloud.tencent.com/document/product/436/31923#policy) フィールドを設定して、操作とリソースを制限することによって、権限を指定された範囲内に制限できます。

COS API権限付与ポリシーについては、以下を参照してください。
- [COS API一時暗号鍵の権限付与ポリシーのガイド](https://cloud.tencent.com/document/product/436/31923)
- [一般的なシナリオにおける一時暗号鍵の権限ポリシーの例](https://cloud.tencent.com/document/product/436/31923#.E5.B8.B8.E8.A7.81.E5.9C.BA.E6.99.AF.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5)

## 一時暗号鍵の取得

一時暗号鍵を提供される[COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk) 方式によって取得できますが、STSクラウドAPIを直接的にリクエストすることによっても取得できます。

### COS STS SDK

COSはSTSに対してSDKと例を提供します。現在Java、Nodejs、PHP、Pythonなどの複数の言語の例があります。
詳細については、[COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk)を参照してください。各SDKの使用説明については、Github上のREADMEと例を参照してください。

COS STS SDKによって提供される[Java SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java)を例とし、一時暗号鍵を取得する例は以下のとおりです：

```java
import com.qcloud.Utilities.Json.JSONObject;

public class Demo {
    public static void main(String[] args) {
        TreeMap<String, Object> config = new TreeMap<String, Object>();

		try {
		    // 固定暗号鍵
		    config.put("SecretId", "AKIDXXXXXXXXXXXXXXXXX");
		    // 固定暗号鍵
		    config.put("SecretKey", "XXXXXXXXXXXXXXXXX");

		    // 一時暗号鍵の有効期間、単位は秒です
		    config.put("durationSeconds", 1800);

		    // お客様のバケットに変更します
		    config.put("bucket", "examplebucket-appid");
		    // バケットが位置する地区に変更します
		    config.put("region", "ap-guangzhou");

		    // ここでは許可されるパスプレフィックスに変更します。Webサイトのユーザーログイン状態に従ってアップロードできるディレクトリを判断できます。例：*またはa / *またはa.jpg
		    config.put("allowPrefix", "*");

		    // 暗号鍵の権限リスト。簡単なアップロードとマルチパートアップロードは以下の権限を必要とし、他の権限リストについては、以下を参照してください：https://cloud.tencent.com/document/product/436/31923
		    String[] allowActions = new String[] {
		            // 簡単なアップロード
		            "name/cos:PutObject",
		            // シャードアップロード
		            "name/cos:InitiateMultipartUpload",
		            "name/cos:ListMultipartUploads",
		            "name/cos:ListParts",
		            "name/cos:UploadPart",
		            "name/cos:CompleteMultipartUpload"
		    };
		    config.put("allowActions", allowActions);

		    JSONObject credential = CosStsClient.getCredential(config);
		    System.out.println(credential);
		} catch (Exception e) {
		    throw new IllegalArgumentException("no valid secret !");
		}
    }
}
```

### 一時暗号鍵を使用してCOSにアクセス

 COS APIが一時暗号鍵を使用してCOSサービスにアクセスする時に、`x-cos-security-token`フィールドによって一時的な`sessionToken`を伝達します；一時的な`SecretId`と` SecretKey`によって署名を計算します。

COS Java SDKを例とし、一時暗号鍵を使用してCOSにアクセスする例は以下のとおりです：
> [ここ](https://github.com/tencentyun/cos-java-sdk-v5)をクリックして、GithubからJava SDKインストールパッケージをダウンロードします。

```java
public class Demo {
    public static void main(String[] args) throws Exception {

        // ユーザーの基本情報
        String tmpSecretId = "AKIDxxxxxx";
        String tmpSecretKey = "xxxxxx";
        String sessionToken = "xxxxxx";

        // 1 ユーザー身元情報（secretId、secretKey）を初期化します
        COSCredentials cred = new BasicCOSCredentials(tmpSecretId, tmpSecretKey);
        // 2 バケットのエリアを設定し、COS地域の略称については、https://cloud.tencent.com/document/product/436/6224を参照してください。
        ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
        // 3 cosクライアントを生成します
        COSClient cosclient = new COSClient(cred, clientConfig);
        // バケット名はappidを含む必要があります
        String bucketName = "mybucket-1251668577";

        String key = "aaa/bbb.txt";
        // objectをアップロードし、20M以下のファイルに対してこのAPIを使用することをお勧めします
        File localFile = new File("src/test/resources/test.txt");
        PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

        // x-cos-security-token headerフィールドを設定します
        ObjectMetadata objectMetadata = new ObjectMetadata();
        objectMetadata.setSecurityToken(sessionToken);
        putObjectRequest.setMetadata(objectMetadata);

        try {
            PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
            // PutObjectResultはファイルのetagを返します
            String etag = putObjectResult.getETag();
        } catch (CosServiceException e) {
            e.printStackTrace();
        } catch (CosClientException e) {
            e.printStackTrace();
        }

        // クライアントの閉鎖
        cosclient.shutdown();

    }
}
```

### STSクラウドAPI
#### APIリクエストアドレス
```shell
https://sts.api.qcloud.com/v2/index.php
```
### APIリクエスト方法
クラウドAPIのパラメータはGETパラメータとPOSTパラメータの2種類のフォーマットをサポートし、以下、GETパラメータのフォーマットを紹介します。
#### APIリクエストパラメータの説明

>? 以下のリクエストパラメータリストにおいて、一時暗号鍵APIに固有のパラメータは以下のとおりです：name、policy、durationSeconds。他のフィールドはクラウドAPIの[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)です。

| フィールド |  説明  |必須項目 | タイプ  |
| ------------ | ------------ | ------------ | ------------ |
| name | 統合身分ユーザーのニックネーム。<br>備考フィールド、身分備考としてユーザーuinを入力できます。|はい | String |
| policy | ポリシー構文、json文字列url encodeの結果であり、本当のリクエストを送信すれば、urlは以下の例に示すような2回のurl encodeの文字列です | はい | String |
| durationSeconds |  一時的証明書の有効期間を指定し、単位：秒。<br>デフォルト値は1800秒であり、最大有効期間：2時間（7200秒）。 | いいえ | Int |
| Action | クラウドAPIのActionパラメータ。GetFederationTokenを指定する必要があります。 | はい | String |
| Timestamp | 現在のUNIXタイムスタンプ。 | はい | Int |
| Nonce | ランダムな正の整数。リプレイ攻撃を防ぐために、Timestampと組み合わせて使用。 | はい | Int |
| Region | クラウドAPI地域パラメータ、空の文字列入力でき、デフォルトでは、近くの地域です。入力可能な地域については、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)を参照してください。 | はい | String |
| SecretId | クラウドAPI暗号鍵で申請された身分を識別するためのSecretId。1つのSecretIdが一意のSecretKeyに対応し、SecretKeyがリクエストの署名Signatureを生成するために使用されます。 | はい | String |
| Signature | リクエストの署名。このリクエストの正当性を検証するために使用され、ユーザーは実際の入力パラメータに基づいて算出する必要があります。<br>計算方法については、[署名方法](https://cloud.tencent.com/document/api/213/6984#.E7.94.9F.E6.88.90.E7.AD.BE.E5.90.8D.E4.B8.B2 "签名方法") のチャプタを参照してください。|はい | String |

#### 戻り結果の説明

| フィールド | タイプ  | 説明  |
| ------------ | ------------ | ------------ |
| expiredTime | Int | 一時暗号鍵が無効になったタイムスタンプ。 |
| credentials | Object | オブジェクトにはToken、tmpSecretId、tmpSecretKeyトライアドが含まれています |
| --tmpSecretId | String| tmpSecretId　署名を計算する時に使用されます。 |
| --tmpSecretKey |String| tmpSecretKey　署名を計算する時に使用されます。 |
| --sessionToken | String | sessionToken リクエストを認証する時に使用され、COS APIはHeaderのx-cos-security-tokenフィールドに配置されます。 |

#### アクセスリクエストの例

```shell
https://sts.api.qcloud.com/v2/index.php?
policy=%7B%0D%0A++%22version%22%3A+%222.0%22%2C%0D%0A++%22statement%22%3A+%5B%0D%0A++++%7B%0D%0A++++++%22action%22%3A+%5B%0D%0A++++++++%22name%2Fcos%3AHead*%22%2C%0D%0A++++++++%22name%2Fcos%3AGet*%22%2C%0D%0A++++++++%22name%2Fcos%3AList*%22%2C%0D%0A++++++++%22name%2Fcos%3AOptionsObject%22%0D%0A++++++%5D%2C%0D%0A++++++%22effect%22%3A+%22allow%22%2C%0D%0A++++++%22resource%22%3A+%5B%0D%0A++++++++%22*%22%0D%0A++++++%5D%0D%0A++++%7D%0D%0A++%5D%0D%0A%7D&name=brady&Action=GetFederationToken&SecretId=AKIDPiqmW3qcgXVSKN8jngPzRhvxzYyDL5qP&Nonce=665530507&Timestamp=1545889218&RequestClient=net-sdk-v5&durationSeconds=7200&Signature=S5LPn2GNbi1mLR3EnAcVAW3iYe8%3D
```

#### 成功した場合に返されたコンテンツの例

```shell
{
  "code": 0,
  "message": "",
  "codeDesc": "Success",
  "data": {
    "credentials": {
      "sessionToken":"xxxxxx",
      "tmpSecretId":"AKIDxxxxx",
      "tmpSecretKey":"xxxxx"
    },
    "expiredTime":1545896418
  }
}
```

## エラーチェック

返された結果のエラーコードは、エラーの主な原因を表します。

- codeは、すべてのモジュールのAPIに適用される共通エラーコードです。codeが0の場合、呼び出しは成功します。それ以外の場合、呼び出しは失敗します。呼び出しが失敗した場合、ユーザーは共通エラーコードリストに基づいてエラーの原因を確認し、対処することができます。

- codeDescは、モジュールに関連したエラーを示すモジュールエラーコードです。呼び出しが失敗した場合、ユーザーはモジュールエラーコードリストに基づいてエラーの原因を確認し、対処することができます。

具体的なエラーの説明については、［エラーコード］（https://intl.cloud.tencent.com/document/product/598/13884）を参照してください。
