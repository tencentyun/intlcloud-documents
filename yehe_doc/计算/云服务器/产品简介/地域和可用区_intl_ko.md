## 리전

### 소개

리전(Region)은 물리적 데이터센터의 지리적 위치입니다. Tencent Cloud는 리전별로 철저히 격리되므로, 리전별 안정성과 내고장성을 최대한 보장합니다. 액세스 딜레이 시간을 단축하고 다운로드 속도를 상승시키려면 클라이언트와 가장 가까운 리전을 선택하시기 바랍니다.

다음의 표를 참고하거나 API [리전 목록 조회](https://intl.cloud.tencent.com/document/product/213/15708)에서 정확한 리전 목록을 조회하시기 바랍니다.

### 관련 특징

- 다른 리전 간의 네트워크는 완벽히 격리됩니다. 리전별 클라우드 서비스는 **기본적으로 내부 네트워크를 통해 통신할 수 없습니다.**
- 다른 리전 간의 클라우드 서비스는 [공인 IP](https://intl.cloud.tencent.com/document/product/213/5224)를 통해 Internet에 액세스하는 방식으로 통신합니다. 다른 VPC 간의 클라우드 서비스는 [CCN](https://intl.cloud.tencent.com/document/product/1003)을 통해 통신하며, 이러한 통신 방식은 상대적으로 안정적이며 속도 또한 빠릅니다.
- [Cloud Load Balacer(CLB)](https://intl.cloud.tencent.com/document/product/214)는 현재 기본적으로 리전 내 트래픽 전달과 로컬 리전 CVM과의 바인딩을 지원합니다. [리전 간 바인딩](https://intl.cloud.tencent.com/document/product/214/12014) 기능을 활성화하면 CLB로 CVM의 리전 간 바인딩을 지원합니다.

## 가용존

### 소개

가용존(Zone)은 동일 리전의 Tencent Cloud에 서로 독립적인 전력 및 네트워크가 적용되는 물리적인 데이터센터입니다. 가용존의 장애를 서로 격리시켜(대형 재난 혹은 대규모 전력 장애 제외) 장애가 확산되지 않고, 사용자의 비즈니스가 온라인에서 지속되는 것을 목표로 하고 있습니다. 독립적인 가용존의 인스턴스를 실행하면 사용자의 응용 프로그램은 단일 위치 장애의 영향을 받지 않습니다.
API [가용존 리스트 조회](https://intl.cloud.tencent.com/document/product/213/35071)를 통해 정확한 가용존 리스트를 조회하실 수 있습니다.

### 관련 특징

동일한 리전 내의 다른 가용존에 있을 경우, 동일한 VPC의 클라우드 서비스끼리는 내부 네트워크로 통신하며, [개인 IP](https://intl.cloud.tencent.com/document/product/213/5225)를 사용하여 직접 액세스할 수 있습니다.
>내부 네트워크 통신은 동일한 계정의 리소스 통신을 의미하며, 서로 다른 계정에 있는 리소스의 내부 네트워크는 완벽히 격리되어 있습니다.
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
		<td rowspan="5">화남 지역(광저우)<br> ap-guangzhou</td>
		<td>광저우 1존(품절)<br> ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>광저우 2존(품절)<br> ap-guangzhou-1</td>
	</tr>
	<tr>
		<td>광저우 3존<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>광저우 4존<br> ap-guangzhou-4</td>
	</tr>
	<tr>
		<td>광저우 6존<br> ap-guangzhou-6</td>
	</tr>
		<td rowspan="5">화동 지역(상하이)<br>ap-shanghai</td>
		<td>상하이 1존<br>ap-shanghai-1</td>
	</tr>
	<tr>
		<td>상하이 2존<br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>상하이 3존<br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>상하이 4존<br>ap-shanghai-4</td>
	</tr>
        <tr>
		<td>상하이 5존<br>ap-shanghai-5</td>
	</tr>
		<tr>
			<td rowspan="2">화동 지역(난징)<br>ap-beijing</td>
			<td>난징 1존<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>난징 2존<br>ap-nanjing-2</td>
	</tr>
	<tr>
			<td rowspan="5">화북 지역(베이징)<br>ap-beijing</td>
			<td>베이징 1존<br>ap-beijing-1</td>
	</tr>
	<tr>
			<td>베이징 2존<br>ap-beijing-2</td>
	</tr>
	<tr>
			<td>베이징 3존<br>ap-beijing-3</td>
	</tr>
	<tr>
			<td>베이징 4존<br>ap-beijing-4</td>
	</tr>
	<tr>
			<td>베이징 5존<br>ap-beijing-5</td>
	</tr>
	<tr>
		<td rowspan="2">서남 지역(청두)<br>ap-chengdu</td>
		<td>청두 1존<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>청두 2존<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >서남 지역(충칭)<br>ap-chongqing</td>
			<td>충칭 1존<br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="2">중국홍콩, 마카오, 대만 지역(중국홍콩)<br>ap-hongkong</td>
			<td>중국홍콩 1존(중국 홍콩 노드로 홍콩/마카오/대만 리전 커버 가능)<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>중국홍콩 2존(중국 홍콩 노드로 홍콩/마카오/대만 리전 커버 가능)<br>ap-hongkong-2</td>
	</tr>
</tbody>
</table>	

<span id="InternationalArea"></span>

## 기타 국가와 지역	
<table class="table-striped">
	<tbody>
	<tr>
			<th>리전</th>
			<th>가용존</th>
		</tr>
		<tr>
			<td  rowspan="2">아시아 태평양 동남부(싱가포르)<br>ap-singapore</td>
			<td>싱가포르 1존(싱가포르 노드로 아시아 태평양 동남부 리전 커버 가능)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>싱가포르 2존(싱가포르 노드로 아시아 태평양 동남부 리전 커버 가능)<br>ap-singapore-2</td>
		</tr>
		<tr>
			<td >아시아 태평양 동북부(서울)<br>ap-seoul</td>
			<td>서울 1존(서울 노드로 아시아 태평양 동북부 리전 커버 가능)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td >아시아 태평양 동북부(도쿄)<br>ap-tokyo</td>
			<td>도쿄 1존(도쿄 노드 가용존은 아시아 태평양 동북부 리전을 커버)<br>ap-tokyo-1</td>
		</tr>
       <tr>
			<td  rowspan="2">아시아 태평양 남부(뭄바이)<br>ap-mumbai</td>
			<td>뭄바이 1존(뭄바이 노드로 아시아 태평양 남부 리전 커버 가능)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>뭄바이 2존(뭄바이 노드로 아시아 태평양 남부 리전 커버 가능)<br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td >아시아 태평양 동남부(방콕)<br>ap-bangkok </td>
				 <td >방콕 1존(방콕 노드로 아시아 태평양 동남부 리전 커버 가능)<br>ap-bangkok-1</td>
		<tr>
			<td>북미 지역(토론토)<br>na-toronto</td>
			<td>토론토 1존(토론토 노드로 북미 지역 커버 가능)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">미국 서부(실리콘밸리)<br>na-siliconvalley</td>
			<td>실리콘밸리 1존(실리콘밸리 노드로 미국 서부 리전 커버 가능)<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>실리콘밸리 2존(실리콘밸리 노드로 미국 서부 리전 커버 가능)<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">미국 동부(버지니아주)<br>na-ashburn</td>
			<td>버지니아 1존(버지니아주 노드로 미국 동부 리전 커버 가능)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>버지니아 2존(버지니아주 노드로 미국 동부 리전 커버 가능)<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td>유럽 지역(프랑크푸르트)<br>eu-frankfurt</td>
			<td>프랑크푸르트 1존(프랑크푸르트 노드로 유럽 리전 커버 가능)<br>eu-frankfurt-1</td>
		</tr>
		<td >유럽 지역(모스크바)<br>eu-moscow</td>
		<td>모스크바 1존(모스크바 노드 가용존은 유럽 리전을 커버)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## 리전 및 가용존 선택 요령

리전 및 가용존을 선택할 때 다음의 요소를 고려해야 합니다.
- CVM이 위치한 리전과 본인 및 타깃 사용자의 지리적 위치.
CVM을 구매할 경우 액세스 딜레이 시간을 단축하고 액세스 속도를 높이기 위해 클라이언트와 가장 가까운 리전을 선택하시길 권장합니다.
- CVM 및 기타 클라우드 서비스의 관계.
기타 클라우드 서비스는 최대한 동일 리전, 동일 가용존의 서비스로 선택하시길 권장합니다. 내부 네트워크로 각 클라우드 서비스 간의 통신이 가능해지면 액세스 딜레이 시간이 줄어들고 액세스 속도가 향상됩니다.
- 비즈니스의 고가용성 및 재해 복구 고려.
시나리오의 VPC가 한 개뿐이더라도, 가용존끼리의 장애를 격리하여 가용존 간 재해 복구를 원활히 진행하기 위해, 비즈니스를 서로 다른 가용존에 배포하시기를 권장합니다.
- 다른 가용존 간에 네트워크 통신 딜레이가 발생할 수 있습니다. 비즈니스의 실제 요구에 따라 검토를 진행하여, 높은 가용성과 낮은 딜레이 사이에서 최적의 밸런스 포인트를 찾아야 합니다.
- 다른 국가 및 리전의 호스트에 액세스하려면, 다른 국가 및 리전의 CVM을 선택하여 액세스하시기 바랍니다. 만약 [중국](#MainlandChina)에서 CVM을 생성했다면, [다른 국가 및 리전의 호스트](#InternationalArea)로 액세스하는 것은 비교적 큰 딜레이가 발생할 수 있으므로 권장하지 않습니다.

## 리소스 위치 설명
이곳에서는 Tencent Cloud의 글로벌 리소스, 가용존이 아닌 리전으로 구분되는 리소스 및 가용존 기반 리소스에 대해 설명합니다.

<table>
	<tr><th>리소스</th><th>리소스 ID 형식<br><리소스 약어>-8자리 숫자 및 문자 부호</th><th>유형</th><th>설명</th></tr>
	<tbody>
	<tr>
	  <td>사용자 계정</td>
	  <td>무제한</td>
	  <td>전 세계 유일</td>
	  <td>사용자는 하나의 계정으로 Tencent Cloud의 글로벌 각지의 리소스에 액세스할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH 키</a> </td>
	  <td>skey-xxxxxxxx</td>
	  <td>전체 리전 사용 가능</td>
	  <td>SSH 키를 사용하여 계정 내 임의 리전의 CVM에 바인딩할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">CVM 인스턴스</a> </td>
	  <td>ins-xxxxxxxx</td>
	  <td>단일 리전의 단일 가용존에서만 사용 가능</td>
	  <td>특정 가용존에서만 CVM 인스턴스를 생성할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941?from_cn_redirect=1">사용자 정의 이미지</a> </td>
	  <td>img-xxxxxxxx</td>
	  <td>단일 리전의 여러 가용존에서 사용 가능</td>
	  <td>인스턴스의 사용자 정의 이미지를 생성하여, 동일한 리전 내의 다른 가용존에서 사용할 수 있습니다. 다른 리전에 사용할 경우, 이미지 복제 기능을 이용하여 사용자 정의 이미지를 다른 리전에 복사하시기 바랍니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a> </td>
	  <td>eip-xxxxxxxx</td>
	  <td>단일 리전의 여러 가용존에서 사용 가능</td>
	  <td>EIP 주소는 하나의 리전에 생성되며, 동일 리전의 인스턴스끼리만 연결할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <https://intl.cloud.tencent.com/document/product/213/12452?from_cn_redirect=1">보안 그룹</a> </td>
	  <td>sg-xxxxxxxx</td>
	  <td>단일 리전의 여러 가용존에서 사용 가능</td>
	  <td>보안 그룹은 하나의 리전에 생성되며, 동일 리전의 인스턴스끼리만 연결할 수 있습니다. Tencent Cloud는 3개의 기본 보안 그룹을 자동 생성합니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362">CBS</a> </td>
	  <td>disk-xxxxxxxx</td>
	  <td>단일 리전의 단일 가용존에서만 사용 가능</td>
	  <td>특정 가용존에만 CBS를 생성할 수 있으며, 동일한 가용존의 인스턴스에 마운트해야 합니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362/31638">스냅샷</a> </td>
	  <td>snap-xxxxxxxx</td>
	  <td>단일 리전의 여러 가용존에서 사용 가능</td>
	  <td>특정 CBS에 스냅샷을 생성하면, 사용자는 해당 리전에서 스냅샷을 사용하여 다른 작업을 진행할 수 있습니다(예: CBS 생성 등).</td>
	</tr>
	<tr>
	<td> <https://intl.cloud.tencent.com/document/product/214/524?from_cn_redirect=1">CLB</a> </td>
	  <td>clb-xxxxxxxx</td>
	  <td>단일 리전의 여러 가용존에서 사용 가능</td>
	  <td>CLB는 단일 리전 내 다른 가용존의 CVM을 바인딩하여 트래픽을 전달할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">VPC</a> </td>
	  <td>vpc-xxxxxxxx</td>
	  <td>단일 리전의 여러 가용존에서 사용 가능</td>
	  <td>한 리전에 VPC를 생성하면 다른 가용존에도 동일한 VPC 리소스를 생성할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535#.E5.AD.90.E7.BD.91">서브넷</a> </td>
	  <td>subnet-xxxxxxxx</td>
	  <td>단일 리전의 단일 가용존에서만 사용 가능</td>
	  <td>가용존 간의 서브넷 생성은 불가능합니다.</td>
	</tr>
	<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/215/31810"> 라우팅 테이블</a> </td>
	  <td> rtb-xxxxxxxx</td>
	  <td>단일 리전의 여러 가용존에서 사용 가능</td>
	  <td>라우팅 테이블을 생성할 때는 VPC의 위치 속성에 따라 특정 VPC를 지정해야 합니다.</td>
	</tr>
	</tbody>
</table>


## 관련 작업

### 인스턴스를 다른 가용존에 마이그레이션

이미 실행 중인 인스턴스의 가용존은 변경할 수 없지만, 다음의 방법을 통해 인스턴스를 다른 가용존에 마이그레이션할 수는 있습니다. 마이그레이션 프로세스는 기존 인스턴스에서의 사용자 정의 이미지 생성, 사용자 정의 이미지를 사용한 새로운 가용존에서의 인스턴스 실행, 신규 인스턴스 구성 업데이트 등의 과정을 포함합니다.
1. 현재 사용 중인 인스턴스의 사용자 정의 이미지를 생성합니다. 자세한 내용은 [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942)을 참조 바랍니다.
2. 사용 중인 인스턴스의 네트워크 환경이 [VPC](https://intl.cloud.tencent.com/document/product/213/5227)이고, 마이그레이션 후에도 현재의 개인 IP 주소를 유지하고 싶다면, 먼저 현 사용 가용존의 서브넷을 삭제한 다음 새로운 가용존에서 기존 서브넷과 동일한 IP 주소 범위의 서브넷을 생성합니다. 가용 인스턴스에 포함되지 않는 서브넷만 삭제할 수 있으므로, 기존 서브넷에 있는 인스턴스는 모두 새로운 서브넷으로 이동시켜야 합니다.
3. 미리 생성해 놓은 사용자 정의 이미지를 사용하여 새로운 가용존에서 신규 인스턴스를 생성합니다. 사용자는 기존의 인스턴스와 같은 유형 및 구성을 선택하거나, 새로운 인스턴스 유형 및 구성을 선택할 수 있습니다. 자세한 내용은 [인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참조 바랍니다.
4. 기존 인스턴스에 EIP 주소가 연결되어 있다면, 이전 인스턴스와의 연결을 해제하고 새로운 인스턴스와 연결합니다. 자세한 내용은 [EIP](https://intl.cloud.tencent.com/document/product/213/5733)를 참조 바랍니다.
5. (선택) 기존 인스턴스가 [종량제](http://intl.cloud.tencent.com/document/product/213/2180) 유형일 경우, 기존 인스턴스를 폐기할 수 있습니다. 자세한 내용은 [인스턴스 폐기](http://intl.cloud.tencent.com/document/product/213/4930)를 참조 바랍니다.

### 이미지를 다른 리전에 복사

인스턴스 실행, 조회 등의 동작은 모두 리전 속성으로 구분됩니다. 만약 인스턴스 실행에 필요한 이미지가 로컬 리전에 존재하지 않을 경우, 이미지를 로컬 리전으로 복사해 와야 합니다. 더 자세한 정보는 [이미지 복사](https://intl.cloud.tencent.com/document/product/213/4943)를 참조 바랍니다.
