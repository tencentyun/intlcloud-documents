## 1. API Description

This API (AcceptVpcPeeringConnectionEx) is used to accept cross-region peering connection request from another account. Once the request is accepted, the peering connection takes effect immediately.
Domain for API request: vpc.api.qcloud.com

## 2. Input Parameters

The following request parameter list only provides API request parameters. Common request parameters need to be added when the API is called. For more information, refer to [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/372/4153). The Action field for this API is AcceptVpcPeeringConnectionEx.

| Parameter Name      | Required | Type   | Description                                      |
| :------------------ | :------- | :----- | :----------------------------------------------- |
| peeringConnectionId | Yes      | String | ID of VPC peering connection, e.g. pcx-6gw5wvmk. |

## 3. Output Parameters

| Parameter Name | Type   | Description                                                  |
| :------------- | :----- | :----------------------------------------------------------- |
| code           | Int    | Error code. 0: Succeeded; other values: Failed.              |
| message        | string | Error message.                                               |
| taskId         | int    | Task ID. The operation result can be queried with taskId. For more information, refer to [API for Querying Task Execution Result](https://intl.cloud.tencent.com/document/api/215/5094). |

## 4. Error Codes

The following error code list only provides the business logic error codes for this API. For additional common error codes, refer to [VPC Error Codes](https://intl.cloud.tencent.com/doc/api/245/4924).

| Error Code                        | Description                                                  |
| :-------------------------------- | :----------------------------------------------------------- |
| InvalidVpc.NotFound               | VPC does not exist. Please check the information you entered. |
| InvalidPeeringConnection.NotFound | Peering connection does not exist. Please check the information you entered. |

## 5. Example

Input



```
https://vpc.api.qcloud.com/v2/index.php?Action=AcceptVpcPeeringConnection&<Common request parameters>&peeringConnectionId=pcx-6gw5wvmk
```


Output

```
{
    "code":"0",
    "message":"",
    "taskId":1254
}
```


  