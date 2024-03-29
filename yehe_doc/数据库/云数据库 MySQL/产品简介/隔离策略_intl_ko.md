
본문은 TencentDB for MySQL의 세 가지 리소스 격리 정책인 기본형, 일반형 및 전용형에 대해 설명합니다.

>?
>- 기존 기본 버전은 ‘단일 노드-기본형’으로, 기존 단일 노드 High IO 버전은 ‘단일 노드-일반형’으로 이름이 변경되었습니다.
>- 2노드 및 3노드 인스턴스는 일반형 및 전용형 정책을 지원합니다.

| 리소스 격리 정책 | 설명                                                         |
| -------- | ------------------------------------------------------------ |
| 기본형   | 단일 노드 인스턴스만 이 정책을 지원합니다. 기본형 단일 노드 인스턴스(기존 기본 버전)는 컴퓨팅-스토리지 분리를 지원하며, 클라우드 디스크에 데이터를 저장합니다. |
| 일반형   | <li>일반 인스턴스는 할당된 메모리와 디스크 리소스를 독점적으로 사용하며, 동일한 물리적 시스템에 있는 다른 일반 인스턴스와 CPU 리소스를 공유합니다. <li>일반 인스턴스는 CPU 리소스를 공유하여 더 낮은 비용으로 더 높은 사양의 이점을 얻습니다. <li>일반 인스턴스의 디스크 용량은 CPU 및 메모리 사양의 영향을 받지 않으므로 유연하게 구성할 수 있습니다. |
| 전용형   | <li>전용 인스턴스는 CPU(CPU가 바인딩된 경우), 메모리 및 디스크 리소스에 독점적으로 액세스할 수 있습니다. 성능이 장기적으로 안정적이며, 물리적 시스템의 다른 인스턴스의 활동에 영향을 받지 않습니다. <li>최고 사양 전용형 인스턴스는 물리적 머신과 모든 리소스를 독점할 수 있습니다. | 


## 다양한 인스턴스 아키텍처의 격리 정책
- TencentDB for MySQL 단일 노드(클라우드 디스크) 인스턴스는 네이티브 TKE를 기반으로 배포되며, 각 인스턴스에는 전용 CPU, 메모리 및 디스크 리소스가 있고, 각 인스턴스는 서로 완전히 격리됩니다.
- TencentDB for MySQL 2노드(로컬 디스크) 및 3노드(로컬 디스크) 인스턴스는 로컬 물리적 머신을 기반으로 배포됩니다. 각 물리적 시스템은 여러 인스턴스를 유지하고, 격리 정책을 채택하고 전용 CPU, 메모리 및 디스크 리소스를 사용하여 각 인스턴스 간의 완전한 격리를 보장합니다.
또한 TencentDB for MySQL은 계정, 리전, AZ 및 네트워크와 같은 여러 차원에서 해당 데이터 격리 정책을 구현합니다.
  
