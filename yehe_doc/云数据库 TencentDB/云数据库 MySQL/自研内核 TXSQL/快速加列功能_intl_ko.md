
본 문서는 instant 알고리즘을 통한 데이터 복사 방지와 빠른 칼럼 추가 기능을 소개합니다. 데이터를 복사하지 않고 디스크 용량과 디스크 I/O를 점유하지 않아 비즈니스 피크 시기에 실시간으로 변경할 수 있습니다.

## 제한 조건
- 인스턴스 버전: MySQL 5.7 고가용성 버전과 파이낸스 버전
- 커널 마이너 버전: 20190830 이상
>?인스턴스 구매는 기본적으로 최신 커널의 마이너 버전입니다. 커널 마이너 버전 조회는 [커널 마이너 버전 조회](https://intl.cloud.tencent.com/document/product/236/35995)를 참조하십시오. 커널 버전의 업데이트 상황은 [커널 버전 업데이트 상태](https://intl.cloud.tencent.com/document/product/236/35989)를 참조하십시오.

## 사용 설명
[데이터베이스 로그인](https://intl.cloud.tencent.com/document/product/236/3130), 구문을 빠르게 추가하는 방법은 다음과 같습니다.
```
ALTER TABLE t1 ADD COLUMN c1 int，algorithm=instant;
```
>?
>- innodb_alter_table_default_algorithm 매개변수는 지정한 디폴트의 ALTER TABLE 알고리즘에 사용합니다. INSTANT 설정 시, ALTER TABLE은 algorithm=instant 구문을 설정할 필요가 없습니다. 사용자는 현재 직접 해당 매개변수의 기본값을 수정할 수 없으며, 수정이 필요하면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)로 수정할 수 있습니다.
>- innodb_alter_table_default_algorithm 매개변수는 INPLACE 또는 INSTANT로 설정할 수 있고, 디폴트값은 INPLACE입니다.
