사용자는 MongoDB를 사용하는 과정에서 요청 지연이 분명히 길어지는 것을 발견했을 경우, 다음 절차를 통해 점검할 수 있습니다. <br>
1. 인스턴스의 요청 지연 모니터링 메트릭에 이상이 있는지 확인하십시오.
인스턴스의 모니터링 데이터를 확인하십시오. 다음과 같이 지연 모니터링 메트릭은 일반적으로 요청이 액세스 레이어에 도달할 때부터 처리 완료 후 클라이언트까지 리턴하는 시간을 반영합니다. 요청 지연이 높은 경우, mongod에 스로우 로그가 있는지 확인해야 합니다.
![](https://main.qcloudimg.com/raw/d67c9fad80b03829168fbd92ad095378.png)

 다음 절차를 참조하십시오. <br>
2. 현재 mongod에 스로우 로그가 있는지 확인하십시오.
[TencentDB for MongoDB 콘솔](https://console.cloud.tencent.com/mongodb)에 로그인하여, 인스턴스의 스로우 로그를 확인하십시오. 추상 조회를 선택할 수 있습니다. 자세한 내용은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/19a7b1568cf38f6b493cb5088cfdff93.png)
command, COLLSCAN, IXSCAN, keysExamined, docsExamined 등 키워드를 유의하십시오. 로그에 관한 더 많은 설명은 [MongoDB 공식 웹사이트](https://docs.mongodb.com/manual/reference/log-messages/index.html)를 참조하십시오.
주의해야 할 키워드는 다음과 같습니다.
 - command는 스로우 로그에 기록한 작업을 표시합니다.
 - COLLSCAN은 해당 조회가 전체 테이블을 스캔하는 것을 의미합니다. IXSCAN은 인덱스로 스캔하는 것을 의미합니다. 필드에 대한 더 많은 설명은 [MongoDB 공식 웝사이트](https://docs.mongodb.com/manual/reference/explain-results/index.html)를 참조하십시오.<br>
 - keysExamined는 인덱스 스캔 항목을 의미합니다. docsExamined는 문서 스캔 항목을 의미합니다. 더 큰 keysExamined와 docsExamined는 인덱싱이 없다는 것을 의미하거나 인덱스의 구분도가 높지 않음을 의미합니다. 인덱스에 대한 생성 필드를 확인하십시오.<br>


3. 포그라운드에서 인덱스를 생성하기 때문에 요청이 잠겨 있는지 확인하십시오.
비즈니스 조회에 사용되는 인덱스에 문제가 없다면, 비즈니스 피크 기간에 포그라운드에서 인덱스를 생성했는지를 확인하십시오. 집합이 인덱스를 생성할 때, 기본적으로 포그라운드 방식(백그라운드 옵션 값: False)을 사용합니다. 해당 조작은 포그라운드에서 인덱스 생성을 완료할 때까지 다른 모든 작업을 차단합니다. 백그라운드 방식으로 인덱스를 생성하면 인덱스 생성 시간 동안 MongoDB가 정상적으로 읽기/쓰기 작업 서비스를 제공할 수 있습니다. 그러나, 이 방식으로 인덱스를 생성하면 인덱스 생성 시간이 길어집니다. 인덱스 생성 옵션에 대한 자세한 설명은 [MongoDB 공식 웹사이트](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/)를 참조하십시오.<br>
currentOp 명령을 통해 현재 인덱스의 진행 상황을 확인할 수 있습니다. 구체적인 명령은 다음과 같습니다.


	db.currentOp(
        {
          $or: [
            { op: "command", "query.createIndexes": { $exists: true } },
            { op: "insert", ns: /\.system\.indexes\b/ }
          ]
        }
        )
다음과 같이 msg 필드는 현재 인덱스의 진행 상황을 의미하며 locks 필드는 해당 작업의 잠금 유형을 의미합니다. 잠금 기능에 관한 더 자세한 설명은 [MongoDB 공식 웹사이트](https://docs.mongodb.com/v3.2/reference/database-profiler/)를 참조하십시오.<br>
![](https://main.qcloudimg.com/raw/355b6c06539ad6a5e3980b90bd200bf0.png)
![](https://main.qcloudimg.com/raw/155583329a2eb2a99575a2b5ce0b8647.png)<br>

4. mongos에 과부하가 발생했는지 확인하십시오.
지연 모니터링 메트릭은 일반적으로 요청이 액세스 레이어에 도달할 때부터 처리 완료 후 클라이언트로 반환될 때까지의 시간을 반영합니다. mongod에 스로우 작업이 없는데 요청 지연이 높은 경우, mongos의 과부하로 인한 것일 수도 있습니다. 이러한 상황이 발생하는 원인은 몇 가지가 있습니다. 예를 들어, 비즈니스가 순간에 다량 연결을 생성하거나 여러 샤딩 데이터를 합계해야 할 경우, mongos 과부하를 초래할 수 있습니다. 이 때는 mongos를 다시 시작할 수 있습니다. 콘솔에서 mongos를 다시 시작할 수 있고 다음 그림을 참조하십시오.<br>
![](https://main.qcloudimg.com/raw/0ab109e9a0adad49c3d96660132ea290.png)
> ! mongos를 다시 시작하면 모든 인스턴스의 연결을 다시 시작하는 순간에 중단합니다. 그러나 비즈니스를 다시 연결하면 됩니다. 비즈니스에 대해 지속적인 영향을 끼치지 않습니다.
