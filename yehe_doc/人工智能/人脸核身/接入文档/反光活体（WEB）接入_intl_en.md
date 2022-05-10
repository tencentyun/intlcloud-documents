# Directions

## Integration Preparations
- Sign up for a Tencent Cloud account and log in to the [FaceID console](https://console.intl.cloud.tencent.com/faceid) to activate the service. 

## Terms and Definitions

- Customer H5: The H5 page developed by a customer
- Customer Server: The business backend of a customer
- Tencent Cloud API: The backend APIs provided by Tencent Cloud and used to obtain the face recognition credentials and the results
- Tencent Cloud H5: The authentication page developed by Tencent Cloud

## Sequence Diagram (Simplified)

![1](https://qcloudimg.tencent-cloud.cn/raw/f963c590fc88067f81da0b7ca3df50f8.png)

Backend APIs: [ApplyWebVerificationToken](https://intl.cloud.tencent.com/zh/document/product/1061/44246) and [GetWebVerificationResult](https://intl.cloud.tencent.com/zh/document/product/1061/44246)
## Sequence Diagram (Detailed)

In the real case, you need to input the URL of the comparison image to the backend API for getting the token. For use instructions and causes, see [Passing Resources](https://console.intl.cloud.tencent.com/faceid).
*`CreateUploadUrl` serves as an independent role in the diagram*

![2](https://qcloudimg.tencent-cloud.cn/raw/491abd12442624139fef0b39959a6745.png)

Backend APIs: [ApplyWebVerificationToken](https://intl.cloud.tencent.com/zh/document/product/1061/44246), [GetWebVerificationResult](https://intl.cloud.tencent.com/zh/document/product/1061/44246), and [CreateUploadUrl](https://intl.cloud.tencent.com/zh/document/product/1061/44246)
