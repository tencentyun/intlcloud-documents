## Cloud-Init

### Cloud-Init란 무엇인가요?
오픈 소스 툴 중의 하나인 Cloud-Init는 CVM 인스턴스 내부에서 실행되는 하나의 비 상주 서비스이며 컴퓨터 시작 시 실행하고 실행 완료되면 바로 로그아웃하며 어떠한 포트도 모니터링하지 않습니다.
Tencent Cloud의 Linux 공용 이미지는 모두 Cloud-Init 서비스를 사전 설치하였습니다. Cloud-Init 서비스는 주로 CVM 인스턴스에 대한 초기화 작업(예시, DNS, Hostname, IP 등 정보에 대한 설정)을 실현하는 데 사용되고, 사용자가 CVM 인스턴스를 생성할 때 처음 컴퓨터 시작과 함께 실행해야 한다고 지정한 일부 사용자 정의 스크립트를 실행하기 때문에 root 사용자로 Cloud-Init 서비스를 실행해야 합니다.

### Linux 인스턴스 내부의 Cloud-Init 서비스의 정상적인 실행 여부를 어떻게 확인하나요?

<span id="checkcloud-init"></span>
#### Cloud-Init 서비스 실행 조사 방안
우선 인스턴스에 로그인하고 다음 명령어를 차례대로 실행한 후 오류 여부를 모니터링하십시오. 실행 결과가 나타나면 서비스 정상 실행을 의미하고 그렇지 않을 경우 오류 원인을 제시합니다. 제시어에 따라 문제를 조사하십시오.
1. cloud-init 캐시 목록을 삭제합니다.
```
rm -rf /var/lib/cloud
```
2. 완전한 cloud-init 초기화를 실행합니다.
```
cloud-init init --local
```
3. 구성된 데이터 소스에 따라 데이터를 pull합니다.
```
cloud-init init
```
4. Cloud-Init 초기화는 여러 개의 stage로 나뉘며 각 stage의 충분한 종속을 보장하기 위해 cloud-init modules는 config stage를 지정하여 실행합니다.
```
cloud-init modules --mode=config
```
5. cloud-init modules는 final stage를 지정하여 실행합니다.
```
cloud-init modules --mode=final
```

### Cloud-Init는 인스턴스 초기화의 어떤 작업을 실행하였나요?

