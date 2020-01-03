Tencent Cloud 서버는 KMS 방법을 사용해 Windows 서버에 권한을 부여합니다.
> 
>- 본 문서는 Tencent Cloud에서 제공하는 Windows Server 공용 미러 이미지에만 해당됩니다. 사용자 정의 이미지 또는 외부 가져오기 이미지는 본 문서의 활성화 방법으로 사용할 수 없습니다.
>- Windows Server 2008 및 Windows Server 2012에서는 이러한 방법의 권한 부여가 필요합니다. Windows Server 2016 공용 미러 이미지에 기본적으로 구성된 KMS 주소(kms.tencentyun.com:1668)는 정확하며 수정할 필요가 없습니다.


## 활성화 전 숙지 사항
1. Windows의 SPP Notification Service는 활성화와 관련된 서비스를 실행하기 위해 사용되며, 정상적으로 실행되도록 보장해야 합니다. 아래 이미지를 참조하십시오.
2. 일부 최적화 소프트웨어는 서비스 관련 실행 프로그램 수정의 실행 권한을 비활성화 할 수 있습니다. 예를 들어 sppsvc.exe 프로세스의 실행 권한이 수정된 경우 서비스가 제대로 실행되지 않을 수 있습니다.
Windows 클라우드 서버를 활성화하기 전에 이 서비스 및 기타 기본 기능이 Windows에서 올바르게 작동하는지 확인하십시오.

## 자동 활성화
Tencent Cloud는 Windows 서버 활성화를 위한 스크립트를 캡슐화하여 수동 활성화 단계를 단순화합니다.
1. Windows 클라우드 서버에 로그인하십시오.
2. 브라우저 주소에서 'http://mirrors.tencentyun.com/install/windows/activate-win.bat'를 접근하여 스크립트를 다운로드하십시오.
3. 스크립트를 실행하여 자동 활성화를 완료하십시오.

## 수동 실행 활성화

### 주의사항
일부 시스템에서 시스템 시계에 문제가 있으면 수동으로 활성화할 때 오류가 발생할 수 있습니다. 이때, 시스템 시계를 동기화해야 합니다. 시계 동기화 작업 순서는 다음과 같습니다.
> Windows 클라우드 서버의 시스템 시계가 정상이면 직접 [활성화 단계](# ActivationStep)를 진행하십시오.
>
1. Windows 클라우드 서버에 로그인하십시오.
2. 운영 체제 인터페이스에서 [시작]> [실행]을 클릭하고 `cmd.exe`를 입력한 다음 콘솔 창을 엽니다.
3. 콘솔 창에서 다음 커맨드를 실행하여 시스템 시계를 동기화하십시오.
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm /resync
```

<span id="ActivationStep"></span>
### 활성화 순서

1. Windows 클라우드 서버에 로그인하십시오.
2. 운영 체제 인터페이스에서 [시작]> [실행]을 클릭하고 `cmd.exe`를 입력한 다음 콘솔 창을 엽니다.
3. 콘솔 창에서 다음 커맨드를 실행하여 수동 실행 활성화를 수행하십시오.
 Windows Server 2008과 Windows Server 2012 서버가 순서대로 실행하는 커맨드는 다음과 같습니다.
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```
 Windows Server 2016 서버가 순서대로 실행하는 커맨드는 다음과 같습니다.
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms1.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```




