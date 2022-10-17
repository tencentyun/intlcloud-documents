본문은 CVM별 청구서 요금에 대해 설명하고 참고용 요금 예시를 제공합니다.

## 과금 항목
CVM별 청구서 계정의 경우 CLB 비용에는 인스턴스 요금, 공중망 요금 및 LCU 요금의 세 부분이 포함됩니다.
<table>
<tr>
<th>계정 유형 </th>
<th>네트워크 유형 </th>
<th>인스턴스 유형 </th>
<th>인스턴스 요금 </th>
<th>공중망 요금 </th>
<th>LCU 요금</th>
</tr>
<tr>
<td rowspan="4" width="15%">CVM별 청구서</td>
<td rowspan="2">공중망 </td>
<td >공유</td>
<td rowspan="2">&#10003; </td>
<td rowspan="2">× </td>
<td>-</td>
</tr>
<tr>
<td >LCU 지원</td>
<td >&#10003; </td>
</tr>
<tr>
<td rowspan="2">사설망 </td>
<td >공유</td>
<td rowspan="2">&#10003; </td>
<td rowspan="2">-</td>
<td >-</td>
</tr>
<tr>
<td >LCU 지원</td>
<td >&#10003; </td>
</tr>
</table>

>?
>+ LCU 지원 CLB 인스턴스에만 LCU 사용 요금이 발생합니다. LCU 지원 CLB 인스턴스는 베타 사용자만 사용할 수 있습니다. 사용하시려면 [신청서를 제출](https://intl.cloud.tencent.com/apply/p/fj5bwo9e6rj) 하십시오. 공유 CLB 인스턴스는 LCU 요금이 무료입니다.
>+ 사설망 CLB는 공중망 요금은 무료지만, 인스턴스 요금이 발생합니다.
>+ 공중망 CLB에는 인스턴스 요금만 발생합니다. CVM에서 공중망을 구입할 수 있습니다. 자세한 내용은 [공용 네트워크 요금](https://intl.cloud.tencent.com/zh/document/product/213/39743)을 참고하십시오.

### 인스턴스 요금
>! Tencent Cloud는 <b>2021년 11월 2일 00:00:00(UTC +8)</b>에 모든 CLB 인스턴스의 아키텍처를 업그레이드했습니다. 업그레이드 후 각 개별 CLB(Cloud Load Balancer) 인스턴스의 보장된 성능은 동시 연결 5만개, 초당 새 연결 5000개 및 QPS 5000개로 증가합니다. CLB 인스턴스(사설망 및 공중망 모두)의 새 단가는 대부분의 리전은 0.686 USD/일, 나머지 리전은 1.029 USD/일입니다. 자세한 내용은 [CLB Instance Upgrade and Price Adjustment](https://intl.cloud.tencent.com/zh/document/product/214/41565)를 참고하십시오.
>
- 사설망 CLB는 공중망 요금은 무료지만, 인스턴스 요금이 발생합니다. 자세한 내용은 [CLB Instance Upgrade and Price Adjustment](https://intl.cloud.tencent.com/zh/document/product/214/41565)를 참고하십시오.
- **공중망 CLB 인스턴스는 종량제 모델을 채택합니다.**
 - 매시간 1회 정산됩니다.
 - 실제 사용 시간을 기준으로 계산됩니다.
 - 과금은 CLB 인스턴스가 성공적으로 생성된 시점에 시작되어 인스턴스 종료를 시작하는 시점에 종료됩니다.
 - 1시간 미만의 사용 시간은 1시간으로 계산됩니다.
- **공중망 CLB 인스턴스 요금은 리전에 따라 다릅니다.**
<table>
<thead>
<tr>
<th >리전</th>
<th >인스턴스 요금(단위: USD/일)</th>
</tr>
</thead>
<tbody><tr>
<td>광저우/상하이/난징/베이징/청두/충칭/중국홍콩/싱가포르/자카르타/실리콘밸리/버지니아/토론토/모스크바</td>
<td>0.686</td>
</tr>
<tr>
<td>방콕/뭄바이/서울/도쿄/프랑크푸르트/상파울루</td>
<td>1.029</td>
</tr>

</tbody></table>


- **과금 예시**:
  광저우에서 09:00:00 - 09:59:59 사이에 공중망 CLB 인스턴스를 사용하는 경우 인스턴스 요금은 0.686 USD이며 다음 시간(10:00:00 - 10:59:59)에 정산 및 차감됩니다.
>!
>- 종량제 CLB 인스턴스를 생성할 때 하나의 정산 주기에 대한 요금이 미리 공제됩니다. 계정 잔액이 충분한지 확인하십시오.
>- CLB 인스턴스는 유휴 상태일 때도 시간당 인스턴스 요금이 발생합니다(즉, 액세스 요청이 없고 실제 서버가 바인딩되지 않음).

### 공중망 요금
Tencent Cloud는 최적의 네트워크 경험을 보장하기 위해 ISP를 위한 고품질 공개 VIP를 제공합니다.
>!CLB에 액세스하는 클라이언트에 대한 공중망 요금은 CVM 청구서에 포함됩니다. 공중망을 구매하지 않으면 공중망 CLB 인스턴스를 통해 CVM 인스턴스에 액세스할 수 없습니다.
>
<table>
<tr>
<th width="18%">CLB IP 버전</th>
<th width="82%">공중망 요금</th>
</tr>
<tr>
<td>IPv4 및 IPv6 NAT64 CLB 인스턴스</td>
<td>클라이언트가 CLB에 액세스하면 발생하는 공중망 요금이 CVM 청구서에 포함됩니다. CVM 인스턴스를 생성할 때 공중망 기능(최대 대역폭) 및 과금 방법을 트래픽별 요금으로 지정해야 합니다. CLB는 공중망 송신 역할만 합니다. 공중망을 구매하지 않으면 공중망 CLB 인스턴스를 통해 CVM 인스턴스에 액세스할 수 없습니다.</td>
</tr>
<tr>
<td>IPv6 CLB 인스턴스</td>
<td> IPv6 CLB는 유료 서비스입니다. CVM별 청구 계정의 경우 IPv6 이중 스택 공중망을 사용하는 IPv6 CLB 인스턴스에 대한 대역폭 요금은 BWP로 정산됩니다(IPv4, IPv6 NAT64의 공중망 과금 방식은 영향을 받지 않음). IPv6 CLB 인스턴스를 생성할 때 공중망 기능(최대 대역폭) 및 과금 방식을 BWP별로 지정해야 합니다. 자세한 내용은<a href="https://intl.cloud.tencent.com/zh/document/product/684/15254" target="_blank"> 과금 개요</a>를 참고하십시오.</td>
</tr>
</table>

### LCU 요금
LCU 요금에 대한 자세한 내용은 [LCU Pricing](https://intl.cloud.tencent.com/zh/document/product/214/41563)을 참고하십시오.
## 관련 문서
[Billing Overview](https://intl.cloud.tencent.com/zh/document/product/214/36999)
