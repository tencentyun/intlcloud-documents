DTS는 자체 구축한 TencentDB 및 타사 클라우드 데이터베이스의 동기화를 지원합니다. 다음은 구체적인 네트워크 연결 방법입니다.

- 공용 네트워크: 원본 데이터베이스는 공용 IP를 통해 액세스할 수 있습니다.
- CVM에서 자체 구축: 원본 데이터베이스가 [CVM](https://intl.cloud.tencent.com/document/product/213) 인스턴스에 배포됩니다.
- Direct Connect: 원본 데이터베이스는 [Direct Connect](https://intl.cloud.tencent.com/document/product/216)를 통해 VPC와 상호 연결될 수 있습니다. 
- VPN 액세스: 원본 데이터베이스는 [VPN 연결](https://intl.cloud.tencent.com/document/product/1037)을 통해 VPC와 상호 연결될 수 있습니다. 
- VPC: 원본 및 대상 데이터베이스가 모두 Tencent Cloud [VPC](https://intl.cloud.tencent.com/document/product/215)에 배포됩니다. 데이터 동기화 기능은 VPC 액세스 유형을 지원합니다. 사용하려면 [티켓을 제출](https://console.cloud.tencent.com/workorder/category)하여 신청하십시오.
- 데이터베이스: 원본 데이터베이스는 TencentDB 데이터베이스입니다.
- CCN: 원본 데이터베이스는 [CCN](https://intl.cloud.tencent.com/document/product/1003)을 통해 VPC와 상호 연결될 수 있습니다.

타사 클라우드 데이터베이스의 경우 일반적으로 공용 네트워크를 선택하거나 실제 네트워크 조건에 따라 VPC 액세스, DC 또는 CCN을 선택할 수 있습니다.

동기화를 지원하는 데이터베이스는 다음과 같습니다.


| **데이터 흐름 방향**            | **동기화 방향** | **원본 데이터베이스**                       | **대상 데이터베이스**                   | **데이터 초기화 유형**           |
| --------------------- | ------------ | ------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| MySQL > MySQL        | To Tencent Cloud         | <li>자체 구축 MySQL 5.5, 5.6, 5.7, 8.0<li>TencentDB for MySQL 5.5, 5.6, 5.7, 8.0<li>타사(AWS 및 Alibaba Cloud) MySQL 5.5, 5.6, 5.7 | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 | <li>구조 초기화<li>전체 데이터 초기화 |
| MySQL > PostgreSQL | To Tencent Cloud         | TencentDB for MySQL 5.6, 5.7 | 클라우드 데이터 웨어하우스 PostgreSQL CDW PG 1.0.0              | <li>구조 초기화<li>전체 데이터 초기화 |
| MySQL  >   TDSQL-A PostgreSQL버전 | To Tencent Cloud | TencentDB for MySQL 5.6, 5.7 | TDSQL-A for PostgreSQL | <li>구조 초기화<li>전체 데이터 초기화 |
| MySQL > TDSQL-C | To Tencent Cloud         | <li>로컬 자체 구축 MySQL 5.5, 5.6, 5.7<li>TencentDB for MySQL 5.5, 5.6, 5.7<li>타사(Alibaba Cloud 및 AWS) MySQL 5.5, 5.6, 5.7 | Cloud Native Database TDSQL-C 5.7 | <li>구조 초기화<li>전체 데이터 초기화 |
| TDSQL-C > MySQL | To Tencent Cloud | Cloud Native Database TDSQL-C 5.7 | TencentDB for MySQL 5.7, 8.0 | <li>구조 초기화<li>전체 데이터 초기화 |
| TDSQL-C > TDSQL-C | To Tencent Cloud | Cloud Native Database TDSQL-C 5.7 | Cloud Native Database TDSQL-C 5.7 | <li>구조 초기화<li>전체 데이터 초기화 |
| TencentDB for MySQL > 로컬 MySQL | From Tencent Cloud | TencentDB for MySQL 5.5, 5.6, 5.7, 8.0 | MySQL 5.5, 5.6, 5.7, 8.0 | - |

>?
>- Tencent Cloud로는 대상 데이터베이스가 Tencent Cloud 데이터베이스 제품인 시나리오를 나타냅니다. From Tencent Cloud는 대상 데이터베이스가 Tencent Cloud 데이터베이스 제품이 아닌 시나리오를 나타냅니다.
>- 동기화 요구 사항: 원본 및 대상 데이터베이스 중 하나 이상은 Tencent Cloud 데이터베이스 인스턴스여야 합니다.
>- 대상 데이터베이스 버전은 원본 데이터베이스 버전보다 높거나 같아야 합니다.

