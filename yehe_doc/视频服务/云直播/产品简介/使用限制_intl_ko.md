CSS 서비스 이용 전 본 서비스의 사용 제한 정보를 확인하십시오.

<table>
<tr><th>제한 항목</th><th>설명</th></tr>
<tr>
<td>라이브 방송 도메인</td>
<td><ul style="margin:0">
 <li>기본적으로 계정에 여러 개의 재생 및 푸시 도메인을 만들 수 있습니다. 도메인 가속이 중국 본토나 글로벌 지역인 경우 공업정보부 ICP 비안이 완료되어야 하며 현재의 비안 정보가 정상적이고 사용 가능해야 합니다.<li>
    <li>각 계정은 기본적으로 100개의 도메인을 관리할 수 있습니다. 비즈니스 규모가 큰 경우 <a href="https://console.cloud.tencent.com/workorder/category">티켓 제출</a>을 통해 최대 도메인 수 추가를 신청할 수 있습니다.</li>
    <li>도메인 길이는 45자를 초과하지 않는 것이 좋습니다. <strong>45자</strong>를 초과하는 경우 <a href="https://console.cloud.tencent.com /workorder/category">티켓 제출</a>을 통해 해결해야 합니다.</li>
<li>CSS가 관리하는 도메인은 도메인 리졸브를 완료해야 라이브 방송 푸시 스트리밍/재생이 가능합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/267/31057">도메인 CNAME 설정</a>을 참고하십시오.</li></ul></td>
</tr><tr>
<td>라이브 방송 푸시 스트리밍</td>
<td>CSS 서비스는 푸시 스트리밍 비트 레이트의 제한이 없으며, 일반 해상도 및 대응 비트 레이트를 지원합니다. 푸시 스트리밍 랙을 피하기 위한 권장 비트 레이트는 4Mbps 미만입니다.</td>
</tr><tr>
<td>라이브 방송 재생</td>
<td><ul style="margin:0">
	<li>라이브 방송 주소 StreamName과 푸시 스트리밍 주소 StreamName이 일치해야 해당하는 스트리밍을 재생할 수 있습니다.</li>
	<li>라이브 방송 재생의 시청자 수는 제한이 없으며, 대역폭 상한 설정을 지원합니다.</li>
	<li/>고객 규모가 갑자기 대폭 증가한 경우, 3 근무일 전에 <a href="https://console.cloud.tencent.com/workorder/category">티켓 제출</a> 또는 비즈니스 매니저 문의를 통해 해결해야 합니다. 대규모 증가에는 다음 두 가지 유형의 시나리오가 포함됩니다.<ul style="margin:0">
		<li/>일일 돌발 피크 대역폭이 200Gbps를 초과하고 증가폭이 일일 피크 대비 200%인 시나리오.
		<li/>일일 돌발 피크 대역폭 증가량이 500Gbps를 초과하는 시나리오.
	</ul>
</ul></td>
</tr><tr>
<td>템플릿 설정</td>
<td>템플릿 연결 설정 성공 후 약 5 - 10분 뒤에 적용됩니다.</td>
</tr><tr>
<td>일 결산 과금 방식 변경</td>
<td>일 결산 과금은 트래픽/피크 대역폭 2가지 과금 방식을 지원하며, 1일 1회 변경이 가능합니다.(변경 시 익일 적용)</td>
</tr><tr>
<td>푸시 스트리밍 지원 프로토콜</td>
<td>RTMP, SRT 프로토콜을 지원합니다. 자세한 설명은 <a href="https://intl.cloud.tencent.com/document/product/267/7968">FAQ</a>를 참고하십시오.</td>
</tr><tr>
<td>재생 지원 프로토콜</td>
<td><ul style="margin:0">
	<li>LVB는 RTMP, FLV, HLS 재생 프로토콜을 지원합니다. 자세한 설명은 <a href="https://intl.cloud.tencent.com/document/product/267/7968">FAQ</a>를 참고하십시오.</li>
	<li>LEB는 WebRTC 재생 프로토콜을 지원합니다.</li>
</ul></td>
</tr></table>


