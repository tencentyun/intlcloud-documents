### Concatenation Rule
A TencentCloud API request URL is concatenated as follows:
> **https:// + request domain name + request path + ? + final request parameter string**

The elements of each URL are described as follows:
- **Request host:** Request domain name is determined by the product or product module to which the API belongs. For example, the request domain name for the Tencent Cloud CVM API for querying instance list (DescribeInstances) is: `cvm.api.qcloud.com`. For the request domain names of specific products, see the description of each API.
- **Request path:** The request path for the product to which the TencentCloud API belongs. Each product has a fixed path. For example, the request path for Tencent Cloud CVM is always `/v2/index.php`.
- **Final request parameter string:** The API request parameter string consists of common request parameters and API request parameters.

### Use Cases
The final request URL for a TencentCloud API is as follows:
Taking Tencent Cloud CVM's [Querying Instance List API](https://intl.cloud.tencent.com/doc/api/229/831) (DescribeInstances) as an example, the first six parameters are common request parameters, while the last six ones are API request parameters.

```
https://cvm.api.qcloud.com/v2/index.php?
Action=DescribeInstances
&SecretId=xxxxxxx
&Region=gz
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature       // Common request parameter
&instanceIds.0=ins-0hm4gvho
&instanceIds.1=ins-8oby8q00
&offset=0
&limit=20
&status=2
&zoneId=100003      // API request parameter
```
