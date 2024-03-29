## 소개

크로스 버킷 복제를 통해 Cloud Object Storage(COS)는 한 버킷에서 다른 버킷으로 증분 객체를 자동으로 비동기식으로 복제할 수 있습니다. 크로스 버킷 복제를 통해 COS는 원본 버킷에서 타깃 버킷으로 객체 메타데이터 및 버전 ID와 함께 정확히 동일한 객체를 정확하게 복제할 수 있습니다. 또한 객체 추가 또는 삭제와 같은 객체 작업을 타깃 버킷과 동기화할 수도 있습니다.

>!
>- 크로스 버킷 복제 기능을 활성화하려면 원본 버킷과 타깃 버킷에 버전 관리 기능이 활성화되어 있어야 합니다.
>- 크로스 버킷 복제 기능 활성화 후, 데이터 복제 시 스토리지 유형을 설정하지 않는 한 모두 원본과 동일한 스토리지 유형으로 유지됩니다.
>- COS 복제 시 원본 버킷의 액세스 제어 리스트(ACL)를 복제합니다. 원본 버킷과 타깃 버킷은 동일한 계정에서 소유해야 합니다.
>



## 적용 시나리오

- **원격 재해 복구: ** COS는 객체 데이터에 대해 ‘트웰브 나인’ 수준의 가용성을 보장하지만, 여전히 전쟁 및 자연 재해와 같은 불가항력으로 인한 데이터 손실 가능성은 존재합니다. 다른 버킷에 별도의 복제본을 명시적으로 저장하여 데이터 손실을 방지하려면, 원격 재해 복구에 도움이 되는 크로스 버킷 복제를 사용할 수 있습니다. 특정 IDC에서 불가항력적인 요소로 인해 데이터가 유실된 경우 다른 버킷의 IDC에서 복제본 데이터를 제공합니다.
- **컴플라이언스 요건: ** COS는 기본적으로 물리적 디스크의 데이터에 대해 여러 복제본 및 삭제 코드를 제공하여 데이터 가용성을 보장합니다. 그러나 일부 산업에서는 복제본을 다른 버킷에 보관하도록 규정하는 규정 준수 요구 사항이 있을 수 있습니다. 크로스 버킷 복제를 사용하면 버킷 간에 데이터를 복제하여 이러한 요구 사항을 충족할 수 있습니다. 
- **액세스 딜레이 최소화: ** 크로스 버킷 복제를 통해 최종 사용자가 다른 지역의 객체에 액세스하는 경우 가장 가까운 버킷에 객체 복제본을 유지할 수 있습니다. 이는 액세스 대기 시간을 최소화하여 더 나은 사용자 경험을 제공합니다. 
- **특별한 기술 요구 사항: ** 두 개의 서로 다른 버킷에 컴퓨팅 클러스터가 있고 클러스터가 크로스 버킷 복제를 사용하여 동일한 데이터 세트를 처리해야 하는 경우, 두 버킷에서 객체 복제본을 유지 관리할 수 있습니다.
- **데이터 마이그레이션 및 백업: ** 비즈니스 확장 수요에 따라 비즈니스 데이터를 한 버킷에서 다른 버킷으로 복제하여 데이터 마이그레이션 및 데이터 백업을 실현할 수 있습니다.

## 주의 사항

#### 복제 소요 시간

COS의 객체 복제 소요 시간은 객체의 크기, 버킷 리전 간의 거리, 객체의 업로드 방식 등의 요소에 의해 결정됩니다. 동기화 소요 시간은 해당 요소에 따라 달라지며, 몇 분에서 몇 시간까지 소요될 수 있습니다.

- 객체 크기: 대용량 객체 복제 시에는 더 많은 시간이 소요됩니다. 대용량 객체는 멀티파트 업로드 방식을 사용하여 객체의 업로드 및 동기화 시간을 단축할 것을 권장합니다.
- 버킷 리전 간의 거리: 리전 간의 거리가 멀수록 동기화 시 더 많은 데이터 전송 시간이 소요됩니다.
- 객체 업로드 방식: 간편 업로드 방식은 동시 작업이 불가능하며, 데이터를 하나씩 순차적으로 업로드 또는 다운로드합니다. 멀티파트 업로드 방식은 동시 작업이 가능하여 대용량 파일 업로드 시 멀티파트 업로드 방식을 이용하면 업로드 및 버킷 복제 작업을 더욱 빠르게 진행할 수 있습니다. 객체 업로드 방식에 대한 자세한 소개는 [간편 업로드](https://intl.cloud.tencent.com/document/product/436/14113) 및 [멀티파트 업로드](https://intl.cloud.tencent.com/document/product/436/14112) 문서를 참고하십시오.

#### 라이프사이클 관련

크로스 버킷 복제를 사용하려면 먼저 버전 관리를 활성화해야 해야 하며, 이 경우 버킷에 객체의 여러 과거 버전이 유지되어 더 많은 스토리지 사용량이 발생합니다. COS 크로스 버킷 복제에는 요청, 다운스트림 트래픽 및 스토리지 사용량에 대한 요금이 발생합니다. 이 중 스토리지 사용량은 타깃 버킷 리전 요금으로 청구됩니다. 비용을 절감하거나 데이터 보존 방법을 사용자 정의하려면, 필요에 따라 [라이프사이클 관리](https://intl.cloud.tencent.com/document/product/436/17028)를 사용하십시오.

- 타깃 버킷의 객체 복제본이 원본 데이터와 동일한 라이프사이클 규칙을 따르도록 설정하려면, 타깃 버킷에 원본 버킷과 동일한 라이프사이클 규칙을 추가하십시오.
- 타깃 버킷에 라이프사이클 규칙을 설정한 경우, 크로스 버킷 복제로 생성된 객체 복제본의 생성 시간은 원본 객체 생성 시간이며, 복제본이 타깃 버킷에 복제된 시간이 아닙니다. 
- 원본 버킷에 라이프사이클 규칙을 설정하였으며, 복제 중인 객체를 라이프사이클 규칙에 따라 삭제해야 하는 경우, 객체는 계속 복제되고 객체 복제본은 타깃 버킷에 유지됩니다.

#### 버전 관리

버킷 복제 설정 시에는 원본 버킷과 타깃 버킷 모두에 버전 관리 기능을 설정해야 합니다. 버전 관리 기능에 대한 자세한 내용은 [버전 제어 개요](https://intl.cloud.tencent.com/document/product/436/19883)를 참고하십시오. 버전 관리 활성화 후, 버전 관리 비활성화 시 버킷 복제 기능에 대한 영향에 주의해야 합니다.

- 버킷 복제 기능을 활성화한 버킷에 버전 관리 기능을 비활성화하는 경우, COS에서 오류를 반환하며 먼저 버킷 복제 규칙 삭제 후 버전 관리 기능을 비활성화하도록 안내합니다.
- 타깃 버킷에 대한 버전 관리를 비활성화하려고 하면, COS에서 이러한 설정이 크로스 버킷 복제에 영향을 미친다는 메시지를 표시합니다. 버전 관리 비활성화를 진행하면 이 버킷을 타깃 버킷으로 하는 크로스 버킷 복제 규칙이 무효화됩니다.
