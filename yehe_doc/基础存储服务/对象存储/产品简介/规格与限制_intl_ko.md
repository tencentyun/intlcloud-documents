<table>
    <tr>
        <th>분류</th> 
        <th>규격 및 제한</th> 
    			<th>상세 설명</th> 
   </tr>
    <tr>
        <td>QPS</td>
    			<td>제한</td>
    			<td><ul  style="margin: 0;"><li>읽기/쓰기 요청: 중국 대륙의 퍼블릭 클라우드 리전에 있는 버킷에 대해 30000QPS 또는 다른 리전에 있는 각 버킷에 대해 3000QPS</li>
					<li>버킷 내 객체/이전 버전/진행 중인 멀티파트 업로드 작업 나열 요청: 기본적으로 모든 리전에서 버킷당 1000QPS.</li>
                    <li>버킷 생성/삭제/열거 요청: 모든 리전에서 각 APPID에 대해 50QPS.</li>					
                    <li>데이터 검색 요청: 모든 리전의 버킷당 100QPS.</li>
                    <li>일회성 인벤토리 작업 생성 요청: 모든 리전의 각 버킷에 대해 1QPS.</li>
					<li>단일 파일 업로드/삭제/List 요청을 통한 트래픽 조절: 50QPS.</li>
					<li>단일 파일 다운로드 요청을 통한 트래픽 조절: 1000QPS.
