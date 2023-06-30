## 작업 시나리오

본 문서는 Windows 시스템의 로컬 기기에서 FTP 서비스를 통해 로컬 파일을 CVM에 업로드하는 방법을 소개합니다.

## 전제 조건

CVM에 FTP 서비스가 구축되어 있어야 합니다.
- CVM이 Linux 운영 체제일 경우, 자세한 작업 방식은 [Linux CVM에서 FTP 서비스 구축](https://intl.cloud.tencent.com/document/product/213/10912)을 참조 바랍니다.
- CVM이 Windows 운영 체제일 경우, 자세한 작업 방식은 [Windows CVM에서 FTP 서비스 구축](https://intl.cloud.tencent.com/document/product/213/10414)을 참조 바랍니다.


## 작업 순서

### CVM 연결
1. 로컬에 오픈 소스 소프트웨어인 FileZilla를 다운로드 및 설치합니다.
> FileZilla 3.5.3 버전을 사용해 FTP를 업로드할 경우, 업로드 실패 등의 문제가 발생할 수 있습니다. 공식 홈페이지에서 FileZilla 3.5.1 버전 혹은 3.5.2 버전을 다운로드받아 사용하시기를 권장합니다.
>
2. FileZilla를 엽니다.
3. FileZilla 창에서 호스트, 사용자 이름, 비밀번호 및 포트 등의 정보를 입력한 후, [빠른 연결]을 클릭합니다.

**구성 정보 설명**
 - 호스트: CVM의 공인 IP입니다. [CVM 콘솔](https://console.cloud.tencent.com/cvm)의 인스턴스 관리 페이지에서 해당 CVM의 공인 IP를 조회할 수 있습니다.
 - 사용자 이름: [FTP 서비스 구축](https://intl.cloud.tencent.com/document/product/213/10912)에서 설정한 FTP 사용자의 계정이며, 이미지의 "ftpuser1"는 예시입니다.
 - 비밀번호: [FTP 서비스 구축](https://intl.cloud.tencent.com/document/product/213/10912)에서 설정한 FTP 사용자 계정의 비밀번호입니다.
 - 포트: FTP 리스너 포트로써 기본값은 **21**입니다.
연결을 완료하면 CVM 원격 사이트 파일을 조회할 수 있습니다.

### 파일 업로드
왼쪽 하단의 "로컬 사이트" 창에서 업로드 대기 중인 로컬 파일을 마우스 우클릭 후 [업로드]를 선택하면 아래의 이미지와 같이 바로 Linux CVM에 파일을 업로드할 수 있습니다.
> 
>- CVM의 FTP 터널은 tar 압축 파일 업로드 후의 자동 압축 해제 및 tar 파일 삭제 기능을 지원하지 않습니다.
>- 원격 사이트 경로는 파일을 Linux CVM에 업로드할 때 이용하는 기본 경로입니다.
>

### 파일 다운로드
오른쪽 하단의 “원격 사이트” 창에서 업로드 대기 중인 CVM 파일을 우클릭한 후 [업로드]를 선택하면 파일을 로컬에 다운로드할 수 있습니다.


