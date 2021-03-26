## 라이브 방송 과금 안내

[](id:live_que1)
### CSS에는 어떤 요금제가 있나요? 비용을 얼마나 지불해야 하나요?
CSS 요금 항목에는 기본 서비스 요금과 부가 서비스 요금이 있습니다. Tencent Cloud에서는 다른 제품과 접목해 제공하는 부가 기능에 대해 서비스 확장 비용을 부과합니다.

- **기본 요금**: 트래픽/대역폭을 기준으로 과금됩니다. 즉, 가속 원본 서버와의 연결로 인해 발생하는 다운스트림 요금으로, 라이브 방송 콘텐츠를 시청하는 사용자가 있으면 트래픽/대역폭 요금이 발생합니다.
>? 트래픽 과금 방식과 대역폭 과금 방식 중 한 가지를 선택할 수 있으며 자세한 단가는 [트래픽 대역폭 과금](https://intl.cloud.tencent.com/document/product/267/2818)을 참조하십시오. 변경 방법은 [과금 방식 변경](https://intl.cloud.tencent.com/document/product/267/30411)을 참조하십시오.
- **부가 요금**: 트랜스 코딩, 녹화, 화면 캡처, 음란물 감지 기능이 포함되며, 해당 4개 기능은 기본적으로 비활성화되어 있습니다. 해당 기능을 활성화하여 사용할 경우 이에 따른 비용이 발생하며, 자세한 단가는 [부가 서비스 요금](https://intl.cloud.tencent.com/document/product/267/2819)를 참조하십시오.
- **확장 요금**: Tencent Cloud의 다른 제품과 결합되어 제공되는 부가 서비스로, 다른 클라우드 서비스 각각의 과금 규정에 따라 관련 비용이 청구됩니다. 부가 서비스를 이용하면 확장 서비스 요금이 부과됩니다. 자세한 단가는 [확장 서비스 요금](https://intl.cloud.tencent.com/document/product/267/2819)을 참조하십시오.

[](id:live_que2)
### 연체 여부는 어떻게 알 수 있나요?
[Tencent CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인한 후, 오른쪽 상단의 [Billing Center]를 클릭하여 요금 개요 페이지로 들어갑니다. 사용 가능한 잔액이 0USD 미만인 경우 연체 상태가 됩니다. CSS 및 기타 서비스에 영향이 미치지 않도록 즉시 충전해 주십시오.

[](id:live_que3)
### 라이브 방송 업스트림 푸시 스트리밍은 유료인가요?
CSS 업스트림 푸시 스트리밍은 무료이며 다운스트림의 트래픽만 유료입니다.

[](id:live_que4)
### 부가 서비스 비용은 언제부터 과금되나요?
녹화, 화면 캡처, 음란물 감지, 워터마크 등 푸시 도메인 관련 부가 서비스는 기능을 활성화한 후 푸시 스트리밍이 발생한 시점부터 비용이 부과됩니다. 트랜스 코딩 등 방송 도메인 부가 서비스는 방송 풀 스트리밍 시작 시점부터 과금되며(즉, 트랜스 코딩 템플릿을 생성 및 연동하고 방송 풀 스트리밍을 하지 않으면 트랜스 코딩 비용이 발생하지 않음) 클라우드 혼합 스트리밍은 혼합 스트리밍 작업의 시작 시점부터 비용이 부과됩니다. 워터마크를 이미 추가하였거나 클라우드 혼합 스트리밍 기능을 켠 경우, 표준 트랜스 코딩 비용이 발생할 수 있으며 해상도는 전송한 라이브 방송 스트리밍 해상도를 기준으로 합니다.



## 트랜스 코딩 요금안내

[](id:tran_que1)
### 라이브 방송 트랜스 코딩의 과금은 어떤 방식으로 이루어지나요? 트랜스 코딩 예상 요금은 어떻게 산정하나요?
CSS 트랜스 코딩은 실제 트랜스 코딩의 코딩 방식, 해상도 및 해당 시간에 따라 과금되며, 라이브 방송 혼합 스트리밍 및 워터마크 추가 또한 트랜스 코딩 모듈을 통해 처리하므로 트랜스 코딩 비용이 발생합니다. 자세한 사항은 [트랜스 코딩 과금](https://intl.cloud.tencent.com/document/product/267/39604)을 참조하십시오.
다수의 사용자가 시청하는 경우 동일 라이브 방송 스트리밍과 동일 부호율에 대해서는 트랜스 코딩 1회 분만 과금됩니다.

2021년 1월 1일 라이브 방송 트랜스 코딩과 워터마크 서비스를 이용하였고, 이 중 A 라이브 방송 스트림이 H.264_720P(1시간)로 트랜스 코딩되고 B 라이브 방송 스트리밍에 워터마크를 추가(30분, 해상도 480P)했다고 가정한 경우입니다.
2021년 1월 2일 발생하는 라이브 방송 트랜스 코딩 비용은 0.0057(USD/분) × 60(분) + 0.0028(USD/분) × 30(분) = 0.426 USD입니다.

[](id:tran_que2)
### 라이브 방송 트랜스 코딩을 사용하지 않았는데 왜 트랜스 코딩 청구서가 발행된 건가요?
CSS 트랜스 코딩에는 라이브 방송 실시간 트랜스 코딩, 클라우드 혼합 스트리밍 및 워터마크 추가의 3가지 종류가 있으며, 혼합 스트리밍 또는 워터마크 기능을 사용한 경우 트랜스 코딩 비용이 청구됩니다.

[](id:tran_que3)
### 라이브 방송 혼합 스트리밍에는 반드시 트랜스 코딩 비용이 발생하나요?
네, 혼합 스트리밍 후 전송한 스트리밍에 따라 트랜스 코딩 비용이 발생합니다. 혼합 스트리밍 작업 완료 후 방송을 하지 않아도 트랜스 코딩 리소스가 소모되어 혼합 스트리밍 시간에 따라 요금이 부과되며, 이는 일반 트랜스 코딩 방송 시간에 따른 과금과는 다릅니다.



## 녹화 요금안내
[](id:record_que1)
### CSS의 녹화 비용은 얼마인가요?
CSS 녹화 기능 비용은 당월 동시 녹화 피크를 기준으로 과금되며, 통계 주기 내 총 녹화 채널 수가 동시 피크 수가 됩니다. 하나의 파일 포맷으로 단일 라이브 방송 스트리밍을 녹화하는 경우 1개의 녹화로 기록되고, 2가지 포맷(MP4와 HLS)으로 녹화하는 경우에는 2개의 녹화로 기록됩니다.

[](id:record_que2)
### 라이브 방송 녹화 채널 수 피크는 어떻게 계산되나요?
1개 채널 라이브 방송 스트리밍(스트리밍 ID 1개)을 1가지 파일 형식으로 녹화하면, 즉 1개 채널의 라이브 방송 녹화 작업을 수행하면 5분 간격으로 현재 녹화되는 작업의 개수를 확인하고 당월 샘플 지점의 최대치를 녹화 과금 기준인 월 피크 채널 수로 정합니다.
**예시:**

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">스트리밍 ID</th>
<th rowspan=2 width="10%" style="text-align:center;">녹화 파일<br>포맷</th>
<th colspan=7 width="50%" style="text-align:center;">당월(1일~30일)</th>
</tr><tr>
<td style="text-align:center;">1일</td><td style="text-align:center;">2일</td><td style="text-align:center;">3일</td>
<td style="text-align:center;">……</td>
<td style="text-align:center;">28일</td><td style="text-align:center;">29일</td><td style="text-align:center;">30일</td>
</tr><tr>
<td rowspan=4 style="text-align:center;">A</td>
<td style="text-align:center;">HLS</td><td></td><td></td><td></td>
<td rowspan=13 style="text-align:center;">녹화 미진행</td>
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
<td colspan=2 style="text-align:center;">녹화 채널 수 피크</td><td colspan=7 style="text-align:center;">11</td>
</tr>
</table>

>? 
>- 노란색: 스트리밍 ID **A** 에서의 녹화 작업
>- 초록색: 스트리밍 ID **B** 에서의 녹화 작업
>- 파란색: 스트리밍 ID **C** 에서의 녹화 작업




[](id:record_que3)
### 라이브 방송 녹화 기능을 이용하였는데 10.5882USD가 차감됐습니다. 그 이유가 궁금합니다. 
두 개의 채널에서 라이브 방송을 동시에 녹화하거나, 한 채널에서 진행되는 라이브 방송에서 두 가지 녹화 파일 형식을 활성화한 경우에는 녹화 채널 수를 두 개로 인식합니다. 녹화 요금은 녹화 채널 피크를 기준으로 청구됩니다. 채널당 한 달 요금은 5.2941USD로, 당월의 라이브 방송 녹화 피크 값이 2이면 10.5882USD의 요금이 청구됩니다. 자세한 내용은 [라이브 방송 녹화 과금](https://intl.cloud.tencent.com/document/product/267/39605)을 참조하십시오.
과금 센터의 [청구서 상세내역] > [[자원 ID 청구서]](https://console.cloud.tencent.com/expense/bill/summary)로 이동하면 라이브 방송 녹화 항목의 청구서를 확인할 수 있습니다. 작업란에서 [청구서 상세내역]을 클릭하면 이전 달의 실제 녹화 피크 채널 수를 확인할 수 있습니다.

