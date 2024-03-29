인스턴스 구성 시 로컬 디스크 또는 CBS를 시스템 디스크 또는 데이터 디스크로 선택할 수 있습니다. 스토리지 미디어를 선택하기 전에 [로컬 디스크](https://intl.cloud.tencent.com/document/product/213/5798) 및 [CBS](https://intl.cloud.tencent.com/document/product/213/4953)를 참고하여 이 두 가지의 특징과 적용 시나리오의 차이를 확인하십시오.
>! 
>- 선택한 인스턴스 사양에 따라 구매 인터페이스에 구매할 수 있는 다양한 유형의 시스템 디스크 및 데이터 디스크가 표시됩니다. 예를 들어, 높은 IO 인스턴스 유형을 선택한 사용자만 SSD 로컬 디스크를 선택할 수 있습니다.
>- 로컬 디스크를 선택한 CVM(시스템 디스크 및 데이터 디스크 포함)은 구성(CPU, 메모리, 디스크)의 업그레이드를 지원하지 않습니다. 대역폭 업그레이드만 지원합니다.
>- 구매 완료 후, 시스템 디스크는 스토리지 미디어 변경을 지원하지 않습니다.
> 

스토리지 미디어(SATA HDD 로컬 디스크, NVME SSD 로컬 디스크, 프리미엄 CBS 및 SSD CBS)의 차이 및 적용 시나리오는 다음 표와 같습니다.

| 스토리지 미디어 | 장점 | 적용 시나리오 |
|---------|---------|---------|
| NVME SSD  로컬 디스크(높은 IO 모델 IT3, IT5 등만 지원) | 저지연: 마이크로 초 수준의 액세스 딜레이. | **임시 읽기 캐시로 사용**: NVME SSD 로컬 디스크의 우수한 랜덤 읽기 기능(4KB/8KB/16KB 랜덤 읽기)은 MySQL, Oracle 등과 같은 관계형 데이터베이스의 읽기 전용 슬레이브 데이터베이스로 사용하기에 적합합니다. <br>메모리 비용은 솔리드 스테이트 디스크보다 여전히 비싸기 때문에, NVME SSD 로컬 디스크는 Redis, Memcache와 같은 캐시형 서비스의 L2 캐시로 사용할 수도 있습니다. <br> **주의사항**: NVME SSD 로컬 디스크에는 단일 포인트 장애 리스크가 존재하므로 데이터 가용성 보장을 위해 응용 레이어에 데이터 이중화 진행을 권장합니다. 핵심 서비스는 SSD CBS를 사용을 권장합니다. |
| SATA HDD 로컬 디스크(빅 데이터 모델 D2 등에서만 지원) | <ul style="margin: 0;"><li>는 가격이 저렴하며, 콜드 데이터 백업, 아카이빙 등 용도로 사용할 수 있습니다. </li><li>높은 처리량: 로컬 HDD의 처리량을 제공합니다. </li></ul> | EMR 및 기타 빅 데이터 처리와 같은 **대용량 파일 순차 읽기/쓰기 시나리오**에 적합합니다. |
| 프리미엄 CBS | 90%의 I/O 시나리오에 적합하며, 고품질 및 저비용의 최상의 선택입니다. | **중소형 데이터베이스, Web 서버** 등의 시나리오에 적합합니다. 장기적으로 안정적인 IO 성능을 제공합니다. <br> 핵심 서비스 테스트 및 연동 테스트 개발 환경의 IO 요구를 충족합니다. |
| SSD CBS | 고성능 및 높은 데이터 신뢰성: 업계 최고의 NVMe 솔리드 스테이트 스토리지를 디스크 미디어로 사용합니다. I/O 집약형 서비스에 적합하며, 장기적으로 안정적이고 매우 높은 수준의 단일 디스크 성능을 제공합니다. | 다음의 시나리오에 적용: <ul style="margin: 0;"><li> **중대형 데이터베이스**: 백만 행 테이블 수준의 MySQL, Oracle, SQL Server 등과 같은 중대형 관계형 데이터베이스 애플리케이션. </li><li> **핵심 서비스 시스템**: 데이터 신뢰성에 요구도가 높은 I/O 집약형과 같은 핵심 서비스 시스템. </li><li> **빅 데이터 분석**: TB, PB 규모 데이터에 대한 분산식 처리 기능을 제공하며, 데이터 분석, 마이닝, 비즈니스 인텔리전스 등의 분야에 적합. </li></ul> |

- [CBS 유형 설명](https://intl.cloud.tencent.com/ko/document/product/213/33000)을 참고하여 더 많은 CBS의 사양, 시나리오 및 애플리케이션 설명에 대해 알 수 있습니다.
- CBS 가격 정보는 [CBS 가격 리스트](https://cloud.tencent.com/document/product/213/2255)를 참고하십시오.
