## 1. API Description

This API (ModifyNetworkAcl) is used to modify network ACL name.
Domain for API request:vpc.api.qcloud.com

## 2. Input Parameters

The following request parameter list only provides API request parameters. Common request parameters need to be added when the API is called. For more information, refer to [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/372/4153). The Action field for this API is ModifyNetworkAcl.

| Parameter Name | Required | Type   | Description                                                  |
| :------------- | :------- | :----- | :----------------------------------------------------------- |
| vpcId          | Yes      | String | Virtual private cloud ID of the subnet, which can be vpcId or unVpcId. unVpcId is recommended. For example: vpc-ktom9wg5. You can query this through API [DescribeVpcEx](https://intl.cloud.tencent.com/document/api/215/1372). |
| networkAclId   | Yes      | String | Network ACL ID assigned by the system. For example: acl-cva92t60. Can be queried via the API [DescribeNetworkAcl](https://intl.cloud.tencent.com/doc/api/245/1441). |
| networkAclName | Yes      | String | Network ACL name; you can specify any name you like, but its length should be limited to 60 characters. |

## 3. Output Parameters

| Parameter Name | Type   | Description                                     |
| :------------- | :----- | :---------------------------------------------- |
| code           | Int    | Error code, 0: Succeeded, other values: Failed. |
| message        | String | Error message.                                  |

## 4. Error Codes

The following error code list only provides the business logic error codes for this API. For additional common error codes, refer to [VPC Error Codes](https://intl.cloud.tencent.com/doc/api/245/4924).

| Error code                   | Description                                                  |
| :--------------------------- | :----------------------------------------------------------- |
| InvalidVpc.NotFound          | Invalid VPC. VPC resource does not exist. Please verify that the resource information you entered is correct. You can query VPCs via the API [DescribeVpcEx](https://intl.cloud.tencent.com/document/api/215/1372). |
| InvalidNetworkAclID.NotFound | Invalid network ACL ID. Network ACL ID does not exist. Please verify that the resource information you entered is correct. You can query network ACL IDs via the API [DescribeNetworkAcl](https://intl.cloud.tencent.com/doc/api/245/1441). |
| InvalidNetworkAclName        | Invalid network ACL name. You can specify any name you like, but its length should be limited to 60 characters. |

## 5. Example

Input

```
  https://vpc.api.qcloud.com/v2/index.php?Action=ModifyNetworkAcl
  &<Common request parameters>
  &vpcId=vpc-ktom9wg5
  &networkAclId=acl-cva92t60
  &networkAclName=barrytt
```

Output

```
{
    "code": 0,
    "message": ""
}
```