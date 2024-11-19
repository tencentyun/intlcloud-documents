<blockquote class="d-mod-alarm">
              <div class="d-mod-title d-alarm-title">
                <i class="d-icon-alarm"></i>공지: 
              </div>
               <p>CDN 공식 범용 로그 필드 - HTTP 프로토콜 식별자(오프라인 로그의 14번째 필드)에 ‘HTTP/3’ 값을 추가할 예정으로, 2021-09-13일부터 카나리 테스트를 배포합니다. 이는 콘솔 및 인터페이스의 모니터링 통계에 영향을 미치지 않습니다. 하지만 오프라인 로그 다운로드 패키지로 데이터 분석을 진행하는 경우, 구체적인 영향을 확인하여 필요에 따라 조정하시기 바랍니다. 양해와 협조에 감사드립니다. </br></br>배경: QUIC 액세스 기능은 베타 테스트 중으로 자세한 내용은 <a href="https://cloud.tencent.com/document/product/228/51800">QUIC</a>를 참고하십시오.</p>
            </blockquote>



## 기능 소개

도메인을 Content Delivery Network(CDN)에 연결하면 모든 사용자 측의 리소스 요청이 CDN 노드에 스케쥴링됩니다. 노드에 해당 리소스가 캐시되어 있는 경우 콘텐츠를 직접 반환하며 캐시되어 있지 않으면 도메인 구성의 원본 서버에 요청을 전달하여 필요한 리소스를 풀링합니다.  

CDN 노드는 대부분의 사용자 요청에 응답하므로 사용자 액세스를 쉽게 분석하기 위해 전체 네트워크 액세스 로그를 시간 단위로 패키징합니다. 기본적으로 30일 동안 저장하며 다운로드 서비스를 제공합니다.  

