본문은 클라이언트에서 마이그레이션 소스를 가져와 소스 서버를 Tencent Cloud CVM으로 마이그레이션하는 방법을 설명합니다.

## 마이그레이션 워크플로
클라이언트에서 마이그레이션 소스를 가져오는 절차는 다음과 같습니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/w6gR606_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230428170713.png)

[](id:prerequisites)
## 마이그레이션 단계
### 1단계: 마이그레이션 준비
- [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 'SecretId'와 'SecretKey'를 생성 및 획득합니다.
- 기존 애플리케이션이 마이그레이션의 영향을 받지 않도록 서버에서 애플리케이션을 중지하고 데이터를 백업하십시오.
 - 소스 서버: 스냅샷 기능이나 기타 방법을 이용하여 소스 서버에 데이터를 백업할 수 있습니다. 소스 서버는 마이그레이션될 서버입니다.
 - 대상 CVM: 인스턴스의 스냅샷을 생성하여([Creating Snapshot](https://www.tencentcloud.com/document/product/362/5755) 참고) 데이터를 백업합니다.
-  서브 계정을 사용하는 경우 루트 계정으로 [CAM 콘솔](https://console.cloud.tencent.com/cam/policy)에 로그인하여 `QcloudCSMFullAccess` 및 `QcloudCVMFullAccess` 권한 부여하십시오.
- 마이그레이션하기 전에 실제 조건에 따라 확인을 진행해야 합니다. 확인 내용은 다음과 같습니다.
 - CVM 인스턴스로 마이그레이션: 소스 서버와 대상 CVM을 확인합니다.
 - CVM 이미지로 마이그레이션: 소스 서버를 확인합니다.
  <table>
  <tr>
	<th>Linux 소스 서버</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtio를 확인하고 설치합니다. 자세한 내용: 
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux 시스템 virtio 드라이버 점검</a>. </li>
		<li>실행 
		<code>which rsync</code>는 rsync가 설치되었는지 여부를 확인합니다. 설치되어 있지 않은 경우 <a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">Rsync는 어떻게 설치하나요?</a>를 참고하여 설치하십시오. </li>
		<li>SELinux의 활성화 여부를 확인합니다. SELinux가 활성화되어 있으면 <a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">SELinux를 비활성화하는 방법은 무엇입니까?</a>를 참고하여 비활성화하십시오. </li>
		<li>Tencent Cloud API로 마이그레이션 요청을 전송한 후 API는 현재의 UNIX 타임을 사용하여 생성된
		Token을 확인합니다. 서버의 시스템 시간이 올바른지 확인하십시오. </li>
	  </ol>
	</td>
 </tr>
  <tr>
	<th>Windows 소스 서버</th>
	<td>
	  <ol style="margin: 0;">
		<li>Virtio를 확인하고 설치합니다. 자세한 내용: 
		<a href="https://intl.cloud.tencent.com/document/product/213/17815">Virtio 드라이버 확인 또는 설치
</a>. </li>
		<li>(선택 사항) Cloudbase-Init를 확인하고 설치합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/32364">Windows 운영 체제에서 Cloudbase-init 설치</a>를 참고하십시오. 마이그레이션 전에 소스 서버에 설치하는 것이 좋습니다. <br>이 경우 마이그레이션 후 네트워크 구성 및 OS 라이선스 활성화가 자동으로 수행됩니다. <br>마이그레이션 전에 설치하지 않으면 <a href="https://intl.cloud.tencent.com/document/product/213/32496">VNC를 사용하여 Windows 인스턴스 로그인</a>하고 마이그레이션 후 대상 서버에서 수동으로 네트워크 구성을 수정해야 합니다. </li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th style="width: 15%;">대상 CVM</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		스토리지 공간: 대상 CVM의 클라우드 디스크(시스템 디스크 및 데이터 디스크 포함)는 소스 서버의 데이터를 저장하기에 충분한 저장 공간을 제공해야 합니다. </li>
		<li>보안 그룹: 포트 80, 포트 443 및 포트 3389가 열립니다. </li>
		<li>
		대역폭 설정: 양쪽 끝의 대역폭 캡을 가능한 가장 높은 값으로 설정합니다. 마이그레이션 과정 중 데이터 양과 비슷한 양의 트래픽이 소비됩니다. 필요 시 사전에 네트워크 과금 방식을 조정하십시오. </li>
<li>
		네트워크 설정: 소스 또는 대상 서버가 IPv6만 지원하고 IPv4는 지원하지 않는 경우 <a href="https://intl.cloud.tencent.com/document/product/213/44340">client.json 파일 매개변수</a>를 참고하십시오. </li>
	  </ol>
	</td>
  </tr>
</table>
<dx-alert infotype="explain" title="">
- `sudo ./go2tencentcloud_x64 --check`를 실행하여 소스 서버를 확인합니다.
- 기본적으로 go2tencentcloud는 실행 시 자동으로 검사를 수행합니다. 검사를 건너뛰려면 client.json 파일을 열고 `Client.Extra.IgnoreCheck` 을`true`로 설정합니다. 
</dx-alert>

[](id:registrationSource)
### 2단계: 마이그레이션 소스 가져오기
#### 마이그레이션 툴을 통해 마이그레이션 소스 가져오기
<dx-tabs>
::: Linux 소스 서버                                       
1. 소스 서버에서 다음 명령을 실행하여 마이그레이션 툴 인  go2tencentcloud.zip을 [다운로드](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)하고 해당 디렉터리로 이동합니다.
```shellsession
wget https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip
``` 
```shellsession
unzip go2tencentcloud.zip
```
```shellsession
cd go2tencentcloud/go2tencentcloud-linux
```
<dx-alert infotype="explain" title="">
`go2tencentcloud` 디렉터리에 있는 파일은 마이그레이션되지 않으므로 이 디렉터리에 마이그레이션할 파일을 두지 마십시오.
</dx-alert>
2. (선택 사항)마이그레이션할 필요가 없는 소스 서버의 파일 및 디렉터리를 제외합니다.
Linux 소스 서버에 마이그레이션할 필요가 없는 파일 또는 디렉터리가 있는 경우 [rsync_excludes_linux.txt 파일](https://intl.cloud.tencent.com/document/product/213/44340)에 추가합니다.
3. 마이그레이션 소스를 가져옵니다.
   1. 64비트 Linux 소스 서버에서 root 사용자로 다음 명령을 순서대로 실행하여 툴을 실행합니다.
```shellsession
chmod +x go2tencentcloud_x64
```
```shellsession
sudo ./go2tencentcloud_x64
```
   2. [준비 사항](#prerequisites)에서 얻은 계정 API 액세스 키의 'SecretId'와 'SecretKey'를 입력하고 **Enter**를 누릅니다. 다음 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/38ff9f9d8c143a4cb0df39cbeaf18713.png)
다음 메시지가 표시되면 소스 서버를 성공적으로 가져온 것입니다. 이제 CVM 콘솔에서 서버를 볼 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f9cf0fd99504aba51ebf82b0cab250b8.png"/>
:::

::: Windows 소스 서버
1. go2tencentcloud.zip을 소스 서버에 [다운로드](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) 또는 업로드하고, 파일을 go2tencentcloud 폴더에 압축 해제합니다. go2tencentcloud-windows를 열면 아래와 같은 디렉터리가 표시됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3f2c9881d9c5323a14d096d0811814cd.png)    
2. 다음과 같은 방법으로 go2tencentcloud_x64.exe 응용 프로그램을 실행합니다.
	- 방법1: go2tencentcloud_x64.exe 응용 프로그램을 관리자 권한으로 우클릭하여 실행하고, 팝업창에 SecretId와 SecretKey를 입력합니다.
	- 방법2: 관리자 권한으로 cmd 또는 powershel 명령 라인 열기: cd /d "go2tencentcloud_x64.exe가 있는 디렉터리의 절대 경로" 및 go2tencentcloud_x64.exe 응용 프로그램을 실행합니다.
3. 팝업 창에 Tencent Cloud API Keys(SecretId 및 SecretKey)를 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b7af60919e710d7d148e791124fce1a0.png) ![](https://qcloudimg.tencent-cloud.cn/raw/8494a126134389796be195ccd268e03a.png)       

3. 다음과 같은 메시지가 나타나면 소스 서버 정보를 가져온 것입니다. 이제 CVM 콘솔에서 소스 서버를 확인할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5ecd29f96415d0cb090fe165909272be.png)
:::
</dx-tabs>
<dx-alert infotype="explain" title="">
Import source server successfully 메시지가 표시되지 않으면 문제 해결을 위해 마이그레이션 툴 디렉터리 아래의 logs/log 파일에서 로그를 확인하십시오.
</dx-alert>

#### 콘솔에서 소스 서버 확인
<a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">CVM 콘솔</a>에 로그인하고 가져온 서버를 확인합니다. 상태는 아래와 같이 **온라인**이어야 합니다. 다음 이미지 참고:
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/rS3s122_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230517153526.png"/>

>!소스 서버 가져오기는 마이그레이션의 첫 번째 단계입니다. 전체 마이그레이션 진행이 끝날 때까지 마이그레이션 툴을 활성화 상태로 유지하십시오. 그렇지 않으면, 마이그레이션 소스가 오프라인 상태가되면 마이그레이션 작업을 완료할 수 없습니다.


### 3단계: 마이그레이션 작업 생성

#### 1. 마이그레이션 작업 생성
[CVM 콘솔](https://console.cloud.tencent.com/cvm/csm/online?rid=1)에 로그인하여 온라인 마이그레이션 페이지로 이동하여 소스 서버를 찾은 후 **마이그레이션 작업 생성**을 클릭합니다. **마이그레이션 작업 생성** 팝업 창에서 작업을 구성합니다. 다음 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/eafa2cf56f1501c48082b3a3bdbb2c2f.png)
[](id:jobSettings) 마이그레이션 작업에 대한 자세한 설정 설명은 다음과 같습니다.

- 기본 옵션:
	<table>
	<thead>
	<tr>
	<th width="18%">구성 항목</th>
	<th width="10%">필수 입력 여부</th>
	<th>설명</th>
	</tr>
	</thead>
	<tbody>
	<tr>
	<td>대상 리전</td>
	<td>Yes</td>
		<td>소스 서버를 마이그레이션할 Tencent Cloud 리전입니다. 리전에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/6091">리전 및 가용존</a>을 참고하십시오. </td>
	</tr>
	<tr>
	<td>작업 이름</td>
	<td>Yes</td>
	<td>마이그레이션 작업 이름입니다. </td>
	</tr>
	<tr>
	<td>작업 설명</td>
	<td>No</td>
	<td>마이그레이션 작업 설명입니다. </td>
	</tr>
	<tr>
	<td>대상 유형</td>
	<td>Yes</td>
	<td>
		Tencent Cloud로 마이그레이션할 소스 서버의 대상 유형을 설정합니다.
			<ul>
			<li><b>CVM 이미지</b>: 소스 서버용 CVM 이미지를 생성합니다.
				<br>이미지 이름: 마이그레이션 소스에 대해 생성될 대상 CVM 이미지의 이름입니다. 동일한 이름이 이미 있는 경우 마이그레이션 작업 ID가 이름에 추가됩니다.
			</li>
			<li><b>CVM 인스턴스</b>: 마이그레이션 대상으로 대상 리전의 CVM 인스턴스를 선택합니다.
				<br>대상 인스턴스: 소스 서버와 대상 CVM에 동일한 운영 체제를 사용하는 것이 좋습니다. 예시: CentOS 7 소스 서버를 마이그레이션하려면 CentOS 7 CVM을 대상으로 선택합니다.
			</li>
		</ul>
	</td>
	</tr>
	<tr>
	<tr>
	<td>네트워크 모드</td>
	<td>Yes</td>
	<td>
		데이터 전송에 사용되는 네트워크입니다.
			<ul>
			<li><b>공중망 네트워크</b>: 공중망을 통해 전송합니다.
			</li>
			<li><b>사설망 네트워크</b>: 사설망을 통해 전송합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/44341">사설망을 통한 마이그레이션</a>을 참고하십시오.
				<br>VPC: CVM 이미지로 마이그레이션할 때 VPC에 릴레이 인스턴스를 생성합니다.
				<br>서브넷: CVM 이미지로 마이그레이션할 때 서브넷에 릴레이 인스턴스를 생성합니다.
			</li>
		</ul>
	</td>
	</tr>	
	<tr>
	<td rowspan='2'>마이그레이션 방법</td>
	<td rowspan='2'>Yes</td>
	<td>
		Linux에서 마이그레이션을 위한 마이그레이션 방법을 설정합니다.
			<ul>
			<li><b>Linux 파일 레벨 마이그레이션</b>: 호환성이 더 높고 전송 속도가 비교적 느린 파일 레벨 마이그레이션입니다.
			</li>
			<li><b>Linux 블록 레벨 마이그레이션</b>: 전송 속도가 더 빠르고 호환성이 상대적으로 낮은 ‘블록’ 레벨 마이그레이션입니다.
			</li>
		</ul>
	</td>
	</tr>	
	<tr>
	<td>
	<b>Windows 블록 레벨 마이그레이션</b>: 전송 속도가 더 빠르고 호환성이 상대적으로 낮은 ‘블록’ 레벨 마이그레이션입니다. 블록 레벨 마이그레이션은 기본적으로 Windows에서의 마이그레이션에 사용됩니다.
		</ul>
	</td>
	</tr>	
	<tr>
	<td>증분 동기화 구성</td>
	<td>No</td>
	<td>증분 동기화 기간을 사용자 지정하여 데이터를 지속적으로 동기화하고 마이그레이션 시간을 유연하게 제어할 수 있습니다.
		<ul>
			<li><b>활성화 안 함</b>: 마이그레이션 툴이 증분을 자동 식별하고 마이그레이션합니다. 일반적으로 한 번만 실행됩니다. </li>
			<li><b>활성화함</b>: 증분 동기화 실행 시간을 선택할 수 있습니다. 마이그레이션 툴은 지속적으로 데이터를 Tencent Cloud에 동기화합니다. 작업 목록에서 증분 동기화를 수동으로 중지할 수도 있습니다. </li>
		</ul>
	</td>
	</tr>
	<td>실행 시간 예약</td>
	<td>No</td> 
	<td>마이그레이션 작업이 생성된 후 자동으로 실행되는 시간을 설정합니다. 실행 시간은 현재 시간으로부터 최소 <b>10</b>분 후로 설정할 수 있습니다. </td>
	</tr>
	</tbody></table>


- 고급 옵션(선택 사항):
<table>
<thead>
<tr>
<th width="18%">구성 항목</th>
<th width="10%">필수 입력 여부</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr>
<td>전송 속도 제한(KB/s)</td>
<td>No</td>  
<td>마이그레이션 중 데이터 전송 속도 제한은 [0, 25600] KB/s입니다. 기본적으로 0(무제한)으로 설정되어 있습니다. Windows 마이그레이션은 이 선택 항목이 지원되지 않습니다. </td>
</tr>
<tr>
<td>Checksum 확인</td>
<td>No</td>  
<td> 활성화하면 데이터 일관성 검사가 강화되지만 전송 속도가 느려질 수 있습니다. Windows 마이그레이션은 이 선택 항목이 지원되지 않습니다. </td>
</tr>
</tbody></table>

#### 2. 마이그레이션 작업을 실행합니다.
<dx-alert infotype="explain" title="">
작업이 예약된 경우 이 단계를 건너뛸 수 있으며 예약된 실행 시간에 자동으로 실행됩니다.
</dx-alert>
마이그레이션 작업 생성 후 <b>마이그레이션 작업</b> 탭을 클릭하여 마이그레이션 작업을 볼 수 있습니다. 다음 이미지와 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png"/>
작업 행 오른쪽에 있는 <b>시작/재시도</b>를 클릭하고 팝업 창에서 <b>확인</b>을 클릭하여 마이그레이션 작업을 시작합니다. 작업 상태가 '마이그레이션 중'이 됩니다. 다음 이미지와 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png"/>
<dx-alert infotype="notice" title="">

- 마이그레이션 대상이 CVM 인스턴스인 경우 대상 CVM은 마이그레이션이 시작된 후 마이그레이션 모드로 진입합니다. 마이그레이션이 종료되고 대상 CVM이 마이그레이션 모드를 종료할 때까지 대상 CVM의 시스템 재설치, 종료, 폐기 또는 비밀번호 재설정을 진행하지 마십시오.
- 마이그레이션 대상이 CVM 이미지인 경우 마이그레이션 시작 후 계정에 릴레이 인스턴스 `do_not_delete_csm_instance`가 생성됩니다. 릴레이 인스턴스를 다시 설치, 종료 또는 폐기하거나 암호를 재설정하지 마십시오. 마이그레이션이 종료되면 시스템에서 자동으로 종료됩니다.
</dx-alert>


### 4단계: 마이그레이션 후 확인[](id:checkAfter)
#### 1. 콘솔에서 마이그레이션 진행률 보기
   마이그레이션 작업의 상태가 **성공**이면 마이그레이션이 성공적으로 완료되었음을 나타냅니다. 다음 이미지 참고:
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)
<dx-alert infotype="explain" title="">
- 데이터 전송 소요 시간은 소스 서버의 데이터 크기, 네트워크 대역폭 등에 따라 다릅니다. 마이그레이션 프로세스가 완료될 때까지 기다리십시오.
- 마이그레이션 작업이 시작된 후 마이그레이션 작업이 있는 행에서 **일시 중지**를 클릭하여 마이그레이션 작업을 중지할 수 있습니다.
- 마이그레이션 툴은 체크포인트 재시작을 지원하며, 작업을 일시 중단한 후 **시작/재시도**를 다시 클릭하면 마지막 일시 중지 지점부터 마이그레이션을 계속할 수 있습니다.
- 데이터 전송 중에 마이그레이션 작업을 일시 중지할 수 있습니다. 콘솔에서 **일시 중지**를 클릭하면 마이그레이션 툴이 진행 중인 데이터 전송을 일시 중지합니다.
- 마이그레이션이 시간이 오래 걸려 중지하려는 경우 먼저 마이그레이션 작업을 일시 중지하고 **삭제**를 클릭하여 마이그레이션 작업을 취소할 수 있습니다.
</dx-alert>

#### 2. 마이그레이션 후 확인
 - **마이그레이션 실패**:
log 파일(기본적으로 마이그레이션 툴 디렉터리의 log 파일), 작업 가이드 또는 [서버 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)에서 오류 정보를 확인하여 문제를 해결할 수 있습니다. 문제 해결 후 작업 열에서 **시작/재시도**를 클릭하여 마이그레이션 작업을 다시 시작할 수 있습니다.
 - **마이그레이션 성공**:
CVM으로 마이그레이션: 대상 CVM이 정상적으로 시작되는지, CVM의 데이터가 소스 서버의 데이터와 일치하는지, 네트워크 및 기타 시스템 서비스가 정상인지 확인합니다.
CVM 이미지로 마이그레이션: 마이그레이션 작업 행의 **CVM 이미지 ID**를 클릭하여 [CVM 이미지 페이지](https://console.cloud.tencent.com/cvm/image/index)로 이동하여 이미지 정보를 볼 수 있으며, 이 이미지를 사용하여 CVM 인스턴스를 생성할 수 있습니다.
</dx-alert>
문의 사항이 있으시거나 마이그레이션에 문제가 있는 경우 <a href="https://intl.cloud.tencent.com/document/product/213/32395">서버 마이그레이션 관련 FAQ</a> 또는 <a href="https://intl.cloud.tencent.com/document/product/213/34837">Contact Us</a>를 통해 해결하실 수 있습니다.
