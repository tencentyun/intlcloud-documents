Tencent CDB 호스팅 데이터 센터는 전세계 여러 장소에 분포해 있으며, 이러한 장소의 노드를 리전(Region)이라고 하고, 각 리전은 여러 개의 가용존(Zone)으로 구성됩니다.
모든 리전(Region)은 독립된 지리적 구역입니다. 리전마다 여러 개의 상호 격리된 위치가 있는데 이를 가용존(Zone)이라고 합니다. 모든 가용존은 독립적이지만, 동일한 리전의 가용존은 딜레이 시간이 짧은 내부 네트워크 링크로 연결됩니다. Tencent Cloud는 사용자가 다른 위치에 클라우드 리소스를 할당하도록 지원하며, 사용자가 시스템을 설계할 때 리소스를 다른 가용존에 배치하여 단일 지점의 장애로 서버를 사용할 수 없는 상황을 방지할 것을 권장합니다.

리전, 가용존의 이름은 데이터 센터의 커버리지 범위를 가장 직접적으로 나타냅니다. 고객의 이해를 돕기 위한 이름 생성 규칙은 다음과 같습니다.
- 리전 이름은 [커버리지 범위+데이터 센터의 소재 도시]로 구성됩니다. 앞부분은 해당 데이터 센터의 커버리지 능력이고, 뒷부분은 해당 데이터 센터의 소재 도시 또는 인근 도시입니다.
- 가용존 이름은 [도시+번호]로 구성됩니다.

## 리전
Tencent Cloud는 각 리전을 완전히 격리하여 리전 간의 안정성과 내고장성을 최대한 보장합니다. 액세스 딜레이 시간을 줄이고, 다운로드 속도를 향상시키기 위해서는 사용자로부터 가장 가까운 리전을 선택할 것을 권장합니다. 사용자가 인스턴스를 실행하거나 조회 등을 할 때 모두 리전 속성을 구분하여 진행됩니다.
클라우드 서비스 내부 네트워크 통신 시 주의사항은 다음과 같습니다.

