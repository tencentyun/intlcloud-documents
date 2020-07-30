>!This is a legacy API which has been hidden and will no longer be updated. We recommend using the new [CKafka API 3.0](https://intl.cloud.tencent.com/document/product/597/36407) which is standardized and faster.
>

> This feature is currently in beta. If you want to try this feature in the console, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to be allowlisted.

## 1. API Description

This API (ListAcl) is used to query the ACL policy list for users of an instance.

API domain name: `ckafka.api.qcloud.com`

## 2. Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/product/406/5883).

| Parameter Name | Required | Type | Description |
| --- | --- | --- | --- |
| instanceId | Yes | String | Instance ID |
| resourceType| Yes | Int| ACL resource type (0: UNKNOWN; 1: ANY; 2: TOPIC; 3: GROUP; 4: CLUSTER; 5: TRANSACTIONAL_ID) |
| resourceName| Yes | String | Resource name is related to `resourceType`. For example, when `resourceType` is `TOPIC`, this field represents the topic name; when `resourceType` is `GROUP`, this field represents the group name |
| searchWord| No | String | (Filter) Filter by resource name. Fuzzy search is supported |
| offset| No | String | Offset. Default value is 0 if left empty |
| limit| No | String | Number of results to be returned. Default value is 10 if left empty. Maximum value is 20 |


## 3. Output Parameters
| Parameter Name | Type | Description |
| --- | --- | --- |
| acls | Array | ACL policy list |
| acls::resourceType | Int | ACL resource type (0: UNKNOWN; 1:ANY; 2:TOPIC; 3:GROUP; 4:CLUSTER; 5:TRANSACTIONAL_ID) |
| acls::resourceName | String | Resource name is related to `resourceType`. For example, when `resourceType` is `TOPIC`, this field represents the topic name; when `resourceType` is `GROUP`, this field represents the group name |
| acls::operation | Int | ACL operation method (0: UNKNOWN; 1: ANY; 2: ALL; 3: READ; 4: WRITE; 5: CREATE; 6: DELETE; 7: ALTER; 8: DESCRIBE; 9: CLUSTER_ACTION; 10: DESCRIBE_CONFIGS; 11: ALTER_CONFIGS; 12: IDEMPOTEN_WRITE) |
| acls::permissionType | Int | Permission type (0: UNKNOWN; 1:ANY; 2:DENY; 3:ALLOW) |
| acls::host | String | Host IP for ACL policy |
| acls::principal | Int | User lists associated with ACL policy |

## 4. Samples


Input:

```
 https://domain/v2/index.php?Action=ListAcl
  &instanceId=ckafka-tadfqa0
  &resourceType=2
  &resourceName=test-topic
  &<Common Request Parameters>
```

Output:

```
{
"code":0,
"message":"",
"codeDesc":"Success",
"data":{
 "acls":[
  {
   "resourceType":2,
   "resourceName":"topic-a",
   "host":"*",
   "permissionType":3,
   "operation":3,
   "principal":"User:anonymous"
  },
  {
   "resourceType":2,
   "resourceName":"topic-a",
   "host":"*",
   "permissionType":3,
   "operation":3,
   "principal":"User:blob"
  }
 ]
}
}

```
