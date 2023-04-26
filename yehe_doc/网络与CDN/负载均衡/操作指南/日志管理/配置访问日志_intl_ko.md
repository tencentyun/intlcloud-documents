CLB(Cloud Load Balancer)는 클라이언트 요청을 더 잘 이해하고, 문제를 해결하고, 사용자 행동을 분석하는 데 도움이 될 수 있는 레이어 7(HTTP/HTTPS) 액세스 로그(Access Log) 구성을 지원합니다. 현재 액세스 로그는 CLS에 저장되고, 미세한 단위로 보고되며, 여러 규칙에 따라 온라인으로 검색할 수 있습니다.

CLB의 액세스 로그는 주로 문제를 빠르게 찾고 해결하는 데 사용됩니다. 액세스 로그 기능에는 로그 리포트, 저장 및 검색이 포함됩니다.
- 로그 리포트는 최선의 서비스(Best-Effort Service)를 제공합니다. 즉, 로그 리포트보다 서비스 포워딩을 우선시합니다.
- 로그 스토리지 및 검색은 현재 사용 중인 스토리지 서비스를 기반으로 SLA를 제공합니다.

>?
>- 현재 액세스 로그는 레이어 7 프로토콜(HTTP/HTTPS)에 대해서만 CLS에 저장할 수 있으며, 레이어 4 프로토콜(TCP/UDP/TCP SSL)에는 저장할 수 없습니다.
>- CLS에 대한 CLB 액세스 로그 저장은 무료입니다. CLS 서비스에 대한 요금만 지불하면 됩니다.
>- 이 기능은 CLS 사용 가능 리전에서만 지원됩니다. 사용 가능한 리전을 참고하십시오.
>



