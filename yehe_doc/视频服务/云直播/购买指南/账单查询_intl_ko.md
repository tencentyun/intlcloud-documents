Tencent LVB(CSS)에서 발생한 청구서 및 사용 명세서는 Tencent Cloud [Bills]>[Bill Details](https://console.cloud.tencent.com/expense/bill/summary)에서 조회할 수 있습니다.
청구서 상세에는 [리소스 ID 청구서](#resources_id) 및 [청구 명세서](#detail)가 포함되어 있습니다.
- 리소스 ID 청구서: 리소스 ID별 명세 내역을 취합한 청구서입니다.
- 청구 명세서: 취합하지 않은 각 비용의 명세 기록입니다.

<span id="resources_id"></span>

## 리소스 ID 청구서

1. [Bill by Instance]를 클릭해 탭으로 이동합니다.
2. [All products] 필터 클릭 후 [LVB CSS]를 선택하여 LVB의 리소스 ID 청구서를 조회할 수 있습니다.

![](https://main.qcloudimg.com/raw/9db167f7285dfaf82d83a9028d589ad8.png)

#### 청구서 필드

<table>
<thead>
<tr>
<th>필드</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>거래 유형</td>
<td><ul style="margin:0;">
    <li>종량제: 일 결산 과금 방식, 일별로 요금 결산</li>
    <li>월 결산: 월 결산 과금 방식, 월별로 전체 요금 결산</li>
    </td>
</tr>
<tr>
<td>설정 설명</td>
<td>이번 달에 사용자가 LVB에서 사용한 하위 기능 항목 및 사용량은 다음과 같습니다.<ul style="margin:0;">
    <li>라이브 방송 트랜스 코딩</li>
    <li>라이브 방송 녹화</li>
    <li>라이브 방송 화면 캡처</li>
    <li>스마트 음란물 감지</li>
    </ul></td>
</tr>
<tr>
<td>원가</td>
<td>이번 달 사용한 하위 기능 항목별 총 요금</td>
</tr>
<tr>
<td>할인율</td>
<td>이번 달 사용자가 받은 할인 혜택은 다음과 같습니다.<ul style="margin:0;"><li>일 결산 사용자에게는 할인 혜택이 제공되지 않습니다. 할인율: 1</li></ul></td>
</tr>
<tr>
<td>총 요금</td>
<td>총 요금 = 원가 × 할인율</td>
</tr>
</tbody></table>

>? 나머지 필드는 모두 Tencent Cloud 공식 사이트의 할당 필드입니다. 자세한 내용은 [신규 버전 청구서 사용 가이드](https://intl.cloud.tencent.com/document/product/555/7432)를 참조하십시오.

<span id="detail"></span>

## 청구 명세서

1. [청구 명세서]를 클릭해 탭으로 이동합니다.
2. [모든 제품] 필터 클릭 후 [LVB CSS]를 선택하여 LVB의 청구서를 조회할 수 있습니다.

![](https://main.qcloudimg.com/raw/0716954d4d5a955a77acd4149961ca1b.png)

#### 청구서 필드

| 필드       | 설명                                                         |
| :--------- | :----------------------------------------------------------- |
| 모듈 유형   | 이번 달 LVB에서 사용한 각 하위 기능 항목                                 |
| 모듈 명칭   | 해당 모듈 유형에서 사용한 기능 항목                                 |
| 모듈 정가 | 해당 모듈에는 할인된 정가 가격이 존재하지 않습니다                                   |
| 모듈 사용량   | 해당 모듈의 사용량                                               |
| 할인율     | 이번 달 사용자가 받은 할인 혜택: 일 결산 사용자에게는 할인 혜택이 제공되지 않으며 할인율은 1입니다. 월 결산 사용자에게 할인 혜택이 제공되며, 상세 할인 내역은 비즈니스 매니저에게 문의하십시오. |
| 사용 기간   | 이번 달 모듈별 총 사용 시간                                     |
| 총 요금     | 총 요금 = 모듈 원가 × 할인율. 그중: 모듈 원가 = 모듈 정가 × 사용시간 |

>? 나머지 필드는 모두 Tencent Cloud 공식 사이트의 할당 필드입니다. 자세한 내용은 [신규 버전 청구서 사용 가이드](https://intl.cloud.tencent.com/document/product/555/7432)를 참조하십시오.

