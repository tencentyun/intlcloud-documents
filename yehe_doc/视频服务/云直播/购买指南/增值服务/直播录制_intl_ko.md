LVB 서비스는 라이브 스트림을 녹화하며 VOD에 저장할 수 있습니다. 녹화 기능을 사용할 경우 비용이 발생하며, **당월 최대 동시 라이브 방송 녹화 채널 수를 정산 기준으로 합니다**. 

### 주의사항

- 녹화 기능은 기본적으로 꺼져 있고 콘솔 또는 클라우드 API를 통해 해당 기능을 활성화할 수 있습니다. 
- 녹화한 비디오 파일은 기본적으로 [VOD](https://console.cloud.tencent.com/vod/overview) 콘솔에 저장되며, [VOD 비용](https://intl.cloud.tencent.com/document/product/266/2838)이 발생합니다. 녹화 기능을 켠 후에는 VOD 서비스가 정상 사용 상태인지 확인해 주십시오. VOD 서비스가 활성화되어 있지 않거나 계정이 연체 상태인 경우 VOD 서비스가 중지되는 상황이 발생하여 라이브 방송을 녹화하지 못하는 상황이 발생할 수 있으며, 해당 기간에는 녹화 파일이 생성되지 않고 녹화 비용이 발생하지 않습니다.
- 최대 녹화 채널 수 계산 방식은 [라이브 방송 녹화 최대 채널 수 계산 방법](https://intl.cloud.tencent.com/document/product/267/32479)을 참조하십시오.



### 과금 가격

| 과금 유형          | 요금(USD/채널/월) |
| ------------ | ------------------ |
| 최대 녹화 채널 수 | 5.2941             |

### 과금 설명

- 과금 항목: 라이브 방송 녹화 채널 수
- 과금 방식: 후불
- 과금 주기: 일별 과금, 매월 1일~5일 지난 달 청구서를 발행하며 비용을 차감함. 자세한 사항은 요금 청구서를 기준으로 함.


### 컴퓨팅 수식

- 유효 녹화 일수 비율 = 월별 녹화 기능 사용 일수 / 해당 월의 총 일수
- 녹화 비용 = 월별 최대 동시 녹화 채널 수 × 유효 녹화 일수 비율 × 녹화 채널 단가
>? 당월 최대 동시 녹화 채널 수: 당월 5분마다 계산되는 녹화된 라이브 채널의 최대 수. 하나의 레코딩 포맷은 하나의 레코딩 스트림으로 계산됩니다. 예를 들어 동일한 스트림 ID로 MP4와 HLS 두 가지 포맷이 녹화되면 두 개의 레코딩 스트림으로 계산됩니다.

### 과금 예시

사용자 갑이 LVB 콘솔에서 A와 B 도메인(LCB 도메인 아님)에 녹화 템플릿을 설정하고 A 도메인에는 **1개** 녹화 파일 포맷, B 도메인에는 **2개** 녹화 파일 포맷을 설정했습니다. 2020년 4월 2일에 A 도메인에서 11개 채널의 라이브 방송 푸시 스트리밍이 발생하고 나머지 5일은 모두 고정적으로 10개 채널의 라이브 방송 푸시 스트리밍이 발생하며, 2020년 4월 29일에 B 도메인에서 1개 채널의 라이브 방송 푸시 스트리밍이 발생한 경우 A와 B 도메인이 녹화 기능을 사용한 일수는 다음 표와 같습니다. 

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">스트리밍 ID</th>
<th colspan=7 width="50%" style="text-align:center;">2020년 4월(1일~30일)</th>
<th rowspan=2 width="10%" style="text-align:center;">녹화 기능 사용<br>유효 일수</th>
</tr><tr>
<td style="text-align:center;">1일</td><td style="text-align:center;">2일</td><td style="text-align:center;">3일</td>
<td style="text-align:center;">……</td>
<td style="text-align:center;">28일</td><td style="text-align:center;">29일</td><td style="text-align:center;">30일</td>
</tr><tr>
<td style="text-align:center;">A</td>
<td id="ye"></td><td id="ye"></td><td id="ye"></td>
<td rowspan=13 style="text-align:center;">녹화 미진행</td>
<td id="ye"></td><td id="ye"></td><td id="ye"></td>
<td style="text-align:center;">6</td>
</tr><tr>
<td style="text-align:center;">B</td>
<td></td><td></td><td></td><td></td><td id="gr"></td><td></td>
<td style="text-align:center;">1</td>
</tr><tr>
<td style="text-align:center;">사용자 갑이<br>녹화 기능 사용</td>
<td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td>
<td style="text-align:center;">6</td>
</tr>
</tr>
</table>


- 2020년 4월 2일 녹화 최대 채널 수 **11개**, 계산 공식: A 도메인 11개 채널 × 포맷 1가지 + B 도메인 0개 채널 × 포맷 2가지 = 11개 채널
- 2020년 4월 29일 녹화 최대 채널 수 **12개**, 계산 공식: A 도메인 10개 채널 × 포맷 1가지 + B 도메인 1개 채널 × 포맷 2가지 = 12개 채널
- 2020년 4월 A 도메인의 녹화 일수는 6일, B 도메인의 녹화 일수는 1일로, 사용자 갑이 4월에 녹화 기능을 사용한 총 일수는 6일이므로, 4월 라이브 방송 녹화 유효 일수 비율 = 6일 /30일 = 0.2

또한 2020년 4월 동시 푸시 스트리밍 최대 채널 수는 12개로, 라이브 방송 녹화 유효 일수 비율은 0.2이므로 지불해야 할 2020년 4월 라이브 방송 녹화 청구서는 다음과 같습니다.
4월 라이브 방송 녹화 비용 = 5.2941(USD/채널/월) × 0.2 × 12개 채널 = 12.70584USD