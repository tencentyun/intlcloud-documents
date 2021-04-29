## 기능 소개
도메인이 CDN에 액세스한 후 모든 사용자 측의 리소스 요청이 CDN 노드로 스케쥴링하고 응답합니다. 노드에 리소스가 캐시되어 있으면 노드는 리소스 콘텐츠를 직접 반환합니다. 노드에 리소스가 캐시되어 있지 않으면 요청을 원본 서버에 전달하여 필요한 리소스를 취득합니다.

CDN 노드는 대부분의 사용자 요청에 응답하기 때문에 사용자 접근을 쉽게 분석하기 위해 CDN 서비스는 전체 네트워크의 액세스 로그를 시간 단위로 패키지화합니다. 액세스 로그는 기본적으로 30일간 보관되며 다운로드 서비스도 제공합니다.

? 현재 노드 액세스 로그만 제공합니다. Origin-pull 로그를 제공하지 않습니다.

## 적용 시나리오
### 액세스 행동 분석
사용자는 액세스 로그를 다운로드함으로써 필요에 따라 인기있는 리소스와 액티브 사용자를 분석할 수 있습니다.

### 서비스 품질 모니터링
액세스 로그를 다운로드함으로써 모든 CDN 노드의 서비스 상태를 파악하고 평균 응답 시간이나 평균 다운로드 속도 같은 지표를 계산할 수 있습니다.

