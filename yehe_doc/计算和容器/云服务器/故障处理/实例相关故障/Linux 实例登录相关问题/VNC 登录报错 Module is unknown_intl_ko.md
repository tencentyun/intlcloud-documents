## 현상 설명
VNC로 CVM에 로그인할 때 비밀번호를 정확히 입력했는데도 로그인이 안되고 “Module is unknown”이라는 오류 메시지가 나타납니다. 다음 이미지를 참고하십시오.

![](https://main.qcloudimg.com/raw/117961622ff73a5859a56bd890011302.png)

## 예상 원인
VNC로 로그인하면 `/etc/pam.d/login`이라는 pam 모듈을 호출해 인증을 진행하고, 해당 모듈이 `/etc/pam.d/system-auth` 모듈을 불러와 인증을 진행합니다. `/etc/pam.d/login` 구성 파일의 내용은 다음 이미지를 참고하십시오.

![](https://main.qcloudimg.com/raw/334e393e16d8a03eec44009be9265ea9.png)

로그인 실패의 원인은 `system-auth` 구성 파일 중 `pam_limits.so` 모듈의 경로 구성 오류 때문일 수 있습니다. 다음 이미지를 참고하십시오.

![](https://main.qcloudimg.com/raw/36f36e0f2f5d0954f6fcebd39095d3b6.png)


>?`pam_limits.so` 모듈의 핵심 기능은 사용자가 대화 시 여러 시스템 리소스의 사용을 제한하는 것입니다. 모듈 경로는 운영 체제의 실제 상황에 따라 입력해야 하며, 경로를 잘못 입력하면 해당 인증 모듈을 찾을 수 없어 로그인 인증 오류가 발생합니다.



## 해결 방법
1. [작업 순서](#ProcessingSteps)를 참조해 `system-auth` 파일로 들어간 뒤 `pam_limits.so` 모듈 경로 구성을 찾습니다.
2. `pam_limits.so` 모듈 경로를 올바른 구성으로 수정합니다. 

[](id:ProcessingSteps)

## 작업 순서

1. SSH를 사용하여 CVM에 로그인합니다. 자세한 내용은 [SSH를 사용해 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)을 참조하십시오.
 - 로그인에 성공하면 다음 단계를 실행합니다.
 - 로그인에 실패하면 단독 사용자 모드를 사용해야 합니다.
2. 로그인 성공 후 다음 명령어를 실행하여 로그 정보를 조회하십시오.

```
vim /var/log/secure
```

이 파일은 일반적으로 보안 관련 정보 기록에 사용되며, 대부분은 사용자의 CVM 로그인 관련 로그입니다. 다음 이미지와 같이 정보 중에서 `/lib/security/pam_limits.so`가 있는 오류 보고 정보를 가져올 수 있습니다.

![](https://main.qcloudimg.com/raw/8f9f992d1835a9058020b435f1ef3c99.png)

3. 다음 명령어를 차례대로 실행하여 `/etc/pam.d`로 들어간 뒤, 로그에서 오류 보고 pam 모듈의 키워드 `/lib/security/pam_limits.so`를 검색합니다.

```
cd /etc/pam.d
```

```
find . | xargs grep -ri "/lib/security/pam_limits.so" -l
```

다음 이미지와 같은 정보가 반환되면 `system-auth` 파일에 해당 파라미터가 설정되었음을 의미합니다.

![](https://main.qcloudimg.com/raw/eab27cf686eccfeb8a8b796360010bb5.png)

4. `system-auth` 파일로 들어가 `pam_limits.so` 모듈 경로 구성을 복구합니다.
예를 들어, 64비트 운영 체제에서 해당 모듈 경로는 절대 경로 `/lib64/security/pam_limits.so` 또는 상대 경로 `pam_limits.so`로 구성할 수 있습니다.


