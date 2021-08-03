<table>
    <tr>
        <th>분류</th> 
        <th>규격 및 제한</th> 
    			<th>상세 설명</th> 
   </tr>
    <tr>
        <td>QPS</td>
    			<td>제한</td>
    			<td>1. 읽기/쓰기 유형 요청: 중국대륙 공유 클라우드 리전에서는 기본적으로 버킷 하나당 30000QPS를, 기타 리전에서는 버킷 하나당 3000QPS를 독점합니다.
<br>2. List 유형 요청: 모든 리전의 기본값은 1200QPS입니다.
<br>3. 데이터 검색 요청: 모든 리전의 기본값은 100QPS입니다.
<br>더 높은 QPS가 필요한 경우, <a href="/document/product/436/13653"> 요청 속도 및 성능 최적화</a>를 참고하십시오.</td>
    </tr>
		    <tr>
        <td>대역폭</td>
    			<td>제한</td>
					<td>중국 대륙 공유 클라우드 리전의 기본 대역폭은 15Gbit/s이며, 기타 리전은 10Gbit/s입니다. 대역폭이 임계값에 이른 경우 요청에 의해 트래픽 제어가 트리거됩니다. 더 넓은 대역폭이 필요한 경우<a href="https://console.cloud.tencent.com/workorder/category">Tencent Cloud A/S 엔지니어</a>에게 문의하십시오.</td>	
    </tr>
    	 <tr>
        <td rowspan="5">스토리지 유형</td>
    			<td>표준 스토리지 제한</td>
    			<td>과금 유의 사항: <br>저장 기간, 저장 단위 무제한 <br>표준 스토리지에 대한 자세한 가격은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</td>
    </tr>
    	 <tr>
        <td>표준IA 스토리지 제한</td>
    			<td>과금 유의 사항: <br><li>저장 기간이 30일 미만인 경우 30일로 계산 <br><li>저장 단위가 64KB 미만인 경우 64KB로 계산하며, 64KB 이상인 경우 실제 크기로 계산<br>표준IA 스토리지에 대한 자세한 가격은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</td>
    </tr>
    	 <tr>
        <td>INTELLIGENT TIERING 스토리지 제한</td>
    			<td>과금 유의 사항: <br><li>저장 기간이 30일 미만인 경우 30일로 계산<br><li>저장 단위가 64KB 미만인 경우 64KB로 계산하며, 64KB 이상인 경우 실제 크기로 계산 <br>INTELLIGENT TIERING 스토리지에 대한 자세한 가격은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</td>
    </tr>
    	 <tr>
        <td>CAS 제한</td>
    			<td>과금 유의 사항: <br><li>저장 기간이 90일 미만인 경우 90일로 계산 <br><li>저장 단위가 64KB 미만인 경우 64KB로 계산하며, 64KB 이상인 경우 실제 크기로 계산 <br>CAS에 대한 자세한 가격은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</td>
    </tr>
    	 <tr>
        <td>DEEP ARCHIVE 제한</td>
    			<td>과금 유의 사항: <br><li>저장 기간이 180일 미만인 경우 180일로 계산 <br><li>저장 단위가 64KB 미만인 경우 64KB로 계산하며, 64KB 이상인 경우 실제 크기로 계산 <br>DEEP ARCHIVE에 대한 자세한 가격은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</td>
    </tr>
     <tr>
        <td rowspan="4">버킷</td>
    			<td>제한</td>
    			<td>1. 버킷은 한 번 생성되면 이름과 소속 리전을 변경할 수 없습니다. <br>2. 동일한 사용자 계정의 모든 버킷 이름은 고유하며 이름을 변경할 수 없습니다. <br>3. 이름은 '-'으로 시작하거나 끝날 수 없으며 영어 소문자와 숫자 [a~z, 0~9], 하이픈 '-' 및 해당 조합으로만 구성할 수 있고, 1~50자까지 지원합니다.</td>
     </tr>
    	 <tr>
    			<td> 버킷 수량</td>
    			<td>루트 계정당 최대 200개(기본)</td>
    		</tr>
				<tr>
    			<td> 객체 수량</td>
    			<td> 버킷당 객체 수량 무제한</td>
    		</tr>
				<tr>
    			<td> 버킷 태그</td>
    			<td>버킷당 최대 50개까지 태그를 설정할 수 있으며, 태그 키는 중복 사용할 수 없습니다.</td>
    		</tr>
    		<tr>
    			<td rowspan="5">객체</td>
    			<td>제한</td>
					<td >객체 키 길이는 1 - 850B까지 지원하며, 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/13324">객체 개요</a>를 참고하십시오.</td>
    		</tr>
    			<tr>
    			<td>업로드</td>
    			<td>1. 콘솔 업로드 객체당 최대 512GB까지 지원합니다. <br>2. API/SDK 업로드 객체당 최대 48.82TB(50,000GB)까지 지원합니다. <br>업로드 인터페이스 규격: <br>&nbsp;&nbsp;(a) 간편 업로드: 객체당 최대 5GB까지 지원합니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/14113">간편 업로드</a>를 참고하십시오. <br>&nbsp;&nbsp;(b) 멀티파트 업로드: 객체당 최대 48.82TB, 파트 크기 1MB - 5GB, 마지막 파트 크기 1MB 이하, 파트 수 1 - 10,000입니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/14112">멀티파트 업로드</a>를 참고하십시오. <br>3. 현재 버킷에서 INTELLIGENT TIERING 스토리지 설정을 활성화한 상태에서만 INTELLIGENT TIERING 스토리지 유형의 객체를 업로드할 수 있습니다. 서로 다른 스토리지 레이어 간의 객체 전환은 INTELLIGENT TIERING 스토리지 설정의 매개변수에 따라 결정됩니다. </td>
    		</tr>
    		<tr>
    			<td >복사</td>
    			<td >1. 리전 내 또는 리전 간 단일 계정의 객체 복사를 지원합니다. <br>2. 리전 내 객체 복사는 무료이며, 리전 간 객체 복사는 트래픽 요금이 발생합니다. 자세한 내용은 <a href="https://buy.cloud.tencent.com/price/cos">과금 설명</a>의 트래픽 요금 정보를 참고하십시오. <br>3. 복사 인터페이스 규격: <br>&nbsp;&nbsp;(a) 간편 복사: 객체당 최대 5GB까지 지원합니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/14117">간편 복사</a>를 참고하십시오. <br>&nbsp;&nbsp;(b) 5GB를 초과하는 경우 반드시 멀티파트 복사를 사용해야 하며, 복사 객체당 최대 48.82TB까지 지원합니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/436/14118">멀티파트 복사</a>를 참고하십시오. <br>4. 현재 표준 스토리지, 표준IA 스토리지, INTELLIGENT TIERING 스토리지 유형은 INTELLIGENT TIERING 스토리지 유형으로 복사할 수 없습니다. </td>
    		</tr>
    		<tr>
    			<td>일괄 삭제</td>
    			<td>API, SDK를 통한 일괄 삭제는 1회당 최대 1,000개의 객체를 삭제할 수 있습니다.</td>
    		</tr>
				<tr>
    			<td>객체 태그</td>
    			<td>동일한 객체에 최대 10개의 태그를 추가할 수 있으며, 태그는 중복될 수 없습니다.</td>
    		</tr>
    		 <tr>
    			<td >액세스 정책</td>
    			<td >규칙 수량</td>
    			<td >루트 계정당(즉, 동일한 APPID) 버킷 ACL 규칙은 최대 1,000개까지 설정할 수 있습니다.</td>
    		</tr>
    		<tr>
    			<td rowspan="3">라이프사이클</td>
    			<td>규칙 수량</td>
    			<td >버킷당 최대 1000개까지 설정할 수 있습니다.</td>
    		</tr>
    		<tr>
    			<td >스토리지 유형 전환</td>
    			<td >표준에서 표준IA로 전환: 최소 1일 <br>표준/표준IA에서 CAS 또는 DEEP ARCHIVE로 전환: 최소 1일</td>
    		</tr>
    		 <tr>
    			<td >만료 삭제</td>
    			<td >표준/표준IA/CAS 만료 삭제: 최소 1일</td>
    		</tr>         
    		<tr>
    			<td colspan="2">SDK 종류</td>
    			<td >12가지: Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, 미니프로그램 SDK</td>
    </tr>
</table>
