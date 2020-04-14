## 작업 시나리오
본 문서는 SCP를 통해 Linux 운영 체제 컴퓨터에서 Linux Cloud Virtual Machine(CVM)로 파일을 업로드하는 방법에 관해 안내합니다.

## 작업 순서

1. Linux 운영 체제의 컴퓨터에서 다음 명령어를 실행하여 파일을 Linux CVM에 업로드합니다.
```
scp 로컬 파일 주소 CVM 로그인 아이디@CVM 공인 IP/도메인: CVM 파일 주소
```
예시, 로컬 파일 `/home/lnmp0.4.tar.gz`를 IP 주소가 '129.20.0.2`인 CentOS 시스템의 CVM 디렉터리에 업로드해야 할 경우, 다음과 같은 명령어를 실행합니다.
```
scp /home/Inmp0.4.tar.gz root@129.20.0.2:/home/Inmp0.4.tar.gz
```
2. **Enter**를 누르고 로그인 비밀번호를 입력하여 업로드를 완료합니다.
