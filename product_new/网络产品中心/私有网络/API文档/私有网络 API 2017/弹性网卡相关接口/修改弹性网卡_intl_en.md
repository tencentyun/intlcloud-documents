## 1. API Description

This API (ModifyNetworkInterface) is used to modify ENIs.
Domain name for API requests: <font style="color:red">vpc.api.qcloud.com</font>


## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see the <a href=" https://intl.cloud.tencent.com/doc/api/245/4772" title="Common Request Parameters">Common Request Parameters</a> page. The Action field for this API is ModifyNetworkInterface.

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| vpcId | Yes | String | VPC ID of the ENI, for example: vpc-7t9nf3pu. |
| networkInterfaceId | Yes | String | ENI ID assigned by the system, for example: eni-m6dyj72l. |
| eniName | Yes | String | ENI name, which cannot exceed 60 characters. |
| eniDescription | No | String | ENI description, which cannot exceed 60 characters. |


## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| code | Int | Error code. 0: Successful; other values: Failed. |
| message | String | Error message |

## 4. Error Codes
The following error codes only include business logic error codes for this API. For additional common error codes, see <a href="https://intl.cloud.tencent.com/doc/api/245/4924" title="VPC Error Codes">VPC Error Codes</a>.

| Error code | Description |
|---------|---------|
| InvalidVpc.NotFound | Invalid VPC. This error code indicates that the VPC resource does not exist. In this case, check whether the resource information that you entered is correct. You can query the VPC through the API <a href="http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8" title="DescribeVpcEx">DescribeVpcEx</a>. |
| InvalidNetworkInterface.NotFound | Invalid ENI. This error code indicates that the ENI does not exist. In this case, verify whether the resource information that you entered is correct. You can query the ENI through the API <a href="https://intl.cloud.tencent.com/doc/api/245/%e6%9f%a5%e8%af%a2%e5%bc%b9%e6%80%a7%e7%bd%91%e5%8d%a1%e4%bf%a1%e6%81%af?viewType=preview" title="DescribeNetworkInterfaces">DescribeNetworkInterfaces</a>. |

## 5. Sample
Input
<pre>
https://vpc.api.qcloud.com/v2/index.php?Action=ModifyNetworkInterface
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common Request Parameters</a>>
&vpcId=vpc-7t9nf3pu
&networkInterfaceId=eni-m6dyj72l
&eniName=barrytest
</pre>
Output
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success"
}
```

