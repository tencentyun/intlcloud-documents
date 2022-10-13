StreamLive는 사용자 지정 키(CustomDRMKeys) DRM 및 SDMCDRM을 지원합니다. DRM을 구성하려면 **Channel Management**로 이동하여 DRM을 구성할 Channel을 찾은 다음 **Edit**를 클릭합니다. **Output Group Setting** 페이지의 DRM 영역에서 **DRM**을 구성합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/95418fc6d0cf376df994b1d0423d3d0d.png)

>? 현재 HLS 출력은 Fairplay DRM만 지원하고 DASH 출력은 Widevine DRM만 지원합니다.


## CustomDRMKeys
### 1. Fairplay
![](https://qcloudimg.tencent-cloud.cn/raw/8cf25c1d7543cd338a45a6cb9979fc12.png)
- **Cid**: Fairplay Content Id입니다. DRM 시스템에서 콘텐츠 ID를 사용하지 않는 경우 사용자 지정 ID를 입력합니다.
- **Key**: Fairplay 암호화 Key.
- **Iv**: Fairplay 암호화 Iv.

### 2. Widevine
Widevine은 AUDIO, SD, HD, UHD1 및 UHD2의 5가지 Track 유형을 지원합니다. 각 Track에 대해 별도의 KeyId와 Key를 구성할 수 있습니다. DRM 시스템이 다른 Track에 대한 키를 제공하지 않거나 동일한 키를 사용하는 경우 All Track을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/177f7f0dbdefb1d89301b743680c54d8.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0e7ac02908541f47db2c7ccf6f2cf8ad.png)


## SDMCDRM
![](https://qcloudimg.tencent-cloud.cn/raw/ef29af2c0bf02295069e35ef7f9aca0c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/385e2c9d4c16f8c4c3d594b18cb58e8c.png)

- **Cid**: SDMC에서 제공한 Content Id입니다. 비워 두면 Channel Id가 사용됩니다.
- **Uid**: SDMC에서 제공한 Uid(사용자 ID)입니다.
- **Secret id**: SDMC에서 제공한 Secret Id입니다.
- **Secret key**: SDMC에서 제공하는 Secret Key입니다.
- **Url**: DRM 키를 가져오는 URL(SDMC 제공)입니다.
- **Tokenname**: SDMC에서 제공하는 키 URL의 Token 이름입니다. 비워 두면 ‘token’이 사용됩니다.
