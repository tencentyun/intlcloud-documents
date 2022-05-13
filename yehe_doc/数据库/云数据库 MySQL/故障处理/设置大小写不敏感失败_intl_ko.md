
## 현상 설명
데이터베이스 케이스 인센시티브 설정 실패로 다음과 같은 오류가 보고됩니다. 
![](https://main.qcloudimg.com/raw/e10049c280384344318379432bc294fb.png)
>?데이터베이스 버전이 8.0인 경우 구매 페이지에서 인스턴스 생성 시에만 테이블 이름의 케이스 센시티브 활성화 여부를 선택할 수 있으며, 인스턴스 생성 후에는 lower_case_table_names 매개변수 수정을 통해 조정할 수 없습니다.

## 예상 원인
DB 테이블 이름에 대문자가 있습니다.

## 처리 단계
해당 인스턴스의 라이브러리, 테이블이 소문자인지 확인하고 대문자 DB 테이블이 있다면 모두 소문자로 변경한 후, lower_case_table_names 매개변수를 수정해야 합니다. 
>!lower_case_table_names 매개변수를 수정하면 데이터베이스가 재시작될 수 있습니다. 
>
- 대문자 테이블 존재 여부 진단
```
select table_schema,table_name from information_schema.tables where   table_schema not in("mysql","information_schema") and (md5(table_name)<>md5(lower(table_name)) or md5(table_schema)<>md5(lower(table_schema)));
```
- 대문자 데이터베이스 존재 여부 진단
```
select SCHEMA_NAME from information_schema.SCHEMATA where md5(SCHEMA_NAME)<>md5(lower(SCHEMA_NAME));
```

