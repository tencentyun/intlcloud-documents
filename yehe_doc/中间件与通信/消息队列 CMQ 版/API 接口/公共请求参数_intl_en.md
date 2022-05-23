
The common parameters are used to authenticate the user and API. If not necessary, these parameters are not described in individual API documents. However, they must be carried by each request in order for the request to be properly initiated.
> ? **The APIs listed on this page are on legacy versions and may be disused in the future. Currently, they are not displayed on the left sidebar. [CVM APIs v3.0](https://intl.cloud.tencent.com/document/api/213/15689) have more standardized definitions and much lower access latency and thus are recommended.**


| **Name**  | **Type** | **Description**                                                     | **Required** |
| :-------- | :------- | :----------------------------------------------------------- | :------- |
| Action    | String   | API name, such as `DescribeInstances`                       | Yes       |
| Region    | String   | Region parameter, which is used to indicate the region of the target instance. Valid values: bj: Beijing; gz: Guangzhou; sh: Shanghai; hk: Hong Kong (China); ca: North America; sg: Singapore; usw: West US; cd: Chengdu; de: Germany; kr: South Korea; gzopen: Guangzhou OPEN | Yes       |
| Timestamp | UInt     | Current Unix timestamp                                             | Yes       |
| Nonce | UInt | A random positive integer used in conjunction with `Timestamp` to prevent replay attacks | Yes       |
| SecretId  | String   | The identifying `SecretId` and `SecretKey` obtained on the Tencent Cloud platform. The latter is used to generate the signature. For more information, see [Signature](https://intl.cloud.tencent.com/document/product/213/31575) | Yes       |
| Signature | String   | Request signature, which is used to verify the validity of the request. For more information, see [Signature](https://intl.cloud.tencent.com/document/product/213/31575) | Yes       |

A typical API request is as follows, where `Action=DescribeInstance` indicates to query the details of a CVM instance.

```
https://cvm.api.qcloud.com/v2/index.php?Action=DescribeInstances
&SecretId=xxxxxxx
&Region=gz
&Timestamp=1402992826
&Nonce=345122
&Signature=mysignature
&instanceId=101
```

`instanceId` is an instruction parameter, and others are common parameters.

