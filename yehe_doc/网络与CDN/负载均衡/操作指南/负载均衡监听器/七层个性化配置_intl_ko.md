CLB는 사용자 지정 구성을 지원하므로 client_max_body_size 및 ssl_protocols와 같은 단일 CLB 인스턴스에 대한 구성 매개변수를 설정하여 고유한 요구 사항을 충족할 수 있습니다.
>?
>- 각 리전에는 최대 200개의 사용자 지정 구성 항목이 있을 수 있습니다.
>- 사용자 지정 구성은 64k 바이트로 제한됩니다.
>- 각 인스턴스는 사용자 지정 구성의 하나의 항목에만 바인딩될 수 있습니다.
>- 사용자 지정 구성은 레이어 7 HTTP/HTTPS CLB(이전 ‘애플리케이션 CLB’) 리스너에만 유효합니다.

## CLB 사용자 지정 구성 매개변수
CLB 사용자 지정 구성은 다음 구성을 지원합니다.

| 구성 |   기본값/권장값  |    매개변수 범위  | 설명  |
| :-------- | :-------- | :------ |:------ |
|ssl_protocols |TLSv1 TLSv1.1 TLSv1.2 TLSv1.3 |TLSv1 TLSv1.1 TLSv1.2 TLSv1.3 |사용된 TLS 프로토콜의 버전입니다. |
|  ssl_ciphers  | 아래 참고 |  아래 참고 | 암호화 제품군입니다. |
|  client_header_timeout  | 60s |  [30-120]s | Client 요청 헤더를 가져오는 타임아웃 시간. 타임아웃의 경우 408 오류가 반환됩니다.|
|  client_header_buffer_size | 4k |[1-256]k | Client 요청 헤더가 저장되는 기본 Buffer의 크기입니다. |
|  client_body_timeout | 60s |  [30-120]s | Client 요청 Body 획득의 타임아웃 시간은, 전체 Body를 획득하는 시간이 아니라 데이터 전송이 없는 유휴 기간을 나타냅니다. 타임아웃의 경우 408 오류가 반환됩니다. |
|  client_max_body_size | 60M |[1-10240]M| <ul><li>기본값: 1M-256M. </li><li>최대 크기: 10240M (10GB). client_max_body_size가 256M보다 크면 <a href="#buffer">proxy_request_buffering</a> 값이 off여야 합니다.</li></ul> |
|  keepalive_timeout | 75s | [0-900]s| Client-Server 지속 연결 유지 시간, 0으로 설정하면 지속 연결이 금지됩니다. 900s 이상으로 설정하시려면 [티켓을 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1)하십시오. 설정할 수 있는 최대값은 3600s입니다. |
|  add_header |사용자 지정|- | add_header xxx yyy 형식으로 클라이언트에 반환되는 특정 헤더 필드입니다. </br>예를 들어 크로스 도메인 시나리오의 경우: `add_header Access-Control-Allow-Methods 'POST, OPTIONS'; add_header Access-Control-Allow-Origin *;`으로 구성할 수 있습니다. |
|  more_set_headers |사용자 지정|- | more_set_headers "A:B"형식으로 클라이언트에 반환되는 특정 헤더 필드입니다. |
|  proxy_connect_timeout | 4s | [4-120]s |upstream 백엔드 연결의 타임아웃 시간입니다.|
|  proxy_read_timeout |60s |[30-3600]s|upstream 백엔드 응답을 읽는 타임아웃 시간입니다.|
|  proxy_send_timeout |60s |[30-3600]s|upstream 백엔드에 요청을 보내는 타임아웃 시간입니다.|
|  server_tokens | on | on, off | <ul><li>on: 버전 정보를 표시합니다. </li><li>off: 버전 정보를 숨깁니다. </li></ul>|
|  keepalive_requests | 100 | [1-10000] |Client-Server 지속 연결을 통해 보낼 수 있는 최대 요청 수입니다.|
|  proxy_buffer_size | 4k |[1-32]k| 기본적으로 proxy_buffer에 설정된 단일 버퍼의 크기인 Server 응답 헤더의 크기입니다. proxy_buffer_size를 사용하려면 proxy_buffers가 동시에 설정되어야 합니다.|
|  proxy_buffers | 8 4k |[3-8] [4-16]k|버퍼 수량 및 크기.|
|  <span id="buffer">proxy_request_buffering</span> | on |on, off|<ul><li>on: 클라이언트 요청 본문을 캐시합니다. CLB 인스턴스는 요청을 캐시하고 요청이 완전히 수신된 후 여러 부분에서 이를 백엔드 CVM 인스턴스로 포워딩합니다. </li><li>off: 클라이언트 요청 본문을 캐시하지 않습니다. 요청을 수신한 후 CLB 인스턴스는 이를 백엔드 CVM 인스턴스로 직접 포워딩하여 백엔드 CVM 성능에 대한 부담을 높입니다. </li></ul>|
|  proxy_set_header   |X-Real-Port $remote_port|<ul><li>X-Real-Port $remote_port</li><li>X-clb-stgw-vip $server_addr</li><li>Stgw-request-id $stgw_request_id</li><li>X-Forwarded-Port $vport</li><li>X-Method $request_method</li><li>X-Uri $uri</li></ul>|<ul><li>X-Real-Port $remote_port 클라이언트 포트. </li><li>X-clb-stgw-vip $server_addr CLB VIP. </li><li>Stgw-request-id $stgw_request_id 요청 ID(CLB에서만 사용됨). </li><li>X-Forwarded-Port CLB 리스너 포트. </li><li>X-Method 클라이언트 요청 메소드. </li><li>X-Uri 클라이언트 요청 URI.</li></ul> |
|  send_timeout | 60s |[1-3600]s|서버에서 클라이언트로의 데이터 전송 타임아웃 시간으로, 전체 요청 전송 기간이 아니라 두 개의 연속 데이터 전송 작업 사이의 시간 간격입니다.|
|  ssl_verify_depth |  1 |[1, 10]|클라이언트 인증서 체인의 검증 Depth입니다.|
|proxy_redirect | http:// https:// | http:// https://  | 업스트림 서버가 리디렉션 또는 새로 고침 요청(코드 301 또는 302)을 반환하면 proxy_redirect는 안전한 리디렉션을 위해 HTTP 헤더의 Location 또는 Refresh 필드에서 http를 https로 재설정합니다.  |
| ssl_early_data  |  off |on, off|TLS 1.3 0-RTT를 활성화하거나 비활성화합니다. ssl_protocols의 필드 값에 TLSv1.3이 포함된 경우에만 ssl_early_data가 적용됩니다. **ssl_early_data를 활성화하기 전에 리플레이 공격의 위험을 고려해야 합니다.**|
|http2_max_field_size|4k|[1-256]k|HPACK으로 압축된 요청 헤더의 최대 크기( Size )를 제한합니다.|
|error_page|-|error_page code [ = [ response]] uri|특정 오류 코드(Code)에 대해 미리 정의된 URI가 표시됩니다. 기본 응답(Response) 코드의 기본값은 302입니다. URI는 `/`로 시작해야 합니다.|
| proxy_ignore_client_abort | off | on, off | 클라이언트가 응답을 기다리지 않고 CLB 인스턴스와 연결을 끊는 경우 실제 서버와 CLB 인스턴스를 연결하거나 연결을 끊습니다.|


