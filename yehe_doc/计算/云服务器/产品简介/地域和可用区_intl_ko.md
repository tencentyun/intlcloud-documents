## 리전

### 개요

리전(Region)은 물리적 IDC의 지리적 위치를 의미합니다. Tencent Cloud는 리전별로 완전히 격리되어, 리전별 안정성과 고장 방지 능력을 최대한 보장합니다. 딜레이를 줄이고 다운로드 속도를 높이려면 클라이언트에서 가장 가까운 리전을 선택하는 것이 좋습니다.

다음 리스트 혹은 [DescribeRegion](https://intl.cloud.tencent.com/document/product/213/15708) API를 통해 전체 리전 리스트를 조회할 수 있습니다.

### 관련 특징

- 리전별로 네트워크는 완전히 격리됩니다. 리전 간 클라우드 서비스는 **기본적으로 사설망을 통해 접속이 불가능합니다**.
- 각 리전 간의 클라우드 서비스는 [공용 네트워크 IP](https://intl.cloud.tencent.com/document/product/213/5224)를 통해 Internet에 접속하는 방식으로 통신합니다. 각각 다른 VPC에 위치한 클라우드 서비스는 더욱 빠르고 안정적인 [CCN](https://intl.cloud.tencent.com/document/product/1003)을 통해 통신합니다.
- [CLB](https://intl.cloud.tencent.com/document/product/214)는 기본적으로 동일 리전의 트래픽을 전달하며 로컬 리전 CVM에 바인딩합니다. [CLB Instance Cross-Region Binding](http://intl.cloud.tencent.com/document/product/214/12014) 기능을 활성화하면 CLB의 리전 간 CVM 바인딩이 지원됩니다.

## 가용존(AZ)

### 개요

가용존(Zone)이란 Tencent Cloud가 동일한 리전 내에서 상호 독립적인 전력과 네트워크를 보유한 물리적인 데이터센터를 말합니다. 가용존의 장애를 서로 격리(대규모 재해 혹은 대규모 전력 장애 제외)하여 확산을 방지하고, 사용자가 온라인 서비스를 유지할 수 있도록 보장합니다. 독립 가용존 내의 인스턴스를 실행하면 사용자는 응용 프로그램이 개별 위치 장애의 영향을 받지 않게 할 수 있습니다.
[DescribeZone](https://intl.cloud.tencent.com/document/product/213/35071) API를 통해 전체 가용존 리스트를 조회할 수 있습니다.

### 관련 특징

동일 리전의 다른 가용존에 있더라도 동일 VPC에 있는 클라우드 서비스는 사설망을 통해 연결됩니다. [사설 IP](http://intl.cloud.tencent.com/document/product/213/5225)를 사용하여 액세스할 수 있습니다.
<dx-alert infotype="explain" title="">
사설망 상호 연결은 동일한 계정으로 리소스를 상호 연결하는 것을 말합니다. 다른 계정의 리소스는 사설망에서 완전히 격리됩니다.
</dx-alert>


## 중국 본토[](id:MainlandChina)
<table class="table-striped">
<tbody>
	<tr>
		<th>리전</th>
		<th>가용존</th>
	</tr>
	<tr>
		<td rowspan="6">화남 지역(광저우)<br> ap-guangzhou</td>
		<td>광저우1존(품절)<br> ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>광저우2존(품절)<br> ap-guangzhou-2</td>
	</tr>
	<tr>
		<td>광저우3존<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>광저우4존<br> ap-guangzhou-4</td>
	</tr>
	<tr>
		<td>광저우6존<br> ap-guangzhou-6</td>
	</tr>
	<tr>
		<td>광저우 7존<br> ap-guangzhou-7</td>
	</tr>
	<tr>
		<td rowspan="6">화동 지역(상하이)<br>ap-shanghai</td>
		<td>상하이1존(품절)<br>ap-shanghai-1</td>
	</tr>
	<tr>
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
		<td>상하이8존<br>ap-shanghai-8</td>
	</tr>
	<tr>
			<td rowspan="3">화동 지역(난징)<br>ap-nanjing</td>
			<td>난징1존<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>난징2존<br>ap-nanjing-2</td>
	</tr>
	<tr>
			<td>난징3존<br>ap-nanjing-3</td>
	</tr>
	<tr>
			<td rowspan="7">화북 지역(베이징)<br>ap-beijing</td>
			<td>베이징1존(품절)<br>ap-beijing-1</td>
	</tr>
	<tr>
			<td>베이징2존<br>ap-beijing-2</td>
	</tr>
	<tr>
			<td>베이징3존<br>ap-beijing-3</td>
	</tr>
	<tr>
			<td>베이징4존<br>ap-beijing-4</td>
	</tr>
	<tr>
			<td>베이징5존<br>ap-beijing-5</td>
	</tr>
		<tr>
			<td>베이징6존<br>ap-beijing-6</td>
	</tr>
		<tr>
			<td>베이징7존<br>ap-beijing-7</td>
	</tr>
	<tr>
		<td rowspan="2">서남 지역(청두)<br>ap-chengdu</td>
		<td>청두1존<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>청두2존<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >서남 지역(충칭)<br>ap-chongqing</td>
			<td>충칭1존<br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="3">중국홍콩, 마카오 및 대만 지역(중국홍콩)<br>ap-hongkong</td>
			<td>홍콩1존(중국 홍콩 노드의 커버리지: 홍콩/마카오/대만 지역)(품절)<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>홍콩2존(중국 홍콩 노드의 커버리지: 홍콩/마카오/대만 지역)<br>ap-hongkong-2</td>
	</tr>
	<tr>
			<td>홍콩3존(중국 홍콩 노드의 커버리지: 홍콩/마카오/대만 지역)<br>ap-hongkong-3</td>
	</tr>
</tbody>
</table>	

<dx-alert infotype="explain" title="">
지난, 항저우, 푸저우, 우한, 창사, 스자좡 리전은 현재 베타 테스트 중이므로 사용을 원하시면 비즈니스 매니저에게 연락하여 신청하십시오.
</dx-alert>


## 기타 국가 및 지역[](id:InternationalArea)	
<table class="table-striped">
	<tbody>
	<tr>
			<th>리전</th>
			<th>가용존</th>
		</tr>
		<tr>
			<td  rowspan="4">동남아(싱가포르)<br>ap-singapore</td>
			<td>싱가포르1존(싱가포르 노드의 커버리지: 동남아 지역)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>싱가포르2존(싱가포르 노드의 커버리지: 동남아 지역)<br>ap-singapore-2</td>
		</tr>
		<tr>
			<td>싱가포르3존(싱가포르 노드의 커버리지: 동남아 지역)<br>ap-singapore-3</td>
		</tr>
   <tr>
			<td>싱가포르4존(싱가포르 노드의 커버리지: 동남아 지역)<br>ap-singapore-4</td>
		</tr>
		<tr>
			<td rowspan="2">동남아(자카르타)<br>ap-jakarta</td>
			<td>자카르타1존(자카르타 노드의 커버리지: 동남아 지역)<br>ap-jakarta-1</td>
		</tr>
		<tr>
			<td>자카르타2존(자카르타 노드의 커버리지: 동남아 지역)<br>ap-jakarta-2</td>
		</tr>
		<tr>
			<td rowspan="2">동북아(서울)<br>ap-seoul</td>
			<td>서울1존(서울 노드의 커버리지: 동북아 지역)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>서울2존(서울 노드의 커버리지: 동북아 지역)<br>ap-seoul-2</td>
		</tr>
		<tr >
			<td rowspan="2">동북아(도쿄)<br>ap-tokyo</td>
			<td>도쿄1존(도쿄 노드 가용존 커버리지: 동북아 지역)<br>ap-tokyo-1</td>
		</tr>
		 <tr>
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
		  	<td rowspan="2">동남아(방콕)<br>ap-bangkok </td>
				 <td >방콕1존  (방콕 노드 사용자 커버리지: 동남아 지역)<br>ap-bangkok-1</td>
		</tr>
		<tr>
			<td >방콕2존(방콕 노드 사용자 커버리지: 동남 아시아 지역)<br>ap-bangkok-2</td>
		</tr>
		<tr>
			<td>북미 지역(토론토)<br>na-toronto</td>
			<td>토론토1존(토론토 노드의 커버리지: 북미 지역)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td>남미 지역(상파울루)<br>sa-saopaulo</td>
			<td>상파울루1존(상파울루 노드의 커버리지: 남미 지역)<br>sa-saopaulo-1</td>
		</tr>
		<tr>
			<td rowspan="2">미국 서부(실리콘밸리)<br>na-siliconvalley</td>
			<td>실리콘 밸리1존(실리콘 밸리 노드의 커버리지: 미국 서부 지역)<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>실리콘 밸리2존(실리콘 밸리 노드의 커버리지: 미국 서부 지역)<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">미국 동부(버지니아)<br>na-ashburn</td>
			<td>버지니아1존(버지니아 노드 사용자 커버리지: 미국 동부 지역)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>버지니아2존(버지니아 노드 사용자 커버리지: 미국 동부 지역)<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td rowspan="2">유럽 지역(프랑크푸르트)<br>eu-frankfurt</td>
			<td>프랑크푸르트1존(프랑크푸르트 노드의 커버리지: 유럽 지역)<br>eu-frankfurt-1</td>
		</tr>
		<tr>
			<td>프랑크푸르트2존(프랑크푸르트 노드의 커버리지: 유럽 지역)<br>eu-frankfurt-2</td>
		</tr>
	</tbody>
</table>

## 리전 및 가용존 선택 방법

리전과 가용존 선택 시, 다음 요소를 고려해야 합니다.
- CVM 소재 지역, 귀하와 귀하의 클라이언트가 위치한 지리적 위치.
CVM 구매 시, 액세스 지연 시간 단축 및 액세스 속도 향상을 위해 클라이언트와 가장 가까운 리전을 선택하시기 바랍니다.
- CVM과 기타 클라우드 서비스의 관계.
기타 클라우드 서비스 선택 시, 최대한 동일 리전의 동일 가용존을 적용하시기 바랍니다. 이 경우에 각 클라우드 제품은 사설망으로 통신하므로 액세스 지연 시간 단축 및 액세스 속도 향상이 가능합니다.
- 서비스 고가용성과 장애 복구 고려
VPC가 1개뿐인 시나리오 역시 가용존 장애 격리 및 가용존 간 재해 복구 보장을 위해 각기 다른 가용존에 서비스를 배포하시기를 권장합니다.
- 가용존 간 네트워크 연결이 지연될 수 있습니다. 서비스의 실제 요구사항에 따라 검토해야 하며, 고가용성과 저지연성의 최적화된 밸런스 포인트를 찾아야 합니다.
- 다른 국가 및 지역의 호스트에 액세스하려면 다른 국가 및 지역의 클라우드 서버를 선택하여 액세스하는 것이 좋습니다. 만약 [중국](#MainlandChina)에 생성한 CVM으로 [기타 국가 및 지역의 서버](#InternationalArea)에 액세스할 경우, 액세스 지연 시간이 길어집니다.

## 리소스 위치 설명
다음은 Tencent Cloud의 글로벌 리소스, 리전 구분/ 가용존 미구분 리소스, 가용존 기반 리소스에 대한 설명입니다.

<table>
	<tr><th width="14%">리소스</th><th>리소스 ID 형식<br><리소스 약자>-8자리 숫자 및 문자 부호</th><th>유형</th><th>설명</th></tr>
	<tbody>
	<tr>
	  <td>사용자 계정</td>
	  <td>제한 없음</td>
	  <td>전 세계 유일</td>
	  <td>사용자는 하나의 계정으로 Tencent Cloud의 세계 각지의 리소스에 액세스할 수 있습니다. </td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH 키</a> </td>
	  <td>skey-xxxxxxxx</td>
	  <td>전체 리전 사용 가능</td>
	  <td>사용자는 SSH 키를 사용하여 계정 내 모든 리전의 CVM을 바인딩 할 수 있습니다. </td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">CVM 인스턴스</a> </td>
	  <td>ins-xxxxxxxx</td>
	  <td>단일 리전의 단일 가용존에서만 사용 가능</td>
	  <td>사용자는 특정 가용존에서만 CVM 인스턴스를 생성할 수 있습니다. </td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941">사용자 정의 이미지</a> </td>
	  <td>img-xxxxxxxx</td>
	  <td>단일 리전의 멀티 가용존 사용 가능</td>
	  <td>사용자는 인스턴스의 사용자 정의 이미지를 생성하여, 동일 리전의 다른 가용존에서 사용할 수 있습니다. 다른 리전에 사용할 경우, 이미지 복제 기능을 사용하여 사용자 정의 이미지를 다른 리전에 복제하십시오. </td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a> </td>
	  <td>eip-xxxxxxxx</td>
	  <td>단일 리전의 멀티 가용존 사용 가능</td>
	  <td>EIP 주소는 임의의 리전에 생성하며, 동일 리전의 인스턴스만 연결 가능합니다. </td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/12452">보안 그룹</a> </td>
	  <td>sg-xxxxxxxx</td>
	  <td>단일 리전의 멀티 가용존 사용 가능</td>
	  <td>EIP 주소는 임의의 리전에 생성하며, 동일 리전의 인스턴스만 연결 가능합니다. Tencent Cloud는 사용자를 위해 세 개의 기본 보안 그룹을 자동으로 생성합니다. </td>
	</tr>
	<tr>
	<td> <a href="https://www.tencentcloud.com/document/product/362">Cloud Block Storage</a> </td>
	  <td>disk-xxxxxxxx</td>
	  <td>단일 리전의 단일 가용존에서만 사용 가능</td>
	  <td>사용자는 지정된 가용존에만 CBS를 생성할 수 있으며, 동일 가용존의 인스턴스에 마운트해야 합니다. </td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362/31638">스냅샷</a> </td>
	  <td>snap-xxxxxxxx</td>
	  <td>단일 리전의 멀티 가용존 사용 가능</td>
	  <td>CBS에 스냅샷을 생성하면, 사용자는 해당 리전에서 이 스냅샷을 이용하여 다른 작업(CBS 생성 등)을 진행할 수 있습니다. </td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/214/524">로드 밸런서</a> </td>
	  <td>clb-xxxxxxxx</td>
	  <td>단일 리전의 멀티 가용존 사용 가능</td>
	  <td>CLB는 트래픽 전달을 위해 단일 리전의 서로 다른 가용존에 있는 CVM과 바인딩될 수 있습니다. </td>
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
	  <td>사용자는 가용존 간에 서브넷을 구축할 수 없습니다. </td>
	</tr>
	<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/215/31810">라우팅 테이블</a> </td>
	  <td>rtb-xxxxxxxx</td>
	  <td>단일 리전의 멀티 가용존 사용 가능</td>
	  <td>사용자의 라우팅 테이블 생성 시 VPC를 지정해야 하므로, VPC의 위치 속성을 따릅니다. </td>
	</tr>
	</tbody>
</table>


## 관련 작업

### 인스턴스를 다른 가용존으로 마이그레이션

이미 실행된 인스턴스는 가용존 변경이 불가능하지만 사용자는 다른 방법으로 인스턴스를 기타 가용존에 마이그레이션 할 수 있습니다. 마이그레이션 프로세스에는 원본 인스턴스에서 사용자 정의 이미지 생성, 사용자 정의 이미지를 사용하여 새 가용존에서 인스턴스 활성화, 새 인스턴스의 구성 업데이트가 포함됩니다.
1. 기존 인스턴스의 사용자 정의 이미지를 생성합니다. 자세한 내용은 [사용자 정의 이미지 생성](http://intl.cloud.tencent.com/document/product/213/4942)을 참고하시기 바랍니다.
2. 만약 현재 인스턴스의 [네트워크 환경](https://cloud.tencent.com/doc/product/213/5227)이 VPC이고 마이그레이션 후 현재의 사설 IP 주소 보존이 필요할 경우, 현재 가용존의 서브넷을 삭제한 뒤 새로운 가용존에서 사용하거나 원본 서브넷과 같은 IP 주소의 범위에서 서브넷을 생성하십시오. 사용 가능한 인스턴스를 포함하고 있지 않는 서브넷만 삭제할 수 있습니다. 따라서 현재 서브넷의 모든 인스턴스를 새 서브넷으로 이동해야 합니다.
3. 새로운 가용존의 새 인스턴스에서 방금 생성한 사용자 정의 이미지를 사용하십시오. 사용자는 원본 인스턴스와 같은 인스턴스 유형 및 구성을 선택하거나 새로운 인스턴스 유형 및 구성을 선택할 수 있습니다. 자세한 내용은 [인스턴스 생성](https://cloud.tencent.com/doc/product/213/4855)을 참고하십시오.
4. 원본 인스턴스에 EIP 주소가 연결된 경우, 기존 인스턴스와의 연결을 해제하고 새 인스턴스와 연결합니다. 자세한 내용은 [Elastic IP](https://intl.cloud.tencent.com/document/product/213/5733)를 참고하십시오.
5. (옵션)기존 인스턴스가 [종량제](https://intl.cloud.tencent.com/document/product/213/2180)인 경우, 기존 인스턴스를 폐기할 수 있습니다. 자세한 내용은 [인스턴스 폐기/반환](https://intl.cloud.tencent.com/document/product/213/4930)을 참고하십시오.

### 다른 리전에 이미지 복제

사용자가 인스턴스 실행, 인스턴스 조회 등의 작업을 진행할 때 리전 속성을 구분하여 진행합니다. 사용자가 인스턴스를 시작하는 데 필요한 이미지가 리전에 없으면 이미지를 리전에 복제해야 합니다. 자세한 내용은 [이미지 복제](https://intl.cloud.tencent.com/document/product/213/4943)를 참고하십시오.

