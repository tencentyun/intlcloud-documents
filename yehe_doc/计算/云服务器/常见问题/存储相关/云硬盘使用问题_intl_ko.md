### 데이터 디스크는 어떻게 조회하나요?
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm)에 로그인합니다.
2. 왼쪽 사이드바에서 [CBS]를 선택하여 CBS 관리 페이지에 접속합니다.
3. [속성] 열을 클릭하고 [**데이터 디스크**]를 선택한 뒤 [확인]을 클릭하면 관련 리전의 모든 데이터 디스크를 조회할 수 있습니다.

### Windows 시스템을 Linux 시스템으로 재설치한 후, 기존 NTFS 유형의 데이터 디스크를 읽기 및 쓰기 하려면 어떻게 해야 하나요?
Windows의 파일 시스템은 일반적으로 NTFS 혹은 FAT32 포맷을 사용하고, Linux의 파일 시스템은 EXT 시리즈의 포맷을 사용합니다. CVM의 운영 체제를 Windows에서 Linux로 재설치하면 운영 체제 유형은 변하지만, CVM의 데이터 디스크는 이전 시스템의 포맷을 따릅니다. 재설치 후 데이터 디스크 파일 시스템에 액세스 불가 현상이 발생할 수 있으니, 포맷 변환 소프트웨어를 사용해 기존 데이터를 읽도록 합니다. 자세한 작업 방식은 [Windows를 Linux로 재설치한 후 기존 NTFS 유형의 데이터 디스크 읽기 및 쓰기](https://intl.cloud.tencent.com/document/product/213/3857)를 참조 바랍니다.

### Linux 시스템을 Windows 시스템으로 재설치한 후, 기존 EXT 유형의 데이터 디스크를 읽으려면 어떻게 해야 하나요?
Windows의 파일 시스템은 일반적으로 NTFS 혹은 FAT32 포맷을 사용하고, Linux의 파일 시스템은 EXT 시리즈의 포맷을 사용합니다. 운영 체제를 CVM에서 Linux로 재설치하면 운영 체제 유형은 변하지만, CVM의 데이터 디스크는 이전 시스템의 포맷을 따릅니다. 재설치 후 데이터 디스크 파일 시스템에 액세스 불가 현상이 발생할 수 있으니, 포맷 변환 소프트웨어를 사용해 기존 데이터를 읽도록 합니다. 자세한 작업 방식은 [Linux를 Windows로 재설치한 후 기존 EXT 유형의 데이터 디스크 읽기](https://intl.cloud.tencent.com/document/product/213/3856)를 참조 바랍니다.

### 프리미엄 CBS, SSD CBS와 향상형 SSD CBS는 어떤 차이점이 있나요?

 ;
- 프리미엄 CBS: Tencent Cloud에서 출시한 하이브리드형 스토리지 유형으로, 캐시 메커니즘을 사용하여 솔리드 스테이트 스토리지에 가까운 고성능 스토리지 능력을 선보이며, 3중 백업의 분산형 메커니즘을 통해 데이터의 신뢰성을 보장하였습니다. 프리미엄 CBS는 데이터의 신뢰성에 대한 요구가 높고, 성능에 대한 요구는 중간 정도인 중소형 시나리오에 적합합니다.
- SSD CBS: Full NVMe SSD 스토리지 미디어를 기반으로, 3중 백업의 분산형 메커니즘을 사용하여 저지연성, 높은 랜덤 IOPS, 높은 처리량의 I/O 능력과 더불어 무려 99.9999999%의 데이터 보안성을 자랑하는 고성능 스토리지입니다. SSD CBS는 I/O 성능에 대한 요구가 비교적 높은 시나리오에 적합합니다.
- 향상형 SSD CBS: Tencent Cloud에서 차세대 스토리지 엔진 기반의 디자인과 Full NVMe SSD 스토리지 미디어 및 최신 네트워크 인프라를 기반으로 제공한 제품 유형으로, 3중 백업의 분산형 메커니즘을 사용하여 저지연성, 높은 랜덤 IOPS, 높은 처리량의 I/O 능력과 더불어 무려 99.9999999%의 데이터 보안성을 자랑하는 스토리지 서비스입니다. 향상형 SSD CBS는 대형 데이터베이스, NoSQL 등 딜레이 시간에 대한 요구가 매우 높은 I/O 집약형 시나리오에 적합합니다.


현재 정상 판매되고 있는 세 가지 CBS 과금 정책은 리전에 따라 다르므로, 응용 프로그램의 요구 및 과금 예산에 따라 필요한 CBS 유형을 선택하시기 바랍니다. 자세한 내용은 [CBS 가격 리스트](https://intl.cloud.tencent.com/document/product/362/2413)를 참조 바랍니다.
디스크 유형 및 성능에 관한 더 많은 정보는 [CBS 유형](https://intl.cloud.tencent.com/document/product/362/31636)을 참조 바랍니다.

### 디스크 성능을 테스트하려면 어떻게 해야 하나요?
FIO를 사용하여 CBS에 대해 스트레스 테스트 및 검증을 진행하시기를 권장합니다. 자세한 작업 방식은 [클라우드 디스크 성능 측정](https://intl.cloud.tencent.com/document/product/362/6741)을 참조 바랍니다.

### CBS에서 자주 쓰는 작업에는 어떤 것들이 있나요?
CBS에 관련된 자주 쓰는 작업은 [CBS 작업 개요](https://intl.cloud.tencent.com/document/product/362/33140)를 참조 바랍니다.

###CBS의 사용 현황과 잔여 용량을 조회하려면 어떻게 해야 하나요?
CVM 인스턴스에 로그인한 후, CVM 인스턴스에서 CBS의 사용 현황과 잔여 용량을 조회할 수 있습니다. 현재 CVM의 콘솔 및 CVM의 API를 통해서는 해당 정보를 조회할 수 없습니다.

### 단독으로 생성한 CBS가 인스턴스와 함께 릴리스된 원인은 무엇인가요??
CBS는 마운트할 때 인스턴스와 함께 자동 릴리스 여부를 설정할 수 있습니다. [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs/index) 혹은 API 중에서 [CBS 속성 변경](https://intl.cloud.tencent.com/document/product/362/15659)을 통해 CVM을 인스턴스와 함께 릴리스되는 기능 활성화 또는 비활성화를 설정할 수 있습니다.

### CBS를 마운트한 후 파티션 및 포맷은 어떻게 하나요?
자세한 작업 방식은 [CBS 초기화(2TB 미만)](https://intl.cloud.tencent.com/document/product/362/31597) 또는 [CBS 초기화(2TB 이상)](https://intl.cloud.tencent.com/document/product/362/31598)을 참조 바랍니다.




