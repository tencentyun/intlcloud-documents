
본 문서는 instant 알고리즘으로 데이터 복사를 막고 대용량 테이블을 빠르게 추가할 수 있는 기능을 소개합니다. 해당 기능은 데이터를 복사하지 않기 때문에 디스크 용량과 디스크 I/O를 점유하지 않으며 작업 피크 시간에도 실시간 변경이 가능합니다.

## 제한 조건
- 인스턴스 버전: MySQL 5.7 이중 노드, 3중 노드
- 커널 마이너 버전: 20190830 이상
>?새로 구매하는 인스턴스는 기본적으로 최신 커널 마이너 버전입니다. 커널 마이너 버전에 대해서는 [커널 마이너 버전 조회](https://intl.cloud.tencent.com/document/product/236/35995)를 참조하십시오. 커널 버전의 업데이트 현황은 [커널 버전 업데이트 현황](https://intl.cloud.tencent.com/document/product/236/35989)을 참조하십시오.

## 사용 설명
[데이터베이스에 로그인](https://intl.cloud.tencent.com/document/product/236/37788)하여 다음 구문을 빠르게 추가합니다.
```
ALTER TABLE t1 ADD COLUMN c1 int, algorithm=instant;
```
>?
>- innodb_alter_table_default_algorithm 매개변수는 기본 ALTER TABLE 알고리즘 지정에 사용됩니다. INSTANT로 설정할 경우 ALTER TABLE은 algorithm=instant 구문을 설정할 필요가 없습니다. 사용자는 현재 해당 매개변수의 기본값을 직접 수정할 수 없으며, 수정이 필요한 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 수정할 수 있습니다.
>- innodb_alter_table_default_algorithm 매개변수는 INPLACE 또는 INSTANT로 설정할 수 있고, 기본값은 INPLACE입니다.
