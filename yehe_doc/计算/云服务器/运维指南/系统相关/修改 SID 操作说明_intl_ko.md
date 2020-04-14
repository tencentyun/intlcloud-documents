## 작업 시나리오

보안 식별자(SID)는 컴퓨터와 사용자에 대해 Microsoft운영 체제로부터 식별됩니다. Windows 도메인 환경을 구축할 때, 동일한 미러 이미지에 기반하여 생성한 클라우드 서버의 인스턴스 SID가 같기 때문에 도메인 입력이 안 되는 문제가 발생할 수 있습니다. 이런 경우엔 SID 수정을 통해 해결할 수 있습니다.
다음은 시스템 자체의 sysprep 및 sidchg툴을 이용하여 SID를 수정하는 방법에 대해 소개합니다.

> **참고: **
> - 본 설명은 Windows Server 2008 R2,Windows Server 2012 및 Windows Server 2016에만 적용됩니다.
> - SID를 일괄 수정해야 할 경우 사용자 정의 이미지를 제작하여("sysprep 미러 이미지 제작 실행" 선택) 진행할 수 있습니다.
> - SID를 수정하면 데이터가 손실되거나 시스템이 손상될 수 있으므로 시스템 디스크 스냅샷이나 미러 이미지를 미리 준비하시길 권장합니다.

## 작업 방식

### sysprep를 사용하여 SID 수정

> **참고: **
> - sysprep를 사용하여 SID를 수정하면 IP설정 정보 등을 포함한 시스템 매개변수 대부분이 재설정되므로 반드시 수동으로 다시 설정해야 합니다.
> - sysprep를 사용하여 SID를 수정하면 C:\Users\Administrator가 초기화되고, 시스템 디스크의 일부 데이터가 삭제되므로 데이터 백업에 유의하세요.

1. 콘솔 VNC를 CVM 인스턴스에 로그인합니다. [조작 가이드(https://cloud.tencent.com/doc/product/213/2155)]를 클릭합니다.
2. 네트워크 설정을 저장합니다.
[시작]>[실행]을 클릭하고 명령어 `cmd`를 입력하여 명령어 페이지를 열고, `ipconfig /all` 명령어를 실행하면 결과 정보 기록 혹은 스크린샷이 저장됩니다.
3. sysprep툴을 엽니다.
 `C:\windows\system32\sysprep` 폴더 안의 `sysprep.exe` 프로그램을 실행합니다.
[시스템 정리 작업] **시스템 점검 (OOBE)에 접속**을 선택하여 [범용] 옵션을 선택하고 [종료 옵션]에서 **재시작**을 선택합니다.
 
4. **확인**을 클릭하면 시스템이 재시작되고, 재시작 후 안내에 따라 설정(언어 선택, 비밀번호 재설정 등)을 완료합니다.
5. SID 인증
[시작]>[실행]을 클릭하고 명령어 `cmd`를 입력하여 명령어 페이지를 열고 `whoami /user` 명령어를 실행하여 SID가 수정되었는지 확인합니다.
 ![](https://main.qcloudimg.com/raw/34efb1f4128c753e6c0546f3e8d58678.png)
6. 2단계를 참고하여 저장한 설정 정보로 게이트웨이 관련 정보 재설정(IP 주소, 게이이트웨이 주소, DNS 등)

### sidchg를 사용하여 SID 수정
1. [sidchg](http://www.stratesave.com/html/sidchg.html) 툴 다운로드
2. sidchg64-2.0n.exe /R. 명령어를 실행한 후 표시되는 메시지에 따라 Trial key 또는 license를 입력하고 엔터를 누릅니다. sidchg 의 시작 옵션 중 /R은 수정 후 재시작을 의미하고, /S는 수정 후 닫기를 의미합니다. 더 자세한 사용 방법은 [공식 매뉴얼](http://www.stratesave.com/html/sidchg.html)을 참고하시기 바랍니다.
Tip: sidchg64-2.0n.exe는 64 비트 버전입니다.
 ![](https://main.qcloudimg.com/raw/18884c02b7775a138e5fc1d45eddf3a9.png)
3. SID를 수정하면 데이터가 손실되거나 시스템이 훼손될 수 있습니다. 계속하겠습니까? 라는 메시지가 뜨면, Y를 입력하고 엔터를 눌러 설정을 진행합니다.
 ![](https://main.qcloudimg.com/raw/2ddf9c5f9a66703ac1a20f3eaeb94ed6.png)
4. 확인을 클릭하면 SID 재설정이 진행되고 시스템이 재시작 됩니다.
![](https://main.qcloudimg.com/raw/b59ec21417cc0de1fd7d851fcd8a2a3b.png)
5. SID 인증, 시스템 재시작 완료 후 다시 로그인합니다.
[시작]>[실행]을 클릭하고 명령어 `cmd`를 입력하여 명령어 페이지를 열고 `whoami /user` 명령어를 실행하여 SID가 수정되었는지 확인합니다.
 ![](https://main.qcloudimg.com/raw/34efb1f4128c753e6c0546f3e8d58678.png)
