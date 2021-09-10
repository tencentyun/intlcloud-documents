<style>.markdown-text-box table td, .markdown-text-box table th {text-align: center;}
.tablestyle{position:absolute;width:1px;height:160px;top:0;left:0;background-color: #d9d9d9;transform:rotate(-69deg);transform-origin:top;}
.th1{position:absolute;right:20px;top:10px;}
.th2{position:absolute;right:80px;top:30px)
</style>


[](id:Billing_items)
## 사용량 통계 방식
TRTC에서는 [방](https://intl.cloud.tencent.com/document/product/647/37714) 안의 사용자로 인해 발생한 모든 [비디오 시간](#v_duration)과 [음성 시간](#s_duration)을 영상 통화 서비스 사용량으로 통계합니다.

>!시간은 초 단위로 통계되며, 당월 누적 시간은 초에서 분으로 전환 후 과금됩니다. 1분 미만일 경우 1분으로 계산합니다.

[](id:v_duration)
### 비디오 시간
비디오 시간은 사용자가 TRTC 방에 입장하여 멀티미디어 스트림을 구독하고 비디오 화면을 수신한 시간입니다. TRTC에서는 사용자가 **실제 수신한 비디오 해상도**에 따라 비디오 등급을 분류하고, 각 비디오 등급의 사용 시간에 따라 과금합니다.
비디오 등급과 그에 해당하는 해상도는 다음과 같습니다.

|비디오 등급|실제 수신 해상도|
|-------|--------|
|SD|640 × 480 이하(포함)|
|HD|640 × 480 ~ 1280 × 720(포함)|
|HD+|1280 × 720 초과|

- 비디오를 구독할 경우 오디오 포함 여부와 관계없이 비디오 시간만 통계하므로, 음성 시간이 중복으로 통계되지 않습니다.
- 단일 사용자가 여러 채널의 비디오를 동시에 구독할 경우, 각각의 비디오 시간을 통계한 후 합산합니다.
- TRTC 전체 플랫폼의 SDK는 비디오 해상도를 제한하지 않습니다. 실제 필요에 따라 직접 [화면 품질 설정](https://intl.cloud.tencent.com/document/product/647/35153)을 변경할 수 있습니다.


[](id:s_duration)
### 음성 시간
영상 통화 시나리오의 음성 시간 = 사용자가 TRTC 방에서 체류한 총 시간 - 비디오 화면을 수신한 체류 시간
사용자가 00:00에 TRTC 방에 입장하여 00:50에 퇴장한 경우, 방 체류 시간은 아래와 같습니다.
![](https://main.qcloudimg.com/raw/b127abe248a205842a6216ccbd7c111e.png)
그림에서 파란색으로 표시된 부분이 사용자의 음성 이용 시간입니다(`총 체류 시간 - 비디오 화면을 수신한 체류 시간 = 50분 - 15분 = 35분`).


- 사용자가 비디오를 구독하지 않은 경우, 음성 시간만 통계됩니다.
- 사용자가 TRTC 방에 입장 후 비디오를 구독하지 않으면 푸시 스트림이 업스트림되지 않아도 음성 시간이 통계됩니다.
- 동일한 방에는 자유롭게 입/퇴장할 수 있습니다. 입/퇴장 시 TRTC에서 실시간으로 음성 시간을 통계하여 합산합니다.


[](id:Fixed_price)
## 서비스 가격

비디오 ILVB 서비스의 정가는 다음과 같습니다.

| 과금 항목   |단가(USD/1,000분)|
| -------- | ------------------- |
| 음성     | 0.99                |
|SD  | 1.99                |
|HD  | 3.99                |
|HD+ | 14.99               |

[](id:Billing_method)

## 과금 방식
TRTC 결제 방식은 **선불 패키지**와 **후불 결제**가 있으며 선불 패키지로 기본 설정되어있습니다. 후불 결제 활성화는 [문서](https://intl.cloud.tencent.com/document/product/647/41979)를 참고하십시오.



[](id:pre-payment)
### 선불 패키지

TRTC는 멀티미디어 범용 패키지를 제공합니다. 음성, SD, HD, HD+의 사용 시간에 따라 **1:2:4:15**로 시간이 차감됩니다. 예를 들어 HD 비디오 시간이 1분이면 범용 패키지에서 4분이 차감됩니다.
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
         <td style="text-align:center"><97%</td>     
     </tr> 
     <tr>
         <td style="text-align:center">250 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center">227</td>   
         <td style="text-align:center"><92%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center">856</td>   
         <td style="text-align:center"><87%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">2416</td>   
         <td style="text-align:center"><82%</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="5">사용자 정의 패키지</td>   
         <td style="text-align:center">0 < T < 25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center" rowspan="5">패키지 단가*패키지 시간 T</td>   
         <td style="text-align:center">100%</td>    
     </tr> 
     <tr>
         <td style="text-align:center">25 ≤ T < 250</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center"><97%</td>    
     </tr> 
     <tr>
         <td style="text-align:center">250 ≤ T < 1000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center"><92%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 ≤ T < 3000</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center"><87%</td>   
     </tr> 
     <tr> 
         <td style="text-align:center">T ≥ 3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center"><82%</td>   
     </tr> 
</table>



>?표의 패키지 단가는 1,000분당 단가를 기준으로 소수점 셋째 자리까지 계산된 것이며, 실제 요금은 분당 단가를 기준으로 소수점 여덟째 자리까지 계산됩니다.

범용 패키지 설명:

- 범용 패키지의 유효 기간은 구매 당일~다음 해 당월 말일까지입니다.
 예를 들어, 2020년 05월 01일 구매한 패키지의 유효 기간은 2020년 05월 01일 ~ 2021년 05월 31일입니다.
- 범용 패키지는 중복 구매가 가능합니다. 각 유형의 사용 시간에 따라 범용 패키지 시간이 실시간으로 차감되며, 기간 만료일이 가까운 패키지가 우선 차감됩니다.
- 패키지를 새로 구매하면 결제 완료 후 약 5분 내에 적용됩니다. **새 패키지 적용 즉시 당일 0시 이후 다른 패키지에서 미차감된 사용량을 차감합니다**.
- 사용자의 원활한 온라인 비즈니스를 위해 **범용 패키지를 모두 사용하거나 기간이 만료되어도 서비스가 자동으로 중단되지 않습니다.** 패키지 사용량을 초과하면 [후불](#post-payment) 과금 방식을 적용합니다.
- 모든 범용 패키지는 유효 기간이 만료되면 잔여 시간이 자동으로 삭제되며 복구할 수 없습니다.


[](id:post-payment)
### 후불
서비스 사용량을 차감할 수 있는 패키지가 없거나 패키지 한도를 초과한 경우, 후불 방식이 적용되고 [정가](#Fixed_price)에 따라 과금됩니다.
TRTC 후불 방식에는 [일 결산](#daily)과 [월 결산](#monthly)이 있습니다.


[](id:daily)
#### 일 결산 후불
2020년 09월 01일 이후 TRTC 콘솔에서 처음으로 [애플리케이션](https://intl.cloud.tencent.com/document/product/647/37714)을 생성한 사용자의 경우, 후불이 적용되고 기본적으로 **일 결산** 방식으로 요금이 부과됩니다. 일별 과금되며, 전날 발생한 비용은 매일 오전 10시에 차감됩니다.


[](id:monthly)
#### 월 결산 후불
2020년 08월 31일 이전에 TRTC 콘솔에서 처음으로 [애플리케이션](https://intl.cloud.tencent.com/document/product/647/37714)을 생성한 사용자의 경우, 후불이 적용되고 기본적으로 **월 결산** 방식으로 요금이 부과됩니다. 매월 1일~5일에 계정 잔액에서 전월 발생한 요금을 차감합니다. 상세 내역은 [요금 청구서](https://intl.cloud.tencent.com/document/product/555/7432)를 참고하십시오.
>!
>- 결산 주기는 임의로 변경할 수 없습니다. 월 결산을 일 결산으로 변경하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 도움을 요청하십시오.
>- 계정 잔액이 부족하여 요금을 차감할 수 없는 경우, 사용 중인 다른 Tencent Cloud 서비스도 자동 중단됩니다. 예를 들어 클라우드 녹화는 **CSS**와 **VOD**에 종속되므로, Tencent Cloud 계정의 요금 연체가 발생할 경우 클라우드 녹화 서비스도 중단됩니다.


[](id:Billing_examples)
## 과금 예시
>!본 문서의 과금 예시는 정가 기준이며, [패키지 구매](https://buy.cloud.tencent.com/trtc)를 통해 비용을 절약할 수 있습니다.

### 음성 단독 사용 예시

사용자 A, B, C가 TRTC 방에 30분 체류했고, 모두 영상 화면을 수신하지 않은 경우, 음성 사용 시간을 기준으로 과금됩니다.

#### 분석:
- **음성 사용 시간 과금 = 음성 단가 × 모든 사용자의 음성 시간의 합**

- 해당 TRTC 방에 발생한 음성 시간의 **총 요금**은 `음성 시간 단가 × 모든 사용자의 음성 시간 길이의 합 = 0.99USD/1,000분 × (30분 + 30분 + 30분) / 1000 = 0.0891USD`입니다.

### 음성/영상 혼합 사용 예시

사용자 A, B, C가 TRTC 방에서 30분 체류했고, A, B, C가 다음 표와 같이 서로의 멀티미디어 스트림을 구독한 경우의 예시입니다.

<table style="width:715px;">
<style>.markdown-text-box table td, .markdown-text-box table th {text-align: center;}
.tablestyle{position:absolute;width:1px;height:160px;top:0;left:0;background-color: #d9d9d9;transform:rotate(-69deg);transform-origin:top;}
.th1{position:absolute;right:20px;top:10px;}
.th2{position:absolute;right:80px;top:30px)
</style>
<tr>
<th style ="position:relative;width:150px" >
  <div class="tablestyle"></div>
  <div class="th1">발신자</div>
  <div class="th2">수신자</div></th>
  <th>A<br>640 × 360(SD)</th>
  <th>B<br>퓨어 오디오</th>
  <th>C<br>1920 × 1080(HD+)</th>
</tr><tr>
  <td>A</td>
  <td>-</td>
  <td>&#10003;</td>
  <td>&#10003;</td>
</tr><tr>
  <td>B</td>
  <td>&#10003;</td>
  <td>-</td>
  <td>&#10003;</td>
</tr><tr>
  <td>C</td>
  <td>&#10003;</td>
  <td>&#10003;</td>
  <td>-</td>
</tr></table>
#### 분석:

- A의 사용량과 요금:
  - **A의 요금 = A가 B를 수신하여 발생된 요금 + A가 C를 수신하여 발생된 요금**
  - A가 B를 수신하여 발생된 요금 = 음성 단가 × 음성 길이 = 0.99 USD/1,000분 × (30분/1000) = 0.0297 USD
  - A가 C를 수신하여 발생된 요금 = HD+ 영상 단가 × HD+ 영상 길이 = 14.99USD / 1000분 × (30분 / 1000) = 0.4497USD
  - A의 요금 = B 수신 요금 + C 수신 요금 = 0.0297 + 0.4497 = 0.4794 USD
- B의 사용량과 요금:
  - **B의 요금 = B가 A를 수신하여 발생된 요금 + B가 C를 수신하여 발생된 요금**
  - B가 A를 수신하여 발생된 요금 = SD 영상 단가 × SD 길이 = 1.99USD/1000분 × (30분 / 1000) = 0.0597 USD
  - B가 C를 수신하여 발생된 요금 = HD+ 단가 × HD+ 길이 = 14.99USD / 1000분 × (30분 / 1000) = 0.4497USD
  - B의 요금 = A 수신 요금 + C 수신 요금 = 0.0597 + 0.4497= 0.5094 USD

- C의 사용량과 요금:
  -  **C의 요금 = C가 A를 수신하여 발생된 요금 + C가 B를 수신하여 발생된 요금**
  -  C가 A를 수신하여 발생된 요금 = SD 영상 단가 × SD 길이 = 1.99USD/1000분 × (30분 / 1000) = 0.0597 USD
  -  C가 B를 수신하여 발생된 요금 = 음성 단가 × 음성 길이 = 0.99USD/1000분 × (30분 / 1000）= 0.0297 USD
  -  C의 요금 = A 수신 요금 + B 수신 요금 = 0.0597 + 0.0297 =0.0894 USD

해당 TRTC 방에서 발생한 **총 요금**은 `사용자 A의 요금 +사용자 B의 요금 +사용자 C의 요금= 1.0782USD`입니다.

[](id:estimate)
## 예상 사용량 및 요금
예상 사용량과 요금은 [TRTC 가격 계산기](https://buy.intl.cloud.tencent.com/pricing/trtc)로 계산할 수 있습니다.
1. 서비스 상황에 따라 **음성 통화, 영상 통화 예상 사용량**에 **일평균 통화 횟수**, **회당 평균 통화 인원**, **인당 평균 통화 시간**을 입력합니다.
2. 사용 유형 **'SD'**, **'HD'** 또는 **'HD+'**를 선택하면 **월간 예상 사용량**을 계산할 수 있습니다.
![](https://main.qcloudimg.com/raw/8a3841e796aeca8e8a3a13c396dd4ae5.png)
3. **예상 요금**에서 **범용 패키지 사용량**, 후불 방식 및 선불 방식에 따른 예상 요금을 볼 수 있습니다.
![](https://main.qcloudimg.com/raw/e910b8adc33df978a533b8aaa0cf91b6.png)



## 관련 문서
- [과금 개요](https://intl.cloud.tencent.com/document/product/647/34610)
- [무료 베타 테스트](https://intl.cloud.tencent.com/document/product/647/39784)
- [음성 ILVB 과금 설명](https://intl.cloud.tencent.com/document/product/647/39785)
- [비디오 ILVB 과금 설명](https://intl.cloud.tencent.com/document/product/647/39786)
- [음성 통화 과금 설명](https://intl.cloud.tencent.com/document/product/647/39787)
- [클라우드 녹화 과금 설명](https://intl.cloud.tencent.com/document/product/647/38385)
- [클라우드 혼합 스트림 트랜스 코딩 과금 설명](https://intl.cloud.tencent.com/document/product/647/38929)
- [구매 가이드](https://intl.cloud.tencent.com/document/product/647/35440)
- [과금 FAQ](https://intl.cloud.tencent.com/document/product/647/39789)
