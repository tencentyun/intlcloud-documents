## 작업 시나리오
현재 Windows시스템에서의 Tencent Cloud COS 작업은 주로 API, COSBrowser, COSCMD 툴로 구현됩니다.

Windows 서버를 즐겨 사용하는 사용자에게 COSBrowser 툴은 대부분 웹 디스크로 간주되며 이는 서버에서 사용하는 프로그램 또는 작업에 적합하지 않습니다. 본 문서는 스토리지 가격이 저렴한 COS를 Windows 서버에 마운트하고 로컬 디스크에 매핑하는 방법을 소개합니다.

>? 본 사례는 Windows 7/Windows Server 2012 이상 버전의 운영 체제에 적합합니다.
>

## 작업 순서
### 다운로드 및 설치

다음과 같은 설치 방법을 제공하며, 사용자의 시스템에 따라 선택할 수 있습니다.
- [Github](https://github.com/billziss-gh/winfsp/releases)에서 Winfsp를 다운로드합니다.
다운로드 완료 후 순서대로 기본적인 설치를 진행합니다.
- [Git 공식 홈페이지](https://gitforwindows.org/) 또는 [Github](https://github.com/git-for-windows/git/releases/)에서 Git 툴을 다운로드합니다.
본 사례에서 다운로드한 버전은 Git-2.31.1-64-bit.exe입니다. 다운로드 완료 후 순서대로 기본적인 설치를 진행합니다.
- [Rclone 공식 홈페이지](https://rclone.org/downloads/) 또는 [Github](https://github.com/rclone/rclone/releases)에서 Rclone 툴을 다운로드합니다.
본 사례에서 다운로드한 버전은 rclone-v1.55.0-windows-amd64.zip입니다. 이 소프트웨어는 설치할 필요가 없으며, 다운로드 후 임의의 영어 디렉터리에서 압축을 해제하면 됩니다. 압축 해제 경로에 중국어가 포함된 경우 오류가 발생할 수 있습니다. 본 사례의 경로 예시는 E:\AutoRclone입니다.

>? Github 다운로드는 속도가 느리거나 열리지 않는 경우가 있으며, 직접 다른 공식 홈페이지의 루트로 다운로드할 수 있습니다.
>

### Rclone 설정

1. 임의의 폴더를 열고, 왼쪽 메뉴 디렉터리의 [내 PC]에서 마우스 오른쪽 버튼을 클릭한 다음 [속성] > [고급 시스템 설정] > [환경 변수] > [시스템 변수] > [Path]에서 [새로 만들기]를 클릭합니다.
2. 팝업 창에서 Rclone 압축 해제 후의 경로(E:\AutoRclone)를 입력하고 [확인]을 클릭합니다.
3. Windows Powershell을 열어 `rclone --version` 명령어를 입력하고 **Enter**를 눌러 Rclone이 설치되었는지 확인합니다.
4. Rclone 설치 확인 후 Windows Powershell에서 `rclone config` 명령어를 입력하고 **Enter**를 누릅니다.
5. Windows Powershell에서 **n**을 입력하고 **Enter**를 눌러 New remote를 생성합니다.
6. Windows Powershell에서 myCOS와 같은 해당 디스크의 이름을 입력하고 **Enter**를 누릅니다.
7. 화면에 보이는 옵션 중 Tencent Cloud를 포함한 옵션을 선택합니다. **4**를 입력하고 **Enter**를 누릅니다.
8. 화면에 보이는 옵션 중 Tencent Cloud COS를 포함한 옵션을 선택합니다. **11**을 입력하고 **Enter**를 누릅니다.
9. `env_auth>`를 실행할 경우 Enter를 누릅니다.
10. `access_key_id>`를 실행할 경우 Tencent Cloud COS의 액세스 키 SecretId를 입력하고 **Enter**를 누릅니다.
>? 여기서는 서브 계정 권한 사용을 권장합니다. [API 키 관리](https://console.cloud.tencent.com/cam/capi)에서 SecretId와 SecretKey를 조회할 수 있습니다.
>
11. `secret_access_key>`를 실행할 경우 Tencent Cloud COS의 액세스 키 SecretKey를 입력하고 **Enter**를 누릅니다.
12. 화면에 보이는 Tencent Cloud 각 리전의 게이트웨이 주소에 따라 버킷이 있는 리전을 조회하여 해당하는 리전을 선택합니다.
본 사례의 예시는 광저우입니다. `cos.ap-guangzhou.myqcloud.com`을 선택한 후 **4**를 입력하고 **Enter**를 누릅니다.
13. 화면에 보이는 Tencent Cloud COS의 권한 유형 중 실제 필요에 따라 private 또는 public-read를 선택합니다. 여기서 선택한 권한 유형은 객체 권한 유형으로, 새로 업로드한 파일에만 유효합니다. 본 사례의 예시는 public-read입니다. **2**를 입력하고 **Enter**를 누릅니다.
14. 화면에 보이는 Tencent Cloud COS의 스토리지 유형 중 실제 필요에 따라 스토리지 유형을 선택하여 COS에 파일을 업로드할 수 있습니다. 본 사례의 예시는 Default입니다. **1**을 입력하고 **Enter**를 누릅니다.
 - Default: 기본값
 - Standard storage class: 표준 스토리지(STANDARD)
 - Infrequent access storage mode: 표준IA 스토리지(Standard_IA)
 - Archive storage mode: CAS(ARCHIVE)
 >?INTELLIGENT TIERING 또는 DEEP ARCHIVE 유형 설정이 필요한 경우 **구성 파일 수정** 방식을 이용하십시오. 구성 파일에서 storage_class 값을 INTELLIGENT_TIERING 또는 DEEP_ARCHIVE로 설정하면 됩니다.
15. `Edit advanced config? (y/n)`를 실행할 경우 **Enter**를 누릅니다.
16. 정보에 오류가 없는지 확인한 후 **Enter**를 누릅니다.
17. **q**를 입력하고 설정을 완료합니다.


### 구성 파일 수정

위 단계의 설정을 완료하면 `C:\Users\사용자 이름\.config\rclone` 폴더에서 rclone.conf라는 이름의 파일을 확인할 수 있습니다. 해당 파일은 rclone의 구성 파일입니다. rclone의 설정은 필요한 경우 직접 수정할 수 있습니다.


### COS를 로컬 디스크로 마운트

1. 설치한 Git CMD를 열고 실제 필요에 따라 다음 명령어를 실행합니다.
<ul>
<li>LAN 공유 드라이버로 매핑(권장):
<pre>
<code class="language-plaintext">rclone mount myCOS:/ Y: --fuse-flag --VolumePrefix=\server\share --cache-dir E:\temp --vfs-cache-mode writes &amp;</code>
</pre>
</li>
<li>로컬 디스크로 매핑:
<pre>
<code class="language-plaintext">rclone mount myCOS:/ Y: --cache-dir E:\temp --vfs-cache-mode writes &</code>
</pre>
	<ul>
		<li>myCOS: 사용자 정의 디스크 이름으로 변경합니다.</li>
		<li>Y: 마운트할 디스크로 변경한 후 디스크의 드라이브 문자를 변경하면 됩니다. 로컬의 C, D, E 드라이브 등과 중복되지 않아야 합니다.</li>
		<li>E:\temp는 로컬 캐시 디렉터리이며 직접 설정할 수 있습니다.</li>
	 </ul>
</li>
</ul>
"The service rclone has been started"가 안내되면 마운트가 성공적으로 완료되었음을 의미합니다.
2. **exit**를 입력하고 터미널을 종료합니다.
3. 로컬 컴퓨터의 [내 PC]에서 myCOS(Y:)란 이름의 디스크를 찾을 수 있습니다.
해당 디스크를 열면 광저우 리전 전체에 속한 모든 버킷 이름을 조회할 수 있습니다. 이때 업로드, 다운로드, 생성, 삭제 등 로컬 디스크에서 자주 쓰는 작업을 진행할 수 있습니다.
>!
> - 작업 도중 오류가 발생하면 git bash 소프트웨어에서 상세 오류 정보를 확인하십시오.
> - 디스크를 마운트하는 도중 버킷에서 삭제 작업을 하면 버킷 내 파일 존재 여부와 상관없이 모두 삭제될 수 있으니 신중히 작업하시기 바랍니다.
> - 디스크를 마운트하는 도중 버킷 이름을 변경하는 경우 COS 버킷 이름이 변경될 수 있으니 신중히 작업하시기 바랍니다.
> 


### 시작 시 디스크 마운트 자동 실행 설정

위 작업은 컴퓨터를 재시작하면 매핑된 디스크가 사라지므로, 다시 수동으로 작업해야 합니다. 따라서 서버가 재시작할 때마다 자동으로 디스크를 마운트하도록 자동 실행을 설정할 수 있습니다.

1. Rclone에 디렉터리 E:\AutoRclone을 설치하고 startup_rclone.vbs와 startup_rclone.bat 파일을 각각 생성합니다.
2. startup_rclone.bat에 다음 마운트 명령어를 입력합니다.
 - LAN 공유 드라이버로 매핑한 경우 다음 명령어를 입력합니다.
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

## 관련 작업

3rd party 상용화 유료 툴을 사용해 COS를 Windows 서버에 마운트한 후 로컬 디스크로 매핑할 수도 있습니다. 다음 작업은 TntDrive 툴 예시입니다.
1. TntDrive를 다운로드 및 설치합니다.
2. TntDrive를 열고 [Account]>[Add New Account]를 클릭해 계정을 생성합니다.
![](https://main.qcloudimg.com/raw/90b4a262b11b6933f48b4922cad4fdc4.png)
주요 매개변수 정보는 다음과 같습니다.
 - Account Name: 사용자 정의 계정 이름
 - Account Type: COS는 S3와 호환되므로, 여기서 [Amazon S3 Compatible Storage]를 선택할 수 있습니다.
 - REST Endpoint: 버킷이 위치한 리전을 입력합니다. 예를 들어, 버킷이 광저우 리전에 있다면 cos.ap-guangzhou.myqcloud.com을 입력합니다.
 - Access Key ID: SecretId를 입력합니다. [API 키 관리](https://console.cloud.tencent.com/capi) 페이지에서 생성 및 획득할 수 있습니다.
 - Secret Access Key: SecretKey를 입력합니다.
3. [Add new account]를 클릭합니다.
4. TntDrive 인터페이스에서 [Add New Mapped Drives]를 클릭해 Mapped Drives를 생성합니다.
![](https://main.qcloudimg.com/raw/fa09500f96ba8e5c8144d39cd5471991.png)
주요 매개변수 정보는 다음과 같습니다.
 - Amazon S3 Bucket: 버킷 경로를 입력하거나 버킷 이름을 선택합니다. 우측 버튼을 클릭해 버킷을 선택할 수 있습니다. 2단계에서 설정한 광저우 리전의 버킷이 표시되며, 버킷 1개당 1개의 디스크가 독립적으로 매핑됩니다.
 - Mapped drives letter: 디스크의 드라이브 문자를 설정합니다. 로컬의 C, D, E 드라이브 등과 중복되지 않아야 합니다.
5. 위의 정보를 확인하고 [Add new drive]를 클릭합니다.
6. 로컬 컴퓨터의 [내 PC]에서 해당 디스크를 찾을 수 있습니다. 모든 버킷을 Windows 서버에 매핑하려면 위 절차를 반복하십시오.



