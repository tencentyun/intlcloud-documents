## 1. API Description

This API (EnableVpcPeeringConnectionEx) is used to activate cross-region peering connection.
Domain for API request: vpc.api.qcloud.com

If the receiver does not accept the request for a cross-account peering connection within 7 days after the request is initiated, the peering connection will expire. Upon the expiration, the receiver will not be able to perform any action on the peering connection. The initiator can use this API to enable the peering connection and notify the receiver to process the connection.

## 2. Input Parameters

The following request parameter list only provides API request parameters. Common request parameters need to be added when the API is called. For more information, refer to [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/372/4153). The Action field for this API is EnableVpcPeeringConnectionEx.

| Parameter Name      | Required | Type   | Description                                      |
| :------------------ | :------- | :----- | :----------------------------------------------- |
| peeringConnectionId | Yes      | String | ID of VPC peering connection, e.g. pcx-6gw5wvmk. |

## 3. Output Parameters

| Parameter Name | Type   | Description                                                  |
| :------------- | :----- | :----------------------------------------------------------- |
| code           | int    | Error code. 0: Succeeded; other values: Failed.              |
| message        | string | Error message.                                               |
| taskId         | int    | Task ID. The operation result can be queried with taskId. For more information, refer to [API for Querying Task Execution Result](https://intl.cloud.tencent.com/document/api/215/5094). |

## 4. Error Code List

The following error code list only provides the business logic error codes for this API. For additional common error codes, refer to [VPC Error Codes](https://intl.cloud.tencent.com/doc/api/245/4924).

| Error Code                        | Description                                                  |
| :-------------------------------- | :----------------------------------------------------------- |
| InvalidVpc.NotFound               | VPC not exist. Please check the information you entered.     |
| InvalidPeeringConnection.NotFound | Peering connection not exist. Please check the information you entered. |

## 5. Example

Input



```
https://vpc.api.qcloud.com/v2/index.php?Action=EnableVpcPeeringConnectionEx&<Common request parameters>&peeringConnectionId=pcx-6gw5wvmk
```


Output

```
{
    "code":"0",
    "message":"",
    "taskId":1584
}
```