### TencentOS Server란?
TencentOS Server(Tencent Linux, TS 또는 tlinux)는 Tencent가 클라우드 시나리오용으로 개발한 Linux 운영 체제로 특정 기능 및 성능 최적화를 제공하여 클라우드 서버 인스턴스의 애플리케이션에 보다 안전하고 안정적인 고성능 운영 환경을 제공합니다.
TencentOS Server는 Tencent OS 팀이 개발한 TencentOS 커널을 포함하고 있으며 클라우드 환경의 심층적인 사용자 정의를 기반으로 하여 최신 Linux 혁신을 시장에 출시하여 다양한 엔터프라이즈 소프트웨어에 초강력 성능, 높은 확장성 및 신뢰성을 제공합니다. TencentOS Server는 무료 베타를 제공하며 사용자는 Tencent OS 팀으로부터 계속 업데이트, 유지 관리 및 기술 지원을 받을 수 있습니다.

### TencentOS Server의 특징은 무엇입니까?
TencentOS Server의 제품 특징은 다음과 같습니다.
- 높은 수준의 커스터마이징, 즉시 사용 가능, 복잡한 설정이 필요 없음.
- 보안 및 컴플라이언스, 핫 패치 지원, 무중단 복구.
- 장기적인 지원, 강력한 운영 지원 팀, 완전한 오픈 소스.
- 클라우드 시나리오를 위해 설계되고 전면 최적화된 고성능 OS.

### 다른 Linux 운영 체제 대비 TencentOS Server의 장점은 무엇입니까?
CentOS 및 Ubuntu와 같은 릴리스 버전 대비 TencentOS Server의 주요 장점은 다음과 같습니다.
- 10년 이상 수많은 Tencent 내부 비즈니스를 통해 검증 및 최적화 되었습니다.
- 권위 있는 커널 전문가 팀의 지원을 받습니다.
- 즉시 사용 가능하며, 주요 성능 최적화 및 클라우드와 컨테이너 시나리오에 대한 커스터마이징 특성을 갖추었습니다.
- 강력한 운영 지원팀을 보유하고 있어 적은 비용으로도 강력한 비즈니스 지원을 받을 수 있습니다.

### TencentOS Server에는 어떤 버전이 있습니까?
현재 다음 두 가지 버전이 포함되어 있습니다.
- TencentOS Server 2 (TS2): CentOS 7 기반의 최신 사용자 모드 패키지.
- TencentOS Server 3 (TS3): RHEL 8 기반의 최신 사용자 모드 패키지.

TencentOS Server 사용자 모드 소프트웨어 패키지는 RHEL과 100% 이진법 호환이 가능합니다.

### TencentOS Server의 커널에는 어떤 버전이 있습니까?
TencentOS Server의 커널(줄여서 TK)에는 다음 두 가지 버전이 포함되어 있습니다.
- TK3: 커뮤니티 4.14 longterm 기반 커널 버전.
- TK4: 커뮤니티 5.4 longterm 기반 커널 버전.

TK의 코드는 GitHub에서 얻을 수 있으며, 자세한 내용은 [TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel)을 참고하십시오.

### TencentOS Server의 라이프사이클은 얼마나 됩니까?
TencentOS Server의 각 버전별 라이프사이클은 다음과 같으며, bugfix 및 보안 패치 업데이트는 해당 라이프사이클이 종료될 때까지 계속 제공될 예정입니다.
- TencentOS Server 2 릴리스 버전: 2024년 12월 31일까지.
- TencentOS Server 2 릴리스 버전: 2029년 12월 31일까지.

### Tencent Cloud에서 TencentOS 서버를 사용하는 방법은 무엇입니까?
Tencent Cloud는 두 가지 버전의 공용 이미지를 제공하며 Linux 운영 체제로 클라우드 서버를 생성할 때 TencentOS Server 이미지 버전을 사용하도록 선택할 수 있습니다.

### TencentOS Server는 어떤 클라우드 서버 인스턴스 유형을 지원합니까?
TencentOS Server는 대부분의 클라우드 서버 인스턴스 유형을 지원하며 [클라우드 서버 구매 페이지](https://buy.intl.cloud.tencent.com/cvm?tab=custom®ionId=1&projectId=-1)에서 이미지를 선택하여 사용할 수 있습니다.

### 클라우드 서버에서 TencentOS Server 사용 시 요금이 발생합니까?
아닙니다. TencentOS Server 자체는 요금이 발생하지 않으며 클라우드 서버 실행 요금만 지불하면 됩니다.

### TencentOS Server 사용 후 소프트웨어 설치 및 업그레이드는 어떻게 하나요?
TencentOS Server 릴리스 버전은 'yum' 명령 또는 TencentOS Server와 함께 제공되는 't' 명령을 통해 소프트웨어 패키지를 관리할 수 있습니다. 그 중 TencentOS Server 3는 `dnf` 명령을 통해 소프트웨어 패키지를 관리할 수도 있습니다.

### TencentOS Server를 로컬에 설치하여 사용할 수 있나요?
네. TencentOS Server 릴리스 버전 ISO는 Tencent Cloud 소프트웨어 보관소(TencentOS Server 2 [클릭하여 다운로드](http://mirrors.tencent.com/tlinux/2.4/iso/), TencentOS Server 3 [클릭하여 다운로드](http://mirrors.tencent.com/tlinux/3.1/iso/x86_64/))에서 다운로드할 수 있습니다.
로컬 서버나 virtualbox와 같은 가상 컴퓨터에 설치하여 사용할 수 있습니다.

### TencentOS Server의 소스 코드를 조회할 수 있나요?
TencentOS Server는 완전히 오픈 소스입니다. [Tencent Cloud 소프트웨어 보관소](http://mirrors.tencent.com/)에서 소스 패키지를 얻거나 시스템에서 `yum downloader --source glibc` 명령어를 사용하여 얻을 수 있습니다.

### TencentOS Server는 32비트 애플리케이션과 라이브러리를 지원합니까?
현재는 지원되지 않습니다. TencentOS Server 2는 yum을 통한 일부 32비트 패키지 설치만 지원합니다.

### TencentOS Server는 시스템 보안을 어떻게 보장합니까?
TencentOS Server 버전은 RHEL7 및 RHEL8과 이진법 호환되며 RHEL의 보안 사양을 준수합니다. Tencent Cloud는 다음과 같은 측면에서 TencentOS Server 시스템의 보안을 보장합니다.
- Tencent가 자체 개발한 취약점 스캐닝 툴과 산업 표준 취약점 스캐닝 및 보안 점검 툴을 사용하여 정기적인 보안 스캔을 수행합니다.
- TencentOS Server의 보안 스캐닝 및 보안 강화를 지원하기 위해 Tencent 보안 팀과 협력합니다.
- 정기적으로 RHEL 및 커뮤니티 CVE 패치를 평가하고 정기적으로 사용자 모드 소프트웨어 패키지를 업데이트하여 보안 취약점을 보완합니다.
- Tencent Cloud의 호스트 보안 기능을 통해 시스템에 대한 보안을 정기적으로 점검하고 사용자 보안 경고 및 수리 솔루션을 배포합니다.



