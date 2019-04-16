
TencentDB for Redis 파악 시, 일반적으로 다음 개념을 만날 것입니다.

**인스턴스**: Tencent Cloud에서 독립적으로 실행하는 데이터베이스 환경입니다. 한 개의 데이터베이스 인스턴스는 여러 개의 사용자가 생성한 데이터베이스를 포함할 수 있습니다.

[**VPC**](https://cloud.tencent.com/document/product/215/20046): 사용자 지정한 가상 네트워크 공간으로 기타 리소스 로직과 격리됩니다.

[**보안 그룹**](https://cloud.tencent.com/document/product/239/30911): Redis 인스턴스에 보안 접근 제어를 진행하며, 인스턴스에 진입할 IP, 프로토콜 및 포트 규칙을 지정합니다.

[**지역과 가용 영역**](https://cloud.tencent.com/document/product/239/4106): Redis 인스턴스와 기타 리소스의 물리적 위치입니다.

[**Tencent Cloud 콘솔**](https://console.cloud.tencent.com/cdb): Web에 기반한 사용자 인터페이스입니다.

[**프로젝트**](https://cloud.tencent.com/document/product/378/10863): 개발자가 클라우드 제품을 더욱 잘 관리하기 위해 개발한 기능으로 이 기능은 주로 프로젝트를 단위로 진행하며, 각 클라우드 제품을 프로젝트에 할당하여 프로젝트 관리를 구현합니다.

[**읽기/쓰기 분리**](https://cloud.tencent.com/document/product/239/19543): TencentDB for Redis는 읽기/쓰기 분리 기능을 시작/종료할 수 있으며, 읽기 작업이 쓰기 작업보다 많은 시나리오에 대해 핫 데이터 집중형 읽기 수요를 해결하며 최대 1 마스터 5 슬레이브 모드를 자랑하고 최대 5배의 가독성 확장 능력을 제공합니다.