## 방법1: 단일 인스턴스 액세스 로그
### 1단계: CLS에서 액세스 로그 스토리지 활성화
1. [CLB 콘솔](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3)에 로그인하고 왼쪽 사이드바에서 **인스턴스 관리**를 클릭합니다.
2. **인스턴스 관리** 페이지에서 CLB 인스턴스 ID를 클릭합니다.
3. **기본 정보** 페이지의 ‘액세스 로그(레이어 7)’ 모듈에서 연필 아이콘을 클릭합니다.
![](https://main.qcloudimg.com/raw/b3f9b4276b4ff2f28ac184478ce7964c.png)
4. **CLS 로그 스토리지 위치 수정** 팝업 창에서 **로그를 활성화**하고 액세스 로그 스토리지에 대한 대상 로그셋 및 로그 테마를 선택한 다음 **제출**을 클릭합니다. 아직 로그셋 또는 로그 테마를 생성하지 않은 경우 [관련 리소스 생성](https://console.cloud.tencent.com/cls/logset) 후 다음 저장 위치로 선택하십시오.
![](https://main.qcloudimg.com/raw/33386c84ae812881548d1b621fbe6a70.png)
>?clb_logset 로그셋에서 **CLB**로 표시된 로그 테마를 사용하는 것이 좋습니다. **CLB**로 표시된 로그 테마와 일반적인 로그 테마의 차이점은 다음과 같습니다.
>- **CLB** 로그 테마는 자동으로 인덱스를 생성할 수 있지만 일반적인 로그 테마는 수동 인덱스 생성이 필요합니다.
>- 기본적으로 **CLB** 로그 테마에 대한 대시보드가 제공되지만 일반적인 로그 테마에 대해서는 수동으로 구성해야 합니다.
6. 로그셋 또는 로그 테마를 클릭하여 CLS의 로그 검색 분석 페이지로 리디렉션합니다.
7. (옵션) 로그를 비활성화하려면 연필 아이콘을 클릭하여 **CLS 로그 저장 위치 수정** 창을 열고 비활성화합니다.

### 2단계: 로그 테마 인덱스 구성
>?단일 인스턴스에 대해 액세스 로그가 구성된 경우 로그 테마에 대한 인덱스를 구성해야 합니다. 그렇지 않으면 로그를 찾을 수 없습니다.
>
권장 인덱스는 다음과 같습니다.

| 키 값 인덱스    | 필드 유형 | 구분 기호 |
| :---------- | :------- | :----- |
| server_addr | text     | 구분 기호 필요 없음     |
| server_name | text     | 구분 기호 필요 없음     |
| http_host   | text     | 구분 기호 필요 없음     |
| status      | long     | -     |
| vip_vpcid   | long     | -     |

단계는 다음과 같습니다.
1. [CLS 콘솔](https://console.cloud.tencent.com/cls)에 로그인하고 왼쪽 사이드바에서 **로그 테마**를 클릭합니다.
2. **로그 테마** 페이지에서 대상 로그 테마 ID를 클릭합니다.
3. 로그 테마 세부 정보 페이지에서 **인덱스 구성** 탭을 선택하고 **편집**을 클릭하여 인덱스를 추가합니다. 인덱스 구성에 대한 자세한 내용은 [Configuring Index](https://intl.cloud.tencent.com/document/product/614/39594)를 참고하십시오.
![](https://main.qcloudimg.com/raw/38b22da412497a25ac9d6d304766d1ac.png)
4. 인덱스 구성 결과는 아래와 같습니다.
![](https://main.qcloudimg.com/raw/6e2393e34cd06c5d073faba88d34110f.png)

### 3단계: 액세스 로그 보기
1. [CLS 콘솔](https://console.cloud.tencent.com/cls)에 로그인하고 왼쪽 사이드바에서 **검색 분석**을 클릭합니다.
3. **검색 분석** 페이지에서 로그셋, 로그 테마 및 시간 범위를 선택하고 **검색 분석**을 클릭하여 CLB에서 CLS에 보고한 액세스 로그를 검색합니다. 검색 구문에 대한 자세한 내용은 [Legacy CLS Search Syntax](https://intl.cloud.tencent.com/document/product/614/37882)를 참고하십시오.
![](https://main.qcloudimg.com/raw/e15271ea2d1ffac0e735eb254224a5e5.png)

## 방법2: 액세스 로그 일괄 구성

### 1단계: 로그셋 및 로그 테마 생성[](id:step2)
CLS에서 액세스 로그를 구성하려면 먼저 로그셋 및 로그 테마를 생성해야 합니다.
로그셋 및 로그 테마를 생성한 경우 [2단계](#step3)로 바로 이동할 수 있습니다.
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인하고 왼쪽 사이드바에서 **액세스 로그**를 선택합니다.
2. **액세스 로그** 페이지에서 로그 집합에 대한 영역을 선택한 다음 **로그셋 정보** 섹션에서 **로그셋 생성**을 클릭합니다.
3. **로그셋 생성** 대화 상자에서 보존 기간을 설정하고 **저장**을 클릭합니다.
>?각 리전에서 ‘clb_logset’이라는 단일 로그셋만 생성할 수 있습니다.
>
4. **액세스 로그** 페이지의 **로그 테마** 섹션에서 **로그 테마 생성**을 클릭합니다.
5. ‘로그 테마 추가’ 팝업 창에서 스토리지 유형 및 로그 저장 시간을 선택한 후, 오른쪽 목록에 추가할 CLB 인스턴스를 선택하고 **저장**을 클릭합니다.
>?
>- 스토리지 유형은 STANDARD, STANDARD_IA로 구분됩니다. 자세한 내용은 [Storage Class Overview](https://www.tencentcloud.com/document/product/614/42003)를 참고하십시오.
>- 로그는 영구적으로 또는 지정된 기간 동안 보관할 수 있습니다.
>- 로그 테마를 생성할 때 필요에 따라 CLB 인스턴스를 추가할 수 있습니다. 추가하려면 목록에서 로그 테마를 선택하고 **작업** 열에서 **관리**를 클릭합니다. 각 CLB 인스턴스는 하나의 로그 테마에만 추가할 수 있습니다.
>- 로그셋에는 여러 로그 테마(Topic)가 포함될 수 있습니다. CLB 로그를 **CLB**로 표시되는 다양한 로그 테마로 분류할 수 있습니다.
>
6. (옵션) 액세스 로그를 닫으려면 로그 테마 우측의 **작업** 열에서 **중지**를 클릭하기만 하면 됩니다.

### 2단계: 액세스 로그 보기[](id:step3)
수동 구성 없이 CLB는 액세스 로그 값으로 인덱스 검색으로 자동 구성되었습니다. 검색 분석을 통해 접속 로그를 직접 조회할 수 있습니다.
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인하고 왼쪽 사이드바에서 **액세스 로그**를 선택합니다.
2. 로그 테마를 선택하고 **작업** 열에서 **검색**을 클릭하면 [CLS 콘솔](https://console.cloud.tencent.com/cls/search)의 ‘검색 분석’ 페이지로 리디렉션됩니다.
3. **검색 분석** 페이지에서 입력 상자에 검색 구문을 입력하고 시간 범위를 선택한 다음 **검색 분석**을 클릭하여 CLB에서 CLS에 리포트한 액세스 로그를 검색합니다.
>?검색 구문에 대한 자세한 내용은 [Overview and Syntax Rules](https://intl.cloud.tencent.com/document/product/614/37803)를 참고하십시오.
>


## 로그 형식 및 변수 설명
### 로그 형식
```
[$stgw_request_id] [$time_local] [$protocol_type] [$server_addr:$server_port]  [$server_name] [$remote_addr:$remote_port] [$status] [$upstream_addr] [$upstream_status] [$proxy_host] [$request] [$request_length] [$bytes_sent] [$http_host] [$http_user_agent] [$http_referer] [$request_time] [$upstream_response_time] [$upstream_connect_time] [$upstream_header_time] [$tcpinfo_rtt] [$connection] [$connection_requests] [$ssl_handshake_time] [$ssl_cipher] [$ssl_protocol] [$vip_vpcid] [$uri] [$server_protocol]
```

### 필드 유형
현재 CLS는 다음 세 가지 필드 유형을 지원합니다.

| 이름   | 유형 설명                 |
| :----- | :----------------------- |
| text   | 텍스트 유형                 |
| long   | 정수형(Int 64)   |
| double | 부동 소수점 유형(64 bit) |

### 로그 변수 설명
<table class="table"><thead><tr><th>변수 이름</th><th>설명</th><th>필드 유형</th></tr></thead>
<tbody><tr><td>stgw_request_id</td><td> 요청 ID. </td><td>text</td></tr>
<tr><td>time_local</td><td> 액세스 시간 및 시간대(예시: ‘01/Jul/2019:11:11:00 +0800’) 여기서 ‘+0800’은 UTC+8, 즉 베이징 시간을 나타냅니다.</td><td>text</td></tr>
<tr><td>protocol_type</td><td> 프로토콜 유형(HTTP/HTTPS/SPDY/HTTP2/WS/WSS).</td><td>text</td></tr>
<tr><td>server_addr</td><td>CLB VIP. </td><td>text</td></tr>
<tr><td>server_port</td><td>CLB VPort, 즉 수신 포트입니다.</td><td>long</td></tr>
<tr><td>server_name</td><td> 규칙의 server_name, 즉 CLB 리스너에 구성된 도메인 이름입니다.</td><td>text</td></tr>
<tr><td>remote_addr</td><td> 클라이언트 IP.</td><td>text</td></tr>
<tr><td>remote_port</td><td> 클라이언트 포트.</td><td>long</td></tr>
<tr><td>status</td><td> 상태 코드가 클라이언트에 반환되었습니다. </td><td>long</td></tr>
<tr><td>upstream_addr</td><td> RS 주소.</td><td>text</td></tr>
<tr><td>upstream_status</td><td> RS에서 CLB로 반환한 상태 코드입니다. </td><td>text</td></tr>
<tr><td>proxy_host</td><td> stream ID. </td><td>text</td></tr>
<tr><td>request</td><td> 요청 라인. </td><td>text</td></tr>
<tr><td>request_length</td><td> 클라이언트에서 받은 요청의 바이트 수입니다. </td><td>long</td></tr>
<tr><td>bytes_sent</td><td> 클라이언트에 보낸 바이트 수입니다. </td><td>long</td></tr>
<tr><td>http_host</td><td> 요청 도메인 이름, 즉 HTTP 헤더의 Host입니다.</td><td>text</td></tr>
<tr><td>http_user_agent</td><td> HTTP 헤더의 user_agent 필드.</td><td>text</td></tr>
<tr><td>http_referer</td><td> HTTP 요청 소스. </td><td>text</td></tr>
<tr><td>request_time</td><td> 요청 처리 시간: 타이밍은 클라이언트로부터 첫 번째 바이트가 수신될 때 시작되고 마지막 바이트가 클라이언트로 전송될 때 중지됩니다. 즉, 클라이언트 요청이 CLB 인스턴스에 도달하고 CLB 인스턴스가 요청을 RS에 전달하고 RS가 응답하여 데이터를 CLB 인스턴스에 보내고 마지막으로 CLB 인스턴스가 클라이언트에 데이터를 CLB 인스턴스에 전달하는 전체 프로세스에 걸리는 총 시간입니다.</td><td>double</td></tr>
<tr><td>upstream_response_time</td><td> 전체 백엔드 요청 프로세스에 걸리는 시간입니다. 타이밍은 CLB 인스턴스가 CONNECT RS할 때 시작되고 RS가 요청을 수신하고 응답할 때 중지됩니다.</td><td>double</td></tr>
<tr><td>upstream_connect_time</td><td> RS와 TCP 연결을 설정하는 데 걸리는 시간입니다. 타이밍은 CLB 인스턴스가 CONNECT RS할 때 시작되고 HTTP 요청을 보낼 때 중지됩니다.</td><td>double</td></tr>
<tr><td>upstream_header_time</td><td> RS에서 HTTP 헤더를 수신하는 데 걸리는 시간입니다. 타이밍은 CLB 인스턴스가 CONNECT RS될 때 시작되고 RS로부터 HTTP 응답 헤더가 수신될 때 멈춥니다.</td><td>double</td></tr>
<tr><td>tcpinfo_rtt</td><td> TCP 연결 RTT. </td><td>long</td></tr>
<tr><td>connection</td><td> 연결 ID. </td><td>long</td></tr>
<tr><td>connection_requests</td><td> 연결 요청 수입니다. </td><td>long</td></tr>
<tr><td>ssl_handshake_time</td><td>x:x:x:x:x:x:x 형식의 각 SSL 핸드셰이크 단계에서 소요된 시간입니다. 이 중 콜론으로 구분된 문자열은 단위는 ms이며, 각 단계에 소요된 시간이 1ms 미만이면 0으로 표시됩니다.
<ul><li>첫 번째 필드는 SSL 세션의 재사용 여부를 나타냅니다.</li>
<li>2번째 필드는 전체 핸드셰이크 시간을 나타냅니다.</li>
<li>3번째에서 7번째 필드는 각 SSL 핸드셰이크 단계에 걸리는 시간을 나타냅니다.</li>
<li>3번째 필드는 CLB가 client hello를 수신한 후부터 server hello done을 보낼 때까지의 시간을 나타냅니다.</li>
<li>4번째 필드는 CLB가 서버 인증서 전송을 시작한 시점부터 서버 인증서 전송을 완료한 시점까지의 시간을 나타냅니다.</li>
<li>5번째 필드는 CLB가 서명을 계산한 시간부터 server key exchange 전송을 완료할 때까지의 시간을 나타냅니다.</li>
<li>6번째 필드는 CLB가 client key exchange 수신을 시작한 시점부터 client key exchange 수신을 완료할 때까지의 시간을 나타냅니다.</li>
<li>7번째 필드는 CLB가 client key exchange을 수신한 시간부터 server finished를 보낼 때까지의 시간을 나타냅니다.</li></ul></td><td>text</td></tr>
<tr><td>ssl_cipher</td><td> SSL 암호 제품군.</td><td>text</td></tr>
<tr><td>ssl_protocol</td><td> SSL 프로토콜 버전.</td><td>text</td></tr>
<tr><td>vip_vpcid</td><td>CLB VIP의 VPC ID. 공중망 CLB 인스턴스의 vip_vpcid는 -1입니다.</td><td>long</td></tr>
<tr><td>request_method</td><td> 요청 방법. POST 및 GET 요청만 지원됩니다.</td><td>text</td></tr>
<tr><td>uri</td><td> 리소스 식별자.</td><td>text</td></tr>
<tr><td>server_protocol</td><td>CLB에 사용되는 프로토콜입니다.</td><td>text</td></tr>
</tbody></table>

### 기본 검색 로그 변수
다음 필드는 기본적으로 ‘CLB’가 있는 로그셋에서 찾을 수 있습니다.
<table class="table"><thead><tr><th>인덱스 필드</th><th>설명</th><th>필드 유형</th></tr></thead>
<tbody>
<tr><td>time_local</td><td> 액세스 시간 및 시간대(예시: ‘01/Jul/2019:11:11:00 +0800’) 여기서 ‘+0800’은 UTC+8, 즉 베이징 시간을 나타냅니다.</td><td>text</td></tr>
<tr><td>protocol_type</td><td> 프로토콜 유형(HTTP/HTTPS/SPDY/HTTP2/WS/WSS).</td><td>text</td></tr>
<tr><td>server_addr</td><td>CLB VIP. </td><td>text</td></tr>
<tr><td>server_name</td><td> 규칙의 server_name, 즉 CLB 리스너에 구성된 도메인 이름입니다.</td><td>text</td></tr>
<tr><td>remote_addr</td><td> 클라이언트 IP.</td><td>text</td></tr>
<tr><td>status</td><td> 상태 코드가 클라이언트에 반환되었습니다. </td><td>long</td></tr>
<tr><td>upstream_addr</td><td> RS 주소.</td><td>text</td></tr>
<tr><td>upstream_status</td><td> RS에서 CLB로 반환한 상태 코드입니다. </td><td>text</td></tr>
<tr><td>request_length</td><td> 클라이언트에서 받은 요청의 바이트 수입니다. </td><td>long</td></tr>
<tr><td>bytes_sent</td><td> 클라이언트에 보낸 바이트 수입니다. </td><td>long</td></tr>
<tr><td>http_host</td><td> 요청 도메인 이름, 즉 HTTP 헤더의 Host입니다.</td><td>text</td></tr>
<tr><td>request_time</td><td> 요청 처리 시간: 타이밍은 클라이언트로부터 첫 번째 바이트가 수신될 때 시작되고 마지막 바이트가 클라이언트로 전송될 때 중지됩니다. 즉, 클라이언트 요청이 CLB 인스턴스에 도달하고 CLB 인스턴스가 요청을 RS에 전달하고 RS가 응답하여 데이터를 CLB 인스턴스에 보내고 마지막으로 CLB 인스턴스가 클라이언트에 데이터를 CLB 인스턴스에 전달하는 전체 프로세스에 걸리는 총 시간입니다.</td><td>double</td></tr>
<tr><td>upstream_response_time</td><td> 전체 백엔드 요청 프로세스에 걸리는 시간입니다. 타이밍은 CLB 인스턴스가 CONNECT RS할 때 시작되고 RS가 요청을 수신하고 응답할 때 중지됩니다.</td><td>double</td></tr>
</tbody></table>
