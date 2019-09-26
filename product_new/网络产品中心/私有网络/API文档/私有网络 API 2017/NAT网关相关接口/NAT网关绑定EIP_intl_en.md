## 1. API Description

This API (EipBindNatGateway) is used to bind EIP for NAT gateway
Domain for API request:vpc.api.qcloud.com

## 2. Input Parameters

The following request parameter list only provides API request parameters. Common request parameters need to be added when the API is called. For more information, refer to [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/372/4153). The Action field for this API is EipBindNatGateway.

| Parameter Name   | Required | Type   | Description                                                  |
| :--------------- | :------- | :----- | :----------------------------------------------------------- |
| natId            | Yes      | string | Unified ID of highly available gateway, for example: nat-df5dfd |
| vpcId            | Yes      | string | Virtual private cloud ID or unified ID (unified ID is recommended), for example: vpc-dfd5dfgd |
| assignedEipSet.n | No       | array  | Elastic IP. One of the two input parameters assignedEipSet and autoAllocEipNum must be passed at least, for example: assignedEipSet.0=183.23.0.0.1 |
| autoAllocEipNum  | No       | int    | The number of elastic IPs for new requests, value range [0, 3]. One of the two input parameters assignedEipSet and autoAllocEipNum must be passed at least |

## 3. Output Parameters

| Parameter Name | Type   | Description                                                  |
| :------------- | :----- | :----------------------------------------------------------- |
| code           | Int    | Error code. 0: Succeeded, other values: Failed               |
| message        | String | Error message                                                |
| taskId         | Int    | Task ID. The operation result can be queried with taskId. For more information, refer to [API for Querying Task Execution Result](https://cloud.tencent.com/doc/api/245/查询任务执行结果接口). |

## 4. Error Code List

The following error code list only provides the business logic error codes for this API. For additional common error codes, refer to [VPC Error Codes](https://cloud.tencent.com/doc/api/245/4924).

| Error Code                   | Description                                                  |
| :--------------------------- | :----------------------------------------------------------- |
| InvalidVpc.NotFound          | Invalid VPC. VPC resource does not exist. Please verify that the resource information you entered is correct. You can query the VPC via the [DescribeVpcEx](http://cloud.tencent.com/doc/api/245/查询私有网络列表) API |
| InvalidNatGatewayId.NotFound | Invalid NAT gateway, NAT gateway resource does not exist. Please verify that the resource information you entered is correct. You can query the NAT gateway via the [DescribeNatGateway](https://cloud.tencent.com/doc/api/245/查询NAT网关?viewType=preview) API |

## 5. Example

Input



```
https://vpc.api.qcloud.com/v2/index.php?Action=EipBindNatGateway&<Common request parameters>&natId=nat-8pbrkzh6&vpcId=314&autoAllocEipNum=1
```


Output

```
{
    "code":"0",
    "message":"",
    "taskId":16167
}
```