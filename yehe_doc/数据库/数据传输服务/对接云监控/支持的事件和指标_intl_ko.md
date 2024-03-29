## 개요
DTS는 Cloud Monitor를 사용하여 데이터 마이그레이션, 동기화 및 구독 작업 중에 이벤트와 메트릭을 모니터링하고 알람 규칙을 설정할 수 있습니다. Cloud Monitor는 이벤트가 트리거되거나 메트릭 예외 발생 즉시 알림을 보내 해당 조치를 취할 수 있도록 합니다.  

> ?현재 이벤트 및 메트릭 모니터링은 MySQL 데이터베이스에서 다른 데이터베이스로의 데이터 마이그레이션, 동기화 및 구독에 대해서만 지원됩니다.

## 지원 이벤트
DTS는 일부 중요한 이벤트에 대한 기본 알람 구성을 지원합니다. 즉, 옵션을 구성하지 않고도 작업이 시작될 때 이벤트를 자동으로 모니터링하고 트리거된 이벤트를 알려줍니다.

| **이벤트 시나리오** | **이벤트 이름**     | **기본 알람 여부** | **설명**                                             |
| ------------ | ---------------- | ---------------- | ---------------------------------------------------- |
| 데이터 마이그레이션     | 데이터 마이그레이션 작업 중단 | 기본 알람         | 데이터 마이그레이션 작업 중단 또는 예외 발생 시 알람이 트리거됩니다. |
| 데이터 동기화     | 데이터 동기화 작업 중단 | 기본 알람         | 데이터 동기화 작업이 중단 또는 예외 발생 시 알람이 트리거됩니다. |
| 데이터 구독     | 데이터 구독 작업 중단 | 기본 알람         | 데이터 구독 작업 또는 예외 발생 시 알림이 트리거됩니다.         |

## 데이터 마이그레이션 지원 메트릭

> ?현재 실시간 모니터링 메트릭 데이터는 증분 마이그레이션 중에만 얻을 수 있습니다.

| **메트릭 이름**  | **단위** | **설명**            |
| ------------------ | ------- | ---------------------------------- |
| 원본 데이터베이스에서 RPS 읽기 | Count/s | DTS가 읽은 원본 데이터베이스의 데이터 행 수/초. |
| 대상 데이터베이스에 작성된 RPS  | Count/s | DTS에 의해 대상 데이터베이스로 마이그레이션된 데이터 행 수/초. |
| 데이터 마이그레이션 시간 지연 | s    | 대상 데이터베이스와 원본 데이터베이스 간의 시간 차이입니다.<br>계산 방법: 대상 데이터베이스의 현재 시간에서 대상 데이터베이스에서 실행 중인 원본 데이터베이스의 최신 binlog Event에 기록된 시간을 뺀 시간. 원본 및 대상 데이터베이스의 시간이 동기화되지 않은 경우 이 값이 정확하지 않을 수 있습니다.<br>‘데이터 마이그레이션 시간 지연’ 계산은 원본 데이터베이스의 증분 binlog에 따라 다릅니다. 따라서 원본 데이터베이스에서 장기간 DDL 또는 DML 작업을 수행하지 않으면 이 메트릭 값이 점차 증가하므로 실제 마이그레이션 시간 지연을 반영할 수 없습니다(값이 ‘-1’이면 기존 데이터가 마이그레이션되었지만 증분 데이터를 새로 고칠 수 없음). 이 경우 원본 데이터베이스에서 SQL문을 실행하여 올바른 메트릭 값을 얻을 수 있도록 메트릭을 새로 고칠 수 있습니다. |
| 데이터 마이그레이션 데이터 지연 | MBytes | 원본 데이터베이스와 대상 데이터베이스 간의 데이터 크기 차이입니다.<br>계산 방법: 원본 데이터베이스의 최신 binlog Event의 파일 오프셋에서 대상 데이터베이스에서 실행 중인 원본 데이터베이스의 최신 binlog Event의 파일 오프셋을 뺀 값. 두 오프셋이 서로 다른 binlog 파일에 있는 경우 이 값이 추정됩니다.<br/>원본 데이터베이스에서 장기간 DDL 또는 DML 작업이 수행되지 않으면 이 메트릭 값이 점차 증가하므로 실제 마이그레이션 데이터 지연을 반영할 수 없습니다(값이 ‘-1’이면 기존 데이터가 마이그레이션되었지만 증분 데이터의 새로고침은 없음). |

## 데이터 동기화 지원 메트릭

> ?현재 실시간 모니터링 메트릭 데이터는 증분 동기화 중에만 얻을 수 있습니다.

