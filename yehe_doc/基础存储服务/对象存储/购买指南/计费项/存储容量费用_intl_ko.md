스토리지 사용량은 사용된 스토리지 용량을 나타냅니다. 객체의 크기와 보관 기간에 따라 요금이 부과됩니다. 스토리지 클래스에 따라 단가, 최소 객체 크기, 최소 저장 기간이 아래와 같이 다릅니다. 실제 요금은 객체의 사용 사례 및 스토리지 클래스에 따라 다릅니다.

>? 스토리지 유형에 대한 더 자세한 소개는 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오.
>


## 스토리지 사용 요금


### STANDARD 스토리지 사용 요금     

<table>
<thead>
<tr><th style="width: 64%;">과금 항목 설명</th><th style="width: 16%;">적용 가능한 리전</th><th style="width: 20%;">적용 가능한 과금 방식</th></tr>
</thead>
<tbody>
<tr>
<td>STANDARD 스토리지 사용량은 STANDARD 스토리지 클래스에 저장된 데이터의 크기를 나타냅니다. 실제 STANDARD 스토리지 사용량과 데이터 저장 기간에 따라 요금이 청구됩니다.</td>
<td>전체 리전</td>
<td>종량제<br>STANDARD 스토리지 패키지</td>
</tr>
</tbody></table>


### MAZ_STANDARD 스토리지 사용 요금    

<table>
<thead>
<tr><th style="width: 64%;">과금 항목 설명</th><th style="width: 16%;">적용 가능한 리전</th><th style="width: 20%;">적용 가능한 과금 방식</th></tr>
</thead>
<tbody><tr>
<td>MAZ_STANDARD 스토리지 사용량은 MAZ_STANDARD 스토리지 클래스에 저장된 데이터의 크기를 나타냅니다. 실제 MAZ_STANDARD 스토리지 사용량과 데이터 저장 기간에 따라 요금이 청구됩니다.</td>
<td>베이징, 상하이, 광저우</td>
<td>종량제</td>
</tr>
</tbody></table>


### STANDARD_IA 스토리지 사용 요금  

<table>
<thead>
<tr><th style="width: 64%;">과금 항목 설명</th><th style="width: 16%;">적용 가능한 리전</th><th style="width: 20%;">적용 가능한 과금 방식</th></tr>
</thead>
<tbody>
<tr>
<td>STANDARD_IA 스토리지 사용량은 STANDARD_IA 스토리지 클래스에 저장된 데이터의 크기를 나타냅니다. 실제 사용 사례에 따라 요금이 청구됩니다. <ul  style="margin: 0;"><li>30일 미만으로 저장된 객체는 30일로 계산됩니다. 64KB보다 작은 단일 객체는 64KB로 계산되는 반면 64KB보다 크거나 같은 객체는 실제 크기에 따라 요금이 청구됩니다. </li><li>버전 관리를 활성화하지 않고 STANDARD_IA에 객체를 성공적으로 업로드한 경우 COS는 동일한 이름을 가진 기존 객체(있는 경우)를 삭제합니다. 이 경우 <strong>객체 조기 삭제</strong>에 대한 스토리지 사용 요금도 발생합니다.</li></ul></td>
<td>전체 리전</td>
<td>종량제<br>STANDARD_IA 스토리지 패키지</td>
</tr>
</tbody></table>


### STANDARD_IA 스토리지 사용 요금   

<table>
<thead>
<tr><th style="width: 64%;">과금 항목 설명</th><th style="width: 16%;">적용 가능한 리전</th><th style="width: 20%;">적용 가능한 과금 방식</th></tr>
</thead>
<tbody>
<tr>
<td>MAZ_STANDARD_IA 스토리지 사용량은 MAZ_STANDARD_IA 스토리지 클래스에 저장된 데이터의 크기를 나타냅니다. 실제 사용 사례에 따라 요금이 청구됩니다. <ul  style="margin: 0;"><li>30일 미만으로 저장된 객체는 30일로 계산됩니다. 64KB보다 작은 단일 객체는 64KB로 계산되는 반면 64KB보다 크거나 같은 객체는 실제 크기에 따라 요금이 청구됩니다. </li><li>버전 관리를 활성화하지 않고 MAZ_STANDARD_IA에 객체를 성공적으로 업로드한 경우 COS는 동일한 이름을 가진 기존 객체(있는 경우)를 삭제합니다. 이 경우 <strong>객체 조기 삭제</strong>에 대한 스토리지 사용 요금도 발생합니다.</li></ul></td>
<td>베이징, 상하이, 광저우</td>
<td>종량제</td>
</tr>
</tbody></table>

### INTELLIGENT TIERING 스토리지 사용 요금   

<table>
<thead>
<tr><th style="width: 64%;">과금 항목 설명</th><th style="width: 16%;">적용 가능한 리전</th><th style="width: 20%;">적용 가능한 과금 방식</th></tr>
</thead>
<tbody>
<tr>
<td>INTELLIGENT TIERING 스토리지 사용량은 INTELLIGENT TIERING 스토리지 클래스에 저장된 데이터의 크기를 나타냅니다. 실제 사용 사례에 따라 요금이 청구됩니다. <ul  style="margin: 0;"><li>스토리지 사용 요금은 저장된 객체의 티어에 따라 다릅니다. 객체가 자주 액세스하는 티어에 저장되어 있으면 STANDARD 가격이 청구됩니다. 객체가 자주 액세스하지 않는 티어에 저장되어 있는 경우 STANDARD_IA 가격이 청구됩니다. </li><li>64KB보다 작은 객체는 항상 자주 액세스하는 티어에 저장됩니다. <br></li><li>모든 객체는 실제 크기에 따라 요금이 청구됩니다.</li></ul></td>
<td>베이징, 난징, 상하이, 광저우, 청두, 충칭, 도쿄, 싱가포르</td>
<td>종량제</td>
</tr>
</tbody></table>

### MAZ_INTELLIGENT TIERING 스토리지 사용 요금 

<table>
<thead>
<tr><th style="width: 64%;">과금 항목 설명</th><th style="width: 16%;">적용 가능한 리전</th><th style="width: 20%;">적용 가능한 과금 방식</th></tr>
</thead>
<tbody>
<tr>
<td>MAZ_INTELLIGENT TIERING 스토리지 사용량은 MAZ_INTELLIGENT TIERING 스토리지 클래스에 저장된 데이터의 크기를 나타냅니다. 실제 사용 사례에 따라 요금이 청구됩니다. <ul  style="margin: 0;"><li>스토리지 사용 요금은 저장된 객체의 티어에 따라 다릅니다. 객체가 자주 액세스하는 티어에 저장되어 있으면 MAZ_STANDARD 가격이 청구됩니다. 객체가 자주 액세스하지 않는 티어에 저장되어 있는 경우 MAZ_STANDARD_IA 가격이 청구됩니다. </li><li>64KB보다 작은 객체는 항상 자주 액세스하는 티어에 저장됩니다. </li><li>모든 객체는 실제 크기에 따라 요금이 청구됩니다.</li></ul></td>
<td>베이징, 상하이, 광저우</td>
<td>종량제</td>
</tr>
</tbody></table>


### ARCHIVE 스토리지 사용 요금       

<table>
<thead>
<tr><th style="width: 64%;">과금 항목 설명</th><th style="width: 16%;">적용 가능한 리전</th><th style="width: 20%;">적용 가능한 과금 방식</th></tr>
</thead>
<tbody><tr>
<td>ARCHIVE 스토리지 사용량은 ARCHIVE 스토리지 클래스에 저장된 데이터의 크기를 나타냅니다. 실제 사용 사례에 따라 요금이 청구됩니다. <ul  style="margin: 0;"><li>90일 미만으로 저장된 객체는 90일로 계산됩니다. 64KB보다 작은 단일 객체는 64KB로 계산되는 반면 64KB보다 크거나 같은 객체는 실제 크기에 따라 요금이 청구됩니다. </li><li> 버전 관리를 활성화하지 않고 객체를 ARCHIVE에 성공적으로 업로드한 경우 COS는 동일한 이름을 가진 기존 객체(있는 경우)를 삭제합니다. 이 경우 <strong>객체 조기 삭제</strong>에 대한 스토리지 사용 요금이 발생합니다.</li></ul></td>
<td>모든 퍼블릭 클라우드 리전(자카르타 제외), 선전 금융</td>
<td>종량제</td>
</tr>
</tbody></table>


### DEEP ARCHIVE 스토리지 사용 요금  

<table>
<thead>
<tr><th style="width: 64%;">과금 항목 설명</th><th style="width: 16%;">적용 가능한 리전</th><th style="width: 20%;">적용 가능한 과금 방식</th></tr>
</thead>
<tbody><tr>
<td>DEEP ARCHIVE 스토리지 사용량은 DEEP ARCHIVE 스토리지 클래스에 저장된 데이터의 크기를 나타냅니다. 실제 사용 사례에 따라 요금이 청구됩니다. <ul  style="margin: 0;"><li>180일 미만으로 저장된 객체는 180일로 계산됩니다. 64KB보다 작은 단일 객체는 64KB로 계산되는 반면 64KB보다 크거나 같은 객체는 실제 크기에 따라 요금이 청구됩니다.</li><li>버전 관리를 활성화하지 않고 객체를 DEEP ARCHIVE에 성공적으로 업로드한 경우 COS는 동일한 이름을 가진 기존 객체(있는 경우)를 삭제합니다. 이 경우 <strong>객체의 조기 삭제</strong>에 대한 스토리지 요금이 발생합니다.</li></ul></td>
<td>베이징, 난징, 상하이, 광저우, 청두, 충칭, 도쿄, 싱가포르</td>
<td>종량제</td>
</tr>
</tbody></table>


[](id:delete)
### 조기 삭제


<table>
<thead>
<tr><th style="width: 64%;">설명</th><th style="width: 16%;">관련된 스토리지 클래스</th></tr>
</thead>
<tbody>
<tr>
<td><strong>조기 삭제</strong>는 STANDARD_IA, MAZ_STANDARD_IA, ARCHIVE 또는 DEEP ARCHIVE 스토리지 클래스에서 객체가 업로드된 후 최소 저장 기간 요구 사항을 충족하기 전에 수행되는 삭제를 의미합니다. <br><br>참고: STANDARD_IA, MAZ_STANDARD_IA, ARCHIVE 및 DEEP ARCHIVE와 같이 최소 저장 기간 요구 사항이 있는 스토리지 클래스에서 조기 삭제 요금이 발생합니다.
<br><br>과금 규칙:
<li>최소 저장 기간 요구 사항을 충족하기 전에 객체가 삭제된 경우 발생하는 스토리지 사용 요금은 아래 설명된 최소 저장 기간을 기준으로 계산됩니다.
<li>STANDARD_IA 또는 MAZ_STANDARD_IA 데이터 저장 기간이 30일 미만인 경우 30일로 계산됩니다.
<li>ARCHIVE 데이터 저장 기간이 90일 미만인 경우 90일로 계산됩니다.
<li>DEEP ARCHIVE 데이터 저장 기간이 180일 미만인 경우 180일로 계산됩니다.
<br><br>다음 작업으로 인해 조기 삭제가 발생할 수 있습니다.
<br>1. 최소 저장 기간 요건을 충족하기 전에 객체를 미리 삭제합니다.
<br>2. 사용자 정의 헤더 또는 스토리지 클래스와 같은 최소 스토리지 기간 요구 사항을 충족하기 전에 객체의 속성을 수정합니다. 이 경우 COS는 수정에 성공한 후 원본 객체를 삭제하며, 조기 객체 삭제에 따른 스토리지 요금이 부과됩니다.
<br>3. 기존 객체가 최소 저장 기간 요구 사항을 충족하기 전에 버전 관리가 활성화되지 않은 버킷에 기존 객체와 이름이 같은 객체를 업로드합니다. 이 경우 COS는 기존 객체를 삭제하며 조기 객체 삭제에 따른 스토리지 요금이 부과됩니다.
</td>
<td>STANDARD_IA<br>MAZ_STANDARD_IA<br>ARCHIVE<br>DEEP ARCHIVE</td>
</tr>
</tbody></table>


## 스토리지 사용량 과금 방식 및 계산 방법

|  과금 방식   |    계산 방법   |
|-----|-------|
|  종량제   | <ul  style="margin: 0;"> <li>일 결산 주기</li><li>일일 스토리지 사용 요금 = 월 단가 / 30 * 일일 스토리지 사용량</li><li>일일 스토리지 사용량 = ‘5분 사용량’ 합계 / 288(통계 포인트 수)</li></ul>  |
|  스토리지      |     다음 유형의 스토리지 패키지를 사용할 수 있습니다. <ul  style="margin: 0;"> <li>STANDARD 스토리지 패키지: STANDARD 스토리지 사용량을 차감할 수 있으며, MAZ_STANDARD 스토리지 사용량은 차감할 수 없습니다.</li><li>STANDARD_IA 스토리지 패키지: STANDARD_IA 스토리지 사용량을 차감할 수 있으며, MAZ_STANDARD_IA 스토리지 사용량은 차감할 수 없습니다.</li></ul>스토리지 패키지의 유효 기간 동안 매일(구입일 포함) 사용한 스토리지 용량은 스토리지 패키지로 차감할 수 있으며, 초과 사용량은 종량제 방식으로 청구됩니다. |

## 스토리지 사용량 가격


>?
>스토리지 사용량의 단가는 [가격](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)을 참고하십시오.

## 과금 사례

>?
>- 다음 예시의 가격은 참고용입니다. 실제 가격은 COS [가격](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)을 참고하십시오.
>- 스토리지 용량은 이진법으로 계산합니다(예: 1TB = 1024GB).

### 사례1: STANDARD 스토리지 사용 요금 + STANDARD 요청 요금

2020년 11월 1일에 사용자 A가 10GB의 데이터를 STANDARD 스토리지 클래스의 광저우 리전에 있는 COS 버킷에 업로드하여 100회의 요청을 생성하고 유효 기간이 1개월인 중국 본토 리전용 STANDARD 스토리지 패키지 10GB를 0.24 USD에 구입했다고 가정합니다. 이 외에 사용자 A는 다른 작업을 수행하지 않았습니다. 다음과 같이 전일 요금이 다음날에 정산됩니다.

- STANDARD 스토리지 사용 요금: 2020년 11월 2일부터 매일 정산됩니다.
- STANDARD 요청 요금: 2020년 11월 2일에 정산됩니다.

두 가지 과금 방식을 기반으로 다음과 같이 분석할 수 있습니다.

- 종량제:
 - STANDARD 스토리지 사용 요금 = 0.024 USD/GB/월 / 30 x 10GB x 30일 = 0.24 USD.
 - STANDARD 요청 요금 = 0.002 USD/1만 회 x 100 회 / 10,000 = 0.00002 USD
- STANDARD 스토리지 패키지: 2020년 11월 1일부터 11월 30일까지 총 30일 동안 매일 10GB의 STANDARD 스토리지 사용량이 차감되었습니다.

위 금액을 모두 합산하면 전체 11월 사용자 A의 총 요금은 0.24 + 0.00002 = 0.24002USD입니다.


### 사례2: STANDARD_IA 스토리지 사용 요금 + STANDARD_IA 요청 요금

사용자 B가 2020년 11월 1일에 STANDARD_IA 스토리지 클래스의 광저우 리전에 있는 버킷에 10GB의 데이터(34KB 객체의 10000개 조각 및 64KB 이상의 객체의 다른 모든 조각 포함)를 업로드하여 100개의 요청을 생성하으며, 유효 기간이 1개월인 중국 본토 리전용 STANDARD_IA 스토리지 패키지 10GB를 0.18 USD에 구매했다고 가정합니다. 이러한 작업 외에 사용자 B는 11월에 다른 작업을 수행하지 않았다고 했을때, 전일 발생한 요금을 일 단위로 정산하면 다음과 같습니다.

- STANDARD_IA 스토리지 사용 요금: 2020년 11월 2일부터 매일 정산됩니다.
- STANDARD_IA 요청 요금: 2020년 11월 2일에 정산됩니다.

두 가지 과금 방식을 기반으로 다음과 같이 분석할 수 있습니다.

- 종량제:
   - STANDARD_IA 스토리지 사용량 = 10GB + 10,000 x (64 - 34)KB = 10.286GB
    >?64KB 미만의 객체는 64KB로 계산하여 10000 x (64 - 34)KB의 추가 스토리지 사용량이 청구됩니다.
- STANDARD_IA 스토리지 사용 요금 = 0.018 USD/GB/월 /30 x 10.286GB x 30일 = 약 0.19 USD
- STANDARD_IA 요청 요금 = 0.01 USD/1만 회 x 100회 / 10000 = 0.0001 USD
- STANDARD_IA 스토리지 패키지: 2020년 11월 1일부터 2020년 11월 30일까지 총 30일간 STANDARD_IA 스토리지 사용량을 매일 10GB씩 차감했습니다.

위 금액을 모두 합산하면 전체 11월 사용자 B의 총 요금은 0.18 + 0.0001 = 0.1801USD입니다.