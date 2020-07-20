### Introduction
COS allows you to configure access permissions for objects, which have a higher priority than that for buckets.

>
>- The access permission for an object is valid only when the user accesses said object via the default domain name. When access is made via a CDN acceleration endpoint domain name or custom domain name, the bucket access permission takes priority.
>- There are limits on the number of access policy rules that can exist at a given time. For details, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

### Directions




1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Find the bucket where the target object is located and click the bucket name to enter the bucket details page.
![](https://main.qcloudimg.com/raw/156823c7ad23708feb85f5d682c61d50.png)
3. In the [File List], find the object for which to configure access permission, and click [Details] on the right to enter the file details page (If it is a folder, click [Permissions] on the right).
![](https://main.qcloudimg.com/raw/6065855393a30c809d60b4d0027628a6.png)
4. Scroll down to the [Object ACL] section near the top of the page and configure access permissions as needed (such as granting object permission to a sub-account, sub-account ID can be found on the [Cloud Access Management](https://console.cloud.tencent.com/cam) console). COS supports two types of object permissions:
 - **Public Permissions**: Inherited permissions, private read/write, and public read/private write. For more information on public permissions, see [Access Permission Types](https://intl.cloud.tencent.com/document/product/436/13324).
 - **User Permissions**: The root account has all object permissions (full access) by default. In addition, COS allows you to grant sub-accounts read/write permission for data and/or permission information and even allows **full access** permission to be granted to sub-accounts.
![](https://main.qcloudimg.com/raw/c9565ab1d2378ce672a301843bf3b072.png)
5. Click [Save] to configure the object access permissions.
6. If you need to configure or modify access permissions for multiple objects by performing a batch operation, you can check multiple objects from the file list and select [Modify Access Permissions] under [More Actions].


