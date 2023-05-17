본문은 go2tencentcloud 마이그레이션 툴을 사용하여 Linux 시스템 서버의 온라인 마이그레이션을 수행하는 방법을 소개합니다.

## 준비 사항

- Tencent Cloud 계정과 대상 CVM이 있어야 합니다.
- 마이그레이션할 때, 현재 사용하고 있는 애플리케이션에 영향을 줄 수 있으므로, 원본 서버의 애플리케이션 사용을 잠시 중지할 것을 권장합니다.
- 마이그레이션 툴 압축 패키지를 [다운로드](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)합니다.
- [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 'SecretId' 및 'SecretKey'를 생성 및 획득합니다.
- 원본 호스트와 대상 CVM이 마이그레이션 조건을 충족하는지 확인합니다. 예를 들어, 대상 CVM의 CBS에는 반드시 원본 호스트 데이터를 저장할 충분한 스토리지 용량이 확보되어야 합니다.
- 마이그레이션하기 전에 다음과 같은 방법으로 데이터를 백업하는 것이 좋습니다.
 - 원본 호스트: 원본 서버 스냅샷 기능 등의 방식을 선택해 데이터를 백업할 수 있습니다.
 - 대상 CVM: [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755) 등의 방식을 선택해 대상 CVM 데이터를 백업할 수 있습니다.

## 마이그레이션 툴킷 설명

### 압축 파일 설명

`go2tencentcloud.zip` 압축 해제 후 파일 설명은 다음과 같습니다.
<table>
	<tr><th width="30%">파일 이름</th><th>설명</th></tr>
	<tr><td>go2tencentcloud-linux.zip</td><td>Linux 시스템용 마이그레이션 zip.</td></tr>
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

<dx-alert infotype="notice" title="">
삭제할 수 없는 구성 파일은 go2tencentcloud의 실행 가능 프로그램과 같은 단계의 디렉터리로 이동해 놓으시기 바랍니다. 
</dx-alert>

### user.json 파일 매개변수 설명[](id:userJsonState)

user.json 구성 파일은 다음과 같이 설명됩니다.

<table>
  <tr>
	<th>매개변수 이름</th>
	<th>유형</th>
	<th>필수 입력 여부</th>
	<th>설명</th>
  </tr>
  <tr>
	<td>SecretId</td>
	<td>String</td>
	<td>Yes</td>
	<td>계정 API 액세스 키 SecretId. 자세한 내용은  
	<a href="https://intl.cloud.tencent.com/document/product/598/32675">액세스 키</a>를 참고하십시오.</td>
  </tr>
  <tr>
	<td>SecretKey</td>
	<td>String</td>
	<td>Yes</td>
	<td>계정 API 액세스 키 SecretKey. 자세한 내용은  
	<a href="https://intl.cloud.tencent.com/document/product/598/32675">액세스 키</a>를 참고하십시오.</td>
  </tr>
  <tr>
	<td>Region</td>
	<td>String</td>
	<td>Yes</td>
	<td>대상 클라우드 서버의 리전은, 리전만 기입하면 되며, 가용존은 기입하지 않으셔도 됩니다. 값은  
	<a href="https://intl.cloud.tencent.com/document/product/213/6091">리전</a> 리스트를 참고하십시오.</td>
  </tr>
  <tr>
	<td>InstanceId</td>
	<td>String</td>
	<td>Yes</td>
	<td>대상 클라우드 서버의 인스턴스 ID. 형식:  
	<code>ins-xxxxxxxx</code>.</td>
  </tr>
  <tr>
	<td>DataDisks</td>
	<td>Array</td>
	<td>No</td>
	<td>원본 호스트에서 마이그레이션할 데이터 디스크 리스트로, 각 요소는 데이터 디스크를 나타내며 최대 20개의 데이터 디스크를 지원합니다.</td>
  </tr>
  <tr>
	<td>DataDisks.Index</td>
	<td>Integer</td>
	<td>No</td>
	<td>데이터 디스크의 일련 번호 범위는 [1에서 20 사이]입니다. 값이 <code>1</code>이면 데이터 디스크가 대상 CVM에 마이그레이션되고 연결되는 첫 번째 디스크임을 나타냅니다. 값이 <code>2</code>이면 데이터 디스크가 두 번째로 마이그레이션되어 대상 CVM에 연결됨을 나타내는 식입니다.</td>
  </tr>
  <tr>
	<td>DataDisks.Size</td>
	<td>Integer</td>
	<td>No</td>
	<td>원본 데이터 디스크 크기. 단위: GB, 범위: [10,16000].</td>
  </tr>
  <tr>
	<td>DataDisks.MountPoint</td>
	<td>String</td>
	<td>No</td>
	<td>원본 데이터 디스크 마운트 포인트. 예:  
	<code>&quot;/mnt/disk1&quot;</code>.</td>
  </tr>
</table>

다음 예시를 참고하여 실제 비즈니스 시나리오를 기반으로 구성 파일을 수정할 수 있습니다.
 - 예시1: Linux 소스 CVM을 Tencent Cloud 광저우 리전의 CVM으로 마이그레이션 할 때의 `user.json` 파일 설정은 다음과 같습니다.
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id"
} 
```
 - 예시2: Linux 소스 CVM(마운트 포인트가 `/mnt/disk1`이며, `10GB` 크기의 데이터 디스크 한 블록 포함)을 Tencent Cloud 광저우 리전의 대상 CVM(최소 한 블록의 데이터 디스크가 마운트되어야 함)으로 마이그레이션할 때의 `user.json` 파일 설정은 다음과 같습니다.
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
 - 예시3: Linux 소스 CVM(포함된 두 데이터 디스크 중, 마운트 포인트가 `/mnt/disk1`인 `10GB` 크기의 disk1을 대상 CVM의 첫 번째 데이터 디스크로 마이그레이션하고, 마운트 포인트가 `/mnt/disk2`인 `20GB` 크기의 disk2를 대상 CVM의 두 번째 데이터 디스크로 마이그레이션 하려는 경우)을 Tencent Cloud 광저우 리전의 CVM(최소 두 데이터 디스크가 마운트 되어있는 경우)으로 마이그레이션 할 때의 `user.json` 파일 설정은 다음과 같습니다.
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
	<td>Client.ToolMode</td>
	<td>bool</td>
	<td>No</td>
	<td>툴 마이그레이션 모드 식별자로, 기본값은 <code>false</code>입니다. 툴을 통한 마이그레이션이 필요한 경우 값을 <code>true</code>로 수정하거나 툴 실행 시 <code>--no-console</code> 매개변수를 추가합니다.</td>
  </tr>
  <tr>
	<td>Client.Net.Mode</td>
	<td>Integer</td>
	<td>Yes</td>
	<td>마이그레이션 모드. 기본값은<code>0</code>이며 공용 네트워크 마이그레이션을 나타냅니다. 유효 값:<code>0</code>(<a href="https://intl.cloud.tencent.com/document/product/213/44340">공용 네트워크 마이그레이션 모드</a>), <code>1</code>(<a href="https://intl.cloud.tencent.com/document/product/213/44340">사설 네트워크 마이그레이션 모드: 시나리오 1</a>), <code>2</code>(<a href="https://intl.cloud.tencent.com/document/product/213/44340">사설 네트워크 마이그레이션 모드: 시나리오 2</a>), <code>3</code>(<a href="https://intl.cloud.tencent.com/document/product/213/44340">사설 네트워크 마이그레이션 모드: 시나리오 3</a>).</td>
  </tr>
  <tr>
	<td>Client.Extra.IgnoreCheck</td>
	<td>Bool</td>
	<td>No</td>
	<td>기본값은 <code>false</code>입니다. 기본적으로 마이그레이션 툴은 툴 실행이 시작될 때 소스 서버 환경을 자동으로 확인합니다. 확인을 건너뛰려면 이 매개변수를 <code>true</code>로 설정하십시오.</td>
  </tr>
  <tr>
	<td>Client.Rsync.BandwidthLimit</td>
	<td>String</td>
	<td>No</td>
	<td>속도 제한 구성 항목. 단위: KBytes/s. 기본값: 공란. 즉, 전송 속도는 기본적으로 제한되지 않습니다.</td>
  </tr>
  <tr>
	<td>Client.Rsync.Checksum</td>
	<td>Bool</td>
	<td>No</td>
	<td>전송 확인. 이 매개변수를 <code>true</code>로 설정하면 전송 일관성 검증을 향상시킬 수 있지만 소스 서버의 CPU
	부하가 증가하고 전송 속도가 느려집니다. 기본값은 기본적으로 확인되지 않음을 의미하는 <code>false</code>입니다.</td>
  </tr>
</table>

원본 서버 또는 대상 CVM 모두 공용 네트워크에 직접 액세스할 수 없는 경우 [VPC Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connection](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003) 또는 [Direct Connect](https://intl.cloud.tencent.com/document/product/216)를 통해 연결을 설정한 다음 사설 네트워크 모드를 통해 마이그레이션할 수 있습니다. 소스 서버 및 대상 CVM의 네트워크 환경에 따라 적절한 마이그레이션 모드를 결정합니다.

###  rsync\_excludes\_linux.txt 파일 설명[](id:_linuxTxtState)

Linux 소스 CVM에서 마이그레이션하지 않을 파일을 제외하거나 디렉터리 안의 구성 파일을 지정합니다. 다음의 디렉터리 및 파일이 제외 파일로 기본 설정되어 있습니다. **삭제하지 마시기 바랍니다**.
```shellsession
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
```
다른 디렉터리 및 파일을 제외하고 싶다면 해당 파일 끝에 내용을 추가하시기 바랍니다. 예시: `/mnt/disk1`에 마운트되어 있는 데이터 디스크의 모든 내용 제외.
```shellsession
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
<th width="18%">매개변수 항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td><code>--help</code></td>
<td>도움말 정보 출력. </td>
</tr>
<tr>
<td><code>--no-console</code></td>
<td>툴을 통해서만 마이그레이션됩니다(콘솔에서 마이그레이션하지 않음).</td>
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
<td><code>--clean</code></td>
<td>대상 CVM이 마이그레이션 모드를 종료하고 사이트를 정리하도록 합니다. 예를 들어 콘솔에 Please execute ‘--clean’ option manually. 라는 메시지가 표시되면 이 매개변수를 사용하여 대상 CVM이 마이그레이션 모드를 종료하도록 해야 합니다.</td>
</tr>
<tr>
<td><code>--version</code></td>
<td>버전 번호 출력.</td>
</tr>
</tbody>
</table>


