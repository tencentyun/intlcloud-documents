본문은 IP별 청구 계정의 요금에 대해 설명하고 관련 요금 예시를 제공합니다.

## 과금 항목
IP별 청구 계정의 경우 CLB 요금에는 인스턴스 요금, 공중망 요금, 리전 간 바인딩 요금 및 LCU 요금의 네 부분이 포함됩니다.
>? 
>+ LCU 지원 CLB 인스턴스에만 LCU 사용 요금이 발생합니다. LCU 지원 CLB 인스턴스는 현재 베타 사용자만 사용할 수 있습니다. 이용하시려면 [신청서를 제출](https://intl.cloud.tencent.com/apply/p/fj5bwo9e6rj)하십시오.
>+ 공유 CLB 인스턴스는 LCU 요금이 무료입니다.
<table>
<tr>
<th>계정 유형 </th>
<th>네트워크 유형 </th>
<th>인스턴스 유형 </th>
<th>인스턴스 요금 </th>
<th>공중망 요금 </th>
<th>리전 간 바인딩 요금 </th>
<th>LCU 요금</th>
</tr>
<tr>
<td rowspan="4" width="15%">IP별 청구</td>
<td rowspan="2">공중망</td>
<td >공유</td>
<td rowspan="2">&#10003; </td>
<td rowspan="2">&#10003; </td>
<td rowspan="2">&#10003; </td>
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
<td rowspan="2">- </td>
<td rowspan="2">- </td>
<td >-</td>
</tr>
<tr>
<td >LCU 지원</td>
<td >&#10003; </td>
</tr>
</table>

+ 사설망 CLB는 공중망 요금 없지만 인스턴스 요금이 발생합니다. 자세한 내용은 [CLB Instance Upgrade and Price Adjustment](https://intl.cloud.tencent.com/document/product/214/41565)를 참고하십시오.
+ 공중망 CLB는 인스턴스 요금과 공중망 요금을 생성합니다.
+ <a href="https://intl.cloud.tencent.com/document/product/214/38441"> 리전 간 바인딩 2.0</a>이 공중망 CLB 인스턴스에 대해 구성되고 활성화된 경우 리전 간 바인딩 요금이 CNN 청구서에 포함됩니다.

>! Tencent Cloud는 <b>2021년 11월 2일 00:00:00(UTC +8)</b>부터 모든 CLB(Cloud Load Balancer) 인스턴스의 아키텍처를 업그레이드할 계획입니다. 업그레이드 후 각 개별 CLB 인스턴스의 보장된 성능은 동시 접속 5만개, 초당 새 접속 5000개 및 QPS 5000개로 증가합니다. CLB 인스턴스(사설망 및 공중망 모두)의 새 단가는 대부분의 지역에서 0.686 USD/일, 나머지 지역에서 1.029 USD/일입니다. 자세한 내용은 [CLB Instance Upgrade and Price Adjustment](https://intl.cloud.tencent.com/document/product/214/41565)를 참고하십시오.


## 종량제 과금[](id:pay-as-you-go)
CLB 요금은 실제 사용량을 기준으로 후불로 계산됩니다.

### 과금 가격
CLB 요금 = [인스턴스 요금](#traffic-instance) + [공중망 요금](#traffic-width) + [LCU 요금](#traffic-lcu)
#### [인스턴스 요금](id:traffic-instance)
인스턴스 요금은 일 단위로 청구되며, 1일에 한 번 정산됩니다. 1시간 미만은 1시간으로 청구됩니다.

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

>!
> - 종량제 CLB 인스턴스 생성 시 1시간 인스턴스 요금이 사전에 차감됩니다. 계정 잔액이 충분한지 확인하십시오.
> - CLB 인스턴스는 유휴 상태일 때도 일당 인스턴스 요금이 발생합니다(즉, 액세스 요청이 없고 실제 서버가 바인딩되지 않음).
#### [공중망 요금](id:traffic-width)
<dx-accordion>

::: 트래픽 기준[](id:traffic)
이 과금 방식은 공중망을 통해 전송되고 매시간 1회 정산되는 총 데이터 양(GB)을 기반으로 하며, 이는 비즈니스 트래픽 변동이 심한 시나리오에 적용할 수 있습니다. 대역폭 사용률이 10% 미만인 경우 요금제를 사용하는 것이 좋습니다.
<dx-alert infotype="explain" title="">
- 현재 아웃바운드 트래픽, 즉 CLB에서 공중망으로의 트래픽이 청구 가능합니다.
- 급격한 트래픽 증가로 인해 높은 비용이 발생하지 않도록 대역폭 최댓값을 지정하여 제한할 수 있습니다. 최댓값을 초과하면 패킷이 손실되어 요금이 청구되지 않도록 기본 설정되어 있습니다.
- 트래픽의 단위 변환 기반은 1024, 즉 1TB = 1024GB, 1GB = 1024MB입니다.
</dx-alert>

<table>
<thead>
<tr>
<th width="70%">리전</th>
<th>공중망 요금(단위: USD/GB)</th>
</tr>
</thead>
<tbody><tr>
<td>중국대륙/서울/중국홍콩/자카르타</td>
<td>0.12</td>
</tr>
<tr>
<td>싱가포르</td>
<td>0.081</td>
</tr>
<tr>
<td>프랑크푸르트/토론토/실리콘밸리</td>
<td>0.077</td>
</tr>
<tr>
<td>모스크바/도쿄</td>
<td>0.13</td>
</tr><tr>
<td>버지니아주</td>
<td>0.075</td>
</tr><tr>
<td>방콕/뭄바이</td>
<td>0.1</td>
</tr><tr>
<td>상파울루</td>
<td>0.15</td>
</tr>
</tbody></table>
:::
::: BWP로 청구[](id:bag)
이 과금 방식은 여러 IP를 집계 방식으로 청구하며 공중망 인스턴스가 서로 다른 시간에 트래픽 피크를 갖는 대규모 비즈니스에 적용할 수 있습니다. 가격 책정에 대한 자세한 내용은 [Dedicated BGP Bandwidth Package](https://intl.cloud.tencent.com/document/product/684/15254#bgp)를 참고하십시오.
:::
</dx-accordion>

#### [LCU 요금](id:traffic-lcu)
종량제 과금 노드에서 LCU가 청구되는 방식에 대한 자세한 내용은 [LCU Pricing](https://intl.cloud.tencent.com/document/product/214/41563)을 참고하십시오.

### 과금 예시
<dx-accordion>
::: 공유
#### 예시1 (공중망은 트래픽에 따라 과금):
트래픽별 공중망에 종량제 CLB 인스턴스를 사용하고 광저우에서 6월 1일 10:00:00 - 6월 2일 09:59:59 사이에 CLB에서 공중망으로의 총 트래픽이 2GB라고 가정합니다.
- 총 인스턴스 요금: 단가 × 사용 기간 = 0.686 USD/일 × 1일 = 0.686 USD.
- 총 공중망 요금: 단가 × 총 트래픽 = 0.12 USD/GB × 2GB = 0.24 USD.
총 요금 = 인스턴스 요금 + 공중망 요금 = 0.686 USD + 0.24 USD = 0.926 USD.

#### 예시2 (공중망은 대역폭 패키지로 청구됨):
광저우에서 6월 1일 10:00:00 - 6월 2일 09:59:59 사이에 BWP 공중망과 함께 사용한 종량제 CLB 인스턴스를 사용한다고 가정합니다.
- 총 인스턴스 요금: 단가 × 사용 기간 = 0.686 USD/일 × 1일 = 0.686 USD.
- 공중망 요금: <a href="https://intl.cloud.tencent.com/document/product/684/15254">BWP 요금</a>은 매월 정산되기 때문에 이 기간의 전체 공중망 요금은 정산할 수 없습니다. 6월 1일 10:00:00 - 6월 2일 09:59:59까지 인스턴스 요금만 청구됩니다.
총 요금 = 인스턴스 요금 = 0.686 USD.
:::
::: LCU 지원
#### 예시 1 (공중망은 트래픽에 따라 청구됨):
트래픽별 공중망에 종량제 CLB 인스턴스를 사용한다고 가정하고 CLB에서 공중망으로의 총 트래픽은 광저우에서 6월 1일 10:00:00 - 6월 2일 09:59:59 사이에 2GB이며 시간당 평균 LCU는 2LCU입니다.
- 총 인스턴스 요금: 단가 × 사용 기간 = 0.686 USD/일 × 1일 = 0.686 USD.
- 총 공용 네트워크 요금: 단가 × 총 트래픽 = 0.12 USD/GB × 2GB = 0.24 USD.
- 총 LCU 요금 = 2 LCU × 0.0072 USD/LCU/시간 × 24시간 = 0.3456 USD.
총 요금 = 인스턴스 요금 + 공중망 요금+ LCU 요금 = 0.686 USD + 0.24 USD + 0.3456 USD) = 1.2716 USD.

#### 예시 2 (공중망은 대역폭 패키지로 청구됨):
광저우에서 6월 1일 10:00:00 - 6월 2일 09:59:59 사이에 BWP 공중망이 있는 종량제 CLB 인스턴스를 사용하고 시간당 평균 LCU는 2 LCU라고 가정합니다.
- 총 인스턴스 요금: 단가 × 사용 기간 = 0.686 USD/일 × 1일 = 0.686 USD.
- 공중망 요금: <a href="https://intl.cloud.tencent.com/document/product/684/15254">BWP 요금</a>은 매월 정산되기 때문에 이 기간의 전체 공중망 요금은 정산할 수 없습니다. 6월 1일 10:00:00 - 6월 2일 09:59:59까지 인스턴스 요금만 청구됩니다.
- 총 LCU 요금 = 2 LCU × 0.0072 USD/LCU/시간 × 24시간 = 0.3456 USD.
총 요금 = 인스턴스 요금(0.686 USD) + LCU 요금(0.0144 USD) = 1.0316 USD.

:::
</dx-accordion>
