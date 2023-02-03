>? [CSS 가격 계산기](https://buy.cloud.tencent.com/price/css/calculator)에서 LVB와 LEB의 예상 요금을 계산할 수 있습니다.

CSS 과금 항목에는 기본 서비스와 부가 서비스가 포함됩니다. CSS와 다른 Tencent Cloud 서비스가 공동으로 제공하는 부가 기능을 사용할 경우 연장된 서비스 요금이 발생합니다. 다음 이미지를 참고하십시오.

![](https://qcloudimg.tencent-cloud.cn/raw/7970d2961c95cd19a4e7568f3ea60467.png)


- [기본 서비스 요금](#base): LVB 및 LEB 사용 요금으로 트래픽 또는 최대 대역폭 사용량에 따라 부과됩니다. LCB는 트래픽 과금 방식만 지원합니다.
- [부가 서비스 요금](#appreciation): 트랜스 코딩, 녹화, 타임 시프트, 화면 캡처, 음란물 감지, 릴레이 등 부가 기능 사용에 대한 요금으로, 해당 기능은 기본적으로 비활성화 되어있으며 활성화된 경우에만 요금이 청구됩니다.
- [확장 서비스 요금](#extensions): CSS와 다른 Tencent Cloud 서비스가 공동으로 제공하는 부가 기능을 사용할 때 발생합니다. 각 Tencent Cloud 서비스는 해당 과금 규칙에 따라 과금됩니다.

[](id:base)
## 기본 서비스 요금

기본 서비스 요금은 라이브 방송 서비스 유형에 따라 LVB 서비스 요금과 LEB 서비스 요금, LCB 서비스 요금으로 나뉩니다.

<table>
<tr><th width="20%">과금 항목</th><th width="60%">설명</th><th>결제 방식</th></tr>
<tr>
<td>LVB 트래픽<br>(기본값)</td>
<td>
<li/>LVB 푸시/풀 스트림에 의해 생성된 업/다운스트림 트래픽에 의해 과금됩니다. 기본적으로 다운스트림 트래픽만 과금됩니다.
<li/>중국 국내 및 해외 과금 기준이 다릅니다.
</td>
<td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#live_pag">선불 리소스 패키지</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/267/2818">후불-일 결산</a></li>
<li/>후불-월 결산
</td>
</tr><tr>
<td>LVB 피크 대역폭</td>
<td>
<li/>LVB 푸시/풀 스트림에 의해 생성된 업/다운스트림 대역폭으로 과금됩니다. 기본적으로 다운스트림 트래픽만 과금됩니다.
<li/>중국 국내 및 해외 과금 기준이 다릅니다.
</td><td>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/2818">후불-일 결산</a>
<li/>후불-월 결산
</td>
</tr><tr>
<td>LEB 트래픽<br>(기본)</td>
<td>
<li/>LEB 푸시/풀 스트림에 의해 생성된 업/다운스트림 트래픽에 의해 과금됩니다. 기본적으로 다운스트림 트래픽만 과금됩니다.
<li/>중국 국내 및 해외 과금 기준이 다릅니다.
</td>
<td>
<li/><a href="https://www.tencentcloud.com/document/product/267/52220#live_pag">선불 리소스 패키지</a>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/39969">후불-일 결산</a>
<li/>후불-월 결산
</td>
</tr><tr>
<td>LEB 피크 대역폭</td>
<td>
<li/>LEB 푸시/풀 스트림에 의해 생성된 업/다운스트림 대역폭으로 과금됩니다. 기본적으로 다운스트림 트래픽만 과금됩니다.
<li/>중국 국내 및 해외 과금 기준이 다릅니다.
</td>
<td>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/39969">후불-일 결산</a>
<li/>후불-월 결산
</td>
</tr></table>

>! 
>- LEB는 대기 시간이 매우 짧은 채널을 사용하기 때문에 트래픽/대역폭 요금이 LVB보다 약간 높습니다.
>- CSS는 월간 수요가 많은 고객에게 월간 과금 방식을 제공합니다. 판매 담당자에게 문의하여 과금 방식을 변경할 수 있습니다.
>- [과금 변경](https://intl.cloud.tencent.com/document/product/267/30411)의 안내에 따라 과금 방식을 변경할 수 있습니다.  


[](id:appreciation)
## 부가 서비스 요금

<table>
<tr><th colspan=2 width="20%">과금 항목</th><th width="60%">과금 안내</th><th>결제 방식</th></tr>
<tr>
<td rowspan=3>라이브 트랜스 코딩</td>
<td>표준 트랜스 코딩</td>
<td><ul style="margin:0">
<li/>표준 라이브 트랜스 코딩을 사용하면 요금이 발생합니다.
<li/>라이브 스트리밍 중 <a href="https://intl.cloud.tencent.com/document/product/267/31064">워터마크</a>, <a href="https://intl.cloud.tencent.com/document/product/267/31071">표준 트랜스 코딩</a>, <a href="https://intl.cloud.tencent.com/document/product/267/37665">스트림 혼합</a>을 사용할 경우 표준 트랜스 코딩 요금이 발생합니다.
<li/>발생하는 비용은 <b>트랜스 코딩 시간에 따라</b>, 출력 라이브 스트림 비디오 해상도의 과금 구간에 따라 과금됩니다.
</ul></td>
<td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#standard_pag">선불 리소스 패키지</a></li>
  <li><a href="https://intl.cloud.tencent.com/document/product/267/39604">후불-일 결산</a></li></ul>
	<li/>후불-월 결산
</td>
</tr><tr>
<td>초고속 코덱 트랜스 코딩</td>
<td><ul style="margin:0">
<li/>라이브 스트리밍 중에 초고속 코덱 트랜스 코딩을 사용하면 요금이 부과됩니다.
<li/><a href="https://intl.cloud.tencent.com/document/product/267/31071">초고속 코덱 트랜스 코딩</a> 사용 시 초고속 코덱 트랜스 코딩 요금이 발생합니다.
<li/>발생하는 비용은 <b>트랜스 코딩 시간에 따라</b>, 출력 라이브 스트림 비디오 해상도의 과금 구간에 따라 과금됩니다.
</ul><td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#topspeed_pag">선불 리소스 패키지</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604">후불-일 결산</a></li>
<li/>후불-월 결산
</td>
</tr><tr>
<td>오디오 트랜스 코딩</td>
<td>
<li/>라이브 스트리밍 중에 오디오 트랜스 코딩을 사용하면 요금이 부과됩니다.
<li/><a href="https://intl.cloud.tencent.com/document/product/267/31071">오디오 트랜스 코딩</a>, 오디오 스트림 믹싱 등 기능을 사용하는 경우 오디오 트랜스 코딩 요금이 부과됩니다.
<li/>요금은 <b>오디오 트랜스 코딩 시간에 따라 과금</b>됩니다.
<td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#standard_pag">선불 리소스 패키지</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604">후불-일 결산</a></li>
<li/>후불-월 결산
</td>
</tr><tr>
  <td colspan=2>라이브 녹화</td>
  <td>
    <li>라이브 녹화 중에는 녹화 템플릿을 기반으로 녹화 파일이 생성되어 VOD에 저장됩니다.</li>
    <li>라이브 방송으로 발생하는 서비스 요금<b>은 최대 동시 라이브 방송 채널 수를 기준으로 과금됩니다</b>.</li>
  </td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39605">후불-월 결산</a></td>
</tr><tr>
<td colspan=2>라이브 타임 시프트</td>
<td>타임 시프트 요금은 총 타임 시프트 시간을 기준으로 합니다.</td>
<td>
<a href="https://www.tencentcloud.com/document/product/267/47534">후불-일 결산</a>
</tr><tr>
<td colspan=2>라이브 스크린 캡처</td>
<td>
  <li>라이브 스크린 캡처 중 라이브 스트림의 스크린샷은 템플릿에 따라 예약된 시점에 캡처되어 COS에 저장됩니다.</li>
  <li>스크린 캡처로 발생하는 서비스 비용은 <b>스크린샷 개수에 따라 과금되며</b>, 매월 첫 1000개의 스크린샷은 무료입니다.</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39606">후불-월 결산</a></td>
</tr><tr>
  <td colspan=2>스마트 화면 캡처 및 음란물 감지</td>
  <td>화면 캡처 및 음란물 감지 기능에는 별도의 요금이 부과됩니다.
    <li>음란물 감지로 인해 발생하는 서비스 비용은 <b>감지된 음란물 스크린샷 수에 따라 과금되며</b>, 매월 첫 1000개의 스크린샷은 무료입니다.</li>
    <li>스크린 캡처로 발생하는 서비스 비용은 <b>스크린샷 개수에 따라 과금되며</b>, 매월 첫 1000개의 스크린샷은 무료입니다.</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39607">후불-월 결산</a></td>
</tr>
<tr><td colspan=2>릴레이</td>
<td>릴레이 작업 시간에 따라 과금됩니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/41059">후불-일 결산</a>
</td>
</tr><tr>
<td colspan=2>서드 파티 URL로 푸시</td>
<td>현재 Tencent Cloud 계정의 CSS 푸시 URL이 아닌 다른 URL로 푸시하면 서드 파티 URL로 푸시하기 위한 요금이 발생합니다.</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/41059">후불-월 결산</a>
</td>
</tr>
</table>

[](id:extensions)
## 확장 서비스 요금

<table>
<tr><th width="20%">과금 항목</th><th width="60%">과금 안내</th><th>결제 방식</th></tr>
<tr>
<td>녹화 저장</td>
<td>라이브 녹화로 생성된 녹화 파일은 VOD로 저장해야 합니다. 발생한 서비스 요금은 <b>실제 보관 기간 및 데이터 양에 따라 과금됩니다. </b>VOD 저장 용량은 별도로 과금됩니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/14666">VOD-종량제</a></td>
</tr><tr>
<td>스크린샷 저장</td>
<td>라이브 스크린 캡처 및 음란물 감지로 생성된 스크린샷 파일은 COS에 저장해야 하며 <strong>발생한 서비스 요금은 실제 저장 기간 및 데이터 볼륨에 따라 과금됩니다.</strong> COS 스토리지 요금은 별도로 과금됩니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS-종량제</a></td>
</tr></table>