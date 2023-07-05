## 리전

### 개요

리전(Region)은 물리적 데이터센터의 지리적 구역입니다. Tencent Cloud는 리전별로 철저히 격리되어, 리전별 안정성과 내고장성을 최대한 확보합니다. 액세스 지연 시간 축소 및 액세스 속도 향상을 위해 클라이언트와 가장 가까운 리전을 선택하시기 바랍니다.

다음 리스트 혹은 API 인터페이스 [DescribeRegion](https://intl.cloud.tencent.com/document/product/213/15708)을 통해 전체 리전 리스트를 조회할 수 있습니다.

### 관련 특징

- 리전별로 네트워크는 완전히 격리됩니다. 리전 간 클라우드 서비스는 **기본적으로 개인 네트워크를 통해 접속이 불가능합니다**.
- 리전 간 클라우드 서비스는 [공용망 서비스](https://intl.cloud.tencent.com/document/product/213/5224)를 통해 Internet에 액세스하는 방식으로 통신합니다. 각 VPC의 클라우드 서비스는 비교적 빠르고 안정적인 [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003)를 통해 통신합니다.
- [Cloud Load Balancer](https://intl.cloud.tencent.com/zh/document/product/214 )는 현재 기본적으로 리전 내 트래픽 전달과 로컬 리전 CVM과의 바인딩을 지원합니다. [cross-region binding](https://intl.cloud.tencent.com/document/product/214/38441) 기능을 활성화하면 CLB로 CVM의 여러 리전을 바인딩할 수 있습니다.

>

## 가용존

### 개요

가용존(Zone)은 동일 리전 내에서 전력과 네트워크가 별개로 적용되는 Tencent Cloud의 물리적 데이터센터입니다. 가용존의 장애를 서로 격리하여(대규모 재해 혹은 대규모 전력 장애 제외) 장애가 확산되지 않게 함으로써, 사용자가 온라인 서비스를 유지하도록 지원합니다. 사용자는 독립된 가용존의 인스턴스를 실행하여 응용 프로그램이 단일 위치에서 발생한 장애의 영향을 받지 않게 보호할 수 있습니다.
API 인터페이스 [DescribeZone](https://intl.cloud.tencent.com/document/product/213/35071)을 통해 전체 가용존 리스트를 조회할 수 있습니다.

### 관련 특징

동일 리전의 다른 가용존에 위치합니다. 동일 VPC의 클라우드 서비스는 개인 네트워크를 통해 연동됩니다. [인트라넷 서비스](http://intl.cloud.tencent.com/document/product/213/5225)를 사용하여 직접 액세스합니다.
>? 내부 네트워크 통신은 같은 계정 내 리소스가 연동됨을 의미하며, 다른 계정의 리소스는 내부 네트워크에서 철저히 격리됩니다.
>

<span id="MainlandChina"></span>
## 중국
<table class="table-striped">
<tbody>
	<tr>
		<th>리전</th>
		<th>가용존</th>
	</tr>
	<tr>
		<td rowspan="3">화남지역(광저우)<br> ap-guangzhou</td>
		<td>광저우3존<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>광저우4존<br> ap-guangzhou-4</td>
	</tr>
	<tr>
		<td>광저우6존<br> ap-guangzhou-6</td>
	</tr>
	<tr>
		<td rowspan="4">화동지역(상하이)<br>ap-shanghai</td>
		<td>상하이2존<br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>상하이3존<br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>상하이4존<br>ap-shanghai-4</td>
	</tr>
 <tr>
		<td>상하이5존<br>ap-shanghai-5</td>
	</tr>
	<tr>
			<td rowspan="2">화동지역(난징)<br>ap-nanjing</td>
			<td>난징1존<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>난징2존<br>ap-nanjing-2</td>
	</tr>
	<tr>
			<td rowspan="5">화북지역(베이징)<br>ap-beijing</td>
			<td>베이징3존<br>ap-beijing-3</td>
	</tr>
	<tr>
			<td>베이징4존<br>ap-beijing-4</td>
	</tr>
	<tr>
			<td>베이징5존<br>ap-beijing-5</td>
	</tr>
		<tr>
			<td>베이징 6존<br>ap-beijing-6</td>
	</tr>
		<tr>
			<td>베이징 7존<br>ap-beijing-7</td>
	</tr>
	<tr>
		<td rowspan="2">서남지역(청두)<br>ap-chengdu</td>
		<td>청두1존<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>청두2존<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td rowspan="1">홍콩/마카오/대만지역(홍콩)<br>ap-hongkong</td>
			<td>홍콩2존(중국 홍콩 노드의 커버리지: 홍콩/마카오/대만 지역)<br>ap-hongkong-2</td>
	</tr>
	<tr>
</tbody>
</table>	

<span id="InternationalArea"></span>

## 기타 국가 및 지역	
<table class="table-striped">
	<tbody>
	<tr>
			<th>리전</th>
			<th>가용존</th>
		</tr>
		<tr>
			<td  rowspan="2">동남아(싱가포르)<br>ap-singapore</td>
			<td>싱가포르1존(싱가포르 노드의 커버리지: 동남아 지역)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>싱가포르2존(싱가포르 노드의 커버리지: 동남아 지역)<br>ap-singapore-2</td>
		</tr>
		<tr>
			<td>동남아(자카르타)<br>ap-jakarta</td>
			<td>자카르타1존(자카르타 노드의 커버리지: 동남아 지역)<br>ap-jakarta-1</td>
		</tr>
		<tr>
			<td rowspan="2">동북아(서울)<br>ap-seoul</td>
			<td>서울1존(서울 노드의 커버리지: 동북아 지역)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>서울2존(서울 노드의 커버리지: 동북아 지역)<br>ap-seoul-2</td>
		</tr>
		<tr >
			<td rowspan="1">동북아(도쿄)<br>ap-tokyo</td>
			<td>도쿄2존(도쿄 노드 가용존 커버리지: 동북아 지역)<br>ap-tokyo-2</td>
		</tr>
       <tr>
			<td  rowspan="2">남아시아(뭄바이)<br>ap-mumbai</td>
			<td>뭄바이1존(뭄바이 노드의 커버리지: 남아시아 지역)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>뭄바이2존(뭄바이 노드의 커버리지: 남아시아 지역)<br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td rowspan="1">동남아(방콕)<br>ap-bangkok </td>
				 <td >방콕1존  (방콕 노드 사용자 커버리지: 동남아 지역)<br>ap-bangkok-1</td>
		</tr>
		<tr>
			<td>북미 지역(토론토)<br>na-toronto</td>
			<td>토론토1존(토론토 노드의 커버리지: 북미 지역)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">미국 동부(버지니아주)<br>na-ashburn</td>
			<td>버지니아 1존(버지니아 노드 사용자 커버리지: 미국 동부 지역)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>버지니아 2존(버지니아 노드 사용자 커버리지: 미국 동부 지역)<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td rowspan="1">유럽 지역(프랑크푸르트)<br>eu-frankfurt</td>
			<td>프랑크푸르트 1존(프랑크푸르트 노드의 커버리지: 유럽 지역)<br>eu-frankfurt-1</td>
		</tr>
		<tr>
		<td >유럽 지역(모스크바)<br>eu-moscow</td>
		<td>모스크바 1존(모스크바 노드의 커버리지: 유럽 지역)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>


## 리전과 가용존 선택하기

리전과 가용존 선택 시, 다음 요소를 고려해야 합니다.
- CVM 소재 지역, 귀하와 귀하의 클라이언트가 위치한 지리적 위치.
CVM 구매 시, 액세스 지연시간 축소 및 액세스 속도 향상을 위해 클라이언트와 가장 가까운 리전을 선택하시기 바랍니다.
- CVM과 기타 클라우드 서비스의 관계
기타 클라우드 서비스 선택 시, 최대한 동일 리전의 동일 가용존을 적용하시기 바랍니다. 이 경우에 각 클라우드 제품은 내부 네트워크로 통신하므로 액세스 지연시간 축소 및 액세스 속도 향상이 가능합니다.
- 서비스 고가용성과 장애 복구 고려
VPC가 1개뿐인 시나리오 역시 가용존 장애 격리 및 가용존 간 재해 복구 보장을 위해 각기 다른 가용존에 서비스를 배포하시기를 권장합니다.
- 가용존별로 네트워크 연결이 지연될 수 있습니다. 서비스의 실제 요구사항에 따라 검토해야 하며, 고가용성과 저지연성의 최적화 밸런스 포인트를 찾아야 합니다.
- 다른 국가와 리전의 호스트에 액세스하려면, 해당 국가와 지역의 CVM을 통해 액세스하시길 권장합니다. [중국](#MainlandChina)에 CVM을 생성하여 [다른 국가 및 지역의 서버](#InternationalArea)에 액세스할 경우, 액세스 딜레이가 길어 추천하지 않습니다.

## 리소스 위치 설명
다음은 Tencent Cloud의 글로벌 리소스, 리전 구분/ 가용존 미구분 리소스, 가용존 기반 리소스를 소개합니다.

<table>
	<tr><th>리소스</th><th>리소스 ID 형식<br><리소스 약자>-8자리 숫자 및 문자 부호</th><th>유형</th><th>설명</th></tr>
	<tbody>
	<tr>
	  <td>사용자 계정</td>
	  <td>제한 없음</td>
	  <td>전 세계 유일</td>
	  <td>사용자는 하나의 계정으로 Tencent Cloud의 세계 각 지역 리소스에 액세스할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH 키</a> </td>
	  <td>skey-xxxxxxxx</td>
	  <td>전체 리전 사용 가능</td>
	  <td>사용자는 SSH 키를 사용하여 계정 내 모든 리전의 CVM을 바인딩 할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">CVM 인스턴스</a> </td>
	  <td>ins-xxxxxxxx</td>
	  <td>단일 리전의 단일 가용존에서만 사용 가능</td>
	  <td>사용자는 특정 가용존에서만 CVM 인스턴스를 생성할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941">사용자 정의 이미지</a> </td>
	  <td>img-xxxxxxxx</td>
	  <td>단일 리전의 멀티 가용존 사용 가능</td>
	  <td>사용자는 인스턴스의 사용자 정의 이미지를 생성하여, 동일 리전의 다른 가용존에서 사용할 수 있습니다. 다른 리전에 사용할 경우, 이미지 복사 기능을 활용하여 사용자 정의 이미지를 다른 리전에 복사하시기 바랍니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a> </td>
	  <td>eip-xxxxxxxx</td>
	  <td>단일 리전의 멀티 가용존 사용 가능</td>
	  <td>EIP 주소는 임의의 리전에 생성하며, 동일 리전의 인스턴스만 연결 가능합니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/12452">보안 그룹</a> </td>
	  <td>sg-xxxxxxxx</td>
	  <td>단일 리전의 멀티 가용존 사용 가능</td>
	  <td>보안 그룹은 임의의 리전에 구축하며, 동일 리전의 인스턴스만 연결 가능합니다. Tencent Cloud는 자동으로 사용자에게 3개의 기본 보안 그룹을 구축합니다.</td>
	</tr>
	<tr>
	<td> <a href="https://cloud.tencent.com/document/product/362">CBS</a> </td>
	  <td>disk-xxxxxxxx</td>
	  <td>단일 리전의 단일 가용존에서만 사용 가능</td>
	  <td>사용자는 지정된 가용존에만 CBS를 생성할 수 있으며, 동일 가용존의 인스턴스에 마운트해야 합니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362/31638">스냅샷</a> </td>
	  <td>snap-xxxxxxxx</td>
	  <td>단일 리전의 멀티 가용존 사용 가능</td>
	  <td>CBS에 스냅샷을 생성하면, 사용자는 해당 리전에서 이 스냅샷을 이용하여 다른 작업(CBS 생성 등)을 진행할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/214/524">로드 밸런서</a> </td>
	  <td>clb-xxxxxxxx</td>
	  <td>단일 리전의 멀티 가용존 사용 가능</td>
	  <td>CLB는 단일 리전의 여러 가용존의 CVM을 바인딩하여 트래픽 전달 가능.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">VPC</a> </td>
	  <td>vpc-xxxxxxxx</td>
	  <td>단일 리전의 멀티 가용존 사용 가능</td>
	  <td>리전에 VPC을 생성하면, 다른 가용존에 동일 VPC 리소스를 생성할 수 있습니다. </td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535#.E5.AD.90.E7.BD.91">서브넷</a> </td>
	  <td>subnet-xxxxxxxx</td>
	  <td>단일 리전의 단일 가용존에서만 사용 가능</td>
	  <td>사용자는 가용존 간에 서브넷을 구축할 수 없습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/31810">라우팅 테이블</a> </td>
	  <td>rtb-xxxxxxxx</td>
	  <td>단일 리전의 멀티 가용존 사용 가능</td>
	  <td>사용자의 라우팅 테이블 생성 시 VPC를 지정해야 하므로, VPC의 위치 속성을 따릅니다.</td>
	</tr>
	</tbody>
</table>


## 관련 작업

###인스턴스를 기타 가용존에 마이그레이션합니다.

이미 실행된 인스턴스는 가용존 변경이 불가능하지만 사용자는 다른 방법으로 인스턴스를 기타 가용존에 마이그레이션 할 수 있습니다. 마이그레이션 프로세스는 원본 인스턴스로 사용자 정의 이미지 생성, 사용자 정의 이미지로 신규 가용존에서 인스턴스 실행, 신규 인스턴스 설정 업데이트 작업을 포함합니다.
1. 기존 인스턴스의 사용자 정의 이미지를 생성합니다. 자세한 내용은 [커스텀 미러 구축](http://intl.cloud.tencent.com/document/product/213/4942)을 참고하시기 바랍니다.
2. 기존 인스턴스의 [네트워크 환경](https://intl.cloud.tencent.com/document/product/213/5227)이 VPC이며, 마이그레이션 후 기존의 개인 IP 주소를 유지해야 할 경우, 사용자는 기존 가용존의 서브넷을 삭제하고, 신규 가용존에서 원본 서브넷과 같은 IP 주소 범위에 서브넷을 생성할 수 있습니다. 주의 사항은, 가용 인스턴스를 포함하지 않는 서브넷만 삭제할 수 있습니다. 그러므로, 기존 서브넷의 전체 인스턴스를 신규 서브넷에 마이그레이션해야 합니다.
3. 신규 생성한 사용자 정의 이미지를 이용하여 신규 가용존에 신규 인스턴스를 생성합니다. 사용자는 원본 인스턴스와 같은 유형 및 사양을 선택하거나, 새로운 유형 및 사양을 선택할 수 있습니다. 자세한 내용은 [구매 페이지를 통한 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하시기 바랍니다.
4. 원본 인스턴스에 EIP 주소를 연결하였을 경우, 기존 인스턴스와의 연결을 해제하고 신규 인스턴스와 연결합니다. 자세한 내용은 [EIP](https://intl.cloud.tencent.com/document/product/213/5733)를 참고하시기 바랍니다.
5. (옵션)기존 인스턴스가 [종량제](https://intl.cloud.tencent.com/document/product/213/2180)인 경우, 기존 인스턴스를 삭제할 수 있습니다. 자세한 내용은 [인스턴스 폐기](https://intl.cloud.tencent.com/document/product/213/4930)를 참고하시기 바랍니다.

### 이미지를 다른 리전에 복사합니다.

사용자의 인스턴스 실행, 조회 등 작업은 리전 속성을 구분합니다. 사용자가 실행하려는 인스턴스 이미지가 로컬에 존재하지 않을 경우, 이미지를 로컬에 복사해야 합니다. 자세한 내용은 [미러 복사](http://intl.cloud.tencent.com/document/product/213/4943)를 참고하시기 바랍니다.