>? 
>- 현재 노드 액세스 로그만 제공하며 Origin-pull 로그는 제공하지 않습니다. 
>- ECDN 도메인 오프라인 로그는 현재 지역별 조회를 지원하지 않습니다. ECDN 오프라인 로그 필드 설명은 [ECDN 제품 문서](https://intl.cloud.tencent.com/document/product/570/15258)를 참고하십시오.

## 적용 시나리오
### 액세스 분석
액세스 로그를 다운로드하여 필요에 따라 인기 리소스와 액티브 유저 등을 분석할 수 있습니다.

### 서비스 품질 모니터링
액세스 로그를 다운로드하여 전체 CDN 노드의 서비스 상태를 파악하고 평균 응답 시간 및 평균 다운로드 속도 등의 지표를 계산할 수 있습니다. 

## 운영 가이드
### 사용 방법
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여, 좌측 디렉터리의 [CLS]를 클릭합니다. 도메인, 시간을 선택하여 액세스 로그를 조회할 수 있으며 다수의 로그 패키지를 선택하고 로컬로 일괄 다운로드 할 수 있습니다. 


>!
>- 액세스 로그는 기본적으로 시간 단위로 패키징되도록 설정되어 있으며 특정 시간대 도메인에서 아무런 요청도 없을 경우 해당 시간대의 로그 패키지는 생성되지 않습니다.
>- 같은 도메인의 중국 외 액세스 로그와 중국 내 액세스 로그는 따로 패키징되며 로그 데이터 패킷의 이름 생성 형식은 ‘시간-도메인-가속 구역’입니다. 
>- 액세스 로그는 각 CDN 가속 노드에서 수집되기 때문에 딜레이 시간이 다를 수 있으며 일반적으로 로그 패키지의 조회, 다운로드 딜레이는 약 30분입니다. 로그 패키지는 계속 추가될 수 있으며 일반적으로 24시간 전후로 안정화됩니다. 
>- 도메인의 액세스 로그 기록은 30일 이내의 로그 패키지만 보관됩니다. 다음 [가이드](https://intl.cloud.tencent.com/document/product/228/36014)에 따라 SCF 함수를 이용하여 로그 패키지를 COS에 영구 저장할 수 있습니다. 

### 필드 설명
로그의 해당 필드 순서 (왼쪽에서 오른쪽으로) 및 그 의미는 다음 표와 같습니다.
<table style="width:660px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">순서</th>
<th align="left" style="width:560px;font-weight:700">로그 콘텐츠 </th>
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
<td>이번 액세스 바이트 수 크기(파일 자체 크기 및 요청 header 크기 포함)</td>
</tr>
</tbody>
<tbody><tr>
<td>6</td>
<td>중국 내 로그는 지역 번호를 나타내며, 중국 외 지역 로그는 지역 번호를 나타냅니다.(매핑 리스트는 다음과 같습니다)</td>
</tr>
</tbody>
<tbody><tr>
<td>7</td>
<td>중국 내 로그는 통신사 번호를 나타내며, 중국 외 지역 로그는 -1로 통일됩니다.(매핑 리스트는 다음과 같습니다)</td>
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
<td>응답 시간(밀리초), 노드가 요청을 받은 후부터 모든 리턴 패킷에 응답하고, 다시 클라이언트에 도달하기까지 소요된 시간</td>
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
<td>HIT/MISS 캐시, CDN 엣지 노드에 히트 혹은 부모 노드에 히트 모두 HIT로 표기</td>
</tr>
<td>16</td>
<td>클라이언트와 CDN 노드를 연결하는 포트. 없을 경우 -</td>
</tr>
</tbody></table>

### 지역 / 통신사 매핑 리스트

[](id:.E7.9C.81.E4.BB.BD.E6.98.A0.E5.B0.84)
#### 중국 내 지역 매핑
<table style="width:660px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">지역 ID</th>
<th align="left" style="width:120px;font-weight:700">지역</th>
<th align="left" style="width:100px;font-weight:700">지역 ID</th>
<th align="left" style="width:120px;font-weight:700">지역</th>
<th align="left" style="width:100px;font-weight:700">지역 ID</th>
<th align="left" style="width:120px;font-weight:700">지역</th>
</tr>
</thead>
<tbody><tr>
<td>22</td>
<td>베이징</td>
<td>86</td>
<td>네이멍구</td>
<td>146</td>
<td>산시</td>
</tr>
<tr>
<td>1069</td>
<td>허베이</td>
<td>1177</td>
<td>톈진</td>
<td>119</td>
<td>닝샤</td>
</tr>
<tr>
<td>152</td>
<td>산시</td>
<td>1208</td>
<td>간쑤</td>
<td>1467</td>
<td>칭하이</td>
</tr>
<tr>
<td>1468</td>
<td>신장</td>
<td>145</td>
<td>헤이룽장</td>
<td>1445</td>
<td>지린</td>
</tr>
<tr>
<td>1464</td>
<td>랴오닝</td>
<td>2</td>
<td>푸젠</td>
<td>120</td>
<td>장쑤</td>
</tr>
<tr>
<td>121</td>
<td>안후이</td>
<td>122</td>
<td>산동</td>
<td>1050</td>
<td>상하이</td>
</tr>
<tr>
<td>1442</td>
<td>저장</td>
<td>182</td>
<td>허난</td>
<td>1135</td>
<td>후베이</td>
</tr>
<tr>
<td>1465</td>
<td>장시</td>
<td>1466</td>
<td>후난</td>
<td>118</td>
<td>구이저우</td>
</tr>
<tr>
<td>153</td>
<td>윈난</td>
<td>1051</td>
<td>충칭</td>
<td>1068</td>
<td>쓰촨</td>
</tr>
<tr>
<td>1155</td>
<td>시짱</td>
<td>4</td>
<td>광동</td>
<td>173</td>
<td>광시</td>
</tr>
<tr>
<td>1441</td>
<td>하이난</td>
<td>0</td>
<td>기타</td>
<td>1</td>
<td>중국홍콩·마카오·타이완</td>
</tr>
<tr>
<td>-1</td>
<td>중국 외 지역</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody></table>


#### 중국 내 통신사 매핑 리스트
<table style="width:660px;">
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
<td>Cernet</td>
</tr>
</tbody>
<tbody><tr>
<td>43</td>
<td>Great Wall Broadband</td>
<td>1046</td>
<td>China Mobile</td>
<td>3947</td>
<td>China Railcom</td>
</tr>
</tbody>
<tbody><tr>
<td>-1</td>
<td>중국 외 지역 통신사</td>
<td>0</td>
<td>기타 통신사</td>
<td></td>
<td></td>
</tr>
</tbody>
</table>


### 중국 외 지역 매핑
<table style="width:710px">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">지역 ID</th>
<th align="left" style="width:170px;font-weight:700">지역</th>
<th align="left" style="width:100px;font-weight:700">지역 ID</th>
<th align="left" style="width:120px;font-weight:700">지역</th>
<th align="left" style="width:100px;font-weight:700">지역 ID</th>
<th align="left" style="width:120px;font-weight:700">지역</th>
</tr>
</thead>
<tbody><tr>
<td>2000000001</td>
<td>아태1존(서비스 지역)</td>
<td>765</td>
<td>슬로바키아</td>
<td>1613</td>
<td>앙골라</td>
</tr>
<tr>
<td>2000000002</td>
<td>아태2존(서비스 지역)</td>
<td>766</td>
<td>세르비아</td>
<td>1617</td>
<td>코트디부아르</td>
</tr>
<tr>
<td>2000000003</td>
<td>아태3존(서비스 지역)</td>
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
<td>남미(서비스 지역)</td>
<td>812</td>
<td>몰도바</td>
<td>1698</td>
<td>기니</td>
</tr>
<tr>
<td>2000000008</td>
<td>아프리카(서비스 지역)</td>
<td>813</td>
<td>마케도니아</td>
<td>1730</td>
<td>세네갈</td>
</tr>
<tr>
<td>-20</td>
<td>아시아(클라이언트 지역)</td>
<td>824</td>
<td>에스토니아</td>
<td>1864</td>
<td>튀니지</td>
</tr>
<tr>
<td>-21</td>
<td>남아메리카(클라이언트 지역)</td>
<td>835</td>
<td>크로아티아</td>
<td>1909</td>
<td>우루과이</td>
</tr>
<tr>
<td>-22</td>
<td>북아메리카(클라이언트 지역)</td>
<td>837</td>
<td>폴란드</td>
<td>1916</td>
<td>그린란드</td>
</tr>
<tr>
<td>-23</td>
<td>유럽(클라이언트 지역)</td>
<td>852</td>
<td>라트비아</td>
<td>2026</td>
<td>중국타이완</td>
</tr>
<tr>
<td>-24</td>
<td>아프리카(클라이언트 지역)</td>
<td>857</td>
<td>요르단</td>
<td>2083</td>
<td>미얀마</td>
</tr>
<tr>
<td>-25</td>
<td>오세아니아(클라이언트 지역)</td>
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
<td>벨라루스</td>
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
<td>-</td>
<td>-</td>
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
<td>도미니카공화국</td>
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
<td>오스트레일리아</td>
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
<td>아시아 기타</td>
</tr>
<tr>
<td>731</td>
<td>아제르바이잔</td>
<td>1559</td>
<td>남아프리카공화국</td>
<td>-14</td>
<td>남아메리카 기타</td>
</tr>
<tr>
<td>734</td>
<td>오스트리아</td>
<td>1567</td>
<td>이집트</td>
<td>-13</td>
<td>북아메리카 기타</td>
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
<td>중국 외 기타 지역</td>
</tr>
</tbody></table>


#### 중국 외 지역 통신사 매핑
<table style="width:220px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">통신사 ID</th>
<th align="left" style="width:120px;font-weight:700">통신사</th>
</tr>
</thead>
<tbody><tr>
<td>-1</td>
<td>중국 외 지역 통신사</td>
</tr>
</tbody>
</table>

### 주의 사항
액세스 로그 다섯 번째 필드에 기록된 바이트 수를 보면 통계 계산된 트래픽 / 대역폭 데이터 및 CDN의 과금 트래픽 / 대역폭 데이터가 불일치합니다. 그 이유는 다음과 같습니다.
- 액세스 로그에는 응용 레이어 데이터만 기록되는데 실제 네트워크 전송에서 생성된 네트워크 트래픽은 응용 레이어 트래픽보다 5% - 15% 많습니다. 이는 두 부분으로 구성됩니다.  
	- TCP/IP 헤더 소모: TCP/IP 프로토콜을 기반으로 하는 HTTP 요청으로 각 패킷의 최대 크기는 1500바이트이며 TCP 및 IP 프로토콜을 위한 40 바이트의 헤더를 포함합니다. 이 헤더 부분은 트래픽을 생성하지만 응용 레이어에서는 집계되지 않습니다. 이 부분은 약 3%입니다.
	- TCP 재전송으로 정상적인 네트워크 전송 과정에서 전송된 패킷의 3%-10%가 인터넷에서 유실됩니다. 서버는 유실된 패킷을 재전송하며 해당 트래픽 역시 응용 레이어에서 통계가 되지 않습니다. 이 부분의 비율은 약 3%-7% 정도입니다.
- 업계 표준으로 과금되는 트래픽은 일반적으로 응용 레이어 트래픽과 상기 소모량을 기반으로 한 트래픽입니다. Tencent Cloud CDN은 이 부분을 10%로 계산하기 때문에 모니터링 트래픽은 로그 계산 트래픽의 약 110%입니다.

## 사용 사례

### 중국 내 액세스 로그 예시
![](https://mc.qcloudimg.com/static/img/a3ef1ea051dc277872ec10a7135872df/logs.png)

### 중국 외 지역 액세스 로그 예시
![](https://main.qcloudimg.com/raw/b0612a5204abdbdc6a4364ad02972900.png)

