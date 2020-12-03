
Tencent Linux(Tlinux)는 Tencent에서 클라우드 시나리오를 목적으로 연구 개발한 Linux 운영 체제입니다. 전문적인 기능 특징 및 성능 최적화를 제공하며 CVM 인스턴스의 응용 프로그램에 대해 높은 성능과 안전하고 믿을 수 있는 실행 환경을 제공합니다. Tencent Linux는 무료로 제공되며 CentOS(또는 릴리스 버전)에서 개발된 응용 프로그램을 Tencent Linux에서 직접 실행할 수 있을 뿐 아니라, 사용자는 Tencent Cloud를 통해 지속적인 업데이트 점검 및 기술 지원을 받을 수 있습니다.

## 사용 설명
Tencent Linux는 다음과 같은 시나리오에 적용할 수 있습니다.
- CVM 각 사양군 대부분 유형의 인스턴스.
- 인스턴스 실행 시 동적 설정을 진행하기 위해, 사용자 데이터(즉 userdata 방식)를 통해 관련 작업을 Cloud-init에 전달해야 합니다.

## 주요 특징

<table>
	<tr><th>특징 유형</th><th>특징 내용</th></tr>
	<tr><td><b>커널 사용자 정의</b></td><td>커널 커뮤니티에서 장기간 지원 중인 4.14.105 버전을 기반으로 만든 사용자 정의 버전으로, 클라우드 시나리오에 새로운 특징을 추가하고 커널 성능을 개선하며 주요 결함을 수정하였습니다</td></tr>
	<tr><td><b>컨테이너 지원</b></td><td>컨테이너 시나리오에 맞춘 최적화를 통해 격리 향상 및 성능 최적화 기능을 제공합니다. <ul style="margin: 0;"><li>meminfo, vmstat, cpuinfo, stat, loadavg 등 격리</li><li>tcp_no_delay_ack, tcp_max_orphans와 같은 Sysctl 격리</li><li>대량의 파일 시스템 및 네트워크의 BUGFIX</li></ul></td></tr>
	<tr><td><b>성능 최적화</b></td><td>컴퓨팅, 스토리지 및 네트워크 서브시스템 모두 최적화하였습니다.<ul style="margin: 0;"><li>xfs 메모리 할당을 최적화하여 xfs kmem_alloc 할당 실패 알람을 해결합니다</li><li>수신된 네트워크 패킷의 대용량 메모리 할당을 최적화하여, 많은 양의 UDP 패킷이 수신될 때 과도한 메모리 사용 문제를 해결합니다</li><li>시스템 page cache의 메모리 사용량을 제한하여 비즈니스 성능 또는 OOM에 영향을 끼칠 수 있는 메모리 부족을 방지합니다</li></ul></td></tr>
	<tr><td><b>소프트웨어 패키지</b></td><td><ul style="margin: 0;"><li>CentOS 7 버전의 소프트웨어 패키지를 기반으로 사용자 정의 패키지를 생성합니다</li><li>사용자 모드 소프트웨어 패키지가 CentOS 7 버전과 호환된다면, 사용자 모드 소프트웨어 패키지를 Tencent Linux 환경에 직접 연결하여 사용할 수 있습니다</li><li>YUM을 사용하여 소프트웨어 패키지를 업데이트 및 설치합니다</li><li>YUM을 통해 epel-release 패키지를 설치한 후에는 epel 저장소의 소프트웨어 패키지를 사용할 수 있습니다</li></ul></td></tr>
	<tr><td><b>결함 지원</b></td><td><ul style="margin: 0;"><li>운영 체제가 크래쉬된 후의 kdump 커널 덤프 기능을 제공합니다</li><li>커널의 핫픽스(Hotfix) 업그레이드 기능을 제공합니다</li></ul></td></tr>
	<tr><td><b>보안 업데이트</b></td><td>Tencent Linux는 정기적인 업데이트를 통해 보안성 및 기능을 향상합니다</td></tr>
</table>

## Tencent Linux 2.4 환경 설명
### 사용자 모드 환경
사용자 모드 소프트웨어 패키지가 최신 버전의 CentOS 7과 호환되면, CentOS 7 버전을 Tencent Linux 2.4에서 직접 연결하여 사용할 수 있습니다.

### 시스템 서비스 및 최적화 설정
#### 시스템 서비스
- `tlinux-irqaffinity`: Tencent Linux가 할당 서비스를 자동 중단합니다.
- `tlinux-bootlocal`: Tencent Linux bootlocal 서비스로서, 시작 시 `/etc/rc.d/boot.local`을 자동 실행합니다.

#### 시스템 툴
`tencent-tools`: tos(t) 명령어로 시스템을 관리하며, 지원하는 매개변수는 다음과 같습니다.
```bash
tos version 2.2
Usage:
	tos TencentOS Server System Management Toolset
	tos -u|-U| update [rpm_name]	Update the system 
	tos -i|-I| install rpm_name	install rpms
	tos -s|-S| show			Show the system version
	tos -c|-C| check [rpm_name]	Check the modified rpms
	tos -f yum | fix yum		Fix yum problems
	tos -f dns | fix dns		Fix DNS problems
	tos -a|-A | analyze		Analyze the system performance 
	tos set dns			Set DNS
	tos set irq			Set irqaffinity, restart irqaffinity service
	tos -cu| check-update		Check available package updates
	tos -b|-B| backup [ reboot ]	Backup the system online, or reboot to backup 
	tos -r|-R| recover|reinstall	Recover or Reinstall the system
	tos -h|-H| help			Show this usage
	tos -v|-V| version		Show the script version
```

#### 시스템 설정
- **pam**: 비밀번호 복잡도 향상.
- **`/etc/bashrc` 수정**: bash 프롬프트 최적화.
- **`/etc/hosts`**: TENCENT64 및 TENCENT64.site 추가.
- **`/root/.bashrc`**: 최적화 설정.

#### Tencent Linux 2.4 커널
longterm 4.14 버전의 커널을 기반으로 하며, 자세한 내용은 [TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel)을 참조 바랍니다.


## Tlinux 다운로드
다음의 방법을 통해 Tencent Linux를 다운로드 및 사용할 수 있습니다.
- CVM 인스턴스 생성 시 공용 이미지를 선택하고, 상응하는 Tencent Linux 버전을 선택합니다.
작업에 대한 자세한 내용은 [인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참조 바랍니다.
- 이미 생성된 CVM 인스턴스는 시스템 재설치를 통해 현재의 운영 체제를 Tencent Linux로 변경할 수 있습니다.
작업에 대한 자세한 내용은 [시스템 재설치](https://intl.cloud.tencent.com/document/product/213/4933)를 참조 바랍니다.

## 배포 설명
| 출시일 | 이미지 버전 | 버전 설명 |
|---------|---------|---------|
| 2019년 9월 17일 | Tencent Linux release 2.4 (Final) | 이미지 ID: img-hdt9xxkt<br>커널 버전: 4.14.105<br>배포 리전: 모든 리전 |


## 기술 지원
Tencent Cloud는 Tencent Linux에 다음과 같은 기술 지원을 제공합니다.
- YUM 저장소에서 보안 업데이트(Security Updates)를 제공하며, `yum update` 명령어를 실행하여 버전을 업데이트할 수 있습니다.
- Tencent Linux는 커널 커뮤니티가 장기간 지원하는 4.14.105 버전을 기반으로 클라우드 환경에 맞춘 운영 체제 이미지입니다. Tencent Cloud에서는 이를 사용하는 동안 발생하는 문제에 대한 기술 지원을 제공합니다.
