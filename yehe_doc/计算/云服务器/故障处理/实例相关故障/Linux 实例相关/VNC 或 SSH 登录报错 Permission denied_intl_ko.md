## 현상 설명
VNC 또는 SSH로 로그인 시 “Permission denied”라는 오류 알림이 나타납니다.
- VNC 로그인 오류 알림은 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/5f1aedd75b6d99cddab4d83fa82d964f.png)
- SSH 로그인 오류 알림은 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/7ab31fbb82391da2c8ae28e8ad3b961f.png)

## 예상 원인
VNC 또는 SSH로 로그인하면 `/etc/pam.d/login`이라는 pam 모듈을 호출해 인증을 진행하고, `/etc/pam.d/login` 구성에서 기본적으로 `system-auth` 모듈을 가져와 인증을 진행합니다. 그러면 `system-auth` 모듈은 기본적으로 `pam_limits.so` 모듈을 가져와 인증을 진행합니다. `system-auth`의 기본 구성은 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/e32db00ec665388bc4c7cb0454fd6fab.png)
`pam_limits.so` 모듈의 핵심 기능은 사용자가 대화 시 여러 시스템 리소스의 사용을 제한하는 것입니다. 기본적으로 해당 모듈의 구성 파일은 `/etc/security/limits.conf`로, 해당 구성 파일은 사용자가 사용 가능한 최대 파일 갯수, 최대 스레드 수, 최대 메모리 등 리소스 사용량을 규정하고 있습니다. 매개변수에 대한 설명은 다음 표와 같습니다.
<table>
<tr>
<th style="width:20%">매개변수</th><th>설명</th>
</tr>
<tr>
<td><code>soft nofile</code></td>
<td>열 수 있는 최대 파일 기술자 수 입니다(soft limits). </td>
</tr>
<tr>
<td><code> hard nofile</code></td>
<td>열 수 있는 최대 파일 기술자 수로(hard limits), 해당 설정값을 초과할 수 없습니다. </td>
</tr>
<tr>
<td><code>fs.file-max </code></td>
<td>시스템 수준에서 열 수 있는 파일 핸들(커널의 struct file)의 수량입니다. 사용자에 대한 제한이 아닌 전체 시스템에 대한 제한입니다. </td>
</tr>
<tr>
<td><code>fs.nr_open</code></td>
<td>개별 프로세스에서 할당할 수 있는 최대 파일 기술자 수(fd 개수). </td>
</tr>
</table> 

정상적으로 로그인할 수 없는 원인은 구성 파일 `/etc/security/limits.conf`에서 root 사용자가 열 수 있는 최대 파일 기술자 수의 개수 설정에 오류가 있기 때문일 수 있습니다. 올바른 구성은 `soft nofile ≤ hard nofile ≤ fs.nr_open`의 관계에 부합해야 합니다.


## 해결 방법
[작업 순서](#ProcessingSteps)를 참조해 `soft nofile`, `hard nofile` 및 `fs.nr_open`을 올바른 구성으로 수정합니다.

[](id:ProcessingSteps)

## 작업 순서

1. SSH를 사용하여 CVM에 로그인합니다. 자세한 내용은 [SSH를 사용해 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)을 참조하십시오.
	- 로그인에 성공하면 다음 단계를 실행합니다.
	- 로그인에 실패하면 단독 사용자 모드를 사용해야 합니다.
2. `soft nofile`, `hard nofile` 및 `fs.nr_open`의 매개변수 값이 `soft nofile ≤ hard nofile ≤ fs.nr_open` 관계에 부합하는지 확인합니다.
 - 다음 명령어를 실행하고 `soft nofile` 및 `hard nofile` 값을 확인합니다.
```
/etc/security/limits.conf
```
본 문서에서 도출한 결과값은 3000001과 3000002입니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/3bc035efb6cf46f70b30017dbefe831a.png)
 - 다음 명령어를 실행하여 `fs.nr_open` 값을 조회하십시오.
```
sysctl -a 2>/dev/null | grep -Ei "file-max|nr_open"
```
본 문서에서 도출한 결과값은 1048576입니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/0fee5e2cda62d6a558cf808652a6b9dd.png)
3. `/etc/security/limits.conf` 파일을 수정하고, 파일 끝에 다음과 같은 구성을 추가하거나 수정합니다. 
 - `root soft nofile`: 100001
 - `root hard nofile`: 100002
4. `/etc/sysctl.conf` 파일을 수정하고, 파일 끝에 다음과 같은 구성을 추가하거나 수정합니다.
>?`soft nofile ≤ hard nofile ≤ fs.nr_open` 관계에 부합하는 경우, 이 단계를 생략할 수 있으며, 시스템 최대 제한이 부족할 경우 조정할 수 있습니다.
>
 - `fs.file-max` = 2000000
 - `fs.nr_open` = 2000000
5. 다음 명령어를 실행하여 설정을 즉시 적용합니다. 설정이 완료되면 다시 로그인이 가능합니다.
```
sysctl -p
```

