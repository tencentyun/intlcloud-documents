## 작업 시나리오
Rdesktop은 원격 데스크톱 프로토콜(RDP)의 오픈 소스 클라이언트로 Windows CVM을 연결하는 등의 작업에 사용됩니다. 본 문서는 로컬 Linux 기기에서 rdesktop을 사용하여 Windows Server 2012 R2 운영 체제의 Tencent Cloud Cloud Virtual Machine(CVM)에 빠르게 파일을 업로드하는 방법을 소개합니다.
>? 
>- 로컬 Linux 기기는 시각화 인터페이스를 구축하지 않으면 rdesktop을 사용할 수 없습니다. 
>- 본 문서의 Linux 운영 체제는 CentOS 7.6을 예로 들어 설명하고 있으며 버전 별로 운영 체제 단계가 상이할 수 있으니 실제 서비스 상황에 맞춰 문서를 참고하시기 바랍니다.  
>

##  전제 조건
Windows CVM을 구매해야 합니다.

## 작업 순서
### 공용 IP 획득
[CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 후, 인스턴스 리스트 페이지에서 파일을 업로드할 CVM의 공용 IP를 다음 이미지와 같이 기록합니다.
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)

### rdesktop 설치
1. 단말기에서 다음 명령어를 실행하여 rdesktop 설치 패키지를 다운로드합니다. 이 단계에서는 rdesktop 1.8.3 버전을 예시로 사용합니다.
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
최신 설치 패키지가 필요한 경우 [GitHub rdesktop 페이지](https://github.com/rdesktop/rdesktop/releases)에서 최신 설치 패키지를 검색하고 명령어 라인에서 최신 설치 경로로 바꿔줍니다.
2. 다음 명령어를 차례로 실행하고 설치 패키지를 압축 해제하여 설치 디렉터리로 들어갑니다. 
```
tar xvzf rdesktop-1.8.3.tar.gz
```
```
cd rdesktop-1.8.3
```
3. 다음 명령어를 차례로 실행하고 rdesktop을 컴파일 설치합니다.
```
./configure 
```
```
make
```
```
make install
```
4. 설치가 완료되면 다음 명령어를 실행하여 정상적으로 설치되었는지 확인할 수 있습니다.
```
rdesktop
```

### 파일 업로드
1. 다음 명령어를 실행하고 CVM에 공유할 폴더를 지정합니다.
```
rdesktop CVM 공인 IP -u CVM 계정 -p CVM 로그인 비밀번호 -r disk: 지정된 공유 폴더 이름=로컬 폴더 경로
```
>?
>- CVM 계정은 `Administrator`로 기본 설정되어 있습니다.
>- 시스템 기본 설정 비밀번호로 인스턴스에 로그인할 경우, [내부 메시지](https://console.cloud.tencent.com/message)로 이동하여 획득하십시오.
>- 비밀번호를 잊으신 경우, [인스턴스 비밀번호 리셋](https://intl.cloud.tencent.com/document/product/213/16566)을 참고하십시오.
>
예: 다음 명령어를 실행하여 로컬 컴퓨터의 `/home` 폴더를 지정된 CVM에 공유하고 공유 폴더 이름을 `share`로 변경합니다.
```
rdesktop 118.xx.248.xxx  -u Administrator -p 12345678 -r disk:share=/home
```
공유가 완료되면 Windows CVM 인터페이스를 실행합니다.
왼쪽 하단의 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px"> > [내 PC]를 클릭하면 CVM 시스템 인터페이스에서 공유 중인 폴더를 확인할 수 있습니다.
2. 더블 클릭으로 공유 폴더를 열고, 업로드하려는 로컬 파일을 Windows CVM의 다른 디스크에 복사해 넣으면 파일 업로드가 완료됩니다.
예: `share` 폴더 안의 A 파일을 Windows CVM의 C: 드라이브로 복사합니다.

### 파일 다운로드
Windows CVM의 파일을 로컬 컴퓨터로 다운로드하려는 경우, 파일 업로드 작업을 참고하여 필요한 파일을 Windows CVM에서 공유 폴더로 복사해 파일을 다운로드할 수 있습니다.
