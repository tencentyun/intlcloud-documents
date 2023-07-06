## Cloud-Init

### Cloud-Init란 무엇인가요?
오픈 소스 툴 중의 하나인 Cloud-Init는 CVM 인스턴스 내부에서 실행되는 하나의 비상주 서비스로, 컴퓨터 시작 시 실행되고 실행 완료 후 바로 종료되어 어떠한 포트도 리스닝하지 않습니다.
Tencent Cloud의 모든 Linux 공용 이미지에 Cloud-Init 서비스가 사전 설치되어있습니다. Cloud-Init 서비스는 주로 CVM 인스턴스 초기화 작업(예: DNS, Hostname, IP 등 정보 설정)과 사용자가 CVM 인스턴스를 생성할 때 컴퓨터 최초 시작 시 실행할 사용자 정의 스크립트를 지정하는 데 사용되기 때문에, root 사용자로 Cloud-Init 서비스를 실행해야 합니다.

### Linux 인스턴스 내부의 Cloud-Init 서비스가 정상적으로 작동되는지 어떻게 확인하나요?


#### Cloud-Init 서비스 실행 문제 해결 방법[](id:checkcloud-init)

[Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참고하여 인스턴스에 로그인하고 다음 명령을 차례로 실행합니다. 오류 여부를 모니터링합니다. 실행 결과가 나타나면 서비스가 정상적으로 작동됨을 의미하고, 반대의 경우 오류 원인을 보고합니다. 보고된 내용에 따라 문제를 해결하시기 바랍니다.
<dx-alert infotype="explain" title="">
이 단계는 Linux 공용 이미지를 사용하여 생성된 CVM 인스턴스에만 적용됩니다. Cloud-Init을 직접 설치하셨다면, 실제 상황에 맞게 실행 명령어를 조정하시기 바랍니다.
</dx-alert>


1. cloud-init 캐시 디렉터리를 삭제합니다.
```shellsession
rm -rf /var/lib/cloud
```
2. 완전한 cloud-init 초기화를 실행합니다.
```shellsession
/usr/bin/cloud-init init --local
```
3. 설정된 데이터 소스에 따라 데이터를 가져옵니다.
```shellsession
/usr/bin/cloud-init init
```
4. Cloud-Init 초기화는 여러 개의 stage로 나뉘며, 각 stage의 종속이 완전하도록 cloud-init modules가 config stage를 지정하여 실행합니다.
```shellsession
/usr/bin/cloud-init modules --mode=config
```
5. cloud-init modules가 final stage를 지정하여 실행합니다.
```shellsession
/usr/bin/cloud-init modules --mode=final
```

### Cloud-Init가 어떤 인스턴스 초기화 작업을 실행했나요?

Tencent Cloud는 Cloud-Init를 통해 인스턴스의 모든 초기화 작업을 구현함으로써 전체 인스턴스 내부의 작업을 보다 투명하도록 하였습니다. 다음 내용은 관련 작업을 간략히 소개합니다. 자세한 내용은 [Cloud-init 공식 문서](http://cloudinit.readthedocs.io/en/latest/)에서 확인할 수 있습니다.

<table>
<tr>
    <th style="width: 18%;">초기화 유형</th>
    <th style="width: 25%;">기본 동작</th>
    <th style="width: 27%;">비활성화 방법</th>
    <th style="width: 30%;">주의사항</th>
  </tr>
  <tr>
	<td>hostname의 초기화</td>
	<td>인스턴스
	<b>최초 시작</b> 시, Cloud-Init는 
	<code>vendor_data.json</code> 중의 hostname 정보에 근거하여 인스턴스의 hostname을 설정합니다. </td>
	<td>
	사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 해당 이미지 내부의 hostname 사용자 정의
	설정을 유지하려면, 사용자 정의 이미지 생성 전 <code>/etc/cloud/cloud.cfg</code> 중의 <code>preserve_hostname</code>를 <code>true</code>로 설정하고, <code>- scripts-user</code> 행의 설정을 삭제합니다.
	</td>
	<td>만약 <code>preserve_hostname</code>을 
	<code>true</code>로 설정하고 <code>- scripts-user</code> 설정을 비활성화하면 인스턴스 내부의 
	<code>/var/lib/cloud/instance/scripts/runcmd</code>
	초기화 스크립트는 실행되지 않으며, 동시에 기타 서브 옵션의 초기화(Tencent Cloud Observability Platform, Cloud Security 설치, Software Source 설정 등)에도 영향을 미칩니다.
	또한 사용자가 CVM을 생성할 때 사용자 정의 스크립트도 실행되지 않습니다. </td>
  </tr>
  <tr>
	<td>/etc/hosts의 초기화</td>
	<td>인스턴스
	<b>최초 실행</b>시, Cloud-Init는 기본으로 
	<code>/etc/hosts</code>를 
	<code>127.0.0.1 $hostname</code>。 </td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 /etc/hosts
	사용자 정의 설정을 유지하려면 사용자 정의 이미지 생성 전 
	<code>/etc/cloud/cloud.cfg</code> 안에서 
	<code>- scripts-user</code> 와 
	<code>- [&#39;update_etc_hosts&#39;, &#39;once-per-instance&#39;]</code> 두 행의 설정을 삭제합니다. </td>
	<td>
	  <ul style="margin: 0px;">
		<li>사용자가 
		<code>- scripts-user</code> 행 설정을 비활성화하면 인스턴스 내부의 
		<code>/var/lib/cloud/instance/scripts/runcmd</code>
		초기화 스크립트는 실행되지 않으며, 동시에 기타 서브 옵션의 초기화(Tencent Cloud Observability Platform, Cloud Security 설치, Software Source 설정 등)에도 영향을 미칩니다. 또한 사용자가 CVM을 생성할 때 사용자 정의 스크립트도 실행되지 않습니다. </li>
		<li>CVM을 재시작할 때마다, 일부 기존 기기의 
		<code>/etc/hosts</code> 설정이 모두 덮어쓰기 됩니다. 이에 대한 해결 방법은 
		<a href="https://intl.cloud.tencent.com/document/product/213/32504">Linux CVM의 etc/hosts
		설정 변경 방법</a>을 참고 바랍니다. </li>
	  </ul>
	</td>
  </tr>
  <tr>
	<td>DNS의 초기화(비 DHCP 시나리오)</td>
	<td>인스턴스
	<b>최초 시작</b> 시, Cloud-Init는 
	<code>vendor_data.json</code> 중의 nameservers 정보에 근거하여 인스턴스의 DNS를 설정합니다. </td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 DNS
	사용자 정의 설정을 유지하려면 사용자 정의 이미지 생성 전 
	<code>/etc/cloud/cloud.cfg</code> 안에서 
	<code>- resolv_conf</code> 와 
	<code>unverified_modules: [&#39;resolv_conf&#39;]</code> 두 행의 설정을 삭제합니다. </td>
	<td>없음. </td>
  </tr>
  <tr>
	<td>소프트웨어 보관소 초기화</td>
	<td>인스턴스
	<b>최초 시작</b> 시, Cloud-Init는 
	<code>vendor_data.json</code> 중의 write_files 정보에 근거하여 인스턴스의 소프트웨어 소스를 설정합니다. </td>
	<td>
	사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 소스 소프트웨어 사용자 정의 설정을 유지하려면 사용자 정의 이미지 생성 전
	<code>/etc/cloud/cloud.cfg</code> 안에서 
	<code>- write-files</code> 행의 설정을 삭제합니다. </td>
	<td>없음. </td>
  </tr>
  <tr>
	<td>NTP 초기화</td>
	<td>인스턴스
	<b>최초 시작</b> 시, Cloud-Init는 
	<code>vendor_data.json</code> 중의 NTP Server 정보에 근거하여 인스턴스의 NTP 서버 구성을 설정하고 NTP
	Service를 시작합니다. </td>
	<td>사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 NTP
	사용자 정의 설정을 유지하려면 사용자 정의 이미지 생성 전 
	<code>/etc/cloud/cloud.cfg</code> 안에서 
	<code>- ntp 행의 설정을 삭제합니다. </code></td>
	<td>없음. </td>
  </tr>
  <tr>
	<td>비밀번호 초기화</td>
	<td>인스턴스
	<b>최초 시작</b> 시, Cloud-Init는 
	<code>vendor_data.json</code> 중의 chpasswd 정보에 근거하여 인스턴스의 기본 계정 비밀번호를 설정합니다. </td>
	<td>
	사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 기본 계정 비밀번호를 유지하려면 사용자 정의 이미지 생성 전	
	<code>/etc/cloud/cloud.cfg</code> 안에서 
	<code>- set-passwords</code> 이 행의 설정을 삭제할 수 있습니다. </td>
	<td>없음. </td>
  </tr>
  <tr>
	<td>키 바인딩</td>
	<td>인스턴스
	<b>최초 시작</b> 시, Cloud-Init는 
	<code>vendor_data.json</code> 중의 ssh_authorized_keys 정보에 근거하여 인스턴스의 기본 계정 키를 설정합니다. </td>
	<td>
	사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 키를 유지하려면 사용자 정의 이미지 생성 전	
	<code>/etc/cloud/cloud.cfg</code> 안에서 
	<code>- users-groups</code> 행의 설정을 삭제합니다. </td>
	<td>
	사용자가 수동 방식으로 인스턴스 내부에서 자체로 키를 바인딩하는 경우, 콘솔을 통한 키 바인딩 작업 전달 시 시스템은 해당 키를 덮어씁니다. </td>
  </tr>
  <tr>
	<td>네트워크 초기화(비 DHCP 시나리오)</td>
	<td>인스턴스
	<b>최초 시작</b> 시, Cloud-Init는 
	<code>network_data.json</code> 중의 정보에 근거하여 인스턴스의 IP, GATEWAY, MASK 등을 설정합니다. </td>
	<td>
	사용자가 사용자 정의 이미지를 사용해 인스턴스를 생성 또는 재설치할 때, 사용자가 사용자 정의 이미지 내부 사용자 정의의 네트워크 정보를 유지하려면 사용자 정의 이미지 생성 전	
	<code>/etc/cloud/cloud.cfg</code> 안에서 
	<code>network: {config: disabled}</code> 이 행의 설정을 추가합니다. </td>
	<td>없음. </td>
  </tr>
</table>



### Cloud-Init의 일반적인 문제는 어떻게 해결하나요? 

#### 1. Cloud-Init의 종속 패키지 언마운트로 인한 오류 발생
- 문제 현상:
명령어를 사용해 Cloud-Init 서비스 정상 작동 여부 확인 시, 다음과 같은 오류가 수신됨:
```
Traceback (most recent call last):
  File "/usr/bin/cloud-init", line 5, in 
    ********
    raise DistributionNotFound(req)
pkg_resources.DistributionNotFound: pyyaml
```
- 문제 분석:
“pkg_resources.DistributionNotFound: xxxxx ”는 Cloud-Init의 설치 종속성이 제거되었음을 나타냅니다.
- 솔루션:
 1. 해당 종속 패키지를 다시 설치합니다.
 2. [Cloud-Init 서비스 실행 문제 해결](#checkcloud-init)에 따라 오류가 없을 때까지 모든 작업을 실행합니다.

#### 2. 기본 Python 인터프리터 수정으로 인한 오류 발생
- 문제 현상:
컴퓨터를 켜고 Cloud-Init 실행 시 오류 발생.
- 문제 분석:
Cloud-Init를 설치할 때 Python 인터프리터는 기본적으로 Python2를 사용합니다(즉, 두 개의 소프트 링크 `/usr/bin/python` 및 `/bin/python`은 Python2를 가리킴). 필요에 따라 인스턴스 내에서 Python의 기본 인터프리터를 Python3으로 변경할 수 있습니다(즉, 두 개의 소프트 링크 `/usr/bin/python` 및 `/bin/python`이 Python3을 가리키도록 수정). 호환성 문제 때문에, 컴퓨터를 켜고 Cloud-Init 실행 시 오류가 발생합니다.
- 솔루션:
 1. Python2.7을 예로 들면, `/usr/bin/cloud-init` 파일에서 지정한 Python 인터프리터를 수정하고 `#/usr/bin/python` 또는 `#/bin/python`을 `#! user/bin/python`으로 수정합니다.
<dx-alert infotype="notice" title="">
소프트링크를 사용하지 않고 직접 구체적인 인터프리터를 가리켜야 합니다.
</dx-alert>
 2. [Cloud-Init 서비스 실행 문제 해결](#checkcloud-init)에 따라 오류가 없을 때까지 모든 작업을 실행합니다.

## Cloudbase-Init

### Cloudbase-Init란 무엇인가요?
Cloud-Init과 유사하게 Cloudbase-Init는 Windows 클라우드 서버 인스턴스와 통신하는 브리지입니다. 인스턴스가 처음 시작되면 Cloudbase-Init 서비스가 실행되어 인스턴스의 초기화 구성 정보를 읽고 인스턴스를 초기화합니다. 동시에 비밀번호 재설정, IP 수정과 같은 기능도 Cloudbase-Init를 통해 구현됩니다.


### Windows 인스턴스 내부의 Cloudbase-Init 서비스의 정상적인 작동 여부는 어떻게 확인하나요?


#### Cloudbase-Init 서비스 실행 문제 해결:[](id:checkcloudbase-init)
1. 인스턴스에 로그인합니다.
<dx-alert infotype="explain" title="">
비밀번호를 잊었거나 Cloudbase-Init 서비스 오류로 인한 비밀번호 재설정 실패의 경우 [2단계](#step02)를 통해 비밀번호를 재설정할 수 있습니다. 
</dx-alert>
2. [](id:step02)**제어판** > **관리 툴** > **서비스**를 엽니다.
3. cloudbase-init 서비스를 찾아 **속성**을 우클릭하여 cloudbase-init의 속성 창을 엽니다.
 - ‘시작 유형’에서 ‘시작 유형’이 ‘자동’으로 설정되어 있어야 합니다. 다음 이미지 참고:
![](https://main.qcloudimg.com/raw/310a278dd2eaf2124d0d52055e0b5b6f.png)
 - ‘로그인 자격’에서 ‘로그인 자격’이 ‘로컬 시스템 계정’이어야 합니다. 다음 이미지 참고:
![](https://main.qcloudimg.com/raw/5a3f623aaf44d55cfe2eaa6aeadb4c12.png)
 - cloudbase-init 서비스를 수동으로 시작하고 관련 오류의 발생 여부를 모니터링합니다.
오류 발생 시 해당 오류를 우선 해결해야 하며, 설치된 보안 프로그램이 cloudbase-init 실행 관련 작업을 차단했는지 확인합니다. 
![](https://main.qcloudimg.com/raw/dbbe8f9fc05b07d8011705d9d217b76c.png)
 - ‘레지스트리’를 열어 모든 ‘LocalScriptsPlugin’을 검색하여 그 값을 2로 설정해야 합니다. 다음 이미지 참고:
![](https://main.qcloudimg.com/raw/16106e540d8cf4ef39e5dccb44251350.png)
 - CD-ROM 로딩이 비활성화되어 있는지 확인합니다. - 다음 이미지와 같이, CD 드라이버 장치를 볼 수 있으면 정상적으로 로딩됨을 의미하고, 반대의 경우 비활성화된 것이므로 비활성화를 취소해야 합니다.
![](https://main.qcloudimg.com/raw/7707e694b475ba4d70b4d1d52a6c98bb.png)

### Cloudbase-Init 실행 로그를 보는 방법은 무엇입니까?
운영 체제에 따라 다음 로그 파일을 볼 수 있습니다:
- Linux 시스템: `/var/log/cloud-init-output.log`
- Windows 시스템: `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\log\cloudbase-init.log`

### Cloudbase-Init의 일반적인 문제는 어떻게 해결하나요?
#### 비밀번호 초기화 및 재설정 실패
- 가능한 원인:
 - cloudbase-init 계정 비밀번호 수동 수정으로 인한 cloudbase-init 서비스 실행 실패 및 비밀번호 초기화 및 재설정 등 작업 실패.
 - cloudbase-init 서비스 비활성화로 인한 비밀번호 초기화 및 재설정 등 작업 실패.
 - 설치된 보안 프로그램의 cloudbase-init 서비스 비밀번호 재설정 작업 차단으로 인한 비밀번호 재설정 프로세스 리턴 성공에도 불구 실제 재설정 실패.
- 솔루션:
예상 원인에 따라 각각 다음 3가지를 참고하여 작업하시기 바랍니다.
 1. cloudbase-init 서비스를 LocalSystem 서비스로 변경합니다. 구체적인 작업 방식은 [Cloudbase-Init 서비스 실행 문제 해결](#checkcloudbase-init)의 [2단계](#step02)를 참고합니다. 
 2. cloudbase-init의 실행 유형을 자동으로 변경합니다. 구체적인 작업 방식은 [Cloudbase-Init 서비스 실행 문제 해결](#checkcloudbase-init)의 [2단계](#step02)를 참고하십시오.
 3. 해당 보안 프로그램을 삭제하거나 cloudbase-init 서비스 관련 작업을 보안 프로그램 얼로우리스트에 추가합니다.


