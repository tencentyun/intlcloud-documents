## 1. API Description

Domain name for API request: vpc.tencentcloudapi.com.

This API (CreateSecurityGroupPolicies) is used to create security group policies (SecurityGroupPolicy).

* The Version field indicates the version number of a security group policy, which is automatically increased by one each time you update the security policy, to prevent expiration of updated routing policies. If it is left empty, conflict is ignored.
* The Protocol field allows you to enter TCP, UDP, ICMP, GRE, and ALL.
* The CidrBlock field allows you to enter any string that conforms to the cidr format. (More details) In a basic network, if CidrBlock contains private IPs on Tencent Cloud for devices within your account other than CVMs, it does not mean this policy allows you to access these devices. The network isolation policies between tenants take priority over the private network policies in security groups.
* The SecurityGroupId field allows you to enter the IDs of security groups that are in the same project as the security group to modify, including the ID of the security group itself, to represent private IPs of all CVMs under the security group. When this field is used, this policy will change as the CVM associated with the ID entered here changes while it's being used to match network messages, and does not need to be modified.
* The Port field allows you to enter a single port number, or two port numbers separated by a minus sign, e.g., 80 or 8000-8010. The Port field is accepted only if the Protocol field is TCP or UDP.
* The Action field only allows you to enter ACCEPT or DROP.
* CidrBlock, SecurityGroupId and AddressTemplate are exclusive to each other, and cannot be entered at the same time. Protocol + Port and ServiceTemplate are mutually exclusive, and cannot be entered at the same time.
* Only policies in one direction can be created in one request. If the PolicyIndex parameter is specified, the indexes of multiple policies must be consistent.

A maximum of 100 requests can be initiated per second for this API.

Note: This API supports Finance regions. Since Finance regions and non-Finance regions are isolated and not interconnected. If the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region that should be identical to the value of Region field, for example: vpc.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/215/15692).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CreateSecurityGroupPolicies |
| Version | Yes |  String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes |  String | Common parameter. For more information, please see the [list of regions](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/215/15692#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| SecurityGroupId | Yes | String | Security group instance ID, such as sg-33ocnj9n. It can be obtained through DescribeSecurityGroups. |
| SecurityGroupPolicySet | Yes | [SecurityGroupPolicySet](https://cloud.tencent.com/document/api/215/##SecurityGroupPolicySet) | Security group policy set. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique request ID, which is returned for each request. RequestId is required for locating a problem. |

## 4. Error Codes

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/215/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameter | Invalid input parameter. |
| InvalidParameterValue | Invalid parameter value. |
| InvalidParameterValue.Malformed | Invalid input parameter format. |
| LimitExceeded | Quota exceeded. |
| ResourceNotFound | Resource does not exist. |
| UnsupportedOperation.VersionMismatch | The specified version number of the security group policy is inconsistent with the latest version. |

## 5. Example

### Example 1 Add egress policies to a security group

#### Input example

```
https://vpc.tencentcloudapi.com/?Action=CreateSecurityGroupPolicies
&Version=2017-03-12
&SecurityGroupId=sg-ohuuioma
&SecurityGroupPolicySet.Version=21
&SecurityGroupPolicySet.Ingress.0.PolicyIndex=1
&SecurityGroupPolicySet.Ingress.0.ServiceTemplate.ServiceId=ppm-f5n1f8da
&SecurityGroupPolicySet.Ingress.0.AddressTemplate.AddressId=ipmg-2uw6ujo6
&SecurityGroupPolicySet.Ingress.0.Action=accept
&SecurityGroupPolicySet.Ingress.0.PolicyDescription=TestPolicy
&SecurityGroupPolicySet.Ingress.1.PolicyIndex=1
&SecurityGroupPolicySet.Ingress.1.ServiceTemplate.ServiceId=ppm-f5n1f8da
&SecurityGroupPolicySet.Ingress.1.AddressTemplate.AddressId=ipmg-2uw6ujo6
&SecurityGroupPolicySet.Ingress.1.Action=accept
&SecurityGroupPolicySet.Ingress.1.PolicyDescription=Test
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "RequestID": "354f4ac3-8546-4516-8c8a-69e3ab73aa8a"
  }
}
```

### Example 2 Add ingress policies to a security group

#### Input example

```
https://vpc.tencentcloudapi.com/?Action=CreateSecurityGroupPolicies
&Version=2017-03-12
&SecurityGroupId=sg-ohuuioma
&SecurityGroupPolicySet.Version=21
&SecurityGroupPolicySet.Ingress.0.PolicyIndex=1
&SecurityGroupPolicySet.Ingress.0.ServiceTemplate.ServiceId=ppm-f5n1f8da
&SecurityGroupPolicySet.Ingress.0.AddressTemplate.AddressId=ipmg-2uw6ujo6
&SecurityGroupPolicySet.Ingress.0.Action=accept
&SecurityGroupPolicySet.Ingress.0.PolicyDescription=TestPolicy
&SecurityGroupPolicySet.Ingress.1.PolicyIndex=1
&SecurityGroupPolicySet.Ingress.1.ServiceTemplate.ServiceId=ppm-f5n1f8da
&SecurityGroupPolicySet.Ingress.1.AddressTemplate.AddressId=ipmg-2uw6ujo6
&SecurityGroupPolicySet.Ingress.1.Action=accept
&SecurityGroupPolicySet.Ingress.1.PolicyDescription=Test
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "RequestID": "354f4ac3-8546-4516-8c8a-69e3ab73aa8a"
  }
}
```


## 6. Other Resources

Cloud API 3.0 comes with the following development tools to make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)
* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

