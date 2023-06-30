## 소개

탄력적 IP(ElP)는 동적 클라우드 컴퓨팅을 위해 설계된 정적 IP입니다. EIP를 사용하면 오류 격리를 위해 계정의 다른 인스턴스(또는 NAT Gateway 인스턴스)에 주소를 빠르게 매핑할 수 있습니다.

공용 IP의 라이프사이클은 CVM에 바인딩되어 있습니다. 즉, 연결된 CVM이 종료되면 공용 IP가 해제됩니다. 그러나 EIP의 라이프사이클은 CVM과 독립적입니다. EIP는 해제하지 않는 한 계정에서 항상 사용할 수 있습니다. 연결된 CVM이 종료된 후에도 공용 IP를 유지하려면 EIP로 변환하십시오.

## EIP와 공용 IP의 차이점
공용 IP와 EIP는 모두 Internet 액세스에 사용됩니다.
- 공용 IP: CVM 생성 시 자동으로 할당되며 CVM에서 바인딩 해제할 수 없습니다.
- EIP: 단독 구매 가능합니다. 클라우드 리소스(CVM, NAT Gateway, ENI 및 HAVIP)와 언제든지 바인딩/해제할 수 있습니다.
>?현재 일반 공용 IP는 일반 BGP IP 회선만 적용할 수 있습니다.
>
EIP에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/215/32382#.E5.85.AC.E7.BD.91-ipv4-.E5.9C.B0.E5.9D.80">IP Addresses</a>를 참고하십시오.
<table>
<thead>
<tr>
<th>항목</th>
<th>공용 IP</th>
<th> EIP</th>
</tr>
</thead>
<tbody><tr>
<td>공용 네트워크 액세스</td>
<td>&#10003; </td>
<td>&#10003; </td>
</tr>
<tr>
<td>독립적인 라이프사이클</td>
<td>×</td>
<td>&#10003; </td>
</tr>
<tr>
<td>자유로운 바인딩/바인딩 해제</td>
<td>×</td>
<td>&#10003; </td>
</tr>
<tr>
<td>대역폭 조정<sup>1</sup></td>
<td>&#10003; </td>
<td>&#10003; </td>
</tr>
<tr>
<td>유휴 요금</td>
<td>×</td>
<td>&#10003; </td>
</tr>
</tbody></table>
<dx-alert infotype="explain" title="">
[공용 IP 콘솔](https://console.cloud.tencent.com/cvm/eip?rid=8)에서는 EIP의 대역폭만 조정할 수 있습니다. 공용 IP의 대역폭을 조정하려면 [네트워크 구성 변경](https://intl.cloud.tencent.com/document/product/213/15517)을 참고하십시오.
</dx-alert>
EIP는 클라우드 리소스의 라이프사이클에서 분리되어 독립적으로 작동할 수 있습니다. 예를 들어, 귀하의 비즈니스와 밀접하게 연결된 특정 공용 IP를 유지해야 하는 경우 EIP로 변경하여 계정에 보관할 수 있습니다.


## 정책과 제한

### 사용 정책

- EIP는 기본 네트워크 및 VPC의 인스턴스와 VPC의 [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015) 인스턴스에 적용됩니다.
- EIP를 CVM 인스턴스와 바인딩하면, 원래의 공용 IP가 동시에 해제됩니다.
- CVM/NAT Gateway 인스턴스가 종료되면 EIP에서 연결이 해제됩니다.
- EIP의 과금 정책과 관련된 내용은 [EIP 과금](https://intl.cloud.tencent.com/document/product/213/17156)을 참고하십시오.
- EIP 작업 순서와 관련된 내용은 [EIP](https://intl.cloud.tencent.com/document/product/213/16586)를 참고하십시오.

### 할당량

| 리소스 | 할당량 |
|---------|:---------:|
| EIP/리전(Region) | 20개 |
| 일일 구매(회) | 지역 EIP 할당량 \* 2회 |
| EIP 바인딩 해제로 인해 할당된 공용 IP/일 | 10회 |

>? 기본적으로 EIP 할당량은 조정할 수 없습니다. [NAT Gateway](https://intl.cloud.tencent.com/product/nat), [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214)에서 IP 컨버전스로 일부 할당량을 확보할 수 있습니다.
> - 조정이 필요한 특별한 상황이 있는 경우, 계정 번호는 해당 클라우드 서비스 리소스를 가지고 있으며 합리적으로 사용해야 합니다.



### CVM에 바인딩된 공용 IP에 대한 제한

>? 2019년 9월 18일 00:00 이전에 구매한 CVM 인스턴스의 경우 각 인스턴스에 바인딩할 수 있는 공용 IP 수는 [내부 IP 수량](https://intl.cloud.tencent.com/document/product/576/18527)과 동일합니다.
>

| CPU 코어 | 공용 IP + EIP |
|---------|---------|
| CPU：1 - 5 | 2 |
| CPU：6 - 11 | 3 |
| CPU：12 - 17 | 4 |
| CPU：18 - 23 | 5 |
| CPU：24 - 29 | 6 |
| CPU：30 - 35 | 7 |
| CPU：36 - 41 | 8 |
| CPU：42 - 47 | 9 |
| CPU：≥ 48 | 10 |