- 동일 리전(동일 계정 및 같은 VPC 내)의 클라우드 리소스는 내부 네트워크를 통해 통신합니다. [개인 IP 주소](http://intl.cloud.tencent.com/document/product/213/5225)를 사용하여 직접 액세스할 수 있습니다.
- 각 리전 간의 네트워크가 완전히 격리되어 있기 때문에, 리전 간의 클라우드 서비스는 내부 네트워크를 통해 통신할 수 없습니다.
- 리전 간 클라우드 서비스는 [공용 IP](https://intl.cloud.tencent.com/document/product/213/5224)를 통해 Internet에 액세스하는 방식으로 통신합니다. 각 VPC의 클라우드 서비스는 더욱 빠르고 안정적인 [CCN](https://intl.cloud.tencent.com/document/product/1003)을 통해 통신합니다.
- [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214)는 현재 기본적으로 리전 내 트래픽 전달과 로컬 리전 CVM과의 바인딩을 지원합니다. [리전 간 바인딩](https://intl.cloud.tencent.com/document/product/214/38441) 기능을 활성화하면 CLB로 CVM의 리전 간 바인딩을 지원합니다.

## 가용존
가용존(Zone)은 Tencent Cloud가 동일 리전에서 전력과 네트워크가 별개로 적용되는 물리적 데이터센터입니다. 가용존의 장애를 서로 격리(대규모 재해 혹은 대규모 전력 장애 제외)하여 장애가 확산되지 않으며, 사용자가 온라인 서비스를 유지하도록 지원합니다. 독립 가용존 내의 인스턴스를 실행하면 사용자는 응용 프로그램이 개별 위치 장애의 영향을 받지 않게 할 수 있습니다.
사용자가 인스턴스를 실행하면 지정한 리전에서 임의의 가용존을 선택할 수 있습니다. 사용자에게 애플리케이션 시스템의 높은 신뢰성이 필요한 경우(특정 인스턴스에 장애 발생 시 서비스 지속 사용 보장), 가용존 통합 배포 솔루션(예: [로드 밸런서](https://intl.cloud.tencent.com/document/product/214), [EIP](https://intl.cloud.tencent.com/document/product/213/5733) 등)을 사용하여 다른 가용존의 인스턴스가 대신 관련 요청을 처리할 수 있습니다.

## 리전과 가용존 리스트
리전(Region)과 가용존(Zone) 구성:
>?외부 네트워크 연결 가능 리전:
>광저우, 상하이, 난징, 베이징, 청두, 충칭, 중국 홍콩, 싱가포르, 서울, 도쿄, 실리콘밸리, 프랑크푸르트.

### 중국
<table class="table-striped">
<tbody>
<tr><th>리전</th><th>가용존</th></tr>
<tr>
<td rowspan="6">화남지역(광저우)<br> ap-guangzhou</td>
<td>광저우 1존(품절)<br> ap-guangzhou-1</td></tr>	
<tr>
<td>광저우 2존<br> ap-guangzhou-2</td></tr>
<tr>
<td>광저우 3존<br> ap-guangzhou-3</td></tr>
<tr>
<td>광저우 4존<br> ap-guangzhou-4</td></tr>
<tr>
<td>광저우 6존<br> ap-guangzhou-6</td></tr>
<tr>
<td>광저우 7존<br> ap-guangzhou-7<td></tr>
<tr>
<td rowspan="5">화동지역(상하이)<br>ap-shanghai</td>
<td>상하이 1존<br>ap-shanghai-1</td></tr>
<tr>
<td>상하이 2존<br>ap-shanghai-2</td></tr>
<tr>
<td>상하이 3존<br>ap-shanghai-3</td></tr>
<tr>
<td>상하이 4존<br>ap-shanghai-4</td></tr>
<tr>
<td>상하이 5존<br>ap-shanghai-5</td></tr>
<td rowspan="3">화동지역(난징)<br>ap-nanjing</td>
<td>난징 1존<br>ap-nanjing-1</td></tr>
<tr>
<td>난징 2존<br>ap-nanjing-2</td></tr>
<tr>
<td>난징 3존<br>ap-nanjing-3</td></tr>
<tr>
<td rowspan="7">화북지역(베이징)<br>ap-beijing</td>
<td>베이징 1존<br>ap-beijing-1</td></tr>
<tr>
<td>베이징 2존<br>ap-beijing-2</td></tr>
<tr>
<td>베이징 3존<br>ap-beijing-3</td></tr>
<tr>
<td>베이징 4존<br>ap-beijing-4</td></tr>
<tr>
<td>베이징 5존<br>ap-beijing-5</td></tr>
<tr>
<td>베이징 6존<br>ap-beijing-6</td></tr>
<tr>
<td>베이징 7존<br>ap-beijing-7</td></tr>
<tr>
<td rowspan="2">서남지역(청두)<br>ap-chengdu</td>
<td>청두 1존<br>ap-chengdu-1</td></tr>
<tr>
<td>청두 2존<br>ap-chengdu-2</td></tr>    
<tr>
<td >서남지역(충칭)<br>ap-chongqing</td>
<td>충칭 1존<br>ap-chongqing-1</td></tr>
<tr>
<td rowspan="3">중국홍콩, 마카오 및 대만 지역(중국홍콩)<br>ap-hongkong</td>
<td>중국 홍콩 1존(중국 홍콩 노드로 중국 홍콩, 중국 마카오, 중국 대만 지역 커버 가능)<br>ap-hongkong-1</td></tr>
<tr>
<td>중국 홍콩 2존(중국 홍콩 노드로 중국 홍콩, 중국 마카오, 중국 대만 지역 커버 가능)<br>ap-hongkong-2</td></tr>
<tr>
<td>중국 홍콩 3존(중국 홍콩 노드로 중국 홍콩, 중국 마카오, 중국 대만 지역 커버 가능)<br>ap-hongkong-3</td></tr>
</tbody></table>	

### [기타 국가 및 지역](id:InternationalArea)
<table class="table-striped">
<tbody>
<tr><th>리전</th><th>가용존</th></tr>
<tr>
<td  rowspan="3">아시아 태평양 동남부(싱가포르)<br>ap-singapore</td>
<td>싱가포르 1존(싱가포르 노드로 아시아 태평양 동남부 지역 커버 가능)<br>ap-singapore-1</td></tr>
<tr>
<td>싱가포르 2존(싱가포르 노드로 아시아 태평양 동남부 지역 커버 가능)<br>ap-singapore-2</td></tr>
<tr>
<td>싱가포르 3존(싱가포르 노드의 커버리지: 동남아시아 지역)<br>ap-singapore-3</td>
</tr>
<td>아시아 태평양 동남부(자카르타)<br>ap-jakarta</td>
<td>자카르타 1존(자카르타 노드로 아시아 태평양 동남부 지역 커버 가능)<br>ap-jakarta-1</td></tr>
<tr>
<td  rowspan="2">아시아 태평양 동남부(방콕)<br>ap-bangkok </td>
<td >방콕1존(방콕 노드로 아시아 태평양 동남부 지역 커버 가능)<br>ap-bangkok-1</td>
<tr>
<td >방콕2존(방콕 노드로 아시아 태평양 동남부 지역 커버 가능)<br>ap-bangkok-2</td>
<tr>
<td  rowspan="2">아시아 태평양 남부(뭄바이)<br>ap-mumbai</td>
<td>뭄바이 1존(뭄바이 노드로 아시아 태평양 남부 지역 커버 가능)<br>ap-mumbai-1</td></tr>
<tr>
<td>뭄바이 2존(뭄바이 노드로 아시아 태평양 남부 지역 커버 가능)<br>ap-mumbai-2</td></tr>		
<tr>
<td rowspan="2">아시아 태평양 동북부(서울)<br>ap-seoul</td>
<td>서울 1존(서울 노드로 아시아 태평양 동북부 지역 커버 가능)<br>ap-seoul-1</td></tr>
<tr>
<td>서울 2존(서울 노드로 아시아 태평양 동북부 지역 커버 가능)<br>ap-seoul-2</td></tr>
<tr>
<td rowspan="2">아시아 태평양 동북부(도쿄)<br>ap-tokyo</td>
<td>도쿄 1존(도쿄 노드로 아시아 태평양 동북부 지역 커버 가능)<br>ap-tokyo-1</td></tr>
<tr>
<td>도쿄 2존(도쿄 노드로 아시아 태평양 동북부 지역 커버 가능)<br>ap-tokyo-2</td></tr>
<tr>
<td rowspan="2">미국 서부(실리콘밸리)<br>na-siliconvalley</td>
<td>실리콘밸리 1존(실리콘밸리 노드로 미국 서부 지역 커버 가능)<br>na-siliconvalley-1</td></tr>
<tr>
<td>실리콘밸리 2존(실리콘밸리 노드로 미국 서부 지역 커버 가능)<br>na-siliconvalley-2</td></tr>
<tr>
<td rowspan="2">미국 동부(버지니아주)<br>na-ashburn</td>
<td>버지니아 1존(버지니아 노드로 미국 동부 지역 커버 가능)<br>na-ashburn-1</td></tr>
<tr>
<td>버지니아 2존(버지니아 노드로 미국 동부 지역 커버 가능)<br>na-ashburn-2</td></tr>
<tr>
<td>북미 지역(토론토)<br>na-toronto</td>
<td>토론토 1존(토론토 노드로 북미 지역 커버 가능)<br>na-toronto-1</td></tr>
<tr>
<td>남미 지역(상파울루)<br>sa-saopaulo</td>
<td>상파울루 1존(상파울루 노드로 남미 리전 커버 가능)<br>sa-saopaulo-1</td></tr>
<tr>
<td rowspan="2">유럽 지역(프랑크푸르트)<br>eu-frankfurt</td>
<td>프랑크푸르트 1존(프랑크푸르트 노드로 유럽 지역 커버 가능)<br>eu-frankfurt-1</td></tr>
<tr>
<td>프랑크푸르트 2존(프랑크푸르트 노드로 유럽 지역 커버 가능)<br>eu-frankfurt-2</td></tr>
<tr>
<td >유럽 지역(모스크바)<br>eu-moscow</td>
<td>모스크바 1존(모스크바 노드로 유럽 지역 커버 가능)<br>eu-moscow-1</td></tr>
</tbody></table>

## 리전과 가용존 선택하기
클라우드 서비스 구매 시 액세스 지연시간 단축 및 다운로드 속도 향상을 위해, 가장 가까운 리전 선택을 권장합니다.
