## 기능 소개
현재 행 형식에 대한 압축과 로그 페이지에 대한 압축이 있지만, 이 두 가지 압축 방법은 테이블의 일부 큰 필드와 기타 많은 작은 필드를 처리하기 때문에 압축과 동시에 작은 필드는 자주 읽기/쓰기 됩니다. 큰 필드의 액세스 빈도가 낮은 경우, 읽기 및 쓰기 액세스 시 컴퓨팅 리소스의 불필요한 낭비가 많이 발생합니다.

칼럼 압축 기능은 액세스 빈도가 높은 큰 필드를 압축하면서 액세스 빈도가 높지 않은 작은 필드는 압축하지 않을 수 있습니다. 이로써 전체 행 필드의 스토리지 공간을 줄일 수 있을 뿐만 아니라 읽기 및 쓰기 액세스 효율을 높일 수 있습니다.

예를 들어, 직원 테이블: `create table employee(id int, age int, gender boolean, other varchar(1000) primary key (id))`, `id, age, gender`의 작은 필드에 자주 액세스하는 반면, 'other' 대형 필드에 대한 액세스 빈도가 상대적으로 낮은 경우, 'other' 칼럼은 압축된 칼럼으로 생성될 수 있습니다. 일반적인 상황에서는 `other`에 대한 읽기 및 쓰기만 칼럼의 압축 및 압축 해제를 트리거하고 다른 칼럼에 대한 액세스는 칼럼의 압축 및 압축 해제를 트리거하지 않습니다. 이를 통해 행 데이터 스토리지 크기를 더욱 줄여 액세스 빈도가 높은 작은 필드 속도를 높이고, 스토리지 용량이 비교적 크고 액세스 빈도가 낮은 필드의 스토리지 용량을 축소할 수 있게 됩니다.

## 지원 버전
커널 버전 MySQL 5.7 20210330 이상

## 적용 시나리오
테이블에 소량의 큰 필드와 다른 많은 작은 필드가 있는데 작은 필드의 액세스 빈도는 높은 반면 큰 필드 액세스 빈도는 낮은 경우 큰 필드를 압축 칼럼으로 설정할 수 있습니다.

## 사용 설명
### 지원되는 데이터 유형
1. `BLOB`(`TINYBLOB`, `MEDIUMBLOB`, `LONGBLOB` 포함)
2. `TEXT`(`TINYTEXT`, `MEDUUMTEXT`, `LONGTEXT` 포함)
3. `VARCHAR`
4. `VARBINARY`

