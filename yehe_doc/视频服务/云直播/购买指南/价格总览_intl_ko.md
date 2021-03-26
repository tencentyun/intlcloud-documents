>? [CSS 가격 계산기](https://buy.cloud.tencent.com/price/css/calculator)에서 LVB와 LEB의 예상 요금을 계산할 수 있습니다.

CSS 요금 항목에는 기본 서비스 요금과 부가 서비스 요금이 있습니다. Tencent Cloud에서는 다른 제품과 접목해 제공하는 부가 기능에 대해 서비스 확장 비용을 부과합니다. 요금 구성 항목은 다음 이미지와 같습니다.

![](https://main.qcloudimg.com/raw/2ce6c231a986ddb89e2ae2680d2c2563.png)


- [기본 서비스 요금](#base): 라이브 방송(LVB 및 LEB 포함) 이용 후 발생하는 라이브 방송 소모 비용으로, LVB와 LEB는 트래픽 방식 또는 대역폭 피크 방식의 두 가지 과금 방식을 지원합니다.
- [부가 서비스 요금](#appreciation): 라이브 방송 트랜스 코딩, 녹화, 화면 캡처, 음란물 감지, 클라우드 스튜디오 등 부가 서비스 이용 비용으로, 해당 기능은 기본적으로 비활성화 상태이며 사용 시에만 과금됩니다.
- [확장 서비스 요금](#extensions): Tencent Cloud의 다른 제품과 결합하여 제공되는 부가 서비스로, 다른 클라우드 서비스 각각의 과금 규정에 따라 관련 비용이 청구됩니다.

<span id="base"></span>

## 기본 서비스 요금

기본 서비스 요금은 라이브 방송 서비스 유형에 따라 LVB 서비스 요금과 LEB 서비스 요금으로 나뉩니다.

<table>
<tr><th width="20%">요금제</th><th width="60%">요금안내</th><th>결제 방식</th></tr>
<tr>
<td>LVB 트래픽<br>(기본)</td>
<td>
<li/>LVB 시청으로 발생하는 다운스트림 트래픽 요금은 일 결산하며 후불제가 적용됩니다.
<li/>중국(대륙), 중국홍콩, 중국마카오, 중국대만 및 GCD의 과금 기준은 각각 상이합니다.
</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/2818">후불 - 일 결산</a></li>
</td>
</tr><tr>
<td>LVB 대역폭 피크</td>
<td>
<li/>LVB 시청으로 발생하는 다운스트림 대역폭 피크 요금은 일 결산하며 후불제가 적용됩니다.
<li/>중국(대륙), 중국홍콩, 중국마카오, 중국대만 및 GCD의 과금 기준은 각각 상이합니다.
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818">후불 - 일 결산</a></td>
</tr><tr>
<td>LEB 트래픽<br>(기본)</td>
<td>LEB 시청으로 중국(대륙)에서 발생하는 다운스트림 트래픽 요금은 일 결산하며 후불제가 적용됩니다. </td>
<td>후불 - 일 결산</a></td>
</tr><tr>
<td>LEB 대역폭 피크</td>
<td>LEB 시청으로 중국(대륙)에서 발생하는 다운스트림 대역폭 피크 요금은 일 결산하며 후불제가 적용됩니다. </td>
<td>후불 - 일 결산</a></td>
</tr></table>

>! 
>- LEB는 최저 수준의 링크 딜레이를 지원하므로 트래픽/대역폭 요금이 LVB보다 높습니다.
>- 과금 방식을 변경하고 싶은 경우, [과금 변경](https://intl.cloud.tencent.com/document/product/267/30411)을 참조하십시오.  


<span id="appreciation"></span>

## 부가 서비스 요금

<table>
<tr><th colspan=2 width="20%">요금제</th><th width="60%">요금안내</th><th>결제 방식</th></tr>
<tr>
<td rowspan=3>라이브 방송 트랜스 코딩</td>
<td>표준 트랜스 코딩</td>
<td><ul style="margin:0">
<li/>라이브 방송 표준 트랜스 코딩 기능을 사용하는 경우 과금됩니다.
<li/><a href="https://intl.cloud.tencent.com/document/product/267/31064">라이브 방송 워터마크</a>, <a href="https://intl.cloud.tencent.com/document/product/267/31071">표준 트랜스 코딩</a>, <a href="https://intl.cloud.tencent.com/document/product/267/37665">라이브 방송 혼합 스트림</a> 등의 기능을 사용하는 경우 표준 트랜스 코딩 비용이 발생합니다.
<li/>발생 비용은 <b>트랜스 코딩 시간에 따라 과금</b>되며, 출력하는 라이브 방송 스트리밍 화면 사이즈의 범위 구간 가격이 과금 단가가 됩니다.
</ul></td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/39604">후불 - 일 결산</a></li></ul>
</td>
</tr><tr>
<td>고속 HD 트랜스 코딩</td>
<td><ul style="margin:0">
<li/>라이브 방송 고속 HD 트랜스 코딩 기능을 사용하는 경우 과금됩니다.
<li/> <a href="https://intl.cloud.tencent.com/document/product/267/31071">고속 고화질 트랜스 코딩</a> 기능을 사용하면 이에 따른 요금이 발생합니다.
<li/>발생 비용은 <b>트랜스 코딩 시간에 따라 과금</b>되며, 출력하는 라이브 방송 스트리밍 화면 사이즈의 범위 구간 가격이 과금 단가가 됩니다.
</ul><td>
<a href="https://intl.cloud.tencent.com/document/product/267/39604">후불 - 일 결산</a></li></td>
</tr><tr>
<td>오디오 트랜스 코딩</td>
<td>
<li/>라이브 방송 오디오 트랜스 코딩 기능을 사용하는 경우 과금됩니다.
<li/><a href="https://intl.cloud.tencent.com/document/product/267/31071">오디오 트랜스 코딩</a>, 오디오 혼합 스트림, 멀티미디어 분리 등의 기능 사용 시 오디오 트랜스 코딩 요금이 발생합니다.
<li/>발생하는 비용은 <b>오디오 트랜스 코딩 시간에 따라 과금</b>됩니다.
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/39604">후불 - 일 결산</a></li></td>
</tr><tr>
  <td colspan=2>라이브 방송 녹화</td>
  <td>
    <li>라이브 방송 녹화는 녹화 템플릿에 따라 생성되는 녹화 파일로 VOD에 저장됩니다.</li>
    <li>녹화로 인해 발생하는 서비스 비용은 <b>LVB 녹화 동시 피크 채널 수에 따라 과금됩니다.</b></li>
  </td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39605">후불 - 월 결산</a></td>
</tr><tr>
<td colspan=2>라이브 방송 화면 캡처</td>
<td>
  <li>라이브 방송 화면 캡처는 템플릿 예약 시간에 따라 라이브 방송 스트리밍 화면을 캡처하며, 이미지는 COS에 저장됩니다.</li>
  <li>화면 캡처로 인해 발생하는 서비스 비용은 <b>화면 캡처 건수에 따라 과금되며</b>, 매월 1,000건까지 무료로 제공됩니다.</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39606">후불 - 월 결산</a></td>
</tr><tr>
  <td colspan=2>스마트 음란물 감지</td>
  <td>음란물 감지 화면 캡처는 음란물 감지 비용과 화면 캡처 비용이 모두 발생합니다.
    <li>음란물 감지에 따른 서비스 비용은 <b>음란물 감지 건수에 따라 과금되며</b>, 매월 1000건까지 무료로 제공됩니다.</li>
    <li>화면 캡처로 인해 발생하는 서비스 비용은 <b>화면 캡처 건수에 따라 과금되며</b>, 매월 1,000건까지 무료로 제공됩니다.</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39607">후불 - 월 결산</a></td>
</tr>
</table>


<span id="extensions"></span>

## 확장 서비스 요금

<table>
<tr><th width="20%">요금제</th><th width="60%">요금안내</th><th>결제 방식</th></tr>
<tr>
<td>녹화 저장</td>
<td>라이브 방송 녹화 파일은 VOD에 저장해야 하며 비용이 발생합니다. <b>데이터의 실제 저장 시간과 저장량에 따라 과금되며</b> 별도의 VOD 저장 비용이 발생합니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/14666">VOD - 종량제</a></td>
</tr><tr>
<td>화면 캡처 저장</td>
<td>라이브 방송 화면 캡처와 음란물 감지로 생성되는 화면 캡처 파일은 COS에 저장해야 하며 비용이 발생합니다. <strong>데이터 실제 저장 시간 및 저장량에 따라 과금되며</strong> 별도의 COS 저장 비용이 발생합니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS - 종량제</a></td>
</tr></table>

