StreamLive supports custom key DRM and SDMC DRM. To configure DRM, go to **Channel Management**, find the channel you want to configure DRM for, and click **Edit**. On the **Output Group Setting** page, configure DRM in the **DRM** area.
![](https://qcloudimg.tencent-cloud.cn/raw/95418fc6d0cf376df994b1d0423d3d0d.png)

>? Currently, HLS outputs support only FairPlay DRM and DASH outputs support only Widevine DRM.


## CustomDRMKeys
### 1. FairPlay
![](https://qcloudimg.tencent-cloud.cn/raw/8cf25c1d7543cd338a45a6cb9979fc12.png)
- **Cid**: The FairPlay content ID. If your DRM system does not use content IDs, enter a custom ID.
- **Key**: The FairPlay encryption key.
- **Iv**: The FairPlay encryption IV.

### 2. Widevine
Widevine supports five track types, namely AUDIO, SD, HD, UHD1, and UHD2. You can configure a separate key ID and key for each track. If your DRM system does not provide keys for different tracks or use the same key, select **All Track**.
![](https://qcloudimg.tencent-cloud.cn/raw/177f7f0dbdefb1d89301b743680c54d8.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0e7ac02908541f47db2c7ccf6f2cf8ad.png)


## SDMCDRM
![](https://qcloudimg.tencent-cloud.cn/raw/ef29af2c0bf02295069e35ef7f9aca0c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/385e2c9d4c16f8c4c3d594b18cb58e8c.png)

- **Cid**: The content ID provided by SDMC. If you leave this empty, the channel ID will be used.
- **Uid**: The user ID provided by SDMC.
- **Secret id**: The secret ID provided by SDMC.
- **Secret key**: The secret key provided by SDMC.
- **Url**: The URL to get the DRM key (provided by SDMC).
- **Tokenname**: The token name for the key URL, which is provided by SDMC. If you leave this empty, `token` will be used.