## 운영 가이드
### 사용 방법
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하고, 왼쪽 메뉴에서【로그 서비스】를 클릭해 도메인과 시간범위를 선택하여 액세스 로그를 조회할 수 있습니다. 여러 로그 패키지를 선택하여 로컬로 일괄 다운로드 할 수 있습니다.
![](https://mc.qcloudimg.com/static/img/043e70b6829ce67d6af125b51736b249/1.png)

>!
- 액세스 로그는 기본적으로 시간 단위로 패키지화되어 있습니다. 어떤 시간에 도메인에 대한 요청가 없을 경우 이 시간 범위에서는 로그 패키지가 생성되지 않습니다.
- 동일 도메인의 중국 외 액세스 로그와 중국 내 액세스 로그는 따로 패키지화되어 있습니다. 로그 데이터 패키지의 이름 생성 규칙은 "시간-도메인-가속 리전"입니다.
- 액세스 로그는 각 CDN 가속 노드로부터 수집되기 때문에 지연 시간은 각자 다를 수 있습니다. 로그 패키지의 조회 및 다운로드는 보통 약 30분의 지연 시간이 있습니다. 로그 패키지는 지속적으로 추가되며 보통 2~3시간 후 안정됩니다.
- 도메인 액세스 로그 패키지는 30일간 보관됩니다. 다음의 [가이드](https://intl.cloud.tencent.com/document/product/228/36014)에 따라 SCF 함수를 사용해서 로그 패키지를 Cloud Object Storage(COS)에 전송하여 영구히 저장할 수 있습니다.

## 필드에 대한 설명
로그의 해당 필드 순서 (왼쪽에서 오른쪽으로) 및 그 의미는 다음 표에 표시되어 있습니다.
<table style="width:660px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">순서</th>
<th align="left" style="width:560px;font-weight:700">로그 내용  </th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>요청 시간</td>
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
<td>이번 액세스된 바이트 수량의 크기에는 파일 자체의 크기와 요청 헤더의 크기가 포함됩니다</td>
</tr>
</tbody>
<tbody><tr>
<td>6</td>
<td> 중국 내 로그는 성 번호를 표시하고 중국 외 로그는 지역의 번호를 표시합니다.(아래의 매핑 테이블을 참조하세요)</td>
</tr>
</tbody>
<tbody><tr>
<td>7</td>
<td> 중국 내 로그는 통신사 번호를 표시하고 중국 외 로그는 -1로 통일 표시되어 있습니다.(아래의 매핑 테이블을 참조하세요)</td>
</tr>
</tbody>
<tbody><tr>
<td>8</td>
<td>HTTP 상태 코드</td>
</tr>
</tbody>
<tbody><tr>
<td>9</td>
<td>referer</td>
</tr>
</tbody>
<tbody><tr>
<td>10</td>
<td> 응답 시간(밀리초), 노드가 요청을 받은 후 모든 패키지에 응답하여 클라이언트로 갈 때까지 걸리는 시간을 말합니다</td>
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
<td>Range 매개변수</td>
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
<td>HTTP 프로토콜 식별자</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>15</td>
<td> 캐시 HIT/MISS가 CDN 엣지 노드에서의 히트와 부모 노드에서의 히트는 HIT로 표기됩니다</td>
</tr>
</tbody></table>

## 리전 / 통신사 매핑 테이블

#### 중국 내 성 매핑
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
<td>내몽골</td>
<td>146</td>
<td>산시성</td>
</tr>
<tr>
<td>1069</td>
<td>허베이성</td>
<td>1177</td>
<td>톈진성</td>
<td>119</td>
<td>닝샤성</td>
</tr>
<tr>
<td>152</td>
<td>샨시성</td>
<td>1208</td>
<td>간쑤성</td>
<td>1467</td>
<td>칭하이성</td>
</tr>
<tr>
<td>1468</td>
<td>신장성</td>
<td>145</td>
<td>헤이룽장성</td>
<td>1445</td>
<td>지린성</td>
</tr>
<tr>
<td>1464</td>
<td>랴오닝성</td>
<td>2</td>
<td>푸젠성</td>
<td>120</td>
<td>지앙쑤성</td>
</tr>
<tr>
<td>121</td>
<td>안후이성</td>
<td>122</td>
<td>산둥성</td>
<td>1050</td>
<td>상하이</td>
</tr>
<tr>
<td>1442</td>
<td>저장성</td>
<td>182</td>
<td>허난성</td>
<td>1135</td>
<td>후베이성</td>
</tr>
<tr>
<td>1465</td>
<td>장시성</td>
<td>1466</td>
<td>후난성</td>
<td>118</td>
<td >구이저우성</td>
</tr>
<tr>
<td>153</td>
<td>윈난성</td>
<td>1051</td>
<td>충칭시</td>
<td>1068</td>
<td>쓰촨성</td>
</tr>
<tr>
<td>1155</td>
<td>티베트</td>
<td>4</td>
<td >광동성</td>
<td>173</td>
<td >구왕시성</td>
</tr>
<tr>
<td>1441</td>
<td>하이난성</td>
<td> 91</td>
<td>기타</td>
<td>1</td>
<td>홍콩·마카오·타이완</td>
</tr>
<tr>
<td>-1</td>
<td>중국 외</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody></table>


#### 중국 내 통신사 매핑
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
<td>교육 사이트</td>
</tr>
</tbody>
<tbody><tr>
<td>43</td>
<td>great wall broadband</td>
<td>1046</td>
<td>China Mobile</td>
<td>3947</td>
<td>China Tietong</td>
</tr>
</tbody>
<tbody><tr>
<td>-1</td>
<td>중국 외 통신사</td>
<td> 91</td>
<td>기타 통신사</td>
<td></td>
<td></td>
</tr>
</tbody>
</table>


#### 해외 지역 매핑
<table style="width:710px">
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
<td>아시아 태평양 존 1(서비스 리전)</td>
<td>765</td>
<td>슬로바키아</td>
<td>1613</td>
<td>앙골라</td>
</tr>
<tr>
<td>2000000002</td>
<td>아시아 태평양 존 2(서비스 리전)</td>
<td>766</td>
<td>세르비아</td>
<td>1617</td>
<td>코트디부아르</td>
</tr>
<tr>
<td>2000000003</td>
<td>아시아 태평양 존 3(서비스 리전)</td>
<td>770</td>
<td>핀란드</td>
<td>1620</td>
<td>술탄</td>
</tr>
<tr>
<td>2000000004</td>
<td>중동(서비스 리전)</td>
<td>773</td>
<td>벨기에</td>
<td>1681</td>
<td>모리셔스</td>
</tr>
<tr>
<td>2000000005</td>
<td>북미(서비스 리전)</td>
<td>809</td>
<td>불가리아</td>
<td>1693</td>
<td>모로코</td>
</tr>
<tr>
<td>2000000006</td>
<td>유럽(서비스 리전)</td>
<td>811</td>
<td>슬로베니아</td>
<td>1695</td>
<td>알제리</td>
</tr>
<tr>
<td>2000000007</td>
<td>남미(서비스 리전)</td>
<td>812</td>
<td>몰도바</td>
<td>1698</td>
<td>기니</td>
</tr>
<tr>
<td>2000000008</td>
<td>아프리카(서비스 리전)</td>
<td>813</td>
<td>마케도니아</td>
<td>1730</td>
<td>세네갈</td>
</tr>
<tr>
<td>-20</td>
<td>아시아(클라이언트 리전)</td>
<td>824</td>
<td>에스토니아</td>
<td>1864</td>
<td>튀니지</td>
</tr>
<tr>
<td>-21</td>
<td>남아메리카(클라이언트 리전)</td>
<td>835</td>
<td>크로아티아</td>
<td>1909</td>
<td>우루과이</td>
</tr>
<tr>
<td>-22</td>
<td>북아메리카(클라이언트 리전)</td>
<td>837</td>
<td>폴란드</td>
<td>1916</td>
<td>그린란드</td>
</tr>
<tr>
<td>-23</td>
<td>유럽(클라이언트 리전)</td>
<td>852</td>
<td>라트비아</td>
<td>2026</td>
<td>중국대만</td>
</tr>
<tr>
<td>-24</td>
<td>아프리카(클라이언트 리전)</td>
<td>857</td>
<td>요르단</td>
<td>2083</td>
<td>미얀마</td>
</tr>
<tr>
<td>-25</td>
<td>오세아니아(클라이언트 리전)</td>
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
<td>투르크메니스탄</td>
</tr>
<tr>
<td>208</td>
<td>스웨덴</td>
<td>1036</td>
<td>싱가포르</td>
<td>2435</td>
<td>라오스</td>
</tr>
<tr>
<td>209</td>
<td>독일</td>
<td>1044</td>
<td>일본</td>
<td>2488</td>
<td>동티모르</td>
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
<td>아랍 에미리트</td>
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
<td>중국마카오</td>
<td>2626</td>
<td>멕시코</td>
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
<td>사우디아라비아</td>
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
<td>중국홍콩</td>
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
<td>아이슬란드</td>
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
<td>그루지야</td>
<td>1543</td>
<td>칠레</td>
<td>-15</td>
<td>아시아의 다른 나라</td>
</tr>
<tr>
<td>731</td>
<td>아제르바이잔</td>
<td>1559</td>
<td>남아프리카공화국</td>
<td>-14</td>
<td>남아메리카의 다른 나라</td>
</tr>
<tr>
<td>734</td>
<td>오스트리아</td>
<td>1567</td>
<td>이집트</td>
<td>-13</td>
<td>북아메리카의 다른 나라</td>
</tr>
<tr>
<td>736</td>
<td>팔레스타인</td>
<td>1590</td>
<td>케냐</td>
<td>-12</td>
<td>유럽의 다른 나라</td>
</tr>
<tr>
<td>737</td>
<td>터키</td>
<td>1592</td>
<td>나이지리아</td>
<td>-11</td>
<td>아프리카의 다른 나라</td>
</tr>
<tr>
<td>759</td>
<td>리투아니아</td>
<td>1598</td>
<td>탄자니아</td>
<td>-10</td>
<td>오세아니아의 다른 나라</td>
</tr>
<tr>
<td>763</td>
<td>오만</td>
<td>1611</td>
<td>마다가스카르</td>
<td>-2</td>
<td>중국 외의 다른 나라</td>
</tr>
</tbody></table>


#### 중국 외의 통신사 매핑
<table style="width:220px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">통신사 ID</th>
<th align="left" style="width:120px;font-weight:700">통신사</th>
</tr>
</thead>
<tbody><tr>
<td>-1</td>
<td>중국 외의 통신사</td>
</tr>
</tbody>
</table>

### 주의사항
액세스 로그의 5번째 필드에 기록된 바이트 수량을 기준으로 계산된 트래픽/대역폭 데이터는 CDN의 과금 트래픽/대역폭 데이터와 일치하지 않습니다. 이유는 다음과 같습니다.
액세스 로그에는 애플리케이션 층의 데이터만 기록되어 있습니다. 실제의 네트워크 전송에서 생성되는 네트워크 트래픽은 애플리케이션 층의 트래픽보다 5%~15% 많습니다. 이러므로 트래픽은 두 부분으로 구성됩니다.
	- TCP/IP 헤더 소비: TCP/IP 프로토콜을 기반으로 하는 HTTP 요청, 각 패키지의 최대 크기는 1500바이트이며 TCP 및 IP 프로토콜의 40 바이트 헤더를 포함합니다. 헤더는 트래픽을 생기지만 애플리케이션 층에서 통계가 불가능하고 이 부분은 약 3%인 것으로 계산됩니다.
	- TTCP 재전송: 정상적인 네트워크 전송 중에는 전송된 네트워크 패키지 3%-10%가 인터넷에서 삭제됩니다. 삭제된 후에 재전송이 진행되며 이 부분의 트래픽은 애플리케이션 층에서 통계가 불가능하고 비율은 약 3%-7%입니다.
- 업계 표준으로 요금 트래픽은 일반적으로 애플리케이션 층 트래픽과 기타 트래픽의 합계입니다. Tencent Cloud CDN에서는 10%로 계산하므로 모니터링 트래픽은 로그 계산 트래픽의 약 110%입니다.

## 사용 사례

### 중국 내 액세스 로그 예시
![](https://mc.qcloudimg.com/static/img/a3ef1ea051dc277872ec10a7135872df/logs.png)

### 중국 외 액세스 로그 예시
![](https://main.qcloudimg.com/raw/b0612a5204abdbdc6a4364ad02972900.png)
