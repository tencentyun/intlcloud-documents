## 소개

이미지 고급 압축은 COS에서 CI를 기반으로 출시한 이미지 압축 기능입니다. 이미지 포맷을 TPG 또는 HEIF의 압축 비율이 높은 포맷으로 효율적으로 트랜스 코딩할 수 있어 이미지 전송 링크 및 로딩 시 소모되는 시간을 효과적으로 단축하고 대역폭 및 트래픽 비용을 절감할 수 있습니다.

>?
>
>- 이미지 고급 압축 기능으로 JPG/PNG/GIF/WEBP 포맷 등의 이미지를 TPG/HEIF 포맷으로 트랜스 코딩할 수 있습니다.
>- TPG는 Tencent가 자체개발한 이미지 포맷입니다. 사용할 경우 **이미지 로딩 환경에서 TPG 디코딩을 지원하는지** 확인하십시오. Tencent Cloud CI는 TPG 디코더의 iOS, Android, [Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip) 터미널 SDK 통합을 제공하여 TPG에 빠르게 액세스하고 사용할 수 있습니다.
>- 현재 iOS 11 이상 및 Android P 시스템은 기본적으로 HEIF 포맷을 지원합니다.
>- 이미지 고급 압축은 유료 서비스이며, CI 서비스에서 요금이 청구됩니다. 요금에 대한 자세한 내용은 CI의 [가격 문서](https://intl.cloud.tencent.com/document/product/1045/33431)를 참조하십시오.

## 작업 순서

1. [COS 콘솔](https://console.cloud.tencent.com/cos5/bucket)에 로그인한 뒤 [버킷 리스트] 페이지에서 이미지 고급 압축 기능을 활성화할 버킷을 선택하고 버킷 관리 페이지로 이동합니다.
2. [데이터 처리]>[이미지 처리] 탭을 클릭하고 인터페이스에서 **이미지 고급 압축** 설정 항목을 찾습니다.
3. [편집]을 클릭하고 현재 상태를 '활성화'로 변경한 후 [저장]을 클릭합니다.
   ![](https://main.qcloudimg.com/raw/f336e71135338664375a4953fabb5a6e.png)
4. 기능을 활성화하면 해당하는 [이미지 고급 압축](https://intl.cloud.tencent.com/document/product/436/40119) API를 사용해 현재 버킷에 있는 이미지 리소스를 다운로드할 때 TPG/HEIF 압축을 수행할 수 있습니다.