Tencent Cloud는 Cloud-Init를 통해 인스턴스의 모든 초기화 작업을 실현함으로써 전체 인스턴스 내부의 작업을 보다 투명하도록 하였습니다. 다음 콘텐츠는 관련 작업 상황을 소개하였으며 더 자세한 내용은 [Cloud-init 공식 문서](http://cloudinit.readthedocs.io/en/latest/)를 참조할 수 있습니다.

<table>
<tr><th style="width: 25%;">초기화 유형</th><th style="width: 25%;">기본 행위</th><th style="width: 25%;">금지 방식</th><th style="width: 25%;">주의사항</th></tr>
<tr>
	<td>hostname의 초기화</td>
	<td>인스턴스<b>처음 실행</b>시, Cloud-Init는 <code>vendor_data.json</code> 중의 hostname 정보에 근거해 인스턴스의 hostname을 설정합니다.</td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 hostname 설정을 유지하려면 사용자 정의 이미지를 제작하기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- scripts-user</code> 이 줄 설정을 삭제할 수 있습니다.</td>
	<td>사용자가 <code>- scripts-user</code> 이 줄 설정을 비활성화하면 인스턴스 내부의 <code>/var/lib/cloud/instance/scripts/runcmd</code> 초기화 스크립트는 실행되지 않으며 동시에 기타 서브 옵션의 초기화(주로 클라우드 모니터링, 클라우드 보안의 설치, 소프트웨어 소스의 설정 관련)에도 영향을 미칩니다. 또한 사용자가 CVM을 생성할 때 사용자 정의 스크립트도 실행되지 않습니다.</td>
</tr>
<tr>
	<td>/etc/hosts의 초기화</td>
	<td>인스턴스<b>처음 시작</b>시, Cloud-Init는 기본으로 <code>/etc/hosts</code> 를 <code>127.0.0.1 $hostname</code>로 초기화합니다.</td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 /etc/hosts 설정을 유지하려면 사용자 정의 이미지를 제작하기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- scripts-user</code> 이 줄 설정을 삭제할 수 있습니다.</td>
	<td>
		<ul style="margin: 0px;">
			<li>사용자가 <code>- scripts-user</code> 이 줄 설정을 비활성화하면 인스턴스 내부의 <code>/var/lib/cloud/instance/scripts/runcmd</code> 초기화 스크립트는 실행되지 않으며 동시에 기타 서브 옵션의 초기화(주로 클라우드 모니터링, 클라우드 보안의 설치, 소프트웨어 소스의 설치 관련)에도 영향을 미칩니다. 또한 사용자가 CVM을 생성할 때 사용자 정의 스크립트도 실행되지 않습니다.</li>
			<li>매번 CVM 재시작할 때, 일부 저장량 기기 <code>/etc/hosts</code>의 설정은 모두 커버됩니다. 솔루션은 <a href="https://cloud.tencent.com/document/product/213/34698">Linux 인스턴스의 etc hosts 설정을 어떻게 효율적으로 수정할 것인가</a></li>를 참조하시길 바랍니다
		</ul>
	</td>
</tr>

<tr>
	<td>DNS의 초기화(비 DHCP 시나리오)</td>
	<td>인스턴스<b>처음 시작</b>시, Cloud-Init는 <code>vendor_data.json</code> 중의 nameservers 정보에 근거해 인스턴스의 DNS를 설정합니다.</td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 DNS 설정을 유지하려면 사용자 정의 이미지를 제작하기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- resolv_conf</code> 와 <code>unverified_modules: ['resolv_conf']</code> 두 줄 설정을 삭제할 수 있습니다.</td>
	<td>없음.</td>
</tr>

<tr>
	<td>소프트웨어 리소스의 초기화</td>
	<td>인스턴스<b>처음 시작</b>시, Cloud-Init는 <code>vendor_data.json</code> 중의 write_files 정보에 근거해 인스턴스의 소프트웨어 소스를 설정합니다.</td><td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 소프트웨어 소스 설정을 유지하려면 사용자 정의 이미지를 제작하기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- write-files</code> 이 줄 설정을 삭제할 수 있습니다.</td>
	<td>없음.</td>
</tr>

<tr>
	<td>NTP의 초기화</td>
	<td>인스턴스<b>처음 시작</b>시, Cloud-Init는 <code>vendor_data.json</code> 중의 NTP Server 정보에 근거해 인스턴스의 NTP 서버 구성을 설정하고 NTP Service를 pull합니다.</td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 NTP 설정을 유지하려면 사용자 정의 이미지를 제작하기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- ntp<code/> 이 줄 설정을 삭제할 수 있습니다.</td>
	<td>없음.</td>
</tr>

<tr>
	<td>비밀번호의 초기화</td>
	<td>인스턴스<b>처음 시작</b>시, Cloud-Init는 <code>vendor_data.json</code> 중의 chpasswd 정보에 근거해 인스턴스의 기본 계정 비밀번호를 설정합니다.</td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 기본 계정 비밀번호를 유지하려면 사용자 정의 이미지를 제작하기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- set-passwords</code> 이 줄 설정을 삭제할 수 있습니다.</td>
	<td>없음.</td>
</tr>

<tr>
	<td>키 바인딩</td>
	<td> 인스턴스<b>처음 시작</b>시, Cloud-Init는 <code>vendor_data.json</code> 중의 ssh_authorized_keys 정보에 근거해 인스턴스의 기본 계정 키를 설정합니다.</td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 키를 유지하려면 사용자 정의 이미지를 제작하기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>- users-groups</code> 이 줄 설정을 삭제할 수 있습니다.</td>
	<td>사용자가 수동 방식으로 인스턴스 내부에서 자체로 키를 바인딩할 경우, 콘솔을 통해 키 바인딩 작업을 전달할 때, 시스템은 해당 키를 커버합니다.</td>
</tr>

<tr>
	<td>네트워크 초기화(비 DHCP 시나리오)</td>
	<td>인스턴스<b>처음 시작</b>시, Cloud-Init는 <code>network_data.json</code> 중의 정보에 근거해 인스턴스의 IP, GATEWAY, MASK 등을 설정합니다.</td>
	<td> 사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 네트워크 정보를 유지하려면 사용자 정의 이미지를 제작하기 전 <code>/etc/cloud/cloud.cfg</code> 안에서 <code>network: {config: disabled}</code> 이 줄 설정을 추가할 수 있습니다.</td>
	<td>없음.</td>
</tr>
</table>

### Cloud-Init FAQ를 어떻게 조사하나요? 

#### 1. Cloud-Init의 종속 패키지를 언마운트하여 오류 발생
- 문제 현상:
명령어를 사용해 Cloud-Init 서비스의 정상적인 실행 여부를 확인할 때 다음의 오류를 받았습니다.
```
Traceback (most recent call last):
  File "/usr/bin/cloud-init", line 5, in 
    ********
    raise DistributionNotFound(req)
pkg_resources.DistributionNotFound: pyyaml
```
- 문제 분석:
“pkg_resources.DistributionNotFound: xxxxx”는 Cloud-Init의 설치 종속 패키지가 언마운트되었음을 표시합니다.
- 솔루션:
 1. 해당 종속 패키지를 다시 설치합니다.
 2. [Cloud-Init 서비스 실행 조사 방안](#checkcloud-init)에 따라 전부 실행 완료하여 오류가 없을 때까지 작업을 실행합니다.

#### 2. 기본 Python 인터프리터를 수정하여 오류 발생
- 문제 현상:
컴퓨터를 시작하면서 Cloud-Init를 실행할 때 오류가 발생하였습니다.
- 문제 분석:
Cloud-Init 설치 시, Python 인터프리터는 기본으로 Python2(즉 `/usr/bin/python` 과 `/bin/python` 이 두 개 소프트링크가 Python2로 링크)를 사용합니다. 사용자의 비즈니스에 수요가 있을 때, 인스턴스 내부에서 Python의 기본 인터프리터를 Python3(즉 `/usr/bin/python` 과 `/bin/python` 이 두 개 소프트링크를 수정하여 이를 Python3로 향하게 함)으로 수정할 수 있습니다. 호환성 문제로 인해 컴퓨터 시작과 함께 Cloud-Init 실행 시 오류가 발생합니다.
- 솔루션:
 1. `/usr/bin/cloud-init` 파일에서 지정한 Python 인터프리터를 수정하고 `#/usr/bin/python` 또는 `#/bin/python`을 `#! user/bin/python`으로 수정합니다.
>! 소프트링크를 사용하지 않고 직접 구체적인 인터프리터를 가리켜야 합니다.
>
 2. [Cloud-Init 서비스 실행 조사 방안](#checkcloud-init)에 따라 전부 실행 완료하여 오류가 없을 때까지 작업을 실행합니다.

## Cloudbase-Init

### Cloudbase-Init란 무엇인가요?
Cloud-Init와 비슷하게 Cloudbase-Init는 Windows CVM 인스턴스와 통신하는 다리입니다. 인스턴스는 처음 시작할 때 Cloudbase-Init 서비스를 실행하며 해당 서비스는 인스턴스의 초기화 설정 정보를 읽고 인스턴스에 대한 초기화 작업을 진행할 수 있습니다. 또한 후속적인 비밀번호 설정, IP 수정 등 기능을 포함하여 모두 Cloudbase-Init를 통해 실현할 수 있습니다.

### Windows 인스턴스 내부의 Cloudbase-Init 서비스의 정상적인 실행 여부를 어떻게 확인하나요?

<span id="checkcloudbase-init"></span>
#### Cloudbase-Init 서비스 실행 조사 방안:
1. 인스턴스에 로그인합니다.
>? 사용자는 비밀번호를 잊거나 Cloudbase-Init 서비스 비정상으로 인해 비밀번호 재설정에 실패할 경우 [2단계](#step02)를 통해 비밀번호를 재설정할 수 있습니다. 
>
2. <span id="step02">**제어판** > **관리 툴** > **서비스**를 엽니다.
3. cloudbase-init 서비스를 찾아 [속성]을 우클릭하여 cloudbase-init의 속성창을 엽니다.</span>
 - "시작 유형"을 조회하여 "시작 유형"이 "자동"임을 보장합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/43f39931ec8932f88ee491f2bdbd7ada.png)
 - "로그인 신원"을 조회하여 "로그인 신원"이 "로컬 시스템 계정"임을 보장합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/5a69afcde36c5bb3259ac1f136f59118.png)
 - cloudbase-init 서비스를 수동으로 시작하고 관련 오류의 발생 여부를 모니터링합니다.
발생한 오류를 우선 해결해야 할 경우 관련 보안 프로그램을 설치하여 cloudbase-init 실행의 관련 작업을 차단해야 하는 지를 확인하세요. 
![](https://main.qcloudimg.com/raw/97684bd42d3b0d05eee996d0106825e3.png)
 - "레지스트리"를 열어 검색하고 모든 "LocalScriptsPlugin"을 찾아 그 값을 2로 보장합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/4f98965fa228c7f948fc8d720424a7ea.png)
 - CD-ROM의 로딩이 비활성화되었는 지 확인합니다. 다음 그림과 같이, 시디롬 드라이브 디바이스를 볼 수 있으면 정상적인 로딩을 표시하고 그렇지 않을 경우 비활성화되었음을 의미하고 비활성화를 취소해야 합니다.
![](https://main.qcloudimg.com/raw/0e8c68537e238fe7a1e4b718848b9e98.png)

### Cloudbase-Init FAQ를 어떻게 조사하나요?
#### 초기화 비밀번호 재설정 실패
- 가능한 원인:
 - cloudbase-init 계정 비밀번호를 수동으로 수정하여 cloudbase-init 서비스 시작 실패를 초래함으로써 초기화 비밀번호 재설정 등 작업이 실패했습니다.
 - cloudbase-init 서비스를 비활성화함으로써 초기화 비밀번호 재설정 등 작업이 실패했습니다.
 - 보안 프로그램을 설치하여 cloudbase-init 서비스 비밀번호 재설정의 작업을 차단함으로써 비밀번호 재설정 프로세스 리턴 성공했지만 실제로는 재설정 실패했습니다.
- 솔루션:
가능한 원인에 대해 다음 3가지를 각각 참고하여 작업하길 바랍니다.
 1. cloudbase-init 서비스를 LocalSystem 서비스로 변경하고 구체적인 작업 방식은 [Cloudbase-Init 서비스 실행 조사 방안](#checkcloudbase-init)의 [2단계](#step02)를 참조하시길 바랍니다. 
 2. cloudbase-init 서비스 시작 유형을 자동으로 변경합니다. 구체적인 작업 방식은 [Cloudbase-Init 서비스 실행 조사 방안](#checkcloudbase-init)의 [2단계](#step02)를 참조하시길 바랍니다.
 3. 대응하는 보안 프로그램을 언마운트하거나 보안 프로그램 안에 cloudbase-init 서비스의 관련 작업에 대한 화이트리스트를 추가합니다.
