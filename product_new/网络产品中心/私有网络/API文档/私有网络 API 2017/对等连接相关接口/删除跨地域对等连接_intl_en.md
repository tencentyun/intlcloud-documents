## 1. API Description

This API (DeleteVpcPeeringConnectionEx) is used to delete cross-region peering connection.
Domain for API request: vpc.api.qcloud.com

1) Either of the sides can delete the peering connection at any time. The peering connection becomes invalid immediately after being deleted.
2) When the peering connection is deleted, the routing entry containing this connection in the routing table will also be deleted.

## 2. Input Parameters

The following request parameter list only provides API request parameters. Common request parameters need to be added when the API is called. For more information, refer to [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/372/4153). The Action field for this API is DeleteVpcPeeringConnectionEx.

| Parameter Name      | Required | Type   | Description                                      |
| :------------------ | :------- | :----- | :----------------------------------------------- |
| peeringConnectionId | Yes      | String | ID of VPC peering connection, e.g. pcx-0jtgah4s. |

## 3. Output Parameters

| Parameter Name | Type   | Description                                                  |
| :------------- | :----- | :----------------------------------------------------------- |
| code           | Int    | Error code. 0: Succeeded; other values: Failed.              |
| message        | string | Error message.                                               |
| taskId         | int    | Task ID. The operation result can be queried with taskId. For more information, refer to [API for Querying Task Execution Result](https://intl.cloud.tencent.com/document/api/215/5094). |

## 4. Error Codes

The following error code list only provides the business logic error codes for this API. For additional common error codes, refer to [VPC Error Codes](https://intl.cloud.tencent.com/doc/api/245/4924).

| Error code                        | Description                                                  |
| :-------------------------------- | :----------------------------------------------------------- |
| InvalidVpc.NotFound               | VPC not exist. Please check the information you entered.     |
| InvalidPeeringConnection.NotFound | Peering connection not exist. Please check the information you entered. |

## 5. Example

Input



```
https://vpc.api.qcloud.com/v2/index.php?Action=DeleteVpcPeeringConnection&<Common request parameters>&peeringConnectionId=pcx-0jtgah4s
```


Output

```
{
    "code":"0",
    "message":"",
    "taskId":121221
}
```


  