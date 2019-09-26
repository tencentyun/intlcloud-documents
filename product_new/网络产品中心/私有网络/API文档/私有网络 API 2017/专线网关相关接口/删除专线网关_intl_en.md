## 1. API Description

This API (DeleteDirectConnectGateway) is used to delete Direct Connect gateway.
Domain for API request:vpc.api.qcloud.com

1) For a NAT gateway, NAT and ACL rules will be cleaned upon the deletion of Direct Connect gateway.
2) When the Direct Connect gateway is deleted, the routing policy associated with the gateway in the routing table will also be deleted.

## 2. Input Parameters

The following request parameter list only provides API request parameters. Common request parameters need to be added when the API is called. For more information, refer to [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/372/4153). The Action field for this API is DeleteDirectConnectGateway.

| Parameter Name         | Required | Type   | Description                                                  |
| :--------------------- | :------- | :----- | :----------------------------------------------------------- |
| vpcId                  | Yes      | String | VPC ID assigned by the system, e.g. vpc-7t9nf3pu.            |
| directConnectGatewayId | Yes      | String | Direct Connect gateway ID assigned by the system, e.g. dcg-7t9nf3pu. |

## 3. Output Parameters

| Parameter Name | Type   | Description                                                  |
| :------------- | :----- | :----------------------------------------------------------- |
| code           | Int    | Error code, 0: Succeeded, other values: Failed.              |
| message        | String | Error message.                                               |
| taskId         | Int    | Task ID. The operation result can be queried with taskId. For more information, refer to [API for Querying Task Execution Result](https://intl.cloud.tencent.com/document/api/215/5094). |

## 4. Error Code List

The following error code list only provides the business logic error codes for this API. For additional common error codes, refer to [VPC Error Codes](https://intl.cloud.tencent.com/doc/api/245/4924).

| Error Code                           | Description                                                  |
| :----------------------------------- | :----------------------------------------------------------- |
| InvalidVpc.NotFound                  | Invalid VPC. VPC resource does not exist. Please verify that you have entered resource information correctly. |
| InvalidDirectConnectGateway.NotFound | Invalid Direct Connect gateway. Direct Connect gateway resource does not exist. Please verify that you have entered resource information correctly. |

## 5. Example

Input



```
https://vpc.api.qcloud.com/v2/index.php?Action=DeleteDirectConnectGateway&<Common request parameters>&vpcId=vpc-dfgg190&directConnectGatewayId=dcg-ddf14d
```


Output

```
{
    "code":"0",
    "message":"",
    "taskId":16284
}
```


  