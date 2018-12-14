## Description

This operation (Get Vault Access Policy) retrieves the access-policy subresource set on the vault.

The access policy can only be deleted by the account that owns the vault, whose UID is "-". If the request is successful, 200 OK is returned.

## Request

### Request syntax

```HTTP
GET /<UID>/vaults/<VaultName>/access-policy HTTP 1.1
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

```json
{
  "policy":"String"
}
```

The values in String are as follows.

```JSON
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "principal": {
              "qcs": [
                "qcs::cam::uin/<RootAccout>:uin/<SubAccount>",
                "qcs::cam::uin/<RootAccout>:uin/<SubAccount>"
              ]
            },
            "action": [
                "name/cas:<ActionName>"
            ],
            "resource": [
                "qcs::cas:<Region>:uid/<Accout>:vaults/<VaultName>",
                "qcs::cas:<Region>:uid/<Accout>:vaults/<VaultName>"
            ],
            "condition": {
                "<ConditionOperator>": {
                    "<ConditionName>": [
                        "<ConditionValue>",
                        "<ConditionValue>"
                    ]
                }
            }
        }
    ]
}
```


