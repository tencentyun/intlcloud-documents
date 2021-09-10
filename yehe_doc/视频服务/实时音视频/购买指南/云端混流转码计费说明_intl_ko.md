>!
>- 2020년 11월 01일부터 TRTC 콘솔에서 처음으로 [애플리케이션](https://intl.cloud.tencent.com/document/product/647/37714)을 생성한 계정은 **2020년 11월 01일**부터 과금됩니다.
>- 2020년 11월 01일 **이전에** TRTC 콘솔에서 처음으로 [애플리케이션](https://intl.cloud.tencent.com/document/product/647/37714)을 생성한 계정은 **2020년 12월 08일**부터 과금됩니다.
>- 본 문서는 [TRTC의 MCU 클러스터 클라우드 혼합 스트림 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618) 사용으로 발생하는 릴레이 트랜스 코딩 비용 관련 설명을 제공합니다. TRTC 멀티미디어 스트림을 CSS로 릴레이 푸시한 후, [CSS의 클라우드 혼합 스트림 기능](https://intl.cloud.tencent.com/document/product/267/ 37665)을 사용할 경우, CSS는 [라이브 방송 트랜스 코딩](https://intl.cloud.tencent.com/document/product/267/39604) 비용을 청구합니다.
- 트랜스 코딩 후 출력된 멀티미디어 스트림을 CSS 시스템에 푸시하여, 시청자에게 [CDN 라이브 방송 시청 실행](https://intl.cloud.tencent.com/document/product/647/35242)을 할 경우, CSS는 [트래픽/대역폭](https://intl.cloud.tencent.com/document/product/267/2818#.E6.B5.81.E9.87.8F.E5.B8.A6.E5.AE.BD) 요금을 청구합니다.


<span id="Billing_items"></span>
## 사용량 통계 방식

TRTC는 동일한 Tencent Cloud 계정에 속한 모든 애플리케이션의 MCU 혼합 스트림 트랜스 코딩 이후 출력된 **트랜스 코딩 길이**를 기준으로 릴레이 트랜스 코딩 서비스 사용량을 계산합니다. 트랜스 코딩 길이는 인코딩 방식과 트랜스 코딩 결과에 따라 다르며, [비디오 시간](#m_video)과 [음성 시간](#m_voice)으로 구분됩니다.

>! 시간은 초 단위로 계산되며, 누적된 일일 초 단위는 분 단위로 전환하여 과금합니다. 1분 이하의 경우 1분으로 계산합니다.

<span id="m_video"></span>
### 비디오 시간
비디오 시간이란 트랜스 코딩 결과물 중 영상 화면이 포함된 시간입니다. TRTC는 트랜스 코딩된 비디오의 해상도에 따라 비디오 등급을 분류한 후, 각 분류된 등급의 비디오 시간에 따라 과금합니다. 비디오 해상도에 따른 등급 분류는 다음과 같습니다.

| 비디오 등급   | 출력 해상도                   |
| ---------- | ---------------------------- |
| SD    | 640 × 480 이하(포함)        |
| HD    |640 × 480 ~ 1280 × 720(포함)|
| FHD |1280 × 720 초과               |

- 트랜스 코딩 후 출력된 스트림의 일정 구간에 비디오와 오디오가 모두 있는 경우, 비디오 시간만 계산하며 음성 시간을 중복 계산하지 않습니다.
- 트랜스 코딩 후 출력된 스트림 해상도는 변동이 있을 수 있습니다. TRTC는 서비스 사용량을 구간별로 통계합니다. 일반적으로 60초마다 한 번씩 업데이트되며, 해상도가 변경되면 즉시 리포트합니다.

<span id="m_voice"></span>
### 음성 시간

음성 시간이란 트랜스 코딩 결과 중 오디오만 있는 시간을 뜻합니다.

<span id="Fixed_price"></span>
## 서비스 가격
TRTC 클라우드 혼합 스트림 트랜스 코딩 서비스의 정가는 아래 표와 같습니다.

| 인코딩 방식 | 과금 항목                   | 단가(USD/분)    |
| -------- | ------------------------ | ------------------- |
| 오디오 트랜스 코딩 | 릴레이 트랜스 코딩-음성            | 0.000799USD/분   |
| H.264    | 릴레이 트랜스 코딩-H264-SD | 0.00228571 USD/분 |
| H.264    | 릴레이 트랜스 코딩-H264-HD    | 0.00464286USD/분 |
| H.264    | 릴레이 트랜스 코딩-H264-FHD | 0.00899USD/분    |

<span id="Billing_method"></span>

## 과금 방식
TRTC 클라우드 혼합 스트림 트랜스 코딩 서비스는 **일 결산 후불** 방식만 지원하며, 일일 과금 방식에 따라 매일 오전 10시에 전일 발생 비용을 차감합니다.

<span id="Billing_examples"></span>
## 과금 예시
>!본 문서는 정가를 기준으로 계산한 금액에 대한 과금 예시입니다. Tencent Cloud 비즈니스 매니저와 계약을 체결한 경우 계약에서 약정한 금액을 기준으로 합니다.

1월 1일에 TRTC의 MCU 클러스터를 사용하여 클라우드 혼합 스트림 트랜스 코딩 진행, H.264 인코딩 사용, 각각 100분 동안 1920 × 1080 및 640 × 360 해상도 비디오 출력, 오디오 트랜스 코딩을 사용하여 100분의 음성을 출력한 경우, 요금은 다음과 같습니다.

**분석: **
- 1920 × 1080 해상도의 비디오는 FHD등급에 해당되며, 단가는 0.00899 USD/분 입니다.
- 640 × 360 해상도의 비디오는 HD등급에 해당되며, 단가는 0.00464286 USD/분 입니다.
- 음성 단가는 0.000799 USD/분 입니다.

1월 2일에 지불해야하는 1월 1일 릴레이 트랜스 코딩 요금 = 0.00899 USD/분 × 100분 + 0.00464286 USD/분 × 100분 + 0.000799 USD/분 × 100분 = 2.16 USD.

## 관련 문서

- [과금 개요](https://intl.cloud.tencent.com/document/product/647/34610)
- [무료 베타 테스트](https://intl.cloud.tencent.com/document/product/647/39784)
- [음성 ILVB 과금 설명](https://intl.cloud.tencent.com/document/product/647/39785)
- [비디오 ILVB 과금 설명](https://intl.cloud.tencent.com/document/product/647/39786)
- [음성 통화 과금 설명](https://intl.cloud.tencent.com/document/product/647/39787)
- [영상 통화 과금 설명](https://intl.cloud.tencent.com/document/product/647/39788)
- [클라우드 녹화 과금 설명](https://intl.cloud.tencent.com/document/product/647/38385)
- [구매 가이드](https://intl.cloud.tencent.com/document/product/647/35440)
- [과금 FAQ](https://intl.cloud.tencent.com/document/product/647/39789)
