## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for image moderation.

| API | Description |
| -------------------------------| -------------------------------- |
| [Moderating single image](https://intl.cloud.tencent.com/document/product/436/48537) |  Scans existing data stored in COS for porn, illegal, and advertising images. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Moderating Existing Image

#### Feature description

The following example shows how to scan existing images stored in COS for porn, illegal, and advertising information.

#### Sample code

[//]: #	".cssg-snippet-sensitive-content-recognition"

```cs
using COSXML.Model.CI;
using COSXML.Auth;
using COSXML;

namespace COSSnippet
{
    public class PictureOperationModel {

      private CosXml cosXml;

      PictureOperationModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://cloud.tencent.com/document/product/436/6224. 
          .Build();
        
        string secretId = "SECRET_ID";   // SecretId of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        string secretKey = "SECRET_KEY"; // SecretKey of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        long durationSecond = 600;          // Validity period of the request signature in seconds
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// Image moderation
      public void SensitiveContentRecognition()
      {
        // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
        string bucket = "examplebucket-1250000000";
        string key = "exampleobject"; // Object key
        //.cssg-snippet-body-start:[sensitive-content-recognition]
        SensitiveContentRecognitionRequest request = 
          new SensitiveContentRecognitionRequest(bucket, key, "ads");
        SensitiveContentRecognitionResult result = cosXml.SensitiveContentRecognition(request);
      }
      
      static void Main(string[] args)
      {
        PictureOperationModel m = new PictureOperationModel();
        /// Image moderation
        m.SensitiveContentRecognition();
      }
    }
}
```

> ?For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PictureOperation.cs).
