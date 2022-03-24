본문은 go2tencentcloud 마이그레이션 툴을 사용하여 온라인 서버 마이그레이션을 수행하는 방법을 소개합니다.


## 마이그레이션 프로세스
툴을 사용한 마이그레이션 프로세스는 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d479b8f46562efde1b2e39d081924c4b.png)

## 준비 사항

- Tencent Cloud 계정과 대상 CVM이 있어야 합니다.
- 마이그레이션할 때, 현재 사용하고 있는 애플리케이션에 영향을 줄 수 있으므로, 원본 서버의 애플리케이션 사용을 잠시 중지할 것을 권장합니다. 
- 마이그레이션 툴 압축 패키지 [다운로드](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip).
- [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 'SecretId' 및 'SecretKey'를 생성 및 획득합니다.
- 원본 호스트와 타깃 CVM이 마이그레이션 조건을 충족하는지 확인합니다. 예를 들어, 타깃 CVM의 CBS에는 반드시 원본 호스트 데이터를 저장할 충분한 스토리지 용량이 확보되어야 합니다.
- 마이그레이션하기 전에 다음과 같은 방법으로 데이터를 백업하는 것이 좋습니다.
 - 원본 CVM: 원본 서버 스냅샷 기능 등의 방식을 선택해 데이터를 백업할 수 있습니다.
 - 대상 CVM: [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755) 등의 방식을 선택해 대상 CVM 데이터를 백업할 수 있습니다.

## 마이그레이션 과정


### 프로파일 수정[](id:modifyConfiguration)

1. 마이그레이션 툴 go2tencentcloud.zip을 원본 호스트에 다운로드하거나 업로드하고 다음 명령을 실행하여 해당 디렉터리로 들어갑니다.
    1. 다음 명령어를 순서대로 실행하여 go2tencentcloud.zip의 압축을 풀고 디렉터리로 들어갑니다.
```sh
unzip go2tencentcloud.zip
```
```sh
cd go2tencentcloud
```
    2. 다음 명령어를 순서대로 실행하여 go2tencentcloud_tool.zip의 압축을 풀고 디렉터리로 들어갑니다.
```sh
unzip go2tencentcloud_tool.zip
```
```sh
cd go2tencentcloud_tool
```
<dx-alert infotype="explain" title="">
`go2tencentcloud` 디렉터리에 있는 파일은 마이그레이션되지 않으므로 이 디렉터리에 마이그레이션할 파일을 두지 마십시오.
</dx-alert>
2. `user.json` 파일에 타깃 CVM을 설정합니다.
[user.json 파일 매개변수 설명](https://intl.cloud.tencent.com/document/product/213/44340)에 따라 필수 항목과 필수 항목의 값을 설정하십시오. 해당 매개변수 값을 실제 구성 매개변수로 바꾸십시오. 참고 예시는 다음과 같습니다.
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
2. (옵션)`client.json` 파일에 마이그레이션 모드와 기타 항목을 설정합니다.
[client.json 파일 매개변수 설명](https://intl.cloud.tencent.com/document/product/213/44340)에 따라 설정하십시오. 원본 호스트와 대상 CVM 중 하나가 공용 네트워크에 직접 액세스할 수 없는 경우 [VPC 피어링 연결](https://intl.cloud.tencent.com/zh/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/zh/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003) 또는 [Direct Connect](https://intl.cloud.tencent.com/zh/document/product/216) 등을 통해 연결 채널을 설정할 수 있습니다. 내부 네트워크 모드 마이그레이션을 수행합니다. 자세한 내용은 [내부 네트워크 마이그레이션 튜토리얼](https://intl.cloud.tencent.com/document/product/213/44341)을 참고하십시오.
3. (옵션)원본 CVM에서 마이그레이션하지 않을 파일 또는 디렉터리를 제외합니다.
Linux 원본 호스트에 마이그레이션할 필요가 없는 파일 또는 디렉터리가 있는 경우 [rsync\_excludes\_linux.txt 파일](https://intl.cloud.tencent.com/document/product/213/44340)에 추가합니다.

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
- 원본 서버는 `sudo ./go2tencentcloud_x64 --check`와 같은 툴 명령어를 사용하여 자동으로 점검할 수 있습니다.
- go2tencentcloud 마이그레이션 툴은 실행 시작 시 자동 점검하도록 기본 설정되어 있습니다. 점검 과정을 건너뛰고 강제 마이그레이션 하려면 client.json 파일의 `Client.Extra.IgnoreCheck` 필드를 `true`로 설정합니다.
</dx-alert>



### 마이그레이션 요청

다음 명령어를 실행하여 툴을 실행합니다.
본문은 64비트 Linux 원본 호스트를 예시로, go2tencentcloud_tool 파일 디렉터리에 입력하고 다음 명령어를 실행하여 root 권한으로 툴을 실행합니다.
```sh
sudo ./go2tencentcloud_x64
```

### 마이그레이션 종료 대기

Tencent Cloud에서 제공하는 go2tencentcloud 마이그레이션 툴은 체크포인트 재시작을 지원하며 마이그레이션 과정은 크게 세 단계로 나뉩니다. 사용자는 툴 실행 과정에서 마이그레이션 진행률을 직관적으로 확인할 수 있습니다.

- **1단계**: 타깃 CVM의 마이그레이션 모드 진입 단계. 마이그레이션을 준비합니다.
- **2단계**: 타깃 CVM의 마이그레이션 모드 진행 단계. 데이터를 마이그레이션 합니다.
- **3단계**: 타깃 CVM의 마이그레이션 모드 종료 단계. 마이그레이션을 완료합니다.

각 단계에서는 일련의 서브 작업을 실행해야 하며, 오랜 시간을 소모하는 일부 서브 작업은 최대 타임아웃 시간이 기본 설정되어 있습니다. 데이터 전송의 소요 시간은 소스 데이터 크기, 네트워크 대역폭 등의 영향을 받으므로, 마이그레이션 과정이 완료될 때까지 기다려 주시기 바랍니다.

<dx-alert infotype="notice" title="">
마이그레이션을 시작한 후에는 대상 CVM이 마이그레이션 모드에 들어가므로, 마이그레이션이 완료되어 마이그레이션 모드를 종료할 때까지 대상 CVM에 시스템 재설치, 셧다운, 폐기, 비밀번호 재설정 등의 작업을 실행하지 마시길 바랍니다. 
</dx-alert>

일반 공용 네트워크 마이그레이션 모드에서 마이그레이션 성공 시 콘솔에 출력되는 내용은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)

### 마이그레이션 사후 점검

- 마이그레이션 결과가 실패인 경우, 로그 파일(마이그레이션 툴 디렉터리 안의 log 파일로 기본 설정)의 오류 정보 출력, 가이드 문서 또는 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 확인하여 문제를 해결하거나 복구하시기 바랍니다.
- 마이그레이션 성공 시, 대상 CVM이 정상적으로 실행되는지, 대상 CVM의 데이터가 소스 CVM과 일치하는지, 네트워크가 정상적인지 또는 다른 시스템 서비스가 정상적인지 등을 확인하시기 바랍니다.

문의 사항이나 마이그레이션 오류 문제 등이 있다면 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 조회하거나 [문의하기](https://intl.cloud.tencent.com/document/product/213/34837)를 통해 해결하실 수 있습니다.
