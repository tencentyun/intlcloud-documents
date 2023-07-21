MAZ_STANDARD_IA, STANDARD_IA, ARCHIVE 또는 DEEP ARCHIVE 스토리지 클래스에 저장된 데이터를 검색하면 검색된 데이터의 크기에 따라 청구되는 데이터 검색 요금이 발생합니다.

>?스토리지 유형에 대한 더 자세한 소개는 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오.
> 


## MAZ_STANDARD_IA/STANDARD_IA 데이터 검색 요금

| 과금 항목 설명       | 적용 스토리지 유형           | 적용 과금 방식               |
| ----------------------- | --------------- |------------------- |
| MAZ_STANDARD_IA 또는 STANDARD_IA에 저장된 데이터는 복원된 후에만 읽기/다운로드할 수 있습니다. 데이터 검색 비용은 객체의 크기에 따라 계산됩니다.                           |      MAZ_STANDARD_IA</br>STANDARD_IA                             |      종량제     |

## ARCHIVE/DEEP ARCHIVE 데이터 검색 요금

| 과금 항목 설명       | 적용 스토리지 유형           | 적용 과금 방식               |
| ----------------------- | --------------- |------------------- |
|         ARCHIVE/DEEP ARCHIVE에 저장된 데이터는 STANDARD 스토리지 클래스로 복구(즉, STANDARD에서 복사본 생성)한 후에만 읽기/다운로드할 수 있습니다. </br></br>다른 스토리지 클래스 및 복구 모드에 대해 다음 요금이 발생할 수 있습니다.<ul style="margin: 0;"><li>ARCHIVE 데이터 검색 요금(고속)</li><li>ARCHIVE 데이터 검색 요금(표준)</li><li>ARCHIVE 데이터 검색 요금(대량)</li><li>DEEP ARCHIVE 데이터 검색 요금(표준)</li><li>DEEP ARCHIVE 데이터 검색 요금(대량)</li></ul>          |       ARCHIVE</br>DEEP ARCHIVE                            |      종량제   |


## 데이터 검색 요금의 과금 방식 및 계산 방법

<table>
   <tr>
      <th>과금 방식</td>
      <th>적용 과금 항목</td>
      <th>계산 방법 </td>
   </tr>
   <tr>
      <td rowspan=1>종량제</td>
      <td><ul style="margin: 0;"><li>STANDARD IA 스토리지(다중AZ) 데이터 검색</li><li>STANDARD IA 스토리지 데이터 검색</li><li>ARCHIVE 데이터 검색</li><li>DEEP ARCHIVE 데이터 검색</li></ul></td>
      <td><ul style="margin: 0;"><li>일 결산</li><li>데이터 검색 요금 = GB당 단가 x 일 데이터 검색량</li></ul></td>
   </tr>
</table>


## 데이터 검색 가격

각 스토리지 유형의 데이터 검색 단가는 [가격](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)을 참고하십시오.




## 과금 사례

>?
> - 다음 예시의 가격은 참고용입니다. 실제 가격은 COS [가격](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)을 참고하십시오.
> - 스토리지 용량은 이진법으로 계산합니다(예시 1TB = 1,024GB).
> 

### 사례: STANDARD_IA 스토리지 용량 요금 + STANDARD_IA 스토리지 데이터 검색 요금 + STANDARD_IA 스토리지 요청 요금 + 공중망 다운스트림 트래픽 요금

2020년 11월 1일에 사용자 B가 STANDARD_IA 스토리지 클래스의 광저우 리전에 있는 버킷에 5GB의 데이터를 업로드하여 100회의 요청을 생성하였으며, 11월 2일에 사용자 B는 CDN이 비활성화된 공중망을 통해 데이터를 읽고 100회의 요청을 생성했고, 이러한 작업 외에 다른 작업을 수행하지 않았다고 가정할 때, 전일 발생 요금을 일 단위로 정산하면 다음과 같습니다.

- STANDARD_IA 스토리지 사용 요금: 2020년 11월 2일부터 매일 정산됩니다.
- STANDARD_IA 데이터 검색 요금: 2020년 11월 2일에 정산됩니다.
- STANDARD_IA 요청 요금: 2020년 11월 2일 및 3일에 정산됩니다.
- 공중망 다운스트림 트래픽 요금: 2020년 11월 3일에 정산됩니다.

데이터 검색에 사용할 수 있는 리소스 패키지가 없으므로 종량제 과금 방식을 기반으로 다음과 같이 분석할 수 있습니다.

종량제:
 - STANDARD_IA 스토리지 용량 요금 = 0.018USD/GB/월 /30 x 5GB x 30일 = 0.09 USD
 - STANDARD_IA 스토리지 데이터 검색 요금 = 0.002USD/GB x 5GB = 0.01USD
 - STANDARD_IA 스토리지 요청 요금 = 0.01USD/1만 회 x 100회 / 10000 x 2 = 0.0002 USD
 - 공중망 다운스트림 트래픽 요금 = 0.1USD/GB x 5GB = 0.5USD

위 금액을 모두 합산하면 전체 11월 사용자 B의 총 요금은 0.09 + 0.01 + 0.0002 + 0.5 = 0.6002 USD입니다.

