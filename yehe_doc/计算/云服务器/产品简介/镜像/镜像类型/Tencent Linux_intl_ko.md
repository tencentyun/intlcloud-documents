
Tencent Linux(약칭 Tlinux)는 Tencent가 클라우드의 시나리오를 대상으로 개발한 Linux 운영 체제로, 전문적인 기능과 최적화 성능에, CVM 인스턴스 중의 애플리케이션에 고성능의 보다 안전하고 신뢰성 있는 실행 환경을 제공합니다. Tencent Linux는 무료로 사용할 수 있고 CentOS(및 릴리스 버전)에서 개발한 애플리케이션은 직접 Tencent Linux에서 실행할 수 있으며 사용자는 Tencent Cloud의 업데이트 유지보수 및 기술 지원도 지속해서 받을 수 있습니다.

## 적용 설명
Tencent Linux는 아래의 시나리오에 적용됩니다.
- 절대다수 CVM 각 사양 패밀리 인스턴스, CPM 2.0 포함.
- 인스턴스 실행 시 사용자 데이터(즉 userdata의 방식)를 통해 관련 작업을 cloud-init로 전달함으로써 인스턴스 실행 시 동적 설정을 하는 목적을 달성해야 합니다.

## 주요 특징

<table>
	<tr><th>특징 유형</th><th>특징 내용</th></tr>
	<tr><td><b>커널 사용자 정의</b></td><td>커널 커뮤니티에서 장기간 지원하는 4.14.105버전에 기반하여 사용자 정의되어 클라우드 시나리오에 적용되는 새로운 특성을 추가하고 커널 성능을 개선하였으며 중대한 결함을 수정합니다.</td></tr>
	<tr><td><b>컨테이너 지원</b></td><td>컨테이너 시나리오에 대해 최적화하고 격리 강화 및 성능 최적화 특성을 제공. <ul style="margin: 0;"><li>meminfo, vmstat, cpuinfo, stat, loadavg 등 격리</li><li>Sysctl 격리, 예를 들어 tcp_no_delay_ack, tcp_max_orphans</li><li>대량 파일 시스템과 네트워크의 BUGFIX</li></ul></td></tr>
	<tr><td><b>성능 최적화</b></td><td>컴퓨팅, 스토리지 및 네트워크 서브 시스템은 모두 최적화 과정을 거쳤고 다음을 포함합니다.<ul style="margin: 0;"><li>xfs 메모리 할당을 최적화하여 xfs kmem_alloc 할당 실패 알람 문제를 해결</li><li>네트워크 리시브 패킷의 대용량 메모리 할당 문제를 최적화하고 UDP 패킷 용량이 클 때 메모리를 지나치게 많이 차지하는 문제를 해결</li><li>시스템 page cache의 메모리 점유율을 제한함으로써 메모리 부족으로 비즈니스 성능 또는 OOM에 미치는 영향을 피했습니다.</li></ul></td></tr>
	<tr><td><b>소프트웨어 패키지</b></td><td><ul style="margin: 0;"><li>CentOS 7 버전의 소프트웨어 패키지에 기반하여 사용자 정의되었습니다</li><li>사용자 소프트웨어 패키지와 CentOS 7 버전은 호환되고 해당 버전의 사용자 모드 소프트웨어 패키지는 Tencent Linux 환경에서 직접 사용할 수 있습니다</li><li>YUM을 사용해 소프트웨어 패키지를 업데이트하고 설치합니다</li><li>YUM을 통해 epel-release 패키지 설치 후 epel 소스 중의 소프트웨어 패키지를 사용할 수 있습니다</li></ul></td></tr>
	<tr><td><b>결함 지원</b></td><td><ul style="margin: 0;"><li>운영 체제가 크래쉬됐을 때 kdump 커널 덤프 기능 제공</li><li>커널의 핫 패치 업그레이드 기능 제공</li></ul></td></tr>
	<tr><td><b>보안 업데이트</b></td><td>Tencent Linux는 정기적인 업데이트를 통해 보안성 및 기능을 강화합니다</td></tr>
</table>

## 배포 설명

| 배포 시간 | 미러 이미지 버전 | 버전 설명 |
|---------|---------|---------|
| 2019년 9월 17일 | Tencent Linux release 2.4 (Final) | 미러 이미지 ID: img-hdt9xxkt<br>커널 버전: 4.14.105<br>배포 리전: 모든 리전 |

## Tlinux 획득
Tencent Cloud는 [CVM 콘솔](https://console.cloud.tencent.com/cvm)에서 Tencent Linux 공용 이미지를 제공하고 있어 사용자는 다음의 방법을 통해 Tencent Linux를 획득하고 사용할 수 있습니다.
- CVM 인스턴스 생성 시 공용 이미지를 선택하고 Tencent Linux의 상응하는 버전을 선택합니다.
자세한 작업 내용은 [인스턴스 생성](http://intl.cloud.tencent.com/document/product/213/4855)을 참조하십시오.
- CVM 인스턴스 생성 후, 시스템 재설치를 통해 기존 운영 체제를 Tencent Linux로 변경할 수 있습니다.
자세한 작업 내용은 [시스템 재설치](http://intl.cloud.tencent.com/document/product/213/4933)를 참조하십시오.

## 기술 지원
Tencent Cloud는 Tencent Linux를 위해 다음의 기술 지원을 제공합니다.
- Tencent Cloud는 YUM repository에 보안 업데이트(Security Updates)를 제공하고 `yum update` 명령을 실행하여 버전 업그레이드할 수 있습니다.
- Tencent Linux는 커널 커뮤니티에서 장기간 지원해 온 4.14.105 커널 버전를 기반으로 클라우드 환경에 맞춘 운영체제 이미지 입니다. Tencent Cloud는 Tencent Linux를 사용하면서 겪는 문제에 대해 기술 지원을 제공해 드립니다.
