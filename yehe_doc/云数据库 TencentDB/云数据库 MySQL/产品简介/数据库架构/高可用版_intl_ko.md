TencentDB for MySQL은 고가용성 버전, 파이낸스 버전, 단일 노드 고IO 버전 및 기본 버전 등 네 가지 구성이 있으며, 본 문서는 고가용성 버전의 구성을 소개합니다.


고가용성 버전은 원 마스터 원 슬레이브의 고가용성 모드를 사용하며, 실시간 핫 백업으로 다운(Down) 시 자동 점검 및 장애 자동 이전을 지원합니다.

## 적용 시나리오
게임, 인터넷, 사물인터넷(IoT), 소매 전자상거래, 물류, 보험, 증권 등 다양한 업종에 사용할 수 있습니다.

## 구성 특징
- 마스터/슬레이브 복제는 비동기화(기본)와 반동기화 두 가지 방식이 있습니다. 복제 방식은 [콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 상세 페이지에서 변경할 수 있으며, 콘솔에서 [파이낸스 버전으로 업그레이드](https://intl.cloud.tencent.com/document/product/236/35986)할 수도 있습니다(원 마스터 투 슬레이브 강제 동기화 모드).
- 읽기 전용 인스턴스, 재해 복구 인스턴스, 보안 그룹, 데이터 마이그레이션, 멀티 가용존 배포 등을 포함한 다양한 특성을 지원하며 이에 대한 자세한 내용은 [제품 장점](https://intl.cloud.tencent.com/document/product/236/5148)을 참조 바랍니다.
- 고가용성 버전 인스턴스의 가용 성능은 99.95%에 달하며 서비스 수준 계약에 대한 자세한 내용은 [서비스 수준 계약(SLA)](https://intl.cloud.tencent.com/zh/document/product/301/30977)을 참조 바랍니다.
- 강력한 하드웨어에 배포된 데이터 노드와 로컬 NVMe SSD 디스크를 사용하는 하위 스토리지로 강력한 IO 성능을 제공함으로써, IOPS가 최대 240000에 달합니다(실제 IOPS 속도는 설정, 페이지 사이즈 및 비즈니스 부하와 관련되며, 해당 값은 MySQL의 기본 페이징 사이즈인 16KB를 기준으로 테스트하여 도출한 것이므로 참고만 하시기 바랍니다).

## 구성의 기본 프레임워크
![Alt text](https://main.qcloudimg.com/raw/77490755263740e5ed8c51952d7309c1.svg)

## 업그레이드 관련 작업
- TencentDB for MySQL은 데이터베이스 엔진 업그레이드를 지원합니다. 자세한 내용은 [데이터베이스 엔진 버전 업그레이드](https://intl.cloud.tencent.com/document/product/236/8126)를 참조 바랍니다.
- TencentDB for MySQL은 고가용성 버전 인스턴스를 파이낸스 버전 인스턴스로 업그레이드하도록 지원합니다. 자세한 내용은 [고가용성 버전을 파이낸스 버전으로 업그레이드](https://intl.cloud.tencent.com/document/product/236/35986)를 참조 바랍니다.
- TencentDB for MySQL은 커널 마이너 버전의 자동/수동 업그레이드를 지원합니다. 자세한 내용은 [커널 마이너 버전 업그레이드](https://intl.cloud.tencent.com/document/product/236/36816)를 참조 바랍니다.
