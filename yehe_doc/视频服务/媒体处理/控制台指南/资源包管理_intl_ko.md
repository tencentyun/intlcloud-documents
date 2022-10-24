## 시나리오
이 페이지는 구매한 일반 트랜스 코딩 및 TESHD(Tencent Extreme Speed High Definition) 트랜스 코딩 리소스 팩과 사용법을 보여줍니다.
## 리소스 팩 조회
[MPS(Media Processing Service) 콘솔](https://console.cloud.tencent.com/mps)에 로그인하고 왼쪽 사이드바에서 [리소스 팩 관리](https://console.cloud.tencent.com/mps/resources?tab=package)를 선택합니다. **리소스 팩** 탭에서 구매한 리소스 팩의 정보를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c81fcdc9a8c3fe4e2c31713c38661039.png)

<table>
<thead>
<tr>
<th width=13%>헤더</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>리소스 팩 ID</td>
<td>리소스 팩의 고유 식별자입니다. 검색 상자에 리소스 팩 ID를 입력하여 리소스 팩을 검색할 수 있습니다.</td>
</tr>
<tr>
<td>상태</td>
<td>리소스 팩의 현재 상태: 유효, 만료, 동결, 소진<ul style="margin:0">
<li><strong>유효</strong>: 리소스 팩이 유효하며 사용할 수 있습니다.</li>
<li><strong>동결</strong>: 리소스 팩이 어떤 이유로 동결되어 더 이상 사용할 수 없습니다.</li>
<li><strong>만료</strong>: 리소스 팩이 만료되어 더 이상 사용할 수 없습니다. 리소스 팩의 유효 기간은 1년입니다.</li>
<li><strong>소진</strong>: 리소스 팩이 소진되었습니다.</li>
</ul>
</td>
</tr>
<tr>
<td>유형</td>
<td>리소스 팩 유형: 일반 트랜스 코딩, TESHD 트랜스 코딩. 해당 유형을 선택하면 일반 트랜스 코딩 팩 또는 TESHD 트랜스 코딩 팩만 볼 수 있습니다.</td>
</tr>
<tr>
<td>총 시간</td>
<td>리소스 팩이 제공하는 총 시간(분)으로, 팩 사용을 시작한 후에도 변경되지 않습니다.</td>
</tr>
<tr>
<td>남은 시간(분)</td>
<td>팩 사용을 시작한 후 감소하는 리소스 팩의 남은 시간(분). 남은 시간(분)이 0이 되면 팩 상태가 만료됩니다.</td>
</tr>
<tr>
<td>시작 시간</td>
<td>리소스 팩이 유효한 시간입니다.</td>
</tr>
<tr>
<td>종료 시간</td>
<td>리소스 팩이 만료되는 시간으로 시작 시간으로부터 1년 후입니다.</td>
</tr>
<tr>
<td>작업</td>
<td><strong>환불</strong>을 클릭하여 리소스 팩을 환불할 수 있습니다. <br>참고: <strong>리소스 팩은 구매 후 5일 이내에만 환불 가능합니다.</strong></td>
</tr>
</tbody></table>

## 사용 내역 조회
[MPS 콘솔](https://console.cloud.tencent.com/mps)에 로그인하고 왼쪽 사이드바에서 [리소스 팩 관리](https://console.cloud.tencent.com/mps/resources?tab=package)를 선택합니다. **사용 세부 정보** 탭에서 리소스 팩의 사용 세부 정보를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/583c667367a63573868e1d18a44e0e23.png)
특정 기간(**차감 시간**)의 특정 리소스 팩(**리소스 팩 ID**)의 차감 세부 정보를 조회할 수 있습니다.

| 헤더 | 설명     |
| ----------------- | ----------------- |
| 차감 시간 | 차감이 발생한 시간입니다. |
| 리소스 팩 ID | 시간이 차감된 리소스 팩의 ID입니다. |
| 유형 | 리소스 팩 유형입니다. 유형을 선택하여 해당 유형에 대한 차감을 볼 수 있습니다. |
| 트랜스 코딩 유형 | 차감의 트랜스 코딩 유형입니다. 동일한 트랜스 코딩 유형에 대한 사용량이 매일 추가됩니다. |
| 차감 전 분 | 차감이 발생하기 전 리소스 팩의 남은 시간(분)입니다. |
| 차감 후 분 | 차감 후 리소스 팩의 남은 시간(분)입니다. |

