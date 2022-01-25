Tencent Cloud 라이브 방송은 라이브 방송 푸시 스트림 중단 기록 및 원인을 빠르게 파악할 수 있도록 스트리밍 중단 진단을 지원합니다.

## 전제 조건
- [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 합니다.
- 현재 Tencent Cloud 계정의 라이브 방송 푸시 스트림에 스트리밍 중단이 발생했어야 합니다.

## 작업 순서

라이브 방송 푸시 스트림이 중단된 후 왼쪽 메뉴바에 있는 [이벤트 센터]>[[스트리밍 중단 기록](https://console.cloud.tencent.com/live/tools/streamevent
)]을 선택해 스트리밍 중단 진단을 시작합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7109f254ed3f4c892bd93632d9f04629.png)

다음을 참고하십시오. 
- **경로**: 푸시 스트림 주소 상의 AppName입니다.
- **스트림 이름**: 푸시 스트림 주소 상의 StreamName입니다.

[](id:erro_code)
## 스트리밍 중단 에러 코드
스트리밍 중단 에러 코드 및 해당 오류 원인은 다음 표를 참조하십시오. 

<table border='0' >
 <col >
 <col >
 <tr >
<th colspan='2' >에러 코드</td>
<th >오류 원인</td>
 </tr>
 <tr >
<td colspan='2' >0</td>
<td >알 수 없는 오류. </td>
 </tr>
 <tr >
<td colspan='2' >1</td>
<td >푸시 클라이언트에서 자발적으로 스트리밍을 중단함. </td>
 </tr>
 <tr >
<td colspan='2' >2</td>
<td >푸시 클라이언트에서 자발적으로 스트리밍을 중단함. </td>
 </tr>
 <tr >
<td colspan='2' >3</td>
<td>푸시 클라이언트에서 자발적으로 스트리밍을 중단함. </td>
 </tr>
 <tr >
<td colspan='2' >4</td>
<td >푸시 클라이언트에서 자발적으로 스트리밍을 중단함. </td>
 </tr>
 <tr>
<td colspan='2' >5</td>
<td >라이브 방송 시스템 내부 오류. </td>
 </tr>
 <tr >
<td colspan='2' >6</td>
<td >RTMP 프로토콜 내용 오류. </td>
 </tr>
 <tr >
<td colspan='2' >7</td>
<td >RTMP 단일 프레임 크기가 설정에 허용된 최대값을 초과. </td>
 </tr>
 <tr >
<td colspan='2' >8</td>
<td >시스템에서 장시간 데이터가 없는 푸시 스트림 차단. </td>
 </tr>
 <tr>
<td colspan='2' >9</td>
<td  >라이브 방송 시스템 내부 오류. </td>
 </tr>
 <tr >
<td colspan='2'  >10</td>
<td  >프록시 레이어에서 스트리밍 중단 명령 수신. </td>
 </tr>
 <tr >
<td colspan='2'  >11</td>
<td  >라이브 방송 시스템 내부 오류. </td>
 </tr>
 <tr >
<td colspan='2'  >12</td>
<td  >푸시 링크 네트워크 오류. </td>
 </tr>
 <tr  >
<td colspan='2'  >13</td>
<td  >푸시 링크 네트워크 오류. </td>
 </tr>
 <tr >
<td colspan='2'  >14</td>
<td  >푸시 링크 네트워크 오류. </td>
 </tr>
 <tr >
<td colspan='2'  >15</td>
<td  >푸시 링크 네트워크 오류. </td>
 </tr>
 <tr  >
<td colspan='2'  >16</td>
<td  >라이브 방송 시스템 내부 오류</td>
 </tr>
 <tr >
<td colspan='2'  >17</td>
<td  >푸시 링크 네트워크 오류. </td>
 </tr>
 <tr  >
<td rowspan='27'>18</td>
<td>100</td>
<td  >라이브 방송 시스템 내부 오류. </td>
 </tr>
 <tr >
<td >101</td>
<td  >라이브 방송 시스템 내부 오류. </td>
 </tr>
 <tr  >
<td >102</td>
<td  >라이브 방송 시스템 내부 오류. </td>
 </tr>
 <tr  >
<td >103</td>
<td  >라이브 방송 시스템 내부 오류</td>
 </tr>
 <tr >
<td >104</td>
<td  >라이브 방송 시스템 내부 오류. </td>
 </tr>
 <tr >
<td >200</td>
<td  >푸시 링크에 해당하는 사용자 정보 가져오기 실패. </td>
 </tr>
 <tr >
<td >201</td>
<td  >사용자의 라이브 방송 서비스가 정지됨. </td>
 </tr>
 <tr  >
<td>202</td>
<td  >계정 연체로 라이브 방송 서비스가 일시적으로 정지되었습니다. 즉시 충전하시기 바랍니다. </td>
 </tr>
 <tr>
<td >203</td>
<td  >사용자의 라이브 방송 서비스가 강제로 정지됨. </td>
 </tr>
 <tr>
<td >300</td>
<td  >IP 주소를 직접 사용한 푸시 스트리밍 불가. </td>
 </tr>
 <tr >
