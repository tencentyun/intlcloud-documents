The final request URL is made up of the following elements:
- Request domain name: the request domain for the [AddProject](https://intl.cloud.tencent.com/document/product/378/4398) API (for creating a project) is account.api.qcloud.com. This value varies by API action. For more information, please see the description of each API.
- Request path: the request path of TencentCloud API is always `/v2/index.php`.
- The final request parameter string consists of common request parameters and API request parameters.

The final request URL is concatenated as follows:
`https:// + request domain name + request path + ? + final request parameter string`

The final request URL is as follows (the first five parameters are common request parameters, and the last two ones are API request parameters):

```
  https://account.api.qcloud.com/v2/index.php?
  Action=AddProject
  &SecretId=xxxxxxx
  &Timestamp=1465055529
  &Nonce=59485
  &Signature=mysignature
  &projectName=test
  &projectDesc=For testing

```
