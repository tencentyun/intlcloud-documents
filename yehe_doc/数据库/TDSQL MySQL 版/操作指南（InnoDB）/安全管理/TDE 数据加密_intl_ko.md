## 작업 시나리오
TDSQL for MySQL은 TDE(Transparent Data Encryption) 기능과 함께 제공됩니다. TDE란 데이터의 암호화, 복호화 작업을 사용자에게 투명하게 보여주는 것으로, 데이터 파일에 대한 I/O 암호화 및 복호화를 실시간으로 진행합니다. 데이터를 디스크에 입력하기 전에 암호화하고 디스크에서 메모리를 읽을 때 복호화함으로써 정적 데이터 암호화의 컴플라이언스 요구를 충족할 수 있습니다.

본문은 콘솔에서 데이터 암호화를 활성화하고 데이터를 암호화/복호화하는 방법을 설명합니다.

## 제한 조건
- TDE 기능은 현재 홍콩의 Percona 5.7 및 MySQL 8.0.24에서만 지원됩니다.
>?TDE 암호화 기능을 사용하려면 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 신청할 수 있습니다.
- [Key Management Service](https://intl.cloud.tencent.com/document/product/1030/32774)는 사전에 활성화하거나 TDE 활성화 시 안내에 따라 활성화해야 합니다.
- KMS 키 권한은 사전에 부여하거나 TDE가 활성화된 경우 안내에 따라 부여해야 합니다.

## 주의 사항
- KMS 활성화 후 [Purchase Method](https://intl.cloud.tencent.com/document/product/1030/31967)에 설명된 대로 KMS 요금이 발생할 수 있습니다.
- 활성화한 TDE 암호화 기능은 비활성화할 수 없습니다.
- 재해 복구 읽기 전용 인스턴스가 생성되면 TDE를 활성화할 수 없습니다.
- TDE가 활성화된 후에는 재해 복구 읽기 전용 인스턴스를 생성할 수 없습니다.
- TDE 암호화가 활성화된 후에는 백업 파일에서 데이터베이스 인스턴스를 복구할 수 없습니다. [데이터베이스 롤백](https://intl.cloud.tencent.com/document/product/1042/47382)에 설명된 대로 복구하는 것이 좋습니다.
- TDE 암호화 기능을 활성화하면 정적 데이터의 보안성은 향상되지만 암호화된 데이터베이스에 액세스 시 읽기 및 쓰기 성능에 영향을 미치므로, 실제 상황에 따라 TDE 암호화 기능의 활성화 여부를 선택하시기 바랍니다.
- TDE가 활성화되면 더 많은 CPU 리소스가 소비되고 성능의 약 5%가 손상됩니다.

## 작업 단계
1. [TDSQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)에 로그인합니다. 인스턴스 ID 또는 **작업** 열의 **관리**를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 **데이터 보안** > **데이터 암호화**를 선택하고 ‘암호화 상태’를 켭니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bdb3fb8cccf8b5f8652b5978aba72dd8.png)
3. 팝업 창에서 KMS 서비스 활성화 및 KMS 키 권한을 부여 받고, 키를 선택한 후에 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/308e3a0ea64a40ff6a5372675fba6dc5.png)
4. 데이터 암호화가 활성화된 후 데이터를 암호화하거나 해독할 수 있도록 데이터베이스 테이블에 대한 DDL 작업도 수행해야 합니다. 자세한 내용은 다음과 같습니다:
 - 새 테이블 암호화:
```
CREATE TABLE t1 (c1 INT) ENCRYPTION='Y'
```
 - 기존 테이블 암호화:
```
ALTER TABLE t1 ENCRYPTION='Y'
```
 - 테이블 복호화:
```
ALTER TABLE t1 ENCRYPTION='N'
```

