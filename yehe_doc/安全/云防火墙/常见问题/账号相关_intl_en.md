
### Can I use CFW under another Tencent Cloud account?
No. CFW cannot be used across accounts. It can only protect cloud assets under the current Tencent Cloud primary account.

### Will my service be affected when I add role authorization?
No. By adding role authorization, you allow the Cloud Firewall console to read your VPCs, subnets, and other cloud resources, so that related data can be displayed on the page. This will not affect any automatic operation of your service.

### Can I receive bandwidth alerts if primary account and sub-account are not configured as alert objects in Alert Management?
If no primary account or sub-account is selected for receiving alerts, you will not be notified via SMS from Alert Management, Message Center, or WeChat. However, alerts will still be displayed on the console.

### How can I grant CFW permissions to sub-accounts?
You need to create a CFW role in CAM, and then add the following permissions to your sub-accounts:
- QcloudCFWReadOnlyAccess
- QcloudAccessForCFWRole
- QcloudAccessForCFWRoleInUploadLog
- QcloudAccessForCFWRoleInVPCFireWall
- QcloudCFWFullAccess
- QcloudCamSubaccountsAuthorizeRoleFullAccess"

### What if I failed to open the CVM overview page with a warning message displayed: you are not authorized to perform operation(cfw:DescribeCfwUserStatus)	?
In this case, grant the following permissions to the current sub-account:
- QcloudCFWFullAccess
- QcloudCFWReadOnlyAccess"
