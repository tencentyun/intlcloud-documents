<table>
    <tr>
        <th>분류</th> 
        <th>규격 및 제한</th> 
    			<th>상세 설명</th> 
   </tr>
    <tr>
        <td>QPS</td>
    			<td>제한</td>
    			<td><ul  style="margin: 0;"><li>읽기/쓰기 요청: 기본적으로 각 버킷은 중국 본토의 퍼블릭 클라우드 리전에서 30000QPS를, 다른 리전에서는 최대 3000 QPS를 향유합니다.
					<li> List 요청: 모든 리전 1200QPS. </ li >
					<li>데이터 검색 요청: 모든 리전의 기본값은 100QPS입니다.
<br>더 높은 QPS가 필요한 경우 <a href="https://intl.cloud.tencent.com/document/product/436/13653">요청 속도 및 성능 최적화</a>를 참고하십시오.</li></ul></td>
    </tr>
		    <tr>
        <td>대역폭</td>
    			<td>제한</td>
					<td>중국 대륙 공유 클라우드 리전의 기본 대역폭: 업/다운스트림 15Gbit/s. 기타 리전: 업/다운스트림 10Gbit/s. 대역폭이 임계값에 도달한 경우 트래픽 제어가 트리거됩니다. 더 높은 대역폭이 필요한 경우<a href="https://console.cloud.tencent.com/workorder/category">Tencent Cloud A/S 엔지니어</a>에게 문의하십시오.</td>	
    </tr>
    	 <tr>
        <td rowspan="5">스토리지 유형</td>
    			<td>표준 스토리지 제한</td>
    			<td>과금 제한: <br>스토리지 기간, 스토리지 단위 무제한 <br>표준 스토리지에 대한 자세한 가격은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</td>
    </tr>
    	 <tr>
        <td>표준IA 스토리지 제한</td>
    			<td>과금 제한: <ul  style="margin: 0;"><li>스토리지 기간 30일 미만 객체는, 30일로 청구됩니다.</li>
					<li>스토리지 단위가 64KB 미만인 경우 64KB로 계산하며, 64KB 이상인 경우 실제 크기로 계산합니다.<br>표준IA 스토리지에 대한 자세한 가격은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</li></ul></td>
    </tr>
    	 <tr>
        <td>인텔리전트 티어링 스토리지 스토리지 제한</td>
    			<td>과금 제한: <ul  style="margin: 0;"><li>스토리지 기간 30일 미만 객체는, 30일로 청구됩니다.</li>
					<li>64KB 미만 객체는 고빈도 액세스 레이어에 저장됩니다. 단일 스토리지 파일의 크기에 관계없이 실제 데이터 크기에 따라 계산됩니다. <br>인텔리전트 티어링 스토리지의 구체적인 가격은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오. </td>
    </tr>
    	 <tr>
        <td>CAS 제한</td>
    			<td>과금 제한: <ul  style="margin: 0;"><li>스토리지 기간 90일 미만 객체는, 90일로 청구됩니다.</li>
					<li>스토리지 단위가 64KB 미만인 경우 64KB로 계산하며, 64KB 이상인 경우 실제 크기로 계산합니다. <br>CAS에 대한 자세한 가격은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</li></ul></td>
    </tr>
    	 <tr>
        <td>DEEP ARCHIVE 제한</td>
    			<td>과금 제한: <ul  style="margin: 0;"><li>스토리지 기간 180일 미만 객체는, 180일로 청구됩니다.</li>
					<li>스토리지 단위가 64KB 미만인 경우 64KB로 계산하며, 64KB 이상인 경우 실제 크기로 계산합니다. <br>DEEP ARCHIVE에 대한 자세한 가격은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</li></ul></td>
    </tr>
     <tr>
        <td rowspan="4">버킷</td>
    			<td>제한</td>
    			<td><ul style="margin: 0;"><li>버킷이 성공적으로 생성되면 이름과 리전을 수정할 수 없습니다. </li>
					<li>지정된 계정에 있는 각 버킷의 이름은 고유하며 변경할 수 없습니다.</li>
					<li> 이름은 ‘-’로 시작하거나 끝날 수 없으며 영문 소문자 및 숫자[az, 0-9], 하이픈 ‘-’만 지원됩니다. 버킷 이름의 최대 글자 수는 < a href= "https://buy.cloud.tencent.com/price/cos">리전 약칭</a> 및 APPID 의 글자 수에 따라 달라집니다. 전체 요청 도메인 이름 글자 수는 최대 60자입니다. </li></ul></td>
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
					<td >객체 키 길이는 1 - 850B까지 지원하며, 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/13324">객체 개요</a>를 참고하십시오.</td>
    		</tr>
    			<tr>
    			<td>업로드</td>
    			<td><ul  style="margin: 0;"><li>콘솔을 통해 업로드할 수 있는 객체 최대 크기는 512GB입니다.</li>
					<li> API/SDK를 통해 업로드할 수 있는 객체의 최대 크기는 48.82TB (50,000GB)입니다.
						<br>인터페이스 업로드 규격: 
						<ul  style="margin: 0;"><li>간편 업로드: 단일 객체 최대 5GB. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/14113">간편 업로드</a>를 참고하십시오.</li>
						<li> 멀티파트 업로드: 단일 객체 최대 48.82TB. 파트 개수 1 - 10,000개. 파트 크기 1MB - 5GB. 마지막 파트 크기는 1MB 미만 가능. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/14112">멀티파트 업로드</a>를 참고하십시오.</li></ul>
					</li>
					<li>현재 버킷에서 인텔리전트 티어링 스토리지 구성이 활성화된 경우에만 객체를 인텔리전트 티어링 스토리지 스토리지 클래스에 업로드할 수 있습니다. 서로 다른 스토리지 레이어 간의 객체 변환은 인텔리전트 티어링 스토리지 구성의 매개변수에 의해 결정됩니다.</li></ul></td>
    		</tr>
    		<tr>
    			<td >복제</td>
    			<td ><ul  style="margin: 0;"><li>하나의 계정으로 리전 내 또는 리전 간 객체 복제를 수행할 수 있습니다.</li>
					<li> 리전 내 객체 복제는 무료이지만 리전 간 객체 복제는 트래픽 요금이 발생합니다. 자세한 내용은 <a href="https://buy.cloud.tencent.com/price/cos">요금 설명</a> 중의 트래픽 요금 정보를 참고하십시오. </li>
					<li>인터페이스 복제 규격: 
						<ul  style="margin: 0;"><li>간편 복사: 단일 객체 최대 5GB. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/14117">간편 복사</a>를 참고하십시오.</li>
						<li>5GB 이상 48.82TB 이하의 객체는 멀티파트 복제를 사용해야 합니다. 자세한 내용은<a href="https://intl.cloud.tencent.com/document/product/436/14118">멀티파트 복제</a>를 참고하십시오.</li></ul>
					</li>
					<li>표준 스토리지, 표준IA 스토리지, 인텔리전트 티어링 스토리지 유형을 인텔리전트 티어링 스토리지 유형으로 복제하는 것은 지원되지 않습니다.</li></ul></td>
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
