>?
>- 본문은 커뮤니티에서 제공한 내용으로, 참고용으로만 제공됩니다. Tencent Cloud 관련 제품과는 무관합니다.
>- 본문에서 언급된 관련 파일 작업은 신중히 진행하시기 바랍니다. 필요한 경우 스냅샷 등 방법을 통해 데이터를 백업할 수 있습니다.
> 

## 현상 설명
[SSH를 사용해 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501) 시 연결이 되지 않거나 연결이 실패하여 Linux 인스턴스에 정상적으로 로그인할 수 없다는 메시지가 표시됩니다.

## 문제 포지셔닝 및 처리[](id:ProcessingSteps)
SSH를 사용한 Linux 인스턴스에 로그인에 실패하고 오류 메시지가 반환되면, 오류 메시지를 기록하고, 다음과 같은 일반적인 오류 메시지와의 매칭을 통해 문제를 빠르게 진단하고, 처리 방법을 참고하여 해결하십시오.

<dx-accordion>
::: SSH 로그인 오류 User root not allowed because not listed in AllowUsers

#### 문제 원인[](id:userNotListAllowUsers)
이 문제는 일반적으로 SSH 서비스가 사용자 로그인 제어 매개변수를 실행하여 사용자 로그인을 제한하였을 때 발생합니다. 매개변수 설명은 다음과 같습니다.
- **AllowUsers**: 로그인이 허용된 사용자 화이트리스트로, 이 매개변수가 표시된 사용자만 로그인할 수 있습니다.
- **DenyUsers**: 로그인이 거부된 사용자 블랙리스트로, 이 매개변수가 표시된 모든 사용자는 로그인이 거부됩니다.
- **AllowGroups**: 로그인이 허용된 사용자 그룹의 화이트리스트로, 이 매개변수가 표시된 사용자 그룹만 로그인할 수 있습니다.
- **DenyGroups**: 로그인이 거부된 사용자 그룹의 블랙리스트로, 이 매개변수가 표시된 사용자 그룹은 모두 로그인이 거부됩니다.

<dx-alert infotype="explain" title="">
거부 정책은 허용 정책보다 우선 순위가 높습니다.
</dx-alert>


