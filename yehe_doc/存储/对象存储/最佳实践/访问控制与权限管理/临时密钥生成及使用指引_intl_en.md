>!
> - When authorizing access with a temporary key, ensure that you follow the principle of the least privilege as needed. If you grant excessive permissions, such as granting permissions to all resources `(resource: *)` or all operations `(action: *)`, data security risks may arise.
> - If you have specified a permission scope for the temporary key when applying for it, you can only use the key within the scope. For example, if you have limited the permissions to only uploading objects to the `examplebucket-1-1250000000`, you **can’t** upload objects to the `examplebucket-2-1250000000` bucket or download objects from the `examplebucket-1-1250000000` bucket.

## Temporary Key

[Temporary keys (temporary access credentials)](https://intl.cloud.tencent.com/document/product/1150/49452) are access-limited keys requested through CAM APIs.
To call the COS API, you use temporary keys to calculate a signature for identity authentication.
When a COS API request uses a temporary key to calculate the signature for authentication, the following three fields in the message returned by the temporary key API are required:
- TmpSecretId
- TmpSecretKey
- Token 

## Benefits to Use a Temporary Key

When using COS on web, iOS, and Android applications, fixed keys are less ideal for permission management and less secure if stored in your client-side code, as the key may be disclosed. In this case, you can use a temporary key.
For example, when applying for a temporary key, you can specify the action and resource by setting the [policy](https://intl.cloud.tencent.com/document/product/436/30580) field to grant limited access permissions.

For COS API authorization policies, see:
- [Working with COS API Access Policies](https://intl.cloud.tencent.com/document/product/436/30580)
- [Examples of Temporary Key Authorization Policies in Common Scenarios](https://intl.cloud.tencent.com/document/product/436/30580#.E5.B8.B8.E8.A7.81.E5.9C.BA.E6.99.AF.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5).

## Getting a Temporary Key

You can get a temporary key via the [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk) or by calling the STS API [GetFederationToken](https://intl.cloud.tencent.com/document/product/1150/49452) directly.


>! The Java SDK is used as an example in this document. To use it, you need to get the SDK code (version number) on GitHub. If you cannot find the SDK version number, check whether this SDK version is available on GitHub.
>

### COS STS SDK 

COS provides SDKs and samples in various languages (e.g., Java, Node.js, PHP, Python, and Go) for STS. For more information, please see [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk). To learn about how to use each SDK, see the README files and samples on GitHub by referring to the following table:

| Language  | Download Address  | Sample |
| ------------------------- | ------ | ------|
| Java              | [Download](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java) | [View Sample](https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/java/src/test/java/com/tencent/cloud/CosStsClientTest.java) |
| .NET             | [Download](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/dotnet) | [View Sample](https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/dotnet/demo/Program.cs)|
| Go            | [Download](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/go) |  [View Sample](https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/go/example/sts_demo.go)|
| Node.js     | [Download](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/nodejs) | [View Sample](https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/nodejs/demo/sts-server.js) |
| PHP       | [Download](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/php) | [View Sample](https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/php/demo/sts_test.php) |
| Python      | [Download](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/python)    | [View Sample](https://github.com/tencentyun/qcloud-cos-sts-sdk/blob/master/python/demo/sts_demo.py) |

>! To avoid the differences between versions of the STS API, STS SDKs take a return parameters structure that may be different from that of the STS API. For more information, see [Java SDK documentation](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java).
>


Here is an example to obtain a temporary key using the downloaded [Java SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java):

#### Sample codes
```java
// Import `java sts sdk` using the integration method with Maven as described on GitHub, with v3.1.0 or later required.
public class Demo {
    public static void main(String[] args) {
        TreeMap<String, Object> config = new TreeMap<String, Object>();

        try {
            // `SecretId` and `SecretKey` represent permanent identities (root account, sub-account) for applying for a temporary key. If it is a sub-account, it must have permission to operate buckets.
            String secretId = System.getenv("secretId");// User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
 			String secretKey = System.getenv("secretKey");// User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Replace it with your Cloud API key SecretId
            config.put("secretId", secretId);
            // Replace it with your Cloud API key SecretKey
            config.put("secretKey", secretKey);

            // Set a domain: 
            // If you use Tencent Cloud CVMs, you can set an internal domain.
            //config.put("host", "sts.internal.tencentcloudapi.com");

            // Validity period of the key, in seconds (default: 1800). The value can be up to 7200 (2 hours) for the root account, and 129600 (36 hours) for a sub-account.
            config.put("durationSeconds", 1800);

            // Replace it with your own bucket
            config.put("bucket", "examplebucket-1250000000");
            // Replace it with the region where your bucket resides
            config.put("region", "ap-guangzhou");

            // Change it to an allowed path prefix. You can determine the upload path based on your login status.
            // Examples of several typical prefix authorization scenarios:
            // 1. Allow access to all objects: "*"
            // 2. Allow access to specified objects: "a/a1.txt", "b/b1.txt"
            // 3. Allow access to objects with specified prefixes: "a*", "a/*", "b/*"
            // If "*" is entered, you allow the user to access all resources. Unless otherwise necessary, grant the user only the limited permissions that are needed following the principle of least privilege.
            config.put("allowPrefixes", new String[] {
                    "exampleobject",
                    "exampleobject2"
            });

            // A list of permissions needed for the key (required)
            // The following permissions are required for simple, form-based, and multipart upload. For other permissions, visit https://intl.cloud.tencent.com/document/product/436/30580.
            String[] allowActions = new String[] {
                     // Simple upload
                    "name/cos:PutObject",
                    // Upload using a form or Weixin Mini Program
                    "name/cos:PostObject",
                    // Multipart upload
                    "name/cos:InitiateMultipartUpload",
                    "name/cos:ListMultipartUploads",
                    "name/cos:ListParts",
                    "name/cos:UploadPart",
                    "name/cos:CompleteMultipartUpload"
            };
            config.put("allowActions", allowActions);
			    /**
             * Set `condition` (if necessary)
             //# Condition for the temporary key to take effect. For the detailed configuration rules of `condition` and `condition` types supported by COS, visit https://cloud.tencent.com/document/product/436/71307.
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
        } catch (Exception e){
            e.printStackTrace();
            throw new IllegalArgumentException("no valid secret !");
        }
    }
}
```

#### FAQs

#### What should I do if NoSuchMethodError occurs due to JSONObject package conflict?

Use 3.1.0 or a later version.


### Accessing COS using a temporary key

 When a COS API accesses COS with a temporary key, it passes the temporary `sessionToken` through the `x-cos-security-token` field, and calculates the signature using the temporary `SecretId` and `SecretKey`.

The following example shows how to use a temporary key obtained by use of COS Java SDK to access COS:
>? Before you run the sample, go to the [GitHub project](https://github.com/tencentyun/cos-java-sdk-v5) to download the Java SDK installation package.
>

```java
// Import `cos xml java sdk` using the integration method with Maven as described on GitHub.
import com.qcloud.cos.*;
import com.qcloud.cos.auth.*;
import com.qcloud.cos.exception.*;
import com.qcloud.cos.model.*;
import com.qcloud.cos.region.*;
public class Demo {
    public static void main(String[] args) throws Exception {

        // Basic user information
        String tmpSecretId = "COS_SECRETID";   // Replace it with the temporary SecretId returned by the STS API. 
        String tmpSecretKey = "COS_SECRETKEY";  // Replace it with the temporary SecretKey returned by the STS API.
        String sessionToken = "Token";  // Replace it with the temporary token returned by the STS API.

        // 1. Initialize user authentication information (`secretId`, `secretKey`).
        COSCredentials cred = new BasicCOSCredentials(tmpSecretId, tmpSecretKey);
        // 2. Set the bucket region. For more information on COS regions, visit https://cloud.tencent.com/document/product/436/6224.
        ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
        // 3. Generate a COS client
        COSClient cosclient = new COSClient(cred, clientConfig);
        // The bucket name must contain `appid`.
        String bucketName = "examplebucket-1250000000";

        String key = "exampleobject";
        // Upload an object. You are advised to call this API to upload objects smaller than 20 MB.
        File localFile = new File("src/test/resources/text.txt");
        PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

        // Set the `x-cos-security-token` header field.
        ObjectMetadata objectMetadata = new ObjectMetadata();
        objectMetadata.setSecurityToken(sessionToken);
        putObjectRequest.setMetadata(objectMetadata);

        try {
            PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
            // Success: PutObjectResult returns the file ETag.
            String etag = putObjectResult.getETag();
        } catch (CosServiceException e) {
			//Failure: CosServiceException is thrown.
            e.printStackTrace();
        } catch (CosClientException e) {
			//Failure: CosClientException is thrown.
            e.printStackTrace();
        }

        // Disable the client
        cosclient.shutdown();

    }
}
```

