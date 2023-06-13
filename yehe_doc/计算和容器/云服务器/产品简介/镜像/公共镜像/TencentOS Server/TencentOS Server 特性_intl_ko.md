## 커널 사용자 정의
커널 커뮤니티에서 장기간 지원해온 버전을 기반으로 만든 사용자 정의 버전으로, 클라우드 시나리오에 적용되는 새로운 특징을 추가하고 커널 성능을 개선하였으며 주요 결함을 수정하였습니다.

## 컨테이너 시나리오에 최적화된 성능
컨테이너 시나리오에 최적화하여 더욱 강화된 격리 및 최적화된 성능을 제공합니다.
- meminfo, vmstat, cpuinfo, stat, loadavg 등을 격리.
- Sysctl 격리, 예: tcp_no_delay_ack、tcp_max_orphans.
- 대용량 파일 시스템 및 네트워크의 BUGFIX.
- IPVS 모드의 높은 동시 접속량 시나리오에서 연결 재사용으로 인한 연결 오류 해결.
- IPVS모드에서 노드(코어 수가 많은)를 많이 구성했을 때 과도한 IPVS 규칙으로 인해 발생한 네트워크 결함을 해결.
- 컨테이너 밀도가 높은 시나리오(단일 노드에 많은 컨테이너가 있는)에서 cAdvisor가 memcg를 읽어 커널 상태가 너무 길어지면서 발생한 네트워크 결함을 해결.
- 많은 노드가 구성되어 있는(코어 수가 많은) 시나리오의 대형 Pod(점유 코어 수가 많고 싱글 코어 점유가 높은)에서 CPU 로드 밸런싱으로 인해 발생한 네트워크 결함을 해결.
- 동시 접속량이 높은 시나리오에서 TCP 연결 모니터링(예: TCP 연결 모니터링 설정을 위한 cAdvisor 단독 배포)으로 인해 주기적으로 발생하는 네트워크 지터 문제를 해결.
- 네트워크 수신 패키지 소프트웨어 인터럽트(soft IRQs) 최적화로 네트워크 성능 향상.

## 컨테이너 사용자 정의 기능
### 컨테이너 리소스 격리 표시
- 호스트 레벨 스위치 추가: 커널에서 LXCFS와 유사한 특성 구현. 사용자가 노드에 LXCFS 파일 시스템을 배포하고 POD spec을 수정할 필요 없이 노드에서 전역 스위치(`sysctl -w kernel.stats_isolated=1`)만 켜면, `/proc/cpuinfo`와 `/proc/meminfo` 등 파일을 가져와 컨테이너별로 격리할 수 있습니다.
<dx-alert infotype="notice" title="">
TencentOS Server 2.4 버전만 'kernel.stats_isolated' 매개변수를 지원하며, TencentOS Server 2.4(TK4) 및 3.1 이후 버전 에서는 지원되지 않습니다.
</dx-alert>
- 컨테이너 레벨 스위치 추가: 노드 모니터링 모듈 등 특수 컨테이너에 대해 컨테이너 레벨의 스위치 `kernel.container_stats_isolated` 추가. 호스트 레벨 스위치 활성화 시 컨테이너 실행 스크립트에서 컨테이너 레벨 스위치(`sysctl -w kernel.container_stats_isolated=0`)만 끄면 컨테이너에서 `/proc/cpuinfo`와 `/proc/meminfo` 파일을 읽어올 때 호스트 정보를 획득할 수 있습니다.

### 커널 매개변수 격리
다음 커널 매개변수의 namespace화 격리 구현:
- `net.ipv4.tcp_max_orphans`
- `net.ipv4.tcp_workaround_signed_windows`
- `net.ipv4.tcp_rmem`
- `net.ipv4.tcp_wmem`
- `vm.max_map_count`

### 컨테이너 디폴트 커널 매개변수 최적화
컨테이너 네트워크 namespace의 `net.core.somaxconn` 디폴트값을 4096로 조정하여, 동시 접속량이 많은 상황에서 세미조인(semi join) 큐가 가득 찼을 때 패킷 손실 문제를 줄여줍니다.

## 성능 최적화
다음과 같은 컴퓨팅, 스토리지 및 네트워크 서브 시스템을 모두 최적합니다.
- xfs 메모리 할당을 최적화하여, xfs kmem_alloc 할당 실패 경고 해결.
- 네트워크 수신 패키지 대용량 메모리 할당을 최적화하여 UDP 패키지 용량이 클 때 메모리를 과도하게 점유하는 문제 해소.
- 시스템 page cache의 메모리 점유율을 제한하여 메모리 부족으로 인한 서비스 성능 저하 또는 OOM에 대한 영향 방지.

## 소프트웨어 패키지 지원
- TencentOS Server 2 사용자 모드 소프트웨어 패키지는 최신 버전의 CentOS 7과 호환되므로, CentOS 7 버전의 소프트웨어 패키지를 TencentOS Server 2.4에서 그대로 사용할 수 있습니다. 
- TencentOS Server 3 사용자 모드 소프트웨어 패키지는 최신 버전의 RHEL 8과 호환되므로, RHEL 8 버전의 소프트웨어 패키지를 TencentOS Server 3.1에서 그대로 사용할 수 있습니다. 
- YUM을 사용해 소프트웨어 패키지 업데이트 및 설치 가능.
- YUM으로 epel-release 패키지 설치 후 epel 소스의 소프트웨어 패키지 사용 가능.

## 버그 지원
- 운영 체제가 다운된 후 kdump 커널 덤프 기능 제공.
- 커널의 핫픽스(hotfix) 업그레이드 기능 제공.

## 보안 업데이트
TencentOS Server는 정기적인 업데이트를 통해 보안과 기능을 강화합니다.
