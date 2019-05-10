사용자는 MongoDB를 사용하는 과정에서 CPU 사용률이 높은 것을 발견했을 경우, 다음 몇 가지 부분으로 점검할 수 있습니다.<br>
1. 먼저 비즈니스에 대해 데이터베이스 조작 빈도가 높은지 확인해야 합니다.
콘솔 모니터링 메트릭을 확인하십시오. 자세한 내용은 다음과 같습니다. 비즈니스의 QPS가 정말로 높은 경우, 인스턴스 구성을 업그레이드해야 하는지 평가하십시오. 비즈니스 QPS가 높지 않다면 스로우 로그가 있는지 점검해야 합니다.
![](https://main.qcloudimg.com/raw/e013e4387e144b8f98ab1de810503c0d.png)


2. 현재 mongod에 스로우 로그가 있는지 확인하십시오.
[TencentDB for MongoDB 콘솔](https://console.cloud.tencent.com/mongodb)에 로그인하여, 인스턴스의 스로우 로그를 확인하십시오. 추상 조회를 선택할 수 있습니다. 자세한 내용은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/19a7b1568cf38f6b493cb5088cfdff93.png)
command, COLLSCAN, IXSCAN, keysExamined, docsExamined 등 키워드를 유의하십시오.


 - command는 스로우 로그에 기록한 작업을 표시합니다.<br>
 - COLLSCAN은 해당 조회가 전체 테이블을 스캔하는 것을 의미합니다. IXSCAN은 인덱스로 스캔하는 것을 의미합니다. 필드에 대한 더 많은 설명은 [MongoDB 공식 웝사이트](https://docs.mongodb.com/manual/reference/explain-results/index.html)를 참조하십시오.<br>
 - keysExamined는 인덱스 스캔 항목을 의미합니다. docsExamined는 문서 스캔 항목을 의미합니다. 더 큰 keysExamined와 docsExamined는 인덱싱이 없다는 것을 의미하거나 인덱스의 구분도가 높지 않음을 의미합니다. 인덱스에 대한 생성 필드를 확인하십시오.<br>
로그에 관한 더 많은 설명은 [MongoDB 공식 웹사이트](https://docs.mongodb.com/manual/reference/log-messages/index.html)를 참조하십시오.
