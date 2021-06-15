## 리전

### 소개

리전(Region)은 물리적인 데이터센터를 말합니다. Tencent Cloud는 리전 간의 완벽한 격리를 통해 각 리전의 안정성과 내고장성을 최대한으로 보장합니다. 액세스 딜레이 시간을 줄이고 다운로드 속도를 높이기 위해 가장 가까운 리전을 선택하는 것을 권장합니다.

아래 테이블 또는 API 인터페이스 [리전 리스트 조회](https://intl.cloud.tencent.com/document/product/213/15708)를 통해 리전 전체 리스트를 확인할 수 있습니다.

### 관련 특징

- 각 리전 간 네트워크는 완벽히 격리됩니다. 리전 간 클라우드 서비스는 **기본적으로 내부 네트워크를 통해 통신할 수 없습니다**.
- 리전 간 클라우드 서비스는 [공용 IP](https://intl.cloud.tencent.com/document/product/213/5224)를 통해 Internet에 액세스하는 방식으로 통신할 수 있습니다. 각 VPC의 클라우드 서비스는 빠르고 안정적인 [CCN](https://intl.cloud.tencent.com/document/product/1003)을 통해 통신합니다.
- [CLB](https://intl.cloud.tencent.com/document/product/214)는 현재 기본적으로 리전 내 트래픽 전달과 로컬 리전 CVM 바인딩을 지원합니다. [리전 간 바인딩](https://intl.cloud.tencent.com/document/product/214/12014) 기능을 활성화하면 CLB의 리전 간 CVM 바인딩이 지원됩니다.

## 가용존

### 소개

가용존(Zone)은 Tencent Cloud가 동일 리전에서 전력과 네트워크가 상호 독립적으로 운영되는 물리적 데이터센터입니다. 가용존의 장애를 서로 격리(대규모 재해 또는 전력 장애 제외)하여 장애의 확산 방지를 지원함으로써 사용자는 끊김 없이 온라인 서비스를 이용할 수 있습니다. 독립 가용존 내의 인스턴스를 실행하면 사용자의 응용 프로그램이 특정 위치에 발생한 장애의 영향을 받지 않습니다.
API 인터페이스의 [가용존 리스트 조회](https://intl.cloud.tencent.com/document/product/213/35071)에서 가용존 전체 리스트를 확인할 수 있습니다.

### 관련 특징

동일 리전 내 다른 가용존에 있더라도 같은 VPC의 클라우드 서비스는 서로 내부 네트워크로 통신하며 [내부 IP](https://intl.cloud.tencent.com/document/product/213/5225)를 사용하여 액세스할 수 있습니다.
>?내부 네트워크 통신은 동일 계정 내 리소스 통신으로, 다른 계정의 리소스 내부 네트워크와 완벽히 격리됩니다.
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
		<td rowspan="5">화난지역(광저우)<br> ap-guangzhou</td>
		<td>광저우 1존(품절)<br> ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>광저우 2존(품절)<br> ap-guangzhou-2</td>
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
		<td rowspan="5">화둥지역(상하이)<br>ap-shanghai</td>
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
			<td rowspan="2">화둥지역(난징)<br>ap-nanjing</td>
			<td>난징 1존<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>난징 2존<br>ap-nanjing-2</td>
	</tr>
	<tr>
			<td rowspan="7">화베이지역(베이징)<br>ap-beijing</td>
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
			<td>베이징 6존<br>ap-beijing-6</td>
	</tr>
	<tr>
			<td>베이징 7존<br>ap-beijing-7</td>
	</tr>
	<tr>
		<td rowspan="2">시난지역(청두)<br>ap-chengdu</td>
		<td>청두 1존<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>청두 2존<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >시난지역(충칭)<br>ap-chongqing</td>
			<td>충칭 1존<br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="3">중국 홍콩/마카오/대만 지역(중국 홍콩)<br>ap-hongkong</td>
			<td>중국 홍콩 1존(중국 홍콩 노드로 중국 홍콩/마카오/대만 지역 커버 가능)<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>중국 홍콩 2존(중국 홍콩 노드로 중국 홍콩/마카오/대만 지역 커버 가능)<br>ap-hongkong-2</td>
	</tr>
	<tr>
			<td>중국 홍콩 3존(중국 홍콩 노드로 중국 홍콩/마카오/대만 지역 커버 가능)<br>ap-hongkong-3</td>
	</tr>
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
			<td  rowspan="3">아시아 태평양 동남부(싱가포르)<br>ap-singapore</td>
			<td>싱가포르 1존(싱가포르 노드로 아시아 태평양 동남부 지역 커버 가능)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>싱가포르 2존(싱가포르 노드로 아시아 태평양 동남부 지역 커버 가능)<br>ap-singapore-2</td>
		</tr>
		<tr>
			<td>싱가포르 3존(싱가포르 노드로 아시아 태평양 동남부 지역 커버 가능)<br>ap-singapore-3</td>
		</tr>
		<tr>
			<td>아시아 태평양 동남부(자카르타)<br>ap-jakarta</td>
			<td>자카르타 1존(자카르타 노드로 아시아 태평양 동남부 지역 커버 가능)<br>ap-jakarta-1</td>
		</tr>
		<tr>
			<td  rowspan="2">아시아 태평양 동북부(서울)<br>ap-seoul</td>
			<td>서울 1존(서울 노드로 아시아 태평양 동북부 지역 커버 가능)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>서울 2존(서울 노드로 아시아 태평양 동북부 지역 커버 가능)<br>ap-seoul-2</td>
		</tr>
		<tr>
			<td rowspan="2">아시아 태평양 동북부(도쿄)<br>ap-tokyo</td>
			<td>도쿄 1존(도쿄 노드 가용존으로 아시아 태평양 동북부 지역 커버 가능)<br>ap-tokyo-1</td>
		</tr>
		<tr>
			<td>도쿄 2존(도쿄 노드 가용존으로 아시아 태평양 동북부 지역 커버 가능)<br>ap-tokyo-2</td>
		</tr>
       <tr>
			<td  rowspan="2">아시아 태평양 남부(뭄바이)<br>ap-mumbai</td>
			<td>뭄바이 1존(뭄바이 노드로 아시아 태평양 남부 지역 커버 가능)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>뭄바이 2존(뭄바이 노드로 아시아 태평양 남부 지역 커버 가능)<br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td >아시아 태평양 동남부(방콕)<br>ap-bangkok </td>
				 <td >방콕 1존(방콕 노드로 아시아 태평양 동남부 지역 커버 가능)<br>ap-bangkok-1</td>
		<tr>
			<td>북미 지역(토론토)<br>na-toronto</td>
			<td>토론토 1존(토론토 노드로 북미 지역 커버 가능)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">미국 서부 지역(실리콘밸리)<br>na-siliconvalley</td>
			<td>실리콘밸리 1존(실리콘밸리 노드로 미국 서부 지역 커버 가능)<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>실리콘밸리 2존(실리콘밸리 노드로 미국 서부 지역 커버 가능)<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">미국 동부(버지니아)<br>na-ashburn</td>
			<td>버지니아 1존(버지니아 노드로 미국 동부 지역 커버 가능)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>버지니아 2존(버지니아 노드로 미국 동부 지역 커버 가능)<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td>유럽 지역(프랑크푸르트)<br>eu-frankfurt</td>
			<td>프랑크푸르트 1존(프랑크푸르트 노드로 유럽 지역 커버 가능)<br>eu-frankfurt-1</td>
		</tr>
		<td >유럽 지역(모스크바)<br>eu-moscow</td>
		<td>모스크바 1존(모스크바 노드로 유럽 지역 커버 가능)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## 리전 및 가용존 선택하기

리전 및 가용존 선택 시 다음 요소를 고려해야 합니다.
- CVM이 속한 리전이나 사용자 및 타깃 사용자의 지리적 위치
CVM 구매 시 액세스 딜레이 시간을 줄이고 액세스 속도를 높이기 위해 클라이언트와 가장 가까운 리전을 선택하는 것이 좋습니다.
- CVM과 기타 클라우드 서비스와의 관계
기타 클라우드 서비스 선택 시 최대한 동일 리전, 동일 가용존 선택을 권장합니다. 클라우드 서비스 간 내부 네트워크를 통한 통신으로 딜레이 시간을 줄이고 액세스 속도를 높일 수 있습니다.
- 비즈니스의 높은 가용성 및 재해 복구
VPC 시나리오가 한 개뿐이어도 가용존 간 장애 격리를 통한 재해 복구가 가능하도록 비즈니스를 서로 다른 가용존에 배포할 것을 권장합니다.
- 가용존 간 네트워크 통신이 딜레이될 수 있습니다. 실제 비즈니스 요구사항을 고려한 평가를 통해 높은 가용성과 낮은 딜레이 시간 사이에서 최적의 균형점을 찾아야 합니다.
- 기타 국가 및 지역의 호스트에 액세스하려면 해당 국가의 CVM을 선택하여 액세스하는 것이 좋습니다. [중국](#MainlandChina)에 CVM을 생성하여 [기타 국가 및 지역의 호스트](#InternationalArea)에 액세스할 경우 딜레이 시간이 길어질 수 있어 권장하지 않습니다.

##리소스 위치 설명
Tencent Cloud의 리소스 중 글로벌 리소스, 리전은 구분하지만 가용존은 구분하지 않는 리소스, 가용존 기반의 리소스를 소개합니다.

<table>
	<tr><th>리소스</th><th>리소스 ID 포맷<br><리소스 약자>-8자리 숫자 및 부호</th><th>유형</th><th>설명</th></tr>
	<tbody>
	<tr>
	  <td>사용자 계정</td>
	  <td>무제한</td>
	  <td>전 세계 유일</td>
	  <td>사용자는 동일한 계정으로 세계 각지의 Tencent Cloud 리소스에 액세스할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH 키</a> </td>
	  <td>skey-xxxxxxxx</td>
	  <td>모든 리전 사용 가능</td>
	  <td>사용자는 SSH 키를 사용하여 계정 내 임의 리전의 CVM을 바인딩할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">CVM 인스턴스</a> </td>
	  <td>ins-xxxxxxxx</td>
	  <td>단일 리전의 단일 가용존에서만 사용 가능</td>
	  <td>사용자는 특정 가용존에서만 CVM 인스턴스를 생성할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941?from_cn_redirect=1">사용자 정의 이미지</a> </td>
	  <td>img-xxxxxxxx</td>
	  <td>단일 리전 다중 가용존 사용 가능</td>
	  <td>사용자는 인스턴스 사용자 정의 이미지를 생성할 수 있고, 동일 리전 내 다른 가용존에서도 사용할 수 있습니다. 다른 리전에서 사용해야 할 경우 이미지 복사 기능을 사용해 사용자 정의 이미지를 해당 리전으로 복사하십시오.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a> </td>
	  <td>eip-xxxxxxxx</td>
	  <td>단일 리전 다중 가용존 사용 가능</td>
	  <td>EIP 주소는 하나의 리전에 생성되며, 동일 리전의 인스턴스끼리만 연결할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/12452?from_cn_redirect=1">보안 그룹</a> </td>
	  <td>sg-xxxxxxxx</td>
	  <td>단일 리전 다중 가용존 사용 가능</td>
	  <td>보안 그룹은 하나의 리전에 생성되며, 동일 리전의 인스턴스끼리만 연결할 수 있습니다. Tencent Cloud는 사용자를 위해 기본적으로 보안 그룹 3개를 자동 생성합니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362">CBS</a> </td>
	  <td>disk-xxxxxxxx</td>
	  <td>단일 리전의 단일 가용존에서만 사용 가능</td>
	  <td>사용자는 특정 가용존에서만 CBS를 생성하고, 동일 가용존 내 인스턴스에만 마운트할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362/31638">스냅샷</a> </td>
	  <td>snap-xxxxxxxx</td>
	  <td>단일 리전 다중 가용존 사용 가능</td>
	  <td>CBS에 스냅샷을 생성하면, 사용자가 해당 리전에서 이 스냅샷을 이용하여 다른 작업을 진행할 수 있습니다(예: CBS 생성).</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/214/524?from_cn_redirect=1">CLB</a> </td>
	  <td>clb-xxxxxxxx</td>
	  <td>단일 리전 다중 가용존 사용 가능</td>
	  <td>CLB는 단일 리전 내 서로 다른 가용존의 CVM을 바인딩하여 트래픽을 전달할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">VPC</a> </td>
	  <td>vpc-xxxxxxxx</td>
	  <td>단일 리전 다중 가용존 사용 가능</td>
	  <td>한 리전에 VPC를 구축하면 다른 가용존에서도 동일한 VPC에 속하는 리소스를 생성할 수 있습니다.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535#.E5.AD.90.E7.BD.91">서브넷</a> </td>
	  <td>subnet-xxxxxxxx</td>
	  <td>단일 리전의 단일 가용존에서만 사용 가능</td>
	  <td>사용자는 가용존 간 서브넷을 생성할 수 없습니다.</td>
	</tr>
	<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/215/31810">라우팅 테이블</a> </td>
	  <td> rtb-xxxxxxxx</td>
	  <td>단일 리전 다중 가용존 사용 가능</td>
	  <td>라우팅 테이블 생성 시 특정 VPC를 지정해야 하므로 VPC의 위치 속성을 따릅니다.</td>
	</tr>
	</tbody>
</table>


## 관련 작업

### 다른 가용존에 인스턴스 마이그레이션

이미 실행 중인 인스턴스의 가용존은 변경할 수 없지만, 다른 방법으로 인스턴스를 다른 가용존에 마이그레이션할 수는 있습니다. 마이그레이션 과정에는 기존 인스턴스에서 사용자 정의 이미지 생성, 생성한 이미지를 사용해 새로운 가용존에서 인스턴스 실행, 신규 인스턴스 설정 업데이트 작업이 포함됩니다.
1. 현재 인스턴스의 사용자 정의 이미지를 생성합니다. 자세한 내용은 [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942)을 참조하십시오.
2. 현재 인스턴스의 네트워크 환경이 [VPC](https://intl.cloud.tencent.com/document/product/213/5227)이고 마이그레이션 후에도 현재의 개인 IP 주소를 유지하려면, 먼저 현재 가용존의 서브넷을 삭제하고 새로운 가용존에서 기존 서브넷과 동일한 IP 주소 범위의 서브넷을 생성할 수 있습니다. 가용 인스턴스를 포함하지 않은 서브넷만 삭제할 수 있으므로, 기존 서브넷에 있는 인스턴스는 모두 신규 서브넷으로 옮겨야 합니다.
3. 방금 생성한 사용자 정의 이미지를 사용해 새로운 가용존에서 신규 인스턴스를 생성합니다. 기존 인스턴스와 동일한 유형과 설정을 선택할 수 있고, 신규 인스턴스의 유형과 설정도 선택할 수 있습니다. 자세한 내용은 [인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참조하십시오.
4. 기존 인스턴스에 EIP 주소가 연결된 경우, 연결을 해제하고 신규 인스턴스와 연결합니다. 자세한 내용은 [EIP](https://intl.cloud.tencent.com/document/product/213/5733)를 참조하십시오.
5. (옵션)기존 인스턴스가 [종량제](https://intl.cloud.tencent.com/document/product/213/2180) 유형일 경우 기존 인스턴스를 폐기할 수 있습니다. 자세한 내용은 [인스턴스 폐기](https://intl.cloud.tencent.com/document/product/213/4930)를 참조하십시오.

### 다른 리전에 이미지 복사

사용자의 인스턴스 실행 및 조회 등은 모두 리전 속성에 따라 구분됩니다. 실행해야 할 인스턴스 이미지가 로컬 리전에 존재하지 않을 경우, 이미지를 로컬 리전으로 복사해야 합니다. 자세한 내용은 [이미지 복사](https://intl.cloud.tencent.com/document/product/213/4943)를 참조하십시오.
