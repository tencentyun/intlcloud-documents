CSS는 라이브 스트림을 녹화하고 VOD에 저장할 수 있습니다. 라이브 녹화를 사용하면 요금이 부과됩니다. **라이브 녹화는 해당 월의 최대 동시 녹화 채널 수에 따라 요금이 청구됩니다**.

### 주의 사항

- 녹화 기능은 기본적으로 비활성화되어 있으며 콘솔 또는 TencentCloud API를 통해 활성화할 수 있습니다.
- 녹화된 비디오 파일은 기본적으로 [VOD](https://console.cloud.tencent.com/vod/overview) 콘솔에 저장되며 [VOD 요금](https://intl.cloud.tencent.com/document/product/266/2838)이 부과됩니다. 녹화 기능을 활성화한 후 VOD 서비스가 정상 상태인지 확인하십시오. 활성화되어 있지 않거나 미결제로 인해 정지된 경우 라이브 녹화가 불가능하며 녹화 파일이 생성되지 않으며 녹화 요금도 발생하지 않습니다.
- 최대 녹화 채널 수 계산 방식은 [라이브 방송 과금](https://intl.cloud.tencent.com/document/product/267/32479)을 참고하십시오.


### 과금 가격

| 과금 항목     | 가격(USD/채널/월) |
| ------------ | ------------------ |
| 최대 녹화 채널 수 |5.2941             |

### 과금 안내

- 과금 항목: 라이브 녹화 채널 수.
- 과금 방식: 종량제 후불.
- 과금 주기: 월간. 매월 발생한 녹화 요금은 다음 달 1일 - 5일 이내에 차감됩니다. 자세한 내용은 청구서를 참고하십시오.


### 계산 공식

- 녹화 일수 비율 = 월별 녹화 기능 사용 일수 / 해당 월의 총 일수.
- 녹화 요금 = 월별 최대 동시 녹화 채널 수 × 녹화 일수 비율 × 단가.
>? 한 달 동안의 최대 동시 녹화 채널 수: 해당 월에 동시에 발생하는 최대 녹화 채널 수입니다(5분 간격으로 데이터 수집). 각 녹화 형식은 하나의 녹화 채널로 계산됩니다. 예를 들어, 동일한 스트림이 MP4 및 HLS에 녹화된 경우 두 개의 녹음 채널로 계산됩니다.

### 과금 예시

사용자 A가 CSS 콘솔에서 도메인 A와 도메인 B에 녹화 템플릿을 바인딩했다고 가정합니다. 템플릿에 따라 도메인 A의 스트림은 **하나**의 형식으로 녹화되고 도메인 B의 스트림은 **두 가지** 형식으로 녹화됩니다. 도메인 A는 2020년 04월 02일 11개의 라이브 스트림을, 그 달의 또 다른 5일 동안 10개의 라이브 스트림이 있었습니다. 도메인 B는 2020년 04월 29일 하나의 라이브 스트림이 있었습니다. 04월 도메인 A와 도메인 B의 녹화 일수는 다음과 같습니다. 

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">스트림 ID</th>
<th colspan=7 width="50%" style="text-align:center;">2020년 04월(01일 - 30일)</th>
<th rowspan=2 width="10%" style="text-align:center;">녹화 기능을 사용한<br>유효 일수</th>
</tr><tr>
<td style="text-align:center;">01일</td><td style="text-align:center;">02일</td><td style="text-align:center;">03일</td>
<td style="text-align:center;">……</td>
<td style="text-align:center;">28일</td><td style="text-align:center;">29일</td><td style="text-align:center;">30일</td>
</tr><tr>
<td style="text-align:center;">A</td>
<td id="ye"></td><td id="ye"></td><td id="ye"></td>
<td rowspan=13 style="text-align:center;">녹화 작업 없음</td>
<td id="ye"></td><td id="ye"></td><td id="ye"></td>
<td style="text-align:center;">6</td>
</tr><tr>
<td style="text-align:center;">B</td>
<td></td><td></td><td></td><td></td><td id="gr"></td><td></td>
<td style="text-align:center;">1</td>
</tr><tr>
<td style="text-align:center;">사용자 A<br>녹화 기능 사용</td>
<td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td>
<td style="text-align:center;">6</td>
</tr>
</tr>
</table>


- 2020년 04월 02일의 피크 녹화 채널 수는 **11개**입니다(도메인 A x 1 형식의 11개 채널 + 도메인 B의 0개 채널 x 2 형식 = 11개 채널).
- 2020년 04월 29일의 피크 녹화 채널 수는 **12개**입니다(도메인 A 10개 채널 x 1 형식 + 도메인 B 1개 채널 x 2개 형식 = 12개 채널).
- 2020년 04월 도메인 A와 도메인 B의 녹화 일수는 각각 6일과 1일입니다. 사용자 A의 녹화 일수는 6일이며, 04월의 녹화 일수 비율은 6일 / 30일 = 0.2입니다.

따라서 2020년 04월 최대 동시 녹화 채널 수는 12개이며, 녹화 일수 비율은 0.2이며, 발생하는 라이브 녹화 요금은 다음과 같습니다.
04월 라이브 녹화 요금 = 5.2941(USD/채널/월) x 0.2 x 12개 채널 = 12.70584 USD.

## COS에 녹화

### 과금 가격

CSS 스트림을 COS에 녹화하는 경우 각 녹화 채널의 녹화 시간에 따라 추가 요금이 과금됩니다.

| 과금 항목          | 가격(USD/분/월) |
| ----------------- | -------------------- |
| COS에 녹화 | 0.000096             |

### 과금 세부 정보

- 과금 항목: COS에 녹화
- 과금 방식: 종량제 후불.
- 과금 주기: 월간. 매월 발생하는 COS 녹화 요금은 다음 달 1일 - 5일 이내에 차감됩니다. 자세한 내용은 청구서를 참고하십시오.

### 과금 예시

사용자가 CSS 콘솔에서 도메인 A와 도메인 B에 녹화 템플릿을 바인딩했다고 가정합니다. 템플릿에 따라 도메인 A의 스트림은 하나의 형식으로 녹화되고 도메인 B의 스트림은 두 가지 형식으로 녹화됩니다. 도메인 A는 2023년 01월 13일에 30분 동안 지속된 10개의 라이브 스트림이 있었습니다. 도메인 B는 2023년 01월 20일에 20분 동안 지속된 하나의 라이브 스트림이 있었습니다. 이와 같이 가정할 때, 2023년 01월에 발생하는 COS 녹화 요금은 다음과 같습니다.
`0.000096(USD/분/월) x (채널 10개 x 형식 1개 x 30분 + 채널 1개 x 형식 2개 x 20분) = 0.03264 USD`.