Cloud Block Storage(CBS)는 CVM에 사용되는 지속적인 데이터 블록별 스토리지 서비스를 제공합니다.

- CBS의 데이터는 자동으로 가용존에 여러 여분 복사본을 저장하여 데이터의 단일 장애점 위험을 방지하므로, 99.9999999%에 달하는 데이터 신뢰성을 제공합니다.
- CBS는 여러 유형 및 사양의 디스크 인스턴스를 제공하므로 안정적이고 낮은 딜레이의 스토리지의 성능적 요구사항을 만족할 수 있습니다.
- CBS는 동일한 가용존의 인스턴스에 대한 마운트/언마운트를 지원하며, 단 몇 분 안에 스토리지 용량을 조절할 수 있어 탄력적인 데이터 수요를 만족합니다. 설정된 리소스 양에 대한 소량의 비용만 지불하면, 위의 기능 및 특징을 모두 누리실 수 있습니다.


## 일반 사용 시나리오
- CVM 사용 중 디스크 용량이 부족하다면 1개 또는 여러 개의 CBS를 구매하고 CVM에 마운트하여 스토리지 용량 수요를 만족할 수 있습니다.
- CVM을 구매할 때에는 추가적인 스토리지 용량이 필요하지 않으며, 스토리지 요구 사항이 있는 경우에는 다시 CBS 구매를 통해 CVM의 스토리지 용량을 확장할 수 있습니다.
- 여러 CVM 간에 데이터를 교환해야 할 때는, CBS(데이터 디스크)를 언마운트하고 다른 CVM에 다시 마운트할 수 있습니다.
- 여러 개의 CBS 구매 및 LVM(Logical Volume Manager) 논리 볼륨 설정을 통해 단일 CBS의 스토리지 용량 최댓값을 확대할 수 있습니다.
- 여러 개의 CBS 구매 및 RAID(Redundant Array of Independent Disks) 정책 설정을 통해 단일 클라우드 디스크 I/O 성능의 최댓값을 확대할 수 있습니다.


## 라이프사이클
CBS에서 **엘라스틱 CBS** 의 라이프사이클은 CVM과 독립되어 있으며, 인스턴스 실행에 영향을 받지 않습니다. 사용자는 여러 개의 CBS를 동일한 인스턴스에 마운트할 수 있으며 인스턴스에서 CBS 연결을 끊고 다른 인스턴스에 마운트할 수도 있습니다.

## 구매 및 사용
- 디스크 제품 유형에 대한 자세한 내용은 [CBS 유형](https://intl.cloud.tencent.com/document/product/362/31636)을 참조 바랍니다.
- CBS 구매에 대한 자세한 내용은 [CBS 가격 리스트](https://intl.cloud.tencent.com/document/product/362/2413)를 참조 바랍니다.
- CVM과 CBS 설정에 대한 자세한 내용은 [CBS 생성](https://intl.cloud.tencent.com/document/product/362/5744)과 [CBS 마운트](https://intl.cloud.tencent.com/document/product/362/5745)를 참조 바랍니다.
- CBS의 스케일 업(Expand), 언마운트, 폐기 및 CBS에 대한 더 많은 모범 사례는 [CBS 제품 문서](https://intl.cloud.tencent.com/document/product/362)를 참조 바랍니다.