## 마이그레이션 과정

### 데이터 백업
- 원본 호스트: 원본 서버 스냅샷 기능 등의 방식을 선택해 데이터를 백업할 수 있습니다.
- 타깃 CVM: [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755) 등의 방식을 선택해 데이터를 백업할 수 있습니다.


### 마이그레이션 사전 점검
마이그레이션하기 전에 원본 호스트와 대상 CVM을 별도로 확인해야 합니다. 다음 표를 확인하십시오.
<table>
  <tr>
	<th style="width: 15%;">타깃 CVM</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		스토리지 공간: 타깃 CVM의 CBS(시스템 디스크 및 데이터 디스크 포함)에는 원본측에서 데이터를 로드할 수 있는 충분한 저장 공간이 있어야 합니다.</li>
		<li>보안 그룹: 443 포트 및 80 포트는 보안 그룹에서 제한할 수 없습니다.</li>
		<li>
		대역폭 설정: 더 빠른 마이그레이션을 위해 양쪽 끝의 대역폭을 최대한 늘리는 것이 좋습니다. 마이그레이션 과정에서 대략 데이터 양만큼의 트래픽 소모가 발생하게 되며, 필요한 경우 미리 네트워크 과금 모드를 변경하시기 바랍니다.</li>
		<li>
		대상 ECS와 원본 호스트의 운영 체제 유형이 동일한지 여부: 운영 체제가 일치하지 않으면 후속 이미지의 정보가 실제 운영 체제와 일치하지 않을 수 있으므로 대상 CVM의 운영 체제는 원본 호스트의 운영 체제 유형과 일치하는 것이 좋습니다. 예를 들어 CentOS
		7 시스템의 원본 호스트를 마이그레이션할 때 CentOS 7 시스템의 CVM을 마이그레이션 대상으로 선택합니다.</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th>Linux 원본 호스트</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtio 확인 및 설치, 작업의 세부 사항은 다음을 참고하십시오. 
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux 시스템 Virtio 드라이버 확인</a>.</li>
		<li>실행 
		<code>which rsync</code> rsync가 설치되어 있는지 확인하는 명령어입니다. 설치되어 있지 않다면 <a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">Rsync 설치 방법</a>을 참고하여 설치를 진행하십시오.</li>
		<li>SELinux의 활성화 여부를 확인하십시오. SELinux가 활성화되어 있으면 <a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">SELinux 비활성화 방법</a>을 참고하여 비활성화하십시오.</li>
		<li>Tencent Cloud API로 마이그레이션 요청이 이루어진 후 Cloud API는 현재의 UNIX 타임을 사용하여 생성된 
		Token을 검사합니다. 현재 시스템 시간이 올바른지 확인하십시오.</li>
	  </ol>
	</td>
  </tr>
