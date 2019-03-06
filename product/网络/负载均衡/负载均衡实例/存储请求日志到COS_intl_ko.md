CLB는 사용자가 요청 로그를 저장하는 능력을 제공하기 때문에 요청 로그를 COS에 저장한 뒤 다운로드하여 분석할 수 있습니다. 현재 7계층 LB 로그 기능은 이미 전수 게시되었으며 광저우, 상하이, 베이징, 금융 지역 등 영역을 지원합니다. 활성화하시길 바랍니다.

## 로그 기능 시작
**CLB 인스턴스 세부 정보** 페이지에서 로그 접근 기능을 시작합니다.

![](https://mc.qcloudimg.com/static/img/17014eeb67628fa78ffe04e2d7a58d8d/log1.png)

해당하는 COS의 버킷을 선택하면 요청 로그는 버킷에 lb-id라는 폴더를 자동 생성하여 저장을 진행합니다. 선택 완료 후, 버킷 주소를 클릭하면 로그 다운로드 페이지로 바로 리디렉션할 수 있습니다.

COS의 버킷을 생성하지 않았다면 [버킷 생성](https://console.cloud.tencent.com/cos4/bucket) 후 해당하는 저장 위치를 선택하십시오.

## 제품 한도와 비용 계산
- 현재 로그 집합 세분화는 1시간입니다.
- 현재 CLB는 7게층(HTTP/HTTPS) 로그의 저장과 다운로드만 지원합니다.
- 로그 데이터 전송은 일정 지연이 있을 수 있습니다.
- 현재 CLB 로그 서비스는 "무료"이며, COS 저장의 무료 한도는 [문서](https://cloud.tencent.com/document/product/436/6240)에 나타나며 50G의 무료 저장 공간을 제공합니다. 로그량이 크다면 제때 데이터를 정리하십시오.
- 로그 접근을 시작하지 않으면, Tencent Cloud는 기본적으로 3일 간의 로그를 보관합니다. 로그 접근을 시작하면 저장 시간은 COS 저장에 따라 결정됩니다.

## 로그 형식 및 변수 설명
### 로그 형식

```
[$stgw_request_id] [$time_local] [$protocol_type] [$server_addr:$server_port] [$server_name] [$remote_addr:$remote_port] [$status]  [$upstream_status] [$proxy_host] [$request] [$request_length] [$bytes_sent] [$http_host] [$http_user_agent] [$http_referer]
[$request_time] [$upstream_response_time] [$upstream_connect_time] [$upstream_header_time] [$tcpinfo_rtt] [$connection] [$connection_requests] [$ssl_handshake_time] [$ssl_cipher] [$ssl_protocol] [$ssl_session_reused]
```

### 로그 변수 설명

| 번호 | 변수 이름 | 설명 |
| :-------- | :-------- | :------ |
| 1 | time_local	|  타임스탬프 |
| 2 | protocol_type |  프로토콜 유형(HTTP/HTTPS/SPDY/HTTP2/WS/WSS) |
| 3 | server_addr:server_port  | 요청한 대상 IP와 대상 포트 |
| 4 | server_name | 규칙의 server_name |
| 5 | remote_addr:remote_port	| 클라이언트 IP：port |
| 6 | status | LB가 클라이언트에 반환하는 상태 코드 |
| 7 | upstream_status | RS가 LB에 반환하는 상태 코드 |
| 8 | proxy_host | upstream ID |
| 9 | request | 요청행 |
| 10 | request_length | 클라이언트에서 수신한 요청 바이트 수 |
| 11 |bytes_sent | 	클라이언트에 발송한 바이트 수 |
| 12 |http_host	 | 요청 도메인 이름 |
| 13 |http_user_agent | 	user_agent |
| 14 |http_referer	 | HTTP 요청 출처 |
| 15 | request_time|요청 처리 시간(클라이언트에게 받은 첫 번째 바이트부터 시작하여 클라이언트에 발송한 마지막 바이트까지 클라이언트가 CLB에 요청, CLB가 RS에 요청을 포워딩, RS 데이터를 CLB에 반응, CLB 데이터를 클라이언트에 포워딩한 총 시간)|
| 16 | upstream_response_time |전체 백 엔드 요청이 소모한 시간(RS 연결부터 RS가 응답을 수신 완료한 시간까지)|
| 17 | upstream_connect_time	|RS와 TCP 연결 생성에 소모한 시간(RS 연결부터 HTTP 요청 발송 시작 시간까지)|
| 18 | upstream_header_time	|  RS가 HTTP 헤더를 수신하는 데 소모한 시간(RS 연결부터 RS가 HTTP 응답 헤더를 수신한 시간까지)|
| 19 | tcpinfo_rtt | TCP가 연결한 RTT |
| 20 | connection | ID 연결 |
| 21 | connection_requests | 연결한 요청 수 |
| 22 | ssl_handshake_time	|SSL 핸드 셰이크 소모 시간 |
| 23 | ssl_cipher| 암호화 세트|
| 24 | ssl_protocol	| SSL 프로토콜 버전 |
| 25 | ssl_session_reused |SSL SESSION 재사용|	 

