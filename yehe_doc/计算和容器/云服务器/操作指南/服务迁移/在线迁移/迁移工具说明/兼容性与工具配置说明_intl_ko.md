## 지원되는 운영 체제

현재 온라인 마이그레이션 툴에서는 다음과 같은 소스 CVM 운영 체제를 지원합니다.

<table>
	<tr><th>Linux 운영 체제</th><th>Windows 운영 체제</th></tr>
	<tr><td>CentOS 5/6/7/8</td><td rowspan=8>Windows Server 2008<br>Windows Server 2012<br>Windows Server 2016<br>Windows Server 2019<br>Windows Server 2022</td></tr>
	<tr><td>Ubuntu 10/12/14/16/18/20 </td></tr>
	<tr><td>Debian 7/8/9/10</td></tr>
	<tr><td>SUSE 11/12/15</td></tr>
	<tr><td>openSUSE 42</td></tr>
	<tr><td>Amazon Linux AMI</td></tr>
	<tr><td>Red Hat 5/6/7/8</td></tr>
	<tr><td>Oracle Linux 5/6/7/8</td></tr>
</table>

## 지원하는 마이그레이션 모드

<dx-tabs>
::: 공중망 마이그레이션 모드[](id:publicMigration)
사용자의 소스 CVM과 대상 CVM 모두 공중망 액세스 기능이 있다면 공중망 마이그레이션 모드의 마이그레이션을 사용할 수 있습니다.
현재 공중망 마이그레이션 모드에서는, 소스 CVM에서 인터넷을 통해 Tencent Cloud API에 액세스하여 마이그레이션 요청을 보낸 다음, 대상 CVM에 데이터를 전송함으로써 소스 CVM을 Tencent Cloud의 대상 CVM으로 마이그레이션합니다. 공중망 마이그레이션 시나리오는 다음 이미지와 같습니다.
 ![](https://main.qcloudimg.com/raw/5203e535f5ba947bb67c1f91dee52f1f.jpg)
:::
::: 사설망 마이그레이션 모드[](id:intranetMigration)
사용자의 소스 CVM이나 대상 CVM이 특정 사설망이나 VPC에 있다면 인터넷을 통해 소스 CVM을 대상 CVM에 바로 연결할 수 없으므로, 툴의 사설망 마이그레이션 모드로 마이그레이션할 수 있습니다. 사설망 마이그레이션을 사용하려면 [Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003) 또는 [Direct Connect](https://intl.cloud.tencent.com/document/product/216) 등의 방법으로 소스 CVM과 대상 CVM 간의 통로를 생성해야 합니다.

- [](id:Scenario1)**시나리오1**: (이 시나리오는 [툴 마이그레이션 사용](https://intl.cloud.tencent.com/document/product/213/35640)만 지원) 사용자의 소스 CVM 혹은 대상 CVM이 공중망에 액세스할 수 없다면, 게이트웨이 같이 공중망 액세스 기능을 갖춘 호스트에서 인터넷을 통해 Tencent Cloud API를 호출하여 마이그레이션을 요청한 다음, 터널을 연결하여 데이터를 대상 CVM으로 마이그레이션 할 수 있습니다. 이 시나리오에서는 소스 CVM과 대상 CVM의 공중망 액세스 기능이 필요하지 않습니다.
![](https://main.qcloudimg.com/raw/19300ddf557d4534b1cd77fcbf64ef6a.jpg)
- [](id:Scenario2)**시나리오2**: 사용자의 소스 CVM이 공중망에 액세스할 수 있다면, 먼저 소스 CVM에서 인터넷을 통해 Tencent Cloud API를 호출하여 마이그레이션을 요청한 다음, 터널을 연결하여 데이터를 대상 CVM으로 마이그레이션 할 수 있습니다. 이 시나리오에서는 소스 CVM의 공중망 액세스 기능이 필요하며 대상 CVM은 해당 기능이 필요하지 않습니다.
![](https://main.qcloudimg.com/raw/90bf988ba7cddb9b80307efb30eaad29.jpg)
- [](id:Scenario3)**시나리오3**: 사용자의 소스 CVM이 프록시를 통해 공중망에 액세스할 수 있다면, 먼저 소스 CVM에서 네트워크 프록시를 통해 Tencent Cloud API를 호출하여 마이그레이션을 요청한 다음, 터널을 연결하여 데이터를 대상 CVM으로 마이그레이션 할 수 있습니다. 이 시나리오에서는 소스 CVM과 대상 CVM의 공중망 액세스 기능이 필요하지 않습니다.
![](https://main.qcloudimg.com/raw/14f81f2c4e6cfff80d912841451c5b69.jpg)
:::
</dx-tabs>


## 압축 파일 설명
`go2tencentcloud.zip` 압축 해제 후 파일 설명은 다음과 같습니다.
<table>
	<tr><th width="30%">파일 이름</th><th>설명</th></tr>
	<tr><td>go2tencentcloud-linux.zip</td><td>Linux 시스템용 마이그레이션 zip.</td></tr>
	<tr><td>go2tencentcloud-windows.zip</td><td>Windows 시스템용 마이그레이션 zip.</td></tr>
	<tr><td>readme.txt</td><td>디렉터리 소개 파일.</td></tr>
	<tr><td>release_notes.txt</td><td>마이그레이션 툴 변경 로그.</td></tr>
</table>

`go2tencentcloud-linux.zip` 압축 해제 후 파일 설명은 다음과 같습니다.
<table>
	<tr><th width="30%">파일 이름</th><th>설명</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>64비트 Linux 시스템의 마이그레이션 툴에서 실행 가능한 프로그램입니다.</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>32비트 Linux 시스템의 마이그레이션 툴에서 실행 가능한 프로그램입니다.</td></tr>
	<tr><td>user.json</td><td>마이그레이션의 사용자 정보입니다.</td></tr>
	<tr><td>client.json</td><td>마이그레이션 툴의 구성 파일입니다.</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync 구성 파일로, Linux 시스템에서 마이그레이션 하지 않을 파일 디렉터리를 제외합니다.</td></tr>
</table>

`go2tencentcloud-windows.zip` 압축 해제 후 파일 설명은 다음과 같습니다.
<table>
	<tr><th width="30%">파일 이름</th><th>설명</th></tr>
	<tr><td>go2tencentcloud_x64.exe</td><td>64비트 Windows 시스템의 마이그레이션 툴에서 실행 가능한 프로그램입니다.</td></tr>
	<tr><td>user.json</td><td>마이그레이션의 사용자 정보입니다.</td></tr>
	<tr><td>client.json</td><td>마이그레이션 툴의 구성 파일입니다.</td></tr>
	<tr><td>client.exe</td><td>Windows 시스템의 마이그레이션 실행 가능 프로그램입니다.</td></tr>
</table>

<dx-alert infotype="notice" title="">
삭제할 수 없는 구성 파일은 go2tencentcloud의 실행 가능 프로그램과 같은 단계의 디렉터리로 이동해 놓으시기 바랍니다. 
</dx-alert>

### user.json 파일 매개변수 설명[](id:userJsonState)

user.json 구성 파일은 다음과 같이 설명됩니다.

<table>
	<tr><th>매개변수 이름</th><th>유형</th><th>필수 입력 여부</th><th>설명</th></tr>
	<tr><td>SecretId</td><td>String</td><td>Yes</td><td>계정 API 호출 키 SecretId. 이에 관한 세부 정보는 <a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>를 참고 바랍니다.</td></tr>
	<tr><td>SecretKey</td><td>String</td><td>Yes</td><td>계정 API 호출 키 SecretKey. 이에 관한 세부 정보는 <a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a>를 참고 바랍니다.</td></tr>
</table>

### client.json 파일 매개변수 설명[](id:clientJsonState)

client.json 구성 파일은 다음과 같이 설명됩니다.

<table>
  <tr>
	<th>매개변수 이름</th>
	<th>유형</th>
	<th>필수 입력<br>여부</th>
	<th>설명</th>
  </tr>
  <tr>
	<td>Client.Extra.IgnoreCheck</td>
	<td>Bool</td>
	<td>No</td>
	<td>기본값:  
	<code>false</code>. 마이그레이션 툴은 기본적으로 툴 실행이 시작될 때 원본 호스트 환경을 자동 확인합니다. 확인을 건너뛰려면  
	<code>true</code>로 설정하십시오.</td>
  </tr>
  <tr>
	<td>Client.Extra.Daemon</td>
	<td>Bool</td>
	<td>No</td>
	<td>기본값:  
	<code>false</code>, 마이그레이션 도구를 백그라운드에서 실행해야 하는 경우 이 매개변수를  
	<code>true</code>로 설정하십시오.</td>
  </tr>
  <tr>
	<td> Client.Net.Proxy.Ip</td>
	<td>String</td>
	<td>No</td>
	<td>기본값은 비어 있습니다. 사설망 마이그레이션 <a href="#Scenario3">시나리오 3</a>에서는 네트워크 프록시의 IP 주소를 구성해야 합니다.</td>
  </tr>
	 <tr>
<td> Client.Net.Proxy.IPv6</td>
	<td>Bool</td>
	<td>No</td>
	<td>기본값은 <code>false</code>입니다. IPv6를 통해 데이터를 전송하려면(예: 소스 IP 범위 또는 피어 끝에서 IPv6 IP만 사용 가능) 값을 <code>true</code>로 설정해야 합니다. 그렇지 않으면 마이그레이션 데이터가 IPv4를 통해 전송됩니다.</td>
  </tr>
  <tr>
	<td> Client.Net.Proxy.Port</td>
	<td>String</td>
	<td>No</td>
	<td>기본값은 비어 있습니다. 사설망 마이그레이션 <a href="#Scenario3">시나리오 3</a>에서는 네트워크 프록시의 포트를 구성해야 합니다.</td>
  </tr>
   <tr>
	<td> Client.Net.Proxy.User</td>
	<td>String</td>
	<td>No</td>
	<td>기본값은 비어 있습니다. 사설망 마이그레이션 <a href="#Scenario3">시나리오 3</a>에서 네트워크 프록시를 확인해야 하는 경우 네트워크 프록시의 사용자 이름을 구성합니다.</td>
  </tr>
   <tr>
	<td> Client.Net.Proxy.Password</td>
	<td>String</td>
	<td>No</td>
	<td>기본값은 비어 있습니다. 사설망 마이그레이션 <a href="#Scenario3">시나리오 3</a>에서 네트워크 프록시를 확인해야 하는 경우 네트워크 프록시의 암호를 구성합니다.</td>
  </tr>
</table>

<dx-alert infotype="explain" title="">
상기 매개변수 외 client.json 파일의 나머지 설정 항목은 일반적으로 입력할 필요가 없습니다.
</dx-alert>

###  rsync\_excludes\_linux.txt 파일 설명[](id:_linuxTxtState)

Linux 소스 CVM에서 마이그레이션하지 않을 파일을 제외하거나 디렉터리 안의 구성 파일을 지정합니다. 다음의 디렉터리 및 파일이 제외 파일로 기본 설정되어 있습니다. **삭제하지 마시기 바랍니다**.
```sh
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
```
다른 디렉터리 및 파일을 제외하고 싶다면 해당 파일 끝에 내용을 추가하시기 바랍니다. 예시: `/mnt/disk1`에 마운트되어 있는 데이터 디스크의 모든 내용 제외.
```sh
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
/mnt/disk1/*
```

## 툴 실행 매개변수 설명

<table>
<thead>
<tr>
<th width="18%">매개변수 항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><code>--help</code></td>
<td>도움말 정보를 출력합니다.</td>
</tr>
<tr>
<td><code>--check</code></td>
<td>소스 서버 확인</td>
</tr>
<tr>
<td><code>--log-file</code></td>
<td>로그 파일 이름 설정. 기본값: <code>log</code>.</td>
</tr>
<tr>
<td><code>--log-level</code></td>
<td>로그 출력 레벨로, 입력값의 범위는<code>1</code>(ERROR 레벨), <code>2</code>(INFO 레벨)과 <code>3</code>(DEBUG 레벨)이며, 기본값은<code>2</code>로 설정되어 있습니다.</td>
</tr>
<tr>
<td><code>--version</code></td>
<td>버전 번호를 출력합니다.</td>
</tr>
<tr>
<td><code>--clean</code></td>
<td>마이그레이션 작업을 종료합니다.</td>
</tr>
</tbody>
</table>
