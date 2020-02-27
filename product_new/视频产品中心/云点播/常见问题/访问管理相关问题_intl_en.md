### What permissions are needed to upload a file?

VOD offers multiple upload methods such as [upload from server](https://intl.cloud.tencent.com/document/product/266/33912), [upload from client](https://intl.cloud.tencent.com/document/product/266/33921), [pull from URL](https://intl.cloud.tencent.com/document/product/266/34118). The permissions required for each method are as follows:

| Upload Method | Permission to Resources |  Permission to Operations | Remarks |
| ---------- | ------------ | ------------------------------------------------------------ | ------------------ |
| Upload from server | Specified subapplication | [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120)<br/>[CommitUpload](https://intl.cloud.tencent.com/document/product/266/34119) | -  |
| Upload from client | Specified subapplication | [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120)<br/>[CommitUpload](https://intl.cloud.tencent.com/document/product/266/34119) | -  |
| Pull from URL | Specified subapplication |  [PullUpload](https://intl.cloud.tencent.com/document/product/266/34118) | - |
| LVB recording   | All subapplications   | -  | The LVB recording feature needs to be enabled |

>[Local upload](https://intl.cloud.tencent.com/document/product/266/33890#.E6.9C.AC.E5.9C.B0.E4.B8.8A.E4.BC.A0.E6.AD.A5.E9.AA.A4) of videos in the VOD Console is a form of upload from client.

### A "no permission" error is returned for upload from server, but upload through other methods can succeed. Why?

This is probably because the server SDK is too old. Please upgrade the SDK to the latest [version](https://intl.cloud.tencent.com/document/product/266/33912#1.-.E5.8F.91.E8.B5.B7.E4.B8.8A.E4.BC.A0).

### What permission is needed to watch videos?

To watch a video is essentially to make a request to VOD CDN as an ordinary viewer rather than a Tencent Cloud account, so you do not need to grant a viewer any permissions (if [hotlink protection](https://intl.cloud.tencent.com/document/product/266/33984) or [video encryption](https://intl.cloud.tencent.com/document/product/266/33968) is enabled, the conditions as described in applicable documents must be met before the video can be watched, but these are irrelevant to access control).

### Can permissions to an individual file be granted?

No. The resource granularity of VOD access control is subapplication.

### What if permission settings are in conflicts?

The possible reasons of conflicts are as follows:

- A custom policy contains multiple statements where there are conflicting descriptions (for example, one statement allows access to a resource, but another one denies such access).
- A subuser is bound to multiple policies where there are conflicting descriptions.

As VOD permission management is based on CAM, VOD permissions are determined in accordance with the policy [judgment logic](https://intl.cloud.tencent.com/document/product/598/10605) of CAM.

### Does VOD support cross-account resource access?

Cross-account resource access refers to that root account A grants all or some of its VOD permissions to root account B (or its subaccounts), that is, the grantor and grantee are two independent Tencent Cloud accounts. VOD **does not support** cross-account resource access, i.e., a Tencent Cloud account can only grant VOD permissions to its own subaccounts.
