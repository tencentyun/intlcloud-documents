
## 과금 개요


CHDFS는 후불 과금 방식을 제공합니다. 실제 사용한 스토리지 용량, 검색량, 대역폭 크기에 따라 과금됩니다. 과금 항목 별로 결산 주기가 다릅니다.

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
      <td>스토리지 용량을 기준으로 <br>계산</td>
      <td nowrap>스토리지 용량 요금 = 스토리지 용량 단가 x 월간 스토리지 용량</td>
      <td nowrap>월간 스토리지 용량 = 당월 ‘일별 스토리지 용량’ 합계 / 당월 일수<br>일별 스토리지 용량 = 당일 ‘매 5분당 스토리지 용량’ 합계 / 288(샘플 카운팅)
			</td>
   </tr>
   <tr>
      <td>표준IA 스토리지 용량 요금</td>
      <td>표준IA 스토리지 용량을 기준으로 <br>계산</td>
      <td nowrap>표준IA 스토리지 용량 요금 = 표준IA 스토리지 용량 단가 x 월간 표준IA 스토리지 용량</td>
      <td nowrap>월간 표준IA 스토리지 용량 = 당월 ‘일별 표준IA 스토리지 용량’ 합계 / 당월 일수<br>일별 표준IA 스토리지 용량 = 당일 ‘매 5분당 표준IA 스토리지 용량’ 합계 / 288(샘플 카운팅)
			</td>
   </tr>
   <tr>
      <td>CAS 용량 요금</td>
      <td>CAS 용량을 기준으로 <br>계산</td>
      <td nowrap>CAS 용량 요금 = CAS 용량 단가 x 월간 CAS 용량</td>
      <td nowrap>월간 CAS 용량 = 당월 ‘일별 CAS 용량’ 합계 / 당월 일수<br>일별 CAS 용량 = 당일 ‘매 5분당 CAS 용량’ 합계 / 288(샘플 카운팅)
			</td>
   </tr>
   <tr>
      <td>DEEP ARCHIVE 용량 요금</td>
      <td>DEEP ARCHIVE 용량을 기준으로 <br>계산</td>
      <td nowrap>DEEP ARCHIVE 용량 요금 = DEEP ARCHIVE 용량 단가 x 월간 DEEP ARCHIVE 용량</td>
      <td nowrap>월간 DEEP ARCHIVE 용량 = 당월 ‘일별 DEEP ARCHIVE 용량’ 합계 / 당월 일수<br>일별 DEEP ARCHIVE 용량 = 당일 ‘매 5분당 DEEP ARCHIVE 용량’ 합계 / 288(샘플 카운팅)
			</td>
   </tr>
   <tr>
      <td>표준IA 스토리지 검색량 요금</td>
      <td>표준IA 스토리지 검색량을 기준으로 <br>계산</td>
      <td nowrap>표준IA 스토리지 검색량 요금 = 표준IA 스토리지 검색량 단가 x 표준IA 스토리지 용량</td>
      <td nowrap>표준IA 스토리지 검색량 = 다운로드된 표준IA 스토리지 파일 크기
			</td>
   </tr>
   <tr>
      <td>CAS 검색량 요금</td>
      <td>CAS 검색량을 기준으로 <br>계산</td>
      <td nowrap>CAS 검색량 요금 = CAS 검색량 단가 x CAS 용량</td>
      <td nowrap>CAS 검색량 = 다운로드된 CAS 파일 크기
			</td>
   </tr>
   <tr>
      <td>DEEP ARCHIVE 검색량 요금</td>
      <td>DEEP ARCHIVE 검색량을 기준으로 <br>계산</td>
      <td nowrap>DEEP ARCHIVE 검색량 요금 = DEEP ARCHIVE 검색량 단가 x DEEP ARCHIVE 용량</td>
      <td nowrap>DEEP ARCHIVE 검색량 = 다운로드된 DEEP ARCHIVE 파일 크기
			</td>
   </tr>
   <tr>
      <td>대역폭 요금</td>
      <td>대역폭을 기준으로 <br>계산</td>
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
      <td>표준IA 스토리지 용량 요금</td>
      <td>월</td>
      <td>후불</td>
      <td>0.01875USD/GB/월</td>
      <td>0.025USD/GB/월</td>
   </tr>
   <tr>
      <td>CAS 용량 요금</td>
      <td>월</td>
      <td>후불</td>
      <td>0.0105USD/GB/월</td>
      <td>0.013USD/GB/월</td>
   </tr>
   <tr>
      <td>DEEP ARCHIVE 용량 요금</td>
      <td>월</td>
      <td>후불</td>
      <td>0.00234USD/GB/월</td>
      <td>0.002813USD/GB/월</td>
   </tr>
   <tr>
      <td>표준IA 스토리지 검색량 요금</td>
      <td>일</td>
      <td>후불</td>
      <td>0.004375USD/GB</td>
      <td>0.00625USD/GB</td>
   </tr>
   <tr>
      <td>CAS 검색량 요금</td>
      <td>일</td>
      <td>후불</td>
      <td>0.04USD/GB</td>
      <td>0.05USD/GB</td>
   </tr>
   <tr>
      <td>DEEP ARCHIVE 검색량 요금</td>
      <td>일</td>
      <td>후불</td>
      <td>0.028USD/GB</td>
      <td>0.0328USD/GB</td>
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
2. 오른쪽 상단 메뉴의 [요금]에서 [과금 센터]를 클릭하여 과금 센터 총람 페이지로 이동합니다.
3. 왼쪽 메뉴에서 [요금 청구서]를 클릭합니다.
3. 드롭다운 메뉴에서 [청구서 내역]을 클릭한 뒤 CHDFS 제품을 선택하여 CHDFS 리소스 ID 청구서와 청구 명세서를 조회합니다.


## 연체 및 서비스 중단


계정 연체 24시간 경과 시 CHDFS 서비스가 중단됩니다. 귀하의 데이터는 120일 동안 보관되며, 이 기간 내에 계정 잔액을 0 이상으로 충전하지 않으면 데이터는 파기됩니다. 연체 통지 수신 후, 비즈니스에 지장이 없도록 콘솔의 [과금 센터](https://console.cloud.tencent.com/expense/recharge)로 이동하여 잔액을 충전하시기 바랍니다.

또한 과금 센터의 잔액 알림 기능을 통해 연체 알람을 설정할 수 있습니다.

