## 1. API Description

This API (DescribeNetworkInterfaces) is used to query the information of ENIs.
Domain name for API requests: `vpc.api.qcloud.com`

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href=" https://intl.cloud.tencent.com/doc/api/372/4153" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is DescribeNetworkInterfaces.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | No | String | VPC ID of an ENI, for example: vpc-7t9nf3pu. |
| networkInterfaceId | No | String | ENI ID assigned by the system, for example: eni-m6dyj72l. |
| eniName | No | String | ENI name, which supports fuzzy search. |
| eniDescription | No | String | ENI description, which supports fuzzy search. |
| instanceId | No | String | CVM instance ID, for example: ins-xx44545f. |
| offset | No | Int | Offset of the initial line. The default is 0. |
| limit | No | Int | Number of lines per page. The default is 20 and the maximum is 50. |
| orderField | No | String | Sorts by a field.<br>Supported fields: eniName and createTime. The default is createTime. |
| orderDirection | No | String | Ascending order (asc) or descending order (desc). The default is desc. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message. |
| data.totalNum | Int | Total number of ENIs. |
| data.data | Array | ENI information array. |

**data is composed as follows:**

| Parameter name | Type | Description |
|---------|---------|---------|
| data.n.vpcId | String | VPC ID of the ENI, for example: vpc-8e0ypm3z. |
| data.n.subnetId | String | Subnet ID of the ENI, for example: subnet-0ap8nwca. |
| data.n.zoneId | Int | Availability zone ID of the subnet of the ENI, For example: 200001. |
| data.n.eniName | String | ENI name. |
| data.n.eniDescription| String | ENI description. |
| data.n.networkInterfaceId | String | ENI ID, For example: eni-m6dyj72l. |
| data.n.primary | Bool | Indicates whether it is a primary ENI. true: Primary ENI; false: Generic ENI. |
| data.n.macAddress | String | MAC address of the ENI, for example: 02:81:60:cb:27:37. |
| data.n.privateIpAddressesSet | Array | IP address bound with the ENI. |
| data.n.instanceSet | Object | CVM bound with the ENI. |
| data.n.groupSet | Array | Security group bound with the ENI. |

**privateIpAddressesSet information array:**

| Parameter name | Type | Description |
|---------|---------|---------|
| privateIpAddress | String | IP address. |
| Primary | Bool | Indicates whether it is a primary IP. true: Yes; false: No. |
| description | String | Comments. |
| wanIp | String | Public IP address. |
| isWanIpBlocked | Bool | Indicates whether the public IP address is blocked. |
| eipId | String | EIP ID. |

**instanceSet information:**

| Parameter name | Type | Description |
|---------|---------|---------|
| instanceId | String | CVM instance ID, for example: ins-xx44545f. |
| attachTime | String | Binding time, for example: 2016-02-15 19:20:54. |

**groupSet information array:**

| Parameter name | Type | Description |
|---------|---------|---------|
| sgId | String | Security group ID, for example: sg-dfg1df54. |
| sgName | String | Security group name. |
| projectId | Int | Security group project ID. |

## 4. Error Codes
The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC resource does not exist. In this case, verify whether the resource information that you entered is correct. You can query the VPC through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| InvalidNetworkInterface.NotFound | Invalid ENI. This error code indicates that the ENI does not exist. In this case, verify whether the resource information that you entered is correct. You can query the ENI through the API <a href="https://intl.cloud.tencent.com/doc/api/245/%e6%9f%a5%e8%af%a2%e5%bc%b9%e6%80%a7%e7%bd%91%e5%8d%a1%e4%bf%a1%e6%81%af?viewType=preview" title="DescribeNetworkInterfaces">DescribeNetworkInterfaces</a>. |

