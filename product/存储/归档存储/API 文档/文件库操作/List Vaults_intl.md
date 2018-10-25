## Description

This operation (List Vaults) lists all vaults owned by the calling user's account. The number of archives and their total size are as of the last vault inventory CAS generated. CAS generates vault inventories approximately daily.

Cross-account operation is supported. The UID is "-" when the operation is performed in the account that owns the vault.

## Request

### Request syntax

```HTTP
GET /<UID>/vaults HTTP/1.1
Host:cas.<Region>.myqcloud.com
Date:date
Authorization: Auth
```

### Request parameters

| Name | Description | Type | Required |
| ------ | ---------------------------------------- | ------ | ---- |
| limit | The maximum number of vaults to be returned. It should be a positive integer ranging from `1`-`1000`. It is `1000` by default. | String | No |
| marker | Lists the QCSs of the vaults starting from the specified marker in lexicographical order. Specifying an empty value for the marker returns a list of vaults starting from the first vault. | String | No    |

### Request headers

No additional request headers are needed except the headers described in "Common Request Headers".

### Request content

No request content.

## Response

### Response headers

No additional response headers are needed except the headers described in "Common Request Headers".

### Response content

| Name | Description | Type |
| ----------------- | ---------------------------------------- | ------ |
| Marker | If not all results are included in the returned list, this value is used as the marker value for the next request. If the returned list displays all results, this value is `null`. | String |
| Vault List | Vault description | Array |
| CreationDate | The date the vault was created. It is in an ISO 8601 date format, for example, `2017-03-20T17:03:43.221Z` | String |
| LastInventoryDate | The date of the last vault inventory. It is in an ISO 8601 date format, for example, `2017-03-20T17:03:43.221Z` | String |
| NumberOfArchives | The number of archives in the vault as of the last inventory date | Number |
| SizeInBytes | The total size of all the archives in the vault as of the last inventory date  | Number |
| VaultQCS | The resource name (QCS) of the vault | String |
| VaultName | The vault name | String |

```JSON

{
  "Marker": String,
  "VaultList": [ 
   {
    "CreationDate": String,
    "LastInventoryDate": String,
    "NumberOfArchives": Number,
    "SizeInBytes": Number,
    "VaultQCS": String,
    "VaultName": String
   }
   ...
  ]
}
```

