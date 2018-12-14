## Description
This operation (Set Vault Notification Configuration) sets notification configuration on the vault. After configuration, the status of the related job changes to Completed. A notification will be sent to the specified URL, whose content is the same as that returned by Describe Job.
If the request is successful, 204 No Content is returned.

## Request
### Request syntax
```HTTP
PUT /<UID>/vaults/<VaultName>/notification-configuration HTTP 1.1
Host:cas.<Region>.myqcloud.com
Date:date
Authorization: Auth
```
### Request parameters
No additional request parameters are needed.
### Request headers
No additional request headers are needed except the headers described in "Common Request Headers".
### Request content
| Name | Description | Type | Required |
| ----------- | ---------------------------------------- | ------ | ---- |
| CallBackUrl | The HTTP address of the callback, which must start with http:// or https:// | String | Yes |
| Event | You can configure one or more events triggered by callback. Enumerated values: `ArchiveRetrievalCompleted`, `InventoryRetrievalCompleted`, `PushToCOSCompleted` and `PullFromCOSCompleted` | String | Yes |
```JSON
{
   "CallBackUrl": String,            //It must start with http:// or https://.
   "Events":[String, ...] 
}
```
## Response
### Response headers
No additional response headers are needed except the headers described in "Common Request Headers".
### Response content
No response content

