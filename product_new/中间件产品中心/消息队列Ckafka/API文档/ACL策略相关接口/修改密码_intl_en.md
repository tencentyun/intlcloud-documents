>!This is a legacy API which has been hidden and will no longer be updated. We recommend using the new [CKafka API 3.0](https://intl.cloud.tencent.com/document/product/597/36407) which is standardized and faster.
>

> This feature is currently in beta. If you want to try this feature in the console, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to be allowed.

## 1. API Description
This API (ModifyPassword) is used to change the password for a user.

API domain name: `ckafka.api.qcloud.com`

## 2. Input Parameters
The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/product/406/5883).
 
| Parameter Name | Required | Type | Description |
| --- | --- | --- | --- |
| instanceId | Yes | String | Instance ID |
| name| Yes | String | Username must begin with a letter and can contain up to 64 letters, digits and underscores |
| passwordOld| Yes | String | Current user password |
| passwordNew| Yes | String | New user password can contain up to 64 letters, underscores and digits |

## 3. Samples

Input:

```
 https://domain/v2/index.php?Action=ModifyPassword
  &instanceId=ckafka-tadfqa0
  &name=user01
  &passwdOld=passold
  &passwdNew=passnew
  &<Common Request Parameters>
```

Output:

```
  {
      "code" : 0,
      "codeDesc":"Success",
      "message" : "ok"
  }

```
