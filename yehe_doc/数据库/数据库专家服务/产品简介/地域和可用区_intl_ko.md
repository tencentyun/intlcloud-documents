
TencentDB 데이터 센터는 전 세계 여러 위치에서 호스팅됩니다. 이러한 위치를 리전(Region)이라고 합니다. 각 리전에는 여러 가용존(AZ)이 있습니다.
각 리전은 여러 개의 격리된 AZ가 있는 독립적인 지리적 영역입니다. 동일한 리전의 개별 AZ는 지연 시간이 짧은 사설망을 통해 연결됩니다. Tencent Cloud를 사용하면 Tencent Cloud 리소스를 여러 위치에 배포할 수 있습니다. 서비스 사용 불가능으로 이어질 수 있는 단일 실패 지점을 제거하기 위해 리소스를 다른 AZ에 배치하는 것이 좋습니다.

리전 이름과 AZ 이름은 데이터 센터의 커버리지 범위를 가장 직접적으로 구현할 수 있습니다. 편의를 위해 다음 이름 생성 규칙이 사용됩니다.
- 리전 이름은 [리전 + 도시]로 구성됩니다. 리전은 데이터 센터가 포함되는 지리적 영역을 나타내고 도시는 데이터 센터가 위치한 도시를 나타냅니다.
- AZ 이름은 [도시 + 숫자] 형식을 사용합니다.

## 리전
Tencent Cloud 리전은 완전히 격리되어 있습니다. 이는 리전 간 최대 안정성과 내결함성을 보장합니다. Tencent Cloud 서비스를 구매할 때 액세스 지연을 최소화하고 다운로드 속도를 향상시키기 위해 최종 사용자와 가장 가까운 리전을 선택하는 것이 좋습니다. 인스턴스 시작 또는 보기와 같은 작업은 리전 레벨에서 수행됩니다.
사설망 통신:

- 동일 리전의 동일한 리전 내 동일한 VPC에 있는 Tencent Cloud 리소스는 사설망을 통해 서로 통신할 수 있습니다. [개인 IP](https://intl.cloud.tencent.com/document/product/213/5225)를 통해서도 액세스할 수 있습니다.
- 다른 리전의 네트워크는 서로 완전히 격리되어 있으며 다른 리전의 Tencent Cloud 서비스는 기본적으로 사설망을 사용하여 통신할 수 없습니다.
- 여러 리전의 Tencent Cloud 서비스는 인터넷을 통해 [공용 네트워크 IP](https://intl.cloud.tencent.com/document/product/213/5224)를 통해 서로 통신할 수 있지만, 서로 다른 VPC에 있는 서비스는 [Cloud Connect Network](https://www.tencentcloud.com/document/product/1003)를 통해 더 빠르고 안정적으로 서로 통신할 수 있습니다.
- [Cloud Load Balancer](https://www.tencentcloud.com/document/product/214)는 현재 기본적으로 리전 내 트래픽 전달을 지원합니다. [Cross-Region Binding](https://www.tencentcloud.com/document/product/214/38441) 기능을 활성화하면 CLB 인스턴스를 다른 리전의 CVM 인스턴스에 바인딩할 수 있습니다.

## 가용존(AZ)
가용존(AZ)은 동일한 리전에 독립적인 전원 공급 장치와 네트워크가 있는 Tencent Cloud의 물리적 IDC(Internet Data Center)입니다. 동일한 리전의 다른 AZ에 영향을 주지 않고 한 AZ의 장애(중대 재해 또는 정전 제외)가 격리되므로 비즈니스 안정성을 보장할 수 있습니다. 독립적인 AZ에서 인스턴스를 시작함으로써 사용자는 단일 장애 지점의 영향을 받는 애플리케이션을 보호할 수 있습니다.
인스턴스를 시작할 때 지정된 리전의 AZ를 선택할 수 있습니다. 높은 안정성을 위해 교차 AZ 배포 솔루션을 채택하여 단일 위치의 인스턴스가 실패할 때 서비스를 계속 사용할 수 있도록 할 수 있습니다. 이러한 솔루션의 예시로는 [Cloud Load Balancer](https://www.tencentcloud.com/document/product/214) 및 [EIP](https://intl.cloud.tencent.com/document/product/213/5733)가 있습니다.

## 리전과 가용존 리스트
리전(Region)과 가용존(AZ) 구성:
>?공중망 연결 가능 리전:
>광저우, 상하이, 난징, 베이징, 청두, 충칭, 중국 홍콩, 싱가포르, 서울, 도쿄, 실리콘밸리, 프랑크푸르트.

### 중국
<table class="table-striped">
<tbody>
<tr><th>리전</th><th>가용존</th></tr>
<tr>
<td rowspan="6">화남 지역(광저우)<br> ap-guangzhou</td>
<td>광저우 1존(품절)<br> ap-guangzhou-1</td></tr>	
<tr>
<td>광저우 2존(품절)<br> ap-guangzhou-2</td></tr>
<tr>
<td>광저우 3존<br> ap-guangzhou-3</td></tr>
<tr>
<td>광저우 4존<br> ap-guangzhou-4</td></tr>
<tr>
<td>광저우 6존<br> ap-guangzhou-6</td></tr>
<tr>
<td>광저우 7존<br> ap-guangzhou-7<td></tr>
<tr>
<td rowspan="3">화남 지역(선전 금융)<br>ap-shenzhen-fsi</td>
<td>선전 금융 1존<span style="background-color: rgb(249, 249, 249);">(금융 기관 및 기업만 <a href="https://cloud.tencent.com/online-service?from=sales&source=PRESALE">온라인 문의</a>를 통해 활성화를 신청할 수 있습니다)<br>ap-shenzhen-fsi-1</span></td></tr>
<tr>
<td>선전 금융 2존<span style="background-color: rgb(249, 249, 249);">(활성화 신청은 금융 기관 및 기업만 문의 가능)<br>ap-shenzhen-fsi-2</span></td></tr>
<tr>
<td>선전 금융 3존<span style="background-color: rgb(249, 249, 249);">(활성화 신청은 금융 기관 및 기업만 문의 가능)<br>ap-shenzhen-fsi-3</span></td></tr>
<tr>
<td rowspan="6">화동 지역(상하이)<br>ap-shanghai</td>
<td>상하이 1존<br>ap-shanghai-1</td></tr>
<tr>
<td>상하이 2존<br>ap-shanghai-2</td></tr>
<tr>
<td>상하이 3존<br>ap-shanghai-3</td></tr>
<tr>
<td>상하이 4존<br>ap-shanghai-4</td></tr>
<tr>
<td>상하이 5존<br>ap-shanghai-5</td></tr>
<tr>
<td>상하이 8존<br>ap-shanghai-8</td></tr>
<tr>
<td rowspan="3">화동 지역(난징)<br>ap-nanjing</td>
<td>난징 1존<br>ap-nanjing-1</td></tr>
<tr>
<td>난징 2존<br>ap-nanjing-2</td></tr>
<tr>
<td>난징 3존<br>ap-nanjing-3</td></tr>
<tr>
<td rowspan="3">화동 지역(상하이 금융)<br>ap-shanghai-fsi</td>
<td>상하이 금융 1존(활성화 신청은 금융 기관 및 기업만 문의 가능)<br>ap-shanghai-fsi-1</td></tr>
<tr>
<td>상하이 금융 2존(활성화 신청은 금융 기관 및 기업만 문의 가능)<br>ap-shanghai-fsi-2</td></tr>
<tr>
<td>상하이 금융 3존(활성화 신청은 금융 기관 및 기업만 문의 가능)<br>ap-shanghai-fsi-3</td></tr>
<tr>
<td rowspan="7">화북 지역(베이징)<br>ap-beijing</td>
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
<td >화북 지역(베이징 금융)<br>ap-beijing-fsi</td>
<td>베이징 금융 1존(활성화 신청은 금융 기관 및 기업만 문의 가능)<br>ap-beijing-fsi-1</td></tr>   
<tr>
<td rowspan="2">서남 지역(청두)<br>ap-chengdu</td>
<td>청두 1존<br>ap-chengdu-1</td></tr>
<tr>
<td>청두 2존<br>ap-chengdu-2</td></tr>    
<tr>
<td >서남 지역(충칭)<br>ap-chongqing</td>
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
<td rowspan="4">동남아(싱가포르)<br>ap-singapore</td>
<td>싱가포르 1존(싱가포르 노드로 동남아 지역 커버 가능)<br>ap-singapore-1</td></tr>
<tr>
<td>싱가포르 2존(싱가포르 노드로 동남아 지역 커버 가능)<br>ap-singapore-2</td></tr>
<tr>
<td>싱가포르 3존(싱가포르 노드로 동남아 지역 커버 가능)<br>ap-singapore-3</td></tr>
<tr>
<td>싱가포르 4존(싱가포르 노드로 동남아 지역 커버 가능)<br>ap-singapore-4</td></tr>
<tr>
<td rowspan="2">동남아(자카르타)<br>ap-jakarta</td>
<td >자카르타 1존<br>ap-jakarta-1</td></tr>
<tr>
<td >자카르타 2존<br>ap-jakarta-2</td></tr>
<tr>
<td rowspan="2">동남아(방콕)<br>ap-bangkok </td>
<td >방콕 1존(방콕 노드로 동남아 지역 커버 가능)<br>ap-bangkok-1</td></tr>
<tr>
<td >방콕 2존(방콕 노드로 동남아 지역 커버 가능)<br>ap-bangkok-2</td></tr>
<tr>
<td  rowspan="2">남아시아(뭄바이)<br>ap-mumbai</td>
<td>뭄바이 1존(뭄바이 노드로 남아시아 지역 커버 가능)<br>ap-mumbai-1</td></tr>
<tr>
<td>뭄바이 2존(뭄바이 노드로 남아시아 지역 커버 가능)<br>ap-mumbai-2</td></tr>		
<tr>
<td rowspan="2">동북아(서울)<br>ap-seoul</td>
<td>서울 1존(서울 노드로 동북아 지역 커버 가능)<br>ap-seoul-1</td></tr>
<tr>
<td>서울 2존(서울 노드로 동북아 지역 커버 가능)<br>ap-seoul-2</td></tr>
<tr>
<td rowspan="2">동북아(도쿄)<br>ap-tokyo</td>
<td>도쿄 1존(도쿄 노드로 동북아 지역 커버 가능)<br>ap-tokyo-1</td></tr>
<tr>
<td>도쿄 2존(도쿄 노드로 동북아 지역 커버 가능)<br>ap-tokyo-2</td></tr>
<tr>
<td rowspan="2">미국 서부(실리콘밸리)<br>na-siliconvalley</td>
<td>실리콘밸리 1존(품절)<br>na-siliconvalley-1</td></tr>
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
<td>동북 유럽 1존(모스크바 노드로 유럽 지역 커버 가능)<br>eu-moscow-1</td></tr>
</tbody></table>

## 리전과 가용존 선택하기
Tencent Cloud 서비스를 구매할 때 액세스 대기 시간을 줄이고 다운로드 속도를 향상시키기 위해 최종 사용자와 가장 가까운 리전을 선택하는 것이 좋습니다.
