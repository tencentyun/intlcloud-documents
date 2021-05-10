TencentOS Server(Tencent Linux, TS 또는 tlinux라고도 함)는 Tencent가 클라우드 시나리오를 위해 연구 개발한 Linux 운영 체제입니다. 특수 기능 및 최적화된 성능으로 CVM 인스턴스의 응용 프로그램을 위해 고성능의 안전하고 안정화된 운영 환경을 제공합니다. TencentOS Server는 무료 제공되며 CentOS(또는 기타 릴리스 버전)에서 개발된 애플리케이션을 TencentOS Server에서 바로 실행할 수 있습니다. 또한 Tencent Cloud OS팀에서 지속적인 업데이트와 점검, 기술 지원을 제공합니다.

## 사용 설명

TencentOS Server는 다음과 같은 시나리오에 적용할 수 있습니다.

- 거의 모든 CVM 인스턴스 패밀리.
- 인스턴스 실행 시, 동적 설정을 진행하기 위해, 사용자 데이터(즉 userdata 방식)를 통해 관련 작업을 cloud-init에 전달해야 합니다.

## TencentOS Server 2.4 환경 설명

### 사용자 모드 환경

사용자 모드 소프트웨어 패키지는 최신 버전의 CentOS 7과 호환되므로 CentOS 7을 TencentOS Server 2.4에서 직접 연결하여 사용할 수 있습니다.

### 시스템 서비스 및 최적화 설정

#### 시스템 서비스

- ‘tlinux-irqaffinity’: TencentOS Server 할당 서비스를 자동 중단합니다.
- `tlinux-bootlocal`: TencentOS Server의 bootlocal 서비스로서, 시작 시 `/etc/rc.d/boot.local`을 자동 실행합니다.

#### 시스템 툴

`tencent-tools`: tos(약칭 t) 명령어로 시스템 관리에 사용됩니다. 지원 매개변수는 다음과 같습니다.

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

#### TencentOS Server 2.4 커널

longterm 4.14 버전의 커널을 기반으로 하며, 자세한 내용은 [TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel)을 참조하십시오.


## TencentOS Server 다운로드

다음의 방법을 통해 TencentOS Server를 다운로드하고 사용할 수 있습니다.

- CVM 인스턴스 생성 시 공용 이미지를 선택하고, 상응하는 TencentOS Server 버전을 선택합니다.
  작업에 대한 자세한 내용은 [인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참조하십시오.
- 이미 생성된 CVM 인스턴스는 시스템 재설치를 통해 기존 운영 체제를 TencentOS Server로 변경할 수 있습니다.
  작업에 대한 자세한 내용은 [시스템 재설치](https://intl.cloud.tencent.com/document/product/213/4933)를 참조하십시오.

## 배포 설명

| 출시일      | 이미지 버전                                                     | 버전 설명                                                     |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 2019년 9월 17일 | TencentOS Server 2.4, 기존 명칭 Tencent linux release 2.4 (Final) | 이미지 ID: img-hdt9xxkt<br>커널 버전: 4.14.105<br>배포 리전: 모든 리전 |


## 기술 지원

Tencent Cloud는 TencentOS Server에 다음과 같은 기술 지원을 제공합니다.

- YUM 저장소에서 보안 업데이트(Security Updates)를 제공하며, `yum update` 명령어를 실행하여 버전을 업데이트할 수 있습니다.
- TencentOS Server는 커널 커뮤니티가 장기간 지원해 온 4.14.105 버전을 기반으로 클라우드 환경에 맞춰 제작된 운영 체제 이미지입니다. Tencent Cloud에서는 이를 사용하는 동안 발생하는 문제 해결을 위해 기술 지원을 제공합니다.
