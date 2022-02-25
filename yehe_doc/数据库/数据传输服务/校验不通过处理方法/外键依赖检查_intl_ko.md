
## MySQL/TDSQL-C 확인 사항
- 외래 키 종속성은 ‘NO ACTION’, ‘RESTRICT’ 또는 ‘CASCADE’로만 설정할 수 있습니다.
- 일부 테이블 마이그레이션 시 외래 키 종속성이 있는 테이블을 마이그레이션해야 합니다.

## TDSQL MySQL 확인 사항

- 외래 키 종속성은 ‘NO ACTION’ 또는 ‘RESTRICT’로만 설정할 수 있습니다.
- 일부 테이블 마이그레이션 시 외래 키 종속성이 있는 테이블을 마이그레이션해야 합니다.

## 수정 방법

### 외래 키 규칙 수정
MySQL에서 외래 키를 설정할 때 ON DELETE 및 ON UPDATE 열에 대해 4가지 값을 선택할 수 있습니다. 
- ‘CASCADE’: 상위 테이블에서 레코드가 삭제되거나 업데이트되면 관련 레코드도 하위 테이블에서 삭제되거나 업데이트됩니다.
- ‘SET NULL’: 부모 테이블에서 레코드가 삭제되거나 업데이트되면 관련 레코드의 외래 키 필드 열이 자식 테이블에서 ‘null’로 설정됩니다(자식 테이블 외래 키는 ‘not null’로 설정할 수 없음).
- ‘RESTRICT’: 부모 테이블에서 레코드가 삭제되거나 업데이트될 때 자식 테이블의 레코드와 연결되어 있으면 상위 테이블의 삭제 요청이 거부됩니다.
- ‘NO ACTION’: RESTRICT와 유사하게 외래 키가 먼저 확인됩니다.

오류가 발생하면 다음과 같이 수정합니다.
#### Windows
1. [원본 데이터베이스 DMC 플랫폼에 로그인](https://intl.cloud.tencent.com/document/product/236/39353)합니다.
2. 왼쪽의 대상 트리에서 수정할 테이블을 선택하고 열린 테이블 편집 페이지에서 **외래 키** 탭을 클릭하면 아래와 같이 외래 키 매개변수가 수정됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9671fd44db2250287d7e81564637f01f.png)
3. 수정을 완료한 후 **저장**을 클릭합니다.
4. 확인 작업을 다시 실행합니다.

#### Linux
1. [원본 데이터베이스에 로그인](https://intl.cloud.tencent.com/document/product/236/37788)합니다.
2. 기존 외래 키 설정을 삭제합니다.
```
alter table ‘테이블 이름 1’ drop foreign key ‘외래 키 이름1’;
```
3. 외래 키 설정을 다시 추가합니다.
```
alter table ‘테이블 이름1’ add constraint ‘외래 키 테이블 이름2’ foreign key ‘테이블 이름1’(‘열 이름1’) references ‘테이블 이름2’(‘열 이름1’)
on delete cascade on update cascade;
```
4. 확인 작업을 다시 실행합니다.

### 마이그레이션 객체 완성
마이그레이션 작업 구성 수정 시 마이그레이션 객체에 연결된 객체를 선택합니다.
1. [DTS 콘솔](https://console.cloud.tencent.com/dts/migration)에 로그인하고 해당 마이그레이션 **작업**을 선택한 다음, 작업 열에서 **더보기** > **수정**을 클릭합니다. 
2. **마이그레이션 객체**에서 연결된 객체를 확인합니다.
3. 확인 작업을 다시 실행합니다. 

