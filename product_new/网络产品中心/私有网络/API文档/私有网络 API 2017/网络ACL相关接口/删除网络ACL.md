## 1. API Description

This API (DeleteNetworkAcl) is used to delete network ACL.
Domain for API request:vpc.api.qcloud.com

Network ACLs with bound subnets cannot be deleted. You need to unbind any subnets from the network ACL before you can delete it.

## 2. Input Parameters

The following request parameter list only provides API request parameters. Common request parameters need to be added when the API is called. See the[ Common Request Parameters](https://intl.cloud.tencent.com/doc/api/372/4153) page for details. The Action field for this API is DeleteNetworkAcl.

| Parameter Name | Required | Type   | Description                                                  |
| :------------- | :------- | :----- | :----------------------------------------------------------- |
| vpcId          | Yes      | String | Virtual private cloud ID of the subnet, which can be vpcId or unVpcId. unVpcId is recommended. For example: vpc-erxok83l. You can query this through API [DescribeVpcEx](https://intl.cloud.tencent.com/document/api/215/1372). |
| networkAclId   | Yes      | String | Network ACL ID assigned by the system. For example: acl-jk7weyp2. Can be queried via the [DescribeNetworkAcl](https://intl.cloud.tencent.com/doc/api/245/1441) API. |

## 3. Output Parameters

| Parameter Name | Type   | Description                                    |
| :------------- | :----- | :--------------------------------------------- |
| code           | Int    | Error code, 0: Succeeded, other values: failed |
| message        | String | Error message                                  |

## 4. Error Codes

The following error code list only provides the business logic error codes for this API. For additional common error codes, refer to [VPC Error Codes](https://intl.cloud.tencent.com/doc/api/245/4924).

| Error code                   | Description                                                  |
| :--------------------------- | :----------------------------------------------------------- |
| InvalidVpc.NotFound          | The VPC does not exist. Please check the information you entered. You can query the VPC via the [DescribeVpcEx](http://intl.cloud.tencent.com/doc/api/245/1372) API. |
| InvalidNetworkAclID.NotFound | The network ACL ID does not exist. Please check the information you entered. You can query network ACL IDs via the [DescribeNetworkAcl](https://intl.cloud.tencent.com/doc/api/245/1441) API. |
| NetworkAclID.InUse           | There are subnets associated with the network ACL. ACLs with associated subnets cannot be deleted. |

## 5. Example

Input

```
  https://vpc.api.qcloud.com/v2/index.php?Action=DeleteNetworkAcl
  &<Common request parameters>
  &vpcId=vpc-erxok83l
  &networkAclId=acl-jk7weyp2
```

Output

```
{
    "code": 0,
    "message": ""
}
```


