### Concatenation rule
A TencentCloud API request URL is concatenated as follows:
> **https:// + request domain name + request path + ? + final request parameter string**

The elements of each URL are described as follows:
- **Request domain name:** subject to the product or product module to which the API belongs. For example, the request domain name for the DescribeInstances API used to query the CVM instance list is `cvm.api.qcloud.com`. For the request domain name of a specific product, see the description of each API.
- **Request path:** a fixed path for requesting TencentCloud APIs. For example, the request path for Tencent Cloud CVM is always `/v2/index.php`.
- **Final request parameter string:** consisting of common request parameters and API request parameters.

### Example
The final request URL for a TencentCloud API is as follows:
Taking Tencent Cloud CVM's [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258) API as an example, the first six parameters are common request parameters, while the last six ones are API request parameters.

```
https://cvm.api.qcloud.com/v2/index.php?
Action=DescribeInstances
&SecretId=xxxxxxx
&Region=gz
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature       // Common request parameters
&instanceIds.0=ins-0hm4gvho
&instanceIds.1=ins-8oby8q00
&offset=0
&limit=20
&status=2
&zoneId=100003      // API request parameters
```
