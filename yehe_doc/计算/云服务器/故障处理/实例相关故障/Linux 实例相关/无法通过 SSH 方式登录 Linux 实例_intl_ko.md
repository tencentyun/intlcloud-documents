본 문서에서는 CentOS 7.5 운영 체제의 CVM을 예로 들어 SSH를 통해 Linux 인스턴스에 로그인할 수 없는 문제점 조사 및 솔루션을 소개합니다.

## 장애 현상

3. [SSH를 사용하여 Linux 인스턴스에 로그인](https://cloud.tencent.com/document/product/213/35700)할 때 연결 불가 또는 연결 실패 알림이 뜹니다.

## 장애 진단 및 처리
### 1단계: 보안 그룹 규칙 설정 조회

[보안 그룹(포트) 인증 툴](https://console.cloud.tencent.com/vpc/helper)을 통해 보안 그룹 규칙 설정의 정확 여부를 점검합니다.
- 보안 그룹 포트 설정 문제로 확인되면 툴의 [원클릭 오픈]기능을 통해 포트를 개방할 수 있습니다. 사용자는 실제 수요에 따라 사용자 정의로 보안 그룹 규칙을 설정할 수도 있습니다.
- 보안 그룹 포트 설정에 문제가 없으면 [다음 단계](#step07)를 실행하십시오.
 
###  2단계: sshd 서비스 포트 조회
1. <span id="step07">[VNC를 사용해 Linux 인스턴스에 로그인](https://cloud.tencent.com/document/product/213/35701)합니다.</span>
>?클라이언트 원격 로그인 방식을 사용할 수 없고 기타 로그인 방식으로도 인스턴스에 로그인할 수 없는 경우, VNC 방식으로 인스턴스에 로그인할 수있습니다. 인스턴스 상태를 확인하고 문제를 야기하는 원인을 찾아 해결하시기 바랍니다.
>
2. 운영 체제 인터페이스에서 다음 명령어를 실행하여 sshd 서비스 모니터링의 포트가 포함되었는지 조회합니다.
```
netstat -tnlp | grep sshd
```
 - 다음 결과를 리턴하면 sshd 프로세스가 22 포트를 이미 모니터링하고 있음을 의미하며 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 피드백하십시오.
```
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1015/sshd  
```
 - 출력이 없으면 sshd 서비스가 실행되지 않았을 수 있으며 [다음 단계](#step09)를 실행하십시오.
 
###  3단계: sshd 서비스의 실행 여부 조회
<span id="step09">다음 명령어를 실행하여 sshd 서비스의 실행 여부를 조회합니다.</span>
```
systemctl status sshd.service
```
 - 이미 실행되었으면 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 피드백하십시오.
 - 실행되지 않았으면 다음 명령어를 실행하여 sshd 서비스를 실행시킨 후 다시 SSH를 사용해 Linux 인스턴스에 로그인하십시오.
```
systemctl start sshd
```

상기 작업을 수행한 후 사용자의 인스턴스가 여전히 연결 불가이면 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 피드백할 것을 권장합니다.

