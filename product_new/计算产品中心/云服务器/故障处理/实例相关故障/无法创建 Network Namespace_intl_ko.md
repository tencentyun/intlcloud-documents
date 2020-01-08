## 문제 설명
새로운 네트워크 네임스페이스(Network Namespace) 생성을 위한 커맨드 실행 시, 커맨드가 멈추며 작업이 진행되지 않습니다. Dmesg 정보 표시: “unregister_netdevice: waiting for lo to become free. Usage count = 1”

## 문제 원인
해당 문제는 커널의 bug입니다. 현재 아래의 커널 버전은 모두 bug가 존재합니다.
- Ubuntu 16.04 x86_64 커널의 버전은 4.4.0-91-generic입니다.
- Ubuntu 16.04 x86_32 커널의 버전은 4.4.0-92-generic입니다.

## 해결 방법

커널 버전을 4.4.0-98-generic 버전으로 업데이트하면 버전의 bug는 수정됩니다.

## 처리 순서
1. 아래의 명령어를 실행하여 현재 커널의 버전을 조회하십시오.
```
uname -r
```
2. 아래의 명령어를 실행하여 4.4.0-98-generic 버전으로 업데이트할 커널이 있는지 조회하십시오.
```
sudo apt-get update
sudo apt-cache search linux-image-4.4.0-98-generic
```
다음의 정보가 표시될 경우, 소스에 버전이 존재하며 업데이트를 진행할 수 있음을 나타냅니다.
```
linux-image-4.4.0-98-generic - Linux kernel image for version 4.4.0 on 64 bit x86 SMP
```
3. 아래의 명령어를 실행하여 새로운 버전의 커널과 대응하는 Header 패키지를 설치하십시오.
```
sudo apt-get install linux-image-4.4.0-98-generic linux-headers-4.4.0-98-generic
```
4. 아래의 명령어를 실행하여 시스템을 재시작하십시오.
```
sudo reboot
```
5. 아래의 명령어를 실행하여 시스템에 진입한 뒤, 커널 버전을 확인하십시오.
```
uname -r
```
다음의 결과가 표시될 경우 버전 업데이트가 완료되었음을 나타냅니다.
```
4.4.0-98-generic
```
