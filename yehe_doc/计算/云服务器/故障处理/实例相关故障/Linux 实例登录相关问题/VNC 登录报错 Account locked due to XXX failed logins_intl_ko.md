## 현상 설명
VNC로 CVM에 정상적으로 로그인할 수 없는 경우, 로그인 비밀번호를 입력하기 전에 ‘Account locked due to XXX failed logins’라는 오류 메시지가 나타납니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/0dcc0c3b62a36ba0f269e629a3365564.png)

## 예상 원인
VNC로 로그인하면 `/etc/pam.d/login`이라는 pam 모듈을 호출해 인증을 진행하고 login 구성 파일에 `pam_tally2.so` 모듈의 인증이 구성됩니다. `pam_tally2.so` 모듈의 기능은 Linux 사용자가 로그인 비밀번호를 N번 잘못 입력했을 때 자동으로 X분 동안 또는 영구적으로 잠금되도록 설정하는 것입니다. 그중 영구 잠금은 수동으로 암호를 해제해야 하며, 해제 전까지 잠금 상태가 유지됩니다.

로그인 실패 횟수가 설정 횟수를 초과하여 계정이 일정 시간동안 잠기거나, 무차별 대입 공격으로 계정이 잠기는 경우 로그인할 수 없습니다. 다음 이미지는 설정된 로그인 시도 가능 횟수입니다.
![](https://main.qcloudimg.com/raw/806c1d8ccded0746f5457320df479177.png)
`pam_tally2` 모듈 매개변수에 관한 설명은 다음 표를 참조하십시오.
<table>
<tr>
<th> 매개변수</th><th>설명</th>
</tr>
<tr>
<td><code>deny=n</code></td>
<td> 로그인 실패 횟수가 n회 이상이면 액세스가 거부됩니다. </td>
</tr>
<tr>
<td><code>lock_time=n </code></td>
<td>로그인 실패 후 계정 잠금 시간(초)입니다. </td>
</tr>
<tr>
<td><code>un lock_time=n</code></td>
<td>로그인 실패 제한 횟수 초과 후 잠금 해제에 필요한 시간입니다. </td>
</tr>
<tr>
<td><code>no_lock_time </code></td>
<td>로그 파일<code>/var/log/faillog</code>에<code>.fail_locktime</code>필드를 기록하지 마십시오. </td>
</tr>
<tr>
<td><code>magic_root   </code></td>
<td>root 사용자가(uid=0) 해당 모듈을 호출하면 카운터가 늘어나지 않습니다. </td>
</tr>
<tr>
<td><code>even_deny_root </code></td>
<td> root 사용자의 로그인 실패 횟수가 deny=n회 이상이면 액세스가 거부됩니다. </td>
</tr>
<tr>
<td><code>root_unlock_time=n  </code></td>
<td><code>even_deny_root</code>에 상응하는 옵션입니다. 해당 옵션 설정 시, root 사용자의 로그인 실패 횟수가 제한 횟수를 초과했을 때 잠기는 시간. </td>
</tr>
</table>

## 해결 방법
1. [작업 순서](#ProcessingSteps)를 참조해 login 설정 파일에서 `pam_limits.so` 모듈 설정을 임시 주석 처리 합니다.
2. 계정이 잠긴 원인을 확인하고 보안 정책을 강화합니다.

[](id:ProcessingSteps)

## 작업 순서

1. SSH를 사용하여 CVM에 로그인합니다. 자세한 내용은 [SSH를 사용해 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)을 참조하십시오.
	- 로그인에 성공하면 다음 단계를 실행합니다.
	- 로그인에 실패하면 단독 사용자 모드를 사용해야 합니다.
2. 로그인 성공 후 다음 명령어를 실행하여 로그 정보를 조회하십시오.
```
vim /var/log/secure
```
이 파일은 일반적으로 보안 관련 정보 기록에 사용되며, 대부분은 사용자의 CVM 로그인 관련 로그입니다. 다음 이미지와 같이 정보 중에서 `pam_tally2`가 있는 오류 보고 정보를 가져올 수 있습니다.
![](https://main.qcloudimg.com/raw/f45fb4564cfea44f0210a6e9b7124b73.png)
3. 다음 명령어를 차례대로 실행하여 `/etc/pam.d`로 들어간 뒤, 로그에서 오류 보고 pam 모듈의 키워드 `pam_tally2`를 검색합니다.
```
cd /etc/pam.d
```
```
find . | xargs grep -ri "pam_tally2" -l
```
다음 이미지와 같은 정보가 반환되면 `login` 파일에 해당 파라미터가 설정되었음을 의미합니다.
![](https://main.qcloudimg.com/raw/a5d272e11a88d4f9cee347244fb98441.png)
4. 다음 명령어를 실행하여 `pam_tally2.so` 모듈 설정을 임시 주석 처리합니다. 설정이 완료되면 다시 로그인이 가능합니다.
```
sed -i "s/.*pam_tally.*/#&/" /etc/pam.d/login
```
4. 계정 잠김이 사용자의 조작 오류 때문인지 무차별 대입 공격 때문인지 확인합니다. 무차별 대입 공격이 원인인 경우 다음과 같은 방법으로 보안 정책을 강화하시기 바랍니다.
 - CVM 비밀번호를 수정합니다. 비밀번호는 대문자, 소문자, 특수 부호, 숫자로 구성된 12-16자리의 복잡하고 임의적인 비밀번호로 설정하십시오. 자세한 내용은 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조하십시오.
 - CVM에서 사용하지 않는 사용자를 삭제합니다.
 - sshd의 기본 포트 22를 1024-65525 사이의 자주 사용하지 않는 포트로 변경합니다. 자세한 방식은 [CVM 원격 기본 포트 수정](https://intl.cloud.tencent.com/document/product/213/35376)을 참조하십시오.
 - CVM과 연결된 보안 그룹의 규칙을 관리하기 위해서는 서비스와 프로토콜에 필요한 포트만 개방하면 되며, 모든 프로토콜과 포트를 개방하는 것은 권장하지 않습니다. 자세한 내용은 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참조하십시오.
 - 공용 네트워크에 핵심 애플리케이션 서비스 포트의 액세스를 개방하는 것은 권장하지 않습니다. 예시: mysql, redis 등 관련 포트를 로컬 액세스 또는 공인 네트워크 액세스 금지로 변경할 수 있습니다.
 - HS, yunsuo 등 보안 소프트웨어를 설치하고 실시간 알람을 추가하여 비정상적인 로그인 정보를 즉각적으로 수집할 수 있습니다.


