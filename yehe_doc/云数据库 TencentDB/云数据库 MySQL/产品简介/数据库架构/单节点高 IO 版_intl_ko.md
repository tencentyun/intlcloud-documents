TencentDB for MySQL은 고가용성 버전, 파이낸스 버전, 단일 노드 고IO 버전 및 기본 버전 등 네 가지 구성이 있으며, 본 문서는 단일 노드 고IO 버전의 구성을 소개합니다.


단일 노드 고IO 버전 단일 물리 노드 배포를 사용하여 가성비가 우수합니다.

## 적용 시나리오
읽기/쓰기 분리 수요가 있는 각 업종에 적합합니다.

## 구성 특징
로컬 NVMe SSD 디스크를 사용하는 하위 스토리지로 강력한 IO 성능을 제공합니다. 현재 [읽기 전용 인스턴스](https://intl.cloud.tencent.com/document/product/236/7270)에 사용되고 있으며 서비스의 읽기 부하를 덜어줄 수 있어 읽기/쓰기 분리 수요가 있는 각 업종에 적합합니다.

## 구성의 기본 프레임워크
![Alt text](http://imgcache.qq.com/open_proj/proj_qcloud_v2/gateway/shopcart/database/css/img/mysql-frame3.svg)
>!
>- 단일 노드 배포에는 단일 장애점이 존재하며, 읽기 전용 인스턴스를 하나만 구매했을 경우 단일 읽기 전용 인스턴스에 장애 발생 시, 서비스가 중지되어 사용자에게 영향을 미칠 수 있으므로 서비스의 고가용성을 보장할 수 없습니다.
>- 단일 읽기 전용 인스턴스를 복구하는 데 소요되는 시간은 비즈니스 데이터양의 영향을 받으므로 그 정도를 확신할 수 없습니다. 따라서, 가용성 수요가 높은 비즈니스 [RO 그룹](https://intl.cloud.tencent.com/document/product/236/11361) 내에서는 최소 두 가지의 읽기 전용 인스턴스를 선택해 구매하시길 권장합니다.


## 관련 작업
- TencentDB for MySQL은 1개 혹은 여러 개의 읽기 전용 인스턴스를 생성하도록 지원합니다. 이에 따라 사용자의 읽기/쓰기를 분리하고, 원 마스터 멀티 슬레이브 응용 시나리오를 지원합니다. 자세한 내용은 [읽기 전용 인스턴스 생성](https://intl.cloud.tencent.com/document/product/236/7270)을 참조 바랍니다.
- TencentDB for MySQL은 1개 혹은 여러 개의 읽기 전용 인스턴스로 RO 그룹을 생성할 수 있도록 지원하여 가용성을 보장할 수 있습니다. 자세한 내용은 [읽기 전용 인스턴스 RO그룹(https://intl.cloud.tencent.com/document/product/236/11361)을 참조 바랍니다.

