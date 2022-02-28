연결 보호는 proxy가 백엔드 데이터베이스에서 연결 해제되었을 때 클라이언트와 proxy 간의 연결을 그대로 유지하므로 백엔드 데이터베이스에 예외가 있는 경우 등에도 proxy가 영향을 받지 않습니다.

proxy가 SQL을 실행하는 동안 데이터베이스에서 연결이 끊어지면 proxy는 SQL과 관련된 모든 연결(자신과 클라이언트 간의 연결 제외)을 닫고 오류를 표시합니다.
```c++
ER_PROXY_TRANSACTION_ERROR // 트랜잭션 중
ER_PROXY_CONN_BROKEN_ERROR // 비 트랜잭션
```

#### 솔루션
- proxy가 백엔드 데이터베이스에서 연결 해제되고 session이 ‘트랜잭션’ 진행 중 상태인 경우 다음과 같이 수정할 수 있습니다(아래의 모든 오류 코드는 ER_PROXY_TRANSACTION_ERROR).
![](https://main.qcloudimg.com/raw/2698586724f600292b4af375192fdd5d.png)

- proxy가 백엔드 데이터베이스에서 연결이 끊겼고 세션이 ‘XA 트랜잭션’ 진행 중 상태인 경우 다음과 같이 수정할 수 있습니다(아래의 모든 오류 코드는 ER_PROXY_TRANSACTION_ERROR).
![](https://main.qcloudimg.com/raw/f927b13caa1157e6262dae2cfdd9cea0.png)

#### 시간 초과 설정
>?proxy가 트랜잭션 실행 중에 백엔드 데이터베이스에서 연결을 끊고 제한 시간이 경과하기 전에 트랜잭션을 롤백하지 못하면 proxy는 클라이언트에서 연결이 끊어집니다.
>
시간 초과 매개변수는 proxy 구성 파일에서 다음과 같이 설정됩니다.
```json
<server_close timeout="60"/>
```
