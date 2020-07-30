>!This is a legacy API which has been hidden and will no longer be updated. We recommend using the new [CKafka API 3.0](https://intl.cloud.tencent.com/document/product/597/36407) which is standardized and faster.
>

> This feature is currently in beta. If you want to try this feature in the console, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to be allowed.

## 1. API Description
This API (DeleteAcl) is used to delete the ACL policy for users of an instance.

API domain name: `ckafka.api.qcloud.com`

## 2. Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/product/406/5883).

| Parameter Name | Required | Type | Description |
| --- | --- | --- | --- |
| instanceId | Yes | String | Instance ID |
| resourceType| Yes | Int| ACL resource type (0: UNKNOWN; 1: ANY; 2: TOPIC; 3: GROUP; 4: CLUSTER; 5: TRANSACTIONAL_ID) |
| resourceName| Yes | String | Resource name is related to `resourceType`. For example, when `resourceType` is `TOPIC`, this field represents the topic name; when `resourceType` is `GROUP`, this field represents the group name |
| operation| Yes | Int| ACL operation method (0: UNKNOWN; 1: ANY; 2: ALL; 3: READ; 4: WRITE; 5: CREATE; 6: DELETE; 7: ALTER; 8: DESCRIBE; 9: CLUSTER_ACTION; 10: DESCRIBE_CONFIGS; 11: ALTER_CONFIGS; 12: IDEMPOTEN_WRITE) |
| permissionType| Yes | Int | Permission type (0: UNKNOWN; 1:ANY; 2:DENY; 3:ALLOW) |
| host| Yes | String | Host IP for ACL policy is \* by default, indicating that any host can access |
| principal| Yes | String | List of users associated with ACL policy. Default value is User:\*, indicating all users of the instance |

## 3. Samples

Input:

```
  https://domain/v2/index.php?Action=AddAcl
  &instanceId=ckafka-tadfqa0
  &resourceType=2
  &resourceName=test-topic
  &operation=0
  &permissionType=3
  &host=*
  &principal=User:user1
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
