본문에서는 COS의 사용량 기반 요금제를 소개합니다. COS의 요금제, 청구 항목 등의 정보는 [COS 요금제](https://cloud.tencent.com/document/product/436/16871)를 참조하십시오.

또한, 다음과 같이 실제 사례에 근거하여 COS 요금제를 알아볼 수 있습니다. 자세한 내용은 [청구 인스턴스](https://cloud.tencent.com/document/product/436/6241)를 참조하십시오.

## 사용량 기반 요금제의 가격

사용량 기반 요금제의 경우, 사용자가 스스로 사용량을 추산하고 **[COS 가격 계산기](https://buy.cloud.tencent.com/price/cos/calculator)**로 구체적인 구매 가격을 계산할 수 있습니다.

### 사용량 기반 요금제의 가격

<table>
   <tr>
      <th rowspan="3" width="75px">사용 지역</th>
      <th rowspan="3">스토리지 클래스</th>
	<th colspan="6"><center>청구 항목</center></th>
   </tr>
   <tr>
      <th rowspan="2">스토리지 용량 비용(USD/GB/월)</th>
      <th rowspan="2" width="150px">읽기/쓰기 요청 비용<br>(USD/만회)</th>
      ·<th rowspan="2">데이터 검색 비용(USD/GB)</th>
      <th colspan="3">트래픽 비용(USD/GB)</th>
   </tr>
   <tr>
      <th>공중망 다운스트림 트래픽</th>
      <th>CDN 오리진 요청 트래픽</th>
      <th>교차 영역 복제의 트래픽</th>
   </tr>
   <tr>
      <td rowspan="3">청두, 충칭</td>
      <td>표준 스토리지</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.05</td>
   </tr>
   <tr>
      <td>저빈도 스토리지</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>보관 스토리지</td>
      <td>0.0045</td>
      <td>0.0147(복구한 후 요청할 수 있음)</td>
      <td width="150px">빠른 되찾기: 0.03<br>표준 되찾기: 0.01<br>배치 되찾기: 0.0025</td>
      <td>0.1(복구한 후 적용할 수 있음)</td>
      <td>해당되지 않음</td>
      <td>해당되지 않음</td>
   </tr>
   <tr>
      <td rowspan="3">중국 대륙 다른 도시</td>
      <td>표준 스토리지</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.05</td>
   </tr>
   <tr>
      <td>저빈도 스토리지</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>보관 스토리지</td>
      <td>0.005</td>
      <td>0.0147(복구한 후 요청할 수 있음)</td>
      <td width="150px">빠른 되찾기: 0.03<br>표준 되찾기: 0.01<br>배치 되찾기: 0.0025</td>
      <td>0.1(복구한 후 적용할 수 있음)</td>
      <td>해당되지 않음</td>
      <td>해당되지 않음</td>
   </tr>
   <tr>
      <td rowspan="2">홍콩</td>
      <td>표준 스토리지</td>
      <td>0.022</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
   </tr>
   <tr>
      <td>저빈도 스토리지</td>
      <td>0.016</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="3">싱가포르</td>
      <td>표준 스토리지</td>
      <td>0.022</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
   </tr>
   <tr>
      <td>저빈도 스토리지</td>
      <td>0.016</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
	 	    <tr>
      <td>보관 스토리지</td>
      <td>0.005</td>
      <td>0.0147(복구한 후 요청할 수 있음)</td>
      <td width="150px">빠른 되찾기: 0.036<br>표준 되찾기: 0.012<br>배치 되찾기: 0.003</td>
      <td>0.072(복구한 후 적용할 수 있음)</td>
      <td>해당되지 않음</td>
      <td>해당되지 않음</td>
   </tr>
   <tr>
      <td rowspan="2">프랑크푸르트</td>
      <td>표준 스토리지</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>저빈도 스토리지</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">토론토</td>
      <td>표준 스토리지</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>저빈도 스토리지</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">몸바이</td>
      <td>표준 스토리지</td>
      <td>0.024</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
   </tr>
   <tr>
      <td>저빈도 스토리지</td>
      <td>0.018</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td rowspan="2">서울</td>
      <td>표준 스토리지</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
   </tr>
   <tr>
      <td>저빈도 스토리지</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">실리콘 밸리</td>
      <td>표준 스토리지</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>저빈도 스토리지</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">버지니아</td>
      <td>표준 스토리지</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>저빈도 스토리지</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">방콕</td>
      <td>표준 스토리지</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
   </tr>
   <tr>
      <td>저빈도 스토리지</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td rowspan="2">모스크바</td>
      <td>표준 스토리지</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>저빈도 스토리지</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">도쿄</td>
      <td>표준 스토리지</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>저빈도 스토리지</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
</table>


