CSS는 Widevine, FariPlay 및 NormalAES를 기반으로 하는 DRM 암호화 기능을 제공하여 콘텐츠를 보호하고 불법 복제 및 링크 도용 방지에 도움을 줍니다. 본문에서는 CSS 콘솔에서 DRM 암호화를 구성하는 방법을 안내합니다.

## 주의 사항
Tencent Cloud는 콘텐츠만 암호화합니다. DRM 라이선스는 라이선스 요금을 부과하는 타사 라이선스 서비스인 SDMC 및 DRMtoday에서 제공합니다. 자세한 내용은 SDMC 또는 DRMtoday에 문의하시기 바랍니다.

## 전제 조건
- CSS를 활성화하고 [재생 도메인 이름](https://intl.cloud.tencent.com/document/product/267/35970)을 추가해야 합니다.
- [SDMC DRM](https://console.multidrm.tv/setting/drm/index) 또는 [DRMtoday](https://castlabs.com/free-trials/drmtoday/)에서 계정을 생성하고 액세스 키를 구성했습니다.

## 콘솔 구성
[](id:step1)

### DRM 키 정보 구성
1. CSS 콘솔에 로그인하고 왼쪽 사이드바에서 **기능 구성** > [DRM 관리](https://console.cloud.tencent.com/live/config/record)를 선택합니다.
2. **편집**을 클릭하고 라이선스 공급자(SDMC 또는 DRMtoday)를 선택한 다음 주요 정보를 입력합니다.
- 라이선스 서비스 제공업체가 **SDMC**인 경우:
   - SDMC UID, SecretID 및 SecretKey를 입력합니다(SDMC에서 정보를 얻어야 함).
![](https://qcloudimg.tencent-cloud.cn/raw/09a9b34d85b87b89c43e5c5831530ee9.png)
-  라이선스 서비스 제공업체가 **DRMtoday**인 경우:
   - DRMtoday MerchantName, MerchantUUID, MerchantApiName, MerchantApiPassword, KeySeedID 및 IvSeedID를 입력합니다. (DRMtoday에서 정보를 얻어야 합니다.)
![](https://qcloudimg.tencent-cloud.cn/raw/292500dccf57d708dca961985020cbc6.png)

[](id:step2)
### 트랜스 코딩 템플릿 생성 및 도메인 바인딩
1. 왼쪽 사이드바에서 **기능 구성** > [라이브 트랜스 코딩](https://console.cloud.tencent.com/live/config/transcode)을 선택합니다.
2. **트랜스 코딩 템플릿 생성**을 클릭하고 템플릿에 대해 DRM 암호화를 활성화합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/048b9d46b1b5305605b2cd41a0a85b75.png)
<table>
<thead><tr><th width=18%>DRM 구성 항목</th><th>필수 입력 여부</th><th>설명</th></tr></thead>
<tbody><tr>
<td>DRM 암호화</td>
<td>No</td>
<td>DRM 암호화 활성화 여부. 기본적으로 비활성화되어 있습니다. 이 기능을 활성화하기 전에 DRM 관리에서 DRM 키 정보를 구성해야 합니다</td>
</tr><tr>
<td>암호화 유형</td>
<td>Yes</td>
<td>Widevine, Fairplay 또는 NomalAES. FairPlay 암호화의 경우 Apple에서 받은 인증서를 플레이어에 업로드해야 합니다. 자세한 내용은 <a href="https://www.tencentcloud.com/document/product/267/48069">Fairplay 인증서 신청</a>을 참고하십시오.</td>
</tr>
<td>트랙(해상도)</td>
<td>Yes</td>
<td>SD, HD, UHD1 또는 UHD2.</a></td>
</tr>
</tbody></table>

3. **도메인 이름 바인딩**을 클릭하여 템플릿을 재생 도메인에 바인딩합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/96151a6cb6428abceca9e85a66728f99.png)

[](id:step3)
### DRM으로 암호화된 재생 URL 얻기
HLS 재생만 DRM 암호화를 지원합니다. [주소 생성기](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)를 사용하여 재생 URL을 생성합니다(생성된 템플릿 선택). 생성된 HLS URL은 DRM으로 암호화됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/823cbe64c7fb7fdcbd88f5b3742eacf5.png) 

[](id:step4)
### 플레이어 구성
DRM 암호화 기능이 작동하려면 플레이어가 다음 요구 사항을 충족해야 합니다.
- [SDMC](https://www.xmediacloud.com/contact-us/)는 비디오 데이터에서 라이선스 정보를 얻고 해독할 수 있는 기능을 갖추고 있어야 합니다.
- iOS 플레이어의 경우 FairPlay 암호화를 사용하고 Android 플레이어의 경우 Widevine 또는 NormalAES를 사용합니다.
- iOS 플레이어의 경우 Apple에서 인증서를 받아 [SDMC 플랫폼](https://console.multidrm.tv/licenses/drm/index)에 업로드해야 합니다.

>? SDMC 콘솔을 방문하려면 먼저 계정을 생성해야 합니다. SDMC 계정 생성 방법에 대한 자세한 안내는 [UID 및 키 정보 가져오기](https://www.tencentcloud.com/document/product/267/48070)를 참고하십시오. 문제 발생 시 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 하시면 전체 프로세스를 책임지고 해결해 드리겠습니다.
