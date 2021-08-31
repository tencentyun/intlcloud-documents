# API Description
 This API is used to obtain the list of CLB instances and output satisfactory CLB instances based on the specified parameters.

Domain name for API calls: `lb.api.qcloud.com`


## Request Parameters
 The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `DescribeLoadBalancers`.

| Parameter | Required | Type | Description |
|---|---|---|---|
|loadBalancerIds.n | No | String | CLB instance ID. |
| loadBalancerType | No | Int | Network type of the CLB instance.<br>2: public network; 3: private network. |
|forward | No | Int | CLB instance type. 1: CLB; 0: classic CLB, -1: all. |
| loadBalancerName | No | String | CLB instance name. |
| domain | No | String | Domain name assigned to a public network classic CLB instance by Tencent Cloud. This field is inapplicable to other types of CLB instances. |
| loadBalancerVips.n | No | String | VIP address of the CLB instance. You can enter several VIP addresses. |
| backendWanIps.n | No | String | Public IP of the real server bound to a CLB instance. |
| backendLanIps.n | No | String | Private IP of the real server bound to a CLB instance. |
| offset | No | Int | Data offset. Default value: 0. |
| limit | No | Int | Number of returned CLB instances. Default value: 20. |
| orderBy | No | String | Sort by field. Valid values: loadBalancerName, createTime, domain, loadBalancerType. |
| orderTyp | No | Int | 1: reverse; 0: sequential. The `createTime` in reverse chronological order will be used by default.|
| searchKey | No | String | Search field which fuzzy matches name, domain name, or VIP. |
|projectId | No | Int | ID of the project to which a CLB instance belongs, which can be obtained via the <a href="https://intl.cloud.tencent.com/document/product/214/1261">DescribeProject</a> API.|
| withRs | No | Int | Whether the CLB instance you want to query is bound to a real server. 0: no; 1: yes; 2: query all. |

## Response Parameters

| Parameter | Type | Description |
|----|---|----|
| code | Int | Common error code. 0: success; other values: failure. For more information, see <a href="https://intl.cloud.tencent.com/document/product/214/11602" title="Common Error Codes">Common Error Codes</a>. |
| message | String | API-related module error message description. |
| codeDesc | String | Error code. For a successful operation, "Success" is returned. For a failed operation, a message describing the failure is returned. |
| totalCount | Int | Total number of CLB instances that meet the filter criteria. |
| loadBalancerSet | Array | Array of returned CLB instances. |

- `loadBalancerSet` structure

| Parameter | Type | Description |
|----|---|----|
| loadBalancerId | String | CLB instance ID. |
| unLoadBalancerId | String | CLB instance ID. |
| loadBalancerName | String | CLB instance name. |
| loadBalancerType | Int | Network type of the CLB instance.<br>2: public network; 3: private network. |
|forward | Int | CLB type identifier. 1: CLB; 0: classic CLB. |
| domain | String | Domain name assigned to a public network classic CLB instance by Tencent Cloud. This field is inapplicable to other types of CLB instances.|
| loadBalancerVips | Array | VIP list of the CLB instance. |
| status | Int | Status of the CLB instance.<br>0: creating; 1: running. |
| createTime | String | Creation time of the CLB instance. |
| statusTime | String | Last time when the status of the CLB instance changes. |
| projectId | Int | ID of the project to which the CLB instance belongs. 0: default project. |
| vpcId | Int | Numerical digits of the VPC ID. 0: classic network. |
| subnetId | Int | Numerical digits of the VPC subnet ID. 0: default subnet. |
| openBgp | Int | Identifier of a high defense LB. 1: high defense CLB; 0: non-high defense CLB. |
| snat | Bool | "snat" is enabled for all private network classic CLB instances created before December 2016. |
| isolation | Int | Isolation status of the CLB instance due to overdue account. 0: not isolated; 1: isolated. |
| log | String | Log information. Only the public network CLB instances that have HTTP or HTTPS listener can generate logs. |


## Example

Querying the CLB instance list using default parameters
```
https://lb.api.qcloud.com/v2/index.php?Action=DescribeLoadBalancers
&<Common request parameters>
&forward=-1
```

Response
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "loadBalancerSet": [
        {
            "loadBalancerId": "lb-hc1vni0f",
            "unLoadBalancerId": "lb-hc1vni0f",
            "loadBalancerName": "cls-qbesvs66_ng1",
            "loadBalancerType": 2,
            "domain": "cls-qbesvs66-ng1.gz.1251707795.clb.myqcloud.com",
            "loadBalancerVips": [
                "111.230.83.36"
            ],
            "status": 1,
            "createTime": "2017-11-30 14:28:45",
            "statusTime": "2017-11-30 14:29:11",
            "vpcId": 2968,
            "uniqVpcId": "vpc-b2h3xykt",
            "subnetId": 1,
            "projectId": 0,
            "forward": 0,
            "snat": false,
            "openBgp": 0,
            "isolation": 0,
            "log": ""
        }
    ],
    "totalCount": 1
}
```
