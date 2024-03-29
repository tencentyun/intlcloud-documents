### 在密钥管理系统中创建的用户主密钥的个数是否有限制？
是。每账户每区域下限制创建200个 CMK，计划删除状态下的除外。不包含云产品密钥。如需创建更多的 CMK，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 或联系腾讯云商务。

### 哪些云服务可以使用密钥管理系统加密数据？ 
KMS 服务无缝对接腾讯云 TencentDB，COS，CBS 等业务，通过 KMS 提供信封加密的方式对云产品数据进行加密。

### 如何使用 KMS 服务加密数据？ 
您可以使用以下三种方式调用腾讯云 KMS 服务：
- 通过 KMS API 调用 KMS 服务。此种场景下，您的业务应用程序在腾讯云内或腾讯云外均可。
- 通过腾讯云 KMS SDK 集成到您自己的业务应用程序中调用 KMS 服务。此种场景下，您的业务应用程序在腾讯云内或腾讯云外均可。
- 通过已经与 KMS 对接的腾讯云产品调用 KMS 服务，对该腾讯云云产品的数据进行加解密操作。

### 如何开启密钥轮换功能？ 
- 您可以在控制台配置让腾讯云 KMS 每年自动轮换 CMK。 
- CMK 轮换后，用户无需重新加密数据，腾讯云会自动保留原 CMK，使用原 CMK 加密的旧的密文依然可以解密，新的数据加密则使用新的 CMK。 

### 关于量子密钥服务？
根据产品发布计划，密钥管理系统已经停止提供量子密钥管理服务，已经使用量子密钥的用户可在 [密钥管理系统](https://console.cloud.tencent.com/kms2) 控制台继续使用。

