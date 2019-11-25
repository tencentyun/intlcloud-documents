## Overview

Cloud Access Management (CAM) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control who can access and use your Tencent Cloud resources through identity and policy management. For more information and uses of CAM policies, see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).

The root account can grant sub-accounts or collaborators permission to access specific cloud log service resources. For more information on resources, see [Action List](https://intl.cloud.tencent.com/document/product/614/32855) and [Resource List](https://intl.cloud.tencent.com/document/product/614/32856).

>
> - It is recommended to grant the minimum permission required for an account to ensure security.
> - Actions marked with `list` indicate that the current user can view all resources rather than only some of the resources. For example, when a user has permission for the listTopic action, all log topic lists in the current logset rather than a partial list of log topics can be displayed. Otherwise, a user without permission for the listTopic action cannot view any log topics.


## Example
#### Console scenario: all permissions for CLS

Description: the root account (UIN: 123456789) grants sub-accounts or collaborators permission to access and operate logs on the [Cloud Log Service Console](https://console.cloud.tencent.com/cls).

The CAM authorization policy is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cls:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```



#### Console scenario: read-only permission for logsets and log topics

Description: the root account (UIN: 123456789) grants sub-accounts or collaborators permission to perform the following operations on the [Cloud Log Service Console](https://console.cloud.tencent.com/cls):

- View the root account logset list.
- View basic information and the log topic list of the logset (abcd0000-abcd-abcd-abcd-abcd11110000) in the Shanghai region.
- View basic information of the log topic (123e4567-e89b-12d3-a456-426655440000) in the current logset, including collection, index, and shipping configurations and shipping task lists.

The CAM authorization policy is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:listLogset"
            ],
            "resource": [
                "qcs::cls:ap-shanghai:uin/123456789:logset/*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "cls:list*",
                "cls:get*"
            ],
            "resource": [
                "qcs::cls:ap-shanghai:uin/123456789:logset/abcd0000-abcd-abcd-abcd-abcd11110000",
                "qcs::cls:ap-shanghai:uin/123456789:topic/123e4567-e89b-12d3-a456-426655440000"
            ]
        }
    ]
}
```



#### Console scenario: read-only permission for server groups

Description: the root account (UIN: 123456789) grants sub-accounts or collaborators permission to perform the following operations on the [CLS Console](https://console.cloud.tencent.com/cls):
- View the root account server group list.
- View information about all server groups in the Shanghai region, including the server list and status.

The CAM authorization policy is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:listMachineGroup",
                "cls:getMachineGroup",
                "cls:getMachineStatus"
            ],
            "resource": [
                "qcs::cls:ap-shanghai:uin/123456789:machinegroup/*"
            ]
        }
    ]
}
```



#### Console scenario: permission for log topic search

Description: the root account (UIN: 123456789) grants sub-accounts or collaborators permission to search the log topic (123e4567-e89b-12d3-a456-426655440000) in the Shanghai logset (abcd0000-abcd-abcd-abcd-abcd11110000) of the root account on the [CLS Console](https://console.cloud.tencent.com/cls).

The CAM authorization policy is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:listLogset"
            ],
            "resource": [
                "qcs::cls:ap-shanghai:uin/123456789:logset/*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "cls:listTopic"
            ],
            "resource": [
                "qcs::cls:ap-shanghai:uin/123456789:logset/abcd0000-abcd-abcd-abcd-abcd11110000"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "cls:searchLog"
            ],
            "resource": [
                "qcs::cls:ap-shanghai:uin/123456789:logset/abcd0000-abcd-abcd-abcd-abcd11110000",
                "qcs::cls:ap-shanghai:uin/123456789:topic/123e4567-e89b-12d3-a456-426655440000"
            ]
        }
    ]
}
```



#### Console scenario: permission for viewing log topic shipping tasks

Description: the root account (UIN: 123456789) grants sub-accounts or collaborators permission to view the shipping task (1234abcd-0000-0000-0000-1234abcd0000) in the log topic (123e4567-e89b-12d3-a456-426655440000) in the Shanghai logset (abcd0000-abcd-abcd-abcd-abcd11110000) of the root account on the [CLS Console](https://console.cloud.tencent.com/cls).

The CAM authorization policy is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:listLogset"
            ],
            "resource": [
                "qcs::cls:ap-shanghai:uin/123456789:logset/*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "cls:listTopic"
            ],
            "resource": [
                "qcs::cls:ap-shanghai:uin/123456789:logset/abcd0000-abcd-abcd-abcd-abcd11110000"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "cls:listShipper"
            ],
            "resource": [
                "qcs::cls:ap-shanghai:uin/123456789:topic/123e4567-e89b-12d3-a456-426655440000"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "cls:listShipperTask"
            ],
            "resource": [
                "qcs::cls:ap-shanghai:uin/123456789:shipper/1234abcd-0000-0000-0000-1234abcd0000"
            ]
        }
    ]
}
```


#### API scenario: write and download permission for log topics

Description: the root account (UIN: 123456789) grants sub-accounts or collaborators permission to perform the following operations through the [API](https://intl.cloud.tencent.com/document/product/614/16907):

- Write data to the log topic (123e4567-e89b-12d3-a456-426655440000) of the root account.
- Download data from the log topic (123e4567-e89b-12d3-a456-426655440000) of the root account.

The CAM authorization policy is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cls:getCursor",
                "cls:downloadLog",
                "cls:pushLog"
            ],
            "resource": [
                "qcs::cls:ap-shanghai:uin/123456789:topic/123e4567-e89b-12d3-a456-426655440000"
            ]
        }
    ]
}
```
