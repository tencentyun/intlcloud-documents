## Cloud-Init

### Cloud-Init란 무엇인가요?
오픈 소스 툴 중의 하나인 Cloud-Init는 CVM 인스턴스 내부에서 실행되는 하나의 비상주 서비스로, 컴퓨터 시작 시 실행하여 실행 완료 후 바로 로그아웃하며 어떠한 포트도 리슨하지 않습니다.
Tencent Cloud의 모든 Linux 공용 이미지에 Cloud-Init 서비스를 사전 설치하였습니다. Cloud-Init 서비스는 주로 CVM 인스턴스 초기화 작업(예시, DNS, Hostname, IP 등 정보에 대한 설정)과 사용자가 CVM 인스턴스를 생성할 때 컴퓨터 최초 시작 시 실행할 사용자 정의 스크립트를 지정하는 데 사용되기 때문에 root 사용자로 Cloud-Init 서비스를 실행해야 합니다.

### Linux 인스턴스 내부의 Cloud-Init 서비스가 정상적으로 작동되는지 어떻게 확인하나요?

<span id="checkcloud-init"></span>
#### Cloud-Init 서비스 실행 문제 해결
우선 인스턴스에 로그인하고 다음 명령어를 차례대로 실행한 후 오류 여부를 모니터링합니다. 실행 결과가 나타나면 서비스가 정상적으로 작동됨을 의미하고, 반대의 경우 오류 원인을 제시합니다. 제시되는 내용에 따라 문제를 해결하시기 바랍니다.
1. cloud-init 캐시 디렉터리를 삭제합니다.
```
rm -rf /var/lib/cloud
```
2. 완전한 cloud-init 초기화를 실행합니다.
```
cloud-init init --local
```
3. 설정된 데이터 소스에 따라 데이터를 가져옵니다.
```
cloud-init init
```
4. Cloud-Init 초기화는 여러 개의 stage로 나뉘며, 각 stage의 종속이 완전하도록 cloud-init modules가 config stage를 지정하여 실행합니다.
```
cloud-init modules --mode=config
```
5. cloud-init modules가 final stage를 지정하여 실행합니다.
```
cloud-init modules --mode=final
```

### Cloud-Init가 어떤 인스턴스 초기화 작업을 실행했나요?

