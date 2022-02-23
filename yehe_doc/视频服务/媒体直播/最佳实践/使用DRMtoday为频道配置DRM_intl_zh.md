### 步骤1：申请账户

1. 申请DRMtoday

   a. 进入[DRMtoday产品页面](https://castlabs.com/drmtoday/)申请开通DRMtoday；
   ![img](https://main.qcloudimg.com/raw/b1fa760d75f68f27c4470bf52f81b800.png)

   b. 申请完成后可获取DRMtoday账户、密码及Dashboard网址。

2. 申请Fairplay证书

   a. 进入[Apple Fairplay官网](https://developer.apple.com/streaming/fps/)。

   b. 单击[Request FPS Deployment Package](https://idmsa.apple.com/IDMSWebAuth/signin.html?path=%2Fcontact%2Ffps%2F&appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757)填写并提交相关信息。
   ![img](https://main.qcloudimg.com/raw/9592e1021494896689ad0d7135f26560.png)

   c. 获取FPS_Deployment_Package.zip文件。

   d. 参照FPS_Deployment_Package.zip解压后的文档，在本地创建受密码保护的私钥、以及CSR（证书签名请求）。

   e. 参照FPS_Deployment_Package.zip解压后的文档，上传CSR给Apple。页面会返回ASK，请妥善保存。

   f. 将官方创建出的FairPlay Certificate（证书）下载到本地。


## 步骤2：上传Fairplay证书至DRMtoday

进入DRMtoday Dashboard网址，选择 Configuration-DRMsettings。
![img](https://main.qcloudimg.com/raw/352f6e951f0ca3252c5bf346ad19464b.png)
参数：

- **Default IV**：可置空。

勾选**Update certificate and keys**后，配置以下参数：

   - **Application secret key(ASK)**：申请Fairplay证书时第5步收到的ASK，以hex编码格式输入。
    
   - Provider certificate：申请Fairplay证书时第6步下载的FairPlay Certificate（证书），上传的证书类型要求为PEM格式，可以使用linux下的openssl工具进行转化。示例：证书名为fairplay.cer，转化命令为：

  ```
  openssl x509 -inform der -in fairplay.cer -out fairplay.pem
  ```

- Provider private key

  ：用户创建受密钥保护的私钥，上传密钥类型要求为PKCS #8 PEM格式，可以使用linux下的openssl工具进行转化。示例：私钥文件名为privatekey.pem，转化命令为:

  ```
  openssl rsa -in privatekey.pem -outform PEM -out out.pem
  ```



## 步骤3：通过DRMtoday API配置Widevine或Fairplay密钥

以下操作均参考DRMtoday官方网站提供的操作文档，原文档见 [DRMtoday Key Ingestion](https://fe.staging.drmtoday.com/frontend/documentation/integration/key_ingestion.html)。

1. CAS认证
   DRMtoday使用CAS（Central Authentication Service）来保护其API免受未经授权的访问，原文档见 [DRMtoday CAS Authentication](https://fe.staging.drmtoday.com/frontend/documentation/integration/cas_authentication.html)。

   a. CAS Login：向Login地址发送HTTP POST请求。

   示例：

   ```
   curl -v 'https://auth.staging.drmtoday.com/cas/v1/tickets' -H 'Content-Type: application/x-www-form-urlencoded' -XPOST -d 'username=${username}&amp;password=${password}'
   ```

   参数：

   - **username、password**：可以使用DRMtoday的账号密码，也可以使用DRMtoday创建的API账号及其密码，[DRMtoday 创建API账号文档](https://fe.staging.drmtoday.com/frontend/documentation/integration/dashboard.html? dummy#adding-accounts)。

   b. CAS Ticket Retrieval：向CAS Login请求后返回的header中的Location地址发送HTTP POST请求。

   示例：

   ```
   curl -v 'https://auth.staging.drmtoday.com/cas/v1/tickets/xxx' -H 'Content-Type: application/x-www-formurlencoded'-XPOST -d 'service=https://fe.staging.drmtoday.com/frontend/api/keys/v2/ingest/${merchantApiName}'
   ```

   参数：

   - **service**：Dashboard-API页面中Ingest key对应的Endpoint，如下图：
     ![img](https://main.qcloudimg.com/raw/299f6fdcdfd5016a48c4b41f530e277a.png)

2. 设置密钥
   认证完成后通过Ingest key API设置Widevine或Fairplay密钥，接口使用文档见[DRMtoday Key Ingestion](https://fe.staging.drmtoday.com/frontend/documentation/integration/key_ingestion.html)。
   示例：

   ```
   curl -v 'https://fe.staging.drmtoday.com/frontend/api/keys/v2/ingest/${merchant}?ticket=${ticket}' -H 'Content-Type: application/json' -H 'Accept: application/json' -XPOST -d '{"assets":[{"type":"CENC","assetId":"assettest","variantId":"varianttest","ingestKeys":[{"streamType":"VIDEO_AUDIO","algorithm":"AES","keyId":"MDAwMDAwMDAwMDAwMDAwMA==","key":"MDAwMDAwMDAwMDAwMDAwMA==","iv":"MDAwMDAwMDAwMDAwMDAwMA=="}]}]}'
   ```

   参数：

   - **merchant**：Dashboard中Ingest key对应的Endpoint。
   - **ticket**：CAS Ticket Retrieval返回的Body内容。
   - **type**：设置为CENC即可支持Widevine和Fairplay。Widevine加密需要配置keyId和key，Fairplay加密需要配置key和iv。
   - **keyId、key、iv**：以base64编码形式设置。“MDAwMDAwMDAwMDAwMDAwMA==” 对应的hex编码为30303030303030303030303030303030。



## 步骤4：在StreamLive上配置DRM密钥

参考StreamLive控制台操作指引 输出组设置（*此处“输出组设置”要跳转链接并定位至“StreamLive频道管理” 三、输出组设置 页面）配置StreamLiveDRM密钥，其中：

- **DRM**：开启
- **Scheme**：Custom DRM Keys

Fairplay密钥：
![img](https://main.qcloudimg.com/raw/d1fd0abc8a2c4b1aa970f74160641731.png)

- **ContentId**：步骤3-2设置密钥中配置的assetId，以hex编码填写。
- **Key**：步骤3-2设置密钥中配置的key，以hex编码填写。
- **Iv**：步骤3-2设置密钥中配置的iv，以hex编码填写。

Widevine密钥：
![img](https://main.qcloudimg.com/raw/d65d6a93e13b12d8014558a601a21692.png)

- **ContentId**：步骤3-2设置密钥中配置的assetId，以hex编码填写。
- **KeyId**：步骤3-2设置密钥中配置的keyId，以hex编码填写。
- **Key**：步骤3-2设置密钥中配置的key，以hex编码填写。


## 步骤5：播放测试

根据StreamLive使用手册配置好播放地址后（例如可以[将直播流输出到StreamPackage的Channel中](https://intl.cloud.tencent.com/document/product/1048/41760#6.-output-content-to-streampackage-through-streamlive)，通过StreamPackage的[Endpoint节点获取播放地址]([控制台指南 | 腾讯云 (tencent.com)](https://intl.cloud.tencent.com/document/product/1063/41787))，可使用[DRMtoday播放页面](https://players.castlabs.com/presto/6.1.2/#/player/config)测试：
![img](https://main.qcloudimg.com/raw/5b8b559d838497dd5b75cf9c7cedf363.png)
![img](https://main.qcloudimg.com/raw/77249ddf9131bc9578bdb28fc3c37fb4.png)
参数：

- **Content URL**：播放内容URL。
- **DRM Environment**：根据实际情况选择。
- **Merchant**：用户在DRMtoday的名称，一般和merchantApiName一致。
- **User ID、Session ID**：可参考[配置文档](https://fe.staging.drmtoday.com/frontend/documentation/integration/dashboard.html#uisetting-Test_dummy)（当License Delivery Authorization类型为Test_dummy时）。
- **Asset ID**：步骤3-2设置密钥中配置的assetId。
- **Variant ID**：步骤3-2设置密钥中配置的variantId。
