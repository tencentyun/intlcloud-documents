사용자 정의 구성에서는 더 풍부한 이미지 플랫폼과 스토리지, 대역폭 및 보안 그룹 등의 고급 설정을 제공하므로, 필요에 따라 적합한 구성을 선택해 사용하실 수 있습니다. 본 문서는 사용자 정의 구성을 예로 들어 소개합니다.

## 가입 및 인증

CVM을 사용하기 전에 다음의 준비 작업을 완료해야 합니다.
1. Tencent Cloud에 계정을 생성하고 실명 인증을 완료합니다.
신규 사용자는 Tencent Cloud 공식 홈페이지에 [가입](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F)해야 합니다. 자세한 작업 방식은 [Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)을 참조 바랍니다.
2. [Tencent Cloud CVM 소개 페이지](https://intl.cloud.tencent.com/product/cvm)로 이동하여 [구매하기]를 클릭합니다.

<span id="SelectType"></span>
## 모델 선택

>
1. 페이지 안내에 따라 다음의 정보를 구성합니다.
![리전 및 모델 선택](https://main.qcloudimg.com/raw/07493412dd043911fe8aa3ecb0d0bcd4.png)
<table>
<tr><th style="width: 20%">유형</th><th style="width: 12%">필수/선택</th><th>구성 설명</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/213/2180">과금 방식</a></td><td>필수</td><td><ul><li><b>종량제</b>: CVM의 유연한 과금 방식입니다.</li></ul></td></tr>
<tr><td>리전</td><td>필수</td><td>고객과 가장 가까운 리전을 선택하여, 액세스의 딜레이를 낮추고 속도를 높이기를 권장합니다.</td></tr>
<tr><td>가용존</td><td>필수</td><td>실제 필요에 따라 선택하세요.</br>여러 대의 CVM을 구매해야 할 경우, 다른 가용존을 선택하여 재해 복구 효과를 체험하시길 권장합니다.</td></tr>
<tr><td>네트워크</td><td>필수</td><td>Tencent Cloud에서 구축한 로직이 분리된 가상 네트워크를 나타내는 것으로, 하나의 VPC는 최소 하나의 서브넷으로 구성됩니다. 시스템에서는 사용자를 위해 각 리전에 기본 VPC 및 서브넷을 제공합니다.</br>
기존의 VPC/서브넷이 사용자의 요구에 맞지 않는다면 VPC 콘솔에서 생성할 수 있습니다.</br><b>주의 사항</b>: <ul><li>동일한 VPC의 리소스는 내부 네트워크 통신으로 기본 설정되어 있습니다.</li><li>구매 시, CVM과 동일한 가용존 속성을 가진 서브넷에서 CVM을 생성해야 합니다.</li></ul></td></tr>
<tr><td>인스턴스</td><td>필수</td><td>Tencent Cloud는 기본 하드웨어 차이에 따라, 여러 종류의 인스턴스 유형을 제공하고 있습니다. 최적의 성능을 원한다면 최신 인스턴스 유형을 사용하시길 권장합니다.</br>인스턴스에 대한 더 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/11518">인스턴스 사양</a>을 참조 바랍니다.</td></tr>
<tr><td>이미지</td><td>필수</td><td>Tencent Cloud는 공용 이미지, 사용자 정의 이미지, 공유 이미지를 제공하므로, <a href="https://intl.cloud.tencent.com/document/product/213/4941">이미지 유형</a>을 참조하여 선택하실 수 있습니다.</br>Tencent Cloud를 처음 사용할 경우, 공용 이미지를 선택하시길 권장합니다. Windows 운영 체제 정품이 활성화되어 있어 추가로 비용을 부담할 필요가 없습니다(북미 지역 제외). </td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">시스템 디스크</a></td><td>필수</td><td>운영 체제 설치에 사용되며, 기본 용량은 50GB입니다.</br>리전에 따라 선택 가능한 CBS 유형이 달라질 수 있으므로, 실제 페이지 안내에 따라 선택하시기 바랍니다.</br>CBS에 대한 더 자세한 설명은 <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS 유형</a>을 참조 바랍니다.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">데이터 디스크</a></td><td>선택</td><td>CVM의 스토리지 용량 확장에 사용되며, 안전하고 효율적인 스토리지 디바이스를 제공합니다. 기본적으로 CBS 데이터 디스크가 추가되어 있지 않습니다.</br>CBS에 대한 더 자세한 설명은 <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS 유형</a>을 참조 바랍니다.</td></tr>
<tr><td>공용 네트워크 대역폭</td><td>필수</td><td>Tencent Cloud는 다음의 두 가지 네트워크 과금 방식을 제공하므로, 실제 필요에 따라 선택하시기 바랍니다.<ul><li><b>대역폭 과금</b>: 고정 대역폭을 선택하여, 해당 대역폭을 초과할 시 패킷이 손실됩니다. 네트워크 변동이 적은 시나리오에 적합합니다.</li><li><b>트래픽 과금</b>: 실제 트래픽 사용량에 따라 과금됩니다. 대역폭 피크 값을 제한하여 예기치 않은 트래픽으로 인한 비용을 방지할 수 있으며, 순간 대역폭이 해당 값을 초과할 시 패킷이 손실됩니다. 네트워크 변동이 큰 시나리오에 적합합니다.</li></ul></td></tr>
<tr><td>수량</td><td>필수</td><td>구매할 CVM 수량을 나타냅니다.</td></tr>
</table>
2. [다음 단계: 호스트 설정]을 클릭하여 호스트 설정 페이지로 이동합니다.

## 호스트 설정
1. 페이지 안내에 따라 다음의 정보를 구성합니다.
![보안 그룹 및 호스트](https://main.qcloudimg.com/raw/a1aff1911b9e82506e93c591dd69ee26.png)
<table>
<tr><th style="width: 20%">유형</th><th style="width: 12%">필수/선택</th><th>구성 설명</th></tr>
<tr><td>서브 항목</td><td>필수</td><td>기본 항목으로 설정되어 있으며, 실제 필요에 따라 이미 구축된 항목을 선택하여 여러 CVM 관리에 사용할 수 있습니다.</td></tr></td></tr>
<tr><td>보안 그룹</td><td>필수</td><td>단일 또는 여러 CVM의 네트워크 액세스 제어에 사용됩니다.</br><b>3389 로그인 포트가 개방되었는지 확인하시기 바랍니다.</br>더 자세한 정보는 <a href="https://intl.cloud.tencent.com/document/product/213/12452">보안 그룹</a>을 참조 바랍니다.</td></tr>
<tr><td>인스턴스 이름</td><td>선택</td><td>생성할 CVM 이름을 나타냅니다.</br>사용자 정의로 설정할 수 있으며, "CVM-01"로 생성할 것을 권장합니다.</td></tr>
<tr><td>로그인 방식 </td><td>필수</td><td> 사용자의 실제 필요에 따라 CVM 로그인 방식을 설정합니다. <ul><li><b>비밀번호 설정</b>: 인스턴스 로그인에 사용할 비밀번호를 사용자 정의로 설정합니다. <li><li><b>비밀번호 자동 생성</b>: 자동 생성된 비밀번호는 <a href="https://console.cloud.tencent.com/message">내부 메시지</a> 방식으로 발송됩니다.</li></ul></td></tr>
<tr><td>보안 강화</td><td>선택</td><td>무료로 활성화되도록 기본 설정되어 있으며, 서버 보안 체계를 구축해 데이터 유출을 방지할 수 있습니다.</td></tr>
<tr><td>클라우드 모니터링</td><td>선택</td><td>무료로 활성화되도록 기본 설정되어 있으며, 3차원 CVM 데이터 모니터링, 스마트 데이터 분석, 실시간 장애 알람 및 커스터마이징 데이터 리포트 설정을 제공하므로, 서비스와 CVM의 상태를 정확하게 파악할 수 있습니다.</td></tr>
<tr><td>고급 설정</td><td>선택</td><td>실제 필요에 따라 더 다양한 인스턴스를 구성할 수 있습니다.<ul><li><b>호스트 이름</b>: CVM 운영 체제 내의 컴퓨터 이름을 설정할 수 있으며, CVM 생성 후 CVM에 로그인하여 조회할 수 있습니다.</li><li><b>CAM 역할</b> : CAM 역할을 설정한 뒤, CVM과 리소스에 접근하고 Tencent Cloud에서 작업할 수 있는 권한을 부여할 수 있습니다. 자세한 설정은<a  href="https://intl.cloud.tencent.com/document/product/213/38290"> [역할 관리]</a> 를 참고하세요.</li><li><b>배치 그룹</b>: 필요에 따라 인스턴스를 배치 그룹에 추가하여 비즈니스의 가용성을 높일 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/15486">배치 그룹</a>을 참조하여 설정할 수 있습니다.</li><li><b>태그</b>: 태그를 설정하면 CVM의 리소스를 분류하여 관리할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/19548">태그</a>를 참조하여 설정할 수 있습니다.</li><li><b>사용자 정의 데이터</b>: 지정된 사용자 정의 데이터로 인스턴스를 구성하여, 인스턴스 실행 시 해당 설정의 스크립트를 실행합니다. 한 번에 여러 대의 CVM을 구매할 경우, 사용자 정의 데이터가 모든 CVM에서 실행됩니다. Windows 운영 체제에서는 PowerShell 형식을 지원하며, 최대 16KB의 원시 데이터를 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/17525">사용자 정의 데이터</a>를 참조 바랍니다.</br><b>주의 사항</b>: Windows 공용 이미지에만 사용자 정의 데이터 구성을 지원합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/19670">cloudbase-init</a>을 참조 바랍니다.</li></ul></td></tr>
</table>
2. [다음 단계: 구성 정보 확인]을 클릭하여 구성 정보 확인 페이지로 이동합니다.

## 구성 정보 확인

1. 구매한 CVM 정보를 확인하고, 각 구성의 비용을 파악합니다.
2. [구매하기]/[활성화]를 클릭하여 결제를 완료합니다. 결제를 완료하면 [CVM 콘솔][https://console.cloud.tencent.com/cvm]에서 CVM을 확인하실 수 있습니다.
CVM의 인스턴스 이름, 공인 IP 주소, 개인 IP 주소, 로그인 아이디, 초기 비밀번호 등의 정보는 계정의 [내부 메시지](https://console.cloud.tencent.com/message)로 전송되며, 이 정보로 인스턴스에 로그인하여 관리할 수 있습니다. 호스트 보안을 위해 CVM 로그인 비밀번호를 신속히 변경하시길 권장합니다.

## 인스턴스 로그인 및 연결

CVM 작업 완료 후, Tencent Cloud 콘솔을 통해 CVM에 로그인하여 실제 필요에 따라 스테이션 구축 등의 작업을 실행할 수 있습니다.
Tencent Cloud 콘솔을 통해 CVM에 로그인하려면, 실제 필요에 따라 적합한 로그인 방식을 선택하시기 바랍니다.
- [RDP 파일을 사용하여 Windows 인스턴스 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5435)
- [원격 데스크톱을 사용하여 Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32498)

## 데이터 디스크 포맷 및 파티션

[모델 선택](#SelectType)에서 데이터 디스크를 추가했다면, 인스턴스에 로그인하여 데이터 디스크의 포맷 및 파티션을 진행해야 합니다. **데이터 디스크를 추가하지 않았다면 이 단계를 건너뛸 수 있습니다.**
디스크 용량 크기와 CVM 운영 체제에 따라 적합한 작업 가이드를 선택하시기 바랍니다.
- 디스크 용량이 2TB 미만인 경우
[CBS 초기화(Windows)](https://intl.cloud.tencent.com/document/product/362/31597)
- 디스크 용량이 2TB 이상인 경우
[CBS 초기화(Windows)](https://intl.cloud.tencent.com/document/product/362/31598)

더 자세한 작업 가이드는 [초기화 시나리오 설명](https://intl.cloud.tencent.com/document/product/362/31596)을 참조 바랍니다.
