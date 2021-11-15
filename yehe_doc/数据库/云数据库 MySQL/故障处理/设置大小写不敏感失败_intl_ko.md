
## 현상 설명
데이터베이스 케이스 인센시티브 설정 실패로 다음과 같은 오류가 보고됩니다. 
![](https://main.qcloudimg.com/raw/e10049c280384344318379432bc294fb.png)

## 예상 원인
- DB 테이블 이름에 대문자가 있습니다. 
- 데이터베이스 버전이 8.0입니다. 

## 해결 절차
### 대문자로 쓴 DB 테이블 이름이 있는 경우
해당 인스턴스의 라이브러리, 테이블이 소문자인지 확인하고 대문자 DB 테이블이 있다면 모두 소문자로 변경한 후, lower_case_table_names 매개변수를 수정해야 합니다. 
>! lower_case_table_names 매개변수를 수정하면 데이터베이스가 재시작될 수 있습니다. 
>
- 대문자 테이블 존재 여부 진단
```
select table_schema,table_name from information_schema.tables where   table_schema not in("mysql","information_schema") and (md5(table_name)<>md5(lower(table_name)) or md5(table_schema)<>md5(lower(table_schema)));
```
- 대문자 데이터베이스 존재 여부 진단
```
select SCHEMA_NAME from information_schema.SCHEMATA where md5(SCHEMA_NAME)<>md5(lower(SCHEMA_NAME));
```

### 데이터베이스 버전이 8.0인 경우
데이터베이스 버전이 8.0인 경우, lower_case_table_names 매개변수를 수정할 수 없습니다. 8.0 버전은 기본적으로 대소문자를 구분합니다.
