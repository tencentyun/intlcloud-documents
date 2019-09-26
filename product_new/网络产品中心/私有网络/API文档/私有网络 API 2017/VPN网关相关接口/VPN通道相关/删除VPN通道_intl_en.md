## 1. API Description

This API (DeleteVpnConn) is used to delete VPN tunnel.
Domain for API request: vpc.api.qcloud.com

## 2. Input Parameters

The following request parameter list only provides API request parameters. Common request parameters need to be added when the API is called. For more information, refer to [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/372/4153). The Action field for this API is DeleteVpnConn.

| Parameter Name | Required | Type   | Description                                                  |
| :------------- | :------- | :----- | :----------------------------------------------------------- |
| vpcId          | Yes      | string | Virtual private cloud ID, which can be vpcId or unVpcId. unVpcId is recommended. For example: vpc-03vihbk9. Can be queried via the API [DescribeVpcEx](http://intl.cloud.tencent.com/doc/api/245/查询私有网络列表). |
| vpnGwId        | Yes      | String | VPN gateway ID assigned by the system, which can be vpnGwId or unVpnGwId. unVpnGwId is recommended. For example: vpngw-dystbrkv. Can be queried via the API [DescribeVpnGw](http://intl.cloud.tencent.com/doc/api/245/查询VPN网关列表). |
| vpnConnId      | Yes      | String | VPN channel ID assigned by the system, which can be vpnConnId or unVpnConnId. unVpnConnId is recommended. For example: vpnx-ol6bcqp0. Can be queried via the API [DescribeVpnConn](http://intl.cloud.tencent.com/document/product/215/5113). |

## 3. Output Parameters

| Parameter Name | Type   | Description                                                  |
| :------------- | :----- | :----------------------------------------------------------- |
| code           | Int    | Error code, 0: Succeeded; other values: Failed               |
| message        | String | Error message                                                |
| data.taskId    | Int    | Task ID. The operation result can be queried with taskId. For more information, refer to [API for Querying Task Execution Result](https://intl.cloud.tencent.com/doc/api/245/查询任务执行结果接口). |

## 4. Error Codes

The following error code list only provides the business logic error codes for this API. For additional common error codes, refer to [VPC Error Codes](https://intl.cloud.tencent.com/doc/api/245/4924).

| Error code              | Description                                                  |
| :---------------------- | :----------------------------------------------------------- |
| InvalidVpc.NotFound     | VPC does not exist. Please check the information you entered. You can query the VPC via the API [DescribeVpcEx](http://intl.cloud.tencent.com/doc/api/245/查询私有网络列表). |
| InvalidVpnGw.NotFound   | VPN gateway does not exist. Please check the information you entered. You can query the VPN gateway via the API [DescribeVpnGw](https://intl.cloud.tencent.com/doc/api/245/查询VPN网关列表?viewType=preview). |
| InvalidVpnConnState     | Invalid VPN tunnel status                                    |
| InvalidVpnConn.NotFound | Invalid VPN tunnel. VPN tunnel does not exist. Please check the information you entered. You can query the VPN channel via the API [DescribeVpnConn](http://intl.cloud.tencent.com/document/product/215/5113). |

## 5. Example

Input

```
  https://vpc.api.qcloud.com/v2/index.php?Action=DeleteVpnConn
  &<Common request parameters>
  &vpcId=vpc-03vihbk9
  &vpnGwId=vpngw-kfldykuz
  &vpnConnId=vpnx-ol6bcqp0
```

Output

```
{
    "code": 0,
    "message": "",
    "data": {
        "vpnGwId": "vpngw-kfldykuz",
        "vpcConnId": "vpnx-ol6bcqp0",
        "taskId": 12615,
        "state": 4
    }
}
```