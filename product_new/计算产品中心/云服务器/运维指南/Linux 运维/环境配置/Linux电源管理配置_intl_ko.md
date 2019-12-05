## 작업 시나리오

x86 기기에는 **APM**(Advanced Power Management, 고급 전원 관리)와 **ACPI**(Advanced Configuration and Power Interface, 고급 사양 및 전원 인터페이스)라는 두 가지 전원 관리가 있습니다. ACPI는 Intel, Microsoft 및 Toshiba가 공동으로 개발한 일종의 전원 관리 표준으로 컴퓨터와 장치를 관리하는데 보다 유연한 인터페이스를 제공하는 반면 APM은 전원 관리의 기존 표준입니다.
Linux는 APM 및 ACPI를 지원하지만, 이 두 표준을 동시에 실행할 수는 없습니다. 디폴트의 경우, Linux는 기본적으로 ACPI를 실행합니다. 동시에 Tencent Cloud에서도 ACPI 전원 관리 방법을 사용하는 것을 권장합니다.
Linux 시스템에 ACPI 관리 프로그램이 설치되어 있지 않은 경우, 소프트 리부팅에 실패합니다. 본 문서는 ACPI 설치 상황과 설치 작업에 대해 설명합니다.

## 설치 설명

CoreOS 시스템의 경우 ACPI를 설치할 필요가 없습니다.

## 작업 순서
 
1. 다음 커맨드를 실행하여 ACPI가 설치되었는지 확인하십시오.
```
ps -ef|grep -w "acpid"|grep -v "grep"
```
 - 프로세스가 없으면 ACPI가 설치되지 않았음을 의미하므로 다음 단계로 이동하십시오.
 - 프로세스가 있으면 ACPI가 설치되었음을 의미하므로 작업이 완료된 것 입니다.
2. 운영 시스템 유형에 따라 ACPI를 설치하고 다른 커맨드를 실행하십시오.
 - Ubuntu / Debian 시스템에서 다음 커맨드를 실행하십시오.
```
sudo apt-get install acpid
```
 - Redhat / CentOS 시스템에서 다음 커맨드를 실행하십시오.
```
yum install acpid
```
 - SUSE 시스템에서 다음 커맨드를 실행하십시오.
```
in apcid
```
