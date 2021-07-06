>? [CSS 가격 계산기](https://buy.cloud.tencent.com/price/css/calculator)에서 LVB와 LEB의 예상 요금을 계산할 수 있습니다.

CSS 과금 항목에는 기본 서비스 요금과 부가 서비스 요금이 있습니다. Tencent Cloud에서는 다른 제품과 연계하여 제공하는 부가 기능에 대해 서비스 확장 비용을 부과합니다. 요금 구성 항목은 다음 이미지와 같습니다.

![](https://main.qcloudimg.com/raw/446418a33f13dc82bc9d26b7b6e96b89.png)

- [기본 서비스 요금](#base): 라이브 방송(LVB, LEB 포함) 사용 후 발생하는 라이브 방송에 소모되는 요금입니다. LVB와 LEB는 트래픽 방식 또는 대역폭 피크 방식의 두 가지 과금 방식을 지원합니다.
- [부가 서비스 요금](#appreciation): 라이브 방송 트랜스 코딩, 녹화, 화면 캡처, 음란물 감지 등 부가 서비스 이용 요금입니다. 해당 기능은 기본적으로 비활성화 상태이며 사용 시에만 과금됩니다.
- [확장 서비스 요금](#extensions): Tencent Cloud의 기타 제품과 결합하여 함께 제공되는 부가 서비스입니다. 기타 클라우드 서비스에서 각각의 과금 규정에 따라 관련 요금을 청구합니다.

[](id:base)

## 기본 서비스 요금

기본 서비스 요금은 라이브 방송 서비스 유형에 따라 LVB 서비스 요금과 LEB 서비스 요금으로 나뉩니다.
<table>
<tr><th width="20%">과금 항목</th><th width="60%">과금 설명</th><th>결제 방식</th></tr>
<tr>
<td>LVB 트래픽<br>(기본)</td>
<td>
<li/>LVB 시청으로 발생하는 다운스트림 트래픽 소모
<li/>중국(대륙), 중국 홍콩/마카오/대만 및 GCD의 과금 기준은 각각 상이합니다.
</td>
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/2818">후불-일 결산</a></li>
</td>
</tr><tr>
<td>LVB 대역폭 피크</td>
<td>
<li/>LVB 시청으로 발생하는 다운스트림 대역폭 피크값
<li/>중국(대륙), 중국 홍콩/마카오/대만 및 GCD의 과금 기준은 각각 상이합니다.
</td><td>
<li/><a href="https://cloud.tencent.com/document/product/267/34175#bandwidth">후불-일 결산</a>
<li/>후불-월 결산
</tr><tr>
<td>LEB 트래픽<br>(기본)</td>
<td>LEB 시청으로 중국(대륙)에서 발생하는 다운스트림 트래픽 요금은 일 결산하여 후불 청구됩니다.</td>
<td><li/><a href="https://intl.cloud.tencent.com/document/product/267/39969">후불-일 결산</a></td>
</tr><tr>
<td>LEB 대역폭 피크</td>
<td>LEB 시청으로 중국(대륙)에서 발생하는 다운스트림 대역폭 피크 요금은 일 결산하여 후불 청구됩니다.</td>
<td><li/><a href="https://intl.cloud.tencent.com/document/product/267/39969">후불-일 결산</a></td>
</table>

>!
>- LEB는 초저딜레이 링크를 적용하여 트래픽/대역폭 요금이 LVB보다 높습니다.
>- CSS는 월별 수요가 비교적 많은 사용자에게 더 효율적인 월 결산 과금 방식을 제공합니다. 필요한 경우 영업 담당자에게 문의하여 과금 방식을 변경할 수 있습니다.
>- 과금 방식을 변경하려면 [과금 변경](https://intl.cloud.tencent.com/document/product/267/30411)을 참조하십시오.  

[](id:appreciation)

## 부가 서비스 요금

<table>
<tr><th colspan=2 width="20%">과금 항목</th><th width="60%">과금 설명</th><th>결제 방식</th></tr>
<tr>
<td rowspan=3>라이브 방송 트랜스 코딩</td>
<td>표준 트랜스 코딩</td>
<td><ul style="margin:0">
<li/>라이브 방송 표준 트랜스 코딩 기능을 사용하는 경우 과금됩니다.
<li/><a href="https://intl.cloud.tencent.com/document/product/267/31064">라이브 방송 워터마크</a>, <a href="https://intl.cloud.tencent.com/document/product/267/31071">표준 트랜스 코딩</a>, <a href="https://intl.cloud.tencent.com/document/product/267/37665">라이브 방송 혼합 스트림</a> 등의 기능을 사용하는 경우, 표준 트랜스 코딩 비용이 발생합니다.
<li/>발생 비용은 <b>트랜스 코딩 시간에 따라 과금</b>되며, 송출하는 라이브 방송 스트림 화면 크기의 범위 구간 가격이 과금 단가가 됩니다.
</ul></td>
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604">후불-일 결산</a></li></ul>
</td>
</tr><tr>
<td>초고속 고화질 트랜스 코딩</td>
<td><ul style="margin:0">
 <li>라이브 방송 초고속 고화질 트랜스 코딩 기능을 사용하는 경우 과금됩니다.
<li><a href="https://intl.cloud.tencent.com/document/product/267/31071">초고속 고화질 트랜스 코딩</a> 기능 사용 시 비용이 발생합니다.
<li>발생 비용은 <b>트랜스 코딩 시간에 따라 과금</b>되며, 송출하는 라이브 방송 스트림 화면 크기의 범위 구간 가격이 과금 단가가 됩니다.
</ul><td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/267/39604">후불-일 결산</a></li></ul>
</tr><tr>
<td>오디오 트랜스 코딩</td>
<td>
<li/>라이브 방송 오디오 트랜스 코딩 기능을 사용하는 경우 과금됩니다.
<li/><a href="https://intl.cloud.tencent.com/document/product/267/31071">오디오 트랜스 코딩</a>, 오디오 혼합 스트림, 멀티미디어 분리 등의 기능을 사용하는 경우, 오디오 트랜스 코딩 요금이 발생합니다.
<li/>발생 비용은 <b>오디오 트랜스 코딩 시간에 따라 과금</b>됩니다.
<td><li><a href="https://intl.cloud.tencent.com/document/product/267/39604">후불-일 결산</a></td>
</tr><tr>
  <td colspan=2>라이브 방송 녹화</td>
  <td>
    <li>라이브 방송 녹화는 녹화 템플릿에 따라 생성되는 녹화 파일로 VOD에 저장됩니다.</li>
    <li>녹화로 인해 발생하는 서비스 비용은 <b>LVB 녹화 동시 피크 채널 수에 따라 과금됩니다.</b></li>
  </td>
<td> <li><a href="https://intl.cloud.tencent.com/document/product/267/39605">후불-월 결산</a></td>
</tr><tr>
<td colspan=2>라이브 방송 화면 캡처</td>
<td>
  <li>라이브 방송 화면 캡처는 템플릿 예약 시간에 따라 라이브 방송 스트리밍 화면을 캡처하며, 이미지는 COS에 저장됩니다.</li>
  <li>화면 캡처로 인해 발생하는 서비스 비용은 <b>화면 캡처 건수에 따라 과금되며</b>, 매월 1000건까지 무료로 제공됩니다.</li>
</td>
<td> <li><a href="https://intl.cloud.tencent.com/document/product/267/39606">후불-월 결산</a></td>
</tr><tr>
  <td colspan=2>스마트 음란물 감지</td>
  <td>음란물 감지 화면 캡처 시 음란물 감지 비용과 화면 캡처 비용이 모두 발생합니다.
    <li>음란물 감지로 인해 발생하는 서비스 비용은 <b>음란물 감지 건수에 따라 과금되며</b>, 매월 1000건까지 무료로 제공됩니다.</li>
    <li>화면 캡처로 인해 발생하는 서비스 비용은 <b>화면 캡처 건수에 따라 과금되며</b>, 매월 1000건까지 무료로 제공됩니다.</li>
</td>
<td> <li><a href="https://intl.cloud.tencent.com/document/product/267/39607">후불-월 결산</a></td>
</tr><tr>
[](id:extensions)

## 확장 서비스 요금

<table>
<tr><th width="20%">과금 항목</th><th width="60%">과금 설명</th><th>결제 방식</th></tr>
<tr>
<td>녹화 저장</td>
<td>라이브 방송 녹화 파일은 VOD에 저장해야 하며 비용이 발생합니다. <b>데이터의 실제 저장 시간 및 저장 용량에 따라 과금되며</b> 별도의 VOD 저장 비용이 발생합니다.
</td>
<td> <li><a href="https://cloud.tencent.com/document/product/266/14667#storage_page">VOD-종량제</a> </td>
</tr><tr>
<td>화면 캡처 저장</td>
<td>라이브 방송 화면 캡처 및 음란물 감지로 생성되는 화면 캡처 파일은 COS에 저장되어야 하며 비용이 발생합니다. <strong>데이터 실제 저장 시간 및 저장 용량에 따라 과금되며</strong> 별도의 COS 저장 비용이 발생합니다.</td>
<td> <li><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS-종량제</a></td>
</tr></table>

