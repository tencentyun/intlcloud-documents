## 라이브 스트리밍
[](id:live_que1)
### CSS 과금 항목은 무엇인가요? 어떤 요금을 지불해야 하나요?
CSS의 과금 항목에는 기본 서비스와 부가 서비스가 포함됩니다. 다른 Tencent Cloud 제품의 기능에 의존하는 CSS 기능을 사용하는 경우에도 확장 서비스 요금이 부과됩니다.

- **기본 서비스 요금**: 캐시 원본 서버와 연결하기 위해 소비된 다운스트림 트래픽/대역폭을 기준으로 과금됩니다. 라이브 스트림이 재생될 때마다 트래픽/대역폭이 소비됩니다.
>? CSS는 트래픽별 과금 및 대역폭별 과금의 두 가지 과금 모드를 제공합니다. 과금 내역은 [기본 서비스](https://intl.cloud.tencent.com/document/product/267/2818)를 참고하십시오. 결제 방식을 변경하려면 [과금 변경](https://intl.cloud.tencent.com/document/product/267/30411)을 참고하십시오.

- **부가 서비스 요금**: 트랜스 코딩, 녹화, 화면 캡처, 음란물 감지 기능을 사용하는 경우 발생합니다. 이 기능은 기본적으로 비활성화되어 있습니다. 자세한 단가는 [부가 가치 서비스 요금](https://intl.cloud.tencent.com/document/product/267/2819)을 참고하십시오.
- **연장 서비스 요금**: 다른 Tencent Cloud 제품의 기능에 의존하는 CSS 기능을 사용하는 경우 발생합니다. 해당 제품의 과금 규정에 따라 요금이 부과됩니다. 자세한 단가는 [가격 리스트](https://intl.cloud.tencent.com/document/product/267/2819)를 참고하십시오.

[](id:live_que2)
### 내 계정에 연체된 결제가 있는지 어떻게 알 수 있나요?
[Tencent Cloud CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인한 후, 오른쪽 상단의 **Billing Center**를 클릭하여 잔액을 확인합니다. 사용 가능한 잔액이 마이너스인 경우 계정에 연체된 결제가 있습니다. CSS 및 기타 서비스를 계속 사용하려면 즉시 충전해 주십시오.

[](id:live_que3)
### 스트림 푸시에 대해 요금이 부과되나요?
- 기본적으로 요금은 다운스트림 사용량에 따라 과금됩니다. 그러나 업스트림 트래픽에 대한 다운스트림 트래픽의 비율이 10:1 미만이고 하루에 사용된 최대 업스트림 대역폭이 100Mbps를 초과하는 경우에도 업스트림 사용량에 대한 요금이 과금됩니다.
- 업스트림 사용에 대한 과금 방식, 정가 및 구간별 가격 책정 규칙은 다운스트림 사용과 동일합니다. 다운스트림 사용량은 2021년 7월 1일 00:00(UTC+08:00)부터 과금되었습니다.

[](id:live_que4)
### 부가 서비스 요금은 언제 발생하나요?
녹화, 화면 캡처, 음란물 감지, 워터마크 템플릿을 푸시 도메인에 바인딩하는 경우 스트림 푸시 시 요금이 발생합니다. 템플릿을 재생 도메인에 바인딩하면 스트림 재생 시 요금이 발생합니다. 즉, 트랜스코딩 템플릿을 만들고 재생 도메인 이름에 바인딩하는 경우 재생에 도메인을 사용하지 않는 한 트랜스코딩 요금이 부과되지 않습니다. 워터마크 또는 스트림 믹스 기능을 사용하면 출력 스트림의 해상도에 따라 표준 트랜스코딩 요금이 발생할 수 있습니다.

[](id:live_que7)
### 음란물 감지에 두 가지 비용이 있습니까?
CSS는 라이브 스트림의 스크린샷을 분석하여 음란물 콘텐츠를 감지하므로 음란물 감지 기능을 사용하면 **화면 캡처** 및 **음란물 감지**의 두 가지 비용이 발생합니다. 음란물 감지 요금은 분석된 스크린샷 수를 기준으로 합니다.
- CSS는 화면 캡처 기능에 대해 월 1000장의 스크린샷 프리 티어를 제공합니다. 1,000장 초과분에 대해서만 과금합니다.
- CSS 음란물 감지를 위해 매월 1000장의 스크린샷 프리 티어를 제공합니다. 1,000장 초과분에 대해서만 과금합니다.

자세한 내용은 [라이브 방송 화면 캡처](https://intl.cloud.tencent.com/document/product/267/39606) 및 [스마트 음란물 감지](https://intl.cloud.tencent.com/document/product/267/39607)를 참고하십시오.

[](id:live_que9)
### CSS 패키지 사용을 실시간으로 모니터링할 수 있나요?
[CSS 콘솔](https://console.cloud.tencent.com/live/resources/package?type=traffic)에서 패키지 사용량을 볼 수 있지만 실시간 사용량 통계는 현재 지원되지 않습니다.
매일 사용량은 다음 날 시스템에서 처리될 때까지 데이터에 반영되지 않습니다(정확한 시간은 다를 수 있음).

[](id:live_que10)
### 유료 사용자만 내 콘텐츠에 액세스하도록 허용할 수 있습니까?
CSS는 현재 유료 사용자를 식별할 수 없습니다. 실시간 스트리밍을 녹화하여 VOD에 저장하면 동영상을 암호화하여 유료 사용자만 콘텐츠에 액세스하도록 할 수 있습니다.



[](id:live_que12)
### 콘솔에 표시되는 트래픽 사용량 데이터가 로그 데이터와 다른 이유는 무엇인가요?

로그에 기록되는 다운스트림 트래픽은 응용 레이어 데이터입니다. 소비되는 실제 트래픽은 애플리케이션 계층 데이터보다 5% - 15% 더 많습니다.

- TCP/IP 헤더: 각 TCP/IP HTTP 요청 패킷은 40바이트 TCP 및 IP 헤더를 포함하여 최대 1500바이트일 수 있습니다. 헤더가 소비하는 트래픽(전체의 약 3%)은 응용 레이어 데이터에 포함되지 않습니다.
- TCP 재전송: 약 3~10%의 패킷이 전송 중에 손실됩니다. 패킷은 서버에서 다시 전송됩니다. 이러한 트래픽(전체의 약 3-7%)은 응용 레이어에서도 계산되지 않습니다.

업계 표준에 따라 과금 가능 트래픽은 응용 레이어 트래픽에 위에서 설명한 추가 트래픽을 더한 것입니다. Tencent Cloud는 추가 트래픽을 전체 트래픽의 10%로 계산하므로 콘솔에 표시되는 트래픽 사용량은 로그에 기록된 트래픽 사용량의 110%입니다.

## 선불 패키지

[](id:pack_que2)
### 트래픽 패키지를 구매했는데도 계정 잔액에서 요금이 차감되는 이유는 무엇입니까?

트래픽 패키지는 일 결산 트래픽 후불 과금 방식에서만 트래픽 사용량을 차감할 수 있습니다.
- 일 결산 대역폭 과금 방식인 경우 트래픽 패키지를 차감에 사용할 수 없습니다. 콘솔에서 과금 방식을 변경할 수 있습니다. 자세한 내용은 [과금 변경](https://intl.cloud.tencent.com/document/product/267/30411)을 참고하십시오.
- 일일 트래픽 과금 방식을 사용 중이고 여전히 계정 잔액에서 요금이 차감되는 경우 라이브 트랜스코딩, 라이브 녹화, 스크린 캡처, 음란물 감지와 같은 [부가 가치 서비스](https://intl.cloud.tencent.com/document/product/267/2819)를 사용했는지 확인하십시오. 부가 서비스는 사용량에 따라 요금이 과금됩니다. 매일 사용량은 다음 날에 과금됩니다. 부가 서비스를 위한 패키지를 구입할 수도 있습니다. CSS는 트래픽 패키지, 표준 트랜스코딩 패키지 및 TSC(Top Speed Codec) 트랜스코딩 패키지의 세 가지 유형의 패키지를 제공합니다. 자세한 내용은 [선불 패키지](https://www.tencentcloud.com/document/product/267/52220)를 참고하십시오.
- 패키지를 다 사용한 후에도 요금이 발생합니다. [**청구서 내역**](https://console.cloud.tencent.com/expense/bill/summary) > **청구 명세서**를 조회하실 수 있습니다. 자세한 방법은 [청구서 조회](https://intl.cloud.tencent.com/document/product/267/36278)를 참고하십시오.


[](id:pack_que3)
### 트래픽 패키지만 구매했습니다. 패키지를 모두 사용한 후 CSS에서 내 계정에 대한 서비스를 일시 중단합니까?
아니요. 트래픽 패키지는 선불이며 사용량은 구매한 패키지에서 차감됩니다.

- LVB에 대한 과금 방식이 트래픽 일 결산 후불 과금 방식인 경우 다운스트림 LVB 트래픽은 먼저 트래픽 패키지에서 차감되고 추가 사용량은 구간별 종량제 요금으로 매일 과금됩니다.
- 패키지를 다 사용한 후에는 계정에 일일 선불 요금을 지불할 수 있는 충분한 잔액이 있는지 확인하십시오. 연체된 결제가 있는 경우 24시간 이내에 충전하십시오. 그렇지 않으면 귀하의 계정에 대한 서비스가 일시 중지됩니다. [계정 잔액](https://console.cloud.tencent.com/expense/overview)을 정기적으로 확인하는 것이 좋습니다.

>? 트래픽 패키지는 월별 트래픽 과금 방식 또는 월별/일별 대역폭별 과금 방식인 경우 차감에 사용할 수 없습니다.

## 트랜스 코딩

[](id:tran_que1)
### 라이브 트랜스코딩 요금은 어떻게 과금되나요? 요금은 어떻게 추정할 수 있습니까?
라이브 트랜스코딩 요금은 트랜스코딩 코덱, 해상도 및 기간에 따라 다릅니다. 스트림 믹싱 및 워터마크는 트랜스코딩 모듈에 의해 구현되기 때문에 이 두 기능을 사용하면 트랜스코딩 비용도 발생합니다. 자세한 내용은 [라이브 트랜스코딩](https://intl.cloud.tencent.com/document/product/267/39604)을 참고하십시오.
트랜스코딩 요금은 여러 시청자가 동일한 비트레이트로 동일한 라이브 스트림을 시청하는 경우 한 번만 과금됩니다.

**예시:** 2021년 01월 01일 스트림 A를 H.264_720P(1시간)로 트랜스코딩하고 스트림 B에 워터마크를 추가했다고 가정합니다(30분, 출력 해상도: 480P). 
2021년 01월 02일 트랜스코딩 요금은 0.0057(USD/분) × 60(분) + 0.0028(USD/분) × 30(분) = 0.426 USD입니다.

[](id:tran_que2)
### 라이브 트랜스코딩 기능을 사용하지 않았습니다. 트랜스코딩 요금이 발생한 이유는 무엇입니까?
트랜스코딩 서비스에는 라이브 트랜스코딩, 스트림 믹싱 및 워터마크가 포함됩니다. 스트림 믹싱 또는 워터마크 기능을 사용하면 트랜스코딩 비용도 발생합니다.

[](id:tran_que3)
### 스트림 믹싱에는 항상 트랜스코딩 요금이 발생하나요?
예. 출력 스트림 재생 여부와 관계없이 스트림 믹싱 중에 트랜스코딩 리소스가 소비되기 때문에 스트림 믹싱은 출력 시간을 기준으로 요금이 과금됩니다. 이는 재생 시간을 기반으로 하는 라이브 트랜스코딩 과금과 다릅니다.

## 라이브 녹화
[](id:record_que1)
### 실시간 녹화 요금은 어떻게 과금되나요?
실시간 녹화 요금은 이번 달 최대 동시 녹화 채널 수를 기준으로 과금됩니다. 하나의 파일 형식으로 녹화된 단일 라이브 스트림은 하나의 녹화 채널로 계산됩니다. 두 가지 형식(MP4 및 HLS)으로 녹화하는 경우 두 개의 녹화 채널로 계산됩니다.

[](id:record_que2)
### 최대 동시 녹화 채널 수는 어떻게 계산되나요?
하나의 형식으로 녹음된 하나의 스트림(스트림 ID)은 하나의 녹음 채널로 계산됩니다. 동시 녹화 채널 수는 5분 간격으로 수집되며, 매월 최대 개수가 과금에 사용됩니다.
**예시:**

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">스트림 ID</th>
<th rowspan=2 width="10%" style="text-align:center;">녹화<br>형식</th>
<th colspan=7 width="50%" style="text-align:center;">당월(01일 - 30일)</th>
</tr><tr>
<td style="text-align:center;">01일</td><td style="text-align:center;">02일</td><td style="text-align:center;">03일</td>
<td style="text-align:center;">……</td>
<td style="text-align:center;">28일</td><td style="text-align:center;">29일</td><td style="text-align:center;">30일</td>
</tr><tr>
<td rowspan=4 style="text-align:center;">A</td>
<td style="text-align:center;">HLS</td><td></td><td></td><td></td>
<td rowspan=13 style="text-align:center;">녹화 작업 없음</td>
<td id="ye"></td><td id="ye"></td>
<td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td>
</tr><tr>
<td rowspan=4 style="text-align:center;">B</td>
<td style="text-align:center;">HLS</td><td></td><td id="gr"></td><td id="gr"></td><td id="gr"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td id="gr"></td><td id="gr"></td><td></td><td id="gr"></td><td id="gr"></td><td></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td></td><td id="gr"></td><td></td><td id="gr"></td><td></td><td id="gr"></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td></td><td id="gr"></td><td></td><td id="gr"></td><td></td><td></td>
</tr><tr>
<td rowspan=4 style="text-align:center;">C</td>
<td style="text-align:center;">HLS</td><td id="br"></td><td></td><td id="br"></td><td id="br"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td></td><td></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td></td><td></td><td></td><td id="br"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td></td><td></td><td></td><td></td><td></td><td id="br"></td>
</tr><tr>
<td colspan=2 style="text-align:center;">녹화 채널 수</td>
<td style="text-align:center;">5</td><td style="text-align:center;">7</td><td style="text-align:center;">6</td><td style="text-align:center;">11</td><td style="text-align:center;">6</td><td style="text-align:center;">5</td>
</tr><tr>
<td colspan=2 style="text-align:center;">최대 녹화 채널 수</td><td colspan=7 style="text-align:center;">11</td>
</tr>
</table>

>? 
>- 노란색: 스트림 **A**에 대한 작업을 기록합니다.
>- 녹색: 스트림 **B**에 대한 작업을 기록합니다.
>- 파란색: 스트림 **C**에 대한 작업을 기록합니다.

[](id:record_que3)
### 라이브 녹화를 사용한 후 10.5882 USD가 과금된 이유는 무엇인가요? 
2개의 라이브 스트림이 동시에 녹화되거나 하나의 라이브 스트림이 두 가지 형식으로 녹화되면 2개의 동시 녹화 채널이 있습니다. 라이브 녹화는 채널당 5.2941 USD로 매달 최대 동시 녹화 채널 수를 기준으로 과금됩니다. 따라서 한 달에 최대 2개의 동시 녹화 채널이 있는 경우 해당 월의 녹화 요금은 10.5882 USD가 됩니다. 자세한 내용은 [라이브 방송 녹화](https://intl.cloud.tencent.com/document/product/267/39605)를 참고하십시오.
이전 달의 최대 동시 녹화 채널 수를 보려면 **청구서 상세 내역** > [**리소스 ID별 청구서**](https://console.cloud.tencent.com/expense/bill/summary)로 이동하여 작업 열에서 **청구서 상세 내역**을 클릭하십시오.