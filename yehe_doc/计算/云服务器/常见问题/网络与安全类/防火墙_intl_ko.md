### Linux 시스템은 어떻게 방화벽 소프트웨어 iptables를 설정하나요?
> **참고:**
> iptables 의 경우, CentOS 7 이전과 이후의 버전에서 큰 차이가 있습니다.
> - CentOS 7 이전에는 iptables 서비스를 기본 방화벽으로 사용하고, `service iptables stop`코드를 사용하며, iptables 서비스가 먼저 규칙을 삭제한 후 iptables 모듈을 언마운트합니다. 다시 start 할 때 구성 파일에서 규칙을 로딩합니다. iptables 서비스를 중단하여 방화벽 제한 여부를 테스트할 수 있습니다.
> ![](https://main.qcloudimg.com/raw/5fbb351650cdd763e8450d7e04b18b78.jpg)
> - CentOS 7 이후에는 firewall 서비스를 기본 방화벽으로 사용하고, 호환성을 위해 iptables_filter 모듈을 동시에 로딩했으나 iptables 서비스가 사라졌습니다. 따라서 CentOS 7 이후 iptables 명령어를 사용해 규칙을 추가할 수 있으나 iptables 서비스가 기본 비활성 상태에 있습니다. 사용자는 iptable_filter 모듈 로딩을 확인하여 즉시 규칙을 적용할 수 있습니다.

방화벽을 판단하는 가장 타당한 방법은 `iptables -nvL` 규칙 조회입니다. 
다음 두 예시를 통해 어떻게 구성하는지 설명합니다. 
#### 시나리오 1
Ubuntu 14 시스템은 보안 그룹을 개방하여 포트를 모니터링 하지만, telnet 가 통신되지 않습니다.
보안 그룹 인바운드 규칙:
![](https://main.qcloudimg.com/raw/4a6a1c7eca94a76ddbce457dbe28affa.png)
보안 그룹 아웃바운드 규칙:
![](https://main.qcloudimg.com/raw/90914e729ba27a6a9253e719bf4a9703.png)
telnet가 통신되지 않았습니다:
![](https://main.qcloudimg.com/raw/74c521a97d4b9dab64b85ce62ab2cf86.png)
#### 해결 방식
1. 우선 호스트에 대해 패킷 캡쳐를 하여, 패킷이 호스트에 도착했는지 판단합니다.
 - 호스트에 도착하지 않았으면 보안 그룹 또는 상층 tgw, 통신사에 의해 차단되었을 수 있습니다.
 - 패킷이 호스트에 도착했으나 리턴 패킷에 문제가 생긴 경우는 호스트 내부의 iptables 정책에 의한 것일 가능성이 아주 높습니다. 다음 그림과 같이 telnet 후 64.11로 TCP 패킷을 리턴하지 않았습니다.
![](https://main.qcloudimg.com/raw/1052893022c8786a9b7b0166a57ce16d.png)  

2. iptables 정책 문제임을 확인한 후, `iptables –nvL`을 통해 정책이 8081 포트를 개방했는지 확인합니다. 이곳은 해당 포트를 개방하지 않았습니다. 
![](https://main.qcloudimg.com/raw/f214d470f1d40ed7061ea155de756bca.jpg) 
3. 명령어를 사용하여 8081 포트 개방 정책을 추가합니다.
```
iptables -I INPUT 5 -p tcp  --dport 8081 -j ACCEPT
```
4. 8081 포트가 개방되었음을 테스트하였으며, 문제를 해결했습니다.  


#### 시나리오 2
iptables 구성으로 볼 때 정책을 개방했으나 타깃 기기의 ping이 아직 개통되지 않습니다.
![](https://main.qcloudimg.com/raw/46fdf4e20187c5b366c7773d73eb1cee.png)
#### 해결 방식
아래의 상황이 나타날 경우:
![](https://main.qcloudimg.com/raw/babfa7fcfe9dd7536ba011c3fbaab7bc.jpg)
명령어를 사용해 output 규칙의 첫 번째 조항을 삭제합니다:
```
iptabels –D OUTPUT 1
```
테스트 완료, 문제를 해결했습니다.

### 방화벽을 어떻게 제거하나요?
#### Windows 인스턴스:
1. 인스턴스에 로그인한 후 [시작]>[제어판][방화벽 설정]을 클릭하여 방화벽 설정 페이지로 이동합니다.

2. 방화벽 및 기타 보안 프로그램(예: safedog 등) 활성화 여부를 점검합니다. 활성화되었을 경우 닫으면 됩니다.

#### Linux 인스턴스:
1. 명령어를 실행하여 고객이 방화벽 정책을 활성화했는지 조회합니다. 정책이 비활성 상태인 경우 2단계를 건너뛰어 바로 3단계를 진행합니다.
```
iptables -vnL
```

2. 방화벽 정책을 활성화한 경우, 명령어를 실행하여 현재 방화벽 정책을 백업합니다.
```
iptables-save
```

3. 명령어를 실행하여 방화벽 정책을 제거합니다.
```
iptables -F
```

### 비 Tencent Cloud CDN 가속 CVM을 사용하는 경우 방화벽에 의해 차단되나요?
차단되지 않습니다. 만일의 상황이 우려된다면 방화벽을 종료할 수 있습니다.