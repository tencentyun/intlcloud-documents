## 사용 시나리오
사용자가 EIP를 통해 외부 네트워크를 액세스할 경우 NAT 모드 또는 EIP 패스스루 모드를 선택할 수 있으며 현재 NAT 모드를 기본으로 합니다.
- NAT 모드에서 EIP는 로컬에서 볼 수 없습니다.
- EIP 패스스루 후, EIP는 로컬에 표시되며 구성 중에 EIP 주소를 매번 수동으로 추가할 필요가 없으므로 개발 비용을 절감할 수 있습니다.

> 현재 EIP 패스스루는 화이트리스트를 통해 제어되며 VPC 내의 장치만 지원합니다.

## 작업 순서
### 1단계: EIP 구성 스크립트 다운로드
EIP 패스스루 프로세스 중 네트워크 중단을 일으킬 수 있으므로 EIP 패스스루 스크립트를 다운로드하고 CVM에 업로드해야 합니다. 순서는 다음과 같습니다.
1.  EIP 패스스루 구성 스크립트를 다운로드하십시오. 다운로드 경로:
 -  [Linux 스크립트 다운로드](https://main.qcloudimg.com/raw/7d07d336030fb1324f3d55c891434612/eip_direct.zip)
 -  [Windows 스크립트 다운로드](https://mc.qcloudimg.com/static/archive/af1eee0dbe7d9407cddb3e1bd510cb3a/eip_windows.zip)

  >Linux 스크립트는 시스템 버전 CentOS 6.x, CentOS 7 및 Ubuntu를 지원합니다.
2. 스크립트를 로컬에 다운로드한 후 EIP 패스스루가 필요한 클라우드 서버에 업로드합니다.

### 2단계: EIP 패스스루 스크립트 실행
1. EIP 패스스루가 필요한 CVM 클라우드 서버에 로그인하십시오.
2. EIP 패스스루 스크립트를 실행하십시오. 자세한 방법:
 - Linux 운영 체제 CentOS
	 - 실행 권한 추가
	```
	chmod +x eip_direct.sh
	```
	- 스크립트 실행
	```
	./eip_direct.sh install XX.XX.XX.XX 
	```
	이 중, `XX.XX.XX.XX`는 선택할 수 있는 EIP 주소입니다.
 - Windows 운영 체제
```
eip_windows.bat XX.XX.XX.XX
```
이 중 `XX.XX.XX.XX`는 EIP 주소입니다.

### 3단계: EIP 패스스루 시작
1. [클라우드 서버 콘솔](https://console.cloud.tencent.com/cvm/overview)에 로그인하십시오.
2. 왼쪽 디렉토리에서 [EIP]를 클릭하여 관리 페이지로 진입합니다.
3. 오른쪽 작업 표시 줄에서 [패스스루]를 클릭하고 활성화합니다.

>- 스크립트는 eth0만 지원하며 현재 보조 ENI는 지원되지 않습니다.
>- NAT Gateway는 패스스루 모드를 활성화한 EIP를 바인딩할 수 있지만 패스스루 효과는 없습니다.
