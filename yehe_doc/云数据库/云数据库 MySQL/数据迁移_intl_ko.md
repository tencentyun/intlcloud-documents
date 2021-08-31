
### 로컬에 있는 SQL 파일을 어떻게 MySQL 데이터베이스에 가져오나요?
>?TencentDB for MySQL 고가용성 버전과 파이낸스 버전 인스턴스만 SQL 파일 가져오기 기능을 지원합니다.
>
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 인스턴스 이름을 클릭해 관리 페이지로 들어갑니다.
2. [데이터베이스 관리]>[데이터베이스 리스트]>[데이터 가져오기]를 클릭하여 가져올 파일을 선택한 후, 타깃 데이터베이스를 선택해 가져옵니다.
>?가져온 SQL 파일은 파일당 2GB를 초과할 수 없으며, 파일명은 알파벳, 숫자, 언더바만 허용됩니다.
>
![](https://main.qcloudimg.com/raw/a8854e74caebb9c69d831dc1583c10c0.png)
자세한 내용은 [SQL 파일 가져오기](https://intl.cloud.tencent.com/document/product/236/8466)를 참조하십시오.

### 데이터베이스 데이터는 어떻게 내보내나요?
- 백업 데이터 내보내기가 필요한 경우, [콘솔](https://console.cloud.tencent.com/cdb)에서 인스턴스 이름을 클릭해 관리 페이지에 들어간 후 [백업 복구] 페이지를 선택해 다운로드하십시오.
- 실시간 데이터 내보내기가 필요한 경우, [읽기 전용 인스턴스](https://intl.cloud.tencent.com/document/product/236/7270)를 구매하여 인스턴스를 연결한 후 mysqldump 툴을 사용해 실시간 데이터를 획득할 수 있습니다.

### 기존 데이터베이스가 대략 7GB 정도인 경우 가장 빠르게 TencentDB for MySQL에 마이그레이션하는 방법은 무엇인가요?
[데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/571/34103) 기능 사용을 권장하며, 소스 라이브러리에 직접 연결하여 데이터를 동기화할 수 있습니다.
