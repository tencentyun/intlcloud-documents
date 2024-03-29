온라인 비디오 산업의 급속한 발전과 함께 저작권 침해가 증가함에 따라 저작권 보호는 콘텐츠 소유자의 주요 관심사가 되었습니다.

엔터프라이즈 DRM 솔루션은 재생 License를 사용하여 높은 수준의 콘텐츠 보호를 제공합니다. 장치가 DRM으로 암호화된 비디오를 재생하려면 비디오를 해독할 수 있는 License(복호화 키, 키의 유효 기간 및 장치 정보와 같은 정보 포함)를 받아야 합니다.

엔터프라이즈 DRM 솔루션의 강점은 다음과 같습니다.

<ul>
<li>키는 콘텐츠 암호 해독 모듈(CDM)에서만 읽을 수 있습니다.</li>
<li>각 License는 하나의 장치에만 사용할 수 있습니다.</li>
<li>License의 유효 기간을 설정할 수 있습니다.</li>
<li>하드웨어 기반 TEE 및 디코딩을 지원합니다.</li>
</ul>

Widevine과 FairPlay는 두 가지 메인 스트림 DRM 솔루션입니다.

| DRM 솔루션 | 어댑티브 비트레이트 스트리밍 프로토콜 | 플레이어 및 브라우저                                        |
| ------------ | ---------- | --------------------------------------------- |
| Widevine     | HLS, DASH   | Andriod 플레이어, Chrome, Firefox, Edge, Opera 등 |
| FairPlay     | HLS        | iOS 플레이어, Safari 등                        |

## VOD DRM 개요
엔터프라이즈 DRM 솔루션은 비디오 콘텐츠에 대한 높은 수준의 보호를 제공하지만 처음부터 사용하기 어려울 수 있습니다. VOD는 엔터프라이즈 DRM 솔루션을 기반으로 하고 DRM 암호화, License 관리, License 배포, 암호 해독 및 재생을 포함한 모든 기능을 통합하는 사용하기 쉬운 DRM 체계를 제공합니다.

다음은 VOD DRM 체계의 작업 흐름입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ae358775adc9711065239394b246ab50.png)

## 통합 가이드
VOD DRM 체계를 빠르게 통합하는 방법에 대한 설명은 [Playing DRM-Encrypted Videos](https://intl.cloud.tencent.com/document/product/266/46642)를 참고하십시오.

## 요금 관련
VOD의 DRM 방식을 사용하면 다음과 같은 요금이 발생할 수 있습니다.

- 트랜스 코딩 요금: 동영상은 DRM 암호화 중에 트랜스 코딩되며, 트랜스 코딩 요금이 발생합니다.
- 스토리지 요금: 트랜스 코딩 후 생성된 영상은 스토리지 공간을 차지하므로 스토리지 요금이 발생합니다.
- DRM 재생 요금: DRM으로 암호화된 동영상을 재생하기 위한 License 요청 건수에 따라 DRM 재생 요금이 부과됩니다.

가격에 대한 자세한 내용은 [구매 가이드](https://intl.cloud.tencent.com/document/product/266/14666)를 참고하십시오.
