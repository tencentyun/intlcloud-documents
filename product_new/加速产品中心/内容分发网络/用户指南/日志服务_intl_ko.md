- 기능 소개
  도메인이 CDN 에 연결되면 모든 사용자 측 자원 요청은 응답을 위해 CDN 노드로 스케줄링되고, 노드가 해당 자원을 캐시한 경우에는 콘텐츠가 직접 반환되며, CDN 노드가 해당 자원을 캐시하지 않은 경우에는 도메인 설정의 오리진 서버로 요청이 전달되어 필요한 자원을 끌어냅니다.

CDN 노드는 대부분의 사용자 요청에 대한 응답으로 사용자 액세스를 분석할 수 있도록 전체 네트워크 액세스 로그를 30 일 동안 기본 스토리지로 데이터 분할 하고 다운로드 서비스를 제공합니다.

> 은 (는) 일시적으로 노드 액세스 로그만 제공하며 Origin-pull 로그로 제공되지 않습니다.

## 적용 시나리오

### 액세스 분석

고객은 액세스 로그를 다운로드하여 자신의 필요에 따라 핫 리소스 분석, 액티브 사용자 분석 등을 수행할 수 있습니다.

### 서비스 품질 모니터링

액세스 로그를 다운로드하여 전체 CDN 노드 서비스 상태를 파악하고 평균 응답 시간, 평균 다운로드 속도 등의 지표를 계산할 수 있습니다.

## 운영 가이드

### 사용 방법

