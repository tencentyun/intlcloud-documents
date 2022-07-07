## 작업 시나리오
본문은 문제를 해결하고 분석하는 데 도움이 되는 CVM 인스턴스의 사용자 로그인 기록을 얻는 방법을 설명합니다.


## 작업 단계

<dx-tabs>
::: Linux 인스턴스
<dx-alert infotype="explain" title="">
본문은 TencentOS Server 3.1(TK4)의 Linux 인스턴스를 예로 사용합니다. 운영 체제에 따라 단계가 다를 수 있으므로 실제 상황에 따라 진행하십시오.
</dx-alert>

1. [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436).
2. 필요에 따라 다음 사용자 로그인 정보를 볼 수 있습니다.
<dx-alert infotype="explain" title="">
사용자 로그인 로그는 일반적으로 `/var/run/utmp`, `/var/log/wtmp`, `/var/log/btmp` 및 `/var/log/lastlog` 파일에 저장됩니다.
</dx-alert>
 - `/var/run/utmp` 파일에서 현재 로그인한 사용자의 정보를 보려면 `who` 명령을 실행합니다. 반환된 결과는 다음과 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/2f54911fac9ee5cbeb2ca180a802f8bc.png"/>
 - `w` 명령을 실행하여 현재 로그인한 사용자의 사용자 이름을 보고 `/var/run/utmp` 파일에 사용자의 현재 실행 중인 작업을 표시합니다. 반환된 결과는 다음과 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/401681d683aafd6cd6ab0f5ffda15cd8.png)
 - `users` 명령을 실행하여 `/var/run/utmp` 파일에서 현재 로그인한 사용자의 사용자 이름을 봅니다. 반환된 결과는 다음과 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/94f318f2bfa670fae34a0a0015f7587d.png)
 - `/var/log/wtmp` 파일에서 현재 및 과거에 로그인한 사용자의 정보를 보려면 `last` 명령을 실행합니다. 반환된 결과는 다음과 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1262a858b41be61a01d2d31e09c2cc70.png)
 - `/var/log/btmp` 파일에서 시스템 로그인에 실패한 모든 사용자의 정보를 보려면 `lastb` 명령을 실행합니다. 반환된 결과는 다음과 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2208f07aba6e73fa4de6959844d38ca5.png)
 - `/var/log/lastlog` 파일에서 마지막 사용자 로그인 정보를 보려면 `lastlog` 명령을 실행합니다. 반환된 결과는 다음과 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/85e42c825afa0bab0e1b25e18895ac52.png)
 - `cat /var/log/secure` 명령을 실행하여 로그인 정보를 봅니다. 반환된 결과는 다음과 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d75c5db721f325d56ed0ba7dd4a20c7b.png)

:::
::: Windows 인스턴스

<dx-alert infotype="explain" title="">
본문은 Windows Server 2012 R2 English의 Windows 인스턴스를 예로 사용합니다. 운영 체제에 따라 단계가 다를 수 있으므로 실제 상황에 따라 진행하십시오.
</dx-alert>


1.  [표준 로그인 방식으로 Windows 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/41018).
2.  바탕 화면에서 <img src="https://main.qcloudimg.com/raw/446c1e8cb7da2ce280d710c6a46b693d.png" style="margin:-6px 0px">을(를) 클릭하여 서버 관리자를 엽니다.
3.  ‘서버 관리자’ 창에서 오른쪽 상단의 **도구** > **이벤트 뷰어**를 선택합니다.
4.  ‘이벤트 뷰어’ 팝업 창에서 왼쪽의 **Windows 로그** > **보안**을 선택하고 오른쪽의 **현재 로그 필터링**을 클릭합니다.
5.  ‘현재 로그 필터링’ 팝업 창에서 ‘<모든 이벤트 ID>’에 `4648`을 입력하고 **확인**을 클릭합니다.
6.  ‘이벤트 뷰어’ 창에서 필터에 맞는 로그를 더블 클릭합니다.
7.  ‘이벤트 속성’ 팝업 창에서 **자세히**를 클릭하면 클라이언트 이름과 주소, 이벤트 녹화 시간을 확인할 수 있습니다.



:::
</dx-tabs>



