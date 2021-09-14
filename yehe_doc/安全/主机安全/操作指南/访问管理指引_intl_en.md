## Background
If you have used multiple Tencent Cloud services, which are managed by different users who share your root account key with the highest permission, the following problems may exist:
- Your key is shared by multiple users, posing huge risks of data breaches.
- Your users might introduce security risks from misoperations due to the lack of user access control.

In this case, you can create multiple users in [CAM](https://intl.cloud.tencent.com/document/product/598/10583) to take charge of different services, and give them permissions on different consoles by associating policies. This document provides samples to guide you on how to use the CWP access policies.

## Samples
### Full access policy
To grant your users full access to all CWP APIs, you need to  associate the policy QcloudCWPFullAccess with them.
See [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602) to grant users full access with the preset policy QcloudCWPFullAccess.

### Read-only policy
To grant users query access to CWP, without other permission to add, delete, and modify, you need to associate the policy QcloudCWPReadOnlyAccess with them. The policy is implemented by restricting user access to the APIs starting with "Describe", "Get", "Check", and "Export".
See [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602) to grant users read-only access with the preset policy QcloudCWPReadOnlyAccess.

### Custom policies
If the preset policies cannot meet your needs, you can [create a custom policy](https://intl.cloud.tencent.com/document/product/598/35596).

<dx-alert infotype="explain" title="">
New users will not be associated with any CWP policies by default, indicating they do not have any permissions. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/598/17848).
</dx-alert>
