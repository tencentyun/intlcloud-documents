## Restricted Access
When you log in to the console to perform an operation on a cloud product, you may receive a message indicating that you have no permission to perform such operation on the resources, as shown below:
![](https://main.qcloudimg.com/raw/d0b3aa8555810a16c0117f72bfc3e355.png)
In this case, it is because the sub-user account or collaborator account you logged in are not granted the relevant permissions - the root account needs to grant the corresponding permissions before you can view the information or perform related operations.

## Authorization Steps
1. Confirm the permissions to be granted.
  The error message  shown above indicates that you are not yet authorized to access API LookupEvents in CloudAudit, so you cannot view the page.

2. Authorize sub-users or collaborators through root accounts or sub-accounts that have management permissions.

   1. Log in to the [CAM console](https://console.cloud.tencent.com/cam). On the **Policy Management** page, click **Create Custom Policy** -> **Create by Policy Generator** to assign permissions to a specific API, such as LookupEvents.
   2. On the policy management page, check the product's system policies and grant the default policies to the sub-user, such as the preset CloudAudit-related policies in this example.
![](https://main.qcloudimg.com/raw/72438c9189b88bcd0833ccd039abcdb0.png)

