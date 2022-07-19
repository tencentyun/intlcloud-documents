CSS는 Widevine, FariPlay 및 NormalAES를 기반으로 하는 DRM 암호화 기능과 링크 도용 방지를 제공하여 콘텐츠를 보호하고 불법 복제를 방지합니다. 본문에서는 CSS 콘솔에서 DRM 암호화를 구성하는 방법을 안내합니다.

## 주의 사항
Tencent Cloud는 동영상만 암호화합니다. DRM 라이선스는 라이선스 요금을 부과하는 서드 파티 라이선스 서비스 SDMC에서 제공합니다. 자세한 사항은 해당 업체에 문의하시기 바랍니다.

## 전제 조건
- CSS를 활성화하고 [재생 도메인 이름](https://intl.cloud.tencent.com/document/product/267/35970)을 추가해야 합니다.
- [SDMC](https://www.xmediacloud.com/contact-us/)로 계정을 생성하고 DRM 키를 구성해야 합니다.

## 콘솔 설정
[](id:step1)

### DRM 키 정보 구성
1. CSS 콘솔에 로그인하고 왼쪽 사이드바에서 **기능 설정**>[DRM 관리](https://console.cloud.tencent.com/live/config/record)를 선택합니다.
2. **편집**을 클릭하고 UID, SecretID 및 SecretKey를 입력합니다(정보는 SDMC에서 제공됨).
![](https://qcloudimg.tencent-cloud.cn/raw/4a88319f757d161c4b86cbeef27cbf84.png)

[](id:step2)
### 트랜스 코딩 템플릿 생성 및 도메인 바인딩
1. 왼쪽 사이드바에서 **기능 설정** > [라이브 트랜스 코딩](https://console.cloud.tencent.com/live/config/transcode)을 선택합니다.
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
<td>Widevine, Fairplay 또는 NomalAES. FairPlay 암호화의 경우 Apple에서 받은 인증서를 플레이어에 업로드해야 합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/267/48069">Obtaining a FairPlay Certificate</a>를 참고하십시오.</td>
</tr>
</tbody></table>

3. **도메인 이름 바인딩**을 클릭하여 템플릿을 재생 도메인에 바인딩합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/96151a6cb6428abceca9e85a66728f99.png)

[](id:step3)
### DRM으로 암호화된 재생 URL 얻기
HLS 재생만 DRM 암호화를 지원합니다. [주소 생성기](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)를 사용하여 재생 URL을 생성합니다(생성된 템플릿 선택). 생성된 HLS URL은 DRM으로 암호화됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/823cbe64c7fb7fdcbd88f5b3742eacf5.png) 

[](id:step4)
### 플레이어 설정
DRM 암호화 기능이 작동하려면 플레이어가 다음 요구 사항을 충족해야 합니다.
- [SDMC](https://www.xmediacloud.com/contact-us/)는 비디오 데이터에서 라이선스 정보를 얻고 해독할 수 있는 기능을 갖추고 있어야 합니다.
- iOS 플레이어의 경우 FairPlay 암호화를 사용하고 Android 플레이어의 경우 Widevine 또는 NormalAES를 사용합니다.
- iOS 플레이어의 경우 Apple에서 인증서를 받아 [SDMC 플랫폼](https://www.xmediacloud.com/contact-us/)에 업로드해야 합니다.
