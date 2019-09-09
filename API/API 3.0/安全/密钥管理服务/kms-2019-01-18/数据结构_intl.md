## Key

Returned CMK list information

Referenced by: ListKeys.

| Name | Type | Description |
|------|------|-------|
| KeyId | String | Globally unique ID of the CMK |

## KeyMetadata

CMK attribute information

Referenced by: DescribeKey, DescribeKeys, ListKeyDetail.

| Name | Type | Description |
|------|------|-------|
| KeyId | String | Globally unique ID of the CMK |
| Alias | String | Alias that makes a key more recognizable and understandable |
| CreateTime | Integer | Key creation time |
| Description | String | CMK description |
| KeyState | String | CMK status. Valid values: Enabled, Disabled, Deleted |
| KeyUsage | String | Current CMK usage: ENCRYPT_DECRYPT |
| Type | Integer | Current CMK type: 1 (common type) |
| CreatorUin | Integer | CMK creator’s Uin |
| KeyRotationEnabled | Boolean | Whether key rotation is enabled |
| Owner | String | CMK creator. User: CMK created by the user; product name: CMK created automatically by the specified Tencent Cloud product |
| NextRotateTime | Integer | Time of next rotation if key rotation is enabled |

