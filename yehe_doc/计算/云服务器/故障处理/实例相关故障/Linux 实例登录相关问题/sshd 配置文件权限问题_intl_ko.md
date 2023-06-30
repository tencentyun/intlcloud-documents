## 현상 설명
SSH를 사용하여 Linux 인스턴스에 로그인할 때 ‘ssh_exchange_identification: Connection closed by remote host’ 또는 ‘no hostkey alg’가 표시됩니다.


## 예상 원인
`/var/empty/sshd` 및 `/etc/ssh/ssh_host_rsa_key` 구성 파일 권한 등 sshd 구성 파일의 권한이 수정되어 SSH를 사용하여 로그인하지 못할 수 있습니다.


## 해결 방법
실제 오류 정보와 결합하여 해당 단계를 선택하여 구성 파일 권한을 수정합니다.
 - 오류 메시지가 ‘ssh_exchange_identification: Connection closed by remote host’인 경우, [/var/empty/sshd 파일 권한 수정](#sshd) 단계를 참고하십시오.
 - 오류 메시지가 ‘no hostkey alg’인 경우, [/etc/ssh/ssh_host_rsa_key 파일 권한 수정](#rsa_key) 단계를 참고하십시오.



## 처리 단계

### /var/empty/sshd 파일 권한 수정[](id:sshd)
1. [VNC 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)합니다.
2. 다음 명령어를 실행하여 오류의 원인을 확인합니다.
```
sshd -t
```
다음과 유사한 정보가 반환됩니다.
```plaintext
“/var/empty/sshd must be owned by root and not group or world-writable.”
```
3. 다음 명령을 실행하여 `/var/empty/sshd/` 파일 권한을 수정합니다.
```
chmod 711 /var/empty/sshd/
```



### /etc/ssh/ssh_host_rsa_key 파일 권한 수정[](id:rsa_key)
1. [VNC 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)합니다.
2. 다음 명령어를 실행하여 오류의 원인을 확인합니다.
```
sshd -t
```
반환된 정보에는 다음 필드가 포함됩니다.
```plaintext
“/etc/ssh/ssh_host_rsa_key are too open”
```
3. 다음 명령을 실행하여 `/etc/ssh/ssh_host_rsa_key` 파일 권한을 수정합니다.
```
chmod 600 /etc/ssh/ssh_host_rsa_key
```
