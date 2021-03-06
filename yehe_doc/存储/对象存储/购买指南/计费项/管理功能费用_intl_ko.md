관리 기능 비용이란 사용자가 관리 기능(리스트 또는 인덱스 기능)을 활성화한 후 사용하면서 발생하는 금액입니다.

>?
>- 관리 기능 단가는 [제품 가격](https://buy.cloud.tencent.com/price/cos)을 참조하십시오.
>- 스토리지 유형에 대한 자세한 소개는 [스토리지 유형 개요](https://cloud.tencent.com/document/product/436/33417)를 참조하십시오.
>



<table>
<thead>
<tr>
<th>과금 항목</th>
<th>적용 스토리지 유형</th>
<th>과금 항목 설명</th>
<th>과금 방식</th>
</tr>
</thead>
<tbody><tr>
<td>리스트 기능 비용</td>
<td nowrap="nowrap">스토리지 유형과 별개</td>
<td>사용자가 리스트 기능을 활성화한 후 버킷 객체 리스트를 나열할 때 발생하는 금액</td>
<td>종량제</li></td>
</tr>
<tr>
<td >인덱스 기능 비용</td>
<td>표준 스토리지<br>표준IA 스토리지</td>
<td>사용자가 인덱스 기능을 활성화한 후 객체를 스캔할 때 발생하는 금액</td>
<td>종량제</td>
</tr>
<tr>
<td>일괄 프로세스 비용</td>
<td nowrap="nowrap">스토리지 유형과 별개</td>
<td>사용자가 일괄 프로세스 기능을 활성화하면 COS가 생성된 작업 수와 객체 처리량에 따라 청구</td>
<td>종량제</td>
</tr>
<tr>
<td>객체 태그 비용</td>
<td nowrap="nowrap">스토리지 유형과 별개</td>
<td>사용자가 객체 태그 기능을 활성화하면 COS가 객체 태그 수에 따라 청구</td>
<td>종량제</td>
</tr>
</tbody></table>



## 관리 기능 비용의 과금 방식 및 계산 방법

<table>
   <tr>
      <th>과금 방식</th>
      <th>과금 항목</th>
      <th>과금 방식</th>
   </tr>
   <tr>
      <td rowspan=4>종량제</td>
      <td>리스트 기능 비용</td>
      <td nowrap="nowrap"><li>일 결산<br><li>리스트 기능 비용 = 나열된 객체 수/1백만 x 단가</td>
   </tr>
   <tr>
      <td>인덱스 기능 비용</td>
      <td nowrap="nowrap"><li>일 결산<br><li>인덱스 기능 비용 = GB당 단가 x 일 누적 데이터 인덱스 수</td>
   </tr>
   <tr>
      <td>일괄 프로세스 비용</td>
			<td nowrap="nowrap">일괄 프로세스 비용에는 작업 비용과 객체 처리 비용이 포함됩니다.<li>일 결산<br><li>작업 비용 = 생성한 작업 수 x 단가<br><li>객체 처리 비용 = 객체 처리 1만 개당 x 단가</td>
   </tr>
   <tr>
      <td>객체 태그 비용</td>
			<td nowrap="nowrap"><li>일 결산<br><li>객체 태그 비용 = 태그 1만 개당 * 단가</td>
   </tr>
</table>

## 과금 사례

>? 다음 사례의 가격은 참고용이며, 실제 가격은 COS [제품 가격](https://buy.cloud.tencent.com/price/cos)을 참조하십시오.
>


### 사례: 표준 스토리지 용량 비용 + 객체 태그 비용 + 요청 비용

사용자 A가 2020년 11월 1일 표준 스토리지 유형의 10GB 데이터를 광저우 리전의 COS 버킷에 업로드하고, 당일 10만 개의 객체에 태그를 일괄 추가했으며, 10만 번의 요청이 발생했고, 다른 시간에는 아무 작업도 하지 않았다고 가정합니다. 이 경우 스토리지 용량 비용, 요청 비용은 월 결산되고 객체 태그 비용은 일 결산됩니다. 이에 따라 2020년 11월 2일 객체 태그 비용이 결산되며 2020년 12월 1일 스토리지 용량 비용과 표준 스토리지 요청 비용이 결산됩니다. 종량제 방식에 따른 비용 분석은 다음과 같습니다.

- 종량제:
 - 표준 스토리지 용량 비용 = 0.024USD/GB/월 x 10GB = 0.24USD
 - 객체 태그 비용 = 0.01USD/태그 1만 개당 x 객체 10만 개 = 0.1USD
 - 표준 스토리지 요청 비용 = 0.002USD/1만 회 x 10만 회 = 0.02USD

위 금액을 모두 합산하면 전체 11월 사용자 A의 총 요금은 0.24 + 0.1 + 0.02 = 0.36USD입니다.