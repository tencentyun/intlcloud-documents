## 1. API Description

This API (DeteleSubnetAclRule) is used to unbind network ACLs from subnets.
Domain for API request:vpc.api.qcloud.com

## 2. Input Parameters

The following request parameter list only provides API request parameters. Common request parameters need to be added when the API is called. For more information, refer to [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/372/4153). The Action field for this API is DeteleSubnetAclRule.

| Parameter Name | Required | Type   | Description                                                  |
| :------------- | :------- | :----- | :----------------------------------------------------------- |
| vpcId          | Yes      | String | VPC ID of the subnet, which can be vpcId or unVpcId. unVpcId is recommended. You can query this through API [DescribeVpcEx](https://intl.cloud.tencent.com/document/api/215/1372). |
| networkAclName | Yes      | String | Network ACL name, which can be 1-60 Chinese or English characters (uppercase and lowercase). Numbers and underscores are also supported. The name must be unique under the same VPC. |
| subnetIds.n    | Yes      | Array  | List of subnet IDs assigned by the system. Both subnetId and unSubnetId are supported. unSubnetId is recommended. You can query it by using the API [DescribeSubnetEx](https://intl.cloud.tencent.com/document/api/215/1371). |

## 3. Output Parameters

| Parameter Name | Type   | Description                                     |
| :------------- | :----- | :---------------------------------------------- |
| code           | Int    | Error code, 0: Succeeded, other values: Failed. |
| message        | String | Error message.                                  |

## 4. Error Code Table

The following error code list only provides the business logic error codes for this API. For additional common error codes, refer to [VPC Error Codes](https://intl.cloud.tencent.com/doc/api/245/4924).

| Error code                   | Description                                                  |
| :--------------------------- | :----------------------------------------------------------- |
| InvalidVpc.NotFound          | Invalid VPC. VPC resource does not exist. Please verify that the resource information you entered is correct. You can query VPCs via the API [DescribeVpcEx](https://intl.cloud.tencent.com/document/api/215/1372). |
| InvalidNetworkAclID.NotFound | Invalid network ACL ID. Network ACL ID does not exist. Please verify that the resource information you entered is correct. You can query network ACL IDs via the API [DescribeNetworkAcl](https://intl.cloud.tencent.com/document/api/215/1441). |

## 5. Example

Input

```
  https://vpc.api.qcloud.com/v2/index.php?Action=DeteleSubnetAclRule
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