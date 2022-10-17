CLB 인스턴스에 대한 TCP SSL 리스너를 만들어 클라이언트에서 암호화된 TCP 요청을 포워딩할 수 있습니다. TCP SSL은 초고성능 및 대규모 TLS 오프로딩이 필요한 시나리오에 적용할 수 있습니다. TCP SSL 리스너의 경우 실제 서버가 실제 클라이언트 IP를 직접 가져올 수 있습니다.
>?TCP SSL 리스너는 현재 CLB에 대해서만 지원되지만 클래식 CLB에는 지원되지 않습니다.
>


## 전제 조건
먼저 [CLB 인스턴스를 생성](https://intl.cloud.tencent.com/document/product/214/6149)해야 합니다.

## 작업 단계
### 1단계: 리스너 구성
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인하고 왼쪽 사이드바에서 **인스턴스 관리**를 클릭합니다.
2. CLB 인스턴스 목록 페이지의 왼쪽 상단 모서리에서 리전을 선택하고 오른쪽의 작업 열에서 **리스너 구성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e3b94945c6dbe084ba51e1e22b46b341.png)
3. TCP/UDP/TCP SSL/QUIC 리스너에서 **생성**을 클릭하고 ‘리스너 생성’ 팝업 창에서 TCP SSL 리스너를 구성합니다.
 **a. 기본 구성**
<table>
<thead>
<tr>
<th width="15%">구성 항목</th>
<th width="70%">설명</th>
<th width="15%">예시</th>
</tr>
</thead>
<tbody><tr>
<td>이름</td>
<td>리스너 이름입니다.</td>
<td><span>test-tcpssl-9000&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>리스너 프로토콜 및 포트</td>
<td><ul><li>리스너 프로토콜: TCP SSL이 이 예시에서 사용됩니다. </li><li>리스너 포트: 요청을 수신하여 실제 서버로 포워딩하는 데 사용되는 포트입니다. 포트 범위: 1 - 65535. </li><li>리스너 포트는 동일한 CLB 인스턴스에서 고유해야 합니다. </li></ul></td>
<td>TCP SSL:9000</td>
</tr>
<tr>
<td>SSL 파싱 메소드</td>
<td>단방향 인증 및양방향 인증이 지원됩니다.</td>
<td>단방향 인증</td>
</tr>
<tr>
<td>서버 인증서</td>
<td><a href="https://console.cloud.tencent.com/ssl">SSL 인증서 서비스</a>에서 기존 인증서를 선택하거나 인증서를 업로드할 수 있습니다.</td>
<td>기존 인증서</td>
</tr>
<tr>
<td>분산 방식</td>
<td>TCP SSL 리스너의 경우 CLB는 WRR(가중 라운드 로빈) 및 WLC(가중 최소 연결)의 두 가지 스케쥴링 알고리즘을 지원합니다. <br><ul><li>WRR: 요청이 가중치에 따라 다른 실제 서버에 순차적으로 전달됩니다. 스케쥴링은 <strong>새 연결 수</strong>를 기반으로 수행됩니다. 여기서 가중치가 더 높은 서버는 더 많은 폴링(즉, 더 높은 확률)을 받는 반면 동일한 가중치를 가진 서버는 동일한 수의 연결을 처리합니다.</li><li>WLC: 서버에 대한 활성 연결 수에 따라 서버 부하가 추정됩니다. 스케쥴링은 서버 로드 및 가중치를 기반으로 수행됩니다. 가중치가 같으면 활성 연결이 적은 서버가 더 많은 폴링을 받게 됩니다(즉, 더 높은 확률). </li></ul></td>
<td>WRR</td>
</tr>
</tbody></table>
 <b>b. 상태 확인</b></br>
자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/214/39251">TCP SSL 상태 확인</a>을 참고하십시오.</br>
 <b>c. 세션 지속성(현재 지원되지 않음)</b></br>
TCP SSL 리스너는 현재 세션 지속성을 지원하지 않습니다.

### 2단계: 실제 서버 바인딩
1. ‘리스너 관리’ 페이지에서 생성된 리스너 `TCP SSL:9000`을 클릭하면 리스너 오른쪽에 바인딩된 실제 서버가 표시됩니다.
2. **바인딩**을 클릭하고 대상 실제 서버를 선택하고 팝업 창에서 서버 포트 및 가중치를 구성합니다.
>? 기본 포트: ‘기본 포트’를 먼저 입력한 다음 CVM 인스턴스를 선택합니다. 모든 CVM 인스턴스의 포트는 기본 포트입니다.
>

### 3단계: 보안 그룹 구성(선택 사항)
공중망 트래픽을 격리하도록 CLB 보안 그룹을 구성할 수 있습니다. 자세한 내용은 [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733)을 참고하십시오.

### 4단계: 리스너 수정 및 삭제(선택 사항)
생성된 리스너를 수정하거나 삭제해야 하는 경우 ‘리스너 관리’ 페이지에서 리스너를 클릭하고 ![](https://qcloudimg.tencent-cloud.cn/raw/4ab10b98316964812832043bbfd99df6.svg) 수정 또는 ![](https://qcloudimg.tencent-cloud.cn/raw/e863cc51c29790d665d53feba800fd90.svg) 삭제를 클릭합니다.
