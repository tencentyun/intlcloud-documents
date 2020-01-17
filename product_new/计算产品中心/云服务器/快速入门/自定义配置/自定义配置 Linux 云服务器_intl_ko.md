CVM 빠른 구성과 비교하여 사용자 정의 구성은 더 많은 미러 이미지 플랫폼과 스토리지, 대역폭 및 보안 그룹 등 고급 설정을 제공하므로 사용자는 필요에 따라 적합한 구성을 선택할 수 있습니다. 본 문서에서는 사용자 정의 구성을 예로 들어 소개합니다.
– 사용자가 빠른 구성을 통해 CVM을 생성할 경우 [Linux CVM 빠른 구성](http://intl.cloud.tencent.com/document/product/213/2936)을 참조하여 구성을 실행하십시오.

## 등록 및 인증

CVM를 사용하기 전 다음과 같은 준비 작업을 완료해야 합니다.
1. Tencent Cloud 계정 등록 및 실명 인증을 완료하십시오.
신규 사용자는 Tencent Cloud 공식 사이트에서 [등록](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F)을 진행해야 합니다. 자세한 내용은 [Tencent Cloud 등록](https://intl.cloud.tencent.com/document/product/378/17985)을 참조하십시오.
2. [Tencent Cloud CVM 소개 페이지](https://intl.cloud.tencent.com/product/cvm)를 액세스하고 [즉시상담]을 클릭합니다.

<span id="SelectType"></span>
## 모델 선택
> 처음으로 계정을 구매할 경우 [빠른 구성] 페이지로 진입합니다. 사용자가 이미 CVM을 구매한 경우 기본으로 [사용자 정의 구성] 페이지로 진입합니다. CVM을 구매하지 않은 경우 [사용자 정의 구성]을 선택하고 작업을 실행하십시오.
>
1. 페이지 알림에 따라 다음 정보를 구성하십시오.
![리전과 모델 선택](https://main.qcloudimg.com/raw/a71d4168ae6bd2b762badd4689c0aba7.png)
<table>
<tr><th style="width: 20%">유형</th><th style="width: 12%">필수/선택</th><th>구성 설명</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/213/2180">과금 방식</a></td><td>필수</td><td>실제 필요에 따라 선택하십시오.<ul><li><b>종량제</b>: CVM의 유연한 과금 방식은 전자 상거래의 대량 구매 등 장치 수요가 순간 변동량이 큰 시나리오에 적합합니다.</li><li><b>스팟 인스턴스</b>: 일종의 새 인스턴스 작업 모드로써 빅 데이터 컴퓨팅, CLB, 온라인 서비스 및 네트워크 서비스 등 시나리오에 적합하며 일반적인 가격 범위는 종량제 요금의 10%~20%사이 입니다.</li></ul></td></tr>
<tr><td>리전</td><td>필수</td><td>사용자의 고객과 가장 가까운 리전을 선택하여 액세스 딜레이 시간을 낮추고 액세스 속도를 높일 것을 권장합니다.</td></tr>
<tr><td>가용존</td><td>필수</td><td>실제 요구 사항에 따라 선택하십시오.</br>여러 대의 CVM을 구매해야 할 경우 서로 다른 가용존을 선택하여 재해 복구 효과를 실현할 것을 권장합니다.</td></tr>
<tr><td>네트워크</td><td>필수</td><td>Tencent Cloud에 구축된 논리적 격리를 나타내는 네트워크 용량으로써 VPC는 최소 하나의 서브넷으로 구성됩니다. 시스템은 사용자를 위해 각 리전에 기본 VPC 및 서브넷을 제공합니다.<br>
기존 VPC/서브넷이 사용자의 요구사항을 충족하지 못한 경우 VPC 콘솔에서 생성할 수 있습니다. </br><b>주의 사항</b>: <ul><li>동일한 VPC에서 리소스는 기본으로 내부 네트워크를 상호 연결합니다.</li><li>구매할 때 CVM과 가용존 속성이 동일한 서브넷에서 CVM을 생성해야 합니다.</li></ul></td></tr>
<tr><td>인스턴스</td><td>필수</td><td>하위 하드웨어 레이어에 따라 Tencent Cloud는 현재 다양한 인스턴스 유형을 제공합니다. 최적의 성능을 얻기 위해 차세대 인스턴스 유형을 사용하는 것을 권장합니다.</br>인스턴스에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/11518">인스턴스 사양</a>을 참조하십시오.</a>.</td></tr>
<tr><td>미러 이미지</td><td>필수</td><td>Tencent Cloud는 공용 이미지, 사용자 정의 이미지, 공유 이미지 및 마켓플레이스를 제공하므로 <a href="https://intl.cloud.tencent.com/document/product/213/4941">미러 이미지 유형</a>을 참조하여 선택하십시오.</br>Tencent Cloud를 처음으로 사용하는 사용자는 공용 네트워크 미러 이미지를 선택하길 권장합니다.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">시스템 디스크</a></td><td>필수</td><td>운영 체제 설치에 사용되는 기본 용량은 50GB입니다.</br>다양한 리전은 CBS 유형의 선택에 영향을 줄 수 있으므로 실제 페이지의 알림에 따라 선택하십시오.</br>CBS에 대한 자세한 내용은<a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS 유형</a>을 참조하십시오.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">데이터 디스크</a></td><td>선택</td><td>CVM의 스토리지 용량 확장에 사용되며 효율적이고 신뢰할 수 있는 스토리지 장치를 제공합니다. 기본 CBS 데이터 디스크는 추가하지 않습니다.</br>CBS에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS 유형</a>을 참조하십시오.</td></tr>
<tr><td>공용 네트워크 대역폭</td><td>필수</td><td>Tencent Cloud는 다음 2가지 네트워크 과금 방식을 제공하므로 실제 필요에 따라 선택하십시오.<ul><li><b>대역폭 과금</b>: 고정적인 대역폭을 선택하여 본 대역폭을 초과할 경우 패킷이 손실됩니다. 네트워크 변동이 적은 시나리오에 적합합니다.</li><li><b>트래픽 과금</b>: 실제 사용한 트래픽에 따라 과금합니다. 피크값 대역폭을 제한하여 예기치 않은 트래픽에 따른 비용을 피할 수 있으며 대역폭이 해당 값을 초과할 경우 패킷이 손실됩니다. 네트워크 변동이 큰 시나리오에 적합합니다.</li></ul></td></tr>
<tr><td>공용 게이트웨이</td><td>선택</td><td>공용망 게이트웨이는 VPC와 공용 네트워크의 일종 인터페이스로서 VPC의 다양한 서브넷에 공인 IP가 없는 CVM 요청을 전달할 수 있습니다. </br> </td></tr> 
<tr><td>수량</td><td>필수</td><td>구매할 CVM 수량을 표시합니다.</td></tr>  
</table>
2. [다음 단계: 호스트 설정]을 클릭하고 호스트 설정 페이지로 진입하십시오.

## 호스트 설정
1. 페이지 알림에 따라 다음 정보를 구성하십시오.
<table>
<tr><th style="width: 20%">유형</th><th style="width: 12%">필수/선택</th><th>구성 설명</th></tr>
<tr><td>세부 항목</td><td>필수</td><td>기본적인 프로젝트로써 실제 필요에 따라 구축된 프로젝트를 선택하고 다양한 CVM 관리에 사용할 수 있습니다.</td></tr></td></tr>
<tr><td>보안 그룹</td><td>필수</td><td>1대 또는 여러 대 CVM의 네트워크 액세스 제어 설정에 사용됩니다.</br><b>22 로그인 포트가 개방되었는지 확인하십시오. </br>자세한 내용은 <a href="https://cloud.tencent.com/document/product/213/12452">보안 그룹</a>을 참조하십시오.</td></tr>
<tr><td>인스턴스 이름</td><td>선택</td><td>생성해야 할 CVM 이름을 표시합니다.</br>사용자가 이름을 정의하고 "CVM-01"로 생성할 것을 권장합니다.</td></tr>
<tr><td>로그인 방식</td><td>필수</td><td>사용자의 실제 필요에 따라 CVM 로그인 방식을 설정하십시오.<ul><li><b>비밀번호 설정</b>: 사용자 정의로 인스턴스 로그인의 비밀번호를 설정하십시오.<li><li><b>키 즉시 연결</b>: SSH 키 연결은 SSH 키 방식을 통해 CVM에 보다 안전하게 로그인할 수 있습니다.</br>키가 없거나 기존 키가 부적합한 경우 [지금 생성]을 클릭하여 생성할 수 있습니다. SSH 키에 대한 자세한 정보는<a href="http://cloud.tencent.com/doc/product/213/SSH%E5%AF%86%E9%92%A5">SSH 키</a>를 참조하십시오.</li><li><b>비밀번호 자동 생성</b>: 자동으로 생성된 비밀번호는 <a href="https://console.cloud.tencent.com/message">내부 메시지</a> 방식으로 전송됩니다.</li></ul></td></tr>
<tr><td>보안 강화</td><td>선택</td><td>무료로 활성화하며 사용자가 서버 보안 체계를 구축하고 데이터 유출을 방지할 수 있도록 도와줍니다.</td></tr>
<tr><td>클라우드 모니터링</td><td>선택</td><td>무료로 활성화하며 3차원 CVM 데이터 모니터링, 스마트한 데이터 분석, 실시간 장애 알람 및 개성화된 데이터 리포트 구성을 제공하여 사용자가 서비스와 CVM 상태를 정확하게 파악할 수 있습니다.</td></tr>
<tr><td>고급 설정</td><td>선택</td><td>실제 필요에 따라 인스턴스를 구성하십시오.<ul><li><b>호스트 이름</b>: 사용자가 CVM 운영 체제 내부의 컴퓨터 이름을 정의할 수 있고, CVM이 성공적으로 생성한 후 로그인하여 내부를 조회할 수 있습니다.</li><li><b>배치 그룹</b>: 수요에 따라 인스턴스를 배치 그룹에 추가하여 서비스 가용성을 향상시킬 수 있습니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/213/15486">배치 그룹</a>에서 설정하십시오.</li><li><b>태그</b>: 태그를 설정한 후 CVM에 대해 리소스를 분류하고 관리할 수 있습니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/213/19548">태그</a>에서 설정하십시오.</li><li><b>사용자 정의 데이터</b>: 사용자 정의 데이터를 지정하여 인스턴스를 배치하고, 인스턴스가 시작될 때 구성을 실행하는 스크립트입니다. 한 번에 여러 대의 CVM을 구매하면 사용자 정의 데이터는 모든 CVM에서 실행됩니다. Linux 운영 체제는 shell 형식을 지원하며 최대 16KB의 로우 데이터를 지원합니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/213/17525">사용자 정의 데이터</a>를 참조하십시오.</br><b>주의 사항</b>: 사용자 정의 데이터 구성은 Cloudinit 서비스를 사용하는 일부 공용 미러 이미지만 지원합니다. 자세한 내용은 <a href="https://cloud.tencent.com/document/product/213/19670">Cloud-Init</a>를 참조하십시오.</li></ul></td></tr>
</table>
2. [다음 단계: 구성 정보 확인]을 클릭하고 구성 정보 확인 페이지로 진입하십시오.


## 구성 정보 확인

1. 각 구성 비용에 대한 자세한 내용은 구매한 CVM 정보를 확인하십시오.
2. [지금 구매]를 클릭하고 결제를 완료하십시오. 결제가 완료되면 [CVM 콘솔](https://console.cloud.tencent.com/cvm)에서 CVM을 조회할 수 있습니다.
CVM 인스턴스 이름, 공인 IP 주소, 개인 IP 주소, 로그인 이름, 초기 로그인 비밀번호 등 정보는 [내부 메시지](https://console.cloud.tencent.com/message)로 계정에 전송됩니다. 이 정보로 인스턴스를 로그인 및 관리할 수 있으며 호스트의 보안성을 보장하기 위해 CVM 로그인 비밀번호를 변경하십시오.

## 인스턴스 로그인 및 연결

CVM 작업 완료 후, Tencent Cloud 콘솔을 통해 CVM에 로그인하여 실제 필요에 따라 스테이션 구축 등 작업을 실행할 수 있습니다.
Tencent Cloud 콘솔을 통한 CVM 로그인 방법은 실제 필요에 따라 해당하는 로그인 방식을 선택하십시오.
- [표준 로그인 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)
- [소프트웨어 원격 로그인 방식으로 Linux 인스턴스에 로그인](https://cloud.tencent.com/document/product/213/35699)
- [SSH을 사용해 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)

## 데이터 디스크 파티션 및 포맷

[모델 선택](#SelectType) 시 데이터 디스크를 추가한 경우 인스턴스에 로그인한 후 데이터 디스크에 대해 포맷 및 파티션을 실행해야 합니다.**데이터 디스크를 추가하지 않은 경우 이 단계를 건너뛸 수 있습니다.**
디스크 용량 크기, CVM 운영 체제 유형에 따라 적합한 작업 가이드를 선택하십시오.
- 디스크 용량이 2TB 미만인 경우
 [CBS 초기화(Linux)](https://intl.cloud.tencent.com/document/product/362/6734)
- 디스크 용량이 2TB 이상인 경우
 [CBS 초기화(Linux)](https://intl.cloud.tencent.com/document/product/362/6735)

더 자세한 내용은 [초기화 시나리오 소개](https://intl.cloud.tencent.com/document/product/362/31596)를 참조하십시오.
