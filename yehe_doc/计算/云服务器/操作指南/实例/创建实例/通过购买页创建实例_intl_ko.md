## 작업 시나리오

본 문서는 사용자 정의 구성 방법을 예로 들어 Tencent Cloud의 Cloud Virtual Machine(CVM)인스턴스를 생성하는 방법을 안내합니다.

## 전제 조건

CVM 인스턴스를 생성하기 전에 다음 작업을 완료해야 합니다.
[Tencent Cloud 계정 가입](https://intl.cloud.tencent.com/document/product/378/17985) 및 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다. 실명 인증을 하지 않은 사용자는 중국 내 CVM 인스턴스를 구매할 수 없습니다.
- 생성하려는 네트워크 유형이 VPC의 CVM 인스턴스일 경우, 타깃 리전에서 [VPC 생성](https://intl.cloud.tencent.com/document/product/215/31805) 후 VPC의 타깃 가용존에서 [서브넷 생성](https://intl.cloud.tencent.com/document/product/215/31806)을 해야 합니다.
- 시스템에 자동 생성된 기본 항목을 사용하지 않으려면, [프로젝트 생성](https://intl.cloud.tencent.com/document/product/378/34726)을 해야 합니다.
- 시스템에 자동 생성된 보안 그룹을 사용하지 않으려면, 타깃 리전에 [보안 그룹을 생성](https://intl.cloud.tencent.com/document/product/213/34271)하고 비즈니스 요구에 따라 보안 그룹 규칙을 추가해야 합니다.
- Linux 인스턴스 생성 시 SSH 키 쌍을 바인딩하려면, 타깃 항목에 [SSH 키 생성](https://intl.cloud.tencent.com/document/product/213/16691)을 해야 합니다.
- 사용자 정의 이미지의 CVM 인스턴스를 생성하려면, [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942)을 진행하거나 [이미지 가져오기](https://intl.cloud.tencent.com/document/product/213/4945)를 해야 합니다.

## 작업 순서

1. [Tencent Cloud 공식 사이트](https://intl.cloud.tencent.com)에 로그인하고 [제품]>[기본]>[컴퓨팅]>[CVM](https://intl.cloud.tencent.com/product/cvm)을 선택한 뒤, [구매하기]를 클릭하여 CVM 구매 페이지로 이동합니다.
 - <b>[사용자 정의 구성](https://buy.cloud.tencent.com/cvm?tab=custom): </b>사용자의 요구에 맞게 CVM 인스턴스를 선택하여 구매할 수 있으므로, 특정 시나리오에 사용하기 적합합니다.
2. 페이지 안내에 따라 다음의 정보를 구성합니다.
<table>
<tr><th style="width: 20%">유형</th><th style="width: 12%">필수/선택</th><th>구성 설명</th></tr>
<tr><td>과금 방식</td><td>필수</td><td>실제 필요에 따라 선택하세요.<ul><li><b>종량제</b>: CVM의 유연한 과금 방식입니다. 더 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/2180">과금 방식 설명</a>을 참조 바랍니다.</td></tr>
<tr><td>리전/가용존</td><td>필수</td><td><ul><li><b>리전</b>: 고객과 가장 가까운 리전을 선택하여, 액세스의 딜레이를 낮추고 속도를 높이기를 권장합니다.</li><li><b>가용존</b>: 실제 필요에 따라 선택하시기 바랍니다.</br>여러 대의 CVM을 구매해야 할 경우, 다른 가용존을 선택하여 재해 복구 효과를 체험하시길 권장합니다.</li></ul>리전 및 가용존 선택에 대한 더 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/6091">리전 및 가용존</a>을 참조 바랍니다.</td></tr>
<tr><td>네트워크</td><td>필수</td><td>Tencent Cloud에서 구축한 로직이 분리된 가상 네트워크를 나타내는 것으로, 하나의 VPC는 최소 하나의 서브넷으로 구성됩니다. 시스템에서는 사용자를 위해 각 리전에 기본 VPC 및 서브넷을 제공합니다.</br>
기존의 VPC/서브넷이 사용자의 요구에 맞지 않는다면 VPC 콘솔에서 생성할 수 있습니다.</br><b>주의 사항</b>: <ul><li>동일한 VPC의 리소스는 내부 네트워크 통신으로 기본 설정되어 있습니다.</li><li>구매 시, CVM과 동일한 가용존 속성을 가진 서브넷에서 CVM을 생성해야 합니다.</li></ul></td></tr>
<tr><td>인스턴스</td><td>필수</td><td>Tencent Cloud는 기본 하드웨어 차이에 따라, 여러 종류의 인스턴스 유형을 제공하고 있습니다. 최적의 성능을 원한다면 최신 인스턴스 유형을 사용하시길 권장합니다.</br>
인스턴스에 대한 더 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/11518">인스턴스 사양</a>을 참조 바랍니다.</td></tr>
<tr><td>이미지</td><td>필수</td><td>Tencent Cloud는 공용 이미지, 사용자 정의 이미지, 공유 이미지를 제공하므로, <a href="https://intl.cloud.tencent.com/document/product/213/4941">이미지 유형</a>을 참조하여 선택하실 수 있습니다.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">시스템 디스크</a></td><td>필수</td><td>운영 체제 설치에 사용되며, 기본 용량은 50GB입니다.</br>리전에 따라 선택 가능한 CBS 유형이 달라질 수 있으므로, 실제 페이지 안내에 따라 선택하시기 바랍니다.</br>CBS에 대한 더 자세한 설명은 <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS 유형</a>을 참조 바랍니다.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">데이터 디스크</a></td><td>선택</td><td>CVM의 스토리지 용량 확장에 사용되며, 안전하고 효율적인 스토리지 디바이스를 제공합니다. 기본적으로 CBS 데이터 디스크가 추가되어 있지 않습니다.</br>CBS에 대한 더 자세한 설명은 <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS 유형</a>을 참조하십시오.</td></tr>
<tr><td>공용 네트워크 대역폭</td><td>필수</td><td>기본적으로 독립적인 공용 IP가 무료로 할당됩니다. </br>Tencent Cloud는 다음과 같은 두 가지 네트워크 과금 방식을 제공합니다. 실제 필요에 따라 0Mbps보다 큰 값을 설정하십시오. <ul><li><b>대역폭 과금</b>: 고정 대역폭을 선택하여 해당 대역폭 초과 시 패킷이 손실됩니다. 네트워크 변동이 적은 시나리오에 적합합니다. </li><li><b>트래픽 과금</b>: 실제 트래픽 사용량을 기준으로 과금됩니다. 예기치 않은 트래픽으로 인한 비용 발생을 방지하기 위해 대역폭 피크값을 제한할 수 있으며, 순간 대역폭이 해당 값을 초과하면 패킷이 손실됩니다. 네트워크 변동이 큰 시나리오에 적합합니다. </li><li><b>BWP 과금</b>: 서비스 중인 공용 네트워크 트래픽의 피크 타임이 서로 다른 시간대에 분포되어 있을 때 BWP를 통한 대역폭 집계 과금이 가능합니다. 대규모 비즈니스, 특히 공용 네트워크의 각 인스턴스 간에 트래픽 피크가 형성되는 시나리오에 적합합니다. <br>BWP는 현재 베타 버전으로, 사용을 원하는 경우 <a href="https://intl.cloud.tencent.com/apply/p/86ulv50u1e8"> 베타 신청</a>양식을 제출하십시오. </li></ul><b>주의 사항</b>: <ul><li>무료로 할당된 독립적인 공용 IP 주소는 인스턴스와의 바인딩을 해제할 수 없습니다. 해당 IP 주소의 바인딩을 해제해야 하는 경우 해당 공용 IP를 EIP로 전환한 뒤 해제할 수 있습니다. EIP에 대한 더 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a>를 참조하십시오. </li><li>다음 두 가지 경우에는 현재 독립적인 공용 IP를 할당할 수 없습니다. 실제 구매 페이지를 참조하십시오.
<ul><li>IP 리소스가 품절된 경우</li><li>일부 리전의 경우</li></ul></li></ul></td></tr>
<tr><td>공용 게이트웨이</td><td>선택</td><td>Linux 관련 이미지에만 사용됩니다.</br>공용 게이트웨이란 사설 네트워크와 공용 네트워크의 인터페이스로, 사설 네트워크의 다른 서브넷에서 공인 IP가 없는 CVM 요청을 포워딩할 수 있습니다.</br><b>주의 사항: </b>2019년 12월 6일부터 Tencent Cloud는 CVM 구매 페이지에서의 공용 게이트웨이 구성 선택을 지원하지 않습니다. 필요한 경우 <a href="https://intl.cloud.tencent.com/document/product/213/34835">공용 게이트웨이 구성</a>을 참조하여 직접 구성하실 수 있습니다.</td></tr> 
<tr><td>수량</td><td>필수</td><td>구매할 CVM 수량을 나타냅니다.</td></tr>
</table>
3. [다음 단계: 호스트 설정]을 클릭하여 호스트 설정 페이지로 이동합니다.
4. 페이지 안내에 따라 다음의 정보를 구성합니다.
<table>
<tr><th style="width: 20%">유형</th><th style="width: 12%">필수/선택</th><th>구성 설명</th></tr>
<tr><td>서브 프로젝트</td><td>필수</td><td>기본 프로젝트로 설정되어 있으며, 실제 필요에 따라 이미 구축된 프로젝트를 선택하여 여러 CVM 관리에 사용할 수 있습니다.</td></tr>
<tr><td>보안 그룹</td><td>필수</td><td><ul><li>사용 가능한 보안 그룹이 없을 경우 [보안 그룹 생성]을 선택하실 수 있습니다.</li><li>사용 가능한 보안 그룹이 있을 경우 [기존 보안 그룹]을 선택하실 수 있습니다.</li></ul>보안 그룹에 대한 더 자세한 설명은<a href="https://intl.cloud.tencent.com/document/product/213/12452">보안 그룹</a>을 참조하십시오.</td></tr>
<tr><td>인스턴스 이름</td><td>선택</td><td>사용자 정의 항목으로, 생성할 CVM 이름을 나타냅니다.</br><ul><li>인스턴스 이름을 설정하지 않을 경우, 인스턴스 이름이 '이름 없음'으로 생성됩니다.</li><li>인스턴스 이름을 변경할 경우 60자 이내여야 하며, <a href="https://intl.cloud.tencent.com/document/product/213/32020">연속된 이름으로 일괄 생성하거나 지정 스트링 패턴으로 이름을 생성</a>할 수 있습니다.</li></ul><b>주의 사항</b>: 해당 이름은 콘솔에서만 표시되는 이름으로, CVM의 hostname이 아닙니다.</td></tr>
<tr><td>로그인 방식</td><td>필수</td><td>사용자의 실제 필요에 따라 CVM 로그인 방식을 설정합니다. <ul><li><b>비밀번호 설정</b>: 인스턴스 로그인에 사용할 비밀번호를 사용자 정의로 설정합니다. </li><li><b>키 즉시 연결(Linux 인스턴스에서만 지원)</b>: SSH 키를 연결합니다. SSH 키 방식을 통해 더욱 안전하게 CVM에 로그인할 수 있습니다.</br>키가 없거나 기존의 키가 부적합한 경우 [지금 생성]을 클릭하여 생성할 수 있습니다. SSH 키에 대한 더 자세한 정보는 <a href="http://cloud.tencent.com/doc/product/213/SSH%E5%AF%86%E9%92%A5">SSH 키</a>를 참조하십시오.</li><li><b>비밀번호 자동 생성</b>: 자동 생성된 비밀번호는 <a href="https://console.cloud.tencent.com/message">내부 메시지</a> 방식으로 발송됩니다.</li></ul></td></tr>
<tr><td>보안 강화</td><td>선택</td><td>DDoS 방어 및 HS 호스트 보호 기능이 무료로 활성화되도록 기본 설정되어 있으며, 서버 보안 체계를 구축해 데이터 유출을 방지할 수 있습니다.</td></tr>
<tr><td>클라우드 모니터링</td><td>선택</td><td>클라우드 서비스 모니터링이 무료로 활성화되도록 기본 설정되어 있습니다. 설치 컴포넌트가 획득한 호스트 모니터링 지표를 모니터링 아이콘 형식으로 표시하며, 사용자 정의 알람 임계값을 설정할 수 있습니다. 또한 3차원 CVM 데이터 모니터링, 스마트 데이터 분석, 실시간 장애 알람 및 커스터마이징 데이터 리포트 설정을 제공하므로, 서비스와 CVM 상태를 정확하게 파악할 수 있습니다.</td></tr>
<tr><td>고급 설정</td><td>선택</td><td>실제 필요에 따라 더 다양한 인스턴스를 구성할 수 있습니다.<ul><li><b>호스트 이름</b>: CVM 운영 체제 내의 컴퓨터 이름을 설정할 수 있으며, CVM 생성 후 CVM에 로그인하여 조회할 수 있습니다.</li><li><b>배치 그룹</b>: 필요에 따라 인스턴스를 배치 그룹에 추가하여 비즈니스의 가용성을 높일 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/15486">배치 그룹</a>을 참조하여 설정할 수 있습니다.</li><li><b>태그</b>: 태그를 설정하면 CVM의 리소스를 분류하여 관리할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/19548">태그</a>를 참조하여 설정할 수 있습니다.</li><li><b>사용자 정의 데이터</b>: 지정된 사용자 정의 데이터로 인스턴스를 구성하여, 인스턴스 실행 시 해당 설정의 스크립트를 실행합니다. 한 번에 여러 대의 CVM을 구매할 경우, 사용자 정의 데이터가 모든 CVM에서 실행됩니다. Linux 운영 체제에서는 Shell 형식을, Windows 운영 체제에서는 PowerShell 형식을 지원하며, 최대 16KB의 원시 데이터를 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/17525">사용자 정의 데이터</a>를 참조하십시오.</br><b>주의 사항</b>: Cloudinit 서비스를 포함하는 일부 공용 이미지에만 사용자 정의 데이터 구성을 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/19670">Cloud-Init</a>을 참조하십시오.</li></ul></td></tr>
</table>
5. [다음 단계: 구성 정보 확인]을 클릭하여 구성 정보 확인 페이지로 이동합니다.
6. 구매한 CVM 정보를 확인하고, 각 항목 구성의 비용을 파악합니다.
7. [<Tencent Cloud 서비스 계약>]를 읽고 동의에 체크합니다.
8. [구매하기]/[활성화]를 클릭하여 결제를 완료합니다. 결제를 완료하면 [CVM 콘솔](https://console.cloud.tencent.com/cvm)에서 CVM을 확인하실 수 있습니다.
CVM의 인스턴스 이름, 공용 IP 주소, 내부 IP 주소, 로그인 아이디, 초기 로그인 비밀번호 등의 정보는 계정의 [내부 메시지](https://console.cloud.tencent.com/message)로 계정에 전송되며, 이 정보로 인스턴스에 로그인하여 관리할 수 있습니다. 호스트 보안을 위해 CVM 로그인 비밀번호를 신속히 변경하시길 권장합니다.