<td >301</td>
<td  >푸시 도메인을 식별할 수 없음. </td>
 </tr>
 <tr >
<td >302</td>
<td  >불법 푸시 도메인. </td>
 </tr>
 <tr >
<td >303</td>
<td  >푸시 도메인이 비활성화됨. </td>
 </tr>
 <tr >
<td >304</td>
<td  >푸시 애플리케이션 이름이 비활성화됨. </td>
 </tr>
 <tr>
<td >305</td>
<td  >푸시 스트림의 스트림 이름이 재생 금지 상태임. </td>
 </tr>
 <tr >
<td>306</td>
<td  >액세스 모드가 채널 모드이나, 아직 해당 푸시 채널을 생성하지 않음. </td>
 </tr>
 <tr >
<td >307</td>
<td  >액세스 모드가 채널 모드이나, 현재 푸시 채널이 이미 종료됨. </td>
 </tr>
 <tr >
<td >308</td>
<td  >푸시 스트림의 스트림 이름에 부적절한 문자가 포함되어 있음. </td>
 </tr>
 <tr >
<td>309</td>
<td  >푸시 스트림의 애플리케이션 이름에 부적절한 문자가 포함되어 있음. </td>
 </tr>
 <tr  >
<td >400</td>
<td  >푸시 클라이언트 IP가 블랙리스트에 포함되어 있음. </td>
 </tr>
 <tr >
<td >401</td>
<td  >푸시 클라이언트 IP가 화이트리스트에 포함되어 있지 않음. </td>
 </tr>
 <tr  >
<td>500</td>
<td  >푸시 스트림에 만료 시간 매개변수 없음. </td>
 </tr>
 <tr >
<td >501</td>
<td  >만료 시간 매개변수 값이 만료됨. </td>
 </tr>
 <tr  >
<td>502</td>
<td  >푸시 스트림에 인증 매개변수 없음. </td>
 </tr>
 <tr  >
<td >503</td>
<td  >인증 매개변수 검증 미통과. </td>
 </tr>
 <tr  >
<td>600</td>
<td  >현재 푸시 스트림 수가 설정 허용된 최대값 초과. </td>
 </tr>
 <tr >
<td >601</td>
<td  >현재 스트림 이름에 해당하는 푸시 스트림 수가 설정 허용된 최대값 초과. </td>
 </tr>
 <tr >
<td colspan='2'  >19</td>
<td  >3rd party 인증 실패. </td>
 </tr>
 <tr >
<td colspan='2'  >20</td>
<td  >시스템에서 장시간 데이터가 없는 푸시 스트림 차단. </td>
 </tr>
 <tr >
<td rowspan='3'>21</td>
<td >100</td>
<td  >클라이언트에서 호출한 스트리밍 중단 요청 수신. </td>
 </tr>
 <tr >
<td>101</td>
<td  >클라이언트에서 호출한 재생 금지 요청 수신. </td>
 </tr>
 <tr >
<td >102</td>
<td  >새로운 푸시 링크로 현재 푸시 스트림 대체 수신. </td>
 </tr>
 <tr  >
<td colspan='2'  >22</td>
<td  >원인을 알 수 없음. </td>
 </tr>
 <tr >
<td colspan='2'  >23</td>
<td  >RTMP 프로토콜 내용 오류. </td>
 </tr>
 <tr >
<td colspan='2'  >24</td>
<td  >라이브 방송 시스템 내부 오류. </td>
 </tr>
 <tr >
<td colspan='2'  >25</td>
<td  >원인을 알 수 없음. </td>
 </tr>
 <tr >
<td colspan='2'  >26</td>
<td  >원인을 알 수 없음. </td>
 </tr>
 <tr >
<td colspan='2'  >27</td>
<td  >원인을 알 수 없음. </td>
 </tr>
 <tr  >
<td colspan='2'  >28</td>
<td  >원인을 알 수 없음. </td>
 </tr>
 <tr >
<td colspan='2'  >29</td>
<td  >원인을 알 수 없음. </td>
 </tr>
 <tr  >
<td colspan='2'  >30</td>
<td  >원인을 알 수 없음. </td>
 </tr>
 <tr>
<td colspan='2'  >31</td>
<td  >원인을 알 수 없음. </td>
 </tr>
 <tr>
<td colspan='2'  >32</td>
<td  >원인을 알 수 없음. </td>
 </tr>
 <tr  >
<td colspan='2'  >33</td>
<td  >RTMP AMF 데이터 오류. </td>
 </tr>
 <tr>
<td colspan='2'  >34</td>
<td  >원인을 알 수 없음. </td>
 </tr>
 <tr >
<td colspan='2'  >35</td>
<td  >푸시 클라이언트에서 자발적으로 스트리밍을 중단함. </td>
 </tr>
</table>

LVB는 API 인터페이스를 통한 조회도 제공합니다. 자세한 내용은 [스트리밍 중단 이벤트 조회](https://intl.cloud.tencent.com/document/product/267/30800)를 참조하십시오.
