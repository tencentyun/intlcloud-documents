# TRTC 과금

본 문서는 TRTC가 월간 통계에 따라 [실시간 음성 통화](https://intl.cloud.tencent.com/document/product/647/36064), [실시간 영상 통화](https://intl.cloud.tencent.com/document/product/647/36063) 및 [인터랙티브 라이브 비디오 스트리밍](https://intl.cloud.tencent.com/document/product/647/36059)의 사용 요금을 계산하는 방법을 소개합니다.

당사 영업팀과 계약을 체결한 경우, 실제 과금 정보는 계약을 기준으로 합니다.

## 과금 구성

매월 말에 TRTC는 해당 월의 [Tencent Cloud 계정](https://console.intl.cloud.tencent.com/trtc)에 속한 모든 프로젝트에서 생성된 오디오 및 비디오 사용량(분 단위)을 계산합니다. 비디오 사용량은 총 해상도 집계를 3등급으로 구분해 가격을 책정합니다. TRTC가 각 개발자 계정별로 제공하는 [매월 10,000분의 무료 시간](https://docs.agora.io/cn/faq/billing_free)을 차감한 후, 잔여 오디오 사용량과 비디오 사용량에 해당하는 단가를 곱하고 합산하여 해당 월의 총 요금을 계산합니다.

기본 과금 공식은 다음과 같습니다.

**월간 요금** = **오디오 사용량** × **오디오 단가** + **각 등급별 비디오 사용량** × **해당 비디오 단가**

### 사용량

각 대화별 사용량은, 해당 대화 내 **모든 사용자 사용량의 합계입니다**.

-   **비디오 사용량**: 사용자가 비디오 스트림을 성공적으로 구독하면 비디오 사용량이 발생합니다. 오디오 스트림과 비디오 스트림을 동시에 구독할 경우 비디오 사용량만 계산됩니다.
-   **오디오 사용량**: 사용자가 비디오 스트림을 구독하지 않으면 오디오 스트림 구독 여부와 관계없이 오디오 사용량이 발생합니다.

### 단가

오디오/비디오 사용량의 단가는 다음과 같습니다.

| 사용량 유형          | 단가(USD/1,000분) |
| :---------------- | :------------------ |
| 오디오              | 0.99                |
| SD        | 1.99                |
| HD        | 3.99                |
| Full HD | 14.99               |

TRTC는 사용자가 수신한 모든 비디오의 총 해상도 집계를 다음 세 가지 비디오 유형으로 나누고 각 유형별 요금을 계산합니다.

| 비디오 사용량 유형      | 사용자가 구독한 비디오의 총 해상도                                  |
| :---------------- | :-------------------------------------------------------- |
| SD        | 총 해상도 집계 ≤ 307,200(640 × 480)                         |
| HD        | 307,200(640 × 480)＜ 총 해상도 집계 ≤ 921,600(1280 × 720) |
| Full HD | 921,600(1280 × 720)＜ 총 해상도 집계                        |

예를 들어 사용자 A가 960 × 720의 해상도로 두 개의 비디오 스트림을 동시 구독한 경우, 총 해상도 집계는 960 × 720 + 960 × 720 = 1,382,400입니다. 비디오 사용량은 Full HD 단가로 과금됩니다.

## 선불 패키지

TRTC는 멀티미디어 범용 패키지(링크 추가)를 제공합니다. 음성, SD, HD, FHD 사용량에 따라 **1:2:4:15**로 시간이 차감됩니다. 예를 들어 HD 비디오 시간이 1분이면 범용 패키지에서 4분이 차감됩니다.

범용 패키지 가격은 다음과 같습니다.

<table>
     <tr>
         <th style="text-align:center">패키지 유형</th>  
         <th style="text-align:center">패키지 시간(1,000분)</th> 
         <th style="text-align:center">정가(USD/1,000분)</th> 
         <th style="text-align:center">패키지 단가(USD/1,000분)</th> 
         <th style="text-align:center">패키지 가격(USD)</th> 
          <th style="text-align:center">할인</th> 
     </tr>
     <tr>
         <td style="text-align:center" rowspan="4">고정 패키지</td>   
         <td style="text-align:center">25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center">24</td>   
         <td style="text-align:center">3% off</td>     
     </tr> 
     <tr>
         <td style="text-align:center">250 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center">227</td>   
         <td style="text-align:center">8% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center">856</td>   
         <td style="text-align:center">13.5% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center">3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">2416</td>   
         <td style="text-align:center">18.7% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="5">사용자 정의 패키지</td>   
         <td style="text-align:center">0 < T < 25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center" rowspan="5">패키지 단가*패키지 시간 T</td>   
         <td style="text-align:center"> original </td>    
     </tr> 
     <tr>
         <td style="text-align:center">25 ≤ T < 250</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center">3% off</td>    
     </tr> 
     <tr>
         <td style="text-align:center">250 ≤ T < 1000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center">8% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 ≤ T ＜ 3000</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center">13.5% off</td>   
     </tr> 
     <tr> 
         <td style="text-align:center">T ≥ 3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">18.7% off</td>   
     </tr> 
</table>

> ?
>-   표의 패키지 단가는 1,000분당 단가를 기준으로 소수점 셋째 자리까지 계산된 것이며, 실제 요금은 분당 단가를 기준으로 소수점 여덟째 자리까지 계산됩니다. 상세 내용
>-   TRTC 선불 서비스를 사용하려면 화이트리스트 심사가 필요합니다. 문의하기[여기에 링크 추가]를 통해 활성화하십시오.
>-   월 평균 시간(분)이 3M 분을 초과하며, 추가 지원 및 견적 서비스를 받고자 하는 경우 영업팀에 문의[여기에 링크 추가] 하시기 바랍니다.

## 과금 예시

본문은 TRTC가 비디오의 총 해상도 집계, 각 서비스 유형별 사용량 및 관련 요금을 계산하는 방법을 설명합니다.

5명의 사용자가 동시에 한 채널에 입장하여 60분의 인터랙티브 라이브 비디오 스트리밍을 진행한 경우를 가정합니다. 3명의 호스트(호스트 A, B, C)가 있고, 호스트 A의 비디오 해상도는 960×720, 호스트 B와 C의 비디오 해상도는 640×480입니다. 2명의 시청자가 모든 호스트의 비디오 스트림을 구독했습니다. 호스트 A는 채널의 다른 모든 사용자와 화면을 공유했습니다. 화면 공유 스트림의 해상도는 1920 × 1080입니다.

### 비디오의 총 해상도 집계

다음 표는 각 사용자의 비디오 사용량 유형과 단가를 결정하기 위해 각 사용자의 구독 비디오 스트림의 총 해상도 집계 계산 방법입니다.

| 사용자              | 구독한 비디오 스트림                 | 비디오 총 해상도                              | 총 해상도  | 비디오 사용량 유형 |
| :---------------- | :--------------------------- | :-------------------------------------------- | :-------- | :----------- |
| 호스트 A + 화면 공유 | 호스트 2명                     | 640 × 480 × 2                                 | 614,400   | HD    |
| 호스트 B            | 호스트 2명 + 호스트 A 화면 공유 | (960 × 720) + (640 × 480) + (1920 x 1080)     | 3,072,000 | FHD |
| 호스트 C            | 호스트 2명 + 호스트 A 화면 공유 | (960 × 720) + (640 × 480) + (1920 x 1080)     | 3,072,000 | FHD |
| 시청자 1            | 호스트 3명 + 호스트 A 화면 공유 | (960 × 720) + (640 × 480 × 2) + (1920 x 1080) | 3,379,200 | FHD |
| 시청자 2            | 호스트 3명 + 호스트 A 화면 공유 | (960 × 720) + (640 × 480 × 2) + (1920 x 1080) | 3,379,200 | FHD |

### 과금

다음 표는 인터랙티브 라이브 비디오 스트리밍에서 발생한 총 요금 계산 방법입니다.

<table>
     <tr>
         <th style="text-align:center">유료 서비스(비디오 사용량 유형)</th>
         <th style="text-align:center">총 사용량(분) = 각 사용자의 사용량 합계</th>
         <th style="text-align:center">단가(USD/1,000분)</th>
         <th style="text-align:center">서비스 요금(USD)</th>
         <th style="text-align:center">총 요금(USD) (소수점 두 자리까지 반올림)</th>
     </tr>
     <tr>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">60</td>
         <td style="text-align:center">3.99</td>
         <td style="text-align:center">(60/1000) × 3.99 = 0.2394</td>
         <td style="text-align:center" rowspan="2">13.68</td>
     </tr>
     <tr>
         <td style="text-align:center">FHD</td>
         <td style="text-align:center">60 × 4 = 240</td>
         <td style="text-align:center">14.99</td>
         <td style="text-align:center">(240/1000) × 14.99 = 13.44</td>
     </tr>
</table>

## 주의 사항

본문은 주의 사항 및 참고 사항입니다.

### 사용량 정확도

TRTC는 해당 월의 초 단위 누적 사용 시간을 통계한 뒤, 분으로 전환하여 과금합니다. 매월 말에 월별 사용량이 정산되면 TRTC는 해당 월에 발생한 오디오와 비디오 유형별 사용량(초 단위)을 각각 더한 다음 60으로 나누어 분 단위 오디오 및 비디오 유형별 사용량을 얻고, **올림**하여 정수를 얻습니다. 예를 들어 한 달에 59초의 오디오 사용량이 발생하면 오디오 사용량은 1분으로 계산되고 61초의 비디오 사용량이 생성되면 비디오 사용량은 2분으로 계산됩니다. 월간 사용량 오차는 1분 이내입니다.

### 듀얼 스트림 해상도

듀얼 스트림 모드에서 사용자의 해상도 계산 방법은 다음과 같습니다.

-   고화질 스트림을 구독하는 경우 사용자의 총 해상도 집계는 발송측이 설정한 고화질 스트림 해상도를 기준으로 계산합니다.
-   저화질 스트림을 구독하는 경우 사용자의 총 해상도 집계는 사용자가 실제로 수신한 해상도를 기준으로 계산합니다.

### 화면 공유 스트림의 해상도

귀하의 시나리오에 화면 공유가 포함되는 경우 화면 공유 스트림의 비디오 단가는 'TRTCVideoEncParam'에서 설정한 비디오 해상도를 기준으로 합니다. 설정 방법은 다음 설명을 참고하십시오.

-   모든 플랫폼 C++: [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#ab1fc5a303726a666d30051c836e33fdd)
-   iOS: [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791) [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4)
-   macOS: [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97)
-   Android:[startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f)

Web 에서는 디바이스 및 브라우저의 제한으로 인해 일부 브라우저가 설정된 화면 속성에 완전히 적용되지 못할 수 있습니다. 이 경우 브라우저는 자동으로 해상도를 조정하고 실제 해상도에 따라 과금합니다. [setScreenProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setScreenProfile)을 참고하십시오.

### 다른 제품 또는 서비스 과금

귀하의 시나리오에서 영상 통화 및 인터랙티브 라이브 스트리밍 외에 다른 TRTC 제품 또는 서비스, 클라우드 혼합 스트림 트랜스 코딩 등이 포함되는 경우 추가 요금 청구됩니다. 자세한 내용은 각 TRTC 제품 또는 서비스에 대한 과금 설명을 참고하십시오.
