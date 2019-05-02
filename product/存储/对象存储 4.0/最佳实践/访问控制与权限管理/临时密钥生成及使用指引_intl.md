## Temporary Key

The temporary key uses an API provided through CAM to get the key with limited permissions.<br>
 A COS API can use a temporary key to calculate a signature for initiating a COS API request.<br>
 When a COS API request uses a temporary key to calculate a API signature, the following three fields in the message returned by the temporary key API are required:
- `tmpSecretId` 
- `tmpSecretKey` 
- `sessionToken` 

## Benefits to Use a Temporary Key

When you use COS in Web, iOS, and Android platforms, permissions cannot be controlled effectively by calculating a signature with a fix key, and the permission key may be leaked out if put into the client code. A temporary key will make it easy and effective to implement permission control.
For example, when applying for a temporary key, you can specify the action and resource by setting the [policy](https://cloud.tencent.com/document/product/436/31923#policy) field to limit the permissions within a specified range.

For COS API authorization policies, see:
- [Guide on COS API Temporary Key Authorization Policies](https://cloud.tencent.com/document/product/436/31923)
- [Examples of Temporary Key Authorization Policies in Common Scenarios](https://cloud.tencent.com/document/product/436/31923#.E5.B8.B8.E8.A7.81.E5.9C.BA.E6.99.AF.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5).

## Getting a Temporary Key

You can get a temporary key by using the provided [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk), or by directly calling the STS Cloud API.

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

### STS API
#### API request address
```shell
https://sts.api.qcloud.com/v2/index.php
```
#### API request method
Cloud API parameters support both GET and POST parameters. The format of GET parameters is described below:
### API request parameters


| Field | Description | Required | Type |
| ------------ | ------------ | ------------ | ------------ |
| name | Nickname of the user with federated identity.<br>It is a remark field, where the user's uin is input as the identity. | Yes | String |
| durationSeconds | No | Int | The validity period of the temporary credentials (in sec).<br>It defaults to 1800 seconds. The maximum is 7200 seconds (2 hours). | No | Int |
| Action | The Action parameter of the cloud API. GetFederationToken should be specified. | Yes | String |
| Timestamp | Current UNIX timestamp | Yes | Int |
| Nonce | A random positive integer that is used in conjunction with Timestamp to prevent replay attacks | Yes | Int |
| Region | The region parameter of the cloud API. It can be an empty string, and defaults to the nearest region. For available regions, see [Common Request Parameters](https://cloud.tencent.com/document/api/213/6976). | Yes | String |
| SecretId | An ID that the user applies for on the Cloud API Key Console for identity authentication. A SecretId is paired with a unique SecretKey, which is used to generate the request signature. | Yes | String |
| Signature | Request signature, which is used to verify the validity of the request. It is generated based on input parameters.<br>For more information, please see [Signature Method](https://cloud.tencent.com/document/api/213/6984#.E7.94.9F.E6.88.90.E7.AD.BE.E5.90.8D.E4.B8.B2 "签名方法"). | String | Yes |

#### Returned result

| Field | Type | Description |
| ------------ | ------------ | ------------ |
| expiredTime | Int | Expiration timestamp of the temporary key |
| credentials | Object | The object contains a triad of token, tmpSecretId, and tmpSecretKey |
| --tmpSecretId | String| It is used when calculating the signature |
| --tmpSecretKey |String| It is used when calculating the signature |
| --sessionToken | String | It is used when requesting authentication. COS API is placed into the x-cos-security-token field of the Header. |

#### Access request example

```shell
https://sts.api.qcloud.com/v2/index.php?
policy=%7B%0D%0A++%22version%22%3A+%222.0%22%2C%0D%0A++%22statement%22%3A+%5B%0D%0A++++%7B%0D%0A++++++%22action%22%3A+%5B%0D%0A++++++++%22name%2Fcos%3AHead*%22%2C%0D%0A++++++++%22name%2Fcos%3AGet*%22%2C%0D%0A++++++++%22name%2Fcos%3AList*%22%2C%0D%0A++++++++%22name%2Fcos%3AOptionsObject%22%0D%0A++++++%5D%2C%0D%0A++++++%22effect%22%3A+%22allow%22%2C%0D%0A++++++%22resource%22%3A+%5B%0D%0A++++++++%22*%22%0D%0A++++++%5D%0D%0A++++%7D%0D%0A++%5D%0D%0A%7D&name=brady&Action=GetFederationToken&SecretId=AKIDPiqmW3qcgXVSKN8jngPzRhvxzYyDL5qP&Nonce=665530507&Timestamp=1545889218&RequestClient=net-sdk-v5&durationSeconds=7200&Signature=S5LPn2GNbi1mLR3EnAcVAW3iYe8%3D
```

#### Example of a response indicating a successful call

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

## Troubleshooting

The error code in the returned result indicates the main cause of the error.

- "code" is the common error code, which applies to the APIs of all modules. The code of 0 indicates a successful call. Other values indicate a failed call. When the call fails, you can identify the cause of error and take appropriate actions according to the common error code list.

- "codeDesc" is the modular error code, which indicates module-related errors. When the call fails, you can identify the cause of error and take appropriate actions according to the modular error code list.

For more information, see [Error Codes](https://cloud.tencent.com/document/product/598/13884).

