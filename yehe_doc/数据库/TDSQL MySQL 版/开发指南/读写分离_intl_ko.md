TDSQL for MySQL 인스턴스는 다음 모드에서 읽기/쓰기 분리를 지원합니다.

- /*slave*/와 같은 주석 플래그를 추가하여 지정된 SQL 문을 slave로 보낼 수 있습니다.
>?` /*slave:slaveonly*/`, ` /*slave:20*/` 및 ` /*slave:slaveonly,20*/`를 포함한 주석 플래그도 지원됩니다. 여기서 값은 slave가 충족해야 하는 지연 요구 사항을 나타내고 slaveonly는 적격한 slave가 없는 경우 쿼리가 기본 서버로 전송되지 않음을 나타냅니다.

- 읽기 전용 계정에서 보낸 요청은 설정된 속성에 따라 보조 서버로 보내집니다.
