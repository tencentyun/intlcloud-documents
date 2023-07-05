Tencent Cloud의 CVM은 KMS 방식을 사용해 Windows 서버에 권한을 부여합니다.
>! 
> - 본 문서의 내용은 Tencent Cloud에서 제공하는 Windows Server 공용 이미지에만 해당합니다. 사용자 정의 이미지 및 외부에서 가져온 이미지는 본 문서의 활성화 방식을 사용할 수 없습니다.
> - Windows Server 2008 및 Windows Server 2012에서는 이런 방식의 권한 부여가 필요하지만, Windows Server 2016 및 Windows Server 2019의 공용 이미지에 기본 설정된 KMS 주소(kms.tencentyun.com:1668)가 정확하므로 수정할 필요가 없습니다.


## 활성화 전 숙지 사항
1. **Windows Server 2008**의 SPP Notification Service는 활성화 관련 서비스에 사용되므로, 아래 이미지와 같이 정상적으로 실행되어야 합니다.
![](https://main.qcloudimg.com/raw/f84f7bd86fae0df1c2394cdc554b6a98.png)
2. 일부 최적화 소프트웨어는 서비스 관련 실행 프로그램의 실행 권한을 수정 금지할 수 있습니다. 예를 들어 아래 이미지와 같이, sppsvc.exe 프로세스의 실행 권한이 수정되면 서비스가 정상적으로 실행되지 않을 수 있습니다.
![](https://main.qcloudimg.com/raw/c1ad23337b0f1b6e186d0c6e50c9e1b5.png)
Windows CVM을 활성화하기 전에, Windows에서 해당 서비스 및 기타 기본 기능이 정상적으로 작동하는지 확인하시기 바랍니다.
 
## 자동 활성화
Tencent Cloud는 Windows 서버의 활성화를 하나의 스크립트로 캡슐화하여, 수동 활성화의 절차를 간소화했습니다. 아래의 과정을 참조하여 스크립트를 활성화하시기 바랍니다.
1. Windows CVM에 로그인합니다.
2. [스크립트](https://iso-1251783334.cos.ap-guangzhou.myqcloud.com/scripts/activate-win.bat)를 다운로드 및 실행하면 자동으로 활성화됩니다.


## 수동 활성화

### 주의 사항
일부 시스템에서는 시스템 시간에 문제가 있으면 수동 활성화에 오류가 발생할 수 있습니다. 이런 경우 시스템 시간을 동기화해야 하며, 시간 동기화 작업 순서는 다음과 같습니다.
>? Windows CVM의 시스템 시간이 정상일 경우 바로 [활성화 순서](# ActivationStep)를 진행하시기 바랍니다.
>
1. Windows CVM에 로그인합니다.
2. 운영 체제 인터페이스에서 [시작]>[실행]을 클릭하고 `cmd.exe`를 입력하여 콘솔 창을 엽니다.
3. 콘솔 창에서 다음 명령어를 순서대로 실행하여 시스템 시간을 동기화합니다.
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm /resync
```

<span id="ActivationStep"></span>
### 활성화 순서

1. Windows CVM에 로그인합니다.
2. 운영 체제 인터페이스에서 [시작]>[실행]을 클릭하고 `cmd.exe`를 입력하여 콘솔 창을 엽니다.
3. 콘솔 창에서 다음 명령어를 순서대로 실행하여 수동으로 활성화합니다.
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```