</table>

<dx-alert infotype="explain" title="">
- `./go2tencentcloud_x64 --no-console --check`과 같은 툴 명령을 사용하여 소스 서버를 자동으로 확인할 수 있습니다.
- go2tencentcloud 마이그레이션 툴은 실행 시작 시 자동 점검하도록 기본 설정되어 있습니다. 점검 과정을 건너뛰고 강제 마이그레이션 하려면 client.json 파일의 `Client.Extra.IgnoreCheck` 필드를 `true`로 설정합니다.
</dx-alert>


### 마이그레이션 시작

Tencent Cloud에서 제공하는 go2tencentcloud 마이그레이션 툴은 체크포인트 재시작을 지원하며 마이그레이션 과정은 크게 세 단계로 나뉩니다. 사용자는 툴 실행 과정에서 마이그레이션 진행률을 직관적으로 확인할 수 있습니다.

- **1단계**: 대상 CVM의 마이그레이션 모드 진입 단계. 마이그레이션을 준비합니다.
- **2단계**: 대상 CVM의 마이그레이션 모드 진행 단계. 데이터를 마이그레이션 합니다.
- **3단계**: 대상 CVM의 마이그레이션 모드 종료 단계. 마이그레이션을 완료합니다.

각 단계에서는 일련의 서브 작업을 실행해야 하며, 오랜 시간을 소모하는 일부 서브 작업은 최대 타임아웃 시간이 기본 설정되어 있습니다. 데이터 전송의 소요 시간은 소스 데이터 크기, 네트워크 대역폭 등의 영향을 받으므로, 마이그레이션 과정이 완료될 때까지 기다려 주시기 바랍니다.
<dx-alert infotype="notice" title="">
마이그레이션을 시작한 후에는 대상 CVM이 마이그레이션 모드에 들어가므로, 마이그레이션이 완료되어 마이그레이션 모드를 종료할 때까지 대상 CVM에 시스템 재설치, 셧다운, 폐기, 비밀번호 재설정 등의 작업을 실행하지 마시길 바랍니다. 
</dx-alert>

<dx-tabs>

:::  공용 네트워크 마이그레이션

1. 마이그레이션 툴 go2tencentcloud.zip을 원본 호스트에 다운로드하거나 업로드하고 다음 명령을 실행하여 해당 디렉터리로 들어갑니다.
  1. 다음 명령어를 순서대로 실행하여 go2tencentcloud.zip의 압축을 풀고 디렉터리로 들어갑니다.
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
  2. 다음 명령어를 순서대로 실행하여 go2tencentcloud-linux.zip의 압축을 풀고 디렉터리로 들어갑니다.
```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
`go2tencentcloud` 디렉터리에 있는 파일은 마이그레이션되지 않으므로 이 디렉터리에 마이그레이션할 파일을 두지 마십시오.
</dx-alert>
2. `user.json` 파일에 타깃 CVM을 설정합니다.
[user.json 파일 매개변수 설명](#userJsonState)에 따라 필수 항목과 필요 항목에 대한 값을 설정합니다.
3. `client.json` 파일에 마이그레이션 모드와 기타 항목을 설정합니다.
`client.json` 파일에서 `Client.ToolMode'를 `true`로 설정합니다. 즉, 툴을 통한 마이그레이션을 선택합니다. 필요한 경우 [client.json 파일의 매개변수 설명](#clientJsonState)을 기반으로 다른 매개변수를 구성합니다.
4. (옵션)원본 CVM에서 마이그레이션하지 않을 파일 또는 디렉터리를 제외합니다.
Linux 소스 서버에서 [rsync_excludes_linux.txt 파일](#_linuxTxtState)로 마이그레이션할 필요가 없는 파일 또는 디렉터리를 추가합니다.
5. 툴을 실행합니다.
예를 들어, 64비트 Linux 소스 서버에서는 root 권한으로 다음 명령어를 실행하여 툴을 실행합니다.
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
client.json에서 `Client.ToolMode`를 `true`로 수정하지 않은 경우 아래와 같이 툴을 실행할 때 `--no-console` 매개변수를 추가해야 합니다.
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
툴이 실행된 후 마이그레이션이 끝날 때까지 기다립니다. 일반적으로 성공적인 공용 네트워크 마이그레이션의 콘솔 출력은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)

:::
:::  사설 네트워크 마이그레이션 시나리오 1

1. 소스 CVM과 타깃 CVM의 연결 터널을 생성합니다.
[Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003) 등의 방법으로 원본 호스트와 타깃 CVM의 연결 터널을 생성합니다.
2. 마이그레이션 툴 go2tencentcloud.zip을 원본 호스트에 다운로드하거나 업로드하고 다음 명령을 실행하여 해당 디렉터리로 들어갑니다.
   1. 다음 명령어를 순서대로 실행하여 go2tencentcloud.zip의 압축을 풀고 디렉터리로 들어갑니다.
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
   2. 다음 명령어를 순서대로 실행하여 go2tencentcloud-linux.zip의 압축을 풀고 디렉터리로 들어갑니다.
```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
`go2tencentcloud` 디렉터리에 있는 파일은 마이그레이션되지 않으므로 이 디렉터리에 마이그레이션할 파일을 두지 마십시오.
</dx-alert>
3. `user.json` 파일에 타깃 CVM을 설정합니다.
[user.json 파일 매개변수 설명](#userJsonState)에 따라 필수 항목과 필요 항목에 대한 값을 설정합니다.
4. `client.json` 파일에 마이그레이션 모드와 기타 항목을 설정합니다.
   - `client.json` 파일의 `Client.ToolMode` 값을 `true`로 설정하여 툴 모드 마이그레이션을 식별합니다.
   - `client.json` 파일의 `Client.Net.Mode` 항목을 `1`, 즉 [사설 네트워크 마이그레이션 모드: 시나리오 1](https://intl.cloud.tencent.com/document/product/213/44340#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BF.81.E7.A7.BB.E6.A8.A1.E5.BC.8F)의 마이그레이션으로 설정합니다. 또한, 다른 항목을 설정해야 하는 경우 [client.json 파일 매개변수 설명](#clientJsonState)에 따라 구성하십시오.
5. (옵션)원본 호스트에서 마이그레이션하지 않을 파일 또는 디렉터리를 제외합니다.
마이그레이션할 필요가 없는 파일이나 디렉터리가 Linux 원본 호스트에 있는 경우 [rsync_excludes_linux.txt 파일](#_linuxTxtState)에 파일이나 디렉터리를 추가할 수 있습니다.
6. [](id:Scenario1_step06)게이트웨이같이 공용 네트워크에 액세스할 수 있는 호스트에서 툴을 실행합니다.
예를 들어, 공용 네트워크에 액세스할 수 있는 CVM에서 다음 명령어로 툴을 실행하여, 1단계 마이그레이션을 진행합니다.
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
client.json의 'Client.ToolMode'를 'true'로 수정하지 않은 경우 툴을 실행할 때 다음과 같이 '--no-console' 매개변수를 추가해야 합니다.
```shell
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
`Stage 1 is finished and please run next stage at source machine.`라는 문구가 출력되면, 1단계 마이그레이션이 완료되었다는 의미입니다. 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/f861b47c464f58ea184e5cc5a6a30e1c.png)
7. [](id:Scenario1_step07)마이그레이션 대기 중인 원본 호스트에서 툴을 실행합니다.
[6단계](#Scenario1_step06)(1단계)가 완료되면, 1단계의 모든 툴 목록을 마이그레이션할 소스 CVM에 복사한 뒤, 다시 툴을 실행하여 2단계 마이그레이션을 진행합니다.
예를 들어, 다음 명령어로 툴을 실행하여 2단계 마이그레이션을 진행합니다.
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
client.json의 'Client.ToolMode'를 'true'로 수정하지 않은 경우 툴을 실행할 때 다음과 같이 '--no-console' 매개변수를 추가해야 합니다.
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
`Stage 2 is finished and please run next stage at gateway machine.`라는 문구가 제시되면, 2단계 마이그레이션이 완료되었다는 의미입니다. 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/5684fc8aee6ebf8ba01e42deff3b4fc2.png)
8. 게이트웨이같이 공용 네트워크에 액세스할 수 있는 호스트에서 툴을 실행합니다.
[7단계](#Scenario1_step07)(2단계)가 완료되면, 2단계의 모든 툴 목록을 1단계의 CVM에 복사한 뒤, 다시 툴을 실행하여 3단계 마이그레이션을 진행합니다.
예를 들어, 다음 명령어로 툴을 실행하여 3단계 마이그레이션을 진행합니다.
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
client.json의 'Client.ToolMode'를 'true'로 수정하지 않은 경우 툴을 실행할 때 다음과 같이 '--no-console' 매개변수를 추가해야 합니다.
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
`Migrate successfully.`라는 문구가 출력되면, 모든 마이그레이션 작업이 완료되었다는 의미입니다. 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/851e90fdc07fb601d3d158386d524985.png)




:::
:::  사설 네트워크 마이그레이션 시나리오 2

1. 소스 CVM과 타깃 CVM의 연결 터널을 생성합니다.
[Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003) 등의 방법으로 원본 호스트와 타깃 CVM의 연결 터널을 생성합니다.
2. 마이그레이션 툴 go2tencentcloud.zip을 원본 호스트에 다운로드하거나 업로드하고 다음 명령을 실행하여 해당 디렉터리로 들어갑니다.
   1. 다음 명령어를 순서대로 실행하여 go2tencentcloud.zip의 압축을 풀고 디렉터리로 들어갑니다.
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
    2. 다음 명령어를 순서대로 실행하여 go2tencentcloud-linux.zip의 압축을 풀고 디렉터리로 들어갑니다.
```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
`go2tencentcloud` 디렉터리에 있는 파일은 마이그레이션되지 않으므로 이 디렉터리에 마이그레이션할 파일을 두지 마십시오.
</dx-alert>
3. `user.json` 파일에 타깃 CVM을 설정합니다.
[user.json 파일 매개변수 설명](#userJsonState)에 따라 필수 항목과 필요 항목에 대한 값을 설정합니다.
4. `client.json` 파일에 마이그레이션 모드와 기타 항목을 설정합니다.
    - `client.json` 파일의 `Client.ToolMode` 값을 `true`로 설정하여 툴 모드 마이그레이션을 식별합니다.
    - `client.json` 파일의 `Client.Net.Mode` 항목을 `2`, 즉 [사설 네트워크 마이그레이션 모드: 시나리오 2](https://intl.cloud.tencent.com/document/product/213/44340#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BF.81.E7.A7.BB.E6.A8.A1.E5.BC.8F)의 마이그레이션으로 설정합니다. 또한, 다른 항목을 설정해야 하는 경우 [client.json 파일 매개변수 설명](#clientJsonState)에 따라 구성하십시오.
5. (옵션)원본 호스트에서 마이그레이션하지 않을 파일 또는 디렉터리를 제외합니다.
마이그레이션할 필요가 없는 파일이나 디렉터리가 Linux 원본 호스트에 있는 경우 [rsync_excludes_linux.txt 파일](#_linuxTxtState)에 파일이나 디렉터리를 추가할 수 있습니다.
6. 툴을 실행합니다.
예를 들어, 64비트 Linux 소스 서버에서는 root 권한으로 다음 명령어를 실행하여 툴을 실행합니다.
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
client.json의 'Client.ToolMode'를 'true'로 수정하지 않은 경우 툴을 실행할 때 다음과 같이 '--no-console' 매개변수를 추가해야 합니다.
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
툴이 실행된 후 마이그레이션 프로세스가 완료될 때까지 기다립니다. 일반적으로 성공적인 마이그레이션의 콘솔 출력 정보는 다음 이미지와 같습니다. ![](https://main.qcloudimg.com/raw/d32b4be8287d4b06697f0cb03cc6cff8.png)




:::
:::  사설 네트워크 마이그레이션 시나리오 3
1. 소스 CVM과 타깃 CVM의 연결 터널을 생성합니다.
[Peering Connection](https://intl.cloud.tencent.com/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003) 등의 방법으로 원본 호스트와 타깃 CVM의 연결 터널을 생성합니다.
2. 마이그레이션 툴 go2tencentcloud.zip을 원본 호스트에 다운로드하거나 업로드하고 다음 명령을 실행하여 해당 디렉터리로 들어갑니다.
    1. 다음 명령어를 순서대로 실행하여 go2tencentcloud.zip의 압축을 풀고 디렉터리로 들어갑니다.
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud
```
    2. 다음 명령어를 순서대로 실행하여 go2tencentcloud-linux.zip의 압축을 풀고 디렉터리로 들어갑니다.
```shellsession
unzip go2tencentcloud-linux.zip
```
```shellsession
cd go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
`go2tencentcloud` 디렉터리에 있는 파일은 마이그레이션되지 않으므로 이 디렉터리에 마이그레이션할 파일을 두지 마십시오.
</dx-alert>
3. `user.json` 파일에 타깃 CVM을 설정합니다.
[user.json 파일 매개변수 설명](#userJsonState)에 따라 필수 항목과 필요 항목에 대한 값을 설정합니다.
4. `client.json` 파일에 마이그레이션 모드와 기타 항목을 설정합니다.
    - `client.json` 파일의 `Client.ToolMode` 값을 `true`로 설정하여 툴 모드 마이그레이션을 식별합니다.
    - `client.json` 파일의 `Client.Net.Mode` 항목을 `3`, 즉 [사설 네트워크 마이그레이션 모드: 시나리오 3](https://intl.cloud.tencent.com/document/product/213/44340#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BF.81.E7.A7.BB.E6.A8.A1.E5.BC.8F)의 마이그레이션으로 설정합니다.
    - `client.json` 파일의 `Client.Net.Proxy.Ip` 및 `Client.Net.Proxy.Port` 항목을 네트워크 프록시의 IP 주소와 포트로 설정합니다. 네트워크 프록시에 인증이 필요한 경우 `Client.Net.Proxy.User` 및 `Client.Net.Proxy.Password`에 네트워크 프록시의 사용자 이름과 비밀번호를 입력하십시오. 인증이 필요하지 않으면 공백으로 두십시오. 
		또한, 다른 항목을 설정해야 하는 경우 [client.json 파일 매개변수 설명](#clientJsonState)에 따라 구성하십시오.
5. (옵션)원본 호스트에서 마이그레이션하지 않을 파일 또는 디렉터리를 제외합니다.
마이그레이션할 필요가 없는 파일이나 디렉터리가 Linux 원본 호스트에 있는 경우 [rsync_excludes_linux.txt 파일](#_linuxTxtState)에 파일이나 디렉터리를 추가할 수 있습니다.
6. 툴을 실행합니다.
예를 들어, 64비트 Linux 소스 서버에서는 root 권한으로 다음 명령어를 실행하여 툴을 실행합니다.
```shellsession
sudo ./go2tencentcloud_x64 
```
<dx-alert infotype="notice" title="">
client.json의 'Client.ToolMode'를 'true'로 수정하지 않은 경우 툴을 실행할 때 다음과 같이 '--no-console' 매개변수를 추가해야 합니다.
```shellsession
sudo ./go2tencentcloud_x64 --no-console
```
</dx-alert>
툴이 실행된 후 마이그레이션 프로세스가 완료될 때까지 기다립니다. 일반적으로 성공적인 마이그레이션의 콘솔 출력 정보는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/2195589176d3669f08fbb5745901040b.png)

:::

</dx-tabs>


### 마이그레이션 사후 점검

- 마이그레이션 결과가 실패인 경우, 로그 파일(마이그레이션 툴 디렉터리 안의 log 파일로 기본 설정)의 오류 정보 출력, 가이드 문서 또는 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 확인하여 문제를 해결하거나 복구하시기 바랍니다.
- 마이그레이션 성공 시, 대상 CVM이 정상적으로 실행되는지, 대상 CVM의 데이터가 소스 CVM과 일치하는지, 네트워크가 정상적인지 또는 다른 시스템 서비스가 정상적인지 등을 확인하시기 바랍니다.

문의 사항이나 마이그레이션 오류 문제 등이 있다면 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 조회하거나 [문의하기](https://intl.cloud.tencent.com/document/product/213/34837)를 통해 해결하실 수 있습니다.