| **메트릭 이름**  | **단위** | **설명**            |
| ------------------ | ------- | ---------------------------------- |
| 원본 데이터베이스에서 RPS 읽기 | Count/s | DTS가 읽은 원본 데이터베이스의 데이터 행 수/초. |
| 대상 데이터베이스에 작성된 RPS  | Count/s | DTS에 의해 대상 데이터베이스로 마이그레이션된 데이터 행 수/초. |
| 데이터 동기화 시간 지연  | s    | 대상 데이터베이스와 원본 데이터베이스 간의 시간 차이입니다.<br>계산 방법: 대상 데이터베이스의 현재 시간에서 대상 데이터베이스에서 실행 중인 원본 데이터베이스의 최신 binlog Event에 기록된 시간을 뺀 시간. 원본 및 대상 데이터베이스의 시간이 동기화되지 않은 경우 이 값이 정확하지 않을 수 있습니다.<br>‘데이터 동기화 시간 지연’ 계산은 원본 데이터베이스의 증분 binlog에 따라 다릅니다. 따라서 원본 데이터베이스에서 장기간 DDL 또는 DML 작업을 수행하지 않으면 이 메트릭 값이 점차 증가하므로 실제 동기화 시간 지연을 반영할 수 없습니다(값이 ‘-1’이면 기존 데이터가 마이그레이션되었지만 증분 데이터를 새로 고칠 수 없음). 이 경우 원본 데이터베이스에서 SQL 문을 실행하여 올바른 메트릭 값을 얻을 수 있도록 메트릭을 새로 고칠 수 있습니다. |
| 데이터 동기화 데이터 지연 | MBytes | 원본 데이터베이스와 대상 데이터베이스 간의 데이터 크기 차이입니다.<br>계산 방법: 원본 데이터베이스의 최신 binlog Event의 파일 오프셋에서 대상 데이터베이스에서 실행 중인 원본 데이터베이스의 최신 binlog Event의 파일 오프셋을 뺀 값. 두 오프셋이 서로 다른 binlog 파일에 있는 경우 이 값이 추정됩니다.<br/>장기간 원본 데이터베이스에 DDL 또는 DML 작업이 없으면 이 메트릭이 점차 증가하므로 실제 동기화 데이터 지연을 반영할 수 없습니다(값이 ‘-1’이면 기존 데이터가 동기화되었음을 나타내지만, 증분 데이터를 새로 고치지 않음). |

## 데이터 구독(Kafka 버전) 지원 메트릭

| **메트릭 이름**    | **단위** | **설명**                                                     |
| --------------- | -------- | ------------------------------------------------------------ |
| Binlog 구문 분석 지연 | Count    | 데이터 구독 서비스에서 이미 구문 분석한 binlog Event의 GTID 수와 원본 데이터베이스에서 생성한 최신 binlog Event의 GTID 수 간의 차이입니다. |
| 초당 구문 분석된 트랜잭션 수  | Count/s  | DTS가 원본 데이터베이스 binlog에서 읽고 구문 분석한 트랜잭션 수/초.                     |

## 데이터 구독 지원 메트릭

| **메트릭 이름**       | **단위** | **설명**                                                     |
| ------------------ | -------- | ------------------------------------------------------------ |
| 데이터 파싱 GTID 지연      | Count    | 구독 서비스에서 구문 분석 중인 binlog의 GTID 수와 원본 데이터베이스에서 생성된 최신 binlog의 GTID 수 간의 차이입니다. |
| SDK 승인 시간 지연       | s       | SDK가 메시지를 사용할 때마다 서버에 ack 메시지를 반환합니다. 이 메트릭은 SDK 메시지 생성과 소비 사이의 시간 차이, 즉 SDK에서 마지막 응답 메시지가 SDK에서 생성된 시점과 구독 서버의 머신 시간 사이의 차이입니다. |
| 초당 트랜잭션 수         | Count/s  | 소비자가 처리한 트랜잭션 수/초.                                     |
| 보류 중인 승인 대기열 사용률   | %        | 클라이언트가 사용하는 메시지의 경우 승인 메시지가 서버로 전송되고 이는 보류 중인 승인 대기열에 추가됩니다. 이 측정 단위는 클라이언트에 캐시된 메시지에서 서버가 승인을 보류 중인 메시지의 비율을 나타냅니다.<br>보류 중인 승인 대기열이 가득 찬 경우 이 메트릭 값은 100%가 되어 프로그램 예외로 인해 클라이언트의 메시지에 대해 AckAsComsumed를 호출하는 데 실패했음을 나타냅니다. |
| 내부 파싱 대기열 사용률 | %        | 메시지를 사용하기 전에 클라이언트는 메시지를 구문 분석하고 내부 구문 분석 대기열에 배치합니다. 이 메트릭은 구문 분석 대기열의 사용률을 나타냅니다. |
| 메시지 대기열 사용률     | %        | 클라이언트가 실행 중일 때 구독 서버에서 메시지를 다운로드하고 메시지 대기열에 캐시합니다. 이 측정 단위는 메시지 대기열의 사용률을 나타냅니다. |
