## 리전

### 개요

리전은 물리 데이터센터의 지리적 리전입니다. Tencent Cloud는 리전별로 철저히 격리되어, 리전별 안정성과 장애 허용성을 최대한 확보합니다. 액세스 지연시간을 줄이고 다운로드 속도 증가를 위해, 클라이언트와 가장 가까운 리전을 선택하시기 바랍니다.
 
다음 리스트 혹은 API 인터페이스[리전 리스트 조회](http://intl.cloud.tencent.com/document/product/213/9456)에서 상세한 리전 리스트를 조회할 수 있습니다.

### 특징

- 리전별로 네트워크는 완전 격리됩니다. 리전별 클라우드 제품은 **기본적으로 사설 네트워크를 통해 접속이 불가능합니다**.
- 리전별 클라우드 제품은 [공용 IP](http://intl.cloud.tencent.com/document/product/213/5224)를 통해 인터넷을 액세스합니다. 사설 네트워크의 클라우드 제품도 Tencent Cloud가 제공하는 [피어링 연결](http://intl.cloud.tencent.com/document/product/215/5000)을 통해 Tencent Cloud의 고속 인터넷 네트워크를 거쳐 안정적으로 인터넷에 액세스합니다.]
- [로드 밸런서](https://intl.cloud.tencent.com/document/product/214)는 기본적으로 동일 리전의 트래픽을 전달하며 같은 리전의 CVM에 바인딩합니다. [리전 간 바인딩](http://intl.cloud.tencent.com/document/product/214/12014) 기능이 활성화 되면 로드 밸런서는 리전 사이의 CVM 바인딩을 지원합니다.

## 가용 영역

### 개요

가용 영역(Zone)은 Tencent Cloud가 동일 리전에서 전력과 네트워크가 별개로 적용되는 물리적 데이터센터입니다. 가용 영역의 장애를 서로 격리(대규모 장애 복구 혹은 대규모 전력 장애 제외)되어 장애가 확산되지 않으며, 온라인상 서비스를 유지하도록 지원합니다. 독립 가용 영역의 인스턴스를 실행하면 애플리케이션은 개별 위치 장애의 영향을 받지 않습니다.
API 인터페이스 [가용 영역 리스트 조회](http://intl.cloud.tencent.com/document/product/213/9455)를 통해 가용 영역 상세 리스트를 조회할 수 있습니다.

### 특징

동일 리전의 다른 가용 영역에 위치합니다. 동일 VPC의 클라우드 제품은 사설 네트워크를 통해 연동됩니다. [사설 IP](http://intl.cloud.tencent.com/document/product/213/5225)를 사용하여 직접 액세스합니다.
>사설 네트워크 연동은 같은 계정 내 리소스가 연동됨을 의미하며, 다른 계정에 의한 리소스 액세스는 철저히 격리됩니다.

<span id="MainlandChina"></span>
## 중국
<table class="table-striped">
<tbody>
	<tr>
		<th>리전</th>
		<th>가용 영역</th>
	</tr>
	<tr>
		<td rowspan="4">화남지역(광저우)<br> ap-guangzhou</td>
		<td>광저우1존(품절)<br> ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>광저우2존<br> ap-guangzhou-2</td>
	</tr>
	<tr>
		<td>광저우3존<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>광저우4존<br> ap-guangzhou-4</td>
	</tr>
	<tr>
		<td rowspan="4">화동지역(상하이)<br>ap-shanghai</td>
		<td>상하이1존<br>ap-shanghai-1</td>
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
			<td rowspan="2">화동지역（남경）<br>ap-nanjing</td>
			<td>남경1존<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>남경2존<br>ap-nanjing-2</td>
	</tr>
	<tr>
			<td rowspan="4">화북지역(베이징)<br>ap-beijing</td>
			<td>베이징1존<br>ap-beijing-1</td>
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
		<td rowspan="2">서남지역(청두)<br>ap-chengdu</td>
		<td>청두1존<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>청두2존<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >서남지역(충칭)<br>ap-chongqing</td>
			<td>충칭1존<br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="2">홍콩/마카오/대만지역(홍콩)<br>ap-hongkong</td>
			<td>홍콩1존(중국 홍콩 노드의 커버리지는 홍콩/마카오/대만리전입니다)<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>홍콩2존(중국 홍콩 노드의 커버리지는 홍콩/마카오/대만리전입니다)<br>ap-hongkong-2</td>
	</tr>
</tbody>
</table>	

<span id="InternationalArea"></span>

## 기타 국가와 지역	
<table class="table-striped">
	<tbody>
	<tr>
			<th>리전</th>
			<th>가용 영역</th>
		</tr>
		<tr>
			<td>아시아-태평양 동남(싱가포르)<br>ap-singapore</td>
			<td>싱가포르1존(싱가포르 노드의 커버리지는 동남아시아 리전입니다)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td >아시아-태평양 동북(서울)<br>ap-seoul</td>
			<td>서울1존(서울 노드의 커버리지는 동북아시아 리전입니다)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td >아시아-태평양 동북(도쿄)<br>ap-tokyo</td>
			<td>도쿄1존(도쿄 노드의 커버리지는 동북아시아 리전입니다)<br>ap-tokyo-1</td>
		</tr>
       <tr>
			<td  rowspan="2">아시아-태평양 남부(뭄바이)<br>ap-mumbai</td>
			<td>뭄바이1존(뭄바이 노드의 커버리지는 남아시아 리전입니다)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>뭄바이2존(뭄바이 노드의 커버리지는 남아시아 리전입니다)<br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td >아시아-태평양 동남(방콕)<br>ap-bangkok </td>
				 <td >방콕1존(방콕 노드의 커버리지는 동남 아시아 리전입니다)<br>ap-bangkok-1</td>
		<tr>
			<td>북미지역(토론토)<br>na-toronto</td>
			<td>토론토1존(토론토 노드의 커버리지는 북미 리전입니다)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">미국 서부(실리콘 밸리)<br>na-siliconvalley</td>
			<td>실리콘 밸리 1존(실리콘 밸리 노드의 커버리지는 미국 서부 리전입니다)<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>실리콘 밸리 2존(실리콘 밸리 노드의 커버리지는 미국 서부 리전입니다)<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">미국 동부(버지니아)<br>na-ashburn</td>
			<td>버지니아 1존(버지니아 노드의 커버리지는 미국 동부 리전입니다)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>버지니아 2존(버지니아 노드의 커버리지는 미국 동부 리전입니다)<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td>유럽지역(프랑크푸르트)<br>eu-frankfurt</td>
			<td>프랑크푸르트1존(프랑크푸르트 노드의 커버리지는 유럽 리전입니다)<br>eu-frankfurt-1</td>
		</tr>
		<td >유럽지역(모스크바)<br>eu-moscow</td>
		<td>모스크바 1존(모스크바 노드의 커버리지는 유럽 리전입니다)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## 리전과 가용 영역 선택하기

리전과 가용 영역을 선택 시, 다음의 요소를 고려해야 합니다.
- 클라우드 가상 머신이 위치한 지역, 귀하와 귀하의 클라이언트가 위치한 지리적 위치.
클라우드 가상 머신을 구매 시, 액세스 지연시간을 줄이고 액세스 속도를 위해 클라이언트와 가장 가까운 리전을 선택하시기 바랍니다.
- 클라우드 가상 머신과 기타 클라우드 제품의 관계
기타 클라우드 제품을 선택, 최대한 동일 리전의 동일 가용 영역을 적용하시기 바랍니다. 이 경우에 각 클라우드 제품은 사설 네트워크로 통신하므로 액세스 지연시간을 줄이고 액세스 속도를 올릴 수 있습니다.
- 서비스 고가용성과 장애 복구 고려
VPC가 1개인 솔루션에서도, 가용 영역의 장애를 격리하고 통합 가용 영역에서 장애 복구를 위해 서로 다른 가용 영역에 배포하시기를 추천합니다.
- 가용 영역별로 네트워크 연결이 지연될 수 있습니다. 서비스의 실제 요구사항에 따라 검토해야 하며, 고가용성과 저지연성의 최적화 밸런스 포인트를 찾아야 합니다.
- 다른 나라와 리전의 호스트를 액세스하려면, 다른 나라와 리전의 CVM을 선택하여 액세스하시기 바랍니다. [중국](#MainlandChina)에 CVM을 구축하여 [다른 나라와 리전의 호스트](#InternationalArea)에 액세스할 경우, 액세스 지연이 높아 추천하지 않습니다.

## 리소스 위치 설명
다음은 Tencent Cloud의 글로벌 리소스, 리전과 가용 영역을 구분할 수 없는 리소스, 가용 영역에서 사용하는 리소스를 구분하여 소개합니다.

<table>
	<tr><th>리소스</th><th>리소스 ID 포멧<br><리소스 약자>-여덟자리 숫자 및 문자 부호</th><th>타입</th><th>설명</th></tr>
	<tbody>
	<tr>
	  <td>사용자 계정</td>
	  <td>무제한</td>
	  <td>전 세계에서 유일</td>
	  <td>사용자는 하나의 계정으로 Tencent Cloud의 글로벌 리전별 리소스에 액세스합니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH 보안키</a> </td>
	  <td>skey-xxxxxxxx</td>
	  <td>전체 리전 가용</td>
	  <td>사용자는 SSH 보안키를 사용하여 계정 내 임의 리전의 클라우드 가상 머신을 바인딩 할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">CVM 인스턴스</a> </td>
	  <td>ins-xxxxxxxx</td>
	  <td>개별 리전의 개별 가용 영역에서만 사용합니다.</td>
	  <td>사용자는 지정된 가용 영역에서만 CVM 인스턴스를 구축할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941#custom-images">커스텀 미러</a> </td>
	  <td>img-xxxxxxxx</td>
	  <td>단위 리전의 멀티 가용 영역을 사용합니다.</td>
	  <td>사용자는 인스턴스의 사용자 지정 미러 이미지를 구축하여, 같은 리전의 다른 가용 영역에서 사용할 수 있습니다. 다른 리전에 사용할 경우, 미러 이미지 복사 기능을 활용하여 사용자 지정 미러 이미지를 다른 리전에 복사하시기 바랍니다.</td>
	</tr>
	<tr>
	<td> <a href="http://intl.cloud.tencent.com/document/product/213/5733">EIP</a> </td>
	  <td>eip-xxxxxxxx</td>
	  <td>단위 리전의 멀티 가용 영역을 사용합니다.</td>
	  <td>EIP 주소는 하나의 리전에 구축하며, 동일 리전의 인스턴스만 연동됩니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/12452">보안 그룹</a> </td>
	  <td>sg-xxxxxxxx</td>
	  <td>단위 리전의 멀티 가용 영역을 사용합니다.</td>
	  <td>보안 그룹은 하나의 리전에 구축하며, 동일 리전의 인스턴스만 연동됩니다. Tencent Cloud는 자동으로 사용자에게 3개의 기본 보안 그룹을 구축합니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362">클라우드 디스크</a> </td>
	  <td>disk-xxxxxxxx</td>
	  <td>개별 리전의 개별 가용 영역에서만 사용합니다.</td>
	  <td>사용자는 지정된 가용 영역에만 클라우드 블록 스토리지를 구축하며, 동일 가용 영역의 인스턴스에 마운트해야 합니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362/2345">스냅숏</a> </td>
	  <td>snap-xxxxxxxx</td>
	  <td>단위 리전의 멀티 가용 영역을 사용합니다.</td>
	  <td>클라우드 디스크에 스냅샷을 구축하면, 사용자는 해당 리전에서 이 스냅샷을 이용하여 다른 조작을 진행합니다(예를 들면 클라우드 디스크를 구축합니다).</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/214/524">로드 밸런서</a> </td>
	  <td>clb-xxxxxxxx</td>
	  <td>단위 리전의 멀티 가용 영역을 사용합니다.</td>
	  <td>로드 밸런서는 단일 리전 멀티 가용 영역의 CVM을 바인딩하여 트래픽을 전달합니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">프라이빗 네트워크</a> </td>
	  <td>vpc-xxxxxxxx</td>
	  <td>단위 리전의 멀티 가용 영역을 사용합니다.</td>
	  <td>한 리전에 사설 네트워크를 구축하면, 다른 가용 영역에 동일 사설 네트워크 리소스를 구축할 수 있습니다. </td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">서브넷</a> </td>
	  <td>subnet-xxxxxxxx</td>
	  <td>개별 리전의 개별 가용 영역에서만 사용합니다.</td>
	  <td>사용자는 통합 가용 영역에서 서브넷 구축이 불가능합니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/4954">라우팅 테이블</a> </td>
	  <td>rtb-xxxxxxxx</td>
	  <td>단위 리전의 멀티 가용 영역을 사용합니다.</td>
	  <td>사용자가 라우팅 테이블을 구축 시 특정 사설 네트워크를 지정해야 하고 사설 네트워크의 위치 속성을 따릅니다.</td>
	</tr>
	</tbody>
</table>


## 조작

### 인스턴스를 기타 가용 영역에 마이그레이션합니다.

기존에 실행한 인스턴스는 가용 영역을 변경 불가능하지만 사용자는 다른 방법으로 인스턴스를 기타 가용 영역에 마이그레이션 할 수 있습니다. 마이그레이션 프로세스는 오리지널 인스턴스가 사용자 지정 미러 이미지를 구축, 사용자 지정 미러 이미지를 이용하여 신규 가용 영역에서 인스턴스를 실행 및 신규 인스턴스 사양을 업데이트하는 등 작업을 포함합니다.
1. 기존 인스턴스의 사용자 지정 미러 이미지를 구축합니다. 자세한 내용은 [사용자 정의 미러 구축](http://intl.cloud.tencent.com/document/product/213/4942)을 참조하시기 바랍니다.
2. 기존 인스턴스의 네트워크 환경은 [사설 네트워크](http://intl.cloud.tencent.com/document/product/213/5227)이며, 마이그레이션 후 기존의 사설 네트워크 IP 주소를 유지해야 할 경우, 사용자는 기존 가용 영역의 서브넷을 삭제하고, 신규 가용 영역에서 기존 서브넷과 같은 IP 주소 범위에 서브넷을 생성할 수 있습니다. 참고로, 가용 인스턴스를 포함하지 않은 서브넷만 삭제할 수 있습니다. 기존 서브넷의 전체 인스턴스를 신규 서브넷에 마이그레이션해야 합니다.
3. 신규 생성한 사용자 지정 미러 이미지를 이용하여 신규 가용 영역에 신규 인스턴스를 구축합니다. 사용자는 기존 인스턴스와 같은 유형, 사양을 선택하거나, 신규 인스턴스의 유형과 사양을 선택할 수 있습니다. 자세한 내용은 [인스턴스 구매 및 실행](http://intl.cloud.tencent.com/document/product/213/4855)을 참조하시기 바랍니다.
4. 기존 인스턴스에 EIP 주소를 연동하였을 경우, 기존 인스턴스의 연결을 해제하고 신규 인스턴스와 연동합니다. 자세한 내용은 [EIP](http://intl.cloud.tencent.com/document/product/213/5733)를 참조하시기 바랍니다.
5. (옵션)기존 인스턴스는 [종량 요금제](http://intl.cloud.tencent.com/document/product/213/2180)를 적용할 경우, 기존 인스턴스를 삭제할 수 있습니다. 자세한 내용은 [인스턴스 삭제 ](http://intl.cloud.tencent.com/document/product/213/4930)를 참조하시기 바랍니다.

### 미러 이미지를 다른 리전에 복사합니다.

사용자가 인스턴스를 시작, 조회하는 등 액션은 리전 속성을 구분합니다. 사용자가 실행하려는 인스턴스 미러 이미지가 로컬에 존재하지 않을 경우, 미러 이미지를 로컬에 복사해야 합니다. 자세한 내용은 [미러 이미지 복사](http://intl.cloud.tencent.com/document/product/213/4943)를 참조하시기 바랍니다.
