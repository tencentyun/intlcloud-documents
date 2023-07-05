본 문서에서는 사용자의 필요에 따라 적합한 과금 방식을 선택할 수 있도록 다양한 공용 네트워크 요금제를 소개합니다.
>?본문은 일반 BGP IP의 공용 네트워크 비용을 소개합니다. 프리미엄 BGP IP, 가속 IP 현재 BWP 과금만 지원합니다. [BWP](#bwp)를 참고하시기 바랍니다.
>
## [트래픽 과금](id:by-traffic)
사용하는 공용 네트워크 트래픽에 따라 후불로 과금하며, 시간 단위로 결산됩니다. 시간대별로 비즈니스 트래픽 피크의 변동이 큰 시나리오에 적합합니다.
**과금 가격**
<table>
<thead>
<tr>
<th rowspan="2" width="65%">리전</th>
<th colspan="2" style="text-align:center;">가격(단위: USD/GB)</th>
</tr>
</thead>
<tbody><tr>
<td>중국대륙(홍콩, 마카오 및 대만 제외), 중국홍콩, 자카르타, 서울</td>
<td>0.12</td>
</tr>
<tr>
<td>도쿄</td>
<td>0.13 </td>
</tr>
<tr>
<td>싱가포르</td>
<td>0.081</td>
</tr>
<tr>
<td>상파울루</td>
<td>0.15</td>
</tr>
<tr>
<td>프랑크푸르트,실리콘밸리,토론토</td>
<td>0.077</td>
</tr>
<tr>
<td>뭄바이,방콕</td>
<td>0.1</td>
</tr>
<tr> 
<td>버지니아</td>
<td>0.075</td>
</tr>
<tr>    
</tbody></table>



**과금 예시**
사용자가 광저우 리전의 EIP를 구매하고 트래픽 과금 방식을 선택했다고 가정합니다. 사용자가 07:00:00 - 07:59:59 사이에 사용한 트래픽이 총 10GB라면, 08:00:00에 발생하는 요금은 0.12USD/GB × 10GB = 1.2USD가 됩니다.

> ?
> - 트래픽의 단위 변환 기반은 1024, 즉 1TB = 1024GB, 1GB = 1024MB입니다.
> - 공용 네트워크 트래픽은 다운스트림 바이트 수(아웃바운드 트래픽 바이트 수)로 통계한 트래픽 데이터입니다. 실제 네트워크 전송 과정에서 생성되는 네트워크 트래픽은 순수 응용 레이어 트래픽보다 약 5%-15% 많으며, Tencent Cloud에서 통계한 트래픽은 사용자 서버에서 자체적으로 통계한 트래픽보다 10% 정도 많을 수 있습니다.
>  - TCP/IP 헤더 소모: TCP/IP 프로토콜 기반의 HTTP 요청으로, 각 패킷의 최대 크기는 1,500바이트이며 이는 TCP 및 IP 프로토콜의 헤더 40바이트를 포함합니다. 헤더 부분 역시 트래픽이 발생하지만 이는 응용 레이어에 의해 통계되지 않으므로, 이 부분의 비용은 약 3%로 계산됩니다.
>  - TCP 재전송: 정상적인 네트워크 전송 과정에서, 전송된 네트워크 패킷의 3%-10%가 인터넷에서 손실되며, 손실된 후 서버에서 누락된 부분을 재전송합니다. 이 부분의 트래픽 응용 레이어 역시 통계되지 않으며, 약 3%-7%를 자치합니다.
> 


## [BWP](id:bwp)
BWP는 멀티 IP 집계 과금 방식으로, 비즈니스 중 공용 네트워크 트래픽 피크가 서로 다른 시간대에 분포되어 있을 때, BWP로 대역폭 집계 과금이 가능해 공용 네트워크 요금을 크게 절감할 수 있습니다.
다른 IP 회선 유형은 아래 이미지와 같이 다른 BWP 유형 및 요금에 해당합니다.
<table>
<thead>
<tr>
<th>IP 회선 유형</th>
<th>BWP 유형</th>
</tr>
</thead>
<tbody><tr>
<td>일반 BGP IP</td>
<td><a href="https://intl.cloud.tencent.com/document/product/684/15254">일반 BGP 대역폭 패키지</a></td>
</tr>
<tr>
<td>명품 BGP IP</td>
<td><a href="https://intl.cloud.tencent.com/document/product/684/15254">명품 BGP 대역폭 패키지</a></td>
</tr>
<tr>
<td>가속 IP</td>
<td><a href="https://intl.cloud.tencent.com/document/product/684/15254">Anycast 가속 BGP 대역폭 패키지</a></td>
</tr>
<tr>
<td>정적 단일 회선 IP</td>
<td><a href="https://intl.cloud.tencent.com/document/product/684/15254">China Mobile/China Unicom/China Telecom 대역폭 패키지</a></td>
</tr>
</tbody></table>

## 관련 문서
- [CVM 대역폭 최댓값](https://intl.cloud.tencent.com/document/product/213/12523)
