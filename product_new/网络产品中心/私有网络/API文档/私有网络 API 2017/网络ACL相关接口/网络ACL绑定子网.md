## 1. API Description

This API (CreateSubnetAclRule) is used to bind network ACLs to subnets.
Domain for API request:vpc.api.qcloud.com

## 2. Input Parameters

The following request parameter list only provides API request parameters. Common request parameters need to be added when the API is called. For more information, refer to [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/372/4153). The Action field for this API is CreateSubnetAclRule.

| Parameter Name | Required | Type   | Description                                                  |
| :------------- | :------- | :----- | :----------------------------------------------------------- |
| vpcId          | Yes      | String | Virtual private cloud ID of the subnet, which can be vpcId or unVpcId. unVpcId is recommended. For example: vpc-erxok83l. You can query this through API [DescribeVpcEx](http://intl.cloud.tencent.com/doc/api/245/). |
| networkAclId   | Yes      | String | Network ACL ID assigned by the system. For example: acl-e9dbyl8s. Can be queried via the API [DescribeNetworkAcl](https://intl.cloud.tencent.com/doc/api/245/1441). |
| subnetIds.n    | Yes      | Array  | List of subnet IDs assigned by the system. Both subnetId and unSubnetId are supported. unSubnetId is recommended. For example: subnet-i6mdq6ra. You can query this through the API [DescribeSubnetEx](http://intl.cloud.tencent.com/doc/api/245/). |

## 3. Output Parameters

| Parameter Name | Type   | Description                                     |
| :------------- | :----- | :---------------------------------------------- |
| code           | Int    | Error code, 0: Succeeded, other values: Failed. |
| message        | String | Error message.                                  |

## 4. Error Code Table

The following error code list only provides the business logic error codes for this API. For additional common error codes, refer to [VPC Error Codes](https://intl.cloud.tencent.com/doc/api/245/4924).

| Error code                   | Description                                                  |
| :--------------------------- | :----------------------------------------------------------- |
| InvalidVpc.NotFound          | Invalid VPC. VPC resource does not exist. Please verify that the resource information you entered is correct. You can query VPCs via the API [DescribeVpcEx](http://intl.cloud.tencent.com/doc/api/245/). |
| InvalidNetworkAclID.NotFound | Invalid network ACL ID. Network ACL ID does not exist. Please verify that the resource information you entered is correct. You can query network ACL IDs via the API [DescribeNetworkAcl](https://intl.cloud.tencent.com/doc/api/245/1441). |

## 5. Example

Input

```
  https://vpc.api.qcloud.com/v2/index.php?Action=CreateSubnetAclRule
  &<Common request parameters>
  &vpcId=vpc-erxok83l
  &networkAclId=acl-e9dbyl8s
  &subnetIds.0=subnet-i6mdq6ra
```

Output

```
{
    "code": 0,
    "message": ""
}
```