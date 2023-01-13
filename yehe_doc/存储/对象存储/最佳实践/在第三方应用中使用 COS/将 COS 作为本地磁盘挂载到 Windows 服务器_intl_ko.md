## 작업 시나리오
현재 Windows시스템에서의 Tencent Cloud COS 작업은 주로 API, COSBrowser, COSCMD 툴로 구현됩니다.

Windows 서버를 사용하는 사용자는 COSBrowser를 클라우드 저장소로만 사용할 수 있으므로 프로그램을 실행하거나 작업을 수행하는 데 적합하지 않습니다. 본 문서는 비용 효율적인 COS를 로컬 드라이브로 Windows 서버에 마운트하는 방법을 소개합니다.

>? 본 문서에 제공된 예시는 Windows 7 또는 Windows Server 2012 / 2016 / 2019 / 2022에만 적용됩니다.
>

## 작업 단계
### 다운로드 및 설치

본 문서에 제공된 예시에는 세 가지 유형의 소프트웨어가 포함됩니다. 시스템과 호환되는 소프트웨어 버전을 설치할 수 있습니다.
- [Github](https://github.com/billziss-gh/winfsp/releases)로 이동하여 Winfsp를 다운로드합니다.
예시로 winfsp-1.12.22301을 다운로드 합니다. 그 다음 기본 옵션으로 설치할 수 있습니다.
>?Windows Server 2012 R2의 경우 Winfsp 1.12.22242는 호환되지 않지만 Winfsp 1.11.22176은 호환됩니다.
2. [Git](https://gitforwindows.org/) 또는 [Github](https://github.com/git-for-windows/git/releases/)로 이동하여 Git을 다운로드합니다.
Git-2.38.1-64-bit는 예시로 다운로드 됩니다. 그런 다음 기본 옵션으로 설치할 수 있습니다.
3. [Rclone](https://rclone.org/downloads/) 또는 [Github](https://github.com/rclone/rclone/releases)에 접속하여 Rclone을 다운로드합니다.
예시로 rclone-v1.60.1-windows-amd64가 다운로드됩니다. 영어로 이름이 지정된 디렉터리에만 압축을 풀면 됩니다(한자가 포함된 경로로 압축을 풀면 오류가 발생할 수 있음). 이 예시에서 패키지는 E:\AutoRclone으로 압축 해제됩니다.

>? GitHub를 열 수 없거나 다운로드 속도가 느린 경우 다른 다운로드 방법을 찾을 수 있습니다.
>

### Rclone 구성

>!다음 구성 프로세스는 rclone-v1.60.1-windows-amd64를 예로 들어 설명합니다. 구성 프로세스는 버전에 따라 다를 수 있습니다.


1. 폴더를 열고 왼쪽 탐색 창에서 **이 PC**를 찾아 우클릭한 다음 **속성 > 고급 시스템 설정 > 환경 변수 > 시스템 변수 > Path**를 선택합니다. **생성**을 클릭합니다.
2. 팝업 창에 Rclone이 압축 해제된 경로(E:\AutoRclone)를 입력하고 **확인**을 클릭합니다.
3. Windows Powershell을 열고 `rclone --version` 명령을 실행하여 **Enter**를 눌러 Rclone이 성공적으로 설치되었는지 확인합니다.
4. Rclone 설치 확인 후 Windows Powershell에서 `rclone config` 명령을 입력하고 **Enter**를 눌러 명령을 실행합니다.
5. Windows Powershell에서 **n**을 입력하고 **Enter**를 눌러 New remote를 생성합니다.
6. Windows Powershell에서 myCOS와 같은 해당 디스크의 이름을 입력하고 **Enter**를 누릅니다.
7. 표시되는 옵션에서 ‘Tencent COS’가 포함된 옵션을 선택(즉, **5** 입력)한 다음 **Enter**를 누릅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/edd4b224879b2c854c9a32167d3f2aaa.png)
8. 표시되는 옵션에서 ‘TencentCOS’가 포함된 옵션(즉, **21** 입력)을 선택한 다음 **Enter**를 누릅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c7ada8335827fff90078628f05927141.png)
9. `env_auth>`가 표시되면 Enter를 누릅니다.
10. `access_key_id>`가 표시되면 COS의 SecretId를 입력하고 **Enter**를 누릅니다.
>? 여기서는 서브 계정 권한 사용을 권장합니다. [API 키 관리](https://console.cloud.tencent.com/cam/capi)로 이동하여 SecretId와 SecretKey를 확인할 수 있습니다.
>
11. `secret_access_key>`가 표시되면 COS의 SecretKey를 입력하고 **Enter**를 누릅니다.
12. 표시되는 Tencent Cloud 리전의 게이트웨이 주소에 따라 버킷 리전을 선택합니다.
여기에서는 광저우 리전을 예로 사용합니다. 따라서 **4**(`cos.ap-guangzhou.myqcloud.com`)를 입력한 후 **Enter**를 누릅니다.
13. 필요에 따라 객체 권한(예시: default, public-read 등)을 선택합니다. 이 권한은 나중에 업로드되는 객체에만 적용됩니다. 여기서는 default가 예로 사용됩니다. 따라서 **1**을 입력한 다음 **Enter**를 누릅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7756d7599713939368c6bb42cd075d07.png)
15. COS에 업로드된 객체의 스토리지 클래스를 선택합니다. 여기서는 Default가 예로 사용됩니다. 따라서 **1**을 입력한 다음 **Enter**를 누릅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/48e7f6c7d65d13d9fdde690e819bad6c.png)
 - Default: 기본값
 - Standard storage class: 스탠다드 스토리지(STANDARD)
 - Archive storage mode: 아카이브 스토리지(ARCHIVE)
 - Infrequent access storage mode: 스탠다드IA 스토리지(STANDARD_IA)
>?INTELLIGENT TIERING 또는 DEEP ARCHIVE 스토리지 클래스를 사용하려면 **구성 파일 수정** 방법을 사용한 다음 storage_class 값을 INTELLIGENT_TIERING 또는 DEEP_ARCHIVE로 설정합니다. 스토리지 클래스에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오.
>
15. `Edit advanced config? (y/n)`이 표시되면 **Enter**를 누릅니다.
16. 정보에 오류가 없는지 확인한 후 **Enter**를 누릅니다.
17. **q**를 입력하여 구성을 완료합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9cd97c7d75b1b9cfd42a244c03d00fff.png)

### 구성 파일 수정

이전 구성이 완료되면 `C:\Users\Username\AppData\Roaming\rclone` 디렉터리에 rclone.conf라는 구성 파일이 생성됩니다. 파일을 직접 수정하여 rclone 구성을 업데이트할 수 있습니다. 파일을 찾을 수 없는 경우 명령줄 창에서 `rclone config file` 명령을 실행하여 rclone 구성 파일을 볼 수 있습니다.


### COS를 로컬 드라이브로 마운트

1. 설치된 Git Bash를 열고 명령 라인 툴에 실행 명령을 입력합니다. 여기에는 두 가지 사용 시나리오가 제공되며(둘 중 하나 선택), 실제 필요에 따라 둘 중 하나를 선택할 수 있습니다.
<ul>
<li>LAN에서 COS를 공유 드라이브로 마운트하려면(권장) 다음 명령을 실행하십시오.
<pre>
<code class="language-plaintext">rclone mount myCOS:/ Y: --fuse-flag --VolumePrefix=\server\share --cache-dir E:\temp --vfs-cache-mode writes &amp;</code>
</pre>
</li>
<li>로컬 디스크로 매핑된 경우 다음과 같이 명령을 실행합니다:
<pre>
<code class="language-plaintext">rclone mount myCOS:/ Y: --cache-dir E:\temp --vfs-cache-mode writes &</code>
</pre>
	<ul>
		<li>myCOS: 사용자 정의 디스크 이름으로 변경합니다.</li>
		<li>Y: 마운트할 디스크로 변경한 후 디스크의 드라이브 문자를 변경하면 됩니다. 로컬의 C, D, E 드라이브 등과 중복되지 않아야 합니다.</li>
		<li>E:\temp: 필요에 따라 설정할 수 있는 로컬 캐시 디렉터리입니다. 디렉터리에 대한 권한이 있습니다.</li>
	</ul>
</li>
</ul>
"The service rclone has been started"가 안내되면 마운트가 성공적으로 완료되었음을 의미합니다.
2. **exit**를 입력하고 터미널을 종료합니다.
3. 로컬 컴퓨터의 **내 PC**에서 myCOS(Y:)란 이름의 디스크를 찾을 수 있습니다.
해당 디스크를 열면 광저우 리전 전체에 속한 모든 버킷 이름을 조회할 수 있습니다. 이때 업로드, 다운로드, 생성, 삭제 등 로컬 디스크에서 자주 쓰는 작업을 진행할 수 있습니다.
>!
> - 작업 도중 오류가 발생하면 git bash 소프트웨어에서 상세 오류 정보를 확인하십시오.
> - 디스크를 마운트하는 도중 버킷에서 삭제 작업을 하면 버킷 내 파일 존재 여부와 상관없이 모두 삭제될 수 있으니 신중히 작업하시기 바랍니다.
> - 디스크를 마운트하는 도중 버킷 이름을 변경하는 경우 COS 버킷 이름이 변경될 수 있으니 신중히 작업하시기 바랍니다.
> 