[CDN 콘솔] (https://console.cloud.tencent.com/cdn) 에 로그인하고 왼쪽 목록 [로그 서비스] 를 클릭하여 도메인, 액세스 로그 쿼리 시간, 여러 로그 패키지 선택 지원, 로컬에 대량 다운로드 가능합니다:
![](https://mc.qcloudimg.com/static/img/043e70b6829ce67d6af125b51736b249/1.png)

> -액세스 로그는 기본적으로 시간별로 패키지화되며, 도메인에 요청이 없을 경우 시간 간격에 대한 로그 패키지가 생성되지 않습니다.
> -동일한 도메인의 해외 액세스 로그는 내부 액세스 로그와 별도로 패킹되며 로그 패킷의 이름 지정 형식은 "시간-도메인-가속 영역" 입니다.
> -액세스 로그는 각 CDN 가속 노드에서 수집하므로 지연이 다양하며 일반적으로 로그 패키지는 쿼리 가능하고 30분 좌우 다운로드 지연은 발생하며 로그 팩은 계속 추가되며 일반적으로 2-3 시간 후에 안정화되는 경향이 있습니다.
> -도메인 이름 내역 액세스 로그는 30 일 이내의 로그 패키지만 보관하며, 아래 가이드에 따라 SCF 함수를 활용하여 로그 패키지를 오브젝트 스토리지 COS 로 영구 저장할 수 있습니다.

### 필드 설명

로그의 해당 필드 순서 (왼쪽에서 오른쪽으로) 및 그 의미는 다음 표에 표시 되어 있습니다.

<table  style="width:494px">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">순서</th>
<th align="left" style="width:560px;font-weight:700">로그 콘텐츠  </th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>요청시간</td>
</tr>
</tbody>
<tbody><tr>
<td>2</td>
<td>클라이언트 IP</td>
</tr>
</tbody>
<tbody><tr>
<td>3</td>
<td>도메인</td>
</tr>
</tbody>
<tbody><tr>
<td>4</td>
<td>요청 경로</td>
</tr>
</tbody>
<tbody><tr>
<td>5</td>
<td>파일 자체 크기 및 요청 header 크기를 포함하는 액세스 바이트 크기</td>
</tr>
</tbody>
<tbody><tr>
<td>6</td>
<td>국내 로그는 Province 번호를 나타내고 해외 로그는 지역 번호를 나타냅니다 (매핑 테이블은 아래 참조)</td>
</tr>
</tbody>
<tbody><tr>
<td>7</td>
<td>국내 로그는 통신업체 번호를 나타내며 해외 로그는 -1 로 통일됩니다 (매핑 테이블은 아래 참조)</td>
</tr>
</tbody>
<tbody><tr>
<td>8</td>
<td>HTTP 상태 코드</td>
</tr>
</tbody>
<tbody><tr>
<td>9</td>
<td>Referer 정보</td>
</tr>
</tbody>
<tbody><tr>
<td>10</td>
<td>응답 시간 (밀리초) 은 노드가 요청을 받은 후 모든 패킷에 응답하고 클라이언트로 다시 응답하는 데 걸리는 시간입니다.</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>11</td>
<td>User-Agent 정보</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>12</td>
<td>Range 파라미터</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>13</td>
<td>HTTP Method</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>14</td>
<td>HTTP 프로토콜 로고</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>15</td>
<td>캐시 HIT/MISS, CDN 에지 노드 적중,  노드 적중시 모두 HIT</td > 로 표시
</tr>
</tbody></table>

### 리전 / 통신사 매핑 테이블

#### 국내 provinces 매핑

<table  style="width:494px">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">리전 ID</th>
<th align="left" style="width:120px;font-weight:700">지역</th>
<th align="left" style="width:100px;font-weight:700">리전 ID</th>
<th align="left" style="width:120px;font-weight:700">지역</th>
<th align="left" style="width:100px;font-weight:700">리전 ID</th>
<th align="left" style="width:120px;font-weight:700">지역</th>
</tr>
</thead>
<tbody><tr>
<td>22</td>
<td>베이징</td>
<td>86</td>
<td>내몽고</td>
<td>146</td>
<td>산서</td>
</tr>
<tr>
<td>1069</td>
<td>하북</td>
<td>1177</td>
<td>톈진</td>
<td>119</td>
<td>닝샤</td>
</tr>
<tr>
<td>152</td>
<td>섬서</td>
<td>1208</td>
<td>간쑤</td>
<td>1467</td>
<td>칭하이</td>
</tr>
<tr>
<td>1468</td>
<td>신강</td>
<td>145</td>
<td>흑룡강</td>
<td>1445</td>
<td>길림</td>
</tr>
<tr>
<td>1464</td>
<td>료녕</td>
<td>2</td>
<td>복건</td>
<td>120</td>
<td>강서</td>
</tr>
<tr>
<td>121</td>
<td>안휘</td>
<td>122</td>
<td>산동</td>
<td>1050</td>
<td>상해</td>
</tr>
<tr>
<td>1442</td>
<td>절강</td>
<td>182</td>
<td>하남</td>
<td>1135</td>
<td>호북</td>
</tr>
<tr>
<td>1465</td>
<td>강서</td>
<td>1466</td>
<td>호남</td>
<td>118</td>
<td>구이저우</td>
</tr>
<tr>
<td>153</td>
<td>운남</td>
<td>1051</td>
<td>충칭</td>
<td>1068</td>
<td>사천</td>
</tr>
<tr>
<td>1155</td>
<td>티베트</td>
<td>4</td>
<td>광동</td>
<td>173</td>
<td>광서</td>
</tr>
<tr>
<td>1441</td>
<td>해남</td>
<td>0</td>
<td>기타</td>
<td>1</td>
<td>홍콩 마카오 대만</td>
</tr>
<tr>
<td>-1</td>
<td>해외</td>
<td>-</td>
<td>-</td>
<td>-</td>
<td>-</td>
</tr>
</tbody></table>



#### 국내 통신사 매핑

<table  style="width:494px">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">통신사 ID</th>
<th align="left" style="width:120px;font-weight:700">통신사</th>
<th align="left" style="width:100px;font-weight:700">통신사 ID</th>
<th align="left" style="width:120px;font-weight:700">통신사</th>
<th align="left" style="width:100px;font-weight:700">통신사 ID</th>
<th align="left" style="width:120px;font-weight:700">통신사</th>
</tr>
</thead>
<tbody><tr>
<td>2</td>
<td>China Telecom</td>
<td>26</td>
<td>China Unicom</td>
<td>38</td>
<td>교육 네트워크</td>
</tr>
</tbody>
<tbody><tr>
<td>43</td>
<td>만리장성 인터넷 서비스</td>
<td>1046</td>
<td>China Mobile</td>
<td>3947</td>
<td>China Railcom</td>
</tr>
</tbody>
<tbody><tr>
<td>-1</td>
<td>해외 통신사</td>
<td>0</td>
<td>기타 통신사</td>
<td>-</td>
<td>-</td>
</tr>
</tbody>
<table >



### 해외 지역 매핑

<table  style="width:494px">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">리전 ID</th>
<th align="left" style="width:170px;font-weight:700">지역</th>
<th align="left" style="width:100px;font-weight:700">리전 ID</th>
<th align="left" style="width:120px;font-weight:700">지역</th>
<th align="left" style="width:100px;font-weight:700">리전 ID</th>
<th align="left" style="width:120px;font-weight:700">지역</th>
</tr>
</thead>
<tbody><tr>
<td>2000000001</td>
<td>아시아 태평양 1지역 (서비스 지역)</td>
<td>765</td>
<td>슬로바키아</td>
<td>1613</td>
<td>앙골라</td>
</tr>
<tr>
<td>2000000002</td>
<td>아시아 태평양 2지역 (서비스 지역)</td>
<td>766</td>
<td>세르비아</td>
<td>1617</td>
<td>코트디부아르</td>
</tr>
<tr>
<td>2000000003</td>
<td>아시아 태평양 3지역 (서비스 지역)</td>
<td>770</td>
<td>핀란드</td>
<td>1620</td>
<td>수단</td>
</tr>
<tr>
<td>2000000004</td>
<td>중동(서비스 지역)</td>
<td>773</td>
<td>벨기에</td>
<td>1681</td>
<td>모리셔스</td>
</tr>
<tr>
<td>2000000005</td>
<td>북미(서비스 지역)</td>
<td>809</td>
<td>불가리아</td>
<td>1693</td>
<td>모로코</td>
</tr>
<tr>
<td>2000000006</td>
<td>유럽(서비스 지역)</td>
<td>811</td>
<td>슬로베니아</td>
<td>1695</td>
<td>알제리</td>
</tr>
<tr>
<td>2000000007</td>
<td>남미 (서비스 지역)</td>
<td>812</td>
<td>몰도바</td>
<td>1698</td>
<td>기니</td>
</tr>
<tr>
<td>2000000008</td>
<td>아프리카 (서비스 지역)</td>
<td>813</td>
<td>마케도니아</td>
<td>1730</td>
<td>세네갈</td>
</tr>
<tr>
<td>-20</td>
<td>아시아 (클라이언트 지역)</td>
<td>824</td>
<td>에스토니아</td>
<td>1864</td>
<td>튀니지</td>
</tr>
<tr>
<td>-21</td>
<td>남미 (클라이언트 지역)</td>
<td>835</td>
<td>크로아티아</td>
<td>1909</td>
<td>우루과이</td>
</tr>
<tr>
<td>-22</td>
<td>북미 (클라이언트 지역)</td>
<td>837</td>
<td>폴란드</td>
<td>1916</td>
<td>그린란드</td>
</tr>
<tr>
<td>-23</td>
<td>유럽 (클라이언트 지역)</td>
<td>852</td>
<td>라트비아</td>
<td>2026</td>
<td>대만</td>
</tr>
<tr>
<td>-24</td>
<td>아프리카 (클라이언트 지역)</td>
<td>857</td>
<td>요르단</td>
<td>2083</td>
<td>미얀마</td>
</tr>
<tr>
<td>-25</td>
<td>오세아니아 (클라이언트 지역)</td>
<td>884</td>
<td>키르기스스탄</td>
<td>2087</td>
<td>브루나이</td>
</tr>
<tr>
<td>35</td>
<td>네팔</td>
<td>896</td>
<td>아일랜드</td>
<td>2094</td>
<td>스리랑카</td>
</tr>
<tr>
<td>57</td>
<td>태국</td>
<td>901</td>
<td>리비아</td>
<td>2150</td>
<td>파나마</td>
</tr>
<tr>
<td>73</td>
<td>인도</td>
<td>904</td>
<td>아르메니아</td>
<td>2175</td>
<td>콜롬비아</td>
</tr>
<tr>
<td>144</td>
<td>베트남</td>
<td>921</td>
<td>예멘</td>
<td>2273</td>
<td>모나코</td>
</tr>
<tr>
<td>192</td>
<td>프랑스</td>
<td>926</td>
<td>벨로루시</td>
<td>2343</td>
<td>안도라</td>
</tr>
<tr>
<td>207</td>
<td>영국</td>
<td>971</td>
<td>룩셈부르크</td>
<td>2421</td>
<td>투르크 메니스탄</td>
</tr>
<tr>
<td>208</td>
<td>스웨덴</td>
<td>1036</td>
<td>뉴질랜드</td>
<td>2435</td>
<td>라오스</td>
</tr>
<tr>
<td>209</td>
<td>독일</td>
<td>1044</td>
<td>일본</td>
<td>2488</td>
<td>동 티모르</td>
</tr>
<tr>
<td>213</td>
<td>이탈리아</td>
<td>1066</td>
<td>파키스탄</td>
<td>2490</td>
<td>통가</td>
</tr>
<tr>
<td>214</td>
<td>스페인</td>
<td>1070</td>
<td>몰타</td>
<td>2588</td>
<td>필리핀</td>
</tr>
<tr>
<td>386</td>
<td>아랍에미리트</td>
<td>1091</td>
<td>바하마</td>
<td>2609</td>
<td>베네수엘라</td>
</tr>
<tr>
<td>391</td>
<td>이스라엘</td>
<td>1129</td>
<td>아르헨티나</td>
<td>2612</td>
<td>볼리비아</td>
</tr>
<tr>
<td>397</td>
<td>우크라이나</td>
<td>1134</td>
<td>방글라데시</td>
<td>2613</td>
<td>브라질</td>
</tr>
<tr>
<td>398</td>
<td>러시아</td>
<td>1158</td>
<td>캄보디아</td>
<td>2623</td>
<td>코스타리카</td>
</tr>
<tr>
<td>417</td>
<td>카자흐스탄</td>
<td>1159</td>
<td>중국 마카오</td>
<td>2626</td>
<td>멕세코</td>
</tr>
<tr>
<td>428</td>
<td>포르투갈</td>
<td>1176</td>
<td>싱가포르</td>
<td>2639</td>
<td>온두라스</td>
</tr>
<tr>
<td>443</td>
<td>그리스</td>
<td>1179</td>
<td>몰디브</td>
<td>2645</td>
<td>엘살바도르</td>
</tr>
<tr>
<td>471</td>
<td>사우디 아라비아</td>
<td>1180</td>
<td>아프가니스탄</td>
<td>2647</td>
<td>파라과이</td>
</tr>
<tr>
<td>529</td>
<td>덴마크</td>
<td>1185</td>
<td>피지</td>
<td>2661</td>
<td>페루</td>
</tr>
<tr>
<td>565</td>
<td>이란</td>
<td>1186</td>
<td>몽골</td>
<td>2728</td>
<td>니카라과</td>
</tr>
<tr>
<td>578</td>
<td>노르웨이</td>
<td>1195</td>
<td>인도네시아</td>
<td>2734</td>
<td>에콰도르</td>
</tr>
<tr>
<td>669</td>
<td>미국</td>
<td>1200</td>
<td>중국 홍콩</td>
<td>2768</td>
<td>과테말라</td>
</tr>
<tr>
<td>692</td>
<td>시리아</td>
<td>1233</td>
<td>카타르</td>
<td>2999</td>
<td>아루바</td>
</tr>
<tr>
<td>704</td>
<td>키프로스</td>
<td>1255</td>
<td>아이슬랜드</td>
<td>3058</td>
<td>에티오피아</td>
</tr>
<tr>
<td>706</td>
<td>체코</td>
<td>1289</td>
<td>알바니아</td>
<td>3144</td>
<td>보스니아 헤르체고비나</td>
</tr>
<tr>
<td>707</td>
<td>스위스</td>
<td>1353</td>
<td>우즈베키스탄</td>
<td>3216</td>
<td>도미니카</td>
</tr>
<tr>
<td>708</td>
<td>이라크</td>
<td>1407</td>
<td>산마리노</td>
<td>3379</td>
<td>한국</td>
</tr>
<tr>
<td>714</td>
<td>네덜란드</td>
<td>1416</td>
<td>쿠웨이트</td>
<td>3701</td>
<td>말레이시아</td>
</tr>
<tr>
<td>717</td>
<td>루마니아</td>
<td>1417</td>
<td>몬테네그로</td>
<td>3839</td>
<td>캐나다</td>
</tr>
<tr>
<td>721</td>
<td>레바논</td>
<td>1493</td>
<td>타지키스탄</td>
<td>4450</td>
<td>호주</td>
</tr>
<tr>
<td>725</td>
<td>헝가리</td>
<td>1501</td>
<td>바레인</td>
<td>4460</td>
<td>중국대륙</td>
</tr>
<tr>
<td>726</td>
<td>조지아</td>
<td>1543</td>
<td>칠레</td>
<td>-15</td>
<td>아시아 기타</td>
</tr>
<tr>
<td>731</td>
<td>아제르바이잔</td>
<td>1559</td>
<td>남아프리카</td>
<td>-14</td>
<td>남미 기타</td>
</tr>
<tr>
<td>734</td>
<td>오스트리아</td>
<td>1567</td>
<td>이집트</td>
<td>-13</td>
<td>북미 기타</td>
</tr>
<tr>
<td>736</td>
<td>팔레스타인</td>
<td>1590</td>
<td>케냐</td>
<td>-12</td>
<td>유럽 기타</td>
</tr>
<tr>
<td>737</td>
<td>터키</td>
<td>1592</td>
<td>나이지리아</td>
<td>-11</td>
<td>아프리카 기타</td>
</tr>
<tr>
<td>759</td>
<td>리투아니아</td>
<td>1598</td>
<td>탄자니아</td>
<td>-10</td>
<td>오세아니아 기타</td>
</tr>
<tr>
<td>763</td>
<td>오만</td>
<td>1611</td>
<td>마다가스카르</td>
<td>-2</td>
<td>해외 기타</td>
</tr>
</tbody></table>



### 해외 ISP 매핑

<table  style="width:494px">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">통신사 ID</th>
<th align="left" style="width:120px;font-weight:700">통신사</th>
</tr>
</thead>
<tbody><tr>
<td>-1</td>
<td>해외 통신사</td>
</tr>
</tbody>
<table >

### 주의사항

액세스 로그의 다섯 번째 필드에 기록된 바이트 수를 통해 통계적으로 계산된 트래픽/대역폭 데이터가 CDN 과금 트래픽/대역폭 데이터와 일치하지 않습니다. 그 이유는 다음과 같습니다.
-애플리케이션 계층 데이터만 액세스 로그에 기록될 수 있으며 실제 네트워크 전송에서는 순수 애플리케이션 계층 트래픽보다 5%-15% 더 많은 네트워크 트래픽을 발생시킵니다. 두 부분으로 구성되어 있습니다:
	- TCP/IP 헤더 소비: TCP/IP 프로토콜을 기반으로 하는 HTTP 요청 각 패킷의 최대 크기는 1500바이트이며 TCP 및 IP 프로토콜을 위한 40 바이트의 헤더를 포함합니다. 또, 응용 계층은 통계가 불가능하지만 이 부분은 약 3%인 것으로 계산됩니다.
	- TTCP 재전송: 정상적인 네트워크 전송 중에는 전송된 네트워크 패킷 3%-10%가 인터넷에서 삭제됩니다. 삭제된 후에 재전송이 진행되며 이 부분의 데이터 응용 계층도 통계가 불가능하지만 비율은 약 3%-7%입니다.
업계 표준으로 요금 트래픽은 일반적으로 응용 계층 트래픽과 위의 비용을 기반으로 하며 Tencent Cloud CDN은 10%를 차지하므로 모니터링 트래픽은 로그 계산 트래픽의 약 110%입니다.

## 사용 사례

### 국내 액세스 로그 사례

![](https://mc.qcloudimg.com/static/img/a3ef1ea051dc277872ec10a7135872df/logs.png)

### 해외 액세스 로그 사례

![](https://main.qcloudimg.com/raw/b0612a5204abdbdc6a4364ad02972900.png)
