## Access Restricted
When you try to perform an operation on a Tencent Cloud service, you may say a message indicating that you are not authorized to perform the operation on the resource as shown below:
![](https://main.qcloudimg.com/raw/bad75cdb92e33a8ef02aaaef50143ab3.png)
That is because the sub-account or collaborator account you use to log in to the console is not granted the necessary permissions. You need to get the permissions from the root account before you can view the information or perform the operation.

## Authorization Steps
1. Verify the permissions you need.
  The error message indicates what permissions you need. As shown in the image above, you do not have the permission to use the `DescribeInstances` API for the CVM product. That is why you cannot see the page.

2. Use the root account or a sub-account that has management permissions to grant necessary permissions to the sub-account or collaborator account.

 - Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview), and go to the [Policies](https://console.cloud.tencent.com/cam/policy) page. Click **Create Custom Policy** > **Create by policy generator**. Grant the permission to use the specified API, such as `DescribeInstances` in this example. For detailed directions, see [Using the Policy Generator to Create Policies](https://intl.cloud.tencent.com/document/product/598/10601).
  - On the Policies page, locate the preset policies corresponding to the product, and associate the policies with the sub-account, such as the preset policies related to CVMs in this example. For details directions, see [Associating a Preset Policy with a User/User Group](https://intl.cloud.tencent.com/document/product/598/10602#associating-a-policy-with-a-user.2Fuser-group).
