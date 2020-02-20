## Value-added Service Fees

Value-added services include instant messaging, relayed live streaming, on-cloud recording, On-Cloud MixTranscoding, screencapturing, and porn information detection. These features can only be implemented when used together with other Tencent Cloud products such as IM, LVB, and VOD. Each value-added service has its own independent billing rule, and fees will be charged by the corresponding Tencent Cloud product.
**IM is offered as the free trial edition for TRTC with other value-added services disabled by default. After a value-added service is activated, it will not be charged if not used.**
Value-added service fees are shown as below:
<!--![Value-added service fees (global website)](Value-added service fees (global website).png)-->

## IM Fees

To facilitate you to integrate both TRTC and IM into the same product, when you create a TRTC application, the system will automatically create an IM application with the same `SDKAppID` as the TRTC application. IM provides real-time communication features such as one-to-one chat, group chat, message push, material and relationship chain hosting, and account authentication.

| Value-added Item | Billed Product | Billing Details |
| :----------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Instant messaging | [IM](https://intl.cloud.tencent.com/document/product/1047) | The Trial Edition for TRTC of IM is free of charge forever. You can purchase different [IM editions]() based on your actual needs. For more information, please see [IM]() |

> Note:
>
> If TRTC and IM applications have the same `SDKAppID`, they can share account and authentication data of each other.

## Relayed Live Streaming Fees

The relayed live streaming feature is disabled by default. For feature overview and instructions, please see [CDN-based Relayed Live Streaming]().

| Value-added Item | Billed Product | Billing Details |
| :----------- | :--------- | :----------------------------------------------------------- |
| CDN-based relayed live streaming | [LVB]() | It can be billed by **traffic** or **bandwidth**. You can choose an appropriate billing mode based on your actual needs. The bill-by-traffic mode is used by default. For more information, please see [LVB]() |

## On-cloud Recording Fees

The on-cloud recording feature is disabled by default. For feature overview and instructions, please see [On-cloud Recording]().

| Value-added Item | Billed Product | Billing Details |
| :------------------------- | :--------- | :----------------------------------------------------------- |
| LVB recording | [LVB]() | It is billed by the **peak number of concurrent LVB recording channels in the current month**. For more information, please see [LVB]() |
| Video file storage | [VOD]() | It is billed by the **storage capacity used by recording files stored in the VOD platform**. For more information, please see [VOD]() |
| Playback or download of recorded video files | [VOD]() | It is billed by the **downstream accelerated traffic**. For more information, please see [VOD]() |

> Note:
>
> If recording fees are charged for on-cloud recording, no traffic or bandwidth fees will be charged again.

## On-Cloud MixTranscoding Fees

The On-Cloud MixTranscoding feature is disabled by default. For feature overview and instructions, please see [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618). To use this feature, you need to activate LVB and [configure transcoding](https://intl.cloud.tencent.com/document/product/267/31062) in the LVB Console based on your business needs.

| Value-added Item | Billed Product | Billing Details |
| :--------------- | :------------------------------------------------------- | :----------------------------------------------------------- |
| On-Cloud MixTranscoding | [LVB](https://intl.cloud.tencent.com/document/product/267) | It is billed by the **duration of On-Cloud MixTranscoding for different codecs and resolutions**. For more information, please see [LVB]() |

## Screencapturing and Porn Information Detection Fees

The screencapturing and porn information detection feature is disabled by default. For feature overview and instructions, please see [Screencapturing and Porn Information Detection Settings](https://intl.cloud.tencent.com/document/product/267/31072).

| Value-added Item | Billed Product | Billing Details |
| :------- | :------------------------------------------------------- | :---------------------------------------- |
| LVB screencapturing | [LVB](https://intl.cloud.tencent.com/document/product/267) | It is billed by the **number of screenshots**. For more information, please see [LVB]() |
| Intelligent porn information detection | [LVB](https://intl.cloud.tencent.com/document/product/267) | It is billed by the **number of images for porn information detection**. For more information, please see [LVB]() |
