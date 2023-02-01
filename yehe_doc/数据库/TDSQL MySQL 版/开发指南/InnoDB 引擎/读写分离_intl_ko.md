
TDSQL for MySQL 인스턴스는 다음 모드에서 읽기/쓰기 분리를 지원합니다.
- `/*slave*/`와 같은 복제 주석 플래그를 SQL 문에 추가할 수 있으며 mysql 뒤에 -c 매개변수가 추가되어 `mysql -c -e "/*slave*/sql"`을 구문 분석하여 SQL 문을 복제 서버로 보냅니다.
>?` /*slave:slaveonly*/`, ` /*slave:20*/` 및 ` /*slave:slaveonly,20*/`를 포함한 주석 플래그도 지원됩니다. 여기서 값은 slave가 충족해야 하는 지연 요구 사항을 나타내고 slaveonly는 적합한 slave가 없는 경우 쿼리가 원본 서버로 전송되지 않음을 나타냅니다.
>
```
//소스에서 데이터 읽기//
select * from emp order by sal，deptno desc；
//복제본에서 데이터 읽기//
/*slave*/ select * from emp order by sal，deptno desc；
```
- 읽기 전용 계정으로 보낸 요청은 구성된 속성을 기반으로 복제 서버로 전송됩니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Bpmr055_10.png)
