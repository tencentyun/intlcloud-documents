– **백업 용량 비용 관련 문제**
 -  [백업 용량 비용은 어떻게 산정됩니까?](#bfwt1)
 -  [어떻게 하면 백업 용량 비용을 절약할 수 있습니까?](#bfwt2)
- **데이터베이스 백업 관련 문제**
 - [자동 백업은 어떻게 설정합니까?](#bfwt3)
 - [수동 백업 작업을 할 수 없는 이유는 무엇입니까?](#bfwt13)
 - [샤딩 로직 콜드 백업 및 다운로드를 할 수 없는 이유는 무엇입니까?](#bfwt14)
 - [개발자는 데이터를 어떻게 백업해야 합니까?](#bfwt4)
 - [백업 보관 기간이 지난 백업 파일을 다운로드 또는 복원할 수 있습니까?](#bfwt11)
 - [데이터 및 로그를 백업하지 않도록 설정할 수 있습니까?](#bfwt12)
 - [백업 작업은 어떻게 취소합니까?](#bfwt9)
 - [백업을 수동으로 삭제할 수 있습니까?](#bfwt8)
- **백업 복구 관련 문제**
 - [xbstream과 qpress 툴은 어떻게 다운로드합니까?](#bfwt16)
 - [다운로드한 백업 파일을 tar로 압축 해제 시 실패하는 이유는 무엇입니까?](#bfwt15)
 - [백업 다운로드가 느린 경우 어떻게 해결해야 합니까?](#bfwt10)
 - [데이터 백업 파일 다운로드에 실패하는 이유는 무엇입니까?](#bfwt6)
 - [다운로드한 백업 파일을 다른 TencentDB for MySQL 인스턴스 상에 복구할 수 있습니까?](#bfwt7)
 - [기본 버전 인스턴스 백업은 어떻게 복원 또는 마이그레이션합니까?](#bfwt5)


<span id = "bfwt1"></span>
### 백업 용량 요금은 어떻게 산정됩니까?
TencentDB for MySQL은 리전에 따라 일정량의 무료 백업 용량을 제공합니다. 무료 백업 용량의 크기는 해당 리전에 있는 모든 고가용성 및 파이낸스 버전의 인스턴스(마스터 인스턴스 및 재해 복구 인스턴스 포함) 스토리지 용량의 합계입니다.
– 무료 용량을 초과한 부분의 백업 용량 요금에 대한 자세한 내용은 [백업 용량 요금 설명](https://intl.cloud.tencent.com/document/product/236/32344)을 참조하십시오.

<span id = "bfwt2"></span>
### 어떻게 하면 백업 용량 비용을 절약할 수 있습니까?
- 더 이상 사용하지 않는 수동 백업 데이터를 삭제합니다. (수동 백업은 [MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 관리 페이지 > Backup and Restore에서 삭제 가능) 
- 비핵심 비즈니스 데이터의 자동 백업 빈도수를 줄입니다. (콘솔에서 백업 주기와 백업 보관 기간을 조절할 수 있으며, 일주일에 2회 이하로 설정)
>?[롤백 기능](https://intl.cloud.tencent.com/document/product/236/7276)은 백업 주기와 백업 보관 기간 내의 데이터 백업 + 로그 백업(binlog)을 기반으로 하여 자동 백업의 빈도수와 보관 기간을 단축해 인스턴스 데이터의 롤백 기간 범위에 영향을 줄 수 있으므로 백업 설정의 밸런스를 적절히 조절하시기 바랍니다.
>
- 비핵심 비즈니스의 데이터 백업과 로그 백업 보관 기간을 줄입니다. (백업 보관 기간은 7일이면 충분하며, 대부분의 시나리오 요구사항 지원)

| 비즈니스 시나리오             | 백업 보관 기간                                                 |
| -------------------- | ------------------------------------------------------------ |
| 핵심 비즈니스             | 7일-732일 추천                                              |
| 비핵심, 비데이터류 비즈니스 | 7일 추천                                                      |
| 보관 비즈니스             | 데이터 백업 보관 기간은 7일을 권장하며, 실제 비즈니스 요구사항에 따라 수동으로 데이터를 백업하고 사용 완료한 파일은 삭제하기를 권장합니다. |
| 테스트 비즈니스             | 데이터 백업 보관 기간은 7일을 권장하며, 실제 비즈니스 요구사항에 따라 수동으로 데이터를 백업하고 사용 완료한 파일은 삭제하기를 권장합니다. |

<span id = "bfwt3"></span>
### 자동 백업은 어떻게 설정합니까?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb) 인스턴스의 Backup and Restore 페이지에서 설정할 수 있습니다.
![](https://main.qcloudimg.com/raw/4df9e17b3d0d23d3e74f284e1e5efacd.png)

<span id = "bfwt4"></span>
### 개발자는 데이터를 어떻게 자체적으로 백업합니까?
TencentDB for MySQL 인스턴스는 기본적으로 매일 전체 백업을 진행하며, 자세한 내용은 [백업 방법](https://intl.cloud.tencent.com/document/product/236/37796)을 참조하십시오. 임시로 데이터 백업이 필요한 경우 다음 방법을 통해 데이터를 백업할 수 있습니다.
- mysqldump 툴을 사용해 자체적으로 데이터 백업 진행
- 3rd party 툴을 사용해 백업 진행(예: Navicat Premium)
- [phpMyAdmin 로그인](https://intl.cloud.tencent.com/document/product/236/32341) 후, 상단 메뉴 [내보내기]를 통해 데이터 백업 진행

<span id = "bfwt5"></span>
### 기본 버전 인스턴스 백업은 어떻게 복원 또는 마이그레이션합니까?
기본 버전 인스턴스는 스냅샷 백업만 지원하며, [TCCLI로 데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/236/8464)을 참조하여 데이터를 마이그레이션할 수 있습니다.

<span id = "bfwt6"></span>
### 데이터 백업 파일 다운로드에 실패하는 이유는 무엇입니까?
`wget -c '백업 파일 다운로드 주소' -O 사용자 정의 파일명.xb` 명령을 사용하여 백업 파일을 다운로드하는 경우 다운로드 주소를 영문 따옴표 `'` 2개로 묶어야 하며, 이는 프로그램이 주소를 인식하고 오류를 방지하기 위해 필요합니다.

<span id = "bfwt7"></span>
### 다운로드한 백업 파일을 다른 TencentDB for MySQL 인스턴스 상에 복구할 수 있습니까?
해당 작업은 현재 지원하지 않습니다. [DTS의 MySQL 인스턴스 데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/571/34103)을 사용해 별도의 MySQL 인스턴스에 복구하기를 권장합니다.

<span id = "bfwt8"></span>
### 백업을 수동으로 삭제할 수 있습니까?
- 자동 백업은 수동으로 삭제할 수 없으며, 백업 보관 기간을 설정할 수 있습니다. 기간 만료 후에는 자동으로 삭제됩니다.
- 수동 백업은 백업 리스트에서 수동으로 삭제할 수 있으며, 수동 삭제하지 않는 한 영구적으로 보관합니다.
 1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤 인스턴스 이름을 클릭하여 Manage 페이지로 이동한 후 [Backup and Restore] 페이지를 선택합니다.
 2. 백업 리스트의 “Operation” 열에서 [Delete]를 클릭해 삭제합니다.

<span id = "bfwt9"></span>
### 백업 작업은 어떻게 취소합니까?
백업 작업은 취소할 수 없습니다.

<span id = "bfwt10"></span>
### 백업 다운로드가 느린 경우 어떻게 해결해야 합니까?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb) 인스턴스의 Backup and Restore 페이지에서 다운로드 주소를 복사한 후, CDB가 있는 PVC의 CVM(Linux 시스템)에 로그인하여 wget 명령어를 사용해 내부 네트워크 고속 다운로드를 사용하는 것을 권장하며 더욱 효율적입니다.
>? wget 명령어 포맷: wget -c '백업 파일 다운로드 주소' -O 사용자 정의 파일명.xb

<span id = "bfwt11"></span>
### 백업 보관 기간이 초과한 백업 파일을 다운로드 또는 복원할 수 있습니까?
기간이 만료된 백업 세트는 자동으로 삭제되며 다운로드 및 복원할 수 없습니다.
- 필요에 따라 백업 보관 기간을 합리적으로 설정하거나 [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 백업 파일을 로컬에 다운로드하십시오.
- 콘솔에서 인스턴스 데이터를 수동으로 백업할 수도 있으며, 수동 백업 파일은 영구 보관됩니다.
>? 수동 백업은 백업 용량을 점유합니다. 따라서 별도의 비용이 청구되지 않도록 백업 용량을 합리적으로 사용하십시오.

<span id = "bfwt12"></span>
### 데이터 및 로그를 백업하지 않도록 설정할 수 있습니까?
불가능합니다. 그러나 [MySQL 콘솔](https://console.cloud.tencent.com/cdb)을 통해 백업 빈도수를 낮추고 더 이상 사용하지 않는 수동 백업 데이터를 삭제하여 백업 용량 점유율을 줄일 수 있습니다.

<span id = "bfwt13"></span>
### 수동 백업 작업을 할 수 없는 이유는 무엇입니까?
자동 백업 작업 기간을 확인해 주십시오. 인스턴스가 매일 자동 백업되고 있는 경우 수동 백업을 할 수 없습니다.

<span id = "bfwt14"></span>
### 샤딩 로직 콜드 백업 및 다운로드를 할 수 없는 이유는 무엇입니까?
[백업 신규 버전](https://intl.cloud.tencent.com/document/product/236/37796) 업그레이드 후에는 로직 콜드 백업이든 물리적 콜드 백업 기능이든 모두 새로운 압축 알고리즘을 사용하며 일부 다운로드 기능은 일시적으로 사용할 수 없습니다. 수동 백업의 [로직 콜드 백업]>[DB 테이블 지정] 기능을 통해 샤딩 로직 콜드 백업을 완료할 수 있으며 이미 완료한 해당 백업 파일을 다운로드할 수 있습니다.

<span id = "bfwt15"></span>
### 다운로드한 백업 파일을 tar로 압축 해제 시 실패하는 이유는 무엇입니까?
신규 버전 백업 파일은 신규 압축 알고리즘을 사용하여 기존의 tar 툴을 사용해 정상적으로 압축을 해제할 수 없으며, xbstream과 qpress 툴을 사용해 압축 해제할 수 있습니다.
xbstream과 qpress 툴을 사용하여 압축 해제하는 방법에 대한 자세한 내용은 [물리적 콜드 백업으로 데이터베이스 복구](https://intl.cloud.tencent.com/document/product/236/31910) 및 [로직 콜드 백업으로 데이터베이스 복구](https://intl.cloud.tencent.com/document/product/236/31909)를 참조하십시오.

<span id = "bfwt16"></span>
### xbstream과 qpress 툴은 어떻게 다운로드합니까?
- xbstream은 Percona사의 xtrabackup 백업 툴에 속하는 프로그램으로 xbstream을 사용할 경우 먼저 Percona사의 xtrabackup을 설치해야 합니다. yum을 사용한 설치 또는 바이너리 설치 방법을 통해 xbstream을 설치할 수 있습니다.
- [qpress 다운로드 주소](http://www.quicklz.com/), 다운로드 후 tar 명령어를 사용해 qpress 바이너리 파일을 압축 해제합니다.
xtrabackup 및 qpress 설치 방법에 대한 자세한 내용은 [물리적 콜드 백업으로 데이터베이스 복구](https://intl.cloud.tencent.com/document/product/236/31910)를 참조하십시오.