<br>QPS 임계값을 높이려면 <a href="https://intl.cloud.tencent.com/document/product/436/13653">요청 속도 및 성능 최적화</a>를 참고하십시오.</li></ul></td>
    </tr>
		    <tr>
        <td>대역폭</td>
    			<td>제한</td>
					<td>중국 대륙의 퍼블릭 클라우드 리전에 있는 각 버킷에 대해 15Gbit/s의 업스트림 및 다운스트림 대역폭 또는 다른 리전에 있는 각 버킷에 대해 10Gbit/s입니다. 이 임계값에 도달하면 트래픽 조절이 요청됩니다. 임계값을 높이려면 <a href="https://console.cloud.tencent.com/workorder/category">Tencent Cloud A/S 엔지니어</a>에게 문의하십시오.</td>	
    </tr>
    	 <tr>
        <td rowspan="5">스토리지 유형</td>
    			<td>MAZ(다중AZ)_STANDARD/STANDARD 제한</td>
    			<td>과금 제한: <br>저장 기간이나 객체 크기에는 제한이 없습니다. <br>STANDARD 가격은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</td>
    </tr>
    	 <tr>
        <td>MAZ_STANDARD_IA/STANDARD_IA 제한</td>
    			<td>과금 제한: <ul  style="margin: 0;"><li>30일 미만 동안 저장된 객체는 30일 기준으로 청구됩니다.</li>
					<li>64KB보다 작은 객체는 64KB로 과금됩니다. 객체 크기가 64KB 이상인 경우 실제 크기를 기준으로 요금이 청구됩니다. <br>STANDARD_IA 과금에 대한 자세한 내용은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</li></ul></td>
    </tr>
    	 <tr>
        <td>MAZ_INTELLIGENT TIERING/INTELLIGENT TIERING 제한</td>
    			<td>과금 제한: <br>64KB보다 작은 객체는 고빈도 액세스 티어에 저장됩니다. 객체는 실제 크기에 따라 요금이 청구됩니다. <br>INTELLIGENT TIERING 과금에 대한 자세한 내용은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</td>
    </tr>
    	 <tr>
        <td>ARCHIVE 제한</td>
    			<td>과금 제한: <ul  style="margin: 0;"><li>90일 미만 동안 저장된 객체는 90일 기준으로 청구됩니다.</li>
					<li>64KB보다 작은 객체는 64KB로 과금됩니다. 객체 크기가 64KB 이상인 경우 실제 크기를 기준으로 요금이 청구됩니다. <br>ARCHIVE 과금에 대한 자세한 내용은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</li></ul></td>
    </tr>
    	 <tr>
        <td>DEEP ARCHIVE 제한</td>
    			<td>과금 제한: <ul  style="margin: 0;"><li>180일 미만 동안 저장된 객체는 180일 기준으로 청구됩니다.</li>
					<li>64KB보다 작은 객체는 64KB로 과금됩니다. 객체 크기가 64KB 이상인 경우 실제 크기를 기준으로 요금이 청구됩니다. <br>DEEP ARCHIVE 과금에 대한 자세한 내용은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>을 참고하십시오.</li></ul></td>
    </tr>
     <tr>
        <td rowspan="4">버킷</td>
    			<td>제한</td>
    			<td><ul  style="margin: 0;"><li>버킷이 생성되면 이름이나 리전을 수정할 수 없습니다.</li>
					<li>동일한 계정에 속한 버킷의 이름은 고유해야 하며 이름을 변경할 수 없습니다.</li>
					<li> 버킷 이름은 하이픈‘-’으로 시작할 수 없으며 영어 소문자, 숫자[a-z，0-9] 및 하이픈‘-’만 포함할 수 있습니다. 버킷 이름의 길이는 <a href="https://intl.cloud.tencent.com/document/product/436/6224">리전 약칭</a> 및 APPID의 문자 수로 제한됩니다. 전체 도메인은 최대 60자를 포함할 수 있습니다.</li></ul></td>
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
					<td >객체 키 길이는 1 - 850B까지 지원됩니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/13324">객체 개요</a>를 참고하십시오.</td>
    		</tr>
    			<tr>
    			<td>업로드</td>
    			<td><ul  style="margin: 0;"><li>콘솔에 업로드할 수 있는 단일 객체 크기는 최대 512GB입니다.</li>
					<li> API/SDK를 통해 업로드할 수 있는 단일 객체 크기는 최대 48.82TB(50,000GB)입니다.
						<br>업로드 API 사양:
						<ul  style="margin: 0;"><li>간편 업로드: 단일 객체는 최대 5GB입니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/14113">간편 업로드</a>를 참고하십시오.</li>
						<li> 멀티파트 업로드: 단일 객체는 최대 48.82TB까지 가능하며, 파트 크기는 1MB - 5GB이어야 하며, 마지막 파트는 1MB보다 작을 수 있습니다. 1 - 10000개의 파트가 있을 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/14112">멀티파트 업로드</a>를 참고하십시오.</li></ul>
					</li>
					<li>현재 MAZ 구성이 활성화된 버킷의 경우 객체를 MAZ 스토리지 클래스(MAZ_STANDARD 또는 MAZ_STANDARD_IA)에 업로드할 수 있습니다. 버킷에 대해 INTELLIGENT TIERING 구성도 활성화된 경우 객체를 MAZ_INTELLIGENT TIERING 스토리지 클래스에 업로드할 수도 있습니다.</li>
					<li>버킷에 대해 INTELLIGENT TIERING을 활성화한 경우에만 INTELLIGENT TIERING 스토리지 클래스에 객체를 업로드할 수 있습니다. 티어 간에 객체를 전환하는 방법은 INTELLIGENT TIERING 구성에 따라 다릅니다.</li></ul></td>
    		</tr>
    		<tr>
    			<td >복사</td>
    			<td ><ul  style="margin: 0;"><li>동일한 계정에 속한 객체는 버킷 내부 및 버킷 간에 복사할 수 있습니다.</li>
					<li> 리전 내 복사는 무료입니다. 그러나 리전 간 복사에는 트래픽 요금이 발생합니다. 자세한 내용은 <a href="https://buy.cloud.tencent.com/price/cos">제품 가격</a>의 트래픽 요금을 참고하십시오. </li>
					<li>API 복사 사양:
						<ul  style="margin: 0;"><li>단순 복사: 복사할 수 있는 단일 객체 크기는 최대 5GB입니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/14117">간편 복사</a>를 참고하십시오.</li>
						<li>객체가 5GB보다 큰 경우 멀티파트 복사를 사용해야 합니다. 복사할 단일 객체는 최대 48.82TB입니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/436/14118">멀티파트 복사</a>를 참고하십시오.</li></ul>
					</li>
					<li>MAZ 버킷의 객체는 OAZ 버킷에 복제할 수 없습니다.</li>
					<li>현재 STANDARD, STANDARD_IA 또는 INTELLIGENT TIERING 객체를 INTELLIGENT TIERING 스토리지 클래스에 복사할 수 없습니다.</li></ul></td>
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
    			<td >각 버킷에는 최대 1000개의 라이프 사이클 규칙이 있을 수 있습니다.</td>
    		</tr>
    		<tr>
    			<td >스토리지 유형 전환</td>
    			<td >STANDARD에서 STANDARD_IA로 전환: 최소 1일. <br>STANDARD/STANDARD_IA에서 ARCHIVE/DEEP ARCHIVE로 전환: 최소 1일. <br>참고: <br>1. MAZ_STANDARD 또는 MAZ_STANDARD_IA 스토리지 유형의 객체는 STANDARD, STANDARD_IA 또는 ARCHIVE 스토리지 유형으로 전환할 수 없습니다. <br>2. 64KB보다 작은 객체는 전환할 수 없습니다.</td>
    		</tr>
    		 <tr>
    			<td >만료 삭제</td>
    			<td >STANDARD/STANDARD_IA/ARCHIVE: 최소 1일</td>
    		</tr>         
    		<tr>
    			<td colspan="2">SDK 종류</td>
    			<td >14가지: Android, C, C++, .NET, Flutter, Go, iOS, Java, JavaScript, Node.js, PHP, Python, React Native, 미니프로그램 SDK</td>
    		</tr>        
    		<tr>
    			<td colspan="2">API 예약 필드</td>
    			<td >API 문서와 관련된 모든 API 필드는 COS 예약 필드입니다. 다음을 포함합니다: <br>acl, uploads, policy, cors, delete, versions, location, referer, lifecycle, versioning, notification, replication, website, logging, tagging, accelerate, domain, inventory, origin, object-lock, live, encryption, intelligenttiering, symlink 등.</br></td>
    		</tr>
</table>


