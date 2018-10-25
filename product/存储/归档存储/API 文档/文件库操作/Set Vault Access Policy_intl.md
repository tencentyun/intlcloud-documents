## Description

This operation (Set Vault Access Policy) configures an access policy for a vault. For more information on policy syntax, see "Verification and Authentication" -> "Access Policy Management".

The access policy can only be configured by the account that owns the vault, whose UID is "-". If the request is successful, 204 No Content is returned.

## Request

### Request syntax

```HTTP
PUT /<UID>/vaults/<VaultName>/access-policy HTTP 1.1
Host:cas.<Region>.myqcloud.com
Date:date
Authorization: Auth
```

### Request parameters

No additional request parameters are needed.

### Request headers

No additional request headers are needed except the headers described in "Common Request Headers".

### Request content

```JSON
{
  "policy":"String"
}
```

For ease of reading, the following table lists the values (i.e. String mentioned above) of the variable "Policy" **without escape character " \ "**. You must **escape quotation marks** and **eliminate line breaks**.

```json
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

Supported condition operations are as follows:

| ConditionOperator | Description | Condition Name | Example |
| ----------------------- | ------ | ---------------------- | ---------------------------------------- |
| ip_equal                | IP is equal to   | IP, which must comply with the CIDR standard.         | {" ip_equal  ":{"qcs:ip":"10.121.2.10/24"}} |
| ip_not_equal            | IP is not equal to  | IP, which must comply with the CIDR standard.         | {" ip_not_equal  ":{"qcs:ip":["10.121.2.10/24",  "10.121.2.20/24"]}} |
| date_not_equal          | Date is not equal to  | qcs:current_time (current time) | {"date_not_equal":{"qcs:current_time":"2016-01-01T12:00:11Z"}} |
| date_greater_than       | Date is greater than   | qcs:current_time (current time) | {" date_greater_than  ":{"qcs:current_time":"2016-01-01T12:00:11Z"}} |
| date_greater_than_equal | Date is greater than or equal to | qcs:current_time (current time) | {"  date_greater_than_equal ":{"qcs:current_time":2016-01-01T12:00:11Z"}} |
| date_less_than          | Date is less than   | qcs:current_time (current time) | {" date_less_than  ":{"qcs:current_time":"2016-01-01T12:00:11Z"}} |
| date_less_than_equal    | Date is less than or equal to | qcs:current_time (current time) | {"  date_less_than_equal ":{"qcs:current_time":"2016-01-01T12:00:11Z"}} |


## Response

### Response headers

No additional response headers are needed except the headers described in "Common Request Headers".

### Response content

No response content.