>?proxy_buffer_size 및 proxy_buffers 값에 대한 요구 사항: 2 * max(proxy_buffer_size, proxy_buffers.size) ≤(proxy_buffers.num - 1)\* proxy_buffers.size. 예를 들어 proxy_buffer_size가 24k이면 proxy_buffers는 8 8k입니다. 2 * 24k = 48k, (8 - 1)\* 8k = 56k 및 48k ≤ 56k이므로 구성 오류가 없습니다.
>
## ssl_ciphers 구성 지침
구성 중인 ssl_ciphers 암호화 제품군은 OpenSSL에서 사용하는 것과 동일한 형식이어야 합니다. 알고리즘 목록은 하나 이상의 `<cipher strings>`입니다. 여러 알고리즘은 ‘:’로 구분해야 합니다. ALL은 모든 알고리즘을 나타냅니다. ‘!’는 알고리즘을 활성화하지 않음을 나타내고 ‘+’는 알고리즘을 마지막 위치로 이동함을 나타냅니다.
기본 강제 비활성화에 대한 암호화 알고리즘은 `!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE`입니다.

**기본값:**
```plaintext
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE:3DES;
```

**매개변수 범위:**
```plaintext
ECDH-ECDSA-AES128-SHA256:ECDH-RSA-AES256-SHA:ECDH-ECDSA-AES256-SHA:SRP-DSS-AES-256-CBC-SHA:SRP-AES-128-CBC-SHA:ECDH-RSA-AES128-SHA256:DH-RSA-AES128-SHA256:DH-RSA-CAMELLIA128-SHA:DH-DSS-AES256-GCM-SHA384:DH-RSA-AES256-SHA256:AES256-SHA256:SEED-SHA:CAMELLIA256-SHA:ECDH-RSA-AES256-SHA384:ECDH-ECDSA-AES128-GCM-SHA256:DH-RSA-AES128-SHA:DH-RSA-AES128-GCM-SHA256:DH-DSS-AES128-SHA:ECDH-RSA-AES128-SHA:DH-DSS-CAMELLIA256-SHA:SRP-AES-256-CBC-SHA:DH-DSS-AES128-SHA256:SRP-RSA-AES-256-CBC-SHA:ECDH-ECDSA-AES256-GCM-SHA384:ECDH-RSA-AES256-GCM-SHA384:DH-DSS-AES256-SHA256:ECDH-ECDSA-AES256-SHA384:AES128-SHA:DH-DSS-AES128-GCM-SHA256:AES128-SHA256:DH-RSA-SEED-SHA:ECDH-ECDSA-AES128-SHA:IDEA-CBC-SHA:AES128-GCM-SHA256:DH-RSA-CAMELLIA256-SHA:CAMELLIA128-SHA:DH-RSA-AES256-GCM-SHA384:SRP-RSA-AES-128-CBC-SHA:SRP-DSS-AES-128-CBC-SHA:ECDH-RSA-AES128-GCM-SHA256:DH-DSS-CAMELLIA128-SHA:DH-DSS-SEED-SHA:AES256-SHA:DH-RSA-AES256-SHA:kEDH+AESGCM:AES256-GCM-SHA384:DH-DSS-AES256-SHA:HIGH:AES128:AES256:AES:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE
```

## CLB 사용자 지정 구성 예시
1. [CLB 콘솔](https://console.cloud.tencent.com/loadbalance/index?rid=8)에 로그인하고 왼쪽 사이드바에서 **사용자 지정 구성**을 클릭합니다.
2. ‘사용자 지정 구성’ 페이지 상단에서 리전을 선택하고 **생성**을 클릭합니다.
3. ‘사용자 지정 구성 생성’ 페이지에서 각 항목이 세미콜론`;`으로 끝나는 구성 이름과 코드 구성 항목을 입력합니다. 모든 정보를 입력한 후 **완료**를 클릭합니다.
![](https://main.qcloudimg.com/raw/7ef70a06f9509ba8759e5a923515a471.png) 
4. ‘사용자 지정 구성’ 페이지로 돌아가십시오. 오른쪽에서 **인스턴스에 바인딩**을 클릭합니다.
5. ‘인스턴스에 바인딩’ 팝업 페이지에서 바인딩할 CLB 인스턴스를 선택하고 **제출**을 클릭합니다.
![](https://main.qcloudimg.com/raw/ad8fb7874b9ce1fe7bf5c9366c7e64e7.png)
6. ‘사용자 지정 구성’ 페이지에서 구성된 ID를 클릭하여 세부 정보 페이지를 입력합니다. 바인딩된 인스턴스는 **바인딩 인스턴스** 탭에서 확인할 수 있습니다.
7. (선택 사항) 이제 인스턴스 목록 페이지에서 해당 사용자 지정 구성 정보를 볼 수 있습니다.
>?‘사용자 지정 구성 바인딩’이 인스턴스 목록에 표시되지 않으면 오른쪽 상단 모서리에 있는 ![](https://main.qcloudimg.com/raw/8cc99da2a299fc570d3d9b314c9dcae6.svg)을(를) 클릭합니다. 팝업 ‘사용자 지정 목록 필드’ 대화 상자에서 ‘사용자 지정 구성 바인딩’을 선택하고 **확인**을 클릭합니다. 목록 페이지에 ‘사용자 지정 구성 바인딩’ 열이 표시되어야 합니다.
>
![](https://main.qcloudimg.com/raw/d07bdbc134480fa89f732c93c3861243.png)
기본 구성 샘플 코드:
```plaintext
ssl_protocols   TLSv1 TLSv1.1 TLSv1.2;
client_header_timeout   60s;
client_header_buffer_size   4k;
client_body_timeout    60s;
client_max_body_size   60M;
keepalive_timeout    75s;
add_header     xxx yyy;
more_set_headers      "A:B";
proxy_connect_timeout    4s;
proxy_read_timeout    60s;
proxy_send_timeout    60s;
```

