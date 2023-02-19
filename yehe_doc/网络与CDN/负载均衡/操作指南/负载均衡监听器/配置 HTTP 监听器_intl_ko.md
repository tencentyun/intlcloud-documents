CLB 인스턴스에 대한 HTTP 리스너를 만들어 클라이언트의 HTTP 요청을 포워딩할 수 있습니다. HTTP는 Web 애플리케이션 및 모바일 App과 같이 요청 내용을 식별해야 하는 애플리케이션에 적합합니다.

## 전제 조건
먼저 [CLB 인스턴스를 생성](https://intl.cloud.tencent.com/document/product/214/6149)해야 합니다.

## 작업 단계
### 1단계: 리스너 구성
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인하고 왼쪽 사이드바에서 **인스턴스 관리**를 클릭합니다.
2. CLB 인스턴스 목록 페이지의 왼쪽 상단 모서리에서 리전을 선택하고 오른쪽의 작업 열에서 **리스너 구성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e3b94945c6dbe084ba51e1e22b46b341.png)
3. HTTP/HTTPS 리스너에서 **생성**을 클릭하고 ‘리스너 생성’ 팝업 창에서 HTTP 리스너를 구성합니다.
 **1. 리스너 생성**
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
<td>리스너의 이름입니다.</td>
<td><span>test-http-80</span></td>
</tr>
<tr>
<td>리스너 프로토콜 및 포트</td>
<td>
<ul><li>리스너 프로토콜: 이 예시에서는 HTTP가 사용됩니다. </li><li>리스너 포트: 요청을 수신하여 리얼 서버로 포워딩하는 데 사용되는 포트입니다. 포트 범위: 1 - 65535. 포트 843, 1020, 1433, 1434, 3306, 3389, 6006, 20000, 36000, 42222, 48369, 56000 및 65010은 시스템 예약 포트이며 열 수 없습니다. </li><li>리스너 포트는 동일한 CLB 인스턴스에서 고유해야 합니다. </li></ul></td>
<td>HTTP:80</td>
</tr>
<tr>
<td>지속적인 연결 활성화</td>
<td>이 기능이 활성화되면 CLB와 리얼 서버 간에 지속적인 연결이 사용되며 CLB는 XFF에서 얻을 수 있는 소스 IP를 더 이상 통과하지 않습니다. 정상적인 포워딩을 위해서는 CLB 보안 그룹에서 기본적으로 허용 기능을 활성화하거나 CVM 보안 그룹에서 100.127.0.0/16을 허용합니다.
<dx-alert infotype="explain" title="">
이 기능이 활성화되면 CLB와 백엔드 서비스 간의 연결 수는 연결 재사용률에 따라 [QPS, QPS*60] 범위에서 변동됩니다. 백엔드 서비스에 최대 연결 수에 대한 제한이 있는 경우 이 기능을 활성화할 때 주의하는 것이 좋습니다. 이 기능은 현재 베타 테스트 중입니다. 사용해 보려면 [티켓 제출](https://console.tencentcloud.com/workorder/category)하십시오.
</dx-alert>
</td>
<td><span>활성화</span></td>
</tr>
</tbody>
</table>
 <b>2. 포워딩 규칙 생성</b>
<table>
<thead>
<tr>
<th width="15%">포워딩 규칙 구성</th>
<th width="70%">설명</th>
<th width="15%">예시</th>
</tr>
</thead>
<tbody><tr>
<td>도메인 이름</td>
<td>포워딩 도메인 이름: <ul style="margin-bottom:0px;"><li>길이: 1 - 80자.</li><li>밑줄 `_`로 시작할 수 없습니다. </li><li>정확한 도메인 이름과 와일드카드 도메인 이름이 지원됩니다. </li><li>정규식이 지원됩니다. </li><li>자세한 구성 규칙은 <a href="https://intl.cloud.tencent.com/document/product/214/9032">레이어 7 도메인 이름 포워딩 및 URL 규칙</a>을 참고하십시오.</li></ul></td>
<td><span>www.example.com</span></td>
</tr>
<tr>
<td>기본 도메인 이름</td>
<td>리스너의 모든 도메인 이름이 일치하지 않으면 시스템은 요청을 기본 도메인 이름으로 보내 기본 액세스를 제어할 수 있게 합니다. 각 리스너는 기본 도메인 이름 하나만으로 구성할 수 있습니다.</td>
<td><span>기본적으로 활성화</span></td>
</tr>
<tr>
<td>URL 경로</td>
<td>
포워딩 URL 경로: <ul style="margin-bottom:0px;"><li>길이: 1 - 200자. </li><li>정규식이 지원됩니다. </li><li>자세한 구성 규칙은 <a href="https://intl.cloud.tencent.com/document/product/214/9032">Layer-7 도메인 이름 포워딩 및 URL 규칙</a>을 참고하십시오.</li></ul></td>
<td>/index</td>
</tr>
<tr>
<td>분산 방식</td>
<td>HTTP 리스너의 경우 CLB는 WRR(가중 라운드 로빈), WLC(가중 최소 연결) 및 IP Hash의 세 가지 스케쥴링 알고리즘을 지원합니다. <ul style="margin-bottom:0px;"><li>WRR: 요청이 가중치에 따라 다른 리얼 서버에 순차적으로 전달됩니다. 스케쥴링은 <b>새 연결 수</b>를 기반으로 수행됩니다. 여기서 가중치가 더 높은 서버는 더 많은 폴링(즉, 더 높은 확률)을 받는 반면 동일한 가중치를 가진 서버는 동일한 수의 연결을 처리합니다. </li><li>WLC: 서버에 대한 활성 연결 수에 따라 서버 부하가 추정됩니다. 스케쥴링은 서버 로드 및 가중치를 기반으로 수행됩니다. 가중치가 같으면 활성 연결이 적은 서버가 더 많은 폴링을 받게 됩니다(즉, 더 높은 확률). </li><li>IP Hash: 해시 키(Hash Key)는 요청의 소스 IP를 기반으로 정적 해시 테이블에서 해당 서버를 찾는 데 사용됩니다. 서버를 사용할 수 있고 오버로드되지 않은 경우 요청이 해당 서버로 전달됩니다. 그렇지 않으면 null 값이 반환됩니다.</li></ul></td>
<td>WRR</td>
</tr>
<tr>
<td>클라이언트 IP 가져오기</td>
<td>기본적으로 활성화</td>
<td>활성화됨</td>
</tr>
<tr>
<td>Gzip 압축</td>
<td>기본적으로 활성화</td>
<td>활성화됨</td>
</tr>
</tbody>
</table>
<b>3. 상태 확인</b></br>
자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/214/39251">HTTP 상태 확인</a>을 참고하십시오.</br> 
<b>4. 세션 지속성</b></br>
<table>
<tr>
<th width="12%">세션 지속성 구성</th>
<th>설명</th>
<th>예시</th>
</tr>
<tr>
<td>세션 지속성 스위치</td>
<td> <ul><li>세션 지속성이 활성화되면 CLB 리스너는 동일한 클라이언트에서 동일한 리얼 서버로 액세스 요청을 분산합니다. </li><li>TCP 세션 지속성은 클라이언트 IP 주소를 기반으로 구현됩니다. 동일한 IP 주소의 액세스 요청은 동일한 리얼 서버로 포워딩됩니다. </li><li>세션 지속성은 WRR 스케쥴링에 대해 활성화할 수 있지만 WLC 스케쥴링에는 활성화할 수 없습니다.</li></ul></td>
<td>활성화</td>
</tr>
<tr>
<td>세션 지속 시간</td>
<td><ul><li>세션 지속 기간을 초과하여 연결 내에서 새 요청이 없으면 세션 지속이 자동으로 비활성화됩니다. </li><li>값 범위: 30 - 3600초.</li></ul></td>
<td>30s</td>
</tr>
</table>


### 2단계: 실제 서버 바인딩
1. ‘리스너 관리’ 페이지에서 생성된 리스너 `HTTP:80`을 선택합니다. 왼쪽의 **+**를 클릭하여 도메인 이름과 URL 경로를 확장하고 원하는 URL 경로를 선택하면 리스너 오른쪽의 경로에 바인딩된 리얼 서버를 볼 수 있습니다.
2. **바인딩**을 클릭하고 대상 실제 서버를 선택하고 팝업 창에서 서버 포트 및 가중치를 구성합니다.
>? 기본 포트: ‘기본 포트’를 먼저 입력한 다음 CVM 인스턴스를 선택합니다. 모든 CVM 인스턴스의 포트는 기본 포트입니다.
>


### 3단계: 보안 그룹 구성(선택 사항)
공중망 트래픽을 격리하도록 CLB 보안 그룹을 구성할 수 있습니다. 자세한 내용은 [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733)을 참고하십시오.

### 4단계: 리스너 수정 및 삭제(선택 사항)
생성된 리스너를 수정하거나 삭제해야 하는 경우 ‘리스너 관리’ 페이지에서 리스너를 클릭하고 ![](https://qcloudimg.tencent-cloud.cn/raw/4ab10b98316964812832043bbfd99df6.svg) 수정 또는 ![](https://qcloudimg.tencent-cloud.cn/raw/e863cc51c29790d665d53feba800fd90.svg) 삭제를 클릭합니다.

