<table>
    <tr>
        <th>범주</th>
        <th>사양 및 제한</th>
    			<th>상세 설명</th>
   </tr>
    <tr>
        <td>QPS</td>
    			<td>제한</td>
    			<td>기본적으로 계정 당 1200QPS입니다. 더 높은 QPS가 필요하면 <a href="/document/product/436/13653">요청 속도 및 성능 최적화</a>를 참조하십시오. </td>
    </tr>
    	 <tr>
        <td rowspan="3">스토리지 클래스</td>
    			<td>표준 스토리지 제한</td>
    			<td>요금 제안:<br> 저장 시간 및 저장 크기에는 제한이 없습니다.<br>표준 스토리지 비용 청구에 대한 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/6239">요금 설명</a>을 참조하십시오.</td>
    </tr>
    	 <tr>
        <td>저빈도 스토리지 제한</td>
    			<td>요금 제한:<br> 저장 시간이 30일 미만인 경우 30일로 계산됩니다.<br>64KB 미만의 저장소 크기는 64KB로 계산됩니다.<br>저빈도 스토리지 요금에 대한 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/6239">요금 설명</a>을 참조하십시오.</td>
    </tr>
    	 <tr>
        <td>보관 스토리지 제한</td>
    			<td>요금 제한:<br> 90일 미만의 저장 시간은 90일로 계산됩니다.<br>48KB 미만의 저장소 크기는 48KB로 계산됩니다.<br>보관 스토리지 요금에 대한 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/6239">요금 설명</a>을 참조하십시오.</td>				
    </tr>
     <tr>
        <td rowspan="3">버킷</td>
    			<td>제한</td>
    			<td>1. 버켓이 성공적으로 작성되면 이름과 위치를 수정할 수 없습니다.<br>2. 동일한 사용자 계정 아래의 모든 버킷 이름은 고유하며 이름 변경을 지원하지 않습니다.<br>3. 이름은 소문자 및 숫자 [a-z, 0-9], 밑줄 "-" 및 그 조합만 지원하며 1-40자를 지원합니다.</td>
     </tr>
    	 <tr>
    			<td> 버킷 수량</td>
    			<td>계정마다 최대 200개의 버킷(기본값)이 가능합니다.</td>
    		</tr>
    			<td> 객체 수량</td>
    			<td> 버킷마다 객체 수량은 제한되지 않습니다.</td>
    		<tr>
    			<td rowspan="4">객체</td>
    			<td>제한</td>
					<td >객체 키 길이는 1-850B를 지원합니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/13324">객체 소개</a>를 참조하십시오.</td>
    		</tr>
    			<tr>
    			<td>업로드</td>
    			<td>1. 콘솔에서 최대 512GB의 단일 객체를 업로드합니다.<br>2. API/SDK는 최대 48.82TB(50,000 GB)까지 단일 객체를 업로드합니다.<br>업로드 API 사양:<br>&nbsp;&nbsp;a) 간편 업로드: 단일 객체의 경우 최대 5GB, 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/14113">간편 업로드</a>를 참조하십시오. <br>&nbsp;&nbsp;b) 멀티파트 업로드: 단일 객체의 최대 크기는 48.82TB, 파트 크기는 1MB~5GB, 마지막 파트는 1MB 미만일 수 있으며, 파트 수는 1~10000입니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/14112">멀티파트 업로도</a>를 참조하십시오.</td>
    		</tr>
    		<tr>
    			<td >복사</td>
    			<td >1. 동일한 지역/지역 간 객체 복사를 지원합니다. <br>2. 같은 지역 객체의 복사는 무료이며, 지역간 객체 복사는 트래픽 요금이 발생합니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/6239">요금제 설명</a>을 참조하십시오.<br>3. API 사양 복사:<br>&nbsp;&nbsp;a) 간편 복사: 단일 복사 객체는 최대 5GB이며 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/14117">간편 복사</a>를 참조하십시오.<br>&nbsp;&nbsp;b) 5GB 이상인 경우 멀티파트로 복사해야 하며, 단일 객체는 최대 48.82TB입니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/14118">멀티파트 복사</a>를 참조하십시오.</td>
    		</tr>
    		<tr>
    			<td>일괄 삭제</td>
    			<td>API/SDK를 통해 일괄적으로 삭제하며, 1회에 최대 1000개의 객체를 삭제할 수 있습니다.</td>
    		</tr>
    		 <tr>
    			<td >액세스 정책</td>
    			<td >규칙 수</td>
    			<td >객체와 버킷 ACL 수 + 버킷 정책 수의 합은 계정마다 1000개로 제한됩니다.</td>
    		</tr>
    		<tr>
    			<td rowspan="3">수명 주기</td>
    			<td>규칙 수</td>
    			<td >버킷 당 최대 1000개</td>
    		</tr>
    		<tr>
    			<td >스토리지 클래스 전환</td>
    			<td >표준 스토리지를 저빈도 스토리지로: 최소 1일<br>표준/저빈도 스토리지를 보관 스토리지로: 최소 1일 </td>
    		</tr>
    		 <tr>
    			<td >만료된 객체 삭제</td>
    			<td >표준/저빈도/보관 스토리지 만료된 객체 삭제: 최소 1일</td>
    		</tr>         
    		<tr>
    			<td colspan="2">SDK 언어</td>
    			<td >10개:<br>Andriod/C/C++/Go/iOS/Java/JavaScript/Node.js/PHP/Python</td>
    </tr>
</table>
