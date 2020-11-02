## 작업 시나리오
보안 그룹은 공용 네트워크나 내부 네트워크로부터의 액세스 요청의 통과 허가 여부 관리에 사용됩니다. 보안상의 이유로, 보안 그룹 인바운드의 대부분은 액세스 거부 정책을 취하고 있습니다. 보안 그룹을 생성 시 '모든 포트 개방' 템플릿이나 '22, 80, 443, 3389 포트 및 ICMP 프로토콜 개방' 템플릿을 선택한 경우, 시스템은 선택한 템플릿 유형에 따라 일부 통신 포트를 자동으로 보안 그룹 규칙에 추가합니다. 자세한 내용은 [보안 그룹 개요](https://intl.cloud.tencent.com/document/product/213/12452)를 참조 바랍니다.

본 문서는 보안 그룹 규칙을 추가하여, 보안 그룹 내 CVM 인스턴스의 공용 네트워크 및 내부 네트워크 액세스를 허용 또는 차단하는 방법을 안내합니다.

## 주의 사항

- 보안 그룹 규칙은 IPv4 보안 그룹 규칙 및 IPv6 보안 그룹 규칙을 지원합니다.
- **Open all ports**에는 IPv4 보안 그룹 규칙 및 IPv6 보안 그룹 규칙이 포함되어 있습니다.

## 전제 조건
- 생성된 보안 그룹이 있어야 합니다. 자세한 작업 방식은 [보안 그룹 생성](https://intl.cloud.tencent.com/document/product/213/34271)을 참조 바랍니다.
- CVM 인스턴스에 어떤 공용 네트워크 및 내부 네트워크의 액세스를 허용 또는 차단해야 하는지 숙지하고 있어야 합니다. 보안 그룹 규칙 설정에 대한 자세한 사례는 [보안 그룹 응용 사례](https://intl.cloud.tencent.com/document/product/213/32369)를 참조 바랍니다.

## 작업 순서
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 왼쪽 메뉴에서 [[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)]을 클릭해 보안 그룹 관리 페이지로 이동합니다.
3. 보안 그룹 관리 페이지에서 [Region]을 선택한 뒤, 규칙을 설정할 보안 그룹을 찾습니다.
4. 규칙을 설정할 보안 그룹 행의 Operation 열에서 [Modify Rules]를 클릭합니다.
5. <span id="step05">보안 그룹 규칙 페이지에서 'Inbound rule'을 클릭한 뒤, 실제 수요에 따라 아래의 방법 중 하나로 작업을 완료합니다.</span>
![](https://main.qcloudimg.com/raw/e4c1f93fe75de51aa8de068da60a2206.png)
>? 다음의 작업은 '방법2: Add a Rule'을 예시로 사용합니다.
>
 - 방법1: Open all ports. ICMP 프로토콜 규칙을 설정할 필요가 없으며, 22, 3389, ICMP, 80, 443, 20, 21 포트를 통해 작업을 완료할 수 있는 시나리오에 적합합니다.
 - 방법2: Add a Rule. ICMP 프로토콜과 같은 여러 통신 프로토콜을 설정해야 하는 시나리오에 적합합니다.
6. 팝업된 'Add Inbound rule' 창에서 규칙을 설정합니다.
![](https://main.qcloudimg.com/raw/0114aa46ffabc46dd9d6921095f6e8fa.png)
규칙 추가 시의 주요 매개변수는 다음과 같습니다.
 - **유형**: '사용자 정의'로 기본 선택되며, 'Windows 로그인' 템플릿, 'Linux 로그인' 템플릿, 'Ping' 템플릿, 'HTTP(80)' 템플릿, 'HTTPS(443)' 템플릿 등 다른 시스템의 규칙 템플릿을 선택할 수도 있습니다.
 - **출처**: 트래픽의 소스(인바운드 규칙) 또는 타깃(아웃바운드 규칙)으로, 다음 옵션 중 하나를 지정하시기 바랍니다.
<table>
	<tr><th>지정한 소스/타깃</th><th>설명</th></tr>
	<tr><td>단일 IPv4 주소 또는 IPv4 주소 범위</td><td>CIDR 표기법(예: <code>203.0.113.0</code>, <code>203.0.113.0/24</code> 또는 <code>0.0.0.0/0</code>, 그중 <code>0.0.0.0/0</code>은 모든 IPv4 주소에 매칭함을 의미) 사용.</td></tr>
	<tr><td>단일 IPv6 주소 또는 IPv6 주소 범위</td><td>CIDR 표기법(예: <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code> 또는 <code>0::0/0</code>, 그중 <code>::/0</code> 또는 <code>0::0/0</code>은 모든 IPv6 주소에 매칭함을 의미) 사용.</td></tr>
	<tr><td>보안 그룹 ID 참조 테이블로, 아래의 보안 그룹 ID를 참조할 수 있습니다.<ul  style="margin: 0;"><li>현재 보안 그룹</li><li>기타 보안 그룹</li></ul>
</td><td><ul  style="margin: 0;"><li>현재 보안 그룹은 CVM에 연결된 보안 그룹 ID를 나타냅니다.</li><li>기타 보안 그룹은 같은 지역 및 같은 프로젝트에 있는 또 다른 보안 그룹 ID를 나타냅니다.</li></ul>
<blockquote class="d-mod-explain"><div class="d-mod-title d-explain-title"><i class="d-icon-explain"></i>설명: </div>
<p></p><ul>
<li>보안 그룹 ID 참조는 고급 기능으로, 사용 여부를 선택할 수 있습니다. 참조된 보안 그룹의 규칙은 현재 보안 그룹에 추가되지 않습니다.</li>
<li>보안 그룹 규칙 설정 시 출처/타깃에 보안 그룹 ID를 입력할 경우, 보안 그룹 ID가 바인딩된 CVM 인스턴스와 ENI의 개인 IP 주소만이 소스/타깃으로 사용되며 공인 IP 주소는 포함되지 않습니다.
</ul>
</blockquote>
</td></tr>
	<tr><td><a href="https://intl.cloud.tencent.com/document/product/215/31867">매개변수 템플릿</a>의 IP 주소 객체 또는 IP 주소 그룹 객체 참조</td><td>-</td></tr>
</table>
 - **프로토콜 포트**: 프로토콜 유형 및 포트 범위를 입력하며, 지원되는 프로토콜 유형에는 TCP, UDP, ICMP, ICMPv6 및 GRE가 있습니다. 또한 [매개변수 템플릿](https://intl.cloud.tencent.com/document/product/215/31867)의 프로토콜 포트 또는 프로토콜 그룹을 참조할 수도 있습니다. 프로토콜 포트가 지원하는 형식은 다음과 같습니다.
    - 단일 포트, 예를 들어 'TCP:80'.
    - 여러 분산 포트, 예를 들어 'TCP:80,443'.
    - 연속 포트, 예를 들어 'TCP:3306-20000'.
    - 모든 포트, 예를 들어 'TCP:ALL'.
 - **정책**: '허용'으로 기본 설정됩니다.
    - 허용: 이 포트에 해당하는 액세스 요청을 허용합니다.
    - 차단: 즉시 데이터 패킷을 손실시키고, 어떠한 응답 정보도 리턴하지 않습니다.
 - **비고**: 사용자 정의 항목으로, 이후 관리상 편의를 위해 규칙에 대해 간략한 설명을 남길 수 있습니다.
7. <span id="step07">[Complete]를 클릭해 보안 그룹의 인바운드 규칙 추가를 완료합니다.</span>
8. 보안 그룹 규칙 페이지에서 'Outbound rule'을 클릭한 뒤, [5단계](#step05) - [7단계](#step07)를 참조하여 보안 그룹의 아웃바운드 규칙 추가를 완료합니다.
