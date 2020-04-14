Tencent Cloud의 CVM은 KMS 방식을 사용해 Windows 서버에 인증 권한을 부여합니다.
> 
> - 본 문서는 Tencent Cloud에서 제공하는 Windows Server 공용 이미지만 지원합니다. 사용자 정의 이미지 또는 미러 이미지 가져오기로는 본 문서의 활성화 방법을 사용할 수 없습니다.
> - Windows Server 2008 및 Windows Server 2012에서 해당 방식을 사용하려면 라이선스 권한을 부여해야 합니다. Windows Server 2016의 공용 이미지에 기본으로 설정된 KMS 주소(kms.tencentyun.com:1668)가 정확하므로 수정할 필요가 없습니다.


## 활성화 전 준수 사항
1. Windows의 SPP Notification Service는 활성화 관련 서비스를 실행하는 데 사용되므로 정상 가동을 유지해야 합니다.
2. 일부 최적화 프로그램에서는 서비스 관련 실행 프로그램의 실행 권한을 수정하지 못할 가능성이 있습니다. 예: sppsvc.exe 프로세스의 실행 권한이 수정되면 서비스가 제대로 실행되지 않는 문제가 발생할 수 있습니다.
Windows CVM을 활성화하기 전에, 해당 서비스 및 기타 기본 기능이 Windows에서 제대로 실행되는지 확인합니다.
 
## 자동 활성화
Tencent Cloud는 Windows 서버 활성화를 위한 스크립트를 캡슐화하여 수동 활성화 단계를 간소화했습니다.
1. Windows CVM에 로그인합니다.
2. 브라우저에서 'http://mirrors.tencentyun.com/install/windows/activate-win.bat'에 액세스하여 스크립트를 다운로드합니다.
3. 스크립트를 실행하여 자동 활성화를 완료합니다.

## 수동 활성화

### 주의 사항
일부 시스템에서 시스템 시계에 문제가 있을 경우, 수동 활성화 과정에 오류가 발생할 수 있습니다. 이런 경우엔 시스템 시계를 동기화 해야 하며, 동기화 순서는 다음과 같습니다.
> Windows CVM의 시스템 시계가 정상이면 직접 [활성화 단계](#ActivationStep)를 진행합니다.
>
1. Windows CVM에 로그인합니다.
2. 운영 체제 인터페이스에서 [시작] > [실행]을 클릭하고 `cmd.exe`를 입력한 다음 콘솔 창을 엽니다.
3. 콘솔 창에서 다음 명령어를 차례대로 실행하여 시스템 시계를 동기화 합니다.
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm /resync
```

<span id="ActivationStep"></span>
### 활성화 순서

1. Windows CVM에 로그인합니다.
2. 운영 체제 인터페이스에서 [시작] > [실행]을 클릭하고 `cmd.exe`를 입력한 다음 콘솔 창을 엽니다.
3. 콘솔 창에서 다음 명령어를 차례대로 실행하여 수동 활성화를 완료합니다.
 - Windows Server 2008과 Windows Server 2012 서버에서 다음과 같이 명령어를 차례대로 실행합니다.
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```
 - Windows Server 2016 서버에서 다음과 같이 명령어를 차례대로 실행합니다.
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms1.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```




