## 概要

Cloud Object Storage（COS）を使用する際、一時キーを使用して対応するリソースの操作権限をユーザーに与えるか、またはご自身のサブユーザーまたはコラボレーターに対し、対応するユーザーポリシーを付与することで、それらのアカウントがCOS上のリソース操作を補助できるよう許可するか、あるいはバケットに対応するバケットポリシーを追加し、指定のユーザーがバケット内で指定された操作を行い、指定されたリソースを操作することを許可するかの、いずれかが必要となる可能性があります。これらの権限設定を行う際は、データアセットのセキュリティを保障するため、必ず**最小権限の原則**に従う必要があります。

**最小権限の原則**とは、権限承認を行う際、必ず権限の範囲を明確化し、**指定するユーザー**に、**どのような条件**の下で、**どのような操作**を実行でき、**どのようなリソース**にアクセスできる権限を承認するかを明確にする必要があることを指します。

## 注意事項
権限承認の際は最小権限の原則を厳守し、ユーザーに対し限られた操作（例えば`action:GetObject`の権限承認など）の実行、限られたリソース（例えば`resource:examplebucket-1250000000/exampleobject.txt`の権限承認など）へのアクセスのみを許可することをお勧めします。 
大きすぎる権限を与えることで、意図しない越権操作が行われ、データセキュリティリスクが生じることを避けるため、ユーザーにすべてのリソースへのアクセス（例えば`resource:*`など）、またはすべての操作（例えば`action:*`など）の権限を承認することは可能な限り避けるよう強く推奨します。

