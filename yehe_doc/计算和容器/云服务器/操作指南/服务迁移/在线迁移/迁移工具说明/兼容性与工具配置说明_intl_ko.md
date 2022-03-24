## 지원되는 운영 체제

현재 온라인 마이그레이션 툴에서는 다음과 같은 소스 CVM 운영 체제(32비트 혹은 64비트)를 지원합니다.

<table>
	<tr><th>Linux 운영 체제</th><th>Windows 운영 체제</th></tr>
	<tr><td>CentOS 5/6/7/8</td><td rowspan=7>Windows Server 2008 R2 이상 버전</td></tr>
	<tr><td>Ubuntu 10/12/14/16/18/20 </td></tr>
	<tr><td>Debian 7/8/9/10</td></tr>
	<tr><td>SUSE 11/12/15</td></tr>
	<tr><td>openSUSE 42</td></tr>
	<tr><td>Amazon Linux AMI</td></tr>
	<tr><td>Red Hat 7/8</td></tr>
</table>

## 지원하는 마이그레이션 모드

<dx-tabs>

::: 콘솔 마이그레이션[](id:consoleMigrate)

콘솔 마이그레이션 툴은 현재 공용 네트워크 마이그레이션 모드만 지원하며 마이그레이션 전송을 위해 공용 네트워크를 사용하여 데이터를 전송합니다.

:::
::: 툴 마이그레이션[](id:toolMigrate)

툴 마이그레이션은 **공용 네트워크 마이그레이션 모드** 및 **내부 네트워크 마이그레이션 모드**를 지원합니다.

#### 공용 네트워크 마이그레이션 모드[](id:publicMigration)
사용자의 소스 CVM과 대상 CVM 모두 공용 네트워크 액세스 기능이 있다면 공용 네트워크 마이그레이션 모드의 마이그레이션을 사용할 수 있습니다.
현재 공용 네트워크 마이그레이션 모드에서는, 소스 CVM에서 인터넷을 통해 Tencent Cloud API에 액세스하여 마이그레이션 요청을 보낸 다음, 대상 CVM에 데이터를 전송함으로써 소스 CVM을 Tencent Cloud의 대상 CVM으로 마이그레이션합니다. 공용 네트워크 마이그레이션 시나리오는 다음 이미지와 같습니다.
 ![](https://main.qcloudimg.com/raw/5203e535f5ba947bb67c1f91dee52f1f.jpg)

​    

#### 내부 네트워크 마이그레이션 모드[](id:intranetMigration)

사용자의 소스 CVM이나 대상 CVM이 특정 내부 네트워크나 VPC에 있다면 인터넷을 통해 소스 CVM을 대상 CVM에 바로 연결할 수 없으므로, 툴의 내부 네트워크 마이그레이션 모드로 마이그레이션할 수 있습니다. 내부 네트워크 마이그레이션을 사용하려면 [Peering Connection](https://intl.cloud.tencent.com/zh/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/zh/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003) 혹은 [Direct Connect](https://intl.cloud.tencent.com/zh/document/product/216) 등의 방법으로 소스 CVM과 대상 CVM 간의 통로를 생성해야 합니다.

- [](id:Scenario1)**시나리오1**: 사용자의 소스 CVM 혹은 대상 CVM이 공용 네트워크에 액세스할 수 없다면, 게이트웨이 같이 공용 네트워크 액세스 기능을 갖춘 호스트에서 인터넷을 통해 Tencent Cloud API를 호출하여 마이그레이션을 요청한 다음, 터널을 연결하여 데이터를 대상 CVM으로 마이그레이션 할 수 있습니다. 이 시나리오에서는 소스 CVM과 대상 CVM의 공용 네트워크 액세스 기능이 필요하지 않습니다.
![](https://main.qcloudimg.com/raw/19300ddf557d4534b1cd77fcbf64ef6a.jpg)
- [](id:Scenario2)**시나리오2**: 사용자의 소스 CVM이 공용 네트워크에 액세스할 수 있다면, 먼저 소스 CVM에서 인터넷을 통해 Tencent Cloud API를 호출하여 마이그레이션을 요청한 다음, 터널을 연결하여 데이터를 대상 CVM으로 마이그레이션 할 수 있습니다. 이 시나리오에서는 소스 CVM의 공용 네트워크 액세스 기능이 필요하며 대상 CVM은 해당 기능이 필요하지 않습니다.  
![](https://main.qcloudimg.com/raw/90bf988ba7cddb9b80307efb30eaad29.jpg)
- [](id:Scenario3)**시나리오3**: 사용자의 소스 CVM이 프록시를 통해 공용 네트워크에 액세스할 수 있다면, 먼저 소스 CVM에서 네트워크 프록시를 통해 Tencent Cloud API를 호출하여 마이그레이션을 요청한 다음, 터널을 연결하여 데이터를 대상 CVM으로 마이그레이션 할 수 있습니다. 이 시나리오에서는 소스 CVM과 대상 CVM의 공용 네트워크 액세스 기능이 필요하지 않습니다.
![](https://main.qcloudimg.com/raw/14f81f2c4e6cfff80d912841451c5b69.jpg)


:::

</dx-tabs>




## 압축 파일 설명
`go2tencentcloud.zip` 압축 해제 후 파일 설명은 다음과 같습니다.
<table>
	<tr><th width="30%">파일 이름</th><th>설명</th></tr>
	<tr><td>go2tencentcloud_console.zip</td><td>콘솔 마이그레이션 압축 패키지 사용.</td></tr>
	<tr><td>go2tencentcloud_tool.zip</td><td>툴 마이그레이션 압축 패키지 사용.</td></tr>
	<tr><td>readme.txt</td><td>디렉터리 소개 파일.</td></tr>
	<tr><td>release_notes.txt</td><td>마이그레이션 툴 변경 로그.</td></tr>
</table>
`go2tencentcloud_console.zip` 또는 `go2tencentcloud_tool.zip` 압축 해제 후 파일 설명은 다음과 같습니다.
<table>
	<tr><th width="30%">파일 이름</th><th>설명</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>64비트 Linux 시스템의 마이그레이션 툴에서 실행 가능한 프로그램입니다.</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>32비트 Linux 시스템의 마이그레이션 툴에서 실행 가능한 프로그램입니다.</td></tr>
	<tr><td>user.json</td><td>마이그레이션 시 소스 CVM과 대상 CVM의 구성 파일로, <a href="#userJsonState">user.json 파일 매개변수 설명</a>을 참고하여 설정을 변경하시기 바랍니다.</td></tr>
	<tr><td>client.json</td><td>마이그레이션 툴의 구성 파일은 일반적으로 콘솔을 통해 마이그레이션할 때 수정할 필요가 없습니다.</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync 구성 파일로, Linux 시스템에서 마이그레이션 하지 않을 파일 디렉터리를 제외합니다.</td></tr>
</table>

<dx-alert infotype="notice" title="">
삭제할 수 없는 구성 파일은 go2tencentcloud의 실행 가능 프로그램과 같은 단계의 디렉터리로 이동해 놓으시기 바랍니다. 
</dx-alert>



### user.json 파일 매개변수 설명[](id:userJsonState)

<dx-tabs>

::: 콘솔 마이그레이션[](id:consoleMigrate)

콘솔 마이그레이션 시 user.json 구성 파일은 다음 표에 설명되어 있습니다.

<table>
	<tr><th>매개변수 이름</th><th>유형</th><th>필수 입력 여부</th><th>설명</th></tr>
	<tr><td>SecretId</td><td>String</td><td>Yes</td><td>계정 API 호출 키 SecretId. 이에 관한 세부 정보는 <a href="https://intl.cloud.tencent.com/document/product/598/32675">액세스 키</a>를 참고 바랍니다.</td></tr>
	<tr><td>SecretKey</td><td>String</td><td>Yes</td><td>계정 API 호출 키 SecretKey. 이에 관한 세부 정보는 <a href="https://intl.cloud.tencent.com/document/product/598/32675">액세스 키</a>를 참고 바랍니다.</td></tr>
</table>

:::
::: 툴 마이그레이션[](id:toolMigrate)

툴 마이그레이션 시 user.json 구성 파일은 다음 표에 설명되어 있습니다.

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
	<td>데이터 디스크의 시리얼 넘버. 범위: [1,20]. 
	<code>1</code>은 데이터 디스크가 대상 CVM에 마운트된 첫 번째 데이터 디스크로 마이그레이션됨을 의미하며 
	<code>2</code>는 대상 CVM에 연결된 두 번째 데이터 디스크를 나타내는 식입니다.</td>
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

<a href="https://intl.cloud.tencent.com/document/product/213/35640">구성 파일 수정</a>의 예시를 참고하여 실제 비즈니스 시나리오에 따라 구성 파일을 수정할 수 있습니다.

:::

</dx-tabs>


### client.json 파일 매개변수 설명[](id:clientJsonState)

<dx-tabs>

::: 콘솔 마이그레이션[](id:consoleMigrate)

콘솔을 사용하여 마이그레이션할 때 일반적으로 client.json 구성 파일을 수정할 필요가 없습니다.

:::
::: 툴 마이그레이션[](id:toolMigrate)

툴 마이그레이션 시 client.json 구성 파일 설명:

<table>
  <tr>
	<th>매개변수 이름</th>
	<th>유형</th>
	<th>필수 입력<br>여부</th>
	<th>설명</th>
  </tr>
  <tr>
	<td>Client.Net.Mode</td>
	<td>Integer</td>
	<td>Yes</td>
	<td>마이그레이션 모드 매개변수. 기본값: 공용 네트워크 전송 사용. 값: 
	<code>0</code>, 값 범위: <code>0</code>(
	<a href="#publicMigration">공용 네트워크 마이그레이션 모드</a>), <code>1</code>(
	<a href="#Scenario1">내부 네트워크 마이그레이션 모드: 시나리오1</a>), <code>2</code>(
	<a href="#Scenario2">내부 네트워크 마이그레이션 모드: 시나리오2</a>), <code>3</code>(
	<a href="#Scenario3">내부 네트워크 마이그레이션 모드: 시나리오3</a>), 내부 네트워크 마이그레이션의 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/44341">내부 네트워크 마이그레이션 튜토리얼</a>을 참고하십시오.</td>
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
	<td>Client.Rsync.BandwidthLimit</td>
	<td>String</td>
	<td>No</td>
	<td>속도 제한 구성 항목. 단위: KBytes/s. 기본값: 공란. 즉, 전송 속도는 기본적으로 제한되지 않습니다.</td>
  </tr>
  <tr>
	<td>Client.Rsync.Checksum</td>
	<td>Bool</td>
	<td>No</td>
	<td>체크섬 전송. 
	<code>true</code>로 설정하면 전송 일관성 인증을 강화할 수 있지만 원본 호스트의 CPU 
	부하가 증가하고 전송 속도가 저하됩니다. 기본값:  
	<code>false</code>, 즉 기본적으로 확인하지 않습니다.</td>
  </tr>
</table>




<dx-alert infotype="explain" title="">
상기 매개변수 외 client.json 파일의 나머지 설정 항목은 일반적으로 입력할 필요가 없습니다.
</dx-alert>

:::

</dx-tabs>

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

<dx-tabs>

::: 콘솔 마이그레이션[](id:consoleMigrate)

콘솔 마이그레이션 시 마이그레이션 툴의 실행 매개변수는 다음 표에 설명되어 있습니다.

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
<td><code>--check</code></td>
<td>소스 CVM에 검사 진행, 마이그레이션 진행하지 않음. </td>
</tr>
<tr>
<td><code>--log-file</code></td>
<td>로그 파일 이름 설정. 기본값:<code>log</code>.</td>
</tr>
<tr>
<td><code>--log-level</code></td>
<td>로그 출력 레벨로, 범위는<code>1</code>(ERROR 레벨), <code>2</code>(INFO 레벨)과 <code>3</code>(DEBUG 레벨)이며, 기본값은<code>2</code>로 설정되어 있습니다.</td>
</tr>
<tr>
<td><code>--version</code></td>
<td>버전 번호 출력. </td>
</tr>
</tbody></table>

:::
::: 툴 마이그레이션[](id:toolMigrate)

툴 마이그레이션 시 마이그레이션 툴의 실행 매개변수는 다음 표에 설명되어 있습니다.

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
<td><code>--check</code></td>
<td>소스 CVM에 검사 진행, 마이그레이션 진행하지 않음.</td>
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
<td>대상 CVM의 마이그레이션 강제 종료 모드로, 모두 클린합니다. 만약 콘솔에 <code>Please execute '--clean' option manually.</code>와 같은 알림이 뜬다면 해당 옵션에서 툴을 실행하여 대상 CVM의 마이그레이션 모드를 종료합니다.</td>
</tr>
<tr>
<td><code>--version</code></td>
<td>버전 번호 출력.</td>
</tr>
</tbody></table>

:::

</dx-tabs>

