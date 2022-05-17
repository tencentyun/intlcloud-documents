
## Integration Preparations
- Sign up for a Tencent Cloud account and log in to the [FaceID console](https://console.intl.cloud.tencent.com/faceid) to activate the service. 
- Download the latest [SDK](https://console.intl.cloud.tencent.com/faceid). 
- Download the [license](https://console.intl.cloud.tencent.com/faceid) 

## Terms and Definitions

- Customer APP: An app developed by a customer
- Customer Server: The business backend of a customer
- Tencent Cloud API: The backend APIs provided by Tencent Cloud and used to obtain the face recognition credentials and the results
- SDK: The SDK provided by Tencent Cloud for Android or iOS, which is used to integrate the customer apps and start the face recognition together with backend APIs.

## Sequence Diagram (Simplified)

Major roles involved are as shown below:
![Figure 1](https://qcloudimg.tencent-cloud.cn/raw/f963c590fc88067f81da0b7ca3df50f8.png)

Backend APIs: [GenerateReflectSequence](https://intl.cloud.tencent.com/zh/document/product/1061/44246) and [DetectReflectLivenessAndCompare](https://intl.cloud.tencent.com/zh/document/product/1061/44246)
## Sequence Diagram (Detailed)

In the real case, you need to input the URLs to the backend APIs. For use instructions and causes, see [Passing Resources](https://console.intl.cloud.tencent.com/faceid).
*`CreateUploadUrl` serves as an independent role in the diagram*
![Figure 2](https://qcloudimg.tencent-cloud.cn/raw/491abd12442624139fef0b39959a6745.png)
Backend APIs: [GenerateReflectSequence](https://intl.cloud.tencent.com/zh/document/product/1061/44246), [DetectReflectLivenessAndCompare](https://intl.cloud.tencent.com/zh/document/product/1061/44246), and [CreateUploadUrl](https://intl.cloud.tencent.com/zh/document/product/1061/44246)