潜在的なデータセキュリティリスクの例を次に挙げます。
- データ漏洩：ユーザーに指定のリソースをダウンロードする権限、例えば`examplebucket-1250000000/data/config.json`および`examplebucket-1250000000/video/`のダウンロード権限を与えても、権限ポリシーに`examplebucket-1250000000/*`を設定していた場合、このバケット下のすべてのオブジェクトのダウンロードが許可されることになり、越権操作行為があった場合は意図しないデータ漏洩が発生します。
- データが上書きされる：ユーザーにリソースをアップロードする権限、例えば`examplebucket-1250000000/data/config.json`および`examplebucket-1250000000/video/`のアップロード権限を与えても、権限ポリシーに`examplebucket-1250000000/*`を設定していた場合、このバケット下のすべてのオブジェクトのアップロードが許可されることになり、越権操作行為があった場合は意図しないオブジェクトの上書きが発生します。このようなリスクを防止するためには、最小権限の原則に従うほか、[バージョン管理](https://intl.cloud.tencent.com/document/product/436/19883)によってデータのすべての過去バージョンを保持し、追跡に役立てることも可能です。
- 権限の漏洩：ユーザーにバケットのオブジェクトリスト`cos:GetBucket`の出力を許可しても、権限ポリシーに`cos:*`を設定していた場合、バケット権限の再承認、オブジェクトの削除、バケットの削除を含む、このバケットのすべての操作が許可されることになり、データに極めて大きなリスクをもたらします。


## 使用ガイド

最小権限の原則の下では、ポリシーに次の情報を明確に指定する必要があります。

- プリンシパル（principal）：どのサブユーザー（ユーザーIDの入力が必要）、コラボレーター（ユーザーIDの入力が必要）、匿名ユーザーまたはユーザーグループに権限を付与したいかを明確に指定する必要があります。一時キーを使用してアクセスする場合、この項の指定は不要です。
- ステートメント（statement）：次のいくつかのパラメータに、対応するパラメータを明確に入力します。
	-  エフェクト（effect）：このポリシーが「許可」であるか「明示的な拒否」であるかを明確に述べる必要があります。allowとdenyの2種類が含まれます。
	-  アクション（action）：このポリシーが許可または拒否するアクションを明確に述べる必要があります。アクションは単一のAPIのアクションまたは複数のAPIアクションのセットとすることができます。
	-  リソース（resource）：このポリシーが権限を承認する具体的なリソースを明確に述べる必要があります。リソースは6つの部分で記述されます。リソース範囲の指定は、`exampleobject.jpg`などの指定されたファイル、または`examplePrefix/*`などの指定されたディレクトリとすることができます。業務上の必要がない限り、すべてのリソースにアクセスする権限（ワイルドカード`*`）をユーザーにみだりに付与しないでください。
	-  条件（condition）：ポリシー発効の制約条件を記述します。条件はオペレーター、アクションキーとアクション値から構成されています。条件値には時間、IPアドレスなどの情報を含めることができます。

### 一時キーの最小権限ガイド

一時キー申請の過程で、権限ポリシーの[Policy](https://intl.cloud.tencent.com/document/product/1150/49452)フィールドを設定することで、操作およびリソースを制限し、権限を指定された範囲内に限定することができます。一時キー生成に関する説明については、[一時キーの生成および使用ガイド](https://intl.cloud.tencent.com/document/product/436/14048)のドキュメントをご参照ください。

#### 権限承認の例

#### Java SDKを使用して、あるオブジェクトへのアクセス権限を承認

Java SDKを使用して、バケット`examplebucket-1250000000`内のオブジェクト`exampleObject.txt`のダウンロード権限を承認したい場合、それに応じて設定する必要があるコードは次のようになります。

```
// githubが提供するmaven統合メソッドによってjava sts sdkをインポートします 
import java.util.*;
import org.json.JSONObject; 
import com.tencent.cloud.CosStsClient;

public class Demo {
    public static void main(String[] args) {
        TreeMap<String, Object> config = new TreeMap<String, Object>();

        try {
            String secretId = System.getenv("secretId");//ユーザーのSecretIdです。サブアカウントのキーを使用し、権限承認は最小権限ガイドに従って行い、使用上のリスクを低減させることをお勧めします。サブアカウントキーの取得については、https://cloud.tencent.com/document/product/598/37140をご参照ください
            String secretKey = System.getenv("secretKey");//ユーザーのSecretKeyです。サブアカウントのキーを使用し、権限承認は最小権限ガイドに従って行い、使用上のリスクを低減させることをお勧めします。サブアカウントキーの取得については、https://cloud.tencent.com/document/product/598/37140をご参照ください
            // ご自身のSecretIdに置き換えます 
            config.put("SecretId", secretId);
            // ご自身のSecretKeyに置き換えます
            config.put("SecretKey", secretKey);

            // 一時キーの有効期間の単位は秒であり、デフォルトでは1800秒、最長7200秒まで設定可能です
            config.put("durationSeconds", 1800);

            // ご自身のbucketに置き換えます
            config.put("bucket", "examplebucket-1250000000");
            // bucketの所在リージョンに置き換えます
            config.put("region", "ap-guangzhou");

            // ここを許可するパスのプレフィックスに変更します。ご自身のウェブサイトのユーザーログインセッションによって、a.jpg または a/* または * などのように、アップロードを許可する具体的なパスを判断することができます。
            // 「*」を入力すると、ユーザーにすべてのリソースへのアクセスを許可することになります。業務上の必要がない限り、最小権限の原則に従って、対応する範囲のアクセス権限をユーザーに与えてください。
            config.put("allowPrefix", "exampleObject.txt");

            // キーの権限リストです。シンプルアップロード、フォームアップロード、マルチパートアップロードには次の権限が必要です。その他の権限リストについてはhttps://cloud.tencent.com/document/product/436/31923をご覧ください
            String[] allowActions = new String[] {
                    // データをダウンロードします
                    "name/cos:GetObject"
            };
            config.put("allowActions", allowActions);

            JSONObject credential = CosStsClient.getCredential(config);
            //成功すると一時キー情報が返されます。次のようにキー情報を印刷します
            System.out.println(credential);
        } catch (Exception e) {
            //失敗するとエラーがスローされます
            throw new IllegalArgumentException("no valid secret !");
        }
    }
}
```

#### APIを使用して、あるオブジェクトへのアクセス権限を承認

APIを使用して、バケット`examplebucket-1250000000`内のオブジェクト`exampleObject.txt`およびディレクトリ`examplePrefix`下のすべてのオブジェクトのダウンロード権限を承認したい場合、そのために書き込む必要があるPolicyは次のようになります。

```shell
{
  "version": "2.0",
  "statement":[
    {
      "action":[
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource":[
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/exampleObject.txt",
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/examplePrefix/*"
      ]
    }
  ]
}
```

### 署名付きURLの最小権限ガイド

署名付きURL方式によって一時的なアップロードおよびダウンロード操作を実現できます。また、署名付きURLは誰にでも送信することができ、有効な署名付きURLを受領した人は誰でもオブジェクトをアップロードまたはダウンロードできます。

>!一時キーとパーマネントキーはどちらも署名付きURLの生成に用いることができますが、最小権限の原則に従って[一時キーの生成](https://intl.cloud.tencent.com/document/product/436/14048)を行い、一時キーを使用して署名の計算を行うことを強く推奨します。セキュリティ上のリスクを防止するため、権限が大きすぎるパーマネントキーは可能な限り使用しないでください。

#### 権限承認の例

#### ユーザーに対し、署名付きURLを使用してオブジェクトをダウンロードする権限を承認

一時キーを使用して署名付きのダウンロードリンクを生成し、返す必要のあるいくつかのパブリックヘッダー（例えばcontent-type、content-languageなど）の上書きを設定します。Javaのサンプルコードは次のとおりです。

```java
// 取得した一時キー (tmpSecretId、tmpSecretKey、sessionToken)を渡します
String tmpSecretId = "SECRETID";
String tmpSecretKey = "SECRETKEY";
String sessionToken = "TOKEN";
COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// bucketのリージョンを設定します。COSリージョンの略称についてはhttps://cloud.tencent.com/document/product/436/6224をご参照ください
// clientConfigにはregion、https(デフォルトではhttp)、タイムアウト、プロキシなどを設定するsetメソッドが含まれます。使用にあたってはソースコードまたはよくあるご質問のJava SDKのパートを参照できます
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// httpsプロトコルを使用したURLを生成したい場合はこの行を設定します。設定することをお勧めします。
// clientConfig.setHttpProtocol(HttpProtocol.https);
// cosクライアントを生成します
COSClient cosClient = new COSClient(cred, clientConfig);
// バケットの命名形式はBucketName-APPIDです 
String bucketName = "examplebucket-1250000000";
// ここでのkeyはオブジェクトキーです。オブジェクトキーはオブジェクトのバケット内での固有識別子です
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// ダウンロード時に返されるhttpヘッダーを設定します
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
String responseContentLanguage = "zh-CN";
// レスポンスヘッダーに含まれるファイル名の情報を設定します
String responseContentDispositon = "filename=\"exampleobject\"";
String responseCacheControl = "no-cache";
String cacheExpireStr =
        DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24L * 3600L * 1000L));
responseHeaders.setContentType(responseContentType);
responseHeaders.setContentLanguage(responseContentLanguage);
responseHeaders.setContentDisposition(responseContentDispositon);
responseHeaders.setCacheControl(responseCacheControl);
responseHeaders.setExpires(cacheExpireStr);
req.setResponseHeaders(responseHeaders);
// 署名の有効期限を設定します(オプション)。設定しない場合は、デフォルトでClientConfigの署名有効期限(1時間)を使用します
// ここでは署名が30分後に期限切れとなるよう設定します
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);
URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());
cosClient.shutdown();
```

### ユーザーポリシーの最小権限ガイド

ユーザーポリシーとは[CAMコンソール](https://console.cloud.tencent.com/cam/policy)で追加するユーザー権限ポリシーを指し、ユーザーにCOSリソースへのアクセス権限を与えるために用いられます。ユーザーアクセスポリシー概要の設定説明については、 [アクセスポリシーの言語概要](https://intl.cloud.tencent.com/document/product/436/18023)のドキュメントをご参照ください。

#### 権限承認の例

#### アカウントに対し、あるオブジェクトへのアクセス権限を承認

アカウントUIN`100000000001`に対し、バケット`examplebucket-1250000000`内のオブジェクト`exampleObject.txt`のダウンロード権限を承認したい場合、それに応じたアクセスポリシーは次のようになります。
```shell
{
   "version": "2.0",
   "principal":{
      "qcs": [
         "qcs::cam::uin/100000000001:uin/100000000001"
      ]
   },
    "statement":[
        {
            "action":[
                "name/cos:GetObject"
            ],
            "effect": "allow",
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000.ap-guangzhou.myqcloud.com/exampleObject.txt"
            ]
        }
    ]
}
```

#### サブアカウントに対し、あるディレクトリへのアクセス権限を承認

サブアカウントUIN`100000000011`（ルートアカウントのUINは`100000000001`）に対し、バケット`examplebucket-1250000000`内のディレクトリ`examplePrefix`下のオブジェクトのダウンロード権限を承認したい場合、それに応じたアクセスポリシーは次のようになります。

```shell
{
   "version": "2.0",
   "principal":{
      "qcs": [
         "qcs::cam::uin/100000000001:uin/100000000011"
      ]
   },
    "statement":[
        {
            "action":[
                "name/cos:GetObject"
            ],
            "effect": "allow",
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000.ap-guangzhou.myqcloud.com/examplePrefix/*"
            ]
        }
    ]
}
```

### バケットポリシーの最小権限ガイド

バケットポリシーとはバケット内で設定するアクセスポリシーを指し、指定のユーザーがバケットおよびバケット内のリソースに対し指定された操作を行うことを許可します。バケットポリシーの設定については、[バケットポリシーの追加](https://intl.cloud.tencent.com/document/product/436/30927)のドキュメントをご参照ください。

#### 権限承認の例

#### サブアカウントに対し特定のオブジェクトへのアクセス権限を承認

サブアカウントUIN`100000000011`（ルートアカウントのUINは`100000000001`）に対し、バケット`examplebucket-1250000000`内のオブジェクト`exampleObject.txt`およびディレクトリ`examplePrefix`下のすべてのオブジェクトのダウンロード権限を承認したい場合、それに応じたアクセスポリシーは次のようになります。

```shell
{
  "Statement": [
    {
      "Action": [
        "name/cos:GetObject"
      ],
      "Effect": "allow",
      "Principal": {
        "qcs": [
          "qcs::cam::uin/100000000001:uin/100000000011"
        ]
      },
      "Resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/exampleObject.txt",
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/examplePrefix/*"
      ]
    }
  ],
  "version": "2.0"
}
```
