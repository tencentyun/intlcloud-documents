## 작업 시나리오

본문은 사용자 정의 구성 방법을 예로 들어 Tencent Cloud의 Cloud Virtual Machine(CVM) 인스턴스를 생성하는 방법을 안내합니다.

## 전제 조건

CVM 인스턴스를 생성하기 전 다음 작업을 완료해야 합니다.
- [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985) 완료해야 합니다.
- 생성하려는 네트워크 유형이 VPC의 CVM 인스턴스일 경우, 타깃 리전에서 [Creating VPC](https://intl.cloud.tencent.com/document/product/215/31805) 후 VPC의 타깃 가용존에서 [Creating Subnets](https://intl.cloud.tencent.com/document/product/215/31806) 해야 합니다.
- 시스템에 자동 생성된 기본 항목을 사용하지 않으려면, [프로젝트 생성](https://intl.cloud.tencent.com/document/product/378/34726)을 해야 합니다.
- 시스템 자동으로 생성된 기본 보안 그룹을 사용하지 않을 경우 목표 리전에 [보안 그룹 생성](https://intl.cloud.tencent.com/document/product/213/34271)하고 사용자 서비스 수요를 충족할 수 있는 보안 그룹 규칙을 추가합니다.
- Linux 인스턴스를 생성할 경우 SSH 키 쌍을 바인딩하려면 목표 프로젝트에 [SSH 키 생성](https://intl.cloud.tencent.com/document/product/213/16691)이 필요합니다.
- 사용자 정의 이미지의 CVM 인스턴스를 생성해야 할 경우 [커스텀 미러 구축](https://intl.cloud.tencent.com/document/product/213/4942) 또는 [미러 이미지 가져오기](https://intl.cloud.tencent.com/document/product/213/4945)를 실행합니다.

## 작업 단계

1. [Tencent Cloud 공식 사이트](https://intl.cloud.tencent.com)에 로그인하고 **제품** > **컴퓨팅 및 컨테이너** > **컴퓨팅** > **[CVM](https://intl.cloud.tencent.com/products/cvm)** 을 선택한 뒤, **구매하기**를 클릭하여 CVM 구매 페이지로 이동합니다.
 - **[사용자 정의 구성](https://buy.intl.cloud.tencent.com/cvm?regionId=1&projectId=-1&templateCreateMode=createLt):** 특정 시나리오에서 사용하기에 적합하며 특정 요구 사항에 맞는 CVM 인스턴스를 더 쉽게 구입할 수 있습니다.
2. 페이지 알림에 따라 다음 정보를 설정합니다.
<table>
  <tr>
	<th style="width: 20%">유형</th>
	<th style="width: 12%">필수/옵션</th>
	<th>설정 설명</th>
  </tr>
  <tr>
	<td>과금 방식</td>
	<td>필수</td>
	<td>실제 필요에 따라 선택하십시오:
	<ul>
	  <li>
	  <b>종량제</b>: 이커머스 타임 세일과 같이 수요가 급격하고 갑작스럽게 변동하는 시나리오에 적합한 유연한 과금 방식입니다.</li>
	  <li>
	  <b>스팟 인스턴스</b>: 빅 데이터 컴퓨팅, 로드 밸런싱이 있는 온라인 비즈니스 및 웹 사이트 서비스와 같은 시나리오에 적합합니다. 일반적인 가격 범위는 종량제 인스턴스의 10%
	  - 20%입니다.</li>
	</ul>과금 방식에 대한 자세한 내용은 
	<a href="https://intl.cloud.tencent.com/document/product/213/2180">과금 방식</a>을 참고하십시오.</td>
  </tr>
  <tr>
	<td>리전/가용존</td>
	<td>필수</td>
	<td>
	<ul>
	  <li>
	  <b>리전</b>: 고객과 가장 가까운 리전을 선택하여 액세스 지연 시간을 줄이고 액세스 속도를 높입니다.</li>
	  <li>
	  <b>가용존</b>: 실제 요구 사항에 따라 선택합니다.
	  <br />여러 CVM 인스턴스를 구매하려는 경우 재해 복구를 위해 서로 다른 가용존을 선택하는 것이 좋습니다.</li>
	</ul>리전 및 가용존 옵션에 대한 자세한 내용은  
	<a href="https://intl.cloud.tencent.com/document/product/213/6091">리전 및 가용존</a>을 참고하십시오.</td>
  </tr>
	<tr>
	<td>인스턴스</td>
	<td>필수</td>
	<td>Tencent Cloud는 다양한 기본 하드웨어와 함께 다양한 인스턴스 유형을 제공합니다.
	<br />인스턴스 세부 정보는  
	<a href="https://intl.cloud.tencent.com/document/product/213/11518">인스턴스 스펙</a>을 참고하십시오.</td>
  </tr>
	<tr>
	<td>이미지</td>
	<td>필수</td>
	<td>Tencent Cloud는 공용 이미지, 사용자 정의 이미지 및 공유 이미지를 제공합니다. 
	<a href="https://intl.cloud.tencent.com/document/product/213/4941">이미지 유형</a>을 참고하십시오.</td>
  </tr>
	<tr>
	<td>
	  <a href="https://intl.cloud.tencent.com/document/product/362/31636">시스템 디스크</a>
	</td>
	<td>필수</td>
	<td>운영 체제를 설치하는 데 사용됩니다. 기본 용량은 50GB입니다.
	<br />사용 가능한 CBS(Cloud Block Storage) 유형은 리전에 따라 다릅니다. 페이지의 안내에 따라 선택하십시오.
	<br />CBS에 대한 자세한 내용은 
	<a href="https://intl.cloud.tencent.com/document/product/362/31636">Cloud Disk Types</a>를 참고하십시오.</td>
  </tr>
  <tr>
	<td>
	  <a href="https://intl.cloud.tencent.com/document/product/362/31636">데이터 디스크</a>
	</td>
	<td>옵션</td>
	<td>더 많은 저장 용량이 필요한 경우 데이터 디스크를 구매하십시오.
	<br />CBS에 대한 자세한 내용은 
	<a href="https://intl.cloud.tencent.com/document/product/362/31636">Cloud Disk Types</a>를 참고하십시오.</td>
  </tr>
  <tr>
	<td>정기 스냅샷</td>
	<td>옵션</td>
	<td>시스템 디스크 또는 데이터 디스크에 대해 정기 스냅샷 정책을 설정합니다. 정기 스냅샷에 대한 자세한 내용은  
	<a href="https://intl.cloud.tencent.com/document/product/362/35238">Scheduled Snapshots</a>를 참고하십시오.</td>
  </tr>
  <tr>
	<td>수량</td>
	<td>필수</td>
	<td>구매할 CVM 인스턴스 수량입니다.</td>
  </tr>
</table>
3. **다음 단계: 네트워크 및 호스트 설정**을 클릭하고 호스트 설정 페이지로 들어갑니다.
4. 페이지 안내에 따라 다음 정보를 설정합니다.
<table>
  <tr>
	<th style="width: 20%">유형</th>
	<th style="width: 12%">필수/옵션</th>
	<th>설정 설명</th>
  </tr>
	 <tr>
	<td>네트워크</td>
	<td>필수</td>
	<td>
	Tencent Cloud에 구축된 논리적으로 격리된 네트워크 공간입니다. VPC에는 하나 이상의 서브넷이 포함됩니다. 시스템은 각 리전에 대한 기본 VPC 및 서브넷을 제공합니다.
	<br />기존 VPC 또는 서브넷이 요구 사항을 충족하지 않는 경우 VPC 콘솔에서 VPC 또는 서브넷을 생성할 수 있습니다.
	<br />
	<b>참고</b>:
	<ul>
	  <li>동일한 VPC의 리소스는 사설망 내에서 상호 연결할 수 있습니다.</li>
	  <li>CVM 인스턴스를 구매할 때 CVM과 서브넷이 동일한 가용존에 있는지 확인하십시오.</li>
	</ul></td>
  </tr>
	 <tr>
	<td>공용 IP</td>
	<td>옵션</td>
	<td>CVM에 공중망 액세스가 필요한 경우 CVM에 공용 IP를 할당해야 합니다. CVM을 생성할 때 공용 IP를 할당하도록 선택하거나 CVM이 생성된 후 CVM에 대한 <a href="https://intl.cloud.tencent.com/document/product/213/5733">Elastic IP</a>를 구성할 수 있습니다.<br><b>참고</b>: 
	<ul>
	  <li>무료로 할당된 공용 IP는 인스턴스에서 직접 바인딩 해제할 수 없으며, 해제하려면 
	  먼저 EIP로 변환해야 합니다. EIP에 대한 자세한 내용은 
	  <a href="https://intl.cloud.tencent.com/document/product/213/5733">Elastic IP</a>를 참고하십시오.</li>
	  <li>다음 두 가지 경우에는 공인 IP 주소를 할당할 수 없습니다:
	  <ul>
		<li>IP 리소스 품절</li>
		<li>리전 제한</li>
	  </ul>
	</td>
	</tr>
	<tr>
	<td>대역폭 과금 방식</td>
	<td>필수</td>
	<td>
	<br />Tencent Cloud는 두 가지 네트워크 과금 방식을 제공합니다. 실제 필요에 따라 0Mbps 이상의 값을 설정하십시오.
	<ul>
	  <li>
	  <b>트래픽별 과금</b>: 실제로 사용된 트래픽을 기반으로 과금됩니다. 대역폭 상한을 지정하여 예기치 않은 트래픽으로 인해 발생하는 요금을 방지할 수 있습니다. 순간 대역폭이 이 값을 초과하면 패킷 손실이 발생합니다. 네트워크 연결이 크게 변동하는 시나리오에 적합합니다.</li>
	  <li>
	  <b>대역폭 패키지</b>: 공용 네트워크 인스턴스에 서로 다른 시간대의 트래픽 피크가 있는 경우 이 통합 과금을 선택합니다. 공중망을 통해 서로 다른 인스턴스 간에 트래픽이 시차를 둘 수 있는 대규모 비즈니스에 적합합니다.
	  <br />대역폭 패키지는 현재 베타 테스트 중입니다. 사용을 원하시면  
	  <a href="https://console.intl.cloud.tencent.com/workorder/category">티켓 제출</a> 하십시오.</li>
	</ul>자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/10578">공용 네트워크 과금 방식</a>을 참고하십시오.
	</td>
  </tr>
	<tr>
	<td>대역폭 값</td>
	<td>옵션</td>
	<td>필요에 따라 CVM의 공용 네트워크 대역폭 최댓값을 설정할 수 있습니다. 자세한 내용은  <a href="https://intl.cloud.tencent.com/document/product/213/12523">공용 네트워크 대역폭 최댓값</a>을 참고하십시오.</td>
	</tr>
  <tr>
	<td>보안 그룹</td>
	<td>필수</td>
	<td>
	<ul>
	  <li>사용 가능한 보안 그룹이 없는 경우, 
	  <b>새 보안 그룹</b>을 선택할 수 있습니다.</li>
	  <li>사용 가능한 보안 그룹이 있는 경우, 
	  <b>기존 보안 그룹</b>을 선택할 수 있습니다.</li>
	</ul>보안 그룹에 대한 자세한 내용은  
	<a href="https://intl.cloud.tencent.com/document/product/213/12452">보안 그룹</a>을 참고하십시오.</td>
  </tr>
  <tr>
	<td>태그</td>
	<td>옵션</td>
	<td>클라우드 리소스를 분류, 검색 및 집계하는 데 사용되는 필요에 따라 인스턴스에 대한 태그를 추가할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/651/13334">Tag</a>를 참고하십시오.</td>
  </tr>
  <tr>
	<td>인스턴스 이름</td>
	<td>옵션</td>
	<td>생성할 CVM 인스턴스의 이름을 사용자 정의할 수 있습니다.
	<br />
	<ul>
	  <li>인스턴스 이름을 지정하지 않으면 기본적으로 ‘이름 없음’이 사용됩니다.</li>
	  <li>인스턴스 이름은 128자를 초과할 수 없으며,  
	  <a href="https://intl.cloud.tencent.com/document/product/213/32020">일괄 연속 이름 생성 혹은 특정 스트링 패턴으로 이름 생성</a>도 지원됩니다.</li>
	</ul>
	<b>참고</b>: 이 이름은 콘솔에만 표시됩니다. CVM 인스턴스의 hostname이 아닙니다.</td>
  </tr>
  <tr>
	<td>로그인 방법</td>
	<td>필수</td>
	<td>사용자가 CVM에 로그인하는 방식을 설정합니다. 실제 필요에 따라 설정하십시오.
	<ul>
	  <li>
	  <b>비밀번호 설정</b>: 인스턴스에 로그인하기 위한 비밀번호를 사용자 정의합니다.</li>
	  <li>
	  <b>SSH 키 쌍(Linux 인스턴스만 해당)</b>: 인스턴스를 SSH 
	  키와 연결하여 CVM 인스턴스에 대한 보안 로그인을 보장합니다.
	  <br />사용 가능한 키가 없거나 기존 키가 적당하지 않은 경우 
	  <b>지금 생성</b>을 클릭하여 키를 만듭니다. SSH 키에 대한 자세한 내용은  
	  <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH 키</a>를 참고하십시오.</li>
	  <li>
	  <b>비밀번호 자동 생성</b>: 자동으로 생성된 비밀번호가  
	  <a href="https://console.cloud.tencent.com/message">메시지 센터</a>를 통해 발송됩니다.</li>
	</ul></td>
  </tr>
  <tr>
	<td>인스턴스 폐기 방지</td>
	<td>옵션</td>
	<td>기본적으로 비활성화되어 있습니다. 필요에 따라 활성화할 수 있습니다. 활성화하면 콘솔이나 또는 API 
	를 통해 인스턴스를 폐기할 수 없습니다. 인스턴스 폐기 방지에 대한 자세한 내용은  
	<a href="https://intl.cloud.tencent.com/document/product/213/47383">인스턴스 폐기 방지 활성화</a>를 참고하십시오.</td>
  </tr>
  <tr>
	<td>보안 강화</td>
	<td>옵션</td>
	<td>기본적으로 Anti-DDoS 
	및 Cloud Workload Protection이 무료로 활성화되어 데이터 유출을 방지하는 CVM 보안 시스템을 구축할 수 있습니다.</td>
  </tr>
  <tr>
	<td>TCOP</td>
	<td>옵션</td>
	<td>
	기본적으로 클라우드 서비스 모니터링은 무료로 활성화되어 있습니다. 컴포넌트를 설치하여 CVM 모니터링 메트릭을 얻고 시각적 차트에 표시할 수 있습니다. 사용자 정의 알람 임계값을 지정할 수도 있습니다. 또한 3차원 CVM 데이터 모니터링, 지능형 데이터 분석, 실시간 오류 알람 및 사용자 정의 데이터 보고서를 구성하여 Tencent Cloud 서비스 및 CVM의 상태를 정확하게 모니터링할 수 있습니다.</td>
  </tr>
  <tr>
	<td>고급 설정</td>
	<td>옵션</td>
	<td>실제 필요에 따라 인스턴스에서 더 많은 구성을 수행합니다.
	<ul>
	  <li>
	  <b>호스트 이름</b>: 사용자는 CVM 운영 체제 내에서 PC 이름을 사용자 정의할 수 있으며, CVM이 성공적으로 생성된 후 CVM에 로그인하여 확인할 ​​수 있습니다.</li>
		<li>
	  <b>프로젝트</b>: 기본 프로젝트가 선택됩니다. 다른 CVM 인스턴스를 관리하기 위해 필요에 따라 기존 프로젝트를 선택할 수 있습니다.</li>
	  <li>
	  <b>CAM 역할</b>: 역할을 설정하고 이를 사용하여 역할 엔터티에 CVM 서비스 및 리소스에 액세스하고 Tencent Cloud에서 작업을 수행할 수 있는 권한을 부여할 수 있습니다. 설정에 대한 자세한 내용은 	  
	  <a href="https://intl.cloud.tencent.com/document/product/213/45917">인스턴스 역할 관리</a>를 참고하십시오.</li>
	  <li>
	  <b>배치 그룹</b>: 서비스 가용성을 향상시키기 위해 필요에 따라 배치 그룹에 인스턴스를 추가할 수 있습니다. 자세한 내용은  
	  <a href="https://intl.cloud.tencent.com/document/product/213/15486">배치 그룹</a> 을 참고하십시오.</li>
	  <li>
	  <b>사용자 정의 데이터</b>: 사용자 정의 데이터를 지정하여 인스턴스를 구성할 수 있으며 구성된 스크립트는 인스턴스가 시작될 때 실행됩니다. 여러 CVM 인스턴스를 함께 구매하는 경우 사용자 정의 데이터가 모든 인스턴스에서 실행됩니다. Linux 
	  운영 체제는 Shell 형식을 지원하는 반면 Windows 운영 체제는 PowerShell 형식과 최대 16KB의 
	  로우(raw) 데이터를 지원합니다. 자세한 내용은 
	  <a href="https://intl.cloud.tencent.com/document/product/213/17525">사용자 설정 데이터(Linux CVM)</a>를 참고하십시오.
	  <br />
	  <b>참고</b>: 사용자 정의 데이터 구성은 Cloudinit 서비스가 있는 특정 공용 이미지만 지원합니다. 자세한 내용은  
	  <a href="https://intl.cloud.tencent.com/document/product/213/19670">Cloud-Init</a>를 참고하십시오.</li>
	</ul></td>
  </tr>
</table>
5. **다음 단계: 설정 정보 확인**을 클릭하고 설정 정보 확인 페이지로 이동합니다.
6. 구매한 CVM 정보를 확인하고 각 설정의 요금 명세서를 확인합니다.
7. ‘<Tencent Cloud 서비스 약관>’을 읽고 동의 체크합니다.
8. 실제 필요에 따라 다음 작업을 수행합니다.
 - **실행 템플릿으로 저장** 선택: 인스턴스의 설정을 실행 템플릿으로 저장하면 빠른 인스턴스 생성에 사용할 수 있습니다. 자세한 내용은 [인스턴스 실행 템플릿 관리](https://intl.cloud.tencent.com/document/product/213/45221)를 참고하십시오.
 - **API Explorer 모범 사례 스크립트 생성** 선택: 선택된 설정에 해당하는 인스턴스를 생성하여 OpenAPI 모범 사례 스크립트 코드를 생성하고, 동일한 설정으로 클라우드 서버 구입을 위한 코드를 저장할 수 있습니다. 자세한 내용은 [인스턴스 생성을 위한 API Explorer 모범 사례 스크립트 생성](https://intl.cloud.tencent.com/document/product/213/39811)을 참고하십시오.
9. **즉시 구매** 또는 **활성화**를 클릭하여 결제를 완료합니다.
결제 완료 후 [CVM 콘솔](https://console.cloud.tencent.com/cvm)에서 CVM 인스턴스를 확인할 수 있습니다.
CVM 인스턴스 이름, 공용 IP 주소, 내부 IP 주소, 로그인 이름, 초기 로그인 비밀번호 등 정보는 [내부 메시지](https://console.cloud.tencent.com/message)로 계정에 전송됩니다. 이 정보로 인스턴스를 로그인 및 관리할 수 있으며 호스트의 보안성을 보장하기 위해 CVM 로그인 비밀번호를 변경하십시오.
