>? [CSS 가격 계산기](https://buy.cloud.tencent.com/pricing/css/calculator)에서 라이브 방송 관련 비용을 예상할 수 있습니다.

CSS 요금제에는 기본 서비스 요금, 부가 서비스 요금 및 확장 서비스 요금이 포함되며, 요금 구성은 다음 그림과 같습니다.

![](https://main.qcloudimg.com/raw/2ce6c231a986ddb89e2ae2680d2c2563.png)


- [기본 서비스 요금](#base): CSS 이용 후 발생하는 라이브 방송 소모 비용으로, 트래픽 방식 또는 대역폭 피크 방식의 두 가지 과금 방식을 제공합니다.
- [부가 서비스 요금](#appreciation): 라이브 방송 트랜스 코딩, 녹화, 화면 캡처, 음란물 감지 등의 부가 서비스 이용 비용으로, 해당 기능은 기본적으로 꺼져 있으며 사용 시에만 과금됩니다.
- [확장 서비스 요금](#extensions): Tencent Cloud의 기타 제품과 결합하여 함께 제공되는 부가 서비스로, 다른 클라우드 서비스가 각각의 과금 규정에 따라 관련 비용을 청구합니다.

<span id="base"></span>

## 기본 서비스 요금
<table>
<tr><th width="20%">과금 항목</th><th width="60%">과금 설명</th><th>결제 방식</th></tr>
<tr>
<td>CSS 트래픽<br>(기본)</td>
<td>
<li/>CSS 시청으로 발생하는 다운스트림 트래픽 사용량은 일별 사용량에 따라 후불 청구됩니다.
<li/>중국(본토), 중국홍콩, 중국마카오, 중국대만 및 기타 해외 지역의 가속 요금 표준은 지역별로 상이합니다.
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#bill-by-traffic">후불-일 결산</a></td>
</tr><tr>
<td>CSS 대역폭 피크</td>
<td>
<li/>CSS 시청으로 발생하는 다운스트림 대역폭 피크는 일별 사용량에 따라 후불 청구됩니다.
<li/>중국(본토), 중국홍콩, 중국마카오, 중국대만 및 기타 해외 지역의 가속 요금 표준은 지역별로 상이합니다.
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#bill-by-bandwidth">후불-일 결산</a></td>
</tr></table>

>! 과금 방식을 변경하고 싶은 경우, [과금 변경](https://intl.cloud.tencent.com/document/product/267/30411)을 참조 바랍니다.  


<span id="appreciation"></span>

## 부가 서비스 요금

<table>
<tr><th colspan=2 width="20%">과금 항목</th><th width="60%">과금 설명</th><th>결제 방식</th></tr>
<tr>
<td rowspan=3>라이브 방송 트랜스 코딩</td>
<td>표준 트랜스 코딩</td>
<td><ul style="margin:0">
<li>라이브 방송 표준 트랜스 코딩 기능을 사용하는 경우에 과금됩니다.
<li><a href="https://intl.cloud.tencent.com/document/product/267/31064">라이브 방송 워터마크</a>、<a href="https://intl.cloud.tencent.com/document/product/267/31071#C_trans">표준 트랜스 코딩</a>、<a href="https://intl.cloud.tencent.com/document/product/267/37665">라이브 방송 혼합 스트림</a> 등의 기능을 사용하는 경우, 표준 트랜스 코딩 비용이 발생합니다.
<li>발생 비용은 <b>트랜스 코딩 시간에 따라 과금</b>되며, 출력하는 라이브 방송 스트리밍 화면 사이즈의 범위 구간 가격을 과금 단가로 합니다.
</ul></td>
<td>
  <li><a href="https://intl.cloud.tencent.com/document/product/267/39604#n_trans">후불-일 결산</a></li></ul>
</td>
</tr><tr>
<td>고속 HD 트랜스 코딩</td>
<td><ul style="margin:0">
<li>라이브 방송 초고속 HD 트랜스 코딩 기능을 사용하는 경우에 과금됩니다.
<li><a href="https://intl.cloud.tencent.com/document/product/267/31071#creating-top-speed-codec-transcoding-template">초고속 HD 트랜스 코딩</a> 기능 사용 시 비용이 발생합니다.
<li>발생 비용은 <b>트랜스 코딩 시간에 따라 과금</b>되며, 출력하는 라이브 방송 스트리밍 화면 사이즈의 범위 구간 가격을 과금 단가로 합니다.
</ul><td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604#s_trans">후불-일 결산</a></li></td>
</tr><tr>
<td>오디오 트랜스 코딩</td>
<td>
<li/>라이브 방송 오디오 트랜스 코딩 기능을 사용하는 경우에 과금됩니다.
<li/><a href="https://intl.cloud.tencent.com/document/product/267/31071#creating-pure-audio-transcoding-template">오디오 트랜스 코딩</a>, 오디오 혼합 스트림, 오디오 분리 등의 기능 사용 시 오디오 트랜스 코딩 비용이 발생합니다.
<li/>발생하는 비용은 <b>오디오 트랜스 코딩 시간에 따라 과금</b>됩니다.
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604#a_trans">후불-일 결산</a></li></td>
</tr><tr>
  <td colspan=2>라이브 방송 녹화</td>
  <td>
    <li>라이브 방송 녹화는 녹화 템플릿에 따라 생성되는 녹화 파일 형식으로 VOD에 저장됩니다.</li>
    <li>녹화로 인해 발생하는 서비스 비용은 <b>CSS 녹화 동시 피크 채널 수에 따라 과금됩니다</b>.</li>
  </td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39605">후불-월 결산</a></td>
</tr><tr>
<td colspan=2>라이브 방송 화면 캡처</td>
<td>
  <li>라이브 방송 화면 캡처는 템플릿 예약 시간에 따라 라이브 방송 스트리밍 화면을 캡처하며, 이미지는 COS에 저장됩니다.</li>
  <li>화면 캡처로 인해 발생하는 서비스 비용은 <b>화면 캡처 건수에 따라 과금되며</b>, 매월 1,000건까지 무료로 제공됩니다.</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39606">후불-월 결산</a></td>
</tr><tr>
  <td colspan=2>스마트 음란물 감지</td>
  <td>음란물 감지 화면 캡처 시 음란물 감지 비용과 화면 캡처 비용이 모두 발생합니다.
    <li>음란물 감지로 인해 발생하는 서비스 비용은 <b>음란물 감지 건수에 따라 과금되며</b>, 매월 1,000건까지 무료로 제공됩니다.</li>
    <li>화면 캡처로 인해 발생하는 서비스 비용은 <b>화면 캡처 건수에 따라 과금되며</b>, 매월 1,000건까지 무료로 제공됩니다.</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39607">후불-월 결산</a></td>
</tr><tr>
</tr>
</table>
 


<span id="extensions"></span>

## 확장 서비스 요금

<table>
<tr><th width="20%">과금 항목</th><th width="60%">과금 설명</th><th>결제 방식</th></tr>
<tr>
<td>녹화 저장</td>
<td>라이브 방송 녹화 파일은 VOD에 저장해야 합니다. 비용은<b>데이터 실제 저장 시간 및 저장량에 따라 과금되며</b>, 별도의 VOD 저장 비용이 발생합니다.</td>
<td><a href="https://intl.cloud.tencent.com/contact-sales">비즈니스 매니저에게 신청하기</a></td>
</tr><tr>
<td>화면 캡처 저장</td>
<td>라이브 방송 화면 캡처와 음란물 감지로 생성되는 화면 캡처 파일은 COS에 저장해야 합니다. 비용은 <strong>데이터 실제 저장 시간 및 저장량에 따라 과금되며</strong>, 별도의 COS 저장 비용이 발생합니다.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS - 종량제</a></td>
</tr></table>
