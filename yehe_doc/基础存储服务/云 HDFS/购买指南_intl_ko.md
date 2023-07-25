
## 과금 개요


CHDFS는 후불 과금 방식을 제공합니다. 실제 사용한 스토리지 용량, 대역폭 크기에 따라 과금됩니다. 과금 항목 별로 결산 주기가 다릅니다.

## 과금 항목 설명

CHDFS의 과금 항목, 요금 설명 및 계산법은 다음과 같습니다.

<table>
   <tr>
      <th>과금 항목</th>
      <th>과금 항목 설명</th>
      <th>과금 계산법</th>
      <th>과금 관련 설명</th>
   </tr>
   <tr>
      <td>스토리지 용량 요금</td>
      <td>스토리지 용량을 기준으로 계산</td>
      <td nowrap>스토리지 용량 요금 = 스토리지 용량 단가 x 월간 스토리지 용량</td>
      <td nowrap>월간 스토리지 용량 = 당월 ‘일별 스토리지 용량’ 합계 / 당월 일수<br>일별 스토리지 용량 = 당일 ‘매 5분당 스토리지 용량’ 합계 / 288(샘플 카운팅)
			</td>
   </tr>
   <tr>
      <td>대역폭 요금</td>
      <td>대역폭을 기준으로 계산</td>
      <td nowrap>대역폭 요금 = 대역폭 단가 x 월간 대역폭 크기</td>
      <td >월간 대역폭 크기 = 월간 대역폭 피크 × 유효 일수 / 당월 일수<br>월간 대역폭 피크: 월 결산 시 5분마다 획득한 대역폭 피크를 높은 순으로 배열하고, 상위 5%를 제거한 대역폭 값이 월간 대역폭 피크입니다.</td>
   </tr>
</table>



## 제품 가격


<table>
   <tr>
      <th>과금 항목</th>
      <th>과금 주기</th>
      <th>과금 방식</th>
      <th>중국대륙 리전 가격</th>
      <th>중국홍콩 및 중국 외 리전 가격</th>
   </tr>
   <tr>
      <td>스토리지 용량 요금</td>
      <td>월</td>
      <td>후불</td>
      <td>0.03375USD/GB/월</td>
      <td>0.0484USD/GB/월</td>
   </tr>
   <tr>
      <td>대역폭 요금</td>
      <td>월</td>
      <td>후불</td>
      <td>0.0766USD/Mbps</td>
      <td>0.116USD/Mbps</td>
   </tr>
</table>


## 소비 내역 조회

1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com)에 로그인합니다.
2. 오른쪽 상단 사이드바의 **요금**에서 **과금 센터**를 클릭하여 과금 센터 전체보기 페이지로 이동합니다.
3. 왼쪽 메뉴에서 **요금 청구서**를 클릭합니다.
3. 드롭다운 메뉴에서 **청구서 내역**을 클릭하여 CHDFS 제품을 선택하고 CHDFS 리소스 ID 청구서와 청구 명세서를 조회합니다.


## 연체 및 서비스 중단


계정 연체 24시간 경과 시 CHDFS 서비스가 중단됩니다. 귀하의 데이터는 120일 동안 보관되며, 이 기간 내에 계정 잔액을 0 이상으로 충전하지 않으면 데이터는 폐기됩니다. 연체 통지 수신 후, 비즈니스에 지장이 없도록 콘솔의 [과금 센터](https://console.cloud.tencent.com/expense/recharge)로 이동하여 잔액을 충전하시기 바랍니다.

또한 과금 센터의 잔액 알림 기능을 통해 연체 알람을 설정할 수 있습니다.

>!If you are a customer of a Tencent Cloud partner, the rules regarding resources when there are overdue payments are subject to the agreement between you and the partner.