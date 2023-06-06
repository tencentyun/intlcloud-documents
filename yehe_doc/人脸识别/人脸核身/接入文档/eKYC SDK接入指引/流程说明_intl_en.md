## Integration Preparations
- Sign up for a Tencent Cloud account and log in to the [eKYC console](https://console.intl.cloud.tencent.com/faceid) to activate the service. 
- [Contact us ](https://www.tencentcloud.com/document/product/1061/52144) to get the latest [SDK](https://console.intl.cloud.tencent.com/faceid) and [license](https://console.intl.cloud.tencent.com/faceid) .

## Terms and Definitions

- Customer APP: An app developed by a customer
- Customer Server: The business backend of a customer
- Tencent Cloud API: The backend APIs provided by Tencent Cloud and used to obtain the face recognition credentials and the results
- SDK: The SDK provided by Tencent Cloud for Android or iOS, which is used to integrate the customer apps and start the face recognition together with backend APIs.

## Sequence Diagram (Simplified)

Major roles involved are as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/728a228977a5c7bfa67d2a5af098722b.png)

Backend APIs: [ApplySdkVerificationToken](https://www.tencentcloud.com/document/product/1061/49954) and [GetSdkVerificationResult](https://www.tencentcloud.com/document/product/1061/49951)
