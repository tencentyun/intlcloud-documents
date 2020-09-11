>Be sure to grant permissions to access with a temporary key following the principle of least authority as needed for your business. If you grant permissions to all resources `(resource: *)` or all operations `(action: *)`, data security risks may arise due to excessive permission granting.

## Temporary Key

[Temporary keys (temporary access credentials)](https://intl.cloud.tencent.com/document/product/598/35838) are access-limited keys requested through CAM APIs.
 To call the COS API, you use temporary keys to calculate a signature for identity authentication.
 When a COS API request uses a temporary key to calculate the signature for authentication, the following three fields in the message returned by the temporary key API are required:
- TmpSecretId
- TmpSecretKey
- Token 

## Benefits to Use a Temporary Key

When using COS on Web, iOS, and Android applications, compared to temporary keys, fixed keys  are less ideal for managing access permissions and less safe if stored in your code as a constant because this highly increases the risk that your API credentials could leak.
For example, when applying for a temporary key, you can specify the action and resource by setting the [policy](https://intl.cloud.tencent.com/document/product/436/30580) field to grant limited access permissions.

For COS API authorization policies, see:
- [Guide on COS API Temporary Key Authorization Policies](https://intl.cloud.tencent.com/document/product/436/30580)
- [Examples of Temporary Key Authorization Policies in Common Scenarios](https://intl.cloud.tencent.com/document/product/436/30580#.E5.B8.B8.E8.A7.81.E5.9C.BA.E6.99.AF.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5).

## Getting a Temporary Key

You can get a temporary key via [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk), or by calling [STS API](https://intl.cloud.tencent.com/document/product/598/35838).


>Take Java SDK as an example. To use it, you need to get the SDK code (version No.) on GitHub. If the SDK version No. cannot be found, check whether this specified SDK version is available on GitHub.

### COS STS SDKs 

COS provides SDKs and samples in various languages (currently including Java, Nodejs, PHP and Python) for STS. For more information, see [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk). For information on how to use each SDK, see README and samples on Github.

>To avoid the differences between versions of the STS API, STS SDKs take a return parameters structure that may be different from that of the STS API. For more information, see [Java SDK documentation](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java).

Here is an example to obtain a temporary key using the downloaded [Java SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java):

```java
// Import `java sts sdk` using the integration method with Maven as described on GitHub 
import java.util.*;
import org.json.JSONObject; 
import com.tencent.cloud.CosStsClient;

public class Demo {
    public static void main(String[] args) {
        TreeMap<String, Object> config = new TreeMap<String, Object>();

		try {
		    // Replace with your own SecretId 
		    config.put("SecretId", "AKIDHTVVaVR6e3");
		    // Replace with your own SecretKey
		    config.put("SecretKey", "PdkhT9e2rZCfy6");
		
		    // Validity period of the temporary key in seconds; default value: 1,800s; maximum value: 7,200s
		    config.put("durationSeconds", 1800);
		
		    // Replace with your own bucket
		    config.put("bucket", "examplebucket-1250000000");
		    // Replace with the region where your bucket resides
		    config.put("region", "ap-guangzhou");
		
		    // Change it to the allowed path prefix such as `a.jpg`, `a/*`, or`*`. You can determine the specific path to which files can be uploaded based on your login status
			// If "*" is entered, the user will be allowed to access all resources; unless it is required by your business, please grant the user only the corresponding permission based on the principle of least privilege.
		    config.put("allowPrefix", "a.jpg");
		
		    // List of key permissions. The following permissions are required for simple upload, upload using a form, and multipart upload. For other permissions, please visit https://intl.cloud.tencent.com/document/product/436/30580
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
		
		    JSONObject credential = CosStsClient.getCredential(config);
			// If it succeeds, the temporary key information will be returned and printed out as shown below:
		    System.out.println(credential);
		} catch (Exception e) {
			// If it fails, an exception will be thrown
		    throw new IllegalArgumentException("no valid secret !");
		}
    }
}
```

### Access COS using a temporary key

 When accessing the COS service with a temporary key, the COS API passes the temporary `sessionToken` through the `x-cos-security-token` field, and calculates the signature using the temporary `SecretId` and `SecretKey`.

The following example shows how to use a temporary key obtained by use of COS Java SDK to access COS:
>Click [here](https://github.com/tencentyun/cos-java-sdk-v5) to download the Java SDK installer package from Github before running the sample below:

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
         String tmpSecretId = "COS_SECRETID"; // Replace with your temporary SecretId returned by the STS API
         String tmpSecretKey = "COS_SECRETKEY"; // Replace with your temporary SecretKey returned by the STS API
         String sessionToken = "Token"; // Replace with your temporary Token returned by the STS API

        // 1. Initialize user authentication information (secretId, secretKey).
        COSCredentials cred = new BasicCOSCredentials(tmpSecretId, tmpSecretKey);
        // 2. Set the bucket region. For COS regions, see https://intl.cloud.tencent.com/document/product/436/6224.
        ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
        // 3. Generate a COS client.
        COSClient cosclient = new COSClient(cred, clientConfig);
        // The bucket name must contain `appid`.
        String bucketName = "examplebucket-1250000000";

        String key = "doc/picture.jpg";
        // Upload an object. This API should be used for the files less than 20 MB.
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
