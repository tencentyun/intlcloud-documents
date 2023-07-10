>!
> - 一時キーを使用してアクセス権限を付与する際は、必ず業務の必要性に応じて、最小権限の原則に従って権限を付与してください。すべてのリソース`(resource:*)`またはすべてのアクション`(action:*)`の権限を直接与えてしまうと、権限が大きすぎるためにデータセキュリティ上のリスクが生じます。
> - 一時キーを申請する際、権限の範囲を指定していると、申請した一時キーも権限の範囲でしか操作を行うことができません。例えば一時キーを申請する際、バケットexamplebucket-1-1250000000にファイルをアップロードできるという権限の範囲を指定していた場合、申請したキーではファイルをexamplebucket-2-1250000000にアップロードすることも、examplebucket-1-1250000000からファイルをダウンロードすることも**できません**。

## 一時キー

[一時キー（一時アクセス証明書）](https://intl.cloud.tencent.com/document/product/1150/49452)はCAMのTencent Cloud APIによって提供されるインターフェースを通じて取得する、権限が限定されたキーです。
COS APIは一時キーを使用して署名を計算し、COS APIリクエストの送信に使用することができます。
COS APIリクエストは一時キーを使用して署名を計算する際、一時キー取得インターフェースから返された情報の中の、次の3つのフィールドを使用する必要があります。
- TmpSecretId
- TmpSecretKey
- Token 

## 一時キーを使用するメリット

Web、iOS、AndroidでCOSを使用する際、固定のキーによる署名計算方式では権限を有効に制御できず、またパーマネントキーをクライアントコードに含めることには極めて大きな漏洩リスクが伴います。一時キー方式を使用すると、権限制御の問題を便利かつ有効に解決することができます。
例えば、一時キー申請の過程で、権限ポリシーの[policy](https://intl.cloud.tencent.com/document/product/436/30580)フィールドを設定することで、操作およびリソースを制限し、権限を指定された範囲内に限定することができます。

COS API権限承認ポリシーに関しては、次をご参照ください。
- [COS API一時キー権限承認ポリシーガイド](https://intl.cloud.tencent.com/document/product/436/30580)
- [一般的なケースにおける一時キー権限ポリシーの例](https://intl.cloud.tencent.com/document/product/436/30580#.E5.B8.B8.E8.A7.81.E5.9C.BA.E6.99.AF.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5)

## 一時キーの取得

一時キーは、提供されている[COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk)方式で取得するか、または[STS Cloud API](https://intl.cloud.tencent.com/document/product/1150/49452)を直接リクエストする方式で取得することもできます。


>! 例で使用しているのはJava SDKであり、GitHubでSDKコード（バージョン番号）を取得する必要があります。対応するSDKバージョン番号が見つからないと表示された場合は、GitHubで対応するバージョンのSDKを取得できないかを確認してください。
>

### COS STS SDK 

COSはSTS向けにSDKおよびサンプルを提供しています。現在はJava、Nodejs、PHP、Python、Goなどの複数の言語のサンプルがあります。具体的な内容については[COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk)をご参照ください。各SDKの使用説明についてはGithubのREADMEとサンプルをご参照ください。各言語のGitHubアドレスは以下の表のとおりです。

| 言語タイプ     | コードインストールアドレス   | サンプルコードアドレス |
| ------------------------- | ------ | ------|
| Java              | [インストールアドレス](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java) | [サンプルアドレス](https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/java/src/test/java/com/tencent/cloud/CosStsClientTest.java) |
| .NET             | [インストールアドレス](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/dotnet) | [サンプルアドレス](https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/dotnet/demo/Program.cs)|
| Go            | [インストールアドレス](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/go) |  [サンプルアドレス](https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/go/example/sts_demo.go)|
| NodeJS       | [インストールアドレス](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/nodejs) | [サンプルアドレス](https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/nodejs/demo/sts-server.js) |
| PHP       | [インストールアドレス](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/php) | [サンプルアドレス](https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/php/demo/sts_test.php) |
| Python      | [インストールアドレス](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/python)    | [サンプルアドレス](https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/python/demo/sts_demo.py) |

>! STS SDKはSTSインターフェース自体のバージョン間の違いを非表示にするため、返されるパラメータの構造がSTSインターフェースと完全には一致しない場合があります。詳細については、[Java SDKドキュメント](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java)をご参照ください。
>


例えばJava SDKをご利用中の場合、まず[Java SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java)をダウンロードした後、次の一時キー取得のサンプルを実行してください。

#### サンプルコード
```java
// githubが提供するmaven統合メソッドによってjava sts sdkをインポートします。3.1.0以上のバージョンを使用します
public class Demo {
    public static void main(String[] args) {
        TreeMap<String, Object> config = new TreeMap<String, Object>();

        try {
            //ここでのSecretIdとSecretKeyは一時キーの申請に用いる永続的なID（ルートアカウント、サブアカウントなど）を表します。サブアカウントにはバケットの操作権限が必要です。
            String secretId = System.getenv("secretId");//ユーザーのSecretIdです。サブアカウントのキーを使用し、権限承認は最小権限ガイドに従って行い、使用上のリスクを低減させることをお勧めします。サブアカウントキーの取得については、https://cloud.tencent.com/document/product/598/37140をご参照ください
 			String secretKey = System.getenv("secretKey");//ユーザーのSecretKeyです。サブアカウントのキーを使用し、権限承認は最小権限ガイドに従って行い、使用上のリスクを低減させることをお勧めします。サブアカウントキーの取得については、https://cloud.tencent.com/document/product/598/37140をご参照ください
            // ご自身のCloud APIキーのSecretIdに置き換えます
            config.put("secretId", secretId);
            // ご自身のCloud APIキーのSecretKeyに置き換えます
            config.put("secretKey", secretKey);

            // ドメイン名を設定します: 
            // Tencent Cloud CVMを使用している場合は、内部ドメイン名を設定できます
            //config.put("host", "sts.internal.tencentcloudapi.com");

            // 一時キーの有効期間の単位は秒であり、デフォルトでは1800秒です。現在はルートアカウントが最長2時間（7200秒）、サブアカウントが最長36時間（129600秒）までです
            config.put("durationSeconds", 1800);

            // ご自身のbucketに置き換えます
            config.put("bucket", "examplebucket-1250000000");
            // bucketの所在リージョンに置き換えます
            config.put("region", "ap-guangzhou");

            // ここを許可するパスのプレフィックスに変更します。ご自身のウェブサイトのユーザーログインセッションによって、アップロードを許可する具体的なパスを判断することができます
            // いくつかの典型的なプレフィックスによる権限承認のケースを挙げます。
            // 1、すべてのオブジェクトへのアクセスを許可する："*"
            // 2、指定のオブジェクトへのアクセスを許可する："a/a1.txt", "b/b1.txt"
            // 3、指定のプレフィックスを持つオブジェクトへのアクセスを許可する："a*", "a/*", "b/*"
            // 「*」を入力すると、ユーザーにすべてのリソースへのアクセスを許可することになります。業務上の必要がない限り、最小権限の原則に従って、対応する範囲のアクセス権限をユーザーに与えてください。
            config.put("allowPrefixes", new String[] {
                    "exampleobject",
                    "exampleobject2"
            });

            // キーの権限リストです。ここで今回の一時キーに必要な権限を指定する必要があります。
            // シンプルアップロード、フォームアップロード、マルチパートアップロードには次の権限が必要です。その他の権限リストについてはhttps://intl.cloud.tencent.com/document/product/436/30580をご参照ください
            String[] allowActions = new String[] {
                     // シンプルアップロード
                    "name/cos:PutObject",
                    // フォームアップロード、ミニプログラムアップロード
                    "name/cos:PostObject",
                    // マルチパートアップロード
                    "name/cos:InitiateMultipartUpload",
                    "name/cos:ListMultipartUploads",
                    "name/cos:ListParts",
                    "name/cos:UploadPart",
                    "name/cos:CompleteMultipartUpload"
            };
            config.put("allowActions", allowActions);
			    /**
             * conditionの設定（必要な場合）
             //# 一時キーの発効条件、conditionに関する詳細な設定ルールおよびCOSがサポートするconditionのタイプについては https://cloud.tencent.com/document/product/436/71307をご参照ください
             final String raw_policy = "{\n" +
             "  \"version\":\"2.0\",\n" +
             "  \"statement\":[\n" +
             "    {\n" +
             "      \"effect\":\"allow\",\n" +
             "      \"action\":[\n" +
             "          \"name/cos:PutObject\",\n" +
             "          \"name/cos:PostObject\",\n" +
             "          \"name/cos:InitiateMultipartUpload\",\n" +
             "          \"name/cos:ListMultipartUploads\",\n" +
             "          \"name/cos:ListParts\",\n" +
             "          \"name/cos:UploadPart\",\n" +
             "          \"name/cos:CompleteMultipartUpload\"\n" +
             "        ],\n" +
             "      \"resource\":[\n" +
             "          \"qcs::cos:ap-shanghai:uid/1250000000:examplebucket-1250000000/*\"\n" +
             "      ],\n" +
             "      \"condition\": {\n" +
             "        \"ip_equal\": {\n" +
             "            \"qcs:ip\": [\n" +
             "                \"192.168.1.0/24\",\n" +
             "                \"101.226.100.185\",\n" +
             "                \"101.226.100.186\"\n" +
             "            ]\n" +
             "        }\n" +
             "      }\n" +
             "    }\n" +
             "  ]\n" +
             "}";

             config.put("policy", raw_policy);
             */				
          
          
            Response response = CosStsClient.getCredential(config);
            System.out.println(response.credentials.tmpSecretId);
            System.out.println(response.credentials.tmpSecretKey);
            System.out.println(response.credentials.sessionToken);
        } catch (Exception e) {
            e.printStackTrace();
            throw new IllegalArgumentException("no valid secret !");
        }
    }
}
```

#### よくあるご質問と回答

#### JSONObjectパッケージの競合によるNoSuchMethodError

3.1.0以上のバージョンを使用してください。


### 一時キーを使用したCOSアクセス

 COS APIが一時キーを使用してCOSサービスにアクセスする際、x-cos-security-tokenフィールドによって一時sessionTokenを渡し、一時SecretIdおよびSecretKeyによって署名を計算します。

COS Java SDKの例では、一時キーを使用したCOSアクセスのサンプルは次のようになります。
>? 次のサンプルを実行する前に、[Githubプロジェクト](https://github.com/tencentyun/cos-java-sdk-v5)でJava SDKインストールパッケージを取得してください。
>

```java
// githubが提供するmaven統合メソッドによってcos xml java sdkをインポートします
import com.qcloud.cos.*;
import com.qcloud.cos.auth.*;
import com.qcloud.cos.exception.*;
import com.qcloud.cos.model.*;
import com.qcloud.cos.region.*;
public class Demo {
    public static void main(String[] args) throws Exception {

        // ユーザー基本情報
        String tmpSecretId = "COS_SECRETID";   // STSインターフェースから返された一時SecretIdに置き換えてください 
        String tmpSecretKey = "COS_SECRETKEY";  // STSインターフェースから返された一時SecretKeyに置き換えてください
        String sessionToken = "Token";  // STSインターフェースから返された一時Tokenに置き換えてください

        // 1 ユーザーID情報(secretId, secretKey)を初期化します
        COSCredentials cred = new BasicCOSCredentials(tmpSecretId, tmpSecretKey);
        // 2 bucketのリージョンを設定します。詳細についてはCOSリージョン https://cloud.tencent.com/document/product/436/6224をご参照ください
        ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
        // 3 cosクライアントを生成します。
        COSClient cosclient = new COSClient(cred, clientConfig);
        // bucket名にはappidを含める必要があります
        String bucketName = "examplebucket-1250000000";

        String key = "exampleobject";
        // objectをアップロードします。20M以下のファイルにはこのインターフェースの使用をお勧めします
        File localFile = new File("src/test/resources/text.txt");
        PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

        // x-cos-security-token headerフィールドを設定します
        ObjectMetadata objectMetadata = new ObjectMetadata();
        objectMetadata.setSecurityToken(sessionToken);
        putObjectRequest.setMetadata(objectMetadata);

        try {
            PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
            // 成功：putobjectResultはファイルのetagを返します
            String etag = putObjectResult.getETag();
        } catch (CosServiceException e) {
			//失敗、CosServiceExceptionをスローします
            e.printStackTrace();
        } catch (CosClientException e) {
			//失敗、CosClientExceptionをスローします
            e.printStackTrace();
        }

        // クライアントを閉じる
        cosclient.shutdown();

    }
}
```

