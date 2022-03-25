## 작업 시나리오

본문은 사용자 정의 구성 방법을 예로 들어 Tencent Cloud의 Cloud Virtual Machine(CVM) 인스턴스를 생성하는 방법을 안내합니다.

## 전제 조건

CVM 인스턴스를 생성하기 전 다음 작업을 완료해야 합니다.
- [Tencent Cloud 계정 생성](https://intl.cloud.tencent.com/document/product/378/17985) 및 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)을 완료해야 합니다.
- 생성하려는 네트워크 유형이 VPC의 CVM 인스턴스일 경우, 타깃 리전에서 [VPC 생성](https://intl.cloud.tencent.com/document/product/215/31805) 후 VPC의 타깃 가용존에서 [서브넷 생성](https://intl.cloud.tencent.com/document/product/215/31806)을 해야 합니다.
- 시스템에 자동 생성된 기본 항목을 사용하지 않으려면, [프로젝트 생성](https://intl.cloud.tencent.com/zh/document/product/378/34726)을 해야 합니다.
- 시스템 자동으로 생성된 기본 보안 그룹을 사용하지 않을 경우 목표 리전에 [보안 그룹 생성](https://intl.cloud.tencent.com/document/product/213/34271)하고 사용자 서비스 수요를 충족할 수 있는 보안 그룹 규칙을 추가합니다.
- Linux 인스턴스를 생성할 경우 SSH 키 쌍을 바인딩하려면 목표 프로젝트에 [SSH 키 생성](https://intl.cloud.tencent.com/document/product/213/16691)이 필요합니다.
- 사용자 정의 이미지의 CVM 인스턴스를 생성해야 할 경우 [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942) 또는 [미러 이미지 가져오기](https://intl.cloud.tencent.com/document/product/213/4945)를 실행합니다.

## 작업 단계

1. [Tencent Cloud 공식 사이트](https://intl.cloud.tencent.com/zh/)에 로그인하고 **제품** > **기본** > **컴퓨팅** > **[CVM](https://intl.cloud.tencent.com/zh/products/cvm)**을 선택한 뒤, **구매하기**를 클릭하여 CVM 구매 페이지로 이동합니다.
 - **[사용자 정의 설정](https://buy.intl.cloud.tencent.com/cvm?tab=custom&step=1&devPayMode=hourly®ionId=4&zoneId=200004&instanceType=SA2.MEDIUM4&vpcId=vpc-mzg9lleo&subnetId=subnet-nr4uyak7&platform=TencentOS&bandwidthType=TRAFFIC_POSTPAID_BY_HOUR&bandwidth=5<CreateMode=createVersion):** 특정 시나리오에 적합하며, 사용자 필요에 따른 CVM 인스턴스 구입이 용이합니다.
2. 페이지 알림에 따라 다음 정보를 설정합니다.
<table>
<tr><th style="width: 20%">유형</th><th style="width: 12%">필수/옵션</th><th>설정 설명</th></tr>
<tr><td>과금 방식</td><td>필수</td><td>실제 필요에 따라 선택하십시오: <ul><li><b>사용량 과금</b>: CVM의 탄력적 과금 방식은 이커머스 타임 세일 등 장치 수요가 순간적으로 크게 변동하는 시나리오에 적용됩니다.</li><li><b>스팟 인스턴스</b>: 일종의 새 인스턴스 작업 모드로서 빅 데이터 컴퓨팅, CLB 온라인 서비스 및 웹 사이트 서비스 등 시나리오에 적용되며 일반 가격 범위는 종량제의 10%-20%입니다.</li></ul>과금 방식에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/2180">과금 방식 안내</a>를 참고하십시오.</td></tr>
<tr><td>리전/가용존</td><td>필수</td><td><ul><li><b>리전</b>: 고객과 가장 가까운 리전을 선택하면, 액세스 딜레이를 낮추고 속도를 높일 수 있습니다.</li><li><b>가용존</b>: 실제 필요에 따라 선택하시기 바랍니다.</br>여러 대의 CVM을 구매하는 경우, 각기 다른 가용존을 선택하면 재해 복구 효과를 구현할 수 있습니다.</li></ul>리전 및 가용존 관련 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/6091">리전 및 가용존</a>을 참고하십시오.</td></tr>
<tr><td>네트워크</td><td>필수</td><td>Tencent Cloud에 구축된 논리적 격리를 나타내는 가상 네트워크로서 VPC는 최소 하나의 서브넷으로 구성됩니다. 시스템은 사용자를 위해 각 리전에 기본 VPC 및 서브넷을 제공합니다.<br>
기존 VPC/서브넷이 사용자의 니즈를 충족하지 못하는 경우 VPC 콘솔에서 생성할 수 있습니다.</br><b>주의 사항</b>:<ul><li>동일한 VPC에서 리소스는 기본으로 내부망에서 상호 연결됩니다.</li><li>구매 시 CVM과 가용존 속성이 동일한 서브넷에서 CVM을 생성해야 합니다.</li></ul></td></tr>
<tr><td>인스턴스</td><td>필수</td><td>Tencent Cloud는 낮은 레이어 하드웨어에 따라 현재 다양한 인스턴스 유형을 제공합니다. 최상의 성능을 얻기 위해 차세대 인스턴스 유형을 사용할 것을 권장합니다.</br>
인스턴스에 대한 더 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/11518">인스턴스 사양</a>을 참고하십시오.</td></tr>
<tr><td>이미지</td><td>필수</td><td>Tencent Cloud는 공용 이미지, 사용자 정의 이미지, 공유 이미지, 마켓 플레이스를 제공하므로, <a href="https://intl.cloud.tencent.com/document/product/213/4941">이미지 유형</a>을 참고하여 선택하실 수 있습니다.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">시스템 디스크</a></td><td>필수</td><td>운영 체제 설치에 사용되며, 기본 용량은 50GB입니다.</br>리전에 따라 선택 가능한 CBS 유형이 달라질 수 있으므로, 실제 페이지 안내에 따라 선택하시기 바랍니다.</br>CBS에 대한 더 자세한 설명은 <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS 유형</a>을 참고하십시오.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">데이터 디스크</a></td><td>옵션</td><td>CVM의 스토리지 용량 확장에 사용되며, 안전하고 효율적인 스토리지 디바이스를 제공합니다. 기본적으로 CBS 데이터 디스크가 추가되어 있지 않습니다.</br>CBS에 대한 더 자세한 설명은 <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS 유형</a>을 참고하십시오.</td></tr>
<tr><td>정기 스냅샷</td><td>옵션</td><td>시스템 디스크 또는 데이터 디스크에 대해 정기 스냅샷 정책을 설정할 수 있습니다. 정기 스냅샷에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/362/35238">정기 스냅샷</a>을 참고하십시오.</td></tr>
<tr><td>공용 네트워크 대역폭</td><td>필수</td><td>기본적으로 독립적인 공용 IP가 무료로 할당됩니다. </br>Tencent Cloud는 다음과 같은 두 가지 네트워크 과금 방식을 제공합니다. 실제 필요에 따라 0Mbps보다 큰 값을 설정하십시오. <ul><li><b>대역폭 과금</b>: 고정 대역폭을 선택하여 해당 대역폭 초과 시 패킷이 손실됩니다. 네트워크 변동이 적은 시나리오에 적합합니다. </li><li><b>트래픽 과금</b>: 실제 트래픽 사용량을 기준으로 과금됩니다. 예기치 않은 트래픽으로 인한 비용 발생을 방지하기 위해 대역폭 피크값을 제한할 수 있으며, 순간 대역폭이 해당 값을 초과하면 패킷이 손실됩니다. 네트워크 변동이 큰 시나리오에 적합합니다. </li><li><b>BWP 과금</b>: 서비스 중인 공용 네트워크 트래픽의 피크 타임이 서로 다른 시간대에 분포되어 있을 때 BWP를 통한 대역폭 집계 과금이 가능합니다. 대규모 비즈니스, 특히 공용 네트워크의 각 인스턴스 간에 트래픽 피크가 형성되는 시나리오에 적합합니다. <br>BWP는 현재 베타 버전으로, 사용을 원하는 경우 <a href="https://cloud.tencent.com/apply/p/8o8lmsr5nj8">베타 신청</a>양식을 제출하십시오. </li></ul><b>주의 사항</b>: <ul><li>무료로 할당된 독립적인 공용 IP 주소는 인스턴스와의 바인딩을 해제할 수 없습니다. 해당 IP 주소의 바인딩을 해제해야 하는 경우 해당 공용 IP를 EIP로 전환한 뒤 해제할 수 있습니다. EIP에 대한 더 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a>를 참고하십시오. </li><li>다음 두 가지 경우에는 현재 독립적인 공용 IP를 할당할 수 없습니다. 실제 구매 페이지를 참고하십시오.
<ul><li>IP 리소스가 품절된 경우</li><li>일부 리전의 경우</li></ul></li></ul></td></tr>
<tr><td>IPv6 주소</td><td>옵션</td><td>인스턴스의 IPv6 주소를 활성화합니다.</a>.</td></tr> 
<tr><td>수량</td><td>필수</td><td>구매할 CVM 수량을 표시합니다.</td></tr> 
<tr><td>기간</td><td>필수</td><td>CVM의 사용 기간을 나타냅니다.</td></tr> 
</table>

3. **다음 단계: 호스트 설정**을 클릭하고 호스트 설정 페이지로 들어갑니다.
4. 페이지의 알람에 따라 다음 정보를 설정합니다.
<table>
<tr><th style="width: 20%">유형</th><th style="width: 12%">필수/옵션</th><th>설정 설명</th></tr>
<tr><td>보안 그룹</td><td>필수</td><td><ul><li>사용 가능한 보안 그룹이 없을 경우 <b>보안 그룹 생성</b>을 선택합니다.</li><li>사용 가능한 보안 그룹이 있는 경우 <b>기존 보안 그룹</b>을 선택합니다. </li></ul>보안 그룹에 대한 더 자세한 설명은 <a href="https://intl.cloud.tencent.com/document/product/213/12452">보안 그룹</a>을 참고하십시오.</td></tr>
<tr><td>세부 항목</td><td>필수</td><td>기본적인 프로젝트로써 실제 필요에 따라 구축된 프로젝트를 선택하고 다양한 CVM 관리에 사용할 수 있습니다.</td></tr>
<tr><td>태그</td><td>옵션</td><td>클라우드 리소스의 분류, 검색 및 취합을 위해 필요에 따라 인스턴스에 태그를 추가할 수 있습니다. 태그에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/651/13334">태그</a>를 참고하십시오.</td></tr>
<tr><td>인스턴스 이름</td><td>옵션</td><td>사용자 정의 항목으로, 생성할 CVM 이름을 나타냅니다.</br><ul><li>인스턴스 이름을 설정하지 않을 경우, 인스턴스 이름이 '이름 없음'으로 생성됩니다.</li><li>인스턴스 이름을 변경할 경우 60자 이내여야 하며, <a href="https://intl.cloud.tencent.com/document/product/213/32020">연속된 이름으로 일괄 생성하거나 지정 스트링 패턴으로 이름을 생성</a>할 수 있습니다.</li></ul><b>주의 사항</b>: 해당 이름은 콘솔에서만 표시되는 이름으로, CVM의 hostname이 아닙니다.</td></tr>
<tr><td>로그인 방식</td><td>필수</td><td>사용자의 실제 필요에 따라 CVM 로그인 방식을 설정하십시오. <ul><li><b>비밀번호 설정</b>: 사용자 정의로 인스턴스 로그인의 비밀번호를 설정하십시오. <li><li><b>지금 키를 연결하십시오.(Linux 인스턴스만 지원함)</b>: SSH 키 연결은 SSH 키 방식을 통해 CVM에 보다 안전하게 로그인할 수 있습니다.</br>키가 없거나 기존 키가 부적합한 경우 <b>즉시 생성</b>을 클릭하여 생성할 수 있습니다. SSH 키에 대한 자세한 정보는 <a href="http://cloud.tencent.com/doc/product/213/SSH%E5%AF%86%E9%92%A5">에서 SSH 키</a>를 참고하십시오.</li><li><b>비밀번호 자동 생성</b>: 자동으로 생성된 비밀번호는 <a href="https://console.cloud.tencent.com/message">내부 메시지</a> 방식으로 전송됩니다.</li></ul></td></tr>
<tr><td>보안 강화</td><td>옵션</td><td>Anti-DDoS 및 CWP를 무료로 활성화하여 사용자가 서버 보안 시스템을 구축하고 데이터 유출을 방지할 수 있도록 지원합니다.</td></tr>
<tr><td>Cloud Monitor</td><td>옵션</td><td>기본적으로 클라우드 서비스 모니터링은 무료로 활성화됩니다. 컴포넌트를 설치하면 호스트 모니터링 지표는 모니터링 아이콘으로 표시되며 사용자 정의 알람의 임계값 설정을 지원합니다. 또한 입체화 CVM 데이터 모니터링, 스마트한 데이터 분석, 실시간 장애 알람 및 개성화 데이터 리포트 설정을 제공하여 사용자가 서비스 및 CVM 상태를 정확하게 파악할 수 있습니다.</td></tr>
<tr><td>자동화 어시스턴트</td><td>옵션</td><td>기본적으로 무료로 활성화됩니다. CVM의 네이티브 유지보수 배포 툴로서 원격으로 인스턴스에 연결할 필요가 없습니다. Shell 명령어를 자동 일괄 실행하여 자동화 유지보수 스크립트 실행, 프로세스 폴링, 소프트웨어 설치/언마운트, 애플리케이션 업데이트 및 패치 설치를 완료할 수 있습니다.</td></tr>
<tr><td>자동 연장</td><td>옵션</td><td>‘계정 잔액이 충분하면 장치 만료 후 매월 자동 연장’을 선택하여 장치 만료 시 자동 갱신되도록 합니다.</br>자동 연장에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/zh/document/product/555/7454">연장 관리</a>를 참고하십시오.</td></tr>
<tr><td>고급 설정</td><td>옵션</td><td>실제 필요에 따라 더 다양한 인스턴스를 설정할 수 있습니다. <ul><li><b>호스트 이름</b>: CVM 운영 체제 내의 컴퓨터 이름을 사용자 정의 설정할 수 있으며, CVM 생성 후 CVM에 로그인하여 조회할 수 있습니다. </li><li><b>CAM의 역할</b>: 역할 설정 후 역할을 통해 CVM에 Tencent Cloud의 서비스 및 운영, 리소스에 대한 액세스 권한을 부여할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/38290">인스턴스 역할 관리</a>를 참고하여 설정하십시오. </li><li><b>배치 그룹</b>: 필요에 따라 인스턴스를 배치 그룹에 추가하여 서비스 가용성을 높일 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/15486">배치 그룹</a>을 참고하여 설정할 수 있습니다. </li><li><b>사용자 정의 데이터</b>: 지정된 사용자 정의 데이터로 인스턴스를 설정하여 인스턴스 실행 시 설정된 스크립트를 실행합니다. 한 번에 여러 대의 CVM을 구매할 경우, 사용자 정의 데이터가 모든 CVM에서 실행됩니다. Linux 운영 체제는 Shell 형식을 지원하고 Windows 운영 체제에서는 PowerShell 형식을 지원하며, 최대 16KB의 원시 데이터를 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/17525">사용자 정의 데이터</a>를 참고하십시오. </br><b>주의 사항</b>: Cloudinit 서비스가 포함된 일부 공용 이미지에만 사용자 정의 데이터 설정을 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/19670">Cloud-Init</a>를 참고하십시오.</li></ul></td></tr>
</table>

5. **다음 단계: 설정 정보 확인**을 클릭하고 설정 정보 확인 페이지로 이동합니다.
6. 구매한 CVM 정보를 확인하고 각 설정의 요금 명세서를 확인합니다.
7. ‘<Tencent Cloud 서비스 계약> 및 <환불 규정>에 동의’ 또는 ‘<Tencent Cloud 서비스 계약>에 동의’를 읽고 체크합니다.
8. 실제 필요에 따라 다음 작업을 수행합니다.
 - **실행 템플릿으로 저장** 선택: 인스턴스 설정을 실행 템플릿으로 저장합니다. 실행 템플릿을 사용하여 인스턴스를 빠르게 생성할 수 있습니다.
 - **API Explorer 모범 사례 스크립트 생성** 선택: 선택된 설정에 해당하는 인스턴스를 생성하여 OpenAPI 모범 사례 스크립트 코드를 생성하고, 동일한 설정으로 클라우드 서버 구입을 위한 코드를 저장할 수 있습니다. 자세한 내용은 [인스턴스 생성을 위한 API Explorer 모범 사례 스크립트 생성](https://intl.cloud.tencent.com/document/product/213/39811)을 참고하십시오.
8. **구매하기** 또는 **활성화**를 클릭하여 결제를 완료합니다. 결제를 완료하면 [CVM 콘솔](https://console.cloud.tencent.com/cvm)에서 CVM을 확인하실 수 있습니다.
CVM 인스턴스 이름, 공용 IP 주소, 개인 IP 주소, 로그인 이름, 초기 로그인 비밀번호 등 정보는 [내부 메시지](https://console.cloud.tencent.com/message)로 계정에 전송됩니다. 이 정보로 인스턴스를 로그인 및 관리할 수 있으며 호스트의 보안성을 보장하기 위해 CVM 로그인 비밀번호를 변경하십시오.
