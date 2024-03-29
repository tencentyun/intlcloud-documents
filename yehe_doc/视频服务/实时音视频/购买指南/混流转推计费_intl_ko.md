본문은 TRTC [혼합 트랜스코딩 릴레이 제품](https://intl.cloud.tencent.com/document/product/647/47631)의 요금 계산 방법에 대해 설명합니다.

당사 영업팀과 계약을 체결한 경우, 실제 과금 정보는 계약을 기준으로 합니다.

## 과금 항목
CDN을 통해 시청자에게 콘텐츠를 전달하려면 TRTC 스트림을 CDN으로 릴레이해야 합니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/73a5c751bc87e73b28be8d3edf056796.png)

1. 앵커 및 공동 앵커링 시청자는 TRTC 푸시 스트림을 통해 음성/영상 통화 및 스트리밍을 구현합니다.
2. 혼합 트랜스코딩 서버는 TRTC 서비스에서 스트림(UDP)을 구독합니다.
3. 혼합 트랜스코딩 서버는 수신한 스트림을 혼합하고 트랜스코딩합니다.
4. 혼합 트랜스코딩 서버는 결과를 CDN으로 보냅니다.

1단계는 TRTC 기본 서비스 요금이 발생합니다. 자세한 내용은 [TRTC 과금](https://intl.cloud.tencent.com/document/product/647/42734)을 참고하십시오.

2, 3, 4단계는 혼합 스트림 릴레이 기능 요금입니다. 그 중 2단계는 무료입니다. 3단계에서는 혼합 트랜스코딩 요금이 발생하고 4단계에서는 릴레이 요금이 발생합니다.

>! 특별 혜택:
> TRTC는 2단계를 무료로 제공할 뿐만 아니라 Tencent Cloud의 라이브 스트리밍 시스템으로 릴레이하는 경우 릴레이 요금도 무료입니다. 즉, 혼합 트랜스코딩 요금만 청구됩니다.

매월 말에 TRTC는 [계정](https://console.intl.cloud.tencent.com/trtc)의 모든 프로젝트에 대해 타사 플랫폼 또는 CDN으로 스트림을 릴레이하는 데 사용되는 총 오디오/비디오 혼합 트랜스코딩 지속 시간(분)과 대역폭(Mbps)을 합산합니다. 비디오 혼합 트랜스코딩 지속 시간은 총 해상도를 기반으로 8가지 카테고리로 분류되며 가격이 다르게 책정됩니다. 월별 혼합 트랜스코딩 요금은 혼합 트랜스코딩 기간에 단가를 곱한 값이고 월간 릴레이 요금은 릴레이에 사용되는 대역폭에 단가를 곱한 값입니다.

과금 공식:

**월별 요금** = **혼합 트랜스코딩 요금** + **릴레이 요금**

### 혼합 트랜스코딩 요금
혼합 스트림 트랜스코딩 서버가 구독한 오디오/비디오 스트림에 대해 혼합 스트림 트랜스코딩 처리를 수행할 때 혼합 스트림 트랜스코딩 요금이 발생합니다.

혼합 스트림 수에 따라 변경되지 않습니다. 예를 들어 사용자 A와 사용자 B의 비디오 스트림이 5분 동안 혼합 트랜스코딩 프로세스에서 혼합된 경우 과금 대상 혼합 트랜스코딩 시간은 5분이 되며 프로세스의 총 해상도에 따라 요금이 청구됩니다.

여러 혼합 트랜스코딩 프로세스가 한 방에서 시작되면 모든 프로세스의 지속 시간이 합산됩니다.

과금 공식:

**월간 혼합 트랜스코딩 요금** = **오디오 지속 시간** × **오디오 단가** + **카테고리별 비디오 길이** × **해당 카테고리의 단가**

>? 오디오 전용 스트림과 비디오 스트림을 동시에 혼합 트랜스코딩하면 비디오 트랜스코딩 요금만 과금됩니다.

#### 단가
TRTC 오디오/비디오 혼합 트랜스코딩 지속 시간의 단가는 다음과 같습니다.

<table>
     <tr>
         <th style="text-align:center">사용량</th>
         <th style="text-align:center">비디오 카테고리</th>
         <th style="text-align:center">단가(USD/1000분)</th>
 </tr>
     <tr>
         <td style="text-align:center">오디오</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">1.99</td>
 </tr>
  <tr>
         <td style="text-align:center" rowspan="4">H.264 비디오</td>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">5.99</td>
 </tr>
     <tr>
         <td style="text-align:center"> Full HD</td>
         <td style="text-align:center">13.99</td>
 </tr>
     <tr>
         <td style="text-align:center">2K</td>
         <td style="text-align:center">25.99</td>
 </tr>
     <tr>
         <td style="text-align:center">2K+</td>
         <td style="text-align:center">69.99</td>
  <tr>
  <tr>
         <td style="text-align:center" rowspan="4">H.265 비디오</td>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">17.99</td>
 </tr>
     <tr>
         <td style="text-align:center">Full HD</td>
         <td style="text-align:center">37.99</td>
 </tr>
     <tr>
         <td style="text-align:center">2K</td>
         <td style="text-align:center">69.99</td>
 </tr>
     <tr>
         <td style="text-align:center">2K+</td>
         <td style="text-align:center">189.99</td>
 </tr> 
</table>

혼합된 모든 비디오의 해상도 합계에 따라 TRTC는 비디오 혼합 트랜스코딩 지속 시간의 해상도를 다음 네 가지 범주로 분류합니다.

| 해상도      | 범위                                         |
| :---------------- | :----------------------------------------------------------- |
| HD        | 총 해상도 ≤ 921,600(1280 × 720)                           |
| Full HD | 921,600(1280 × 720)＜ 총 해상도 ≤ 2,073,600(1920 × 1080) |
| 2K                | 2,073,600 (1920 × 1080) ＜ 총 해상도 ≤ 3,686,400 (2560 × 1440) |
| 2K+               | 3,686,400 (2560 × 1440)＜ 총 해상도 ≤ 8,847,360 (4096 × 2160) |

예를 들어 혼합 트랜스코딩 프로세스가 2개의 960 × 720 비디오 스트림을 혼합하는 경우 총 해상도는 960 × 720 + 960 × 720 = 1,382,400이며 Full HD 범주에 속합니다.

#### 과금 예시
**오디오 라이브 스트리밍**

앵커는 오디오 전용 콘텐츠를 30분 동안 스트리밍한 다음 다른 사람과 30분 동안 공동 앵커링했습니다. 이 시간 동안 두 앵커의 스트림이 혼합되어 Tencent Cloud의 라이브 스트리밍 시스템에 게시되었습니다.

처음 30분 동안에는 앵커가 한 명만 있었기 때문에 혼합 트랜스코딩 요금이 과금되지 않았습니다. 그 후 30분 동안 두 명의 앵커가 오디오로 통신을 했기 때문에 오디오 혼합 트랜스코딩 요금이 과금됩니다.

혼합 트랜스코딩 요금 = 1.99 × 30/1,000 = 0.0597 USD

**비디오 라이브 스트리밍**

앵커 A는 1920 × 1080 해상도로 30분 동안 스트리밍된 비디오 콘텐츠를 10분 동안 앵커 B와 공동 앵커링했습니다. 앵커 B의 비디오 해상도는 1280 × 720이었습니다. 두 앵커의 스트림이 혼합되어 Tencent Cloud의 CSS 시스템에 게시되었습니다.

앵커 A의 경우 자신의 영상이 큰 이미지로 표시되고 앵커 B의 영상이 오른쪽 상단의 작은 창에 표시되었습니다. 앵커 A가 본 영상의 해상도는 1920 x 1080이었습니다. 앵커 B의 경우 큰 비디오 창에 자신의 영상이, 우측 상단의 작은 창에 앵커 A의 영상이 표시되었습니다. 앵커 B가 본 영상의 해상도는 1280 x 720이었습니다.

처음 30분 동안에는 앵커가 한 명만 있었기 때문에 혼합 트랜스코딩 요금이 과금되지 않습니다. 그 후 10분 동안 두 명의 앵커가 비디오를 통해 통신했고 두 개의 혼합 트랜스코딩 프로세스가 시작되었으며 별도로 요금이 과금됩니다. 두 프로세스의 총 해상도는 1920 x 1080 + 1280 x 720 = 2,995,200이었고 H.264 코덱이 사용되었으므로 H.264 2K 범주가 적용됩니다. 해당 비디오 카테고리는 출력 비디오의 해상도에 의해 결정되지 않습니다.

혼합 트랜스코딩 요금 = 25.99 x 10/1,000 + 25.99 x 10/1,000 = 0.5198 USD

### 릴레이 요금
Tencent Cloud의 CSS 시스템에 게시하는 경우 릴레이 요금을 청구하지 않습니다. 타사 플랫폼 또는 CDN에 게시하는 경우 사용된 대역폭에 따라 릴레이 요금이 과금됩니다.

과금 공식:

**릴레이 요금** = **월간 최대 대역폭** × **릴레이 단가**

#### 단가
TRTC 릴레이에 사용되는 대역폭의 단가는 다음과 같습니다.

| 사용량 | 가격(USD/Mbps/월) |
| :------- | :------------------- |
| 월간 최대 대역폭 | 18.99               |

#### 과금 예시
타사 플랫폼에 게시한 스트림의 비트 레이트가 500Kbps(오디오 비트 레이트와 비디오 비트 레이트의 합)이고 해당 일에 최대 10개의 릴레이 작업이 있었다고 가정합니다.
일일 최대 대역폭 = 500(Kbps) × 10 = 5,000(Kbps) = 5Mbps.

2022년 6월에 릴레이 기능을 사용했고 릴레이에 사용된 대역폭이 피크에서 5Mbps에 도달했다고 가정합니다.
2022년 6월 릴레이 요금 = 18.99(USD/Mbps/월) x 5(Mbps) = 94.95 USD.