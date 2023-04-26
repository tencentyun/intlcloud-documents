리스너를 구성할 때 상태 확인을 활성화하여 리얼 서버의 가용성 정보를 얻을 수 있습니다. 상태 확인에 대한 자세한 내용은 [Health Check Overview](https://intl.cloud.tencent.com/document/product/214/6097)를 참고하십시오.

[](id:postreq)
## 전제 조건
1. CLB 인스턴스 생성을 완료합니다. 자세한 내용은 [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149)를 참고하십시오.
2. CLB 리스너 생성을 완료합니다.
 - TCP 리스너 생성하려면 [Configuring TCP Listener](https://intl.cloud.tencent.com/document/product/214/32517)에서 자세한 정보를 참고하십시오.
 - UDP 리스너를 생성하려면 [Configuring a UDP Listener](https://intl.cloud.tencent.com/document/product/214/32518)에서 자세한 정보를 참고하십시오.
 - TCP SSL 리스너를 생성하려면 [Configuring TCP SSL Listener](https://intl.cloud.tencent.com/document/product/214/32519)에서 자세한 정보를 참고하십시오.
 - HTTP 리스너를 생성하려면 [Configuring HTTP Listener](https://intl.cloud.tencent.com/document/product/214/32515)에서 자세한 정보를 참고하십시오.
 - HTTPS 리스너를 생성하려면 [Configuring HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516)에서 자세한 정보를 참고하십시오.

## TCP 리스너[](id:tcp)
레이어 4 TCP 리스너는 레이어 4 TCP, 레이어 7 HTTP 및 사용자 지정 프로토콜의 세 가지 상태 확인을 지원합니다.
- TCP 상태 확인은 SYN 패킷으로 수행됩니다. 즉, TCP 3방향 핸드셰이크가 시작되어 백엔드 CVM 인스턴스의 상태 정보를 얻습니다.
- HTTP 상태 확인은 백엔드 CVM 인스턴스의 상태 정보를 얻기 위해 HTTP 요청을 전송하여 수행됩니다.
- 사용자 지정 프로토콜 상태 확인은 백엔드 CVM 인스턴스의 상태 정보를 얻기 위해 응용 레이어 프로토콜의 입력 및 출력 내용을 사용자 지정하여 수행됩니다.

### TCP 상태 확인 구성
1. [전제 조건](#postreq)을 참고하여 ‘상태 확인’ 탭으로 이동합니다.
2. ‘상태 확인’ 탭에서 프로토콜로 ‘TCP’를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e2d2dc5608a515513f5a77cb71b7f639.png)
<table>
<tr>
<th>매개변수</th><th>설명</th>
</tr>
<tr>
<td>상태 확인</td><td>활성화되거나 비활성화 될 수 있습니다. 백엔드 CVM 인스턴스에 대한 자동 확인 및 비정상 포트 제거를 활성화하는 것이 좋습니다.</td>
</tr>
<tr>
<td>상태 확인 소스 IP</td><td>기본적으로 CLB VIP인 상태 확인 패킷의 소스 IP입니다. TKE 시나리오에서 컨테이너 루프백 문제를 해결할 수 있는 100.64 IP 범위일 수도 있습니다. 이 기능은 현재 베타 단계에 있습니다. 사용해 보려면 <a href="https://console.cloud.tencent.com/workorder/category">Submit Ticket</a>하십시오.</td>
</tr>
<tr>
<td>프로토콜 확인</td><td>‘TCP’를 선택하면 TCP 상태 확인이 수행됩니다.</td>
</tr>
<tr>
<td>포트 확인</td><td>선택 사항입니다. 특정 포트를 확인해야 하는 경우가 아니면 포트를 지정하지 않는 것이 좋습니다. 여기서 포트를 지정하지 않으면 리얼 서버 포트가 확인됩니다.</td>
</tr>
<tr>
<td>고급 옵션 표시</td><td>자세한 내용은 <a href="#advance">고급 옵션</a>을 참고하십시오.</td>
</tr>
</table>

### HTTP 상태 확인 구성
1. [전제 조건](#postreq)을 참고하여 ‘상태 확인’ 탭으로 이동합니다.
2. ‘상태 확인’ 탭에서 ‘HTTP’를 프로토콜로 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/792bd8086cf30d829c7d8a03dc9b0c78.png)
<table>
<tr>
<th>매개변수</th><th>설명</th>
</tr>
<tr>
<td>상태 확인</td><td>활성화되거나 비활성화 될 수 있습니다. 백엔드 CVM 인스턴스에 대한 자동 확인 및 비정상 포트 제거를 활성화하는 것이 좋습니다.</td>
</tr>
<tr>
<td>상태 확인 소스 IP</td><td>기본적으로 CLB VIP인 상태 확인 패킷의 소스 IP입니다. TKE 시나리오에서 컨테이너 루프백 문제를 해결할 수 있는 100.64 IP 범위일 수도 있습니다. 이 기능은 현재 베타 단계에 있습니다. 사용해 보려면 <a href="https://console.cloud.tencent.com/workorder/category">Submit Ticket</a>하십시오.</td>
</tr>
<tr>
<td>프로토콜</td><td>‘HTTP’를 선택하면 HTTP 상태 확인이 수행됩니다.</td>
</tr>
<tr>
<td>포트 확인</td><td>선택 사항입니다. 특정 포트를 확인해야 하는 경우가 아니면 포트를 지정하지 않는 것이 좋습니다. 여기서 포트를 지정하지 않으면 리얼 서버 포트가 확인됩니다.</td>
</tr>
<tr>
<td>도메인 확인</td><td>상태 확인 도메인 이름에 대한 요구 사항:
<ul>
<li>길이: 1 - 80자.</li>
<li>기본 값: 포워딩 도메인 이름.</li>
<li>정규식은 지원되지 않습니다. 포워딩 도메인 이름이 와일드카드 이름인 경우 고정(비정규) 도메인 이름을 상태 확인 도메인 이름으로 지정해야 합니다.</li>
<li>지원되는 문자: 영어 소문자(a-z), 숫자(0-9), 소수점(.), 하이픈(-).</li>
</ul></td>
</tr>
<tr>
<td>경로 확인</td><td>상태 확인 경로에 대한 요구 사항:
<ul>
<li>길이: 1 - 200자.</li>
<li>/는 기본값이며, 첫 번째 문자여야 합니다.</li>
<li>정규식은 지원되지 않습니다. 상태 확인을 위해 고정 URL(정적 웹 페이지)을 지정하는 것이 좋습니다.</li>
<li>지원되는 문자: 영어 소문자(a-z), 영어 대문자(A-Z), 숫자(0-9), 소수점(.), 하이픈(-), 밑줄(_), 슬래시(/), 등호 (=) 및 물음표(?).</li>
</ul></td>
</tr>
<tr>
<td>HTTP 요청 방법</td><td>상태 확인의 HTTP 요청 방법입니다. 옵션: GET(기본 방법) 및 HEAD.
<ul>
<li>HEAD를 선택하면 서버는 HTTP 헤더 정보만 반환하므로 백엔드 오버헤드를 줄이고 요청 효율성을 높일 수 있습니다. 리얼 서버는 HEAD를 지원해야 합니다.</li>
<li>GET을 선택하면 리얼 서버가 GET을 지원해야 합니다.</li>
</ul></td>
</tr>
<tr>
<td>HTTP 버전</td><td>리얼 서버의 HTTP 버전입니다.
<ul>
<li>리얼 서버에서 지원하는 버전이 HTTP 1.0이면 요청의 Host 필드는 인증이 필요하지 않습니다. 즉, 확인 도메인을 구성할 필요가 없습니다.</li>
<li>리얼 서버에서 지원하는 버전이 HTTP 1.1인 경우 요청의 Host 필드에 인증이 필요합니다. 즉, 확인 도메인을 구성해야 합니다.</li>
</ul>
<dx-alert infotype="explain" title="">
HTTP/1.1 버전을 선택한 경우, 이 때 도메인 이름 확인이 구성되지 않은 경우 HTTP 표준 프로토콜에 따라 백엔드 서버는 상태 확인이 비정상임을 나타내는 오류 코드 400을 반환합니다. <b>정상 상태 코드</b> http_4xx을(를) 선택하는 것이 좋습니다.
</dx-alert>
</td>
</tr>
<tr>
<td>정상 상태 코드</td><td>상태 코드가 선택된 것의 경우 리얼 서버는 활성(정상)으로 간주됩니다. 옵션: http_1xx, http_2xx, http_3xx, http_4xx 및 http_5xx. 여러 상태 코드를 선택할 수 있습니다.</td>
</tr>
<tr>
<td>고급 옵션 표시</td><td>자세한 내용은 <a href="#advance">고급 옵션</a>을 참고하십시오.</td>
</tr>
</table>

### 사용자 지정 프로토콜 상태 확인 구성
1. [전제 조건](#postreq)을 참고하여 ‘상태 확인’ 탭으로 이동합니다.
2. ‘상태 확인’ 탭에서 ‘사용자 지정 프로토콜’을 프로토콜로 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/fd5c4d5442ba8bce5c06a390467f86eb.png)
<table>
<tr>
<th width="25%">매개변수</th><th>설명</th>
</tr>
<tr>
<td>상태 확인</td><td>활성화되거나 비활성화 될 수 있습니다. 백엔드 CVM 인스턴스에 대한 자동 확인 및 비정상 포트 제거를 활성화하는 것이 좋습니다.</td>
</tr>
<tr>
<td>상태 확인 소스 IP</td><td>기본적으로 CLB VIP인 상태 확인 패킷의 소스 IP입니다. TKE 시나리오에서 컨테이너 루프백 문제를 해결할 수 있는 100.64 IP 범위일 수도 있습니다. 이 기능은 현재 베타 단계에 있습니다. 사용해 보려면 <a href="https://console.cloud.tencent.com/workorder/category">Submit Ticket</a>하십시오.</td>
</tr>
<tr>
<td>프로토콜 확인</td><td>‘사용자 지정 프로토콜’을 선택한 경우 사용자 지정 프로토콜 상태 확인이 수행됩니다. 이것은 TCP의 비 HTTP 프로토콜에 적용할 수 있습니다.</td>
</tr>
<tr>
<td>포트 확인</td><td>선택 사항입니다. 특정 포트를 확인해야 하는 경우가 아니면 포트를 지정하지 않는 것이 좋습니다. 여기서 포트를 지정하지 않으면 리얼 서버 포트가 확인됩니다.</td>
</tr>
<tr>
<td>입력 형식</td><td>텍스트 및 16진법 문자열이 지원됩니다.
<ul>
<li>텍스트를 선택하면 요청을 보내고 반환된 결과를 비교하기 위해 텍스트가 이진법 문자열로 변환됩니다.</li>
<li>16진법을 선택하면 요청을 보내고 반환된 결과를 비교하기 위해 16진법 문자열이 이진법 문자열로 변환됩니다.</li>
</ul></td>
</tr>
<tr>
<td>요청 확인</td><td>DNS 서비스 상태 확인을 위한, F13E0100000100000000000003777777047465737403636F6D0774656E63656E7403636F6D0000010001와 같이 필수로 필요한 사용자 지정 상태 확인 요청 콘텐츠입니다.</td>
</tr>
<tr>
<td>반환된 확인 결과</td><td>상태 확인 요청을 사용자 지정할 때 DNS 서비스 상태 확인의 경우 F13E와 같이 반환된 상태 확인 결과를 입력해야 합니다.</td>
</tr>
<tr>
<td>고급 옵션 표시</td><td>자세한 내용은 <a href="#advance">고급 옵션</a>을 참고하십시오.</td>
</tr>
</table>


## UDP 리스너[](id:udp)
UDP 리스너는 포트를 확인하고 PING 명령을 실행하여 수행할 수 있는 UDP 상태 확인을 지원합니다.

### UDP 상태 확인 구성 - 포트 확인
1. [전제 조건](#postreq)을 참고하여 ‘상태 확인’ 탭으로 이동합니다.
2. ‘상태 확인’ 탭에서 ‘포트’를 프로토콜로 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/72052a24264ec37179faa545575979d6.png)
<table>
<tr>
<th width="25%">매개변수</th><th>설명</th>
</tr>
<tr>
<td>상태 확인</td><td>활성화되거나 비활성화 될 수 있습니다. 백엔드 CVM 인스턴스에 대한 자동 확인 및 비정상 포트 제거를 활성화하는 것이 좋습니다.</td>
</tr>
<tr>
<td>상태 확인 소스 IP</td><td>기본적으로 CLB VIP인 상태 확인 패킷의 소스 IP입니다. TKE 시나리오에서 컨테이너 루프백 문제를 해결할 수 있는 100.64 IP 범위일 수도 있습니다. 이 기능은 현재 베타 단계에 있습니다. 사용해 보려면 <a href="https://console.cloud.tencent.com/workorder/category">Submit Ticket</a>하십시오.</td>
</tr>
<tr>
<td>프로토콜 확인</td><td>’포트 확인’을 선택하면 UDP 감지 패킷이 VIP를 통해 백엔드 CVM 인스턴스로 전송되고(즉, 클라이언트에게 서비스를 제공하기 위해 CLB 인스턴스에서 사용하는 IP 주소) 백엔드 CVM 인스턴스의 IP가 Ping되어 백엔드 CVM 인스턴스 상태를 얻습니다.</td>
</tr>
<tr>
<td>포트 확인</td><td>선택 사항입니다. 특정 포트를 확인해야 하는 경우가 아니면 포트를 지정하지 않는 것이 좋습니다. 여기서 포트를 지정하지 않으면 리얼 서버 포트가 확인됩니다.</td>
</tr>
<tr>
<td>입력 형식</td><td>텍스트 및 16진법 문자열이 지원됩니다.
<ul>
<li>텍스트를 선택하면 요청을 보내고 반환된 결과를 비교하기 위해 텍스트가 이진법 문자열로 변환됩니다.</li>
<li>16진법을 선택하면 요청을 보내고 반환된 결과를 비교하기 위해 16진법 문자열이 이진법 문자열로 변환됩니다.</li>
</ul></td>
</tr>
<tr>
<td>요청 확인</td><td>DNS 서비스 상태 확인을 위한, F13E0100000100000000000003777777047465737403636F6D0774656E63656E7403636F6D0000010001와 같은 사용자 지정 상태 확인 요청 콘텐츠입니다.</td>
</tr>
<tr>
<td>반환된 확인 결과</td><td>상태 확인 요청을 사용자 지정할 때 DNS 서비스 상태 확인의 경우 F13E와 같이 반환된 상태 확인 결과를 구성해야 합니다.</td>
</tr>
<tr>
<td>고급 옵션 표시</td><td>자세한 내용은 <a href="#advance">고급 옵션</a>을 참고하십시오.</td>
</tr>
</table>


### UDP 상태 확인 구성 - PING 명령
1. [전제 조건](#postreq)을 참고하여 ‘상태 확인’ 탭으로 이동합니다.
2. ‘상태 확인’ 탭에서 프로토콜로 ‘PING’을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/116957dad78ba97cde202151eba54757.png)
<table>
<tr>
<th>매개변수</th><th>설명</th>
</tr>
<tr>
<td>상태 확인</td><td>활성화되거나 비활성화 될 수 있습니다. 백엔드 CVM 인스턴스에 대한 자동 확인 및 비정상 포트 제거를 활성화하는 것이 좋습니다.</td>
</tr>
<tr>
<td>상태 확인 소스 IP</td><td>기본적으로 CLB VIP인 상태 확인 패킷의 소스 IP입니다. TKE 시나리오에서 컨테이너 루프백 문제를 해결할 수 있는 100.64 IP 범위일 수도 있습니다. 이 기능은 현재 베타 단계에 있습니다. 사용해 보려면 <a href="https://console.cloud.tencent.com/workorder/category">Submit Ticket</a>하십시오.</td>
</tr>
<tr>
<td>프로토콜 확인</td><td>‘PING’을 선택하면 백엔드 CVM 인스턴스의 IP가 Ping되어 백엔드 CVM 인스턴스 상태를 얻습니다.</td>
</tr>
<tr>
<td>고급 옵션 표시</td><td>자세한 내용은 <a href="#advance">고급 옵션</a>을 참고하십시오.</td>
</tr>
</table>


## TCP SSL 리스너[](id:tcp-ssl)

### TCP 상태 확인 구성
1. [전제 조건](#postreq)을 참고하여 ‘상태 확인’ 탭으로 이동합니다.
2. ‘상태 확인’ 탭에서 프로토콜로 ‘TCP’를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d0e44625bb1e61658f43143a5a5c4637.png)
<table>
<tr>
<th>매개변수</th><th>설명</th>
</tr>
<tr>
<td>상태 확인</td><td>활성화되거나 비활성화 될 수 있습니다. 백엔드 CVM 인스턴스에 대한 자동 확인 및 비정상 포트 제거를 활성화하는 것이 좋습니다.</td>
</tr>
<tr>
<td>상태 확인 소스 IP</td><td>기본적으로 CLB VIP인 상태 확인 패킷의 소스 IP입니다. TKE 시나리오에서 컨테이너 루프백 문제를 해결할 수 있는 100.64 IP 범위일 수도 있습니다. 이 기능은 현재 베타 단계에 있습니다. 사용해 보려면 <a href="https://console.cloud.tencent.com/workorder/category">Submit Ticket</a>하십시오.</td>
</tr>
<tr>
<td>프로토콜 확인</td><td>‘TCP’를 선택하면 TCP 상태 확인이 수행됩니다.</td>
</tr>
<tr>
<td>포트 확인</td><td>TCP SSL 리스너의 상태 확인 포트와 수신 포트는 동일합니다.</td>
</tr>
<tr>
<td>고급 옵션 표시</td><td>자세한 내용은 <a href="#advance">고급 옵션</a>을 참고하십시오.</td>
</tr>
</table>

### HTTP 상태 확인 구성
1. [전제 조건](#postreq)을 참고하여 ‘상태 확인’ 탭으로 이동합니다.
2. ‘상태 확인’ 탭에서 ‘HTTP’를 프로토콜로 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/84cbb3b6477a6aa35b34cf5c9cab2009.png)
<table>
<tr>
<th>매개변수</th><th>설명</th>
</tr>
<tr>
<td>상태 확인</td><td>활성화되거나 비활성화 될 수 있습니다. 백엔드 CVM 인스턴스에 대한 자동 확인 및 비정상 포트 제거를 활성화하는 것이 좋습니다.</td>
</tr>
<tr>
<td>상태 확인 소스 IP</td><td>기본적으로 CLB VIP인 상태 확인 패킷의 소스 IP입니다. TKE 시나리오에서 컨테이너 루프백 문제를 해결할 수 있는 100.64 IP 범위일 수도 있습니다. 이 기능은 현재 베타 단계에 있습니다. 사용해 보려면 <a href="https://console.cloud.tencent.com/workorder/category">Submit Ticket</a>하십시오.</td>
</tr>
<tr>
<td>프로토콜</td><td>‘HTTP’를 선택하면 HTTP 상태 확인이 수행됩니다.</td>
</tr>
<tr>
<td>포트 확인</td><td>TCP SSL 리스너의 상태 확인 포트와 수신 포트는 동일합니다.</td>
</tr>
<tr>
<td>도메인 확인</td><td>상태 확인 도메인 이름에 대한 요구 사항:
<ul>
<li>길이: 1 - 80자.</li>
<li>기본 값: 포워딩 도메인 이름.</li>
<li>정규식은 지원되지 않습니다. 포워딩 도메인 이름이 와일드카드 이름인 경우 고정(비정규) 도메인 이름을 상태 확인 도메인 이름으로 지정해야 합니다.</li>
<li>지원되는 문자: 영어 소문자(a-z), 숫자(0-9), 소수점(.), 하이픈(-).</li>
</ul></td>
</tr>
<tr>
<td>경로 확인</td><td>상태 확인 경로에 대한 요구 사항:
<ul>
<li>길이: 1 - 200자.</li>
<li>/는 기본값이며, 첫 번째 문자여야 합니다.</li>
<li>정규식은 지원되지 않습니다. 상태 확인을 위해 고정 URL(정적 웹 페이지)을 지정하는 것이 좋습니다.</li>
<li>지원되는 문자: 영어 소문자(a-z), 영어 대문자(A-Z), 숫자(0-9), 소수점(.), 하이픈(-), 밑줄(_), 슬래시(/), 등호 (=) 및 물음표(?).</li>
</ul></td>
</tr>
<tr>
<td>HTTP 요청 방법</td><td>상태 확인의 HTTP 요청 방법입니다. 옵션: GET(기본 방법) 및 HEAD.
<ul>
<li>HEAD를 선택하면 서버는 HTTP 헤더 정보만 반환하므로 백엔드 오버헤드를 줄이고 요청 효율성을 높일 수 있습니다. 리얼 서버는 HEAD를 지원해야 합니다.</li>
<li>GET을 선택하면 리얼 서버가 GET을 지원해야 합니다.</li>
</ul></td>
</tr>
<tr>
<td>HTTP 버전</td><td>리얼 서버의 HTTP 버전입니다. HTTP 1.1만 지원됩니다. 리얼 서버는 요청의 Host 필드를 인증해야 합니다. 즉, 확인 도메인을 구성해야 합니다.
<dx-alert infotype="explain" title="">
도메인 이름 확인이 구성되지 않은 경우 HTTP 표준 프로토콜에 따라 백엔드 서버는 상태 확인이 비정상임을 나타내는 오류 코드 400을 반환합니다. <b>정상 상태 코드</b> http_4xx을(를) 선택하는 것이 좋습니다.
</dx-alert>
</td>
</tr>
<tr>
<td>정상 상태 코드</td><td>상태 코드가 선택된 것의 경우 리얼 서버는 활성(정상)으로 간주됩니다. 옵션: http_1xx, http_2xx, http_3xx, http_4xx 및 http_5xx. 여러 상태 코드를 선택할 수 있습니다.</td>
</tr>
<tr>
<td>고급 옵션 표시</td><td>자세한 내용은 <a href="#advance">고급 옵션</a>을 참고하십시오.</td>
</tr>
</table>

[](id:http)
## HTTP 리스너[](id:http)
### HTTP 상태 확인 구성
1. [전제 조건](#postreq)을 참고하여 ‘상태 확인’ 탭으로 이동합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7c87cf8289ae26e1be279afc290b77da.png)
<table>
<tr>
<th>매개변수</th><th>설명</th>
</tr>
<tr>
<td>상태 확인</td><td>활성화되거나 비활성화 될 수 있습니다. 백엔드 CVM 인스턴스에 대한 자동 확인 및 비정상 포트 제거를 활성화하는 것이 좋습니다.</td>
</tr>
<tr>
<td>상태 확인 소스 IP</td><td>기본적으로 CLB VIP인 상태 확인 패킷의 소스 IP입니다. TKE 시나리오에서 컨테이너 루프백 문제를 해결할 수 있는 100.64 IP 범위일 수도 있습니다. 이 기능은 현재 베타 단계에 있습니다. 사용해 보려면 <a href="https://console.cloud.tencent.com/workorder/category">Submit Ticket</a>하십시오.</td>
</tr>
<tr>
<td>도메인 확인</td><td>상태 확인 도메인 이름에 대한 요구 사항:
<ul>
<li>길이: 1 - 80자.</li>
<li>기본 값: 포워딩 도메인 이름.</li>
<li>정규식은 지원되지 않습니다. 포워딩 도메인 이름이 와일드카드 이름인 경우 고정(비정규) 도메인 이름을 상태 확인 도메인 이름으로 지정해야 합니다.</li>
<li>지원되는 문자: 영어 소문자(a-z), 숫자(0-9), 소수점(.), 하이픈(-).</li>
</ul></td>
</tr>
<tr>
<td>경로 확인</td><td>상태 확인 경로는 리얼 서버의 루트 디렉터리 또는 지정된 URL로 설정할 수 있습니다. 요구 사항은 다음과 같습니다.
<ul>
<li>길이: 1 - 200자.</li>
<li>/는 기본값이며, 첫 번째 문자여야 합니다.</li>
<li>정규식은 지원되지 않습니다. 상태 확인을 위해 고정 URL(정적 웹 페이지)을 지정하는 것이 좋습니다.</li>
<li>지원되는 문자: 영어 소문자(a-z), 영어 대문자(A-Z), 숫자(0-9), 소수점(.), 하이픈(-), 밑줄(_), 슬래시(/), 등호 (=) 및 물음표(?).</li>
</ul>
</td>
</tr>
<tr>
<td>응답 시간 초과</td><td><ul><li> 상태 확인에 대한 최대 응답 시간 초과입니다. </li><li>리얼 서버가 제한 시간 내에 응답하지 않으면 비정상으로 간주됩니다. </li><li>값 범위: 2 - 60초.</li></ul></td>
</tr>
<tr>
<td>확인 간격</td><td><ul><li>두 상태 확인 사이의 간격입니다. </li><li>값 범위: 2 - 300초.</li></ul></td>
</tr>
<tr>
<td>비정상 임계값</td><td><ul><li>상태 확인 결과가 n회(n은 사용자 지정 가능한 값) 동안 실패하면 백엔드 CVM 인스턴스가 비정상으로 간주되어 콘솔에 표시되는 상태가 비정상입니다.</li><li>값 범위: 2 - 10회.</li></ul></td>
</tr>
<tr>
<td>상태 임계값</td><td><ul><li>상태 확인 결과가 n회(n은 사용자 지정 가능한 값) 동안 성공하면 백엔드 CVM 인스턴스가 정상으로 간주되고 콘솔에 표시되는 상태가 정상입니다.</li><li>값 범위: 2 - 10회. </li></ul></td>
</tr>
<tr>
<td>HTTP 요청 방법</td><td>상태 확인의 HTTP 요청 방법입니다. 옵션: GET(기본 방법) 및 HEAD.
<ul>
<li>HEAD를 선택하면 서버는 HTTP 헤더 정보만 반환하므로 백엔드 오버헤드를 줄이고 요청 효율성을 높일 수 있습니다. 리얼 서버는 HEAD를 지원해야 합니다.</li>
<li>GET을 선택하면 리얼 서버가 GET을 지원해야 합니다.</li>
</ul></td>
</tr>
<tr>
<td>정상 상태 코드</td><td>상태 코드가 선택된 것의 경우 리얼 서버는 활성(정상)으로 간주됩니다. 옵션: http_1xx, http_2xx, http_3xx, http_4xx 및 http_5xx. 여러 상태 코드를 선택할 수 있습니다.</td>
</tr>
</table>

## HTTPS 리스너[](id:https)
>?HTTPS 리스너 포워딩 규칙의 백엔드 프로토콜로 HTTP를 선택하면 HTTP 상태 확인이 수행됩니다. HTTPS를 선택하면 HTTPS 상태 확인이 수행됩니다.
>
HTTPS 리스너의 상태 확인 구성은 <a href="#http">HTTP 리스너</a>를 참고하십시오.

[](id:advance)
## 고급 옵션
| 상태 확인 구성    | 설명                    | 기본값                               |
| ------- | ------------------------ | ---------------------------------------- |
| 응답 시간 초과 | <li> 상태 확인에 대한 최대 응답 시간 초과입니다. </li><li>리얼 서버가 제한 시간 내에 응답하지 않으면 비정상으로 간주됩니다. </li><li>값 범위: 2 - 60초.</li> | 2초 |
| 확인 간격 | <li>두 상태 확인 사이의 간격입니다. </li><li>값 범위: 2 - 300초.</li> | 5초 |
| 비정상 임계값 | <li>상태 확인 결과가 n회(n은 사용자 지정 가능한 값) 동안 실패하면 백엔드 CVM 인스턴스가 비정상으로 간주되어 콘솔에 표시되는 상태가 **비정상**입니다. </li><li>값 범위: 2 - 10회.</li> | 3회 |
| 정상 임계값 |<li>상태 확인 결과가 n회(n은 사용자 지정 가능한 값) 동안 성공하면 백엔드 CVM 인스턴스가 정상으로 간주되고 콘솔에 표시되는 상태가 **정상**입니다.</li><li>값 범위: 2 - 10회. </li> | 3회 |



## 관련 문서
- [Health Check Overview](https://intl.cloud.tencent.com/document/product/214/6097)
- [Configuring Alarm Policy](https://intl.cloud.tencent.com/document/product/214/8886)
