본문은 CLB(Cloud Load Balancer) 인스턴스 과금에 대한 설명입니다.


## 과금 항목
CLB 비용은 인스턴스 요금, 공중망 요금, 리전 간 바인딩 요금 및 LCU(Loadbalancer Capacity Unit) 요금의 네 부분으로 구성됩니다.
<dx-alert infotype="explain" title="">
- LCU 지원 ‘성능 용량’ CLB 인스턴스에만 LCU 사용 요금이 발생합니다.
- Tencent Cloud는 IP별 청구와 CVM별 청구의 두 가지 유형의 계정을 제공합니다. 2020년 6월 17일 00:00:00(UTC +8) 이후에 등록된 모든 Tencent Cloud 계정은 IP별 청구 계정입니다. 그 이전에 계정을 생성했다면 <a href="https://console.cloud.tencent.com/cvm/eip">EIP 콘솔</a>의 인스턴스 목록 상단에서 계정 유형을 확인할 수 있습니다.
- 전용 CLB 인스턴스를 사용하려면 영업 담당자에게 문의하십시오.
</dx-alert>
<table>
<tr>
<th>인스턴스 유형 </th>
<th>계정 유형 </th>
<th>인스턴스 요금 </th>
<th>공중망<br/>요금 </th>
<th>리전 간<br/>바인딩 요금 </th>
<th>성능 용량 단위<br/> LCU 요금</th>
</tr>
<tr>
<td rowspan="2">공중망 </td>
<td >IP별 청구 계정 </td>
<td >&#10003; </td>
<td >&#10003; </td>
<td >&#10003; </td>
<td >&#10003;</td>
</tr>
<tr>
<td >CVM별 청구 계정 </td>
<td >&#10003; </td>
<td >× </td>
<td >-</td>
<td >&#10003;</td>
</tr>
<tr>
<td >사설망 </td>
<td >모든 계정 </td>
<td >&#10003;</td>
<td >-</td>
<td >-</td>
<td >&#10003;</td>
</tr>
</table>

## IP별 청구 계정 과금 설명
+ 사설망 CLB는 공용망 요금은 없지만 인스턴스 요금이 발생합니다. 자세한 내용은 [CLB Instance Upgrade and Price Adjustment](https://intl.cloud.tencent.com/zh/document/product/214/41565)를 참고하십시오.
+ 공중망 CLB는 인스턴스 요금과 공중망 요금을 과금합니다.
+ <a href="https://intl.cloud.tencent.com/zh/document/product/214/38441"> 리전 간 바인딩 2.0</a>이 공중망 CLB 인스턴스에 대해 구성되고 활성화된 경우 리전 간 바인딩 요금이 CNN 청구서에 포함됩니다.
+ LCU 지원 CLB 인스턴스에는 LCU 요금이 발생하지만 공유 CLB 인스턴스에는 요금이 부과되지 않습니다.

## CVM별 청구 계정 과금 설명
+ 사설망 CLB는 공중망 요금은 없지만 인스턴스 요금이 발생합니다. 자세한 내용은 [CLB Instance Upgrade and Price Adjustment](https://intl.cloud.tencent.com/zh/document/product/214/41565)를 참고하십시오.
+ 공중망 CLB는 인스턴스 요금만 발생합니다. CVM에서 공중망을 구입할 수 있습니다. 자세한 내용은 [공용 네트워크 요금](https://intl.cloud.tencent.com/zh/document/product/213/39743)을 참고하십시오.
+ CVM별 청구 계정은 리전 간 바인딩을 지원하지 않으므로 바인딩 요금이 생성되지 않습니다.
+ LCU 지원 CLB 인스턴스에는 LCU 요금이 발생하지만 공유 CLB 인스턴스에는 요금이 부과되지 않습니다.

## 관련 문서
- [Billing for Bill-by-IP Accounts](https://intl.cloud.tencent.com/zh/document/product/214/36998)
- [Billing for Bill-by-CVM Accounts](https://intl.cloud.tencent.com/zh/document/product/214/8848)