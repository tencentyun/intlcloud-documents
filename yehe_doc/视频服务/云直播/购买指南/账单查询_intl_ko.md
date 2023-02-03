CSS 청구서 및 결제 세부 정보를 보려면 Tencent Cloud 콘솔에서 **요금 청구서>[청구서 세부 정보](https://console.cloud.tencent.com/expense/bill/summary)**로 이동하십시오.
청구서 세부 정보 페이지에는 [리소스 ID별 청구서](#resources_id) 및 [청구 명세서](#detail) 탭이 있습니다.
- 리소스 ID별 청구서: 리소스 ID별로 집계된 청구서를 표시합니다.
- 청구 명세서: 집계를 수행하지 않고 각 차감 내역을 표시합니다.

[](id:resources_id)
## 리소스 ID별 청구서
1. **리소스 ID별 청구서** 탭을 클릭합니다.
2. **모든 제품**을 클릭한 다음 **CSS**를 선택하면 리소스 ID별 청구서를 볼 수 있습니다.
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
<td><ul style="margin:0;">
    <li>종량제: 일 결산 과금 방식, 매일 요금 차감</li>
    <li>월 결산: 매월 월별 요금 차감</li>
    <li>정액 과금제: CSS 리소스 패키지</li></ul>
    </td>
</tr>
<tr>
<td>구성 설명</td>
<td>이번 달에 사용된 CSS 기능 및 사용량:<ul style="margin:0;">
    <li>라이브 방송 트랜스 코딩</li>
    <li>라이브 방송 녹화</li>
    <li>라이브 방송 화면 캡처</li>
    <li>스마트 음란물 감지</li>
    </ul></td>
</tr>
<tr>
<td>원가</td>
<td>당월에 CSS 기능을 사용한 총 요금</td>
</tr>
<tr>
<td>할인율</td>
<td>당월 할인 혜택: 일 결산 과금 주기의 사용자에게는 할인 혜택이 제공되지 않으므로 할인율은 1입니다.</td>
</tr>
<tr>
<td>총 요금</td>
<td>총 요금 = 원가 × 할인율</td>
</tr>
</tbody></table>

>? 다른 필드는 Tencent Cloud에서 할당합니다. 자세한 내용은 [About Billing](https://intl.cloud.tencent.com/document/product/555)을 참고하십시오.

[](id:detail)
## 청구 명세서
1. ** 청구 명세서** 탭을 클릭합니다.
2. **모든 제품**을 클릭한 다음 **CSS**를 선택하면 CSS 청구서의 세부 정보를 볼 수 있습니다.

![](https://main.qcloudimg.com/raw/0716954d4d5a955a77acd4149961ca1b.png)

#### 청구서 필드

| 필드       | 설명                                                         |
| :--------- | :----------------------------------------------------------- |
| 컴포넌트 유형   | 이번 달에 사용한 CSS 기능                                 |
| 컴포넌트 이름   | 사용된 기능의 서브 항목                                 |
| 컴포넌트 정가 | 할인이 적용되지 않은 컴포넌트의 정가                                   |
| 컴포넌트 사용량   | 컴포넌트의 사용량                                               |
| 할인율     | 해당 월의 할인 혜택: 일 결산 청구 사용자에게는 할인 혜택이 제공되지 않으므로 할인율은 1입니다. 월 결산 청구 사용자에게는 할인 혜택이 제공됩니다. 상세 할인 내역은 영업팀에 문의하십시오. |
| 사용 기간   | 당월 컴포넌트 총 사용 시간                                     |
| 총 요금     | 총 요금 = 컴포넌트 원가 × 할인율, 그 중: 컴포넌트 원가 = 컴포넌트 정가 × 사용 시간 |

>?다른 필드는 Tencent Cloud에서 할당합니다. 자세한 내용은 [About Billing](https://intl.cloud.tencent.com/document/product/555)을 참고하십시오.