### 시작 시 자동으로 마운트된 드라이브 실행

마운트된 드라이브는 서버가 재시작되면 사라집니다. 따라서 다음 작업을 수행하여 시작 시 드라이브가 자동 실행되도록 설정할 수 있습니다.

1. E:\AutoRclone 디렉터리에 startup_rclone.vbs 및 startup_rclone.bat 파일을 생성합니다.
>? Powershell을 통해 텍스트 파일을 생성할 때 올바른 인코딩을 사용하십시오. 그렇지 않으면 생성된 .bat 및 .vbs 파일을 실행할 수 없습니다.
2. startup_rclone.bat에 다음 마운트 명령어를 입력합니다.
 - COS가 LAN에서 공유 드라이브로 마운트된 경우 다음 명령을 실행합니다.
```plaintext
rclone mount myCOS:/ Y: --fuse-flag --VolumePrefix=\server\share --cache-dir E:\temp --vfs-cache-mode writes &
```
 - 로컬 디스크로 매핑한 경우 다음 명령어를 입력합니다.
```
rclone mount myCOS:/ Y: --cache-dir E:\temp --vfs-cache-mode writes &
```
3. startup_rclone.vbs에 다음 코드를 입력합니다.
```plaintext
CreateObject("WScript.Shell").Run "cmd /c E:\AutoRclone\startup_rclone.bat",0
```
>! 코드 경로를 실행 경로로 수정하십시오.
>
4. startup_rclone.vbs 파일을 잘라내 %USERPROFILE%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup 폴더에 붙여 넣습니다.
5. 서버를 재시작합니다.
>?일반적으로 자동 마운트 구성이 완료되고 서버가 다시 시작되면 마운트 성공 메시지가 수십 초 후에 표시됩니다.



## 관련 작업

3rd party 상용화 유료 툴을 사용해 COS를 Windows 서버에 마운트한 후 로컬 디스크로 매핑할 수도 있습니다. 다음 작업은 TntDrive 툴 예시입니다.
1. TntDrive를 다운로드 및 설치합니다.
2. TntDrive를 열고 **Account > Add New Account**를 클릭해 계정을 생성합니다.
![](https://main.qcloudimg.com/raw/90b4a262b11b6933f48b4922cad4fdc4.png)
주요 매개변수 정보는 다음과 같습니다.
 - Account Name: 사용자 정의 계정 이름
 - Account Type: COS는 S3와 호환되므로, 여기서 **Amazon S3 Compatible Storage**를 선택할 수 있습니다.
 - REST Endpoint: 버킷이 위치한 리전을 입력합니다. 예를 들어, 버킷이 광저우 리전에 있다면 cos.ap-guangzhou.myqcloud.com을 입력합니다.
 - Access Key ID: SecretId를 입력합니다. [API 키 관리](https://console.cloud.tencent.com/capi) 페이지에서 생성 및 획득할 수 있습니다.
 - Secret Access Key: SecretKey를 입력합니다.
3. **Add new account**를 클릭합니다.
4. TntDrive 인터페이스에서 **Add New Mapped Drives**를 클릭해 Mapped Drives를 생성합니다.
![](https://main.qcloudimg.com/raw/fa09500f96ba8e5c8144d39cd5471991.png)
주요 매개변수 정보는 다음과 같습니다.
 - Amazon S3 Bucket: 버킷 경로를 입력하거나 버킷 이름을 선택합니다. 우측 버튼을 클릭해 버킷을 선택할 수 있습니다. 2단계에서 설정한 광저우 리전의 버킷이 표시되며, 버킷 1개당 1개의 디스크가 독립적으로 매핑됩니다.
 - Mapped drives letter: 디스크의 드라이브 문자를 설정합니다. 로컬의 C, D, E 드라이브 등과 중복되지 않아야 합니다.
5. 위의 정보를 확인하고 **Add new drive**를 클릭합니다.
6. 로컬 컴퓨터의 **내 PC**에서 드라이브를 찾습니다. 모든 버킷을 Windows 서버에 매핑하려면 위의 단계를 반복합니다.




