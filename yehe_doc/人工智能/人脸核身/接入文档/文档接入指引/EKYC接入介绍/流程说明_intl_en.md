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

# 图片1

Backend APIs: [ApplySdkVerificationToken](https://intl.cloud.tencent.com/zh/document/product/1061/44246) and [GetSdkVerificationResult](https://intl.cloud.tencent.com/zh/document/product/1061/44246)