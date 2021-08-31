>?해당 제품은 실시간 가격 조회 및 비용 예측을 지원합니다. [가격 센터](https://intl.cloud.tencent.com/pricing/cdb)에서 가격 조회 및 관련 비용 예측에 대한 자세한 정보를 확인할 수 있습니다.

## 과금 방식

TencentDB for MySQL 글로벌 포털에 정액 과금제가 추가되었습니다. 기존 종량제 가격은 변동 없이 유지됩니다.



TencentDB for MySQL은 사용자의 효율적인 사용을 위해 메모리와 디스크에 개별 가격을 책정하여 다양한 과금 방식을 지원합니다.

인스턴스 가격 계산 공식: 인스턴스 가격 = 메모리 사양 요금 + 스토리지 용량 요금






## 고급 기능

### 백업 용량

백업 용량은 정액 과금제를 지원하지 않습니다. 종량제 가격을 참조하십시오.

**인스턴스 연장 관리**

연장 관리 페이지에서는 인스턴스에 대한 일괄 연장, 자동 연장, 만료일 통일, 연장 안 함 표기 등의 기능을 제공합니다.



**인스턴스 업그레이드 알고리즘**

인스턴스의 만료 기간이 T일이고, 업그레이드할 타깃 설정과 기존 설정의 월간 선불금 차액이 C라고 했을 때, 업그레이드 총비용의 계산 공식은 T/30C입니다.

예를 들어 만료 기간이 15일 남아 있는 싱글코어 1000MB 메모리 100G 디스크 인스턴스(선불금 24.511USD/월)를 싱글코어 1000MB 메모리 200G 디스크(선불 34.653USD/월)로 업그레이드하는 경우, 업그레이드 총비용은 15/30(34.653-24.511)=5.071USD입니다.



**인스턴스 디스크 용량 제한 초과 설명**

원활한 비즈니스 진행을 위해 디스크 용량이 다 차기 전 미리 데이터베이스 인스턴스 사양을 업그레이드하거나 디스크 용량을 구매하시기 바랍니다.

인스턴스 스토리지의 데이터 양이 인스턴스를 초과할 경우, 인스턴스가 잠겨 데이터 읽기만 가능하고 입력은 불가능해집니다. 용량을 확장하거나 콘솔에서 일부 DB 테이블을 삭제하여 읽기 전용 모드를 해제해야 합니다.

데이터베이스가 반복적으로 잠기는 현상을 방지하려면 인스턴스의 남은 용량이 20% 이상 또는 50G 이상으로(두 조건 중 한 가지만 만족) 유지되어야 합니다. 해당 상태가 되면 인스턴스의 잠금 상태가 해제되고, 정상적으로 읽고 쓸 수 있습니다.



**재해 복구 인스턴스 동기화 트래픽 요금**

프로모션 기간에는 TencentDB for MySQL 재해 복구 동기화 트래픽 요금이 발생하지 않습니다.

상용화 후 요금 부과 시 별도로 공지합니다.

## 종량제

종량제는 사용 시간에 따라 총 세 단계로 구분합니다.

| 사용 시간 | 차등 가격 |
|---------|---------|
| 0시간＜사용 시간 ≤ 96시간 | 종량제 1단계 가격 |
| 96시간＜사용 시간 ≤ 360시간 | 종량제 2단계 가격 |
| 사용 시간＞360시간 | 종량제 3단계 가격 |

### 인스턴스 가격

#### 과금 공식
**총비용 = 메모리 사양 요금 + 스토리지 용량 요금 + 백업 용량 요금 + 트래픽 요금(현재 무료)**

#### 과금 항목
<table>
<thead>
<tr>
<th width="15%">과금 항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>메모리 사양 요금<br></td>
<td>구매 페이지에서 선택한 인스턴스 사양 요금은 종량제 차등 가격을 지원합니다. 자세한 내용은 <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">제품 가격</a>을 참조하십시오.</td>
</tr>
<tr>
<td>스토리지 용량 요금</td>
<td>구매 페이지에서 선택한 디스크 크기의 요금은 종량제 가격을 지원합니다. 자세한 내용은 <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">제품 가격</a>을 참조하십시오. <br>스토리지 용량은 TencentDB for MySQL 실행에 필요한 데이터 파일, 공유 리스트 용량, 오류 로그 파일, REDO LOG, UNDO LOG, 데이터 사전 및 binlog 등의 저장에 사용됩니다.</tr>
<tr>
<td>백업 용량 요금</td>
<td>TencentDB for MySQL은 리전에 따라 일정 한도의 백업 용량을 무료로 제공합니다. 무료 백업 용량의 크기는 해당 리전에 있는 이중 노드와 3중 노드 인스턴스(마스터 인스턴스 포함)의 전체 스토리지 용량 합계입니다. <br>무료 백업 용량을 초과하는 부분에 대한 요금은 <a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">백업 용량 요금 설명</a>을 참조하십시오.</td>
</tr>
<tr>
<td>트래픽 요금</td>
<td>공용 네트워크 트래픽 요금은 현재 무료입니다.</td>
</tr>
</tbody></table>


#### 종량제 가격

##### 고가용성 버전
<table >
  <td rowspan=2>리전</td>
  <td colspan=3 >메모리 가격(USD/GB/시간)</td>
  <td rowspan=2 >디스크(USD/GB/시간)</td>
 </tr>
 <tr >
  <td >1단계</td>
  <td>2단계</td>
  <td>3단계</td>
 </tr>
 <tr >
  <td >광저우</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>칭위안</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>상하이</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>베이징</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>청두</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>충칭</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>중국홍콩</td>
  <td class=xl66 align=right>0.0688</td>
  <td class=xl65 align=right>0.0516</td>
  <td class=xl65 align=right>0.0344</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>타이베이</td>
  <td class=xl65 align=right>0.0688</td>
  <td class=xl65 align=right>0.0516</td>
  <td class=xl65 align=right>0.0344</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>싱가포르</td>
  <td class=xl65 align=right>0.0705</td>
  <td class=xl65 align=right>0.0528</td>
  <td class=xl65 align=right>0.0352</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>방콕</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>뭄바이</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>서울</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>도쿄</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>실리콘밸리</td>
  <td class=xl65 align=right>0.0550</td>
  <td class=xl65 align=right>0.0413</td>
  <td class=xl65 align=right>0.0275</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>버지니아주</td>
  <td class=xl65 align=right>0.0444</td>
  <td class=xl65 align=right>0.0333</td>
  <td class=xl65 align=right>0.0222</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>토론토</td>
  <td class=xl65 align=right>0.0265</td>
  <td class=xl65 align=right>0.0199</td>
  <td class=xl65 align=right>0.0133</td>
  <td class=xl65 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>프랑크푸르트</td>
  <td class=xl65 align=right>0.0550</td>
  <td class=xl65 align=right>0.0413</td>
  <td class=xl65 align=right>0.0275</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>모스크바</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 </tr>
</table>

##### 읽기 전용 인스턴스

<table>
  <td rowspan=2>리전</td>
  <td colspan=3 >메모리 가격(USD/GB/시간)</td>
  <td rowspan=2 >디스크(USD/GB/시간)</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>1단계</td>
  <td class=xl1529815>2단계</td>
  <td class=xl1529815>3단계</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>광저우</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>칭위안</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>상하이</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>베이징</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>청두</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>충칭</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>중국홍콩</td>
  <td class=xl6529815 align=right>0.0344</td>
  <td class=xl6529815 align=right>0.0258</td>
  <td class=xl6529815 align=right>0.0172</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>타이베이</td>
  <td class=xl6529815 align=right>0.0344</td>
  <td class=xl6529815 align=right>0.0258</td>
  <td class=xl6529815 align=right>0.0172</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>싱가포르</td>
  <td class=xl6529815 align=right>0.0352</td>
  <td class=xl6529815 align=right>0.0264</td>
  <td class=xl6529815 align=right>0.0176</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>방콕</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>뭄바이</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>서울</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>도쿄</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>실리콘밸리</td>
  <td class=xl6529815 align=right>0.0275</td>
  <td class=xl6529815 align=right>0.0206</td>
  <td class=xl6529815 align=right>0.0138</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>버지니아주</td>
  <td class=xl6529815 align=right>0.0222</td>
  <td class=xl6529815 align=right>0.0167</td>
  <td class=xl6529815 align=right>0.0111</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>토론토</td>
  <td class=xl6529815 align=right>0.0133</td>
  <td class=xl6529815 align=right>0.0099</td>
  <td class=xl6529815 align=right>0.0066</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>프랑크푸르트</td>
  <td class=xl6529815 align=right>0.0275</td>
  <td class=xl6529815 align=right>0.0206</td>
  <td class=xl6529815 align=right>0.0138</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>모스크바</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0002</td>
 </tr>
</table>


## 과금 예시
>?다음 제시되는 가격은 예시이며, 실제 가격은 리전, 이벤트, 정책 등에 따라 변동되니 공식 홈페이지의 실제 가격을 참조하십시오.
>

### 정액 과금제
광저우 리전의 예시:
- 광저우3존에서 4코어 8000MB 메모리, 500GB 디스크의 TencentDB for MySQL 인스턴스(고가용성 버전) 1개를 정액 과금제로 1달간 구매한 경우
- 광저우4존에서 4코어 8000MB 메모리, 200GB 디스크의 TencentDB for MySQL 인스턴스(고가용성 버전) 1개를 정액 과금제로 1달간 구매한 경우

총비용 = 메모리 사양 요금 + 스토리지 용량 요금 + 백업 용량 요금

##### 메모리 사양 요금 + 스토리지 용량 요금
요금 계산은 아래와 같습니다.
메모리 사양 요금 + 스토리지 용량 요금 = 2 × 114.93USD/월 + (500GB + 200GB) × 0.1014USD/GB/월 × 1개월 = 300.84USD

##### 백업 용량 요금
광저우3존에서 실행 중인 고가용성 버전 인스턴스에서 구매한 데이터베이스 스토리지 용량이 월 500GB이고, 광저우4존에서 실행 중인 고가용성 버전 인스턴스에서 구매한 데이터베이스 스토리지 용량이 월 200GB라면, 광저우 리전에서는 매월 700GB의 무료 백업 용량이 제공됩니다.

광저우 리전의 총 백업 용량이 700GB를 초과할 경우, 예를 들어 데이터 백업이 800GB, 로그 백업이 100GB에 근접할 경우 과금 용량은 800 + 100 - 700 = 200GB이며, 초과한 200GB에 대한 별도 요금이 발생합니다. 초과분의 과금은 해당 방식으로 계속 이어집니다.

백업 용량 부과 요금(시간당) = 200GB (초과한 백업 용량은 실제 시나리오에 따라 지속 변동될 수 있음) × 0.000127USD/GB/시간

### 종량제
광저우 리전에서 4코어 8000MB 메모리, 500GB 디스크의 TencentDB for MySQL 인스턴스 1개를 종량제로 400시간 구매한 경우
1단계 요금: (0.0250USD/GB/시간×8GB+500GB × 0.0003)×96시간=33.6USD
2단계 요금: (0.0200USD/GB/시간×8GB+500GB × 0.0003)×264시간=81.84USD
3단계 요금: (0.0150USD/GB/시간×8GB+500GB × 0.0003)×40시간=10.8USD
인스턴스 요금 = 1단계 요금 + 2단계 요금 + 3단계 요금 = 126.24USD

## 핵심 질문
#### 정액 과금제 인스턴스를 사용 중인데, 다른 요금이 추가로 차감되는 이유는 무엇인가요?
백업 용량이 무료 한도를 초과했는지 확인하시기 바랍니다. 무료 한도를 초과한 백업 용량에 대해서는 요금이 부과될 수 있습니다.
백업 용량 사용 정보는 [MySQL 콘솔](https://console.cloud.tencent.com/cdb/backup)의 데이터베이스 백업 페이지에서 확인할 수 있으며, 자세한 백업 용량 요금 정보는 [백업 용량 요금 부과 설명](https://cloud.tencent.com/document/product/236/36263)을 참조하십시오.

#### 종량제 인스턴스를 사용하지 않을 경우 요금이 부과되나요?
종량제 인스턴스는 요금이 계속 차감됩니다. 인스턴스를 사용하지 않을 때는 과금되지 않도록 즉시 폐기하시기 바랍니다.

#### 스토리지 용량을 점유하는 파일은 어떤 것들이 있나요?

- 데이터 파일: 생성한 리스트, 인덱스 등을 포함한 데이터가 점유하는 용량입니다.
- 시스템 파일: 공유 리스트 용량, 오류 로그 파일, REDO LOG, UNDO LOG, 데이터 사전을 포함한 시스템 필수 파일이 점유하는 용량입니다.
- binlog 파일: 모든 DDL 및 DML 명령(데이터 쿼리 명령인 select, show 등 제외)을 기록합니다. binlog의 주요 목적은 복사 및 복구로, 변경 데이터가 많을수록 binlog가 많이 생성됩니다. 생성된 [binlog 파일](https://cloud.tencent.com/document/product/236/53513)은 COS에 업로드되어 로컬 binlog 점유 용량을 줄입니다.

## 관련 문서
- TencentDB for MySQL은 콘솔과 API를 통한 인스턴스 구매를 지원합니다. 자세한 내용은 [구매 방식](https://intl.cloud.tencent.com/document/product/236/5160)을 참조하십시오.
- TencentDB for MySQL은 만료 전 리소스가 릴리스될 때까지 사용자에게 알람 메시지를 발송합니다. 자세한 내용은 [연체 설명](https://intl.cloud.tencent.com/document/product/236/5159)을 참조하십시오.
- TencentDB for MySQL은 콘솔을 통한 반품 및 환불 신청을 지원합니다. 자세한 내용은 [환불 설명](https://intl.cloud.tencent.com/document/product/236/14618)을 참조하십시오.
- TencentDB for MySQL은 인스턴스 사양의 업그레이드/다운그레이드를 지원합니다. 자세한 내용은 [인스턴스 비용 조정 설명](https://intl.cloud.tencent.com/document/product/236/32345)을 참조하십시오.
