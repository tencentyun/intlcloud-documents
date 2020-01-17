### 작업 시나리오

본 문서는 사용자 정의 구성 방법을 예로 들어 Tencent Cloud의 클라우드 서버(Cloud Virtual Machine，CVM)인스턴스를 생성하는 방법을 안내합니다.

### 전제 조건

CVM 인스턴스를 생성하기 전 다음 작업을 완료해야 합니다.
- [Tencent Cloud 계정 등록](https://intl.cloud.tencent.com/document/product/378/17985) 및 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629) 을 완료하십시오.
- VPC의 CVM 인스턴스를 위한 네트워크 유형을 생성하려면 목표 리전에 [VPC 생성](https://cloud.tencent.com/document/product/215/20109) 하고 VPC의 목표 가용존에 [서브넷 생성](https://cloud.tencent.com/document/product/215/20110) 을 완료합니다.
- 시스템이 자동으로 생성한 기본 프로젝트를 사용하지 않을 경우 [프로젝트 생성](https://cloud.tencent.com/document/product/378/10861)이 필요합니다.
- 시스템 자동으로 생성된 기본 보안 그룹을 사용하지 않을 경우 목표 리전에 [보안 그룹 생성](https://intl.cloud.tencent.com/document/product/213/18197) 하고 사용자 서비스 수요를 충족할 수 있는 보안 그룹 규칙을 추가합니다.
- Linux 인스턴스를 생성할 경우 SSH 키 쌍을 바인딩하려면 목표 프로젝트에 [SSH 키 생성](https://intl.cloud.tencent.com/document/product/213/16691) 이 필요합니다.
- 사용자 정의 이미지의 CVM 인스턴스를 생성해야 할 경우 [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942) 또는 [미러 이미지 가져오기](https://intl.cloud.tencent.com/document/product/213/4945) 를 실행합니다.

## 작업 순서

1. [Tencent Cloud 공식 사이트](https://cloud.tencent.com)에 로그인한 후[제품]>[기본]>[컴퓨팅]>[[CVM](https://intl.cloud.tencent.com/product/cvm)]선택 및[지금 구매]를 클릭하고 CVM 구매 페이지로 들어가십시오.
 - **[빠른 구성](https://buy.cloud.tencent.com/cvm?tab=lite)：** 일반 환경에서 사용하기 적합하고 사용자의 요구에 부합되는 CVM 인스턴스를 선택할 수 있습니다
 - **[사용자 정의 구성](https://buy.cloud.tencent.com/cvm?tab=custom)：** 특정 환경에서 사용하기 적합하고 사용자의 특정 요구에 부합되는 CVM 인스턴스를 선택할 수 있습니다.
2. 페이지 알림에 따라 다음 정보를 구성하십시오.
<table>
<tr><th style="width: 20%">유형</th><th style="width: 12%">필수/선택</th><th>구성 설명</th></tr>
<tr><td>청구 모드</td><td>필수</td><td>실제 수요에 따라 선택하십시오：<ul><li><b>종량제</b>：CVM의 탄력적 청구 모드는 전자 상거래 사재기 등 장치 수요가 순간적으로 크게 변동하는 시나리오에 적용됩니다.</li><li><b>스팟 인스턴스</b>：일종의 새 인스턴스 작업 모드로써 빅 데이터 컴퓨팅, CLB 온라인 서비스 및 웹 사이트 서비스 등 시나리오에 적용되며 일반 가격 범위는 온디맨드 요금의 10%-20%입니다. <li></ul>청구 모드에 대한 자세한 내용은<a href="https://intl.cloud.tencent.com/document/product/213/2180">에서 청구 모드 설명을</a>참조하십시오.</td></tr>
<tr><td>리전/가용존</td><td>필수</td><td><ul><li><b>리전</b>：액세스 지연시간을 줄이고 액세스 속도를 향상하려면 고객과 가장 가까운 리전을 선택하는 것을 권장합니다.<li><li><b>가용존</b>：실제 수요에 따라 선택하십시오. <br>여러 CVM을 구매해야 할 경우 장애 복구를 위해 다양한 가용존을 선택하는 것을 권장합니다.</li></ul>선택 가능한 리전 및 가용존에 대한 소개는<a href="https://cloud.tencent.com/document/product/213/6091">리전 및 가용존</a>을 참조하십시오.</td></tr>
<tr><td>네트워크</td><td>필수</td><td>Tencent Cloud에 구축된 논리적 격리를 나타내는 네트워크 용량으로써 VPC는 적어도 하나의 서브넷으로 구성됩니다. 시스템은 사용자를 위해 각 리전에 기본 VPC 및 서브넷을 제공합니다.<br>
기존 VPC/서브넷이 사용자 수요를 충족하지 않으면 VPC 콘솔에서 생성할 수 있습니다. br><b>주의 사항</b>：<ul><li>동일한 VPC에서 리소스는 기본 인트라넷에 의해 상호 연결됩니다.</li><li>구매할 때 CVM과 가용존 속성이 같은 서브넷에 CVM을 생성해야 합니다.</li></ul></td></tr>
<tr><td>인스턴스</td><td>필수</td><td>Tencent Cloud는 낮은 레이어 하드웨어에 따라 현재 다양한 인스턴스 유형을 제공합니다. 최상의 성능을 얻기 위해 차세대 인스턴스 유형을 사용할 것을 권장합니다.<br>
더 많은 인스턴스에 관한 자세한 내용은<a href="https://intl.cloud.tencent.com/document/product/213/11518">인스턴스 규격</a>을 참조하십시오.</td></tr>
<tr><td>미러 이미지</td><td>필수</td><td>Tencent Cloud는 공용 이미지, 사용자 정의 이미지, 공유 이미지 및 마켓플레이스를 제공하므로<a href="https://intl.cloud.tencent.com/document/product/213/4941">에서 미러 이미지 유형을 참조하고</a>선택하십시오.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">시스템 디스크</a></td><td>필수</td><td>운영 체제 설치에 사용되는 기본 값은 50GB입니다.</br>다양한 리전은 CBS 유형의 선택에 영향을 줄 수 있으므로 실제 페이지의 알림에 따라 선택하십시오.</br>CBS에 대한 자세한 내용은<a href="https://intl.cloud.tencent.com/document/product/362/31636">에서 CBS 유형을</a>참조하십시오.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">데이터 디스크</a></td><td>선택</td><td>CVM의 스토리지 용량 확장에 사용되며 효율적이고 신뢰할 수 있는 스토리지 장치를 제공합니다. 기본 CBS 데이터 디스크는 추가하지 않습니다.</br>CBS에 대한 자세한 내용은<a href="https://intl.cloud.tencent.com/document/product/362/31636">에서 CBS 유형을</a>참조하십시오.</td></tr>
<tr><td>공용 네트워크 대역폭</td><td>필수</td><td>무료로 독립된 공용 네트워크 IP 주소를 할당합니다.</br>Tencent Cloud는 다음과 같이 두 가지 네트워크 청구 방식을 제공하므로 실제 수요에 따라 0Mbps보다 큰 값을 설정하십시오. <ul><li><b>대역폭 과금</b>：고정 대역폭을 선택하면 본 대역폭을 초과 시 패킷합니다. 네트워크 변동이 적은 환경에 적합합니다. <li><li><b>트래픽 사용량에 따라 과금</b>：실제 사용한 트래픽에 따라 청구합니다. 피크 대역폭을 제한하면 우발적으로 발생하는 트래픽 요금을 절감할 수 있으며 대역폭이 해당 값을 초과하면 제한합니다. 네트워크 변동이 큰 환경에 적합합니다.</li></ul><b>주의 사항</b>：무료로 할당된 독립적인 공용 네트워크 IP 주소는 인스턴스와 바인딩 해제할 수 없습니다. 해당 IP 주소를 바인딩 해제하려면 공용 네트워크 IP 주소를 EIP로 전환한 후 다시 바인딩 해제하십시오. EIP에 관한 자세한 내용은 <a href="https://cloud.tencent.com/document/product/213/5733">EIP</a>를 참조하십시오.</td></tr>
<tr><td>공용 게이트웨이</td><td>선택</td><td>Linux관련 미러 이미지만 해당합니다.</br>공용망 게이트웨이는 VPC와 공용 네트워크의 일종 인터페이스로서 VPC의 다양한 서브넷에 공용 IP가 없는 CVM 요청을 전달할 수 있습니다. </br>자세한 내용은<a href="https://cloud.tencent.com/document/product/215/20078">공용망 게이트웨이</a>를 참조하십시오,</td></tr> 
<tr><td>수량</td><td>필수</td><td>구매할 CVM 수량을 표시합니다.</td></tr>  
</table>
3. [다음 단계：호스트 설정]을 클릭하고 호스트 설정 페이지도 들어가십시오.
4. 페이지의 알람에 따라 다음 정보를 구성하십시오.
<table>
<tr><th style="width: 20%">유형</th><th style="width: 12%">필수/선택</th><th>구성 설명</th></tr>
<tr><td>서브 프로젝트</td><td>필수</td><td>기본적인 프로젝트로써 실제 수요에 따라 구축된 프로젝트를 선택하고 다양한 CVM 관리에 사용할 수 있습니다.</td></tr></td></tr>
<tr><td>보안 그룹</td><td>필수</td><td><ul><li>사용 가능한 보안 그룹이 없다면[보안 그룹 생성]을 선택할 수 있습니다.</li><li>사용 가능한 보안 그룹이 있다면[기존 보안그룹]을 선택할 수 있습니다.</li></ul>보안 그룹에 대한 자세한 내용은<a href="https://cloud.tencent.com/document/product/213/12452">보안그룹</a>을 참조하십시오.</td></tr>
<tr><td>인스턴스 이름</td><td>선택</td><td>사용자 정의는 생성해야 할 CVM 이름을 표시합니다.</br><ul><li>인스턴스 이름을 정의하지 않을 경우 인스턴스를 생성한 후 이름은 “이름 없음”으로 됩니다.</li><li>인스턴스 이름을 정의할 경우 인스턴스 이름은 60자 이내로 제한하거나 <a href="https://cloud.tencent.com/document/product/213/34343">일괄 연속 명명 및 지정된 패턴 명명으로 지정할 수 있습니다</a>.</li></ul><b>주의 사항</b>：해당 이름은 콘솔에서만 표시되는 이름이며 CVM의 hostname은 아닙니다.</td></tr>
<tr><td>로그인 방식</td><td>필수</td><td>사용자의 실제 수요에 따라 CVM 로그인 방식을 설정하십시오.<ul><li><b>비밀번호 설정</b>：사용자 정의로 인스턴스 로그인의 비밀번호를 설정하십시오.<li><li><b>지금 키를 연결하십시오.（Linux 인스턴스만 지원함）</b>：SSH 키 연결은 SSH 키 방식을 통해 CVM에 보다 안전하게 로그인할 수 있습니다.</br>키가 없거나 기존 키가 부적합한 경우[지금 생성]을 클릭하여 생성할 수 있습니다. SSH 키에 대한 자세한 정보는<a href="http://cloud.tencent.com/doc/product/213/SSH%E5%AF%86%E9%92%A5">에서 SSH 키</a>를 참조하십시오.</li><li><b>비밀번호 자동 생성</b>：자동으로 생성된 비밀번호는<a href="https://console.cloud.tencent.com/message">내부 메시지</a> 방식으로 전송됩니다.</li></ul></td></tr>
<tr><td>보안 강화</td><td>선택</td><td>DDoS 보호 및 Host Security 호스트 보호는 무료로 활성화하고 사용자가 서버 보안 시스템을 구축하고 데이터 유출을 방지할 수 있도록 지원합니다.</td></tr>
<tr><td>클라우드 모니터링</td><td>선택</td><td>기본적으로 클라우드 서비스 모니터링은 무료로 활성화됩니다. 구성 요소를 설치하면 호스트 모니터링 메트릭은 모니터링 아이콘으로 표시되며 사용자 정의 알람의 임계 값 설정을 지원합니다. 또한 입체화 CVM 데이터 모니터링, 스마트한 데이터 분석, 실시간 장애 알람 및 개성화 데이터 리포트 구성을 제공하여 사용자가 서비스 및 CVM 상태를 정확하게 파악할 수 있습니다.</td></tr>
<tr><td>고급 설정</td><td>선택</td><td>실제 수요에 따라 인스턴스를 구성하십시오.<ul><li><b>호스트 이름</b>：사용자가 CVM 운영 체제 내부의 컴퓨터 이름을 정의 할 수 있고, CVM이 성공적으로 생성한 후 로그인하여 내부를 조회할 수 있습니다.</li><li><b>배치그룹</b>：수요에 따라 인스턴스를 배치 그룹에 추가하여 서비스 가용성을 향상시킬 수 있습니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/213/15486">배치그룹</a>에서 설정하십시오.</li><li><b>태그</b>：태그를 설정한 후 CVM에 대해 리소스를 분류하고 관리할 수 있습니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/213/19548">태그</a>에서 설정하십시오.</li><li><b>사용자 정의 데이터</b>：사용자 정의 데이터를 지정하여 인스턴스를 배치하고, 인스턴스가 시작될 때 구성을 실행하는 스크립트입니다. 한 번에 여러 대의 CVM을 구매하면 사용자 정의 데이터는 모든 CVM에서 실행됩니다. Linux 운영 체제는 shell 형식을 지원하고 Windows 운영 체제는 PowerShell 형식을 지원하며 최대로 16KB 로우 데이터를 지원합니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/213/17525">사용자 정의 데이터</a>를 참조하십시오.</br><b>주의 사항</b>：사용자 정의 데이터 구성은 Cloudinit 서비스를 사용하는 일부 공용 미러 이미지만 지원합니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/213/19670">Cloud-Init</a>를 참조하십시오.</li></ul></td></tr>
</table>
5.[다음 단계：구성 정보 확인]을 클릭하고 구성 정보 확인 페이지로 진입하십시오.
6. 구매한 CVM 정보를 확인하고 각 구성의 요금 명세서를 확인하십시오.
7. [지금 구매]를 클릭하고 결제를 완료하십시오. 결제가 완료되면 [CVM 콘솔](https://console.cloud.tencent.com/cvm) 에서 CVM을 조회할 수 있습니다.
CVM 인스턴스 이름, 공용 네트워크 IP 주소, 개인 IP 주소, 로그인 이름, 초기 로그인 비밀번호 등 정보를 [내부 메시지](https://console.cloud.tencent.com/message) 방식으로 계정에 전송됩니다. 이 정보로 인스턴스를 로그인 및 관리할 수 있으며 호스트의 보안성을 보장하기 위해 CVM 로그인 비밀번호를 변경하십시오.