## 5. Sample
Input
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=DescribeNetworkInterfaces
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&vpcId=vpc-fyc4pilj
</pre>
Output
```
{
	"code": 0,
	"message": "",
	"codeDesc": "Success",
	"data": {
		"totalNum": 3,
		"data": [{
				"vpcId": "vpc-fyc4pilk",
				"vpcName": "test",
				"subnetId": "subnet-pq7ptksb",
				"zoneId": 100002,
				"eniName": "large",
				"eniDescription": "",
				"networkInterfaceId": "eni-d6m4m0iy",
				"primary": false,
				"macAddress": "20:90:6F:59:8D:79",
				"createTime": "2017-08-31 11:33:59",
				"flowLogsSet": [],
				"privateIpAddressesSet": [{
					"privateIpAddress": "10.53.54.19",
					"primary": true,
					"wanIp": "119.29.158.39",
					"description": "asdfasdfasdf",
					"isWanIpBlocked": false,
					"eipId": "eip-07vqn979"
				}],
				"instanceSet": {
					"instanceId": "ins-7s7zjjcz",
					"attachTime": "2017-12-12 11:55:07"
				},
				"groupSet": [{
						"sgId": "sg-lb62wxwb",
						"sgName": "asdfsadf",
						"projectId": 1079263
					},
					{
						"sgId": "sg-ikmc8kcy",
						"sgName": "full drop",
						"projectId": 0
					}
				]
			},
			{
				"vpcId": "vpc-fyc4pilk",
				"vpcName": "test",
				"subnetId": "subnet-pq7ptksb",
				"zoneId": 100002,
				"eniName": "manual",
				"eniDescription": "",
				"networkInterfaceId": "eni-ay1ac9c7",
				"primary": false,
				"macAddress": "20:90:6F:94:86:77",
				"createTime": "2017-07-28 20:09:34",
				"flowLogsSet": [],
				"privateIpAddressesSet": [{
						"privateIpAddress": "10.53.54.230",
						"primary": true,
						"wanIp": "",
						"description": "",
						"isWanIpBlocked": false,
						"eipId": ""
					},
					{
						"privateIpAddress": "10.53.54.231",
						"primary": false,
						"wanIp": "",
						"description": "",
						"isWanIpBlocked": false,
						"eipId": ""
					}
				],
				"instanceSet": {
					"instanceId": "",
					"attachTime": ""
				},
				"groupSet": [{
						"sgId": "sg-lb62wxw9",
						"sgName": "asdfsadf",
						"projectId": 1079263
					},
					{
						"sgId": "sg-37tmkdiz",
						"sgName": "Open port 3389 to Internet on Windows-20170928143645736",
						"projectId": 0
					}
				]
			},
			{
				"vpcId": "vpc-fyc4pilk",
				"vpcName": "test",
				"subnetId": "subnet-pq7ptksb",
				"zoneId": 100002,
				"eniName": "Create an ENI manually",
				"eniDescription": "",
				"networkInterfaceId": "eni-a7hx9qae",
				"primary": false,
				"macAddress": "20:90:6F:31:88:B4",
				"createTime": "2017-07-28 17:39:39",
				"flowLogsSet": [],
				"privateIpAddressesSet": [{
					"privateIpAddress": "10.53.54.200",
					"primary": true,
					"wanIp": "",
					"description": "",
					"isWanIpBlocked": false,
					"eipId": ""
				}],
				"instanceSet": {
					"instanceId": "",
					"attachTime": ""
				},
				"groupSet": [{
						"sgId": "sg-lb62wxwe",
						"sgName": "asdfsadf",
						"projectId": 1079263
					},
					{
						"sgId": "sg-5y2tai6e",
						"sgName": "createPolicy_repair_test",
						"projectId": 0
					},
					{
						"sgId": "sg-q7bvssoa",
						"sgName": "del usg test",
						"projectId": 0
					},
					{
						"sgId": "sg-0cgr10ie",
						"sgName": "bilibili no icmp",
						"projectId": 0
					},
					{
						"sgId": "sg-ei2rr0qf",
						"sgName": "Guangzhou",
						"projectId": 0
					},
					{
						"sgId": "sg-oodf2fc6",
						"sgName": "offset",
						"projectId": 0
					}
				]
			}
		]
	}
}
```

