## 现象描述

在 [SSL 证书管理控制台](https://console.cloud.tencent.com/ssl) 上传第三方 SSL 证书时提示 “解析失败，请检查证书是否符合标准”。

## 可能原因
- 原因1：上传的证书格式错误。

- 原因2：上传的证书链不完整。

- 原因3：因证书格式校验，需删除多余空格。


## 解决办法

#### 上传的证书格式错误

请检查上传的证书格式是否正确。
- 证书文件以 “-----BEGIN CERTIFICATE-----” 开头，以 “-----END CERTIFICATE-----” 结尾。

- 私钥格式以 “-----BEGIN (RSA) PRIVATE KEY-----” 开头，以 “-----END (RSA) PRIVATE KEY-----” 结尾。


#### 上传的证书链不完整

请检查上传的证书链是否完整，详情请参考 [如何补全 SSL 证书链](https://intl.cloud.tencent.com/document/product/1007/39701)。

#### 因证书格式校验，需删除多余空格

请检查上传的证书内容是否包含多余空格。