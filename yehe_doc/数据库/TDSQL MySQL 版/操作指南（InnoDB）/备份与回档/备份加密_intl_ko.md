## 기능 개요
분산형 TDSQL for MySQL은 TDE(Transparent Data Encryption) 기능을 지원합니다. TDE란 데이터의 암호화, 복호화 작업을 사용자에게 투명하게 보여주는 것으로, 데이터 파일에 대한 I/O 암호화 및 복호화를 실시간으로 진행합니다. 데이터를 디스크에 입력하기 전에 암호화하고 디스크에서 메모리를 읽을 때 복호화함으로써 정적 데이터 암호화의 컴플라이언스 요구를 충족할 수 있습니다.

TDE는 홍콩 리전의 Percona 5.7 버전에서만 지원되지만 향후 더 많은 커널 버전에서 사용할 수 있습니다. [TDSQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)의 인스턴스 관리 페이지에서 **데이터 보안** > **데이터 암호화**에 액세스할 수 있습니다.

데이터 암호화가 활성화된 후에는 백업 파일에서 데이터베이스 인스턴스를 복구할 수 없습니다. [데이터베이스 롤백](https://intl.cloud.tencent.com/document/product/1042/47382)에 설명된 대로 복구하는 것이 좋습니다. 
>?데이터 암호화 기능을 사용하려면 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 신청할 수 있습니다.


## 주의 사항
- 현재 KMS가 활성화된 인스턴스에 대해 재해 복구 읽기 전용 인스턴스를 생성할 수 없습니다. KMS에 대한 자세한 내용은 [Getting Started](https://intl.cloud.tencent.com/document/product/1030/32774)를 참고하십시오.
- 활성화한 TDE 암호화 기능은 비활성화할 수 없습니다.
- TDE 암호화 기능을 활성화하면 정적 데이터의 보안성은 향상되지만 암호화된 데이터베이스에 액세스 시 읽기 및 쓰기 성능에 영향을 미치므로, 실제 상황에 따라 TDE 암호화 기능의 활성화 여부를 선택하시기 바랍니다.
- TDE가 활성화되면 더 많은 CPU 리소스가 소비되고 성능의 약 5%가 손상됩니다.