#### 해결 방식
1. [처리 순서](#ProcessingSteps1)를 참고하여 SSH 구성 파일 `sshd_config`로 이동한 후, 설정을 확인합니다.
2. 사용자 로그인 제어 매개변수를 삭제하고 SSH 서비스를 다시 시작합니다.


#### 처리 순서[](id:ProcessingSteps1)
1. [VNC 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)합니다.
2. 다음 명령을 실행하고 VIM 편집기를 사용하여 `sshd_config` 구성 파일로 이동합니다.
```shell
vim /etc/ssh/sshd_config
```
3. **i**를 눌러 편집 모드로 이동하고, 다음 설정을 찾아 삭제하거나, 각 행의 시작 부분에 `#`을 추가하여 주석을 진행합니다.
```shell
AllowUsers root test
DenyUsers test
DenyGroups test
AllowGroups root
```
4. **Esc**를 눌러 편집 모드를 종료하고 **:wq**를 입력하여 변경 사항을 저장합니다.
5. 실제 운영 체제에 따라 다음 명령을 실행하여 SSH 서비스를 재시작합니다.
  - CentOS
```shell
systemctl restart sshd.service
```
  - Ubuntu
```shell
service sshd restart
```

SSH 서비스를 재시작한 후 SSH를 사용하여 로그인할 수 있습니다. 상세 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/32501">SSH를 사용하여 Linux 인스턴스에 로그인</a>을 참고하십시오.


::: 
::: SSH 로그인 오류 Disconnected:No supported authentication methods available

#### 현상 설명[](id:noSupportesAuthentication)
SSH를 사용하여 로그인하면 다음 오류 메시지가 나타납니다.
```
Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
sshd[10826]: Connection closed by xxx.xxx.xxx.xxx.
Disconnected:No supported authentication methods available.
```

#### 문제 원인
원인은 SSH 서비스가 'PasswordAuthentication' 매개변수를 수정하고 비밀번호 인증 로그인을 비활성화하였기 때문입니다.


#### 해결 방식
1. [처리 순서](#ProcessingSteps2)를 참고하여 SSH 구성 파일 `sshd_config`로 이동합니다.
2. 'PasswordAuthentication' 매개변수를 수정하고 SSH 서비스를 재시작합니다.


#### 처리 순서[](id:ProcessingSteps2)
1. [VNC 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)합니다.
2. 다음 명령을 실행하고 VIM 편집기를 사용하여 `sshd_config` 구성 파일로 이동합니다.
```shell
vim /etc/ssh/sshd_config
```
3. **i**를 눌러 편집 모드로 이동한 후, `PasswordAuthentication no`를 `PasswordAuthentication yes`로 변경합니다.
4. **Esc**를 눌러 편집 모드를 종료하고 **:wq**를 입력하여 변경 사항을 저장합니다.
5. 실제 운영 체제에 따라 다음 명령을 실행하여 SSH 서비스를 재시작합니다.
  - CentOS
```shell
systemctl restart sshd.service
```
  - Ubuntu
```shell
service sshd restart
```
SSH 서비스를 재시작한 후 SSH를 사용하여 로그인할 수 있습니다. 상세 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/32501">SSH를 사용하여 Linux 인스턴스에 로그인</a>을 참고하십시오.

:::
::: SSH 로그인 오류 ssh_exchange_identification: read: Connection reset by peer

####  현상 설명[](id:connectionResetByPeer)
SSH를 사용하여 로그인할 때, “ssh_exchange_identification: read: Connection reset by peer” 오류 메시지 또는 다음 오류 메시지가 나타납니다.
- “ssh_exchange_identification: Connection closed by remote host”
- “kex_exchange_identification: read: Connection reset by peer”
- “kex_exchange_identification: Connection closed by remote host”


#### 문제 원인
이러한 유형의 문제에는 여러 가지 원인이 있으며 일반적인 원인은 다음과 같습니다.
- 로컬 액세스 제어로 인한 연결 제한
- 일부 침입 방지 소프트웨어가 Fail2ban, denyhost 등과 같은 방화벽 규칙을 변경함
- sshd 설정의 최대 연결 수 제한
- 로컬 네트워크 문제


#### 해결 방식
[처리 순서](#ProcessingSteps3)를 참고하여 액세스 정책, 방화벽 규칙, sshd 설정 및 네트워크 환경 관련 문제를 진단 및 해결합니다.



#### 처리 순서[](id:ProcessingSteps3)


#### 액세스 정책 설정 확인 및 조정
Linux에서 `/etc/hosts.allow` 및 `/etc/hosts.deny` 파일을 통해 액세스 정책을 설정할 수 있습니다. 두 파일은 각각 허용 및 차단 정책에 해당됩니다. 예를 들어, `hosts.allow` 파일에 신뢰할 수 있는 호스트 규칙을 설정하고, `hosts.deny` 파일에 다른 모든 호스트를 거부할 수 있습니다. 다음은 'hosts.deny' 차단 정책 구성 예시입니다.
```
in.sshd:ALL# 모든 ssh 연결 차단
in.sshd:218.64.87.0/255.255.255.128# 218.64.87.0—-127의 ssh 차단
ALL:ALL# 모든 TCP 연결 차단
```


[VNC를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32494)한 후, `/etc/hosts.deny` 파일과 `/etc/hosts.allow` 파일을 확인합니다. 그리고 확인 결과에 따라 다음 처리 방법을 선택합니다.
 - 설정 오류. 필요에 따라 수정합니다. 수정 작업은 즉시 적용됩니다.
 - 미설정 또는 설정 오류 없음. 다음 단계를 진행합니다.

<dx-alert infotype="explain" title="">
액세스 정책 미설정의 경우, 기본 파일이 비어 있고 모든 연결이 허용됩니다.
</dx-alert>




#### iptables 방화벽 규칙 확인
Fail2ban 및 denyhost와 같은 일부 침입 방지 소프트웨어 사용으로 인해 iptables 방화벽 규칙이 수정되었는지 확인합니다. 다음 명령어를 실행하여 방화벽이 SSH 연결을 차단했는지 확인합니다.
```
sudo iptables -L --line-number
```
 - SSH 연결이 차단된 경우, 해당 소프트웨어 화이트리스트 및 기타 관련 정책을 통해 직접 설정하시기 바랍니다.
 - SSH 연결이 차단되지 않은 경우 다음 단계를 진행합니다.


#### sshd 설정 확인 및 조정
1. 다음 명령을 실행하고 VIM 편집기를 사용하여 `sshd_config` 구성 파일로 이동합니다.
```
vim /etc/ssh/sshd_config
```
2. 'MaxStartups' 값을 조정해야 하는지 확인합니다. `sshd_config` 구성 파일에서 허용되는 최대 연결 수는 `MaxStartups`에 의해 설정되며, 짧은 시간에 더 많은 연결을 설정해야 하는 경우 이 값을 적절하게 조정해야 합니다.
 - 조정이 필요한 경우 다음 단계를 참고하여 수정하십시오.
    1. **i**를 눌러 편집 모드로 이동하고, 수정이 완료된 후 **Esc**를 눌러 편집 모드를 종료하고, **:wq**를 입력하여 수정 사항을 저장합니다.
<dx-alert infotype="explain" title="">
MaxStartups 10:30:100은 SSH 보호 프로세스의 미인증 최대 접속 수량을 지정하는 기본 설정입니다. 10:30:100은 10번째 연결부터 연결 수가 100개에 도달할 때까지 30% 확률(증분)로 새 연결이 거부됨을 의미합니다.
</dx-alert>
    2. 다음 명령어를 실행하여 sshd 서비스를 재시작합니다.
```
service sshd restart
```
 - 조정이 필요하지 않은 경우 다음 단계를 진행합니다.


#### 네트워크 환경 테스트
1. [개인 IP](https://intl.cloud.tencent.com/document/product/213/5225) 사용 여부를 확인합니다.
  - 사용한 경우, [공용 네트워크 IP](https://intl.cloud.tencent.com/document/product/213/5224)로 전환한 후 재시도합니다.
  - 사용하지 않은 경우, 다음 단계를 진행합니다.
2. 다른 네트워크 환경을 사용하여 연결이 정상인지 테스트합니다.
  - 정상인 경우, 인스턴스를 재시작하고 VNC를 사용하여 인스턴스에 로그인합니다.
  - 비정상인 경우, 테스트 결과에 따라 네트워크 환경 문제를 해결합니다.


여전히 SSH 로그인 문제가 해결되지 않으면, 시스템 커널 이상 발생 또는 기타 잠재적인 원인을 의심해볼 수 있습니다. [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 고객센터에 연락하여 문제를 해결하시기 바랍니다.
:::
::: SSH 로그인 오류 Permission denied, please try again

#### 현상 설명[](id:permissionDenied)
root 사용자가 SSH를 사용하여 Linux 인스턴스에 로그인할 때 “Permission denied, please try again” 이라는 오류 메시지가 나타납니다.


#### 문제 원인
가능한 원인은 시스템의 SELinux 서비스 활성화 또는 SSH 서비스의 `PermitRootLogin` 설정 수정입니다.


#### 해결 방식
[처리 순서](#ProcessingSteps4)를 참고하여 SELinux 서비스와 SSH 구성 파일 `sshd_config`의 `PermitRootLogin` 매개변수를 확인하여, 문제 원인 파악 및 해결을 진행합니다.

#### 처리 순서[](id:ProcessingSteps4)


#### SELinux 서비스 확인 및 비활성화 
1. [VNC 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)합니다.
2. 다음 명령어를 실행하여 현재 SELinux 서비스 상태를 확인합니다.
```
/usr/sbin/sestatus -v 
```
반환 매개변수가 'enabled'이면 아래와 같이 활성화 상태이며, 'disabled'이면 비활성화 상태입니다.
```
SELinux status:       enabled
```
3. 실제 상황에 따라 SELinux 서비스를 일시적 또는 영구적으로 비활성화할 수 있습니다.
  - SELinux 서비스 일시적인 비활성화
SELinux를 일시적으로 비활성화하려면 다음 명령을 실행합니다. 수정 사항은 시스템이나 인스턴스를 재시작하지 않고도 실시간으로 적용됩니다.
```
setenforce 0
```
  - SELinux 서비스 영구적인 비활성화
SELinux 서비스를 비활성화 하려면 다음 명령을 실행합니다.
```
sed -i 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
```
<dx-alert infotype="notice" title="">
- 이 명령은 SELinux 서비스가 enforcing 상태일 때만 적용됩니다.
- 명령을 실행한 후 수정 사항을 적용하려면 시스템 또는 인스턴스를 재시작해야 합니다.
</dx-alert>


#### sshd 설정 확인 및 조정
1. [VNC 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)합니다.
2. 다음 명령을 실행하고 VIM 편집기를 사용하여 `sshd_config` 구성 파일로 이동합니다.
```shell
vim /etc/ssh/sshd_config
```
3. **i**를 눌러 편집 모드로 이동한 후, `PermitRootLogin no`를 `PermitRootLogin yes`로 변경합니다.
>?
>- `sshd_config`에 이 매개변수가 설정되어 있지 않으면 기본적으로 root 사용자의 로그인을 허용합니다.
>- 이 매개변수는 SSH를 통한 root 사용자의 로그인에만 영향을 미치며, 다른 방법을 통한 root 사용자 인스턴스 로그인에는 영향을 미치지 않습니다.
>
4. **Esc**를 눌러 편집 모드를 종료하고 **:wq**를 입력하여 변경 사항을 저장합니다.
5. 다음 명령어를 실행하여 SSH 서비스를 재시작합니다.
```shell
service sshd restart
```
SSH 서비스를 재시작한 후 SSH를 사용하여 로그인할 수 있습니다. 상세 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/32501">SSH를 사용하여 Linux 인스턴스에 로그인</a>을 참고하십시오.
:::
::: SSH 로그인 오류 Too many authentication failures for root

#### 현상 설명[](id:tooManyFailures)
SSH를 사용하여 로그인할 때 비밀번호를 여러 번 입력한 후 “Too many authentication failures for root”라는 오류 메시지가 반환되고 연결이 중단됩니다.

#### 문제 원인
잘못된 비밀번호를 여러 번 반복하여 입력하면 SSH 서비스의 비밀번호 재설정 정책이 트리거됩니다.


#### 해결 방식
1. [처리 순서](#ProcessingSteps5)를 참고하여 SSH 구성 파일 `sshd_config`로 이동합니다.
2. SSH 서비스 비밀번호 재설정 정책의 'MaxAuthTries' 매개변수 설정을 확인 및 수정하고 SSH 서비스를 다시 시작합니다.


#### 처리 순서[](id:ProcessingSteps5)
1. [VNC 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)합니다.
2. 다음 명령을 실행하고 VIM 편집기를 사용하여 `sshd_config` 구성 파일로 이동합니다.
```shell
vim /etc/ssh/sshd_config
```
3. 다음과 유사한 설정이 포함되어 있는지 확인합니다.
```
MaxAuthTries 5
```
<dx-alert infotype="explain" title="">
- 이 매개변수는 기본적으로 활성화되어 있지 않으며 사용자가 SSH를 사용하여 로그인할 때마다 잘못된 암호를 연속 입력할 수 있는 횟수를 제한하는 데 사용됩니다. 횟수를 초과하면 SSH 연결이 끊어지고 관련 오류 메시지가 표시됩니다. 그러나 해당 계정은 잠기지 않으며 SSH를 사용하여 다시 로그인할 수 있습니다.
- 실제 상황에 따라 설정 수정 여부를 판단하고 수정이 필요한 경우 `sshd_config` 구성 파일을 백업해 두는 것을 권장합니다.
</dx-alert>
4. **i**를 눌러 편집 모드로 이동한 후, 다음 설정을 수정하거나, 행 시작 부분에 `#`을 추가하여 주석을 진행합니다.
```
MaxAuthTries <잘못된 비밀번호를 입력할 수 있는 횟수>
```
5. **Esc**를 눌러 편집 모드를 종료하고 **:wq**를 입력하여 변경 사항을 저장합니다.
6. 다음 명령어를 실행하여 SSH 서비스를 재시작합니다.
```shell
service sshd restart
```
SSH 서비스를 재시작한 후 SSH를 사용하여 로그인할 수 있습니다. 상세 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/32501">SSH를 사용하여 Linux 인스턴스에 로그인</a>을 참고하십시오.

:::
::: SSH 실행 오류 error while loading shared libraries

#### 현상 설명[](id:errorLibraries)
Linux 인스턴스가 SSH 서비스를 실행할 때, secure 로그 파일에서 또는 직접적으로 다음과 유사한 오류 메시지가 반환됩니다.
- “error while loading shared libraries:  libcrypto.so.10: cannot open shared object file: No such file or directory”
- “PAM unable to dlopen(/usr/lib64/security/pam_tally.so): /usr/lib64/security/pam_tally.so: cannot open shared object file: No such file or directory”


#### 문제 원인
가능한 원인은 SSH 서비스 실행 관련 시스템 라이브러리 파일 손실이나 권한 설정 등의 예외 발생입니다.


#### 해결 방식
[처리 순서](#ProcessingSteps6)를 참고하여 시스템 라이브러리 파일을 확인하고 복구합니다.



#### 처리 순서[](id:ProcessingSteps6)
<dx-alert infotype="explain" title="">
이 글은 libcrypto.so.10 라이브러리 파일 예외 해결을 예로 들어 설명하며, 다른 라이브러리 파일 예외 해결도 이와 유사하므로 실제 상황에 따라 작업하시기 바랍니다.
</dx-alert>



#### 라이브러리 파일 정보 가져오기
1. [VNC 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)합니다.
2. 다음 명령어를 실행하여 libcrypto.so.10 라이브러리 파일 정보를 확인합니다.
```
ll /usr/lib64/libcrypto.so.10
```
다음과 유사한 정보가 반환되는 경우, `/usr/lib64/libcrypto.so.10`가 `libcrypto.so.1.0.2k` 라이브러리 파일의 소프트 링크임을 나타냅니다.
```
lrwxrwxrwx 1 root root 19 Jan 19  2021 /usr/lib64/libcrypto.so.10 -> libcrypto.so.1.0.2k
```
2. 다음 명령어를 실행하여 `libcrypto.so.1.0.2k` 라이브러리 파일 정보를 확인합니다.
```
ll /usr/lib64/libcrypto.so.1.0.2k
```
다음과 유사한 정보가 반환됩니다.
```
-rwxr-xr-x 1 root root 2520768 Dec 17  2020 /usr/lib64/libcrypto.so.1.0.2k
```
3. 일반 라이브러리 파일의 경로, 권한, 그룹 정보를 기록하고 다음과 같이 처리합니다.
	 - [라이브러리 파일 찾기 및 바꾸기](#findAndReplace)
	 - [외부 파일 업로드](#fileUpload)
	 - [스냅샷 롤백을 통한 복구](#snapshotRollback)



#### 라이브러리 파일 찾기 및 바꾸기[](id:findAndReplace)
1. 다음 명령어를 실행하여 `libcrypto.so.1.0.2k` 파일을 찾습니다.
```
find / -name libcrypto.so.1.0.2k
```
2. 반환된 결과에 따라 다음 명령을 실행하여 라이브러리 파일을 일반 디렉터리에 복사합니다.
```
cp <1단계에서 얻은 라이브러리 파일의 절대 경로> /usr/lib64/libcrypto.so.1.0.2k
```
3. 다음 명령어를 순서대로 실행하여 파일 권한, 소유자, 그룹을 수정합니다.
```
chmod 755 /usr/lib64/libcrypto.so.1.0.2k
```
```
chown root:root /usr/lib64/libcrypto.so.1.0.2k
```
4. 다음 명령을 실행하여 소프트 링크를 생성합니다.
```
ln -s /usr/lib64/libcrypto.so.1.0.2k /usr/lib64/libcrypto.so.10
```
5. 다음 명령어를 실행하여 SSH 서비스를 실행합니다.
```
service sshd start
```


#### 외부 파일 업로드[](id:fileUpload)
1. FTP 소프트웨어를 통해 다른 일반 서버의 `libcrypto.so.1.0.2k` 라이브러리 파일을 타깃 서버의 `\tmp` 디렉터리로 업로드합니다.
<dx-alert infotype="explain" title="">
본문은 타깃 서버에 업로드된 `\tmp` 디렉터리를 예로 들며, 실제 상황에 맞게 수정할 수 있습니다.
</dx-alert>
2. 다음 명령을 실행하여 라이브러리 파일을 일반 디렉터리에 복사합니다.
```
cp /tmp/libcrypto.so.1.0.2k /usr/lib64/libcrypto.so.1.0.2k
```
3. 다음 명령어를 순서대로 실행하여 파일 권한, 소유자, 그룹을 수정합니다.
```
chmod 755 /usr/lib64/libcrypto.so.1.0.2k
```
```
chown root:root /usr/lib64/libcrypto.so.1.0.2k
```
4. 다음 명령을 실행하여 소프트 링크를 생성합니다.
```
ln -s /usr/lib64/libcrypto.so.1.0.2k /usr/lib64/libcrypto.so.10
```
5. 다음 명령어를 실행하여 SSH 서비스를 실행합니다.
```
service sshd start
```


#### 스냅샷 롤백을 통한 복구[](id:snapshotRollback)
라이브러리 파일은 인스턴스 시스템 디스크의 과거 스냅샷을 롤백하여 복원할 수 있으며, 자세한 내용은 [스냅샷에서 데이터 롤백](https://intl.cloud.tencent.com/document/product/362/5756)을 참고하십시오.

<dx-alert infotype="notice" title="">
- 스냅샷 롤백은 스냅샷 생성 후 데이터 손실의 원인이 되므로 주의하시기 바랍니다.
- SSH 서비스가 정상적으로 실행될 때까지 스냅샷 생성 시간이 가까운 순으로 롤백을 시도하는 것을 권장합니다. 롤백 후에도 SSH 서비스가 정상적으로 실행되지 않는 경우 해당 시점의 시스템이 비정상적임을 의미합니다.
</dx-alert>

:::
::: SSH 서비스 실행 오류 fatal: Cannot bind any address
#### 현상 설명[](id:cannotBindAddress)
Linux 인스턴스가 SSH 서비스를 실행할 때, secure 로그 파일에서 또는 직접적으로 다음과 유사한 오류 메시지가 반환됩니다.
```
FAILED.
fatal: Cannot bind any address.
address family must be specified before ListenAddress.
```


#### 문제 원인
SSH 서비스의 'AddressFamily' 매개변수의 부적절한 설정으로 인해 발생합니다. 'AddressFamily' 매개변수는 실행 시 사용되는 프로토콜군을 지정하는 데 사용됩니다. 매개변수가 IPv6으로만 설정되어 있고 시스템에서 IPv6이 활성화되어 있지 않거나 IPv6 설정이 유효하지 않은 경우 이 문제가 발생할 수 있습니다.


#### 해결 방식
1. [처리 순서](#ProcessingSteps7)를 참고하여 SSH 구성 파일 `sshd_config`로 이동한 후, 설정을 확인합니다.
2. `AddressFamily` 매개변수를 수정하고 SSH 서비스를 재시작합니다.



#### 처리 순서[](id:ProcessingSteps7)
1. [VNC 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)합니다.
2. 다음 명령을 실행하고 VIM 편집기를 사용하여 `sshd_config` 구성 파일로 이동합니다.
```
vim /etc/ssh/sshd_config
```
3. 다음과 유사한 구성이 포함되어 있는지 확인합니다.
```
AddressFamily inet6
``` 상용 매개변수 관련 설명은 다음과 같습니다.
 - **inet**: 기본값인 IPv4 프로토콜군 사용.
 - **inet6**: IPv6 프로토콜군 사용.
 - **any**: IPv4 및 IPv6 프로토콜군 동시 활성화.
4. **i**를 눌러 편집 모드로 이동한 후, 다음 설정을 수정하거나, 행 시작 부분에 `#`을 추가하여 주석을 진행합니다. 
```
AddressFamily inet
```
<dx-alert infotype="notice" title="">
'AddressFamily' 매개변수는 'ListenAddress' 이전에 구성해야 적용됩니다.
</dx-alert>
5. **Esc**를 눌러 편집 모드를 종료하고 **:wq**를 입력하여 변경 사항을 저장합니다.
6. 다음 명령어를 실행하여 SSH 서비스를 재시작합니다.
```shell
service sshd restart
```
SSH 서비스를 재시작한 후 SSH를 사용하여 로그인할 수 있습니다. 상세 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/32501">SSH를 사용하여 Linux 인스턴스에 로그인</a>을 참고하십시오.

:::
::: SSH 서비스 실행 오류 Bad configuration options

#### 현상 설명[](id:badConfigureOptions)
Linux 인스턴스가 SSH 서비스를 실행할 때, secure 로그 파일에서 또는 직접적으로 다음과 유사한 오류 메시지가 반환됩니다.
```
/etc/ssh/sshd_config: line 2: Bad configuration options:\\ 
/etc/ssh/sshd_config: terminating, 1 bad configuration options
```


#### 문제 설명
구성 파일은 파일 인코딩이나 구성 오류와 같은 비정상적인 문제로 인해 발생합니다.


#### 해결 방식
다음 처리 항목을 참고하여 `sshd_config` 구성 파일을 복구합니다.
- [오류 정보에 해당하는 구성 파일 수정](#changeSetting)
- [외부 파일 업로드](#upload)
- [SSH 서비스 재설치](#installSSH)
- [스냅샷 롤백을 통한 복구](#rollBack)


#### 해결 절차


#### 오류 정보에 해당하는 구성 파일 수정[](id:changeSetting)
오류 정보에 오류 설정이 명확하게 표시된 경우, VIM 편집기를 통해 `/etc/ssh/sshd_config` 구성 파일을 직접 수정할 수 있습니다. 또한, 다른 인스턴스의 올바른 구성 파일을 참고하여 수정할 수 있습니다.


#### 외부 파일 업로드[](id:upload)
1. FTP 소프트웨어를 통해 다른 일반 서버의 `/etc/ssh/sshd_config` 라이브러리 파일을 타깃 서버의 `\tmp` 디렉터리에 업로드합니다.
<dx-alert infotype="explain" title="">
본문은 타깃 서버에 업로드된 `\tmp` 디렉터리를 예로 들며, 실제 상황에 맞게 수정할 수 있습니다.
</dx-alert>
2. 다음 명령을 실행하여 라이브러리 파일을 일반 디렉터리에 복사합니다.
```
cp /tmp/sshd_config /etc/ssh/sshd_config
```
3. 다음 명령어를 순서대로 실행하여 파일 권한, 소유자, 그룹을 수정합니다.
```
chmod 600 /etc/ssh/sshd_config
``` ```
chown root:root /etc/ssh/sshd_config
```
4. 다음 명령어를 실행하여 SSH 서비스를 실행합니다.
```
service sshd start
```


#### SSH 서비스 재설치[](id:installSSH)
1. [VNC 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)합니다.
2. 다음 명령어를 실행하여 SSH 서비스를 언마운트 합니다.
```
rpm -e openssh-server
```
3. 다음 명령어를 실행하여 SSH 서비스를 설치합니다.
```
yum install openssh-server
```
4. 다음 명령어를 실행하여 SSH 서비스를 실행합니다.
```
service sshd start
```

#### 스냅샷 롤백을 통한 복구[](id:rollBack)
라이브러리 파일은 인스턴스 시스템 디스크의 과거 스냅샷을 롤백하여 복원할 수 있으며, 자세한 내용은 [스냅샷에서 데이터 롤백](https://intl.cloud.tencent.com/document/product/362/5756)을 참고하십시오.

<dx-alert infotype="notice" title="">
- 스냅샷 롤백은 스냅샷 생성 후 데이터 손실의 원인이 되므로 주의하시기 바랍니다.
- SSH 서비스가 정상적으로 실행될 때까지 스냅샷 생성 시간이 가까운 순으로 롤백을 시도하는 것을 권장합니다. 롤백 후에도 SSH 서비스가 정상적으로 실행되지 않는 경우 해당 시점의 시스템이 비정상적임을 의미합니다.
</dx-alert>



:::
</dx-accordion>


<br>
문제가 여전히 해결되지 않으면, [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 고객센터에 도움을 요청하십시오.

