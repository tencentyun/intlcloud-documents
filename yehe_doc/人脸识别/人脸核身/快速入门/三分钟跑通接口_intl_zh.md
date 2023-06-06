## 操作场景

该文档指导您在购买腾讯云人脸核身服务后，通过 API 3.0 Explorer 在线接口调试页面调用腾讯云人脸核身接口，并将该接口对应语言的 SDK 集成到项目。您只需要完成以下步骤，即可快速接入腾讯云人脸核身接口。
## 前提条件

进入腾讯云人脸核身 [API 3.0 Explorer 在线接口调试页面](https://console.tencentcloud.com/api/explorer?Product=faceid&Version=2018-03-01&Action=ApplySdkVerificationToken)，按照以下操作步骤调用接口。
## 操作步骤

以下步骤以调用[申请SDK核验令牌](https://www.tencentcloud.com/zh/document/product/1061/49954)接口为示例
### 步骤一：
在[API 3.0 Explorer 在线接口调试页面](https://console.tencentcloud.com/api/explorer?Product=faceid&Version=2018-03-01&Action=ApplySdkVerificationToken)左侧导航栏，选择申请SDK核验令牌的接口，填入必填参数，发起调用，得到响应结果 。
![ApplySdkVerificationToken](https://staticintl.cloudcachetci.com/yehe/backend-news/Gnrv261_ApplySdkVerificationToken.png)

- Region 参数：参考接口文档为必填参数，域名中的地域信息，该参数决定访问的接入点，例如 `ap-hongkong` 就是要访问香港这个接入点 。每个接口支持的 Region 可能会有所不同，具体可参考您当前调用的接口文档中的   `list of regions` , 如本篇示例[申请SDK核验令牌](https://www.tencentcloud.com/zh/document/product/1061/49954)接口的可支持 Region 需参考 [list of regions](https://www.tencentcloud.com/document/api/1061/36934#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)
	![parameters](https://staticintl.cloudcachetci.com/yehe/backend-news/MUuN845_parameters.png)
- NeedVerifyIdCard 参数：参考接口文档为必填参数，表示是否需要身份证鉴伪，如果不需要，则仅做证件OCR。当前仅IdCardType为HK支持鉴伪 。

### 步骤二：

选择对应的后台语言，生成代码，集成 SDK 到项目中，这里以 Java 为例：
1. 集成代码到项目中，需要导入 SDK 依赖包（可参考以下截图右上角[JAVA SDK使用说明](https://www.tencentcloud.com/zh/document/product/494/7245)）、获取密钥信息并填充到代码的  `SecretId`  和  `SecretKey`  位置，才能调用成功 。
2. 生成代码中的部分字段信息和填写内容是关联的。如需调整传入参数，要在左侧修改参数值后重新生成代码 。

![api](https://staticintl.cloudcachetci.com/yehe/backend-news/mHPB015_api.png)
## 注意事项

- SecretId/SecretKey 生成地址： `https://console.tencentcloud.com/cam/capi` 。
- 当入参中需要传图片/视频 Base64时，需要去掉相关前缀 `data:image/jpg;base64,` 和换行符 `\n` 。
- 如果请求结果提示如下， 需要手动设置签名类型：
  ```
  [TencentCloudSDKException]message:AuthFailure.SignatureFailure-The provided credentials
  could not be validated because of exceeding request size limit, please use new signature 
  method `TC3-HMAC-SHA256`. requestId:719970d4-5814-4dd9-9757-a3f11ecc9b20
  ​```
  
  设置签名类型：
  ​```
   `clientProfile.setSignMethod("TC3-HMAC-SHA256"); // 指定签名算法（默认为 HmacSHA256）`
   ```