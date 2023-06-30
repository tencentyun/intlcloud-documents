Tencent Cloud 서버는 KMS 방법을 사용해 Windows 서버에 권한을 부여합니다.

<dx-alert infotype="notice" title="">

- 본 문서는 Tencent Cloud에서 제공하는 Windows Server 공용 이미지에만 해당됩니다. 사용자 정의 이미지 또는 외부 소스에서 가져온 이미지에는 적용되지 않습니다.
- Windows Server 2008 및 Windows Server 2012는 이 방법을 사용하여 인증해야 합니다. Windows Server 2016 및 Windows Server 2019의 공용 이미지에 대해 설정된 기본 KMS 주소(kms.tencentyun.com:1668)는 올바르며 수정할 필요가 없습니다.
  </dx-alert>



## 활성화 전 숙지 사항

1. 정품 인증에는 **Windows Server 2008**의 SPP Notification Service가 사용됩니다. 다음 이미지와 같이 제대로 실행되는지 확인합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/40c2d2a0895902917c5ca419e43905fc.png)
2. 일부 최적화 소프트웨어는 서비스 관련 실행 프로그램의 실행 권한을 수정 금지할 수 있습니다. 예를 들어 아래 이미지와 같이, sppsvc.exe 프로세스의 실행 권한이 수정되면 서비스가 정상적으로 실행되지 않을 수 있습니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b45ca678ce7615c53a053d1d36ef78bc.png)
   Windows 클라우드 서버를 활성화하기 전에 이 서비스 및 기타 기본 기능이 Windows에서 올바르게 작동하는지 확인하십시오.

## 자동 활성화

Tencent Cloud는 Windows 서버의 활성화를 하나의 스크립트로 캡슐화하여, 수동 활성화의 절차를 간소화했습니다. 아래의 과정을 참조하여 스크립트를 활성화하시기 바랍니다.

1. Windows CVM에 로그인합니다.
2. [스크립트](https://iso-1251783334.cos.ap-guangzhou.myqcloud.com/scripts/activate-win.bat)를 다운로드 및 실행하면 자동으로 활성화됩니다.

## 수동 실행 활성화

### 주의 사항

일부 시스템에서 시스템 시계에 문제가 있으면 수동으로 활성화할 때 오류가 발생할 수 있습니다. 이때, 시스템 시계를 동기화해야 합니다. 시계 동기화 작업 순서는 다음과 같습니다.
<dx-alert infotype="explain" title="">
Windows CVM의 시스템 시간이 정상일 경우 바로 [활성화](#ActivationStep)를 진행하시기 바랍니다.
</dx-alert>

1. Windows CVM에 로그인합니다.
2. 바탕 화면에서 **시작** > **실행**을 선택합니다. 실행 대화 상자에 `cmd.exe`를 입력한 다음 콘솔 창을 엽니다.
3. 콘솔 창에서 다음 명령을 순서대로 실행하여 시스템 시계를 동기화합니다.
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm /resync
```

### 활성화[](id:ActivationStep)

1. Windows CVM에 로그인합니다.
2. 바탕 화면에서 **시작** > **실행**을 선택합니다. 실행 대화 상자에 `cmd.exe`를 입력한 다음 콘솔 창을 엽니다.
3. 콘솔 창에서 다음 명령을 순차적으로 실행하여 수동 활성화를 완료합니다.
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```
