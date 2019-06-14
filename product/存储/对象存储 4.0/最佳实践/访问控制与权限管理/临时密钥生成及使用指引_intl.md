## Temporary Key

Tencent Cloud CAM API provides you temporary keys that have limited access permissions.
To call the COS API, you use temporary keys to calculate a signature for identity authentication.
When calculating the signature for COS API requests, you can find the temporary keys in the following fields returned by the CAM API:

- `tmpSecretKey` 
- `sessionToken` 

## Advantages of Temporary Keys

When using COS on  Web, iOS, and Android applications, compared to temporary keys, fixed keys  are less ideal for managing access permissions and less safe if stored in your code as a constant because this highly increases the risk that your API credentials could leak.
For example, when applying for a temporary key, you can specify the action and resource by setting the [policy](https://intl.cloud.tencent.com/document/product/436/30580#policy) field to grant limited access permissions. 


For COS API authorization policies, see:
- [Guide on COS API Temporary Key Authorization Policies](https://intl.cloud.tencent.com/document/product/436/30580)
- [Examples of Temporary Key Authorization Policies in Common Scenarios](https://intl.cloud.tencent.com/document/product/436/30580).

## Getting a Temporary Key

You can get a temporary key via [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk), or calling STS Cloud API directly.


### COS STS SDK 

COS provides SDKs and examples in various languages (such as Java, Nodejs, PHP, Python) for STS.
For more information, see [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk). For information on how to use each SDK, see README and examples on Github.

Here is an example to obtain a temporary key using the [Java SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java) provided by COS STS SDK.

```java
import com.qcloud.Utilities.Json.JSONObject;

public class Demo {
    public static void main(String[] args) {
        TreeMap<String, Object> config = new TreeMap<String, Object>();

		try {
		    // Fixed key
		    config.put("SecretId", "AKIDXXXXXXXXXXXXXXXXX");
		    // Fixed key
		    config.put("SecretKey", "XXXXXXXXXXXXXXXXX");
		
		    // Validity period of the temporary key (in sec)
		    config.put("durationSeconds", 1800);
		
		    // Use your bucket
		    config.put("bucket", "examplebucket-appid");
		    // Use the region where your bucket locates
		    config.put("region", "ap-guangzhou");
		
		    // Change it to an allowed path prefix, such as a/* or a.jpg. You can determine the directory to which files are allowed to be uploaded based on your login status.
		    config.put("allowPrefix", "*");
		
		    // List of key permissions. The following permissions are required for simple upload and multipart upload. For other permissions, see https://cloud.tencent.com/document/product/436/31923.
		    String[] allowActions = new String[] {
		            // Simple Upload
		            "name/cos:PutObject",
		            // Multipart upload
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

### Access COS using a temporary key

 When accessing the COS service with a temporary key, the COS API passes the temporary `sessionToken` through the `x-cos-security-token` field, and calculates the signature using the temporary `SecretId` and `SecretKey`.

The following example shows how to use a temporary key obtained by use of COS Java SDK to access COS:
> Click [here](https://github.com/tencentyun/cos-java-sdk-v5) to download the Java SDK installer package from Github.

```java
public class Demo {
    public static void main(String[] args) throws Exception {

        // User basic information
        String tmpSecretId = "AKIDxxxxxx";
        String tmpSecretKey = "xxxxxx";
        String sessionToken = "xxxxxx";

        // 1. Initialize user authentication information (secretId, secretKey).
        COSCredentials cred = new BasicCOSCredentials(tmpSecretId, tmpSecretKey);
        // 2. Set the region where the bucket resides. For the abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224.
        ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
        // 3. Generate the COS client.
        COSClient cosclient = new COSClient(cred, clientConfig);
        // The bucket name must contain appid.
        String bucketName = "mybucket-1251668577";

        String key = "aaa/bbb.txt";
        // Upload an object. This API should be used for the files less than 20 MB.
        File localFile = new File("src/test/resources/test.txt");
        PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

        // Set the x-cos-security-token header field.
        ObjectMetadata objectMetadata = new ObjectMetadata();
        objectMetadata.setSecurityToken(sessionToken);
        putObjectRequest.setMetadata(objectMetadata);

        try {
            PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
            // The file etag is returned by putobjectResult.
            String etag = putObjectResult.getETag();
        } catch (CosServiceException e) {
            e.printStackTrace();
        } catch (CosClientException e) {
            e.printStackTrace();
        }

        // Shut down the client
        cosclient.shutdown();

    }
}
```