>!`LONGBLOB`과 `LONGTEXT`의 최대 길이는 $2^{32}-2$까지 지원되며, 이는 공식 [String Type Storage Requirements](https://dev.mysql.com/doc/refman/5.7/en/storage-requirements.html)가 지원하는 $2^{32}-1$ 보다 1바이트 적습니다.

### 지원되는 DDL 구문 유형
공식 [테이블 구문](https://dev.mysql.com/doc/refman/5.7/en/create-table.html)와 비교했을 때, `column_definition`의 `COLUMN_FORMAT` 정의가 변경되었습니다. 동시에 칼럼 압축은 Innodb 스토리지 엔진 유형 테이블만 지원됩니다.
```sql
      column_definition:
        data_type [NOT NULL | NULL] [DEFAULT default_value]
          [AUTO_INCREMENT] [UNIQUE [KEY]] [[PRIMARY] KEY]
          [COMMENT 'string']
          [COLLATE collation_name]
          [COLUMN_FORMAT {FIXED|DYNAMIC|DEFAULT}|COMPRESSED=[zlib]]  # COMPRESSED 압축된 칼럼 키
          [STORAGE {DISK|MEMORY}]
          [reference_definition]
```

간단한 예시는 다음과 같습니다.
```javascript
CREATE TABLE t1(
  id INT PRIMARY KEY,
  b BLOB COMPRESSED
);
```

이 때, 압축 알고리즘은 생략합니다. 기본적으로 'zlib' 압축 알고리즘이 선택되어 있습니다. 또한 지정된 압축 알고리즘 키워드를 표시할 수도 있습니다. 현재는 'zlib' 압축 알고리즘만 지원됩니다.
```javascript
CREATE TABLE t1(
  id INT PRIMARY KEY,
  b BLOB COMPRESSED=zlib
);
```

지원되는 DDL 구문은 다음과 같이 요약됩니다.
**create table 방면:**

| DDL                                         | 압축 속성 상속 여부 |
| ------------------------------------------- | ---------------- |
| `CREATE TABLE t2 LIKE t1;`                  | Y                |
| `CREATE TABLE t2 SELECT * FROM t1;`         | Y                |
| `CREATE TABLE t2(a BLOB) SELECT * FROM t1;` | N                |

**alter table 방면:**

| DDL                                               | 설명                 |
| ------------------------------------------------- | -------------------- |
| `ALTER TABLE t1 MODIFY COLUMN a BLOB;`            | 압축 칼럼을 비압축으로 변경 |
| `ALTER TABLE t1 MODIFY COLUMN a BLOB COMPRESSED;` | 비압축 칼럼을 압축으로 변경 |

 
### 새 변수 설명

| 매개변수 이름                                  | 동적 | 유형    | 기본값 | 매개변수 값 범위      | 설명                                                         |
| --------------------------------------- | ---- | ------- | ---- | --------------- | ------------------------------------------------------------ |
| innodb_column_compression_zlib_wrap     | Yes  | bool    | TRUE | true/false   | 활성화 시 데이터의 zlib 헤더와 zlib 테일이 생성되고 adler32 인증을 진행합니다.    |
| innodb_column_compression_zlib_strategy | Yes  | Integer | 0    | [0,4]           | 칼럼 압축에 사용되는 압축 정책. 최소값: 0, 최대값: 4. 0 - 4는 각각 zlib의 압축 정책 Z_DEFAULT_STRATEGY, Z_FILTERED, Z_HUFFMAN_ONLY, Z_RLE 및 Z_FIXED에 해당합니다 .<br>일반적으로 Z_DEFAULT_STRATEGY는 텍스트 데이터에 가장 적합하고 Z_RLE는 이미지 데이터에 가장 적합합니다. |
| innodb_column_compression_zlib_level    | Yes  | Integer | 6    | [0,9]           | 칼럼 압축에 사용되는 압축 수준. 최소값: 0, 최대값: 9. 0은 압축하지 않음을 의미하며, 값이 클수록 압축된 더 작게 압축되지만 압축 시간은 길어집니다. |
| innodb_column_compression_threshold     | Yes  | Integer | 256  | [0, 0xffffffff] | 칼럼 압축에 사용되는 압축 임계값. 최소값: 1, 최대값: 0xffffffff, 단위: 바이트. 길이가 이 값 이상이면 데이터가 압축되며, 그렇지 않으면 원본 데이터가 변경되지 않고 그대로 유지되고 압축 헤더만 추가됩니다. |
| innodb_column_compression_pct           | Yes  | Integer | 100  | [1, 100]        | 칼럼 압축에 사용되는 압축률. 최소값: 1, 최대값: 100. 단위: 백분율. **압축 후 데이터 크기 / 압축 전 데이터 크기**가 이 값보다 작으면 데이터가 압축되며, 그렇지 않으면 원본 데이터가 변경되지 않고 그대로 유지되고 압축 헤더만 추가됩니다. |


### 상태 설명 추가

| 이름                         | 유형    | 설명                                                |
| ---------------------------- | ------- | ---------------------------------------------------------- |
| `Innodb_column_compressed`   | Integer | 칼럼 압축의 압축 횟수. 비압축 형식과 압축 형식의 두 가지 상태 포함    |
| `Innodb_column_decompressed` | Integer | 칼럼 압축의 압축 횟수. 비압축 형식과 압축 형식의 두 가지 상태 포함 |

### 오류 설명 추가

| 이름                                                         | 범위                       | 설명                                                  |
| ------------------------------------------------------------ | ------------------------------- | ------------------------------------------------------------ |
| `Compressed column '%-.192s' can't be used in key specification` | 압축 칼럼 이름 지정                  | 인덱싱된 칼럼에 대한 압축 속성 지정 불가                                 |
| `Unknown compression method: %s"`                            | DDL 명령에 지정된 압축 알고리즘 이름 | `create table` 또는 `alter table` 시 `zlib` 이외의 잘못된 압축 알고리즘 지정 |
| `Compressed column '%-.192s' can't be used in column format specification` | 압축 칼럼 이름 지정                  | 동일 칼럼에 `COLUMN_FORMAT` 속성이 지정되어 있으면 압축 속성을 지정할 수 없으며, `COLUMN_FORMAT`은 NDB에서만 사용됨 |
| `Alter table ... discard/import tablespace not support column compression` | \                 | 칼럼 압축이 있는 테이블은 `Alter table ... discard/import tablespace` 명령 실행 불가 |

### 성능
전체 성능은 DDL과 DML의 두 가지 측면으로 나뉩니다.
DDL의 경우 sysbench를 사용하여 테스트합니다:
- 칼럼 압축은 COPY 알고리즘의 DDL 성능에 비교적 큰 영향을 미치며 압축 후 성능은 이전보다 7 - 8배 느려집니다.
- inplace에 미치는 영향은 압축된 데이터의 크기에 따라 달라지며, 압축 후 전체 데이터 크기를 줄이면 DDL의 성능이 향상되고 그렇지 않으면 성능이 일정 수준 저하됩니다.
- instant 에서는, 칼럼 압축은 이러한 유형의 DDL에 거의 영향을 미치지 않습니다.

DML 측면: 가장 일반적인 압축 시나리오(압축 비율 1:1.8)를 고려합니다. 8개의 컬럼을 갖는 테이블이 존재하며, 테이블에 큰 varchar 컬럼이 존재합니다. 삽입된 데이터 길이는 1에서 6000 사이로 균일하게 임의적이며, 삽입된 랜덤 문자는 0-9 및 a - b 사이입니다. 기타 칼럼의 데이터 유형은 char(60) 또는 int입니다. 비압축 칼럼 삽입, 삭제, 쿼리에 대해서는 10% 미만의 향상 효과가 있고, 비압축 칼럼 업데이트의 경우에는 10% 미만의 감소 효과가 있습니다. 압축 칼럼 업데이트의 경우에는 15% 미만의 성능 저하가 있습니다. 이것은 업데이트 프로세스 동안 MySQL이 먼저 행의 값을 읽은 다음 행의 업데이트된 값을 쓰기 때문입니다. 전체 업데이트 프로세스는 압축 해제 및 압축을 트리거하는 반면 삽입 및 쿼리는 한 번만 압축 또는 압축 해제됩니다.

### 주의 사항
1. 로직 내보내기의 경우, 로직 내보내기 시 create table에는 여전히 Compressed 관련 키워드가 수반됩니다. 따라서 가져올 때 TencentDB for MySQL 내에서 지원됩니다. 기타 MySQL 브랜치 및 공식 버전:
   - 공식 버전 번호 5.7.18 미만이며 바로 가져올 수 있습니다.
   - 공식 버전 번호 5.7.18 이상이며 로직 내보내기 후 압축 키워드를 제거해야 합니다.
2. DTS를 다른 클라우드나 사용자에게 내보낼 때 binlog 동기화 과정 중 비호환성 문제가 발생할 수 있으므로 압축된 키워드를 수반한 DDL 명령을 건너뛸 수 있습니다.

