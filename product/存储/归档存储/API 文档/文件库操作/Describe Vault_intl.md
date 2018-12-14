## Description

This operation (Describe Vault) returns information about a vault. The number of archives and their total size are as of the last vault inventory CAS generated. CAS generates vault inventories approximately daily. If the request is successful, 200 OK is returned.

Cross-account operation is supported. The UID is "-" when you get the information of a vault under the current account.

## Request

### Request syntax

```HTTP
GET /<UID>/vaults/<VaultName> HTTP 1.1
Host:cas.<Region>.myqcloud.com
Date:date
Authorization: Auth
```

### Request parameters

No additional request parameters are needed.

### Request headers

No additional request headers are needed except the headers described in "Common Request Headers".

### Request content

No request content

## Response

### Response headers

No additional response headers are needed except the headers described in "Common Request Headers".

### Response content

| Name | Description | Type |
| ----------------- | ---------------------------------------- | ------ |
| CreationDate | The UTC date when the vault was created. It is in an ISO 8601 date format, for example, `2017-03-20T17:03:43.221Z`. | String |
| LastInventoryDate | The UTC date when CAS completed the last vault inventory. It is in an ISO 8601 date format, for example, `2017-03-20T17:03:43.221Z`. | String |
| NumberOfArchives | The number of archives in the vault as per the last vault inventory. This field will return null if an inventory has not yet run on the vault. | Number |
| SizeInBytes | The total size in bytes of the archives in the vault as of the last inventory date. This field will return null if an inventory has not yet run on the vault. | Number |
| VaultQCS | The resource name (QCS) of the vault | String |
| VaultName | The vault name that was specified at creation time | String |

```JSON
{
  "CreationDate" : String,
  "LastInventoryDate" : String,
  "NumberOfArchives" : Number,
  "SizeInBytes" : Number,
  "VaultQCS" : String,
  "VaultName" : String
}
```
