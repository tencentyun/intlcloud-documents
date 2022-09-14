StreamLive DRM加密支持用户自定义秘钥（CustomDRMKeys）和SDMCDRM。设置入口在**Channel Management**中，对需要配置的Channel进行**Edit**，进入到**Output Group Setting**中的**DRM**设置模块。
![](https://qcloudimg.tencent-cloud.cn/raw/95418fc6d0cf376df994b1d0423d3d0d.png)

>? 目前HLS类固定为Fairplay，DASH类固定为Widevine。


## CustomDRMKeys
### 1. Fairplay
![](https://qcloudimg.tencent-cloud.cn/raw/8cf25c1d7543cd338a45a6cb9979fc12.png)
- **Cid**：Fairplay加密Content Id，如您使用的DRM系统不需要，则可以填一个唯一ID代替。
- **Key**：Fairplay加密Key。
- **Iv**：Fairplay加密Iv。

### 2. Widevine
Widevine支持AUDIO、SD、HD、UHD1、UHD2五种类型的Track，每个Track可以单独配置各个的KeyId和Key。如您使用的DRM系统没有单独为不同类型Track提供秘钥或者使用了相同秘钥，则您可以使用All Track统一设置。
![](https://qcloudimg.tencent-cloud.cn/raw/177f7f0dbdefb1d89301b743680c54d8.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0e7ac02908541f47db2c7ccf6f2cf8ad.png)


## SDMCDRM
![](https://qcloudimg.tencent-cloud.cn/raw/ef29af2c0bf02295069e35ef7f9aca0c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/385e2c9d4c16f8c4c3d594b18cb58e8c.png)

- **Cid**：SDMC DRM提供的Content Id（可选），如不填则使用Channel Id代替。
- **Uid**：SDMC DRM提供的Uid（用户ID）。
- **Secret id**：SDMC DRM提供的Secret Id。
- **Secret key**：SDMC DRM提供的Secret Key。
- **Url**：获取SDMC DRM秘钥的地址，由SDMC DRM提供。
- **Tokenname**：请求SDMC DRM秘钥的地址时的Token名称（可选），由SDMC DRM提供，不填默认使用'token'。
