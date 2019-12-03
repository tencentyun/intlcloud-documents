엘라스틱 Cloud Block Storage（CBS）(클라우드 서버의 데이터 디스크로 사용)를 동일한 가용존에 있는 임의의 클라우드 서버에 마운트하여 사용할 수 있습니다. 클라우드 서버당 최대 20개의 데이터 디스크를 지원하며, 다음과 같은 방법으로 CBS를 마운트할 수 있습니다.
- 새 클라우드 서버를 시작할 때, 해당 사용자 정의 이미지 및 데이터 디스크 스냅샷을 지정하십시오.
자동 마운트 후에는 파티션, 포맷과 같은 디스크 초기화 작업을 수행하지 않고도 바로 데이터 디스크를 읽고 쓸 수 있습니다.
- 별로도 구매한 CBS는 콘솔 또는 API 인터페이스를 통해 수동으로 엘라스틱 CBS를 동일한 가용존에 있는 기존 클라우드 인스턴스에 마운트하십시오.
 - 직접 생성한 CBS
 수동 마운트 후에는 디스크 파티션, 포맷 등 초기화 작업을 진행해야 합니다. 자세한 내용은 [CBS 초기화(2TB 미만)](https://intl.cloud.tencent.com/document/product/362/31597) 또는 [CBS 초기화(2TB 이상)](https://intl.cloud.tencent.com/document/product/362/31598)을 참조하십시오.
 - 스냅샷에서 생성한 CBS
  CBS 용량이 스냅샷 용량과 같을 경우, 수동으로 마운트한 후에는 파티션, 포맷 등의 디스크 초기화 작업 없이 직접 읽고 쓸 수 있습니다.
	CBS 용량이 스냅샷 용량보다 큰 경우, 파일 시스템을 확장하거나 파티션을 변환해야 합니다.

 >일부 Linux 클라우드 서버에서는 엘라스틱 CBS를 인식하지 못할 수 있습니다. 그럴 경우 먼저 클라우드 서버에서 디스크 핫 플러그 기능을 시작할 수 있습니다. 자세한 내용은 [디스크 핫 플러그 기능 켜기](#modprobeacpiphp)를 참조하십시오.

## 자동 마운트
### 데이터 디스크 마운트(Windows)
Windows 클라우드 서버 인스턴스를 시작할 때, 해당 데이터 디스크 스냅샷으로 생성된 CBS를 자동으로 마운트해야 하는 경우, 지정된 사용자 정의 이미지 및 데이터 디스크 스냅샷은 다음 요구 사항을 충족해야 합니다.
- 데이터 디스크는 스냅샷을 생성하기 전에 **반드시** `ntfs` 또는 `fat32` 포맷으로 포맷되어 있어야 합니다.
- 사용자 정의 이미지의 SAN 정책은 'onlineAll'입니다.
  >?텐센트 클라우드에서 현재 제공되는 Windows 공유 미러 이미지는 기본으로 설정되어 있지만, 사용자 정의 이미지를 만들기 전에 기본 구성을 확인할 것을 권장합니다. 확인 방법은 다음과 같습니다.
 ![](https://main.qcloudimg.com/raw/edac7337395de380c0ec801646e0a627.png)

 
 
### 데이터 디스크 마운트(Linux)
Linux 클라우드 서버 인스턴스를 시작할 때, 해당 데이터 디스크 스냅샷으로 생성된 CBS를 자동으로 마운트해야 하는 경우, 지정된 사용자 정의 이미지 및 데이터 디스크 스냅샷은 다음 요구 사항을 충족해야 합니다.
- 데이터 디스크는 스냅샷을 생성하기 전에 **반드시** 포맷되어 있어야 합니다. 클라우드 서버 에서 mount가 완료되어 있어야 합니다.
- 시스템 디스크에서 사용자 정의 이미지를 생성하기 전에 `/etc/rc.local` 파일에 다음 커맨드를 추가하여 데이터 디스크 마운트 포인트를 파일에 생성해야 합니다.
 ```
 mkdir -p <mount-point>
 mount <device-id> <mount-point>
 ```
>
> - `<mount-point>`는 `/mydata`와 같이 파일 시스템의 마운트 포인트로 설정해야 합니다.
> - `<device-id>` 를 실제 파일 파티션 위치로 설정해야 합니다. 예를 들어, 파일 시스템에 파티션이 없으면 `/dev/vdb`를 작성하고, 파일 시스템에 파티션이 있으면 `/dev/vdb1`을 입력하십시오.

## 수동 마운트

### 콘솔을 사용해 CBS 마운트
1. [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs)에 로그인하십시오.
2. CBS 리스트에서, 다음과 같은 방법으로 CBS를 마운트할 수 있습니다:
 a. 상태가 **마운트 대기**인 CBS 라인에서 [더 알아보기]> [마운트]를 클릭합니다.
 b. 상태가 **마운트 대기**로 체크되어 있으면 CBS 리스트 위의 [마운트]를 클릭하여 일괄 마운트를 진행합니다.
3. 팝업 창에서 타깃 클라우드 서버를 선택하고 [확인]을 클릭하십시오.
4. 클라우드 디스크 리스트를 새로고침하십시오.
 CBS의 상태가 [마운트 완료]로 변경되면 마운트가 완료된 것입니다.
5. CBS의 상황에 따라 해당하는 후속 조작을 실행하도록 선택해야만 CBS를 사용 가능합니다.
 <table>
 <tr>
 <th>생성 모드</th>
 <th>CBS 용량</th>
 <th>후속 조작</th>
 </tr>
 <tr>
 <td  rowspan="2">직접 생성</td>
 <td>CBS 용량 < 2TB</td>
 <td><a href="https://intl.cloud.tencent.com/document/product/362/31597">CBS 초기화(2TB 미만)</a></td>
 </tr>
 <tr>
  <td>CBS 용량 ≥ 2TB</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/362/31598">CBS 초기화(2TB 이상)</a></td>
 </tr>
  <tr>
	<td  rowspan="3">스냅샷에서 생성</td>
	<td>CBS 용량 = 스냅샷 용량</td>
	<td>후속 작업이 필요하지 않으며 마운트 후 바로 사용할 수 있습니다.</td>
 </tr>
 </tr>
 <tr>
 <td nowrap="nowrap">스냅샷 용량 <CBS 용량 ≤ 2TB <br/> 또는 <br/> 2TB <스냅샷 용량 <CBS 용량</td>
<td><ul><li>Windows 클라우드 서버에 마운트:<a href="https://intl.cloud.tencent.com/document/product/362/6737">파티션 및 파일 시스템 (Windows) 확장</a></li><li>Linux 클라우드 서버에 마운트: <a href="https://intl.cloud.tencent.com/document/product/362/6738">파티션 및 파일 시스템 (Linux) 확장</a></li></ul></td>
 </tr> 
 <tr>
 <td>스냅샷 용량 ≤ 2TB <CBS 용량</td>
<td nowrap="nowrap">￼<ul><li>스냅샷에서 MBR 파티션 형식을 사용하는 경우: </li><a href="https://intl.cloud.tencent.com/document/product/362/31598">CBS 초기화(2TB 이상)를 참고하고</a> GPT를 사용하여 새로 파티션을 생성합니다.￼<b>이 작업은 기존 데이터 전부 삭제합니다￼</b><li>스냅샷에서 GPT 파티션 형식을 사용하는 경우: <ul><li> Windows 클라우드 서버에 마운트: <a href="https://intl.cloud.tencent.com/document/product/362/6737">파티션 및 파일 시스템(Windows) 확장</a></li><li> Linux 클라우드 서버에 마운트: <a href="https://intl.cloud.tencent.com/document/product/362/6738">파티션 및 파일 시스템(Linux) 확장</a></li></ul>￼</td>
 </tr> 
 </table>

### API를 사용해 CBS 마운트
AttachDisks 인터페이스를 사용하여 스냅샷을 생성할 수 있습니다. 자세한 내용은 [CBS 마운트](https://intl.cloud.tencent.com/document/product/362/16313)를 참조하십시오.

<span id="modprobeacpiphp"></span>
### 디스크 핫 플러그 기능 활성화
현재 제공되는 모든 미러 이미지는 이미 엘라스틱 CBS의 마운트/언마운트 작업을 지원합니다. **CBS를 언마운트하기 전에 `umount`(Linux) 또는 오프라인(Windows)을 실행하십시오. 그렇지 않으면 클라우드 서버가 다시 엘라스틱 CBS를 마운트할 때 서버가 인식되지 않을 수 있습니다.**
그러나 이전에 다음 운영 체제의 클라우드 서버를 구매하여 엘라스틱 CBS를 마운트하려는 경우, 우선 클라우드 서버에 관련 드라이버를 추가하여 핫 플러그 기능을 추가하시기 바랍니다.
<table>
<tbody>
<tr><th>CVM 운영 체제 유형</th><th>버전</th>
<tr><td rowspan="4">CentOS</td><td>5.11 64비트</td>
<tr><td>5.11 32비트</td>
<tr><td>5.8 64비트</td>
<tr><td>5.8 32비트</td>
<tr><td >Debian</td><td>6.0.3 32비트</td>
<tr><td rowspan="2">Ubuntu</td><td>10.04 64비트</td>
<tr><td>10.04 32비트</td>
<tr><td rowspan="2">openSUSE</td><td>12.3 64비트</td>
<tr><td>12.3 32비트</td>
</tbody>
</table>

1. root 사용자로서 [Linux 클라우드 서버에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)
2. 다음 커맨드를 실행하여 드라이버를 추가하십시오.
```
modprobe acpiphp
```
>클라우드 서버를 종료하거나 재시작 후, ‘acpiphp’ 드라이버 모듈을 다운받아야 할 경우, [3단계](#step3)를 실행하여 ‘acpiphp’ 모듈을 자동 로딩 시작으로 설정하십시오
<span id="step3"></span>
3. (선택 사항)다른 운영 체제에 따라 해당하는 운영 방법을 선택하여 'acpiphp'모듈이 자동 로딩 시작으로 설정하십시오.
 - **CentOS 5 시리즈**
 a. 다음 커맨드를 실행하여 `acpiphp.modules` 파일을 생성하고 여십시오.
```
vi /etc/sysconfig/modules/acpiphp.modules
```
b. 파일에 다음 내용을 추가하고 저장하십시오.
```
 #!/bin/bash
 modprobe acpiphp >& /dev/null
```
c. 다음 커맨드를 실행하여 실행 권한을 추가하십시오.
```
chmod a+x /etc/sysconfig/modules/acpiphp.modules
```
 - **Debian 6 시리즈, Ubuntu 10.04 시리즈**
 a. 다음 커맨드를 실행하여 파일을 수정하십시오.
```
vi /etc/modules
```
b. 파일에 다음 내용을 추가하고 저장하십시오.
```
acpiphp
```
 - **openSUSE 12.3 시리즈**
 a. 다음 커맨드를 실행하여 파일을 수정하십시오.
```
vi /etc/sysconfig/kernel
```
b. 파일에 다음 내용을 추가하고 저장하십시오.
```
MODULES_LOADED_ON_BOOT="acpiphp"
```
