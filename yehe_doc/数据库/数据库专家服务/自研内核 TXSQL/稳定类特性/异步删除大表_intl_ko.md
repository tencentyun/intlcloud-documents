## 기능 소개
이 기능은 주로 IO 지터를 피하기 위해 대용량 데이터 파일이 있는 테이블을 삭제하는 데 사용됩니다.

DROP TABLE은 원본 데이터베이스 파일(.ibd)의 이름을 변경하여 새 임시 파일을 만들고 성공을 반환합니다. 임시 파일은 innodb_async_drop_tmp_dir 매개변수로 지정된 디렉토리에 저장되며 백엔드에서 일괄적으로 truncate. 매번 truncate 파일의 크기는 innodb_async_truncate_size 매개변수에 의해 제어됩니다. 비동기 테이블 삭제 기능의 상태는 innodb_async_truncate_work_enabled 매개변수에 의해 제어됩니다.

이 기능은 사용자 작업이 필요하지 않으며 커널에 의해 자동으로 완료됩니다. 그 원리는 테이블이 드롭될 때 테이블의 데이터 파일에 대해 다른 디렉터리에 하드 링크를 생성하는 것이므로 drop table을 실행하면 해당 파일에 대한 하드 링크만 삭제됩니다. 그 후 백엔드 스레드는 하드 링크된 디렉터리에서 삭제해야 하는 파일을 스캔하고 drop 테이블의 데이터 파일을 자동으로 truncate 합니다.

## 지원 버전
- 커널 버전 MySQL 5.6 20220303 이상
- 커널 버전 MySQL 5.7 20190203 이상
- 커널 버전 MySQL 8.0 20200630 이상

## 적용 시나리오
이 기능은 삭제할 테이블 데이터 파일이 매우 큰 시나리오에 적합합니다.

## 사용 설명
- MySQL 5.6 및 5.7의 경우 innodb_async_truncate_work_enabled 매개변수를 ON으로 설정하여 DROP TABLE의 비동기 모드를 활성화할 수 있습니다. 기본값은 OFF입니다.
- MySQL 8.0의 경우 innodb_table_drop_mode 매개변수를 ASYNC_DROP으로 설정하여 DROP TABLE의 비동기 모드를 활성화할 수 있습니다. 기본값은 SYNC_DROP입니다.
- 매번 truncate 파일의 크기는 innodb_async_truncate_size 매개변수에 의해 제어됩니다(MySQL 5.6에서는 지원되지 않음).
- [FAST DDL](https://intl.cloud.tencent.com/document/product/236/43489)의 지시에 따라 innodb_fast_ddl 매개변수를 활성화하면 빅 테이블의 비동기 삭제를 보다 효율적으로 만들 수 있습니다.

<dx-tabs>
::: MySQL 5.6 매개변수 설명
| 매개변수 이름                             | 동적 | 유형   | 기본 | 매개변수 값 범위                        | 설명                            |
| ---------------------------------- | ---- | ------ | ---- | ------------------------- | ------------------------------ |
| innodb_async_truncate_work_enabled | Yes  | string |  OFF   | ON/OFF      | 빅 테이블을 비동기식으로 삭제할지 여부입니다.          |
:::
::: MySQL 5.7 매개변수 설명
| 매개변수 이름                             | 동적 | 유형   | 기본 | 매개변수 값 범위                        | 설명                            |
| ---------------------------------- | ---- | ------ | ---- | ------------------------- | ------------------------------ |
| innodb_async_truncate_work_enabled | Yes  | string |  OFF   | ON/OFF      | 빅 테이블을 비동기식으로 삭제할지 여부입니다.          |
| innodb_async_truncate_size         | Yes  | int    | 5.7, 20210630 이하 버전, 기본값: 128<br>5.7, 20211030 이상 버전, 기본값: 64  | 5.7, 20210630 및 이전 버전, 범위: 128MB-2048MB<br>버전 5.7, 20211030 이상 버전, 범위: 16MB-256MB | 비동기화 DROP TABLE 백그라운드 truncate 파일 크기/회(단위 MB) |
:::
::: MySQL 8.0 매개변수 설명
| 매개변수 이름                             | 동적 | 유형   | 기본 | 매개변수 값 범위                        | 설명                            |
| ---------------------------------- | ---- | ------ | ---- | ------------------------- | ------------------------------ |
| innodb_table_drop_mode | Yes  | string |  SYNC_DROP   | SYNC_DROP/ASYNC_DROP    | 빅 테이블을 비동기식으로 삭제할지 여부입니다.          |
| innodb_async_truncate_size         | Yes  | int    | 128  | 128 - 168 | DROP TABLE의 비동기 모드가 활성화된 후 백엔드에서 매번 truncate 파일의 크기입니다. 단위: MB |
:::
</dx-tabs>

>?현재 상기 매개변수의 값을 직접 수정할 수 없습니다. 필요한 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하여 도움을 받으십시오.
>

