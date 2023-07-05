## 개요
온라인 마이그레이션이란 시스템 작동을 멈추지 않은 상태에서, 서버나 가상 컴퓨터의 시스템, 서비스 프로세스 등을 자체 구축 데이터 센터(IDC) 혹은 클라우드 플랫폼 등의 환경에서 Tencent Cloud로 마이그레이션 하여 동기화하는 것을 의미합니다.
Tencent Cloud에서는 [go2tencentcloud 마이그레이션 툴](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)을 제공하므로, 마이그레이션 하려는 소스 CVM에서 마이그레이션 툴을 실행하면 CVM 전체를 Tencent Cloud의 타깃 CVM으로 바로 마이그레이션 할 수 있습니다. 이 마이그레이션 툴을 사용하면 이미지를 생성, 업로드 및 가져오는 번거로움 없이, 원본에서 클라우드로 바로 마이그레이션 할 수 있어 기업의 클라우드 도입, 클라우드 플랫폼 간 마이그레이션, 계정/리전 간 마이그레이션 혹은 하이브리드 클라우드 배포 등 비즈니스 수요를 만족할 수 있습니다.

## 마이그레이션 툴 설명

### 지원하는 마이그레이션 모드

<dx-tabs>
::: 기본 모드[](id:DefaultMode)
사용자의 소스 CVM과 타깃 CVM 모두 공용 네트워크 액세스 기능이 있다면 기본 모드의 마이그레이션을 사용할 수 있습니다.
현재 기본 모드에서는, 소스 CVM에서 인터넷을 통해 Tencent Cloud API에 액세스하여 마이그레이션 요청을 보낸 다음, 타깃 CVM에 데이터를 전송함으로써 소스 CVM을 Tencent Cloud의 타깃 CVM으로 마이그레이션합니다.
![](https://main.qcloudimg.com/raw/5203e535f5ba947bb67c1f91dee52f1f.jpg)
:::
::: 내부 네트워크 마이그레이션 모드[](id:intranetMigration)
사용자의 소스 CVM이나 타깃 CVM이 특정 내부 네트워크나 VPC에 있다면 인터넷을 통해 소스 CVM을 타깃 CVM에 바로 연결할 수 없으므로, 툴의 내부 네트워크 마이그레이션 모드로 마이그레이션할 수 있습니다. 내부 네트워크 마이그레이션을 사용하려면 [VPC 피어링 연결](https://intl.cloud.tencent.com/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network(CCN)](https://intl.cloud.tencent.com/document/product/1003) 혹은 [Direct Connect(DC)](https://intl.cloud.tencent.com/document/product/216) 등의 방법으로 소스 CVM과 타깃 CVM 간의 터널을 생성해야 합니다.

- [](id:Scenario1) 시나리오1: 사용자의 소스 CVM 혹은 타깃 CVM이 공용 네트워크에 액세스할 수 없다면, 게이트웨이같이 공용 네트워크 액세스 기능을 갖춘 호스트에서 인터넷을 통해 Tencent Cloud API를 호출하여 마이그레이션을 요청한 다음, 터널을 연결하여 데이터를 타깃 CVM으로 마이그레이션 할 수 있습니다. 이 시나리오에서는 소스 CVM과 타깃 CVM의 공용 네트워크 액세스 기능이 필요하지 않습니다.
![](https://main.qcloudimg.com/raw/19300ddf557d4534b1cd77fcbf64ef6a.jpg)
- [](id:Scenario2) 시나리오2: 사용자의 소스 CVM이 공용 네트워크에 액세스할 수 있다면, 먼저 소스 CVM에서 인터넷을 통해 Tencent Cloud API를 호출하여 마이그레이션을 요청한 다음, 터널을 연결하여 데이터를 타깃 CVM으로 마이그레이션 할 수 있습니다. 이 시나리오에서는 소스 CVM의 공용 네트워크 액세스 기능이 필요하며 타깃 CVM은 해당 기능이 필요하지 않습니다.  
![](https://main.qcloudimg.com/raw/90bf988ba7cddb9b80307efb30eaad29.jpg)
- [](id:Scenario3) 시나리오3: 사용자의 소스 CVM이 프록시를 통해 공용 네트워크에 액세스할 수 있다면, 먼저 소스 CVM에서 네트워크 프록시를 통해 Tencent Cloud API를 호출하여 마이그레이션을 요청한 다음, 터널을 연결하여 데이터를 타깃 CVM으로 마이그레이션 할 수 있습니다. 이 시나리오에서는 소스 CVM과 타깃 CVM의 공용 네트워크 액세스 기능이 필요하지 않습니다.
![](https://main.qcloudimg.com/raw/14f81f2c4e6cfff80d912841451c5b69.jpg)
:::
</dx-tabs>


### 지원하는 운영 체제
현재 온라인 마이그레이션 툴에서는 다음과 같은 소스 CVM 운영 체제(32비트 혹은 64비트)를 지원합니다.
<table>
	<tr><th>Linux 운영 체제</th><th>Windows 운영 체제</th></tr>
	<tr><td>CentOS 5/6/7/8</td><td rowspan=7>-</td></tr>
	<tr><td>Ubuntu 10/12/14/16/18	</td></tr>
	<tr><td>Debian 7/8/9	</td></tr>
	<tr><td>SUSE 11/12/15</td></tr>
	<tr><td>openSUSE 42</td></tr>
	<tr><td>Amazon Linux AMI</td></tr>
	<tr><td>Red Hat 7/8</td></tr>
</table>

### 압축 파일 설명

<table>
	<tr><th>파일 이름</th><th>설명</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>64비트 Linux 시스템의 마이그레이션 툴에서 실행 가능한 프로그램입니다.</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>32비트 Linux 시스템의 마이그레이션 툴에서 실행 가능한 프로그램입니다.</td></tr>
	<tr><td>user.json</td><td>마이그레이션 시 소스 CVM과 타깃 CVM의 구성 파일로, <a href="#userJsonState">user.json 파일 매개변수 설명</a>을 참조하여 설정을 변경하시기 바랍니다.</td></tr>
	<tr><td>client.json</td><td>마이그레이션 툴의 구성 파일로, <a href="#clientJsonState">client.json 파일 매개변수 설명</a>을 참조하여 설정을 변경하시기 바랍니다.</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync 구성 파일로, Linux 시스템에서 마이그레이션 하지 않을 파일 디렉터리를 제외합니다.</td></tr>
</table>

>?  삭제할 수 없는 구성 파일은 go2tencentcloud의 실행 가능 프로그램과 같은 단계의 디렉터리로 이동해 놓으시기 바랍니다. 
>

- <span id="userJsonState">user.json 파일 매개변수 설명:</span>
<table>
	<tr><th>매개변수 이름</th><th>유형</th><th>필수 입력 여부</th><th>설명</th></tr>
	<tr><td>SecretId</td><td>String</td><td>필수</td><td>계정 API 호출 키 SecretId. 이에 관한 세부 정보는 <a href="https://intl.cloud.tencent.com/document/product/598/32675">액세스 키</a>를 참조 바랍니다.</td></tr>
	<tr><td>SecretKey</td><td>String</td><td>필수</td><td>계정 API 호출 키 SecretKey. 이에 관한 세부 정보는 <a href="https://intl.cloud.tencent.com/document/product/598/32675">액세스 키</a>를 참조 바랍니다.</td></tr>
	<tr><td>Region</td><td>String</td><td>필수</td><td>타깃 CVM의 리전. 가용존은 입력하지 않고 리전만 입력하면 되며, 이에 관한 값은 <a href="https://intl.cloud.tencent.com/document/product/213/6091">리전</a> 목록을 참조 바랍니다.</td></tr>
	<tr><td>InstanceId</td><td>String</td><td>필수</td><td>타깃 CVM의 인스턴스 ID. <code>ins-xxxxxxxx</code>와 같은 형식입니다.</td></tr>
	<tr><td>DataDisks</td><td>Array</td><td>선택</td><td>소스 CVM의 마이그레이션 대기 중인 데이터 디스크 목록. 요소마다 하나의 데이터 디스크를 대표하며, 최대 20블록의 데이터 디스크를 지원합니다.</td></tr>
	<tr><td>DataDisks.Index</td><td>Integer</td><td>선택</td><td>데이터 디스크의 시리얼 넘버로, [1,20] 사이의 값을 입력합니다. 값이 <code>1</code>인 경우 해당 블록의 데이터 디스크를 타깃 CVM에 마운트된 첫 번째 블록의 데이터 디스크로 마이그레이션하고, 값이 <code>2</code>인 경우 타깃 CVM에 마운트된 두 번째 블록의 데이터 디스크로 마이그레이션함을 의미하며, 이러한 형식으로 계속 이어집니다.</td></tr>
	<tr><td>DataDisks.Size</td><td>Integer</td><td>선택</td><td>소스 데이터 디스크의 크기로, 단위는 GB이며, [10,16000] 사이의 값을 입력합니다.</td></tr>
	<tr><td>DataDisks.MountPoint	</td><td>String</td><td>선택</td><td>소스 데이터 디스크의 마운트 포인트로, <code>"/mnt/disk1"</code> 등을 예를 들 수 있습니다.</td></tr>
</table>
예시, Linux 소스 CVM을 Tencent Cloud 광저우 리전의 CVM으로 마이그레이션 할 때의 user.json 파일 설정은 다음과 같습니다.
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id"
}  
```
<dx-alert infotype="explain" title="">
해당하는 매개변수 값을 실제 설정 매개변수로 변경하시기 바랍니다.
</dx-alert>
예를 들어 Linux 소스 CVM(마운트 포인트가 <code>/mnt/disk1</code>이며, <code>10</code>GB 크기의 데이터 디스크 한 블록 포함)을 Tencent Cloud 광저우 리전의 타깃 CVM(최소 한 블록의 데이터 디스크가 마운트되어야 함)으로 마이그레이션할 때의 user.json 파일 설정은 다음과 같습니다.
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		}
	]
}  
```
예를 들어 Linux 소스 CVM(포함된 두 데이터 디스크 중, 마운트 포인트가 <code>/mnt/disk1</code>인 <code>10</code>GB 크기의 disk1을 타깃 CVM의 첫 번째 데이터 디스크로 마이그레이션하고, 마운트 포인트가 <code>/mnt/disk2</code>인<code>20</code>GB 크기의 disk2를 타깃 CVM의 두 번째 데이터 디스크로 마이그레이션 하려는 경우)을 Tencent Cloud 광저우 리전의 타깃 CVM(최소 두 데이터 디스크가 마운트 되어있는 경우)으로 마이그레이션 할 때의 user.json 파일 설정은 다음과 같습니다.
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		},
		{
			"Index": 2,
			"Size": 20,
			"MountPoint": "/mnt/disk2"
		}
	]
}  
```
<dx-alert infotype="explain" title="">
해당하는 매개변수 값을 실제 설정 매개변수로 변경하시기 바랍니다.
</dx-alert>
- <span id="clientJsonState">client.json 파일 매개변수 설명: </span>
<table>
	<tr><th>매개변수 이름</th><th>유형</th><th>필수 입력 여부</th><th>설명</th></tr>
	<tr><td>Client.Net.Mode</td><td>Integer</td><td>필수</td><td>기본값은 <code>0</code>이며, 입력 값의 범위는 <code>0</code>(<a href="#DefaultMode">기본 모드</a>), <code>1</code>(<a href="#Scenario1">내부 네트워크 마이그레이션 모드: 시나리오1</a>), <code>2</code>(<a href="#Scenario2">내부 네트워크 마이그레이션 모드: 시나리오2</a>), <code>3</code>(<a href="#Scenario3">내부 네트워크 마이그레이션 모드: 시나리오3</a>)으로 구성되므로, 마이그레이션 시 실제 수요에 맞는 모드 및 시나리오에 해당하는 매개변수 값을 입력하시기 바랍니다.</td></tr>
	<tr><td>Client.Net.Proxy.Ip</td><td>String</td><td>선택</td><td>네트워크 프록시 IP 주소, <a href="#Scenario3">내부 네트워크 마이그레이션 모드: 시나리오3</a>의 마이그레이션을 진행할 경우 필수 입력 사항입니다.</td></tr>
	<tr><td>Client.Net.Proxy.Port</td><td>Integer</td><td>선택</td><td>네트워크 프록시 포트. <a href="#Scenario3">내부 네트워크 마이그레이션 모드: 시나리오3</a>의 마이그레이션을 진행할 경우 필수 입력 사항입니다.</td></tr>
	<tr><td>Client.Net.Proxy.User</td><td>String</td><td>선택</td><td>네트워크 프록시 사용자 이름. <a href="#Scenario3">내부 네트워크 마이그레이션 모드: 시나리오3</a>의 마이그레이션을 진행하고 네트워크 프록시의 인증이 필요하다면, 네트워크 프록시 사용자 이름을 입력하시기 바랍니다.</td></tr>
	<tr><td>Client.Net.Proxy.Password</td><td>String</td><td>선택</td><td>네트워크 프록시 비밀번호. <a href="#Scenario3">내부 네트워크 마이그레이션 모드: 시나리오3</a>의 마이그레이션을 수행하고 네트워크 프록시의 인증이 필요하다면, 네트워크 프록시 비밀번호를 입력하시기 바랍니다.</td></tr>
	<tr><td>Client.Extra.IgnoreCheck</td><td>Bool</td><td>선택</td><td>기본값은 <code>false</code>이며, 마이그레이션 툴 실행을 시작할 때 자동으로 소스 CVM의 환경을 검사하도록 기본 설정되어 있습니다. 검사를 생략하려면 <code>true</code>로 설정하시기 바랍니다.</td></tr>
	<tr><td>Client.Rsync.BandwidthLimit</td><td>String</td><td>선택</td><td>속도 제한 설정 항목으로, 단위는 KBytes/s입니다. 기본값은 공백으로, 전송 시 속도를 제한하지 않도록 기본 설정되어 있습니다.</td></tr>
	<tr><td>Client.Rsync.Checksum</td><td>Bool</td><td>선택</td><td>전송 검사 항목으로, <code>true</code>로 설정하면 전송 일치성 검사가 강화되지만, 소스 CVM의 CPU 부하가 상승하며 전송 속도가 저하될 수 있으며, 검사하지 않도록 <code>false</code>로 기본 설정되어 있습니다.
</table>
<blockquote class="doc-tip"><p class="doc-tip-tit"><i class="doc-icon-tip"></i>설명:</p><p>상기 매개변수 외에, client.json 파일의 나머지 설명 항목은 대체로 입력하지 않아도 됩니다.</p>
</blockquote>
- <span id="_linuxTxtState">rsync\_excludes\_linux.txt 파일 설명:</span>
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

### 툴 실행 매개변수 설명
<table>
<thead>
<tr>
<th width="15%">매개변수 항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><code>--help</code></td>
<td>도움말 정보 출력. </td>
</tr>
<tr>
<td><code>--check</code></td>
<td>소스 CVM에 검사 진행, 마이그레이션 진행하지 않음. </td>
</tr>
<tr>
<td><code>--log-file</code></td>
<td>로그 파일 이름 설정, 기본값은<code>log</code>로 설정되어 있음. </td>
</tr>
<tr>
<td><code>--log-level</code></td>
<td>로그 출력 레벨로，입력값의 범위는<code>1</code>(ERROR 레벨), <code>2</code>(INFO 레벨)과<code>3</code>(DEBUG 레벨)이며，기본값은<code>2</code>로 설정되어 있습니다. </td>
</tr>
<tr>
<td><code>--clean</code></td>
<td>타깃 CVM의 마이그레이션 강제 종료 모드로, 모두 클린합니다. 만약 콘솔에 <code>Please execute '--clean' option manually.</code>와 같은 알림이 뜬다면 해당 옵션에서 툴을 실행하여 타깃 CVM의 마이그레이션 모드를 종료합니다. </td>
</tr>
<tr>
<td><code>--version</code></td>
<td>버전 번호 출력. </td>
</tr>
</tbody></table>

## 마이그레이션 전 점검
마이그레이션을 하기 전, 소스 CVM 및 타깃 CVM에 별도의 점검이 필요합니다. 소스 CVM 및 타깃 CVM에 필요한 점검 내용은 다음과 같습니다.
<table>
	<tr><th style="width: 15%;">타깃 CVM</th><td><ol  style="margin: 0;"><li>스토리지 용량: 소스 데이터를 불러오기에 충분하도록 타깃 CVM의 CBS(시스템 디스크, 데이터 디스크 포함) 스토리지 용량을 확보해야 합니다.</li><li>보안 그룹: 보안 그룹에 443 포트 및 80 포트는 제한할 수 없습니다.</li><li>대역폭 설정: 마이그레이션 속도 향상을 위해, 대역폭의 범위를 가능한 크게 조정하기를 권장합니다. 마이그레이션 과정에서 데이터양과 거의 동일한 트래픽이 소모되므로, 필요할 경우 네트워크 과금 방식을 먼저 변경해 주시기 바랍니다.</li><li>타깃 CVM 및 소스 CVM의 운영 체제 유형 일치 여부: 운영 체제가 다를 경우, 이후에 생성한 이미지의 정보가 실제 운영 체제와 부합하지 않게 되므로, 타깃 CVM과 소스 CVM의 운영 체제 유형을 통일해 주시기 바랍니다. 예를 들어, CentOS 7 시스템의 소스 CVM 마이그레이션 시 타깃 CVM도 CentOS 7 시스템이어야 합니다.</li></ol></td></tr>
	<tr><th>Linux 소스 CVM</th><td><ol  style="margin: 0;"><li>Virtio를 점검 및 설치합니다. 자세한 작업 방식은 <a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux 시스템 Virtio 드라이버 점검</a>을 참조 바랍니다.</li><li><code>which rsync</code> 명령어를 실행하여 rsync의 설치 여부를 확인합니다. </li><li>SELinux가 열려있는지 확인합니다. 만약 SELinux가 열려있다면, SELinux를 종료하시기 바랍니다.</li><li>Tencent Cloud API에 마이그레이션 요청을 보내면, 클라우드 API가 현재 UNIX 시간을 사용하여 생성된 Token을 점검하므로, 시스템 시간이 정확한지 확인하시기 바랍니다.</li></ol></td></tr>
</table>

>? 
> - 소스 CVM은 `sudo ./go2tencentcloud_x64 --check`와 같은 툴 명령어를 사용하여 자동으로 점검할 수 있습니다.
> - go2tencentcloud 마이그레이션 툴은 실행 시작 시 자동 점검하도록 기본 설정되어 있습니다. 점검 과정을 건너뛰고 강제 마이그레이션 하려는 경우, client.json 파일의 `Client.Extra.IgnoreCheck` 필드를 `true`로 설정하시기 바랍니다.
> 

## 마이그레이션 과정
Tencent Cloud에서 제공하는 go2tencentcloud 마이그레이션 툴의 마이그레이션 과정은 크게 세 가지 단계로 나뉩니다. 사용자는 툴을 실행하는 과정에서 마이그레이션 진도를 직관적으로 확인할 수 있습니다.
- **1단계**: 타깃 CVM의 마이그레이션 모드 진입 단계. 마이그레이션을 준비합니다.
- **2단계**: 타깃 CVM의 마이그레이션 모드 진행 단계. 데이터를 마이그레이션 합니다.
- **3단계**: 타깃 CVM의 마이그레이션 모드 종료 단계. 마이그레이션을 완료합니다.

각 단계에서는 일련의 서브 작업을 실행해야 하며, 오랜 시간을 소모하는 일부 서브 작업은 최대 타임아웃 시간이 기본 설정되어 있습니다. 데이터 전송의 소요 시간은 소스 데이터 크기, 네트워크 대역폭 등의 영향을 받으므로, 마이그레이션 과정이 완료될 때까지 기다려 주시기 바랍니다. 마이그레이션 툴은 데이터 전송 시 중단점에 이어서 전송할 수 있도록 지원합니다.

>! 마이그레이션을 시작한 후에는 타깃 CVM이 마이그레이션 모드에 들어가므로, 마이그레이션이 완료되어 마이그레이션 모드를 종료할 때까지 타깃 CVM에 시스템 재설치, 셧다운, 폐기, 비밀번호 재설정 등의 작업을 실행하지 마시길 바랍니다. 
>

<dx-tabs>
::: 기본 모드의 마이그레이션 과정
1. user.json 파일에 타깃 CVM을 설정합니다.
[user.json 파일 매개변수 설명](#userJsonState)에 따라 필수 항목과 필요 항목에 대한 값을 설정합니다.
2. client.json 파일에 마이그레이션 모드와 기타 항목을 설정합니다.
client.json 파일 안의 `Client.Net.Mode` 항목을 `0`으로 설정하여 [기본 모드](#DefaultMode) 마이그레이션을 실행합니다. 이외에 다른 항목을 설정해야 한다면 [client.json 파일 매개변수 설명](#clientJsonState)에 따라 설정하시기 바랍니다.
3. 소스 CVM에서 마이그레이션 하지 않을 파일 또는 디렉터리를 제외합니다. (선택)
Linux 소스 CVM을 마이그레이션 할 때 일부 마이그레이션 하지 않을 파일 및 디렉터리를 제외해야 한다면, [rsync\_excludes\_linux.txt 파일](#_linuxTxtState)으로 추가할 수 있습니다.
4. 툴을 실행합니다.
예를 들어, 64비트 Linux 소스 CVM에서는 root 권한으로 다음 명령어를 실행하여 툴을 실행합니다.
```
sudo ./go2tencentcloud_x64
```
툴을 실행할 때 로그 파일 이름 및 로그 출력 수준을 설정해야 한다면 다음 명령어를 실행할 수 있습니다.
```
sudo ./go2tencentcloud --log-file=my.log --log-level=3
```
툴을 실행한 후, 마이그레이션 과정이 완료될 때까지 기다려 주시기 바랍니다. 
기본 모드에서 마이그레이션 성공 시 콘솔에 출력되는 내용은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)
:::
::: 내부 네트워크 마이그레이션 모드의 마이그레이션 과정
#### 시나리오1의 마이그레이션 과정
1. 소스 CVM과 타깃 CVM의 연결 터널을 생성합니다.
[VPC 피어링 연결](https://intl.cloud.tencent.com/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network(CCN)](https://intl.cloud.tencent.com/document/product/1003) 등의 방법으로 소스 CVM과 타깃 CVM의 연결 터널을 생성해야 합니다.
2. user.json 파일에 타깃 CVM을 설정합니다.
 [user.json 파일 매개변수 설명](#userJsonState)에 따라 필수 항목과 필요 항목에 대한 값을 설정합니다.
3. client.json 파일에 마이그레이션 모드와 기타 항목을 설정합니다.
client.json 파일 안의 `Client.Net.Mode` 항목을 `1`로 설정하여 [내부 네트워크 마이그레이션 모드: 시나리오1](#Scenario1) 마이그레이션을 실행합니다. 이외에 다른 항목을 설정해야 한다면 [client.json 파일 매개변수 설명](#clientJsonState)에 따라 설정하시기 바랍니다.
4. 소스 CVM에서 마이그레이션 하지 않을 파일 또는 디렉터리를 제외합니다. (선택)
Linux 소스 CVM을 마이그레이션 할 때 일부 마이그레이션 하지 않을 파일 및 디렉터리를 제외해야 한다면, [rsync_excludes_linux.txt 파일](#_linuxTxtState)로 추가할 수 있습니다.
5. <span id="Scenario1_step05">게이트웨이같이 공용 네트워크에 액세스할 수 있는 호스트에서 툴을 실행합니다.</span>
예를 들어, 공용 네트워크에 액세스할 수 있는 CVM에서 다음 명령어로 툴을 실행하여, 1단계 마이그레이션을 진행합니다.
```
sudo ./go2tencentcloud_x64
```
`Stage 1 is finished and please run next stage at source machine.`라는 문구가 출력되면, 1단계 마이그레이션이 완료되었다는 의미입니다.
![](https://main.qcloudimg.com/raw/f861b47c464f58ea184e5cc5a6a30e1c.png)

6. <span id="Scenario1_step06">마이그레이션 대기 중인 소스 CVM에서 툴을 실행합니다.</span>
[과정5](#Scenario1_step05)(1단계)가 완료되면, 1단계의 모든 툴 목록을 마이그레이션할 소스 CVM에 복사한 뒤, 다시 툴을 실행하여 2단계 마이그레이션을 진행합니다.
예를 들어, 다음 명령어로 툴을 실행하여 2단계 마이그레이션을 진행합니다.

```
sudo ./go2tencentcloud_x64
```
만약 `Stage 2 is finished and please run next stage at gateway이 나타난다면 
machine.`는 2단계 마이그레이션이 완료되었다는 의미입니다.
![](https://main.qcloudimg.com/raw/5684fc8aee6ebf8ba01e42deff3b4fc2.png)
7. 게이트웨이같이 공용 네트워크에 액세스할 수 있는 호스트에서 툴을 실행합니다.
[과정6](#Scenario1_step06)(2단계)가 완료되면, 2단계의 모든 툴 목록을 1단계의 CVM에 복사한 뒤, 다시 툴을 실행하여 3단계 마이그레이션을 진행합니다.
예를 들어, 다음 명령어로 툴을 실행하여 3단계 마이그레이션을 진행합니다.
```
sudo ./go2tencentcloud_x64
```
`Migrate successfully.`라는 문구가 출력되면, 모든 마이그레이션 작업이 완료되었다는 의미입니다.
![](https://main.qcloudimg.com/raw/851e90fdc07fb601d3d158386d524985.png)

#### 시나리오2의 마이그레이션 과정

1. 소스 CVM과 타깃 CVM의 연결 터널을 생성합니다.
[VPC 피어링 연결](https://intl.cloud.tencent.com/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network(CCN)](https://intl.cloud.tencent.com/document/product/1003) 등의 방법으로 소스 CVM과 타깃 CVM의 연결 터널을 생성해야 합니다.
2. user.json 파일에 타깃 CVM을 설정합니다.
 [user.json 파일 매개변수 설명](#userJsonState)에 따라 필수 항목과 필요 항목에 대한 값을 설정합니다.
3. client.json 파일에 마이그레이션 모드와 기타 항목을 설정합니다.
 client.json 파일 안의 `Client.Net.Mode` 항목을 `2`로 설정하여 [내부 네트워크 마이그레이션 모드: 시나리오2](#Scenario2) 마이그레이션을 실행합니다. 이외에 다른 항목을 설정해야 한다면 [client.json 파일 매개변수 설명](#clientJsonState)에 따라 설정하시기 바랍니다.
4. 소스 CVM에서 마이그레이션 하지 않을 파일 또는 디렉터리를 제외합니다. (선택)
Linux 소스 CVM을 마이그레이션 할 때 일부 마이그레이션 하지 않을 파일 및 디렉터리를 제외해야 한다면, [rsync_excludes_linux.txt 파일](#_linuxTxtState)으로 추가할 수 있습니다.
5. 툴을 실행합니다.
예를 들어, 64비트 Linux 소스 CVM에서는 root 권한으로 다음 명령어를 실행하여 툴을 실행합니다.

```
sudo ./go2tencentcloud_x64
```
툴을 실행한 후, 마이그레이션 과정이 완료될 때까지 기다려 주시기 바랍니다.

마이그레이션 성공 시 콘솔에 출력되는 내용은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/d32b4be8287d4b06697f0cb03cc6cff8.png)

#### 시나리오3의 마이그레이션 과정

1. 소스 CVM과 타깃 CVM의 연결 터널을 생성합니다.
 [VPC 피어링 연결](https://intl.cloud.tencent.com/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network(CCN)](https://intl.cloud.tencent.com/document/product/1003) 등의 방법으로 소스 CVM과 타깃 CVM의 연결 터널을 생성합니다.
2. user.json 파일에 타깃 CVM을 설정합니다.
[user.json 파일 매개변수 설명](#userJsonState)에 따라 필수 항목과 필요 항목에 대한 값을 설정합니다.
3. client.json 파일에 마이그레이션 모드와 기타 항목을 설정합니다.
 1. client.json 파일 안의 `Client.Net.Mode` 항목을 `3`으로 설정하여 [내부 네트워크 마이그레이션 모드: 시나리오3](#Scenario3) 마이그레이션을 실행합니다.
 2. client.json 파일 안의 `Client.Net.Proxy.Ip`와 `Client.Net.Proxy.Port` 항목을 네트워크 프록시의 IP 주소 및 포트로 설정합니다.
네트워크 프록시에 대한 인증이 필요하다면 `Client.Net.Proxy.User`와 `Client.Net.Proxy.Password` 항목에 네트워크 프록시의 사용자 이름과 비밀번호를 입력해야 합니다. 인증이 필요하지 않다면 입력하지 않아도 됩니다. 이외에 다른 항목을 설정해야 한다면 [client.json 파일 매개변수 설명](#clientJsonState)에 따라 설정하시기 바랍니다.
4. 소스 CVM에서 마이그레이션 하지 않을 파일 또는 디렉터리를 제외합니다. (선택)
Linux 소스 CVM을 마이그레이션 할 때 일부 마이그레이션 하지 않을 파일 및 디렉터리를 제외해야 한다면, [rsync_excludes_linux.txt 파일](#_linuxTxtState)으로 추가할 수 있습니다.
5. 툴을 실행합니다.
예를 들어, 64비트 Linux 소스 CVM에서는 root 권한으로 다음 명령어를 실행하여 툴을 실행합니다.

```
sudo ./go2tencentcloud_x64
```
툴을 실행한 후, 마이그레이션 과정이 완료될 때까지 기다려 주시기 바랍니다.
마이그레이션 성공 시 콘솔에 출력되는 내용은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/2195589176d3669f08fbb5745901040b.png)
:::
</dx-tabs>


## 마이그레이션 후 점검
1. 마이그레이션에 실패했다는 결과가 나올 경우, 로그 파일(마이그레이션 툴 디렉터리 안의 log 파일로 기본 설정)의 오류 정보 출력, 가이드 문서 또는 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)을 확인하여 문제를 해결하거나 복구하시기 바랍니다.
2. 마이그레이션에 성공했다는 결과가 나올 경우, 타깃 CVM이 정상적으로 실행되는지, 타깃 CVM의 데이터가 소스 CVM과 일치하는지, 네트워크가 정상적인지 또는 다른 시스템 서비스가 정상적인지 등을 확인하시기 바랍니다.
3. 문의 사항이나 마이그레이션 오류 문제 등이 있다면 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 조회하거나 [고객센터](https://intl.cloud.tencent.com/document/product/213/34837)을 통해 해결하실 수 있습니다.

