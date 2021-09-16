>!본 문서는 TRTC의 저지연 라이브 방송 방의 과금에 대한 설명입니다. TRTC 방의 오디오 스트림을 CSS 시스템에 릴레이하여 시청자들이 라이브 방송 CDN을 통해 시청하게 되면 추가 요금이 발생합니다. 자세한 내용은 [CDN 라이브 방송 시청 실행> 관련 비용](https://intl.cloud.tencent.com/document/product/647/35242)을 참고하십시오.

[](id:Billing_items)
## 사용량 통계 방식

TRTC는 [방](https://intl.cloud.tencent.com/document/product/647/37714) 안의 사용자로 인해 발생한 모든 **음성 시간**을 음성 ILVB 서비스 사용량으로 통계합니다.


- TRTC 방 체류 시간은 사용자의 음성 시간으로 집계됩니다.
- 사용자가 TRTC 방에 입장한 후부터 요금이 부과됩니다. 방에 혼자 있더라도 음성 시간으로 집계됩니다.
- 동일한 방에는 자유롭게 입/퇴장할 수 있습니다. 입/퇴장 시 TRTC에서 실시간으로 음성 시간을 통계하여 합산합니다.

>!음성 시간은 초 단위로 통계되며, 당월 누적 시간은 초에서 분으로 전환 후 과금됩니다. 1분 미만일 경우 1분으로 계산합니다.

[](id:Fixed_price)
## 서비스 가격

음성 ILVB 서비스의 정가는 다음과 같습니다.

|과금 유형|단가(USD/1,000분)|
|---|---|
|음성|0.99|

[](id:Billing_method)
## 과금 방식
TRTC 결제 방식은 **선불 패키지**와 **후불 결제**가 있으며 선불 패키지로 기본 설정되어있습니다. 후불 결제 활성화는 [문서](https://intl.cloud.tencent.com/document/product/647/41979)를 참고하십시오.

[](id:pre-payment)

### 선불 패키지

범용 패키지는 **1:1**로 음성 시간을 차감합니다. 예를 들어, 음성 시간을 1분 사용하면 범용 패키지에서 1분이 차감됩니다.
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
   예를 들어, 2021년 05월 01일 구매한 패키지의 유효 기간은 2021년 05월 01일~2022년 05월 31일입니다. 범용 패키지의 유효 기간은 구매 당일~다음 해 당월 말일까지입니다.
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
>- 결산 주기는 임의로 변경할 수 없습니다. 월 결산을 일 결산으로 변경하려면 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 도움을 요청하십시오.
>- 계정 잔액이 부족하여 요금을 차감할 수 없는 경우, 사용 중인 다른 Tencent Cloud 서비스도 자동 중단됩니다. 예를 들어 클라우드 녹화는 **CSS**와 **VOD**에 종속되므로, Tencent Cloud 계정의 요금 연체가 발생할 경우 클라우드 녹화 서비스도 중단됩니다.


[](id:Billing_examples)
## 과금 예시
>!본 문서의 과금 예시는 정가 기준이며, [패키지 구매](https://buy.cloud.tencent.com/trtc)를 통해 비용을 절약할 수 있습니다.

사용자 A, B, C가 TRTC 방에 30분 체류했고, 모두 영상 화면을 수신하지 않은 경우, 음성 사용 시간을 기준으로 과금됩니다.

#### 분석:
-**음성 사용 시간 과금 = 음성 단가 × 모든 사용자의 음성 시간의 합**
- 해당 TRTC 방에 발생한 음성 시간의 **총 요금**은 `음성 시간 단가 × 모든 사용자의 음성 시간 길이의 합 = 0.99USD/1,000분 × (30분 + 30분 + 30분) / 1000 = 0.0891USD`입니다.



[](id:estimate)
## 예상 사용량 및 요금
예상 사용량과 요금은 [TRTC 가격 계산기](https://buy.intl.cloud.tencent.com/pricing/trtc)로 계산할 수 있습니다.
1. 서비스 상황에 따라 **음성 ILVB, 비디오 ILVB 예상 사용량**에 **평균 방 개수/일**, **평균 호스트 수/방**, **평균 시청자 수/방** 및 **회당 평균 라이브 방송 시간/방**을 입력합니다.
2. 사용 유형 **음성**을 선택하면 **월간 예상 사용량**을 계산할 수 있습니다.
![](https://main.qcloudimg.com/raw/871d7e1d43e83674f82a3960a079ff7c.png)
3. **예상 요금**에서 **범용 패키지 사용량**, 후불 방식 및 선불 방식에 따른 예상 요금을 볼 수 있습니다.
![](https://main.qcloudimg.com/raw/871d7e1d43e83674f82a3960a079ff7c.png)


## 관련 문서
- [과금 개요](https://intl.cloud.tencent.com/document/product/647/34610)
- [무료 베타 테스트](https://intl.cloud.tencent.com/document/product/647/39784)
- [비디오 ILVB 과금 설명](https://intl.cloud.tencent.com/document/product/647/39786)
- [음성 통화 과금 설명](https://intl.cloud.tencent.com/document/product/647/39787)
- [영상 통화 과금 설명](https://intl.cloud.tencent.com/document/product/647/39788)
- [클라우드 녹화 과금 설명](https://intl.cloud.tencent.com/document/product/647/38385)
- [클라우드 혼합 스트림 트랜스 코딩 과금 설명](https://intl.cloud.tencent.com/document/product/647/38929)
- [구매 가이드](https://intl.cloud.tencent.com/document/product/647/35440)
- [과금 FAQ](https://intl.cloud.tencent.com/document/product/647/39789)
