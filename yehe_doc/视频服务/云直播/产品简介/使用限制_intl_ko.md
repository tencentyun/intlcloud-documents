CSS 서비스 이용 전 본 서비스의 사용 제한 정보를 확인하십시오.

<table>
<tr><th>제한 항목</th><th>설명</th></tr>
<tr>
<td>라이브 방송 도메인</td>
<td><ul style="margin:0">
 <li>기본적으로 계정별로 여러 개의 재생 및 푸시 스트림 도메인을 생성할 수 있습니다. 중국 (대륙)에서 도메인을 사용할 경우, 도메인 ICP 비안을 발급 받고 현재 비안 정보는 정상적으로 사용 가능해야 합니다. </li><li>기본적으로 계정별로 도매인 100개까지 관리할 수 있습니다. 비즈니스 사용량이 많다면 <a href="https://console.cloud.tencent.com/workorder/category">티켓 제출</a>을 통해 최대 도메인 수 확장을 신청할 수 있습니다.</li><li>도메인 길이는 30자를 초과할 수 없으며, <strong>30자</strong>를 초과하는 경우 <a href="https://console.cloud.tencent.com/workorder/category">티켓 제출</a>을 통해 해결해야 합니다.</li>
<li>CSS가 관리하는 도메인은 도메인 리졸브를 완료해야 라이브 방송 푸시 스트리밍/재생이 가능합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/267/31057">도메인 설정 CNAME</a>을 참고하십시오.</li></td>
</tr><tr>
<td>라이브 방송 푸시 스트리밍</td>
<td>CSS 서비스는 푸시 스트리밍 비트 레이트의 제한이 없으며, 일반 해상도 및 대응 비트 레이트를 지원합니다. 푸시 스트리밍 랙을 피하기 위한 권장 비트 레이트는 4Mbps 미만입니다.</td>
</tr><tr>
<td>라이브 방송 재생</td>
<td><ul style="margin:0">
<li>라이브 방송 주소 StreamName과 푸시 스트림 주소 StreamName이 동일해야 해당 스트림을 재생할 수 있습니다.</li><li>라이브 방송 재생 시청 인원수에는 제한이 없으며 대역폭 상한을 설정할 수 있습니다.</li></td>
</tr><tr>
<td>템플릿 설정</td>
<td>템플릿 연결 설정 성공 후 약 5 - 10분 뒤에 적용됩니다.</td>
</tr><tr>
<td>일 결산 과금 방식 변경</td>
<td>일 결산 과금은 트래픽/피크 대역폭 2가지 과금 방식을 지원하며, 1일 1회 변경이 가능합니다.(변경 시 익일 적용)</td>
</tr><tr>
<td>푸시 스트리밍 지원 프로토콜</td>
<td>RTMP, SRT 출력 프로토콜을 지원합니다. 자세한 설명은 <a href="https://intl.cloud.tencent.com/document/product/267/7968">FAQ</a>를 참고하십시오.</td>
</tr><tr>
<td>재생 지원 프로토콜</td>
<td><ul style="margin:0">
<li>LVB는 RTMP, FLV, HLS 재생 프로토콜을 지원합니다. 자세한 설명은 <a href="https://intl.cloud.tencent.com/document/product/267/7968">FAQ</a>를 참고하십시오.</li>
<li>LEB는 webRTC 재생 프로토콜을 지원합니다. </li>
<li>풀 스트림 재생 대역폭은 최대 200G까지 지원합니다. 이를 초과하는 경우 <a href="https://console.cloud.tencent.com/workorder/category">티켓 제출</a> 또는 비즈니스 매니저 연락을 통해 해결하십시오.</li></td>
</tr><tr>
<td>스튜디오</td>
<td><ul style="margin:0">
<li>계정별로 스튜디오 인스턴스를 <b>3</b>개 생성할 수 있으며, 스튜디오 인스턴스를 삭제한 후 다시 추가할 수 있습니다. 여러 개의 스튜디오가 필요한 경우 <a href="https://console.cloud.tencent.com/workorder/category">티켓 제출</a>을 신청하십시오.</li>
<li>VOD 입력 재생 목록은 VOD 파일을 최대 5개까지 지원합니다.</li>
<li>3rd party 푸시는 최대 3개까지 지원합니다. 이중 1개는 기본적으로 Tencent Cloud CSS 계정을 푸시하고, 나머지 2개는 3rd party를 푸시합니다.</li></td>
</tr></table>
 
