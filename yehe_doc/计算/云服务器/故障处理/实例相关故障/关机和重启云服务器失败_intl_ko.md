CVM 종료, 재시작 작업 시 매우 낮은 확률로 종료 실패 또는 재시작 실패의 문제가 발생할 수 있습니다. 이러한 문제가 발생하면 CVM에서 아래와 같이 진단 및 처리할 수 있습니다.

## 예상 원인

- CPU 또는 메모리 사용률이 지나치게 높을 수 있습니다.
- Linux 운영 체제의 CVM에 ACPI 관리 프로그램이 설치되어 있지 않을 수 있습니다.
- Windows 운영 체제의 CVM에서 시스템 업데이트 시간이 너무 길 경우 문제가 발생할 수 있습니다.
- 처음 Windows CVM을 구매했을 때, 해당 CVM의 초기화가 미완료 상태일 수 있습니다.
- 운영 체제에서 일부 소프트웨어를 설치하고 있거나 트로이 목마 바이러스에 감염되어 시스템 자체가 손상되었을 수 있습니다.

## 장애 처리

### CPU/메모리의 사용 현황 확인

1. CVM 운영 체제의 유형에 따라 CPU/메모리의 사용 현황을 확인합니다.
 - Windows CVM: CVM에서 마우스 우클릭하여 '작업 표시줄'의 [작업 관리자]를 선택합니다.
 - Linux CVM: `top` 명령어를 실행하여 `%CPU` 열과 `%MEM` 열의 정보를 확인합니다.
2. 실제 CPU/메모리 사용량에 따라 CPU 또는 메모리 사용량이 지나치게 높은 프로세스를 종료합니다.
그래도 종료/재시작 할 수 없다면 [강제 종료/재시작 기능](#MandatoryShutdownOrRestart)을 실행하시기 바랍니다.

### ACPI 관리 프로그램 설치 여부 확인
> 해당 작업은 Linux 운영 체제의 CVM을 대상으로 합니다.
>
다음 명령어를 실행하여 ACPI 프로세스가 존재하는지 확인합니다.
```
ps -ef | grep -w "acpid" | grep -v "grep"
```
 -  ACPI 프로세스가 존재한다면 [강제 종료/재시작 기능](#MandatoryShutdownOrRestart)을 실행하시기 바랍니다.
 -  ACPI 프로세스가 존재하지 않는다면 ACPI 관리 프로그램을 설치하시기 바랍니다. 자세한 작업 내용은 [Linux 전원 관리 구성](https://intl.cloud.tencent.com/document/product/213/2129)을 참조 바랍니다.


### WindowsUpdate 진행 여부 확인
> 해당 작업은 Windows 운영 체제의 CVM을 대상으로 합니다.
>
Windows CVM 운영 체제 인터페이스에서 [시작]> [제어판]> [Windows 업데이트]를 클릭하여 현재 업데이트 중인 패치 또는 프로그램이 존재하는지 확인합니다.
- Windows가 일부 패치 작업 중에 시스템을 종료할 때 일부 프로세스를 수행합니다. 이 때, 업데이트 시간이 너무 길면 종료/재시작에 실패할 수 있습니다. Windows 업데이트 완료를 기다린 후 다시 CVM의 작업을 종료/재시작 하길 권장합니다.
- 업데이트 중인 패치 또는 프로그램이 없다면, [강제 종료/재시작 기능](#MandatoryShutdownOrRestart)을 실행하시기 바랍니다.


### CVM의 초기화 완료 여부 확인
> 해당 작업은 Windows 운영 체제의 CVM을 대상으로 합니다.
>
처음 Windows CVM을 구매했을 때, 시스템이 Sysprep 방식을 통해 이미지를 전송하기 때문에 초기화 과정에서 비교적 오랜 시간이 소요됩니다. 초기화가 완료되기 전까지 Windows에서 종료/재시작 작업을 생략하므로 작업에 실패할 수 있습니다.
- 구매한 Windows CVM이 초기화 중이라면, Windows CVM 초기화가 완료될 때까지 기다린 다음, CVM 작업 종료/재시작을 다시 시도하시길 권장합니다.
- CVM이 이미 초기화를 완료했다면 [강제 종료/재시작 기능](#MandatoryShutdownOrRestart)을 실행하시기 바랍니다.

### 소프트웨어 정상 설치 여부 확인
 
검사 툴 또는 바이러스 백신 소프트웨어를 통해 CVM에 설치된 소프트웨어가 정상적인지, 트로이 목마 등 바이러스에 감염되었는지 등을 확인합니다.
- 이상이 발견되면 시스템 자체가 손상되어 종료/재시작에 실패한 것일 수 있습니다. 해당 소프트웨어를 제거하고 보안 소프트웨어를 사용하여 바이러스 검출 또는 데이터 백업 후 시스템 재설치를 권장합니다.
- 이상이 발견되지 않으면 [강제 종료/재시작 기능](#MandatoryShutdownOrRestart)을 실행하시기 바랍니다.

<span id="MandatoryShutdownOrRestart"></span>
### 강제 종료/재시작 기능

> Tencent Cloud는 CVM 종료/재시작에 여러 번 실패했을 때 사용할 수 있도록 강제 종료/재시작 기능을 제공하고 있습니다. 이 작업은 CVM을 강제로 **종료/재시작**하기 때문에, CVM 데이터 손실 또는 파일 시스템 손실을 일으킬 수 있습니다.
>
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 인스턴스 관리 페이지에서 종료 또는 재시작 대기 중인 CVM을 선택하고 실제 수요에 맞는 작업을 진행합니다.
 - CVM 종료: [More]> [Instance Status]> [Shutdown]을 클릭합니다.
 - CVM 재시작: [More]> [Instance Status]> [Restart]를 클릭합니다.
3. 팝업된 'Shutdown' 또는 'Restart Instance' 창에서 [Forced Shutdown] 또는 [Forced Restart]를 체크하고 [확인]을 클릭합니다.
 - 아래 이미지와 같이 [Forced Shutdown]에 체크합니다.
 ![](https://main.qcloudimg.com/raw/22db326eebab11c60e6bbcf8baa23144.png)
 - 아래 이미지와 같이 [Forced Restart]에 체크합니다.
 ![](https://main.qcloudimg.com/raw/61ae4a4185110b7ff86507e15047211f.png)
