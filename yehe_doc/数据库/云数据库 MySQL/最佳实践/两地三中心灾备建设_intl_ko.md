본 문서에서는 가용존(AZ) 전체에 인스턴스를 배포하고 원격 재해 복구 인스턴스를 생성하여 2리전 3데이터센터 아키텍처를 설정하는 방법을 설명합니다.

## 2리전 3데이터센터 배포 아키텍처
![](https://qcloudimg.tencent-cloud.cn/raw/1ad2c4f70918774892a6b453c80d3186.png)
- 1리전 2데이터센터:
리전 A의 3존과 5존은 1리전 2데이터센터 아키텍처를 형성합니다. 3존이 실패하면 5존으로 전환하여 데이터베이스를 보호할 수 있습니다.
- 크로스 리전 재해 복구:
리전 A와 B는 교차 지역 재해 복구 아키텍처를 형성합니다. A 리전의 3, 5존에 있는 모든 데이터 센터에 장애가 발생하더라도 B 리전의 데이터 센터로 전환한 후 비즈니스를 계속할 수 있습니다.

## 다중 AZ 배포
TencentDB for MySQL는 다중 AZ 배포를 지원합니다. 단일 AZ 배포 체계와 비교할 때 다중 AZ 배포 체계는 재해 복구 기능이 더 우수하고 데이터베이스 인스턴스 오류, AZ 중단 및 IDC 수준 오류의 영향을 받지 않도록 데이터베이스를 보호할 수 있습니다.

TencentDB for MySQL에서는 여러 AZ가 단일 다중 AZ로 결합되어 데이터베이스 인스턴스의 고가용성 및 장애 조치 기능을 보장합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d36cb036272104a4be5e763ce38a82e2.png)

### 전제 조건
- 인스턴스가 실행 중입니다.
- 인스턴스가 있는 리전에는 최소 2개의 AZ가 있어야 합니다.
- 대상 AZ에 충분한 컴퓨팅 리소스가 있습니다.

### 지원되는 리전 및 AZ
현재 TencentDB for MySQL의 다중 AZ 배포는 광저우, 상하이, 난징, 베이징, 청두, 중국홍콩, 싱가포르, 자카르타, 방콕, 뭄바이, 서울, 도쿄, 버지니아 및 프랑크푸르트 리전에서 지원됩니다. 다른 리전에서 사용 가능한 원본 및 복제본 AZ는 [TencentDB for MySQL 구매 페이지](https://buy.Intl.cloud.tencent.com/cdb)에 표시된 대로입니다.
- 이 기능은 점차 더 많은 리전과 AZ를 지원할 예정입니다.
- 비즈니스 요구 사항에 맞게 다른 리전이나 AZ에 인스턴스를 배포하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청하십시오.

### 요금 설명
이 기능은 무료입니다. 단일 AZ에서 여러 AZ로 인스턴스를 마이그레이션하는 데는 요금이 부과되지 않습니다.

## 크로스 리전 재해 복구 인스턴스
서비스 연속성, 데이터 안정성 및 규정 준수에 대한 요구 사항이 높은 애플리케이션의 경우 TencentDB for MySQL은 리전 간 재해 복구 인스턴스를 제공하여 낮은 비용으로 지속적인 서비스를 제공하고 데이터 안정성을 개선할 수 있는 기능을 향상하는 데 도움이 됩니다.
별도의 데이터베이스 연결 주소를 사용하여 크로스 리전 재해 복구 인스턴스는 더 낮은 비용의 장치 이중화로 근거리 액세스 및 데이터 분석과 같은 다양한 시나리오에 대한 읽기 액세스 기능을 제공할 수 있습니다. 고가용성 원본/복제본 아키텍처는 데이터베이스의 단일 실패 지점을 방지하는 데 도움이 됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bf639c6f2d80718b2c272cfc0008be54.png)

### 요금 설명
재해 복구 인스턴스의 비용은 연결된 원본 인스턴스와 동일합니다.

## 2리전 3데이터센터 아키텍처 설정
### 1단계: 다중 AZ 배포 설정
#### 인스턴스 구매 시 다중 AZ 배포 선택
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb/)에 로그인한 후 인스턴스 리스트에서 **생성**을 클릭하여 구매 페이지로 이동합니다.
2. 구매 페이지에서 지원되는 리전을 선택한 다음 **복제본 AZ**에 대해 원본 AZ와 다른 AZ를 선택합니다.
>?원본/복제본이 서로 다른 AZ에 있는 경우 네트워크 동기화 지연이 2~3ms 증가할 수 있습니다.
>
![](https://qcloudimg.tencent-cloud.cn/raw/1713bdbe69eae9890560c36283cd52ef.png)
3. 모든 항목이 올바른지 확인한 후 **즉시 구매**를 클릭합니다. 결제 후 **인스턴스 세부 정보 페이지 > 가용성 정보**에서 인스턴스의 원본 및 복제본 AZ를 볼 수 있습니다.

#### 기존 인스턴스의 단일 AZ 배포를 다중 AZ 배포로 변경
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb/)에 로그인합니다.
2. 인스턴스 리스트에서 대상 인스턴스의 **작업** 열에 있는 ID 또는 **관리**를 클릭하여 인스턴스 세부 정보 페이지로 이동합니다.
3. 인스턴스 세부 정보 페이지의 **가용성 정보 > 배포 모드**에서 **복제본 AZ 수정**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c0e598dbb2c9459397f62f155b2d7413.png)
4. 팝업 창에서 다중 AZ 배포에 대해 **예**를 선택하고 복제본 AZ를 선택한 다음 **제출**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8730f424e5a67407cc6f966d774f92cf.png)

### 2단계: 크로스 리전 재해 복구 인스턴스 설정
>?재해 복구 인스턴스는 1GB 메모리 및 50GB 디스크 용량 이상 사양의 InnoDB 엔진을 사용하는 MySQL 5.6 이상의 고가용성 GTID 지원 원본 인스턴스에 대해서만 구입할 수 있습니다. 원본 인스턴스가 이 사양보다 낮으면 먼저 업그레이드하십시오.

#### 2.1 재해 복구 인스턴스 생성
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb/)에 로그인한 후, 인스턴스 리스트에서 인스턴스 ID 또는 **작업** 열의 **관리**를 클릭하여 세부 정보 페이지로 이동합니다.
2. 인스턴스 상세 페이지에서 인스턴스의 기본 정보를 확인하여 GTID 기능이 활성화되어 있는지 확인합니다. 인스턴스 아키텍처 다이어그램에서 **재해 복구 인스턴스 추가**를 클릭하여 재해 복구 인스턴스 구매 페이지로 이동합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/45177bca4dd63114c97eee5a45ab72b9.png)
3. 구매 페이지에서 청구 모드, 리전 및 동기화 정책과 같은 재해 복구 인스턴스의 기본 정보를 구성합니다.
 - 동기화 정책이 **즉시 동기화**인 경우 재해 복구 인스턴스가 생성되는 즉시 데이터가 동기화됩니다.
 - 동기화 정책이 **생성 후 동기화**인 경우 인스턴스가 성공적으로 생성된 후 재해 복구 동기화 링크를 구성해야 합니다. 자세한 사용법은 아래의 [동기화 링크 생성](#cjtblj)을 참고하십시오.
>?
>- 생성을 완료하는 데 필요한 시간은 데이터 양에 따라 다르며 생성 중에는 콘솔의 원본 인스턴스에 대해 어떤 작업도 수행할 수 없습니다. 적절한 시기에 하는 것이 좋습니다.
>- 현재 전체 인스턴스 데이터만 동기화할 수 있습니다. 디스크 공간이 충분한지 확인하십시오.
>- 원본 인스턴스가 실행 상태이고 구성 조정 작업, 다시 시작 작업 및 기타 수정 작업이 실행되지 않았는지 확인해야 합니다. 그렇지 않으면 동기화 작업이 실패할 수 있습니다.  
4. 모든 항목이 올바른지 확인한 후 **즉시 구매**를 클릭하고 재해 복구 인스턴스가 전달될 때까지 기다립니다.
5. 인스턴스 리스트로 되돌아갑니다. 인스턴스 상태가 **실행 중**으로 변경되면, 정상적으로 사용할 수 있습니다.

## 2리전 3데이터센터 아키텍처 보기
구성이 완료되면 아래와 같이 데이터베이스가 2리전 3데이터센터 아키텍처로 배포됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/4e541bac303a064366b980080d6178aa.png)