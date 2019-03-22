[//]: # (chinagitpath:XXXXX)

### Concatenation Rule
The structure of an Tencent Cloud API request URL
> **https:// + domain name + Request path + ? + lists of request parameters**

Descrption:
-  **Domain name:** The domain name for an API request is subject to product or product module. For example, when you sent an API request to query a list of Tencent Cloud CVM instances (Action: DescribeInstances), the domain name is: `cvm.api.qcloud.com`. For more information about domain names, see relevant API documents.
-  **Request path:** The path for an API request is subject to product. Each product has a fixed path. For example, the request path for Tencent Cloud CVM is `/v2/index.php`.
- **lists of request parameters:** Common request parameters and API request parameters

### Use Case
This example shows the URL of a Tencent Cloud API request: you sent an API request to query a list of Tencent Cloud CVM instances (Action: DescribeInstances). Domain name is: `cvm.api.qcloud.com`. First 6 parameters are common request parameters, and the last 6 ones are API request parameters.

```
https://cvm.api.qcloud.com/v2/index.php?
Action=DescribeInstances
&SecretId=xxxxxxx
&Region=gz
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature       //Common request parameters
&instanceIds.0=ins-0hm4gvho
&instanceIds.1=ins-8oby8q00
&offset=0
&limit=20
&status=2
&zoneId=100003      //API request parameters
```

