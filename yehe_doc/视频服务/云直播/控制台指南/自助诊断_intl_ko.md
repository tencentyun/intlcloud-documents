 Tencent Cloud CSS는 자가 진단 툴을 제공합니다. 이 툴은 자가 점검을 수행하고 사용자, URL, 도메인 및 스트림과 같은 진단 항목을 포함하여 일반적인 라이브 스트리밍/재생 문제를 신속하게 진단하는 솔루션을 제공합니다. 현재 오픈 베타 테스트 단계이며 진단 결과는 참고용입니다.

## 전제 조건
- [직접 조합 URL](https://intl.cloud.tencent.com/document/product/267/38393) 또는 [주소 생성기 생성](https://intl.cloud.tencent.com/document/product/267/31084) 방식을 통해 푸시 스트림/재생 주소를 생성합니다.
- 푸시 스트림 주소는 온라인 [라이브 스트리밍](https://intl.cloud.tencent.com/document/product/267/31558) 상태입니다.


## 진단 단계
라이브 푸시 스트림/라이브 방송에 이상 경고가 발생한 경우 장애 진단을 통해 감지 제안을 할 수 있습니다. 단계는 다음과 같습니다:
1. CSS 콘솔에 로그인 후 왼쪽 사이드바에서 [**자가 진단**](https://console.cloud.tencent.com/live/tools/selfcheck)을 선택합니다.
2. 진단할 푸시 스트림 주소 또는 재생 주소를 입력하십시오.
3. **진단 실행**을 클릭하면 진단 결과가 생성됩니다.

![](https://main.qcloudimg.com/raw/90fc6fce80283550af50214782c25b3c.png)

## 진단 결과
진단이 완료되면 아래와 같이 진단 결과가 생성되며, 진단 제안을 참고하여 오류를 처리할 수 있습니다. 진단 항목은 다음과 같습니다.

<table>
<thead><tr><th width=15%>진단 항목</th><th width=15%>진단 유형</th><th>설명</th></tr></thead>
<tbody><tr>
<td rowspan=2>클라이언트 정보 가져오기</td>
<td>APPID</td>
<td>사용자 계정 APPID</td>
</tr><tr>
<td>상태</td>
<td>사용자 계정 상태</td>
</tr><tr>
<td rowspan=3>도메인 점검</td>
<td>도메인</td>
<td>도메인</td>
</tr><tr>
<td>도메인 유형</td>
<td>푸시 스트림/재생 도메인</td>
</tr><tr>
<td>CNAME</td>
<td>CNAME 리졸브 상황</td>
</tr><tr>
<td rowspan=2>스트림 상태 점검</td>
<td>스트림</td>
<td>스트림 ID</td>
</tr><tr>
<td>상태</td>
<td>스트림 상태</td>
</tr><tr>
<td rowspan=12>URL 점검</td>
<td>URL</td>
<td>푸시 스트림/재생 주소</td>
</tr><tr>
<td>AppName</td>
<td>URL 경로 매개변수</td>
</tr><tr>
<td>StreamName</td>
<td>txSecret 인증 정보를 계산하는 데 사용되는 StreamName</td>
</tr><tr>
<td rowspan=3>인증 설정</td>
<td>활성화/비활성화 상태</td>
</tr><tr>
<td>인증 메인 key</td>
</tr><tr>
<td>인증 서브 key</td>
</tr><tr>
<td rowspan=6>푸시 스트림/재생 인증</td>
<td>인증 성공/인증 실패</td>
</tr><tr>
<td>실패 원인</td>
</tr><tr>
<td>StreamnNme 인증</td>
</tr><tr>
<td>txSecret: 푸시 스트림 인증을 활성화하면 생성되는 인증 문자열입니다.</td>
</tr><tr>
<td>txTime: 푸시 스트림 주소에 설정된 타임스탬프</td>
</tr><tr>
<td>URL 실제 만료 시간</td>
</tr><tr>
<td rowspan=4>액세스 대역폭 점검</td>
<td rowspan=2>대역폭 상한 설정</td>
<td>활성화됨/비활성화</td>
</tr><tr>
<td>가속 영역</td>
</tr><tr>
<td rowspan=2>액세스 상황</td>
<td>상태</td>
</tr><tr>
<td>현재 대역폭</td>
</tr><tr>
<td rowspan=6>서비스 자체 검사</td>
<td rowspan=3>클라이언트 자체 검사</td>
<td>
<li/>PC 푸시 스트림: <a href="https://intl.cloud.tencent.com/document/product/267/31569">OBS 푸시 스트림</a>사용 권장
 <li/>PC 재생: <a href="https://intl.cloud.tencent.com/document/product/267/32483">VLC 플레이어</a></td>사용 권장
</tr><tr>
<td>
<li/>Web 푸시 스트림: <a href="https://console.cloud.tencent.com/live/tools/webpush">Web 푸시 스트림</a></td>사용 권장
</tr><tr>
<td>
<li/>모바일 푸시 스트림: <a href="https://intl.cloud.tencent.com/document/product/1071/38147">TCToolkit App</a> 다운로드 및 설치, RTMP 푸시 스트림 선택
<li/>모바일 재생: <a href="https://intl.cloud.tencent.com/document/product/1071/38147">TCToolkit App</a> 다운로드 및 설치, LVB 재생 선택</td>
</tr><tr>
<td>IP 제한 자체 검사</td>
<td>IP 블록리스트/얼로우리스트, IP 리전 제한을 확인하여 IP 제한으로 인한 예외 해결.</td>
</tr><tr>
<td>스트림 데이터 모니터링</td>
<td>라이브 스트림의 실시간 모니터링 데이터를 분석하여 네트워크 정체, 지터 등으로 인한 이상 여부 판단. <a href="https://console.cloud.tencent.com/live/analysis/stream">스트리밍 데이터 조회</a>.</td>
</tr>
</tbody></table>


>? 진단 보고서로 문제가 해결되지 않으면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 진행하거나 Tencent Cloud 기술자에게 문의하시기 바랍니다.
