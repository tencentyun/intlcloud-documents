## 개요

이미지 고급 압축은 COS에서 CI를 기반으로 출시한 이미지 압축 기능입니다. 이미지를 TPG 또는 HEIF 등 압축 비율이 높은 포맷으로 효율적으로 전환할 수 있어 이미지 전송 링크 및 로딩 시 소모되는 시간을 효과적으로 단축하고 대역폭 및 트래픽 비용을 절감할 수 있습니다.

| 기능      | 소개                                                         |
| :-------- | :----------------------------------------------------------- |
| TPG 압축  | TPG는 Tencent가 출시한 자체개발 이미지 포맷입니다. JPG, PNG, GIF, WEBP 포맷 등의 이미지를 TPG 포맷으로 전환할 수 있으며, 이미지 크기를 대폭 줄일 수 있습니다. |
| HEIF 압축 | iOS 환경의 이미지 사용 시나리오에서 JPG, PNG, GIF, WEBP 포맷 등의 이미지를 HEIF 포맷으로 전환할 수 있으며, HEIF 포맷은 초고압축률의 이미지 포맷입니다. |

>?
>
>- TPG는 Tencent가 자체개발한 이미지 포맷입니다. 사용할 경우 **이미지 로딩 환경에서 TPG 디코딩을 지원하는지** 확인하십시오. Tencent Cloud CI는 TPG 디코더의 iOS, Android, [Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip) 터미널 SDK 통합을 제공하여 TPG에 빠르게 액세스하고 사용할 수 있습니다.
>- 현재 iOS 11 이상 및 Android P 시스템은 기본적으로 HEIF 포맷을 지원합니다.
>- 이미지 고급 압축은 유료 서비스이며, CI 서비스에서 요금이 청구됩니다. 요금에 대한 자세한 내용은 CI의 [가격 문서](https://intl.cloud.tencent.com/document/product/1045/33431)를 참조하십시오.

## 적용 시나리오

PC, App 등 여러 단말의 이미지 압축 요건을 충족하며 이커머스, 미디어 등 비즈니스 시나리오에 적합합니다.

## 사용 방법

#### COS 콘솔 사용

COS 콘솔을 사용해 이미지 고급 압축 기능을 활성화할 수 있습니다. 자세한 내용은 [이미지 고급 압축 설정](https://intl.cloud.tencent.com/document/product/436/40117) 콘솔 가이드 문서를 참조하십시오.

#### REST API 사용 

API를 사용해 버킷에 있는 이미지를 압축할 수 있습니다. 자세한 내용은 [이미지 고급 압축](https://intl.cloud.tencent.com/document/product/436/40119) API 문서를 참조하십시오.
