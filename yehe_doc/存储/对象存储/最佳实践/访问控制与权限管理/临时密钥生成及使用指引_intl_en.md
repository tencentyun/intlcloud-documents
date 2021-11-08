>!
> - When authorizing access with a temporary key, ensure that you follow the principle of the least privilege as needed. If you grant excessive permissions, such as granting permissions to all resources `(resource: *)` or all operations `(action: *)`, data security risks may arise.
> - If you have specified a permission scope for the temporary key when applying for it, you can only use the key within the scope. For example, if you have limited the permissions to only uploading objects to the `examplebucket-1-1250000000`, you can **not** upload objects to the `examplebucket-2-1250000000` bucket or download objects from the `examplebucket-1-1250000000` bucket.

## Temporary Key

The temporary key (access credential) obtains limited permissions using Tencent Cloud CAM APIs.
To call the COS API, you use temporary keys to calculate a signature for identity authentication.
When a COS API request uses a temporary key to calculate the signature for authentication, the following three fields in the message returned by the temporary key API are required:
- TmpSecretId
- TmpSecretKey
- Token 

## Benefits to Use a Temporary Key

When using COS on Web, iOS, and Android applications, fixed keys are less ideal for permission management and less safe if stored in your client-side code, as the key could leak. In this case, you can use a temporary key.
For example, when applying for a temporary key, you can specify the action and resource by setting the [policy](https://intl.cloud.tencent.com/document/product/436/30580) field to grant limited access permissions.

For COS API authorization policies, see:
- [Working with COS API Access Policies](https://intl.cloud.tencent.com/document/product/436/30580)
- [Examples of Temporary Key Authorization Policies in Common Scenarios](https://intl.cloud.tencent.com/document/product/436/30580#.E5.B8.B8.E8.A7.81.E5.9C.BA.E6.99.AF.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5).

## Getting a Temporary Key

You can get a temporary key via [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk).


>!The Java SDK is used as an example in this document. To use it, you need to get the SDK code (version number) on GitHub. If you cannot find the SDK version number, check whether this SDK version is available on GitHub.

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


Here is an example to obtain a temporary key using the downloaded [Java SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java):

#### Sample codes
```java
// Import `java sts sdk` using the integration method with Maven as described on GitHub 
import java.util.*;
import org.json.JSONObject; 
import com.tencent.cloud.CosStsClient;

public class Demo {
    public static void main(String[] args) {
        TreeMap<String, Object> config = new TreeMap<String, Object>();

        try {
            // Replace it with your own SecretId
            config.put("SecretId", "AKID****************************");
            // Replace it with your own SecretKey
            config.put("SecretKey", "*******************************");

            // Validity period of the key, in seconds (default: 1800). The value can be up to 7200 (2 hours) for the root account, and 129600 (36 hours) for a sub-account.
            config.put("durationSeconds", 1800);

            // Replace it with your own bucket
            config.put("bucket", "examplebucket-1250000000");
            // Replace it with the region where your bucket resides
            config.put("region", "ap-guangzhou");

            // Change it to the allowed path prefix (such as "a.jpg", "a/*", or "*"). You can determine the upload path based on your login status.
            // If "*" is entered, you allow the user to access all resources. If not necessary, please grant the user only the limited permissions that are needed, following the principle of the least privilege.
            config.put("allowPrefixes", new String[] {
                    "exampleobject",
                    "exampleobject2"
            });

            // A list of permissions needed for the key (required)
            // The following permissions are required for simple upload, upload using a form, and multipart upload. For other permissions, please visit https://intl.cloud.tencent.com/document/product/436/30580
            String[] allowActions = new String[] {
                     // Simple upload
                    "name/cos:PutObject",
                    // Upload using a form or Wechat Mini Program
                    "name/cos:PostObject",
                    // Multipart upload
                    "name/cos:InitiateMultipartUpload",
                    "name/cos:ListMultipartUploads",
                    "name/cos:ListParts",
                    "name/cos:UploadPart",
                    "name/cos:CompleteMultipartUpload"
            };
            config.put("allowActions", allowActions);

            Response response = CosStsClient.getCredential(config);
            // If it succeeds, the temporary key information will be returned and printed out as shown below:
            System.out.println(Jackson.toJsonPrettyString(response));
        } catch (Exception e) {
            e.printStackTrace();
            throw new IllegalArgumentException("no valid secret !");
        }
    }
}
```

#### FAQs

#### NoSuchMethodError due to JSONObject package conflict

Use 3.1.0 or a later version.


### Accessing COS using a temporary key

 When a COS API accesses COS with a temporary key, it passes the temporary `sessionToken` through the `x-cos-security-token` field, and calculates the signature using the temporary `SecretId` and `SecretKey`.

The following example shows how to use a temporary key obtained by use of COS Java SDK to access COS:
>? Before you run the sample, go to the [GitHub project](https://github.com/tencentyun/cos-java-sdk-v5) to download the Java SDK installation package.

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

        // 1. Initialize user authentication information (secretId, secretKey).
        COSCredentials cred = new BasicCOSCredentials(tmpSecretId, tmpSecretKey);
        // 2. Set the bucket region. For COS regions, see https://cloud.tencent.com/document/product/436/6224.
        ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
        // 3. Generate a COS client.
        COSClient cosclient = new COSClient(cred, clientConfig);
        // The bucket name must contain `appid`.
        String bucketName = "examplebucket-1250000000";

        String key = "doc/picture.jpg";
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

        // Shut down the client.
        cosclient.shutdown();

    }
}
```

