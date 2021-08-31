### CVM은 FTP 업로드 기능을 보유하고 있나요?
FTP는 사용자의 실제 필요에 따라 직접 설치 및 설정해야 합니다.
- Windows 자체의 FTP 서비스를 사용하여 FTP 사이트를 구축하려면, [Windows CVM에서 FTP 서비스 구축](https://intl.cloud.tencent.com/document/product/213/10414)을 참조 바랍니다.
- vsftpd 소프트웨어를 사용하여 FTP 사이트를 구축하려면, [Linux CVM에서 FTP 서비스 구축](https://intl.cloud.tencent.com/document/product/213/10912)을 참조 바랍니다.

### Windows CVM에 파일을 업로드하려면 어떻게 해야 하나요?
- 로컬 컴퓨터가 Windows 운영 체제를 사용할 경우, [MSTSC를 사용하여 CVM에 파일 업로드](https://intl.cloud.tencent.com/document/product/213/2761)를 참조 바랍니다.
- 로컬 컴퓨터가 Linux 운영 체제를 사용할 경우, [RDP방식으로 CVM에 파일 업로드](https://intl.cloud.tencent.com/document/product/213/34822)를 참조 바랍니다.
- 로컬 컴퓨터가 MacOS 운영 체제를 사용할 경우, [MRD를 사용하여 CVM에 파일 업로드](https://intl.cloud.tencent.com/document/product/213/34820)를 참조 바랍니다.

### 로컬 호스트와 Windows CVM 간의 데이터 전송은 어떻게 하나요?
다음과 같은 방법으로 전송할 수 있습니다.
- Windows 시스템 로컬 컴퓨터에서 RDP 파일을 사용하여 Windows CVM에 로그인하면 로컬 파일을 CVM에 직접 드래그하여 업로드할 수 있습니다.
- [원격 데스크톱에서 MSTSC를 연결하는 방식으로 데이터 전송](https://intl.cloud.tencent.com/document/product/213/2761)을 통해 데이터를 전송할 수 있습니다.
- [FTP 서비스 구축](https://intl.cloud.tencent.com/document/product/213/10912)을 통해 CVM에 파일을 업로드할 수 있습니다.

### WinSCP를 사용하여 Linux CVM에 파일을 업로드하려면 어떻게 해야 하나요?
자세한 작업 방식은 [Windows 시스템에서 WinSCP를 사용하여 Linux CVM에 파일 업로드](https://intl.cloud.tencent.com/document/product/213/2131)를 참조 바랍니다.

### Linux CVM에서 SCP를 사용하여 파일을 업로드, 다운로드 하려면 어떻게 해야 하나요?
자세한 작업 방식은 [Linux 시스템에서 SCP를 사용하여 Linux CVM에 파일 업로드](https://intl.cloud.tencent.com/document/product/213/2133)를 참조 바랍니다.

### FTP를 사용하여 파일을 업로드할 때, 클라이언트의 서버 연결이 타임아웃되면 어떻게 해야 하나요?
서버의 방화벽이나 보안 그룹 차단으로 인해 타임아웃되었을 가능성이 있으므로, 다음의 작업을 통해 해결하시기 바랍니다.
1. 서버 방화벽 설정을 확인합니다.
2. 방화벽을 비활성화하거나, 해당하는 규칙을 추가합니다.
