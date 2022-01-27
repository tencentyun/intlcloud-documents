Cloud Access Management (CAM) is a user and permission management system provided by Tencent Cloud for the refined management of access to IMS and its specific APIs. Currently, IMS supports **service-level authorization** and console operations. For more information, see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

>? You can skip this section if you don't need to manage access to IMS resources for sub-accounts. This will not affect your understanding and use of the other sections of the document.

## Use Cases

- If you have multiple businesses under your Tencent Cloud account which need to be managed separately, you can create sub-users/collaborators in CAM and assign them to the admins of different businesses.
- CAM enables you to configure different access permissions for your partners or employees and specify which operations they can perform and which resources they can access, thus implementing least privilege management.
- If you have set up an account management system based on the private network, you can connect CAM to your existing authentication system to grant your employees and partners access to Tencent Cloud services and resources.