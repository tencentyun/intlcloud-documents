## 라이브 방송 요금 안내

[](id:live_que1)
### CSS에는 어떤 요금 항목이 있나요? 지불해야 할 비용을 어떻게 알 수 있나요?
CSS 요금 항목에는 기본 서비스 요금과 부가 서비스 요금이 있습니다. Tencent Cloud에서는 다른 제품과 접목해 제공하는 부가 기능에 대해 서비스 확장 비용을 부과합니다.

- **기본 요금**: 트래픽/대역폭을 기준으로 과금됩니다. 즉, 가속 원본 서버와의 연결로 인해 발생하는 다운스트림 요금으로, 라이브 방송 콘텐츠를 시청하는 사용자가 있으면 트래픽/대역폭 요금이 발생합니다.
>? 트래픽 과금 방식과 대역폭 과금 방식 중 한 가지를 선택할 수 있으며 자세한 단가는 [트래픽 대역폭 과금](https://intl.cloud.tencent.com/document/product/267/2818)을 참고하십시오. 변경 방법은 [과금 변경](https://intl.cloud.tencent.com/document/product/267/30411)을 참고하십시오.
- **부가 요금**: 트랜스 코딩, 녹화, 화면 캡처, 음란물 감지 기능이 포함되며, 해당 4개 기능은 기본적으로 비활성화되어 있습니다. 해당 기능을 활성화하여 사용할 경우 이에 따른 비용이 발생하며, 자세한 단가는 [부가 서비스 요금](https://intl.cloud.tencent.com/document/product/267/2819)을 참고하십시오.
-** 확장 요금**: Tencent Cloud의 다른 제품과 결합되어 제공되는 부가 서비스로, 다른 클라우드 서비스 각각의 과금 규정에 따라 관련 비용이 청구됩니다. 부가 서비스를 이용하면 확장 서비스 요금이 부과됩니다. 자세한 단가는 [확장 서비스 요금](https://intl.cloud.tencent.com/document/product/267/2819)을 참고하십시오.

[](id:live_que2)
### 연체 여부는 어떻게 알 수 있나요?
[Tencent Cloud CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인한 후, 오른쪽 상단의 [Billing Center]을 클릭하면 요금 개요 페이지로 이동합니다. 사용 가능한 잔액이 0원 미만이면 연체 상태입니다. CSS 및 기타 서비스에 영향이 미치지 않도록 즉시 충전해 주십시오.

[](id:live_que3)
### 라이브 방송 업스트림 푸시 스트리밍은 유료인가요?
- 기본적으로 다운스트림 재생 요금만 청구됩니다. 업스트림/다운스트림 사용이 불균형한 비즈니스 시나리오(업스트림 푸시 스트림:다운스트림 재생>1:10)인 경우, 푸시 스트림의 일 피크 대역폭이 100Mbps를 초과하면 실제 푸시 스트림 사용량에 따라 별도로 푸시 스트림 요금을 청구합니다.
- 업스트림 푸시 스트림과 다운스트림 재생의 과금 방식 및 정가는 동일하며, 사용량이 일정 구간에 도달하면 개별적으로 과금됩니다. 업스트림 푸시 스트림은 2021년 7월 1일 0시부터 과금됩니다.


[](id:live_que4)
### 부가 서비스 비용은 언제부터 과금되나요?
녹화, 화면 캡처, 음란물 감지, 워터마크 등 푸시 스트리밍 도메인 관련 부가 서비스는 기능을 활성화한 후 푸시 스트리밍이 발생한 시점부터 비용이 부과됩니다. 트랜스 코딩 등 방송 도메인 부가 서비스는 방송 풀 스트리밍 시작 시점부터 과금되며(즉, 트랜스 코딩 템플릿을 생성 및 연동하고 방송 풀 스트리밍을 하지 않으면 트랜스 코딩 비용이 발생하지 않음) 클라우드단의 혼합 스트리밍은 혼합 스트리밍 작업 시작 시점부터 비용이 부과됩니다. 워터마크를 이미 추가하였거나 클라우드 단의 혼합 스트리밍 기능을 켠 경우, 표준 트랜스 코딩 비용이 발생할 수 있으며 해상도는 전송한 라이브 방송 스트리밍 해상도를 기준으로 합니다.

## 트랜스 코딩 요금 안내

[](id:tran_que1)
### 라이브 방송 트랜스 코딩의 과금 방식은 어떻게 되나요? 트랜스 코딩의 예상 비용은 어떻게 계산하나요?
CSS 트랜스 코딩은 실제 트랜스 코딩의 인코딩 방식, 해상도 및 해당 시간에 따라 과금되며, 라이브 방송 혼합 스트리밍 및 워터마크 추가 또한 트랜스 코딩 모듈을 통해 처리하므로 트랜스 코딩 비용이 발생합니다. 자세한 사항은 [트랜스 코딩 과금](https://intl.cloud.tencent.com/document/product/267/39604)을 참고하십시오.
다중 사용자가 시청하는 상황에서 동일 라이브 방송 스트리밍, 동일 비트 레이트에 대해서는 트랜스 코딩 1회 비용만 과금됩니다.

**예시:**2021년 1월 1일 라이브 방송 트랜스 코딩과 워터마크 서비스를 이용하였고, 이 중 A 라이브 방송 스트림이 H.264_720P(1시간)로 트랜스 코딩되고 B 라이브 방송 스트리밍에 워터마크를 추가(30분, 해상도 480P)했다고 가정합니다.
2021년 1월 2일 발생하는 라이브 방송 트랜스 코딩 비용은 0.0325(RMB/분) x 60(분) + 0.016(RMB/분) x 30(분) = 2.43 RMB입니다.

[](id:tran_que2)
### 라이브 방송 트랜스 코딩을 사용하지 않았는데 트랜스 코딩 청구서가 발행되는 이유는 무엇인가요?
CSS 트랜스 코딩에는 라이브 방송 실시간 트랜스 코딩, 클라우드단의 혼합 스트리밍 및 워터마크 추가 3가지 종류가 있습니다. 혼합 스트리밍 또는 워터마크 기능을 사용한 경우에도 트랜스 코딩 비용이 청구됩니다.

[](id:tran_que3)
### 라이브 방송 혼합 스트리밍은 반드시 트랜스 코딩 비용이 발생하나요?
네, 혼합 스트리밍 후 전송한 스트리밍에 따라 트랜스 코딩 비용이 발생합니다. 혼합 스트리밍 작업 완료 후 방송을 하지 않아도 트랜스 코딩 리소스가 소모되어 혼합 스트리밍 시간에 따라 요금이 부과되며, 이는 일반 트랜스 코딩 방송 시간에 따른 과금과는 다릅니다.



## 녹화 요금 안내
[](id:record_que1)
### CSS의 녹화 비용은 어떻게 되나요?
CSS 녹화 기능 비용은 당월 동시 녹화 피크를 과금 기준으로 하며, 통계 주기 내 총 녹화 채널 수가 동시 피크 수가 됩니다. 단일 라이브 방송 스트리밍을 1개 형식의 파일로 녹화하는 경우, 1개 채널로 기록됩니다. 2개 형식(MP4와 HLS)으로 녹화하는 경우 2개 채널로 기록됩니다.

[](id:record_que2)
### 라이브 방송 녹화 채널 수 피크는 어떻게 계산되나요?
1개 채널 라이브 방송 스트리밍(스트리밍 ID 1개)을 1가지 파일 형식으로 녹화, 즉 1개 채널의 라이브 방송 녹화 작업을 한다면 5분 간격으로 현재 녹화 작업 수를 확인하고 당월 표본점의 최대치를 녹화 과금 기준인 월 피크 채널 수로 정합니다.
**예시: **

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">스트리밍 ID</th>
<th rowspan=2 width="10%" style="text-align:center;">녹화 파일<br>형식</th>
<th colspan=7 width="50%" style="text-align:center;">당월(01일 - 30일)</th>
</tr><tr>
<td style="text-align:center;">01일</td><td style="text-align:center;">02일</td><td style="text-align:center;">03일</td>
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
>- 노란색: 스트리밍 ID **A** 에서의 녹화 작업.
>- 초록색: 스트리밍 ID **B** 에서의 녹화 작업.
>- 파란색: 스트리밍 ID **C** 에서의 녹화 작업.




[](id:record_que3)
### 라이브 방송 녹화 기능을 이용하였는데 60RMB가 차감된 이유는 무엇인가요? 
2개 채널에서 라이브 방송을 동시에 녹화하거나, 1개 채널에서 진행되는 라이브 방송에서 두 가지 녹화 파일 형식을 활성화한 경우에는 녹화 채널 수를 2개로 인식합니다. 녹화 요금은 녹화 채널 피크를 기준으로 청구됩니다. 채널당 한 달 요금은 30RMB로, 당월의 라이브 방송 녹화 피크 값이 2이면 60RMB의 요금이 청구됩니다. 자세한 내용은 [라이브 방송 녹화 과금 가격](https://intl.cloud.tencent.com/document/product/267/39605)을 참고하십시오.
비용 센터의 [청구서 상세 내역] > [[리소스 ID 청구서]](https://console.cloud.tencent.com/expense/bill/summary)로 이동하면 라이브 방송 녹화 항목의 청구서를 확인할 수 있습니다. 작업열에서 [청구서 상세내역]을 클릭하면 전월 실제 녹화 피크 채널 수를 확인할 수 있습니다.

