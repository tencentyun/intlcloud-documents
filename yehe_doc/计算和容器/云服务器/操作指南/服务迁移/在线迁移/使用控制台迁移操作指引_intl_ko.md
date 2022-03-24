
본문은 CVM 콘솔 온라인 마이그레이션 기능을 통해 온라인 서버 마이그레이션을 수행하는 방법에 대해 설명합니다.
<dx-alert infotype="explain" title="">
콘솔 온라인 마이그레이션 서비스는 현재 공개 베타 테스트 기간 중이며, 이용을 원하시면 [문의하기](https://intl.cloud.tencent.com/document/product/213/34837)를 통해 서비스 신청을 해주시기 바랍니다.
</dx-alert>

## 마이그레이션 프로세스
콘솔을 사용한 마이그레이션 프로세스는 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/389fc9a72678bbd7fac097c2a8339666.png)

## 준비 사항[](id:prerequisites)

- Tencent Cloud 계정이 있어야 합니다.
- 서브 계정으로 콘솔 마이그레이션하는 경우, 루트 계정을 사용하여 [CAM 콘솔](https://console.cloud.tencent.com/cam/policy)에 로그인하고 서브 계정에 'QcloudCSMFullAccess' 권한을 부여해야 합니다.
- [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 'SecretId' 및 'SecretKey'를 생성 및 획득합니다.
- 마이그레이션 툴 압축 패키지 [다운로드](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip).
- 마이그레이션할 때, 현재 사용하고 있는 애플리케이션에 영향을 줄 수 있으므로, 원본 서버의 애플리케이션 사용을 잠시 중지할 것을 권장합니다. 
- 마이그레이션하기 전에 다음과 같은 방법으로 데이터를 백업하는 것이 좋습니다.
 - 원본 CVM: 원본 서버 스냅샷 기능 등의 방식을 선택해 데이터를 백업할 수 있습니다.
 - 대상 CVM: [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755) 등의 방식을 선택해 대상 CVM 데이터를 백업할 수 있습니다.

## 마이그레이션 과정


### 마이그레이션 사전 점검

마이그레이션하기 전에 실제 상황에 따라 다음 표의 내용을 확인하십시오.
 - 마이그레이션 타깃이 CVM인 경우 원본 호스트와 타깃 CVM을 확인해야 합니다.
 - 마이그레이션 타깃이 CVM 이미지인 경우 원본 호스트만 확인하면 됩니다.

<table>
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
  <tr>
	<th style="width: 15%;">타깃 CVM(옵션)</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		스토리지 공간: 대상 CVM의 CBS(시스템 디스크 및 데이터 디스크 포함)에는 원본측에서 데이터를 로드할 수 있는 충분한 저장 공간이 있어야 합니다.</li>
		<li>보안 그룹: 443 포트 및 80 포트는 보안 그룹에서 제한할 수 없습니다.</li>
		<li>
		대역폭 설정: 더 빠른 마이그레이션을 위해 양쪽 끝의 대역폭을 최대한 늘리는 것이 좋습니다. 마이그레이션 과정에서 대략 데이터 양만큼의 트래픽 소모가 발생하게 되며, 필요한 경우 미리 네트워크 과금 모드를 변경하시기 바랍니다.</li>
		<li>
		대상 ECS와 원본 호스트의 운영 체제 유형이 동일한지 여부: 운영 체제가 일치하지 않으면 후속 이미지의 정보가 실제 운영 체제와 일치하지 않을 수 있으므로 대상 CVM의 운영 체제는 원본 호스트의 운영 체제 유형과 일치하는 것이 좋습니다. 예를 들어 CentOS
		7 시스템의 원본 호스트를 마이그레이션할 때 CentOS 7 시스템의 CVM을 마이그레이션 대상으로 선택합니다.</li>
	  </ol>
	</td>
  </tr>
</table>


<dx-alert infotype="explain" title="">
- 원본 서버는 `sudo ./go2tencentcloud_x64 --check`와 같은 툴 명령어를 사용하여 자동으로 점검할 수 있습니다.
- go2tencentcloud 마이그레이션 툴은 실행 시작 시 자동 점검하도록 기본 설정되어 있습니다. 점검 과정을 건너뛰고 강제 마이그레이션 하려면 client.json 파일의 `Client.Extra.IgnoreCheck` 필드를 `true`로 설정합니다.
</dx-alert>



### 마이그레이션 소스 가입[](id:registrationSource)

1. 마이그레이션 툴 go2tencentcloud.zip을 원본 호스트에 다운로드하거나 업로드하고 다음 명령을 실행하여 해당 디렉터리로 들어갑니다.
    1. 다음 명령어를 순서대로 실행하여 go2tencentcloud.zip의 압축을 풀고 디렉터리로 들어갑니다.
```sh
unzip go2tencentcloud.zip
```
```sh
cd go2tencentcloud
```
    2. 다음 명령어를 순서대로 실행하여 go2tencentcloud_console.zip의 압축을 풀고 디렉터리로 들어갑니다.
```sh
unzip go2tencentcloud_console.zip
```
```sh
cd go2tencentcloud_console
```
<dx-alert infotype="explain" title="">
`go2tencentcloud` 디렉터리에 있는 파일은 마이그레이션되지 않으므로 이 디렉터리에 마이그레이션할 파일을 두지 마십시오.
</dx-alert>
2. (옵션)원본 CVM에서 마이그레이션하지 않을 파일 또는 디렉터리를 제외합니다.
Linux 원본 호스트에 마이그레이션할 필요가 없는 파일 또는 디렉터리가 있는 경우 [rsync_excludes_linux.txt 파일](https://intl.cloud.tencent.com/document/product/213/44340)에 추가합니다.
3. 마이그레이션 소스를 가져옵니다.
  1. 64비트 Linux 원본 호스트를 예시로, go2tencentcloud 파일 디렉터리에 들어가 root 권한으로 다음 명령어를 순서대로 실행하여 툴을 실행합니다.
```sh
chmod +x go2tencentcloud_x64
```
```sh
sudo ./go2tencentcloud_x64
```
   2. 안내에 따라 [준비 사항](#prerequisites)에서 얻은 계정 API 액세스 키의 'SecretId'와 'SecretKey'를 입력하고 **Enter**를 누릅니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/38ff9f9d8c143a4cb0df39cbeaf18713.png)
<dx-alert infotype="explain" title="">
실행하기 전에 user.json 파일에서 계정 API 액세스 키를 설정할 수도 있습니다.
</dx-alert>
마이그레이션 툴 인터페이스에 다음 이미지와 같은 정보가 나타나면 마이그레이션 소스를 콘솔로 성공적으로 가져온 것이므로 콘솔로 이동하여 마이그레이션 소스를 볼 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f9cf0fd99504aba51ebf82b0cab250b8.png"/>
<br><a href="https://console.cloud.tencent.com/cvm/csm/online?rid=1">온라인 마이그레이션 콘솔</a>에 로그인하여 가져온 마이그레이션 소스가 ‘온라인’ 상태임을 확인할 수 있습니다. 아래 이미지와 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/11b1e6cada0384dae292e89378629ddc.png"/>
Import source server successfully 메시지가 표시되지 않으면 마이그레이션 원본 가져오기가 실패했음을 의미합니다. 로그(기본적으로 마이그레이션 툴 디렉터리의 logs/log 파일) 조회를 통해 문제를 해결한 후, 마이그레이션 툴을 다시 실행하여 마이그레이션 소스를 가져올 수 있습니다.
<dx-alert infotype="notice" title="">
마이그레이션 소스를 성공적으로 가져온 후 마이그레이션 작업이 완료될 때까지 인스턴스에서 마이그레이션 툴을 닫지 마십시오. 그렇지 않으면 마이그레이션 소스가 오프라인되어 마이그레이션 작업을 완료할 수 없습니다.
</dx-alert>



### 마이그레이션 작업 생성 및 실행

1. 마이그레이션 작업 생성
[온라인 마이그레이션 콘솔](https://console.cloud.tencent.com/cvm/csm/online?rid=1)에 로그인하여 타깃 마이그레이션 소스가 있는 행 우측의 **마이그레이션 작업 생성**을 클릭합니다. 마이그레이션 작업 생성 팝업 창에서 다음 정보를 참고하여 구성합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/63c9481797c861890a2ea9ca37c4f272.png)
[](id:jobSettings) 마이그레이션 작업에 대한 자세한 설정 설명은 다음과 같습니다.
<table>
<thead>
<tr>
<th width="18%">설정 옵션</th>
<th width="10%">필수 입력 여부</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr>
<td>타깃 리전</td>
<td>네</td>
  <td>원본 호스트가 마이그레이션될 Tencent Cloud 리전입니다. 리전의 경우 <a href="https://intl.cloud.tencent.com/document/product/213/6091">리전 및 가용존</a>을 참고하십시오.</td>
</tr>
<tr>
<td>작업 이름</td>
<td>네</td>
<td>마이그레이션 작업 이름입니다.</td>
</tr>
<tr>
<td>작업 설명</td>
<td>아니오</td>
<td>마이그레이션 작업 설명입니다. </td>
</tr>
<tr>
<td>타깃 유형</td>
<td>네</td>
<td>
  마이그레이션 소스의 타깃 유형을 Tencent Cloud로 설정합니다.
    <ul>
    <li><b>CVM 이미지</b>: 마이그레이션 작업 완료 후 마이그레이션 소스에 대한 타깃 Tencent Cloud 이미지가 생성됩니다.
      <br>이미지 이름: <b>필수 입력</b>, 마이그레이션 소스에 대해 생성된 대상 Tencent Cloud 이미지의 이름입니다. 타깃 리전에서 이미지 이름이 중복되면 마이그레이션 작업이 이미지 이름에 작업 ID를 자동으로 추가합니다.
    </li>
    <li><b>CVM 인스턴스</b>: 마이그레이션 타깃으로 타깃 리전의 CVM 인스턴스를 선택합니다.
      <br>타깃 인스턴스: <b>필수 입력</b>, 타깃 CVM의 운영 체제는 원본 호스트의 운영 체제와 동일한 것이 좋습니다. 예를 들어 CentOS 7 시스템을 원본 호스트로 마이그레이션할 때 CentOS 7 시스템 CVM을 마이그레이션 타깃으로 선택합니다.
    </li>
  </ul>
</td>
</tr>
<tr>
<td>실행 예약 시간</td>
<td>아니오</td> 
  <td>마이그레이션 작업이 생성된 후 설정한 시간에 자동으로 마이그레이션 작업이 시작됩니다. 실행 예약 시간은 현재 시간으로부터 최소 <b>10</b>분 후로 설정할 수 있습니다.</td>
</tr>
<tr>
<td>전송 한도(KB/초)</td>
<td>아니오</td>  
<td>마이그레이션 프로세스 중 데이터 전송을 위한 대역폭의 상한값(Mbps)입니다. </td>
</tr>
<tr>
<td>Checksum 인증</td>
<td>아니오</td>  
<td>활성화되면 데이터 일관성 검사를 향상시킬 수 있지만 전송 속도가 느려질 수 있습니다.</td>
</tr>
</tbody></table>
2. 마이그레이션 작업을 실행합니다.
<dx-alert infotype="explain" title="">
실행 예정 작업은 이 단계를 건너뛸 수 있으며, 예약된 실행 시간에 도달하면 자동으로 마이그레이션 작업이 시작됩니다.
</dx-alert>
마이그레이션 작업 생성 후 <b>마이그레이션 작업</b> 탭을 클릭하여 마이그레이션 작업을 볼 수 있습니다. 아래 이미지와 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7d2447ea7e6f348d779e41ad2c08fd93.png"/>
마이그레이션 작업은 작업 행 오른쪽에 있는 <b>시작/재시도</b>를 클릭하면 시작됩니다. 이 때 작업 상태가 ‘마이그레이션 중’으로 변경됩니다. 아래 이미지와 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/bcbad8eb9a093814f18ff82aab7bc308.png"/>
<dx-alert infotype="notice" title="">
- 콘솔을 통해 마이그레이션할 때, 시스템 디스크와 원본 호스트의 마운트된 모든 데이터 디스크를 자동으로 마이그레이션하고 소스 디스크와 동일한 파티션 구조로 대상 디스크를 자동으로 생성하는 데 도움이 됩니다.
- 콘솔 마이그레이션은 현재 공용 네트워크 마이그레이션만 지원하며, 내부 네트워크 마이그레이션은 마이그레이션 툴을 사용하여 구현할 수 있습니다. 자세한 내용은 [내부 네트워크 마이그레이션 튜토리얼](https://intl.cloud.tencent.com/document/product/213/44341)을 참고하십시오.
- 마이그레이션 타깃이 CVM인 경우 마이그레이션을 시작한 후에는 타깃 CVM이 마이그레이션 모드에 들어가므로, 마이그레이션이 완료되어 마이그레이션 모드를 종료할 때까지 타깃 CVM에 Reinstall the system, 종료, 폐기, 비밀번호 재설정 등의 작업을 실행하지 마시길 바랍니다.
- 마이그레이션 타깃이 CVM 이미지인 경우 마이그레이션 시작 후 계정 아래에 'do_not_delete_csm_instance'라는 전송 인스턴스가 생성됩니다. 전송 인스턴스에 대해 시스템 재설치,​ ​종료, 폐기, 비밀번호 재설정 등의 작업을 하지 마십시오. 마이그레이션이 완료되면 시스템은 생성된 전송 인스턴스를 자동 폐기합니다.
</dx-alert>


### 마이그레이션 작업 종료 대기

마이그레이션 작업의 상태가 ‘성공’이면 마이그레이션이 성공적으로 완료되었음을 나타냅니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)

<dx-alert infotype="explain" title="">
- 데이터 전송 시간은 원본 데이터의 크기, 네트워크 대역폭 및 기타 요인의 영향을 받으므로 마이그레이션 프로세스가 완료될 때까지 기다려 주십시오.
- 마이그레이션 작업이 시작된 후 마이그레이션 작업이 있는 행에서 **일시 중지**를 클릭하여 마이그레이션 작업을 중지할 수 있습니다.
- 마이그레이션 툴은 체크포인트 재시작을 지원하며, 작업을 일시 중단한 후 **시작/재시도**를 다시 클릭하면 마지막 일시 중지 지점부터 마이그레이션을 계속할 수 있습니다.
- 마이그레이션 작업은 데이터 전송 단계에서만 일시 중지를 지원합니다. 콘솔의 마이그레이션 작업에서 **일시 중지**를 클릭하면 마이그레이션 툴이 데이터 전송 단계에서 데이터 전송을 일시 중지합니다.
- 마이그레이션 프로세스가 너무 오래 걸리고 마이그레이션을 중지해야 하는 경우 마이그레이션 작업을 일시 중지하고 **삭제**를 클릭하여 마이그레이션 작업을 취소할 수 있습니다.
</dx-alert>



### 마이그레이션 사후 확인[](id:checkAfter)

- **마이그레이션 실패**:
로그 파일(마이그레이션 툴 디렉터리 안의 log 파일로 기본 설정)의 오류 정보, 가이드 문서 또는 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 확인하여 문제를 해결하거나 복구하시기 바랍니다. 복구 후 마이그레이션 작업 열에서 **시작/재시도**를 클릭하여 마이그레이션 작업을 다시 시작합니다.
- **마이그레이션 성공**:
 - 마이그레이션 타깃이 CVM인 경우, 타깃 CVM 정상 실행 여부, 타깃 CVM의 데이터와 원본 호스트의 일치 여부, 네트워크 및 다른 시스템 서비스의 정상 여부 등을 확인하시기 바랍니다.
 - 마이그레이션 타깃이 CVM 이미지인 경우 마이그레이션 작업이 있는 행의 ‘CVM 이미지 ID’를 클릭하여 [CVM 이미지 페이지](https://console.cloud.tencent.com/cvm/image/index)로 이동하여 이미지 정보를 볼 수 있으며, 이미지를 활용하여 CVM을 생성할 수 있습니다.

문의 사항이나 마이그레이션 오류 문제 등이 있다면 [서비스 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 조회하거나 [문의하기](https://intl.cloud.tencent.com/document/product/213/34837)를 통해 해결하실 수 있습니다.