Tencent Cloud는 Cloud-Init를 통해 인스턴스의 모든 초기화 작업을 구현함으로써 전체 인스턴스 내부의 작업을 보다 투명하도록 하였습니다. 아래의 콘텐츠에 관련 작업 상황을 소개하였으며, 더 자세한 내용은 [Cloud-init 공식 문서](http://cloudinit.readthedocs.io/en/latest/)를 참조할 수 있습니다.

<table>
<tr><th style="width: 25%;">초기화 유형</th><th style="width: 25%;">기본 동작</th><th style="width: 25%;">비활성화 방식</th><th style="width: 25%;">주의사항</th></tr>
<tr>
	<td>hostname의 초기화</td>
	<td>인스턴스 <b>최초 시작</b> 시, Cloud-Init가 <code>vendor_data.json</code> 중의 hostname 정보에 근거하여 인스턴스의 hostname을 설정합니다.</td>
	<td>사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 해당 이미지 내부의 hostname 사용자 정의 설정을 유지하려면 사용자 정의 이미지를 만들기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- scripts-user</code> 이 행의 설정을 삭제할 수 있습니다.</td>
	<td>사용자가 <code>- scripts-user</code> 라는 행 설정을 비활성화하면 인스턴스 내부의 <code>/var/lib/cloud/instance/scripts/runcmd</code> 초기화 스크립트는 실행되지 않으며, 동시에 기타 서브 옵션의 초기화(주로 Cloud Monitoring 및 클라우드 보안의 설치, 소프트웨어 보관소 등의 설정과 관련)에도 영향을 미칩니다. 또한 사용자가 CVM을 생성할 때 사용자 정의 스크립트도 실행되지 않습니다.</td>
</tr>

<tr>
	<td>/etc/hosts의 초기화</td>
	<td>인스턴스<b>최초 시작</b> 시, Cloud-Init는 기본으로 <code>/etc/hosts</code> 를 <code>127.0.0.1 $hostname</code>로 초기화합니다.</td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 /etc/hosts 설정을 유지하려면 사용자 정의 이미지를 만들기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- scripts-user</code> 와 <code>- ['update_etc_hosts', 'once-per-instance']</code> 이 두 행의 설정을 삭제할 수 있습니다.</td>
	<td>
		<ul style="margin: 0px;">
			<li>사용자가 <code>- scripts-user</code> 라는 행 설정을 비활성화하면 인스턴스 내부의 <code>/var/lib/cloud/instance/scripts/runcmd</code> 초기화 스크립트는 실행되지 않으며, 동시에 기타 서브 옵션의 초기화(주로 Cloud Monitoring 및 클라우드 보안의 설치, 소프트웨어 보관소 등의 설정과 관련)에도 영향을 미칩니다. 또한 사용자가 CVM을 생성할 때 사용자 정의 스크립트도 실행되지 않습니다.</li>
			<li>CVM을 재시작할 때마다, 일부 인벤토리 기기 <code>/etc/hosts</code>의 설정이 모두 덮어쓰게 됩니다. 솔루션은 <a href="https://intl.cloud.tencent.com/document/product/213/32504">Linux 인스턴스의 etc hosts 설정을 효율적으로 수정하는 방법</a>을 참조 바랍니다.</li>
		</ul>
	</td>
</tr>

<tr>
	<td>DNS의 초기화(비 DHCP 시나리오)</td>
	<td>인스턴스<b>최초 시작</b> 시, Cloud-Init는 <code>vendor_data.json</code> 중의 nameservers 정보에 근거하여 인스턴스의 DNS를 설정합니다.</td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 DNS 설정을 유지하려면 사용자 정의 이미지를 만들기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- resolv_conf</code> 와 <code>unverified_modules: ['resolv_conf']</code> 이 두 행의 설정을 삭제할 수 있습니다.</td>
	<td>없음.</td>
</tr>

<tr>
	<td>소프트웨어 보관소의 초기화</td>
	<td>인스턴스<b>최초 시작</b> 시, Cloud-Init는 <code>vendor_data.json</code> 중의 write_files 정보에 근거하여 인스턴스의 소프트웨어 보관소를 설정합니다.</td><td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 소스 소프트웨어 설정을 유지하려면 사용자 정의 이미지를 만들기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- write-files</code> 이 행의 설정을 삭제할 수 있습니다.</td>
	<td>없음.</td>
</tr>

<tr>
	<td>NTP의 초기화</td>
	<td>인스턴스<b>최초 시작</b> 시, Cloud-Init는 <code>vendor_data.json</code> 중의 NTP Server 정보에 근거하여 인스턴스의 NTP 서버 구성을 설정하고 NTP Service를 가져옵니다.</td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 NTP 설정을 유지하려면 사용자 정의 이미지를 만들기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- ntp<code/> 이 행의 설정을 삭제할 수 있습니다.</td>
	<td>없음.</td>
</tr>

<tr>
	<td>비밀번호의 초기화</td>
	<td>인스턴스<b>최초 시작</b> 시, Cloud-Init는 <code>vendor_data.json</code> 중의 chpasswd 정보에 근거하여 인스턴스의 기본 계정 비밀번호를 설정합니다.</td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 기본 계정 비밀번호를 유지하려면 사용자 정의 이미지를 만들기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- set-passwords</code> 이 행의 설정을 삭제할 수 있습니다.</td>
	<td>없음.</td>
</tr>

<tr>
	<td>키 바인딩</td>
	<td> 인스턴스 <b>최초 시작</b> 시, Cloud-Init는 <code>vendor_data.json</code> 중의 ssh_authorized_keys 정보에 근거하여 인스턴스의 기본 계정 키를 설정합니다.</td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 키를 유지하려면 사용자 정의 이미지를 만들기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- users-groups</code> 이 행의 설정을 삭제할 수 있습니다.</td>
	<td>사용자가 수동 방식으로 인스턴스 내부에서 자체로 키를 바인딩할 경우, 콘솔을 통해 키 바인딩 작업을 전달할 때, 시스템은 해당 키를 덮어씁니다.</td>
</tr>

<tr>
	<td>네트워크 초기화(비 DHCP 시나리오)</td>
	<td>인스턴스<b>최초 시작</b> 시, Cloud-Init는 <code>network_data.json</code> 중의 정보에 근거하여 인스턴스의 IP, GATEWAY, MASK 등을 설정합니다.</td>
	<td> 사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 네트워크 정보를 유지하려면 사용자 정의 이미지를 만들기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>network: {config: disabled}</code> 이 행의 설정을 추가할 수 있습니다.</td>
	<td>없음.</td>
</tr>
</table>

### Cloud-Init의 FAQ는 어떻게 해결하나요? 

#### 1. Cloud-Init의 종속 패키지를 언마운트하여 오류 발생
- 문제 현상:
명령어를 사용해 Cloud-Init 서비스의 정상적인 작동 여부를 확인할 때 다음의 오류를 받았습니다.
```
Traceback (most recent call last):
  File "/usr/bin/cloud-init", line 5, in 
    ********
    raise DistributionNotFound(req)
pkg_resources.DistributionNotFound: pyyaml
```
- 문제 분석:：
“pkg_resources.DistributionNotFound: xxxxx”는 Cloud-Init의 설치 종속 패키지가 언마운트되었음을 의미합니다.
- 솔루션:
 1. 해당 종속 패키지를 다시 설치합니다.
 2. [Cloud-Init 서비스 실행 문제 해결](#checkcloud-init)에 따라 오류가 없을 때까지 모든 작업을 실행합니다.

#### 2. 기본 Python 인터프리터를 수정하여 오류 발생
- 문제 현상:
컴퓨터를 시작하면서 Cloud-Init를 실행할 때 오류가 발생하였습니다.
- 문제 분석:
Cloud-Init 설치 시, Python 인터프리터는 기본으로 Python2(즉 `/usr/bin/python` 과 `/bin/python` 이 두 개 소프트링크가 Python2로 링크)를 사용합니다. 사용자의 비즈니스에 수요가 있을 때, 인스턴스 내부에서 Python의 기본 인터프리터를 Python3(즉 `/usr/bin/python` 과 `/bin/python` 이 두 개 소프트링크를 수정하여 이를 Python3로 향하게 함)으로 수정할 수 있습니다. 호환성 문제로 인해 컴퓨터 시작과 함께 Cloud-Init 실행 시 오류가 발생합니다.
- 솔루션:
 1. `/usr/bin/cloud-init` 파일에서 지정한 Python 인터프리터를 수정하고 `#/usr/bin/python` 또는 `#/bin/python`을 `#! user/bin/python`으로 수정합니다.
> 소프트링크를 사용하지 않고 직접 구체적인 인터프리터를 가리켜야 합니다.
>
 2. [Cloud-Init 서비스 실행 문제 해결](#checkcloud-init)에 따라 오류가 없을 때까지 모든 작업을 실행합니다.

## Cloudbase-Init

### Cloudbase-Init란 무엇인가요?
Cloud-Init와 비슷하게 Cloudbase-Init는 Windows CVM 인스턴스와 통신하는 다리입니다. 인스턴스는 최초 시작할 때 Cloudbase-Init 서비스를 실행하며 해당 서비스는 인스턴스의 초기화 설정 정보를 읽고 인스턴스에 대한 초기화 작업을 진행할 수 있습니다. 또한 이후의 비밀번호 설정, IP 수정 등의 기능 모두 Cloudbase-Init를 통해 구현할 수 있습니다.

### Windows 인스턴스 내부의 Cloudbase-Init 서비스의 정상적인 작동 여부를 어떻게 확인하나요?

<span id="checkcloudbase-init"></span>
#### Cloudbase-Init 서비스 실행 문제 해결:
1. 인스턴스에 로그인합니다.
> 사용자는 비밀번호를 잊거나 Cloudbase-Init 서비스 오류로 인해 비밀번호 재설정에 실패할 경우 [2단계](#step02)를 통해 비밀번호를 재설정할 수 있습니다. 
>
2. <span id="step02">**제어판** > **관리 툴** > **서비스**를 엽니다.
3. cloudbase-init 서비스를 찾아 [속성]을 우클릭하여 cloudbase-init의 속성창을 엽니다.</span>
 - 아래 이미지와 같이 “시작 유형”에서 “시작 유형”이 “자동”으로 설정되어 있어야 합니다.
![](https://main.qcloudimg.com/raw/43f39931ec8932f88ee491f2bdbd7ada.png)
 - 아래 이미지와 같이 “로그인 자격”에서 “로그인 자격”이 “로컬 시스템 계정”이어야 합니다.
![](https://main.qcloudimg.com/raw/5a69afcde36c5bb3259ac1f136f59118.png)
 - cloudbase-init 서비스를 수동으로 시작하고 관련 오류의 발생 여부를 모니터링합니다.
오류 발생 시 해당 오류를 우선 해결해야 하며, 관련 보안 프로그램을 설치하여 cloudbase-init 실행 관련 작업을 차단했는지 확인합니다. 
![](https://main.qcloudimg.com/raw/97684bd42d3b0d05eee996d0106825e3.png)
 - 아래 이미지와 같이 “레지스트리”를 열어 모든 “LocalScriptsPlugin”을 검색하여 그 값을 2로 설정해야 합니다.
![](https://main.qcloudimg.com/raw/4f98965fa228c7f948fc8d720424a7ea.png)
 - CD-ROM의 로딩이 비활성화되었는지 확인합니다. 아래의 그림과 같이 CD 드라이버 장치를 볼 수 있으면 정상적으로 로딩됨을 의미하고, 반대의 경우 비활성화를 의미하므로 비활성화를 취소해야 합니다.
![](https://main.qcloudimg.com/raw/0e8c68537e238fe7a1e4b718848b9e98.png)

### Cloudbase-Init의 FAQ는 어떻게 해결하나요?
#### 비밀번호 초기화 및 재설정 실패
- 가능한 원인:
 - cloudbase-init 계정 비밀번호를 수동으로 수정하여 cloudbase-init 서비스 시작 실패를 초래함으로써 비밀번호 초기화 및 재설정 등 작업이 실패하게 됩니다.
 - cloudbase-init 서비스를 비활성화하여, 비밀번호 초기화, 재설정 등 작업이 실패하게 됩니다.
 - 보안 프로그램을 설치하여 cloudbase-init 서비스 비밀번호의 재설정 작업을 차단함으로써, 비밀번호 재설정 프로세스 리턴에 성공해도 실제로는 재설정 실패하게 됩니다.
- 솔루션:
예상되는 원인에 대해 다음 3가지를 각각 참조하여 작업 바랍니다.
 1. cloudbase-init 서비스를 LocalSystem 서비스로 변경하고, 구체적인 작업 방식은 [Cloudbase-Init 서비스 실행 문제 해결](#checkcloudbase-init)의 [2단계](#step02)를 참조 바랍니다. 
 2. cloudbase-init 서비스 시작 유형을 자동으로 변경합니다. 구체적인 작업 방식은 [Cloudbase-Init 서비스 실행 문제 해결](#checkcloudbase-init)의 [2단계](#step02)를 참조 바랍니다.
 3. 해당하는 보안 프로그램을 언마운트하거나 보안 프로그램 안에 cloudbase-init 서비스 관련 작업의 화이트리스트를 추가합니다.
