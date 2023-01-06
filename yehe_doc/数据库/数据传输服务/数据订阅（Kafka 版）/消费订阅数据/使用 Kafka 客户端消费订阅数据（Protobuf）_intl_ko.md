## 작업 시나리오

데이터 구독(Kafka Edition)에서는 [DOWNLOAD](http://kafka.apache.org/downloads)에서 제공되는 Kafka 0.11 이상을 통해 구독 데이터를 사용할 수 있습니다. 이 문서는 데이터 소비 프로세스를 빠르게 테스트하고 데이터 구문 분석 방법을 이해할 수 있도록 Java, Go 및 Python용 클라이언트 소비 Demo 예시를 제공합니다.

구독 작업을 구성할 때 ProtoBuf, Avro 및 Json을 포함하여 구독 데이터의 다른 형식을 선택할 수 있습니다. ProtoBuf와 Avro는 소비 효율성이 높은 이진법 형식을 채택하고 Json은 사용하기 쉬운 경량 텍스트 형식을 채택합니다. 참고용 Demo는 선택한 데이터 형식에 따라 다릅니다.

본 문서는 Protobuf 형식의 Demo를 제공합니다. Demo에는 Protobuf 프로토콜 파일이 이미 포함되어 있으므로 별도로 다운로드할 필요가 없습니다. [Protobuf 프로토콜 파일](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe.proto)을 직접 다운로드하는 경우 코드 생성에 Protobuf 3.X를 사용하여 데이터 구조가 호환되는지 확인하십시오.

## 주의 사항

- **Demo는 소비된 데이터만 출력하지만 그러한 데이터의 사용 지침은 포함되지 않습니다. Demo를 기반으로 고유한 데이터 처리 로직을 작성해야 합니다**. 다른 언어의 Kafka 클라이언트를 사용하여 데이터를 사용하고 구문 분석할 수도 있습니다.
- 현재 사용을 위한 Kafka에 대한 데이터 구독은 Tencent Cloud 사설망을 통해 구현할 수 있지만 공중망에서는 구현할 수 없습니다. 또한 구독된 데이터베이스 인스턴스와 데이터 소비자는 동일한 리전에 있어야 합니다.
- DTS에서 Kafka 메시지 구독의 전달 의미는 적어도 한 번(at least once) 메시지를 전달하는 것입니다. 따라서 특별한 경우에 소비된 데이터가 중복될 수 있습니다. 예를 들어 구독 작업이 다시 시작되면 다시 시작한 후 중단 오프셋 전에 원본 Binlog가 당겨져 메시지가 반복적으로 전달됩니다. 등록된 객체 수정 및 비정상 작업 복원과 같은 콘솔 작업은 중복 메시지를 유발할 수 있습니다. 비즈니스가 중복 데이터에 민감한 경우 소비 Demo에서 비즈니스 데이터를 기반으로 중복 제거 로직을 추가해야 합니다.


## 소비자 Demo 다운로드
| Demo 언어 | TencentDB for MySQL, MariaDB, TDSQL-C MySQL           | TDSQL MySQL                                | TDSQL PostgreSQL                             |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Go            | [다운로드](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_go_demo_1.2.0.zip) | [다운로드](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_subscribe_kafka_go_demo_1.0.3.zip) | [다운로드](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_postgresql_subscribe_kafka_go_demo_1.0.0.zip) |
| Java          | [다운로드](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_java_demo_1.2.0.zip) | [다운로드](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_subscribe_kafka_java_demo_1.0.3.zip) | [다운로드](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_postgresql_subscribe_kafka_java_demo_1.0.0.zip) |
| Python3       | [다운로드](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_python_demo_1.2.0.zip) | [다운로드](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_subscribe_kafka_python_demo_1.0.3.zip) | [다운로드](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_postgresql_subscribe_kafka_python_demo_1.0.0.zip) |


## Java Demo 사용 설명
컴파일 환경: Maven 또는 Gradle 패키지 관리 툴, JDK8.
실행 환경: Tencent CVM(구독 인스턴스와 같은 리전이어야만 Kafka 서버의 내부 네트워크 주소에 액세스 가능), JRE8 설치.
작업 순서:
1. 데이터 구독 작업(NewDTS)을 생성합니다. 자세한 내용은 [TDSQL for MySQL 데이터 구독 생성](https://www.tencentcloud.com/document/product/571/47354)을 참고하십시오.
2. 하나 이상의 소비자 그룹을 생성합니다. 자세한 내용은 [소비자 그룹 추가](https://intl.cloud.tencent.com/document/product/571/39534)를 참고하십시오.
3. Java Demo를 다운로드하고 파일의 압축을 해제합니다.
4. 압축 해제 후 디렉터리로 들어간 뒤 사용하기 쉽도록 디렉터리에 Maven 모델 파일, pom.xml 파일 및 Gradle 관련 구성 파일을 각각 세팅하여 사용자가 필요에 따라 선택하도록 합니다.
  - Maven을 사용한 패키징: mvn clean package.
  - Gradle을 사용한 패키징: gradle fatJar 패키징 및 모든 종속 포함, 또는 gradle jar 패키징.
5. Demo 실행.
 - Maven으로 프로젝트 패키징 후 target 폴더로 이동하여 `java -jar sub_demo-1.0-SNAPSHOT-jar-with-dependencies.jar --brokers=xxx --topic=xxx --group=xxx--user=xxx --password=xxx --trans2sql`을 실행합니다.
 - Gradle로 프로젝트 패키징 후 build/libs폴더로 이동하여 `java -jar sub_demo-with-dependencies-1.0-SNAPSHOT.jar --brokers=xxx --topic=xxx --group=xxx--user=xxx --password=xxx --trans2sql`을 실행합니다.
여기서 `broker`는 Kafka에 대한 데이터 구독을 위한 사설망 액세스 주소이고 `topic`은 구독 topic이며 [구독 상세 조회](https://intl.cloud.tencent.com/document/product/571/42660)의 안내에 따라 구독 세부 정보 페이지에서 볼 수 있습니다. `group`, `user`, `password`는 소비자 그룹의 이름, 계정, 비밀번호이며 [소비자 그룹 관리](https://intl.cloud.tencent.com/document/product/571/39535)의 안내에 따라 소비 관리 페이지에서 조회할 수 있습니다. `trans2sql`은 SQL 문으로의 변환 활성화 여부를 나타냅니다. java 코드에서 이 매개변수가 전달되면 변환이 활성화됩니다.
6. 소비 상황을 관찰합니다.
![](https://main.qcloudimg.com/raw/fffa3de2a6e38b3752512183e1ffe785.png)

컴파일 및 패키징에 IDE를 사용할 수도 있습니다. 패키징 후 프로젝트 루트 디렉터리의 target 폴더에서 sub_demo-1.0-SNAPSHOT-jar-with-dependencies를 볼 수 있습니다. 이는 필요한 모든 종속성을 포함하는 실행 가능한 jar 패키지입니다.

## Golang Demo 사용 설명
컴파일 환경: Golang 1.12 버전 이상, Go Module 환경 설정.
실행 환경: Tencent CVM(구독 인스턴스와 같은 리전이어야만 Kafka 서버의 내부 네트워크 주소에 액세스 가능).
작업 순서:
1. 데이터 구독 작업(NewDTS)을 생성합니다. 자세한 내용은 [TDSQL for MySQL 데이터 구독 생성](https://www.tencentcloud.com/document/product/571/47354)을 참고하십시오.
2. 하나 이상의 소비자 그룹을 생성합니다. 자세한 내용은 [소비자 그룹 추가](https://intl.cloud.tencent.com/document/product/571/39534)를 참고하십시오.
3. Golang Demo를 다운로드하고 파일의 압축을 해제합니다.
4. 압축을 해제한 디렉터리에 액세스하고 `go build -o subscribe ./main`을 실행하여 subscribe 실행 파일을 생성합니다.
5. `./subscribe --brokers=xxx --topic=xxx --group=xxx --user=xxx --password=xxx --trans2sql=true`를 실행합니다.
  여기서 `broker`는 Kafka에 대한 데이터 구독을 위한 사설망 액세스 주소이고 `topic`은 구독 topic이며 [구독 상세 조회](https://intl.cloud.tencent.com/document/product/571/42660)의 안내에 따라 구독 세부 정보 페이지에서 볼 수 있습니다. `group`, `user`, `password`는 소비자 그룹의 이름, 계정, 비밀번호이며 [소비자 그룹 관리](https://intl.cloud.tencent.com/document/product/571/39535)의 안내에 따라 소비 관리 페이지에서 조회할 수 있습니다. `trans2sql`은 SQL 문으로의 변환 활성화 여부를 나타냅니다.
6. 소비 상황을 관찰합니다.
  ![](https://main.qcloudimg.com/raw/c94d9cfe2a62e903a6593e22ce2c60bf.png)

## Python3 Demo 사용 설명
컴파일 실행 환경: Tencent CVM(구독 인스턴스와 같은 리전이어야만 Kafka 서버의 내부 네트워크 주소에 액세스 가능), Python3 설치, pip3(종속 패키지 설치에 사용).
pip3를 사용해 설치하는 종속 패키지:
```
pip install flag
pip install kafka-python
pip install protobuf
```
작업 순서:
1. 데이터 구독 작업(NewDTS)을 생성합니다. 자세한 내용은 [TDSQL for MySQL 데이터 구독 생성](https://www.tencentcloud.com/document/product/571/47354)을 참고하십시오.
2. 하나 이상의 소비자 그룹을 생성합니다. 자세한 내용은 [소비자 그룹 추가](https://intl.cloud.tencent.com/document/product/571/39534)를 참고하십시오.
3. Python3 Demo를 다운로드하고 파일의 압축을 해제합니다.
4. `python main.py --brokers=xxx --topic=xxx --group=xxx --user=xxx --password=xxx --trans2sql=1`을 실행합니다.
여기서 `broker`는 Kafka에 대한 데이터 구독을 위한 사설망 액세스 주소이고 `topic`은 구독 topic이며 [구독 상세 조회](https://intl.cloud.tencent.com/document/product/571/42660)의 안내에 따라 구독 세부 정보 페이지에서 볼 수 있습니다. `group`, `user`, `password`는 소비자 그룹의 이름, 계정, 비밀번호이며 [소비자 그룹 관리](https://intl.cloud.tencent.com/document/product/571/39535)의 안내에 따라 소비 관리 페이지에서 조회할 수 있습니다. `trans2sql`은 SQL 문으로의 변환 활성화 여부를 나타냅니다.
5. 소비 상황을 관찰합니다.
![](https://main.qcloudimg.com/raw/6055041985904335b43d7df8f4e75561.png)

## [Demo 핵심 로직 설명](id:dgxljjj)

### 메시지 생성 로직

이 섹션에서는 소비 로직을 더 잘 이해하는 데 도움이 되는 메시지 생성 로직에 대해 설명합니다.
Protobuf는 직렬화에 사용됩니다. 각 프로그래밍 언어에 대한 Demo에는 몇 가지 주요 데이터 구조를 정의하는 Protobuf 정의 파일이 포함되어 있습니다. Envelope는 결국 전송된 Kafka 메시지의 구조입니다. Entry는 개별 구독 이벤트의 구조입니다. Entries는 Entry 구조의 집합입니다. 다음은 이들의 관계입니다.

![](https://qcloudimg.tencent-cloud.cn/raw/3dcceab6ea08686edf64c0517019d70d.png)

생성 프로세스는 다음과 같습니다.

1. Binlog 메시지를 풀링해 개별 Binlog Event를 하나의 Entry 구조체로 인코딩합니다.
```
message Entry { //Entry는 개별 구독 이벤트의 구조로, 이벤트는 MySQL의 binlog event와 유사함
    Header header = 1;  //이벤트 헤더
    Event event   = 2;  //이벤트 본문
}


message Header {
    int32       version        = 1;   //Entry의 프로토콜 버전
    SourceType  sourceType     = 2;   //원본 데이터베이스 유형(예: MySQL 및 Oracle)
    MessageType messageType    = 3;   //BEGIN, COMMIT, DML 등의 메시지 유형 즉, Event 유형
    uint32 timestamp           = 4;   //원본 binlog의 Event 타임스탬프
    int64  serverId            = 5;   //원본 데이터베이스의 serverId
    string fileName            = 6;   //원본 binlog의 파일 이름
    uint64 position            = 7;   //원본 binlog 파일의 이벤트 오프셋
    string gtid                = 8;   //현재 트랜잭션의 gtid
    string schemaName          = 9;   //수정된 schema
    string tableName           = 10;  //수정된 table
    uint64 seqId               = 11;  //글로벌 증분 일련 번호
    uint64 eventIndex          = 12;  //대규모 event가 샤딩된 경우 샤드 번호는 0부터 시작하며, 이 매개변수는 현재 버전에서 의미가 없으며 향후 사용을 위해 예약되어 있음
    bool   isLast              = 13;  //현재 샤드가 샤드된 event의 마지막 샤드인지 여부; 그렇다면 값은 true, 이 매개변수는 현재 버전에서 의미가 없으며 향후 사용을 위해 예약되어 있음
    repeated KVPair properties = 15;
}


message Event {
    BeginEvent      beginEvent      = 1;  //binlog의 begin 이벤트
    DMLEvent        dmlEvent        = 2;  //binlog의 dml 이벤트
    CommitEvent     commitEvent     = 3;  //binlog의 commit 이벤트
    DDLEvent        ddlEvent        = 4;  //binlog의 ddl 이벤트
    RollbackEvent   rollbackEvent   = 5;  //rollback 이벤트, 이 매개변수는 현재 버전에서 의미가 없으며 향후 사용을 위해 예약되어 있음
    HeartbeatEvent  heartbeatEvent  = 6;  //원본 데이터베이스에서 정기적으로 보내는 하트비트 이벤트
    CheckpointEvent checkpointEvent = 7;  //구독 백엔드에 추가된 checkpoint 이벤트는 10초마다 자동으로 생성되며 Kafka 생산 및 소비 오프셋 관리에 사용됨
    repeated KVPair properties      = 15;
}
```
2. 메시지의 양을 줄이기 위해 여러 Entry를 병합합니다. Entry가 병합된 구조는 Entries이며, Entries.items 필드는 Entry 시퀀스 리스트입니다. 병합 수량은 병합 후 Kafka 단일 메시지 크기 제한을 넘지 않는 것을 기준으로 계산합니다. 단일 Event가 크기 제한을 초과한 경우에는 병합되지 않고 Entries 내의 유일한 단독 Entry가 됩니다.
```
message Entries {
        repeated Entry items = 1; //entry list
}
```
3. Protobuf를 사용하여 Entries를 이진 배열로 인코딩합니다.
4. Entries의 이진 배열을 Envelope의 data 필드에 삽입합니다. 단일 Binlog Event의 크기가 너무 커 이진 배열이 Kafka 단일 메시지 크기 제한을 초과할 경우, 이를 여러 세그먼트로 분할하여 Envelope에 로드합니다.
Evelope.total와 Envelope.index는 각각 Envelope 구조의 총 수와 현재 Envelope 구조의 일련 번호(0부터 시작)를 기록합니다.
```
message Envelope {
        int32  version                  = 1; //data 콘텐츠가 디코딩되는 방식을 결정하는 protocol version
        uint32 total                    = 2;
        uint32 index                    = 3;
        bytes  data                     = 4; //여기서 version은 1이며 data가 PB 형식으로 직렬화된 Entries임을 표시
        repeated KVPair properties      = 15;
}
```
5. 앞서 생성한 1개 또는 여러 개의 Envelope을 순서대로 Protobuf 인코딩한 뒤, Kafka 파티션으로 전달합니다. 동일한 Entries가 분할되어 만들어진 여러 개의 Envelope를 차례대로 같은 파티션으로 전달합니다.

### 메시지 소비 로직

다음은 소비 로직에 대한 간략한 설명입니다. Tencent Cloud에서 제공하는 3가지 언어의 Demo는 모두 동일한 프로세스를 따릅니다.

1. Kafka 소비자를 생성합니다.
2. 소비를 실행합니다.
3. 원본 메시지를 차례대로 소비하고 메시지의 파티션에 따라 파티션에 상응하는 partitionMsgConsumer 객체를 찾으면, 해당 객체가 메시지를 처리합니다.
4. partitionMsgConsumer는 원본 메시지를 Envelope 구조로 역직렬화 합니다.
```
	// Kafka 메시지의 Value를 Envelope으로 변환
	envelope := subscribe.Envelope{}
	err := proto.Unmarshal(msg.Value, &envelope)
```
5. partitionMsgConsumer는 Envelope에 기록된 index와 total에 따라 하나 또는 다수의 메시지를 Envlope.index가 Envelope.total-1(위의 소비 생산 로직을 참조하면 하나의 완전한 Entries를 수신했음을 의미)과 같아질 때까지 소비합니다.
6. 수신된 연속적인 여러 Envelope의 data 필드를 순서대로 조합합니다. 조합된 이진 배열을 Protobuf를 사용해 Entries로 디코딩합니다.
```
	if envelope.Index == 0 {
		pmc.completeMsg = envelope
	} else {
        // Entries의 분할된 이진법 시퀀스를 연결함
		pmc.completeMsg.Data = append(pmc.completeMsg.Data, envelope.Data...)
	}
	if envelope.Index < envelope.Total-1 {
		return nil
	}
	// Envelope.Data를 Entries로 역직렬화
	entries := subscribe.Entries{}
	err = proto.Unmarshal(pmc.completeMsg.Data, &entries)

```
7. Entries.items를 순서대로 처리하고 원본 Entry 구조를 출력하거나 SQL 명령으로 변환합니다.
8. Checkpoint 메시지(10초에 한 번씩 구독 백엔드에서 Kafka에 작성하는 특별 메시지)가 소비되면 소비자로부터 Kafka 메시지 오프셋을 제출합니다. 

## 데이터베이스 필드 매핑 및 저장

이 섹션에서는 데이터베이스 필드 유형과 Protobuf 프로토콜에 정의된 데이터 유형 간의 매핑을 설명합니다.
MySQL과 같은 원본 데이터베이스의 필드 값은 Protobuf 프로토콜의 다음 데이터 구조에 저장됩니다.

```
message Data {
     DataType     dataType = 1;
     string       charset  = 2;  //bv에 값이 저장된 DataType_STRING의 인코딩(문자열) 유형
     string       sv       = 3;  //DataType_INT8/16/32/64/UINT8/16/32/64/Float32/64/DataType_DECIMAL의 문자열 값
     bytes        bv       = 4;  //DataType_STRING/DataType_BYTES의 값
}
```
여기에서 DataType 필드는 저장된 필드 유형을 의미하며 다음 이미지와 같은 열거 값을 얻을 수 있습니다.
```
enum DataType {
     NIL     = 0; //값은 NULL
     INT8    = 1;
     INT16   = 2;
     INT32   = 3;
     INT64   = 4;
     UINT8   = 5;
     UINT16  = 6;
     UINT32  = 7;
     UINT64  = 8;
     FLOAT32 = 9;
     FLOAT64 = 10;
     BYTES   = 11;
     DECIMAL = 12;
     STRING  = 13;
     NA      = 14; //값이 존재하지 않음 (N/A)
}
```
여기에서 bv 필드에는 STRING과 BYTES 유형의 이진법 표기가, sv 필드에는 INT8/16/32/64/UINT8/16/32/64/DECIMAL 유형의 문자열 표기가, charset 필드에는 STRING의 컴파일 유형이 저장됩니다.

MySQL/TDSQL의 원본 유형과 DataType의 매핑 관계는 다음과 같습니다(UNSIGNED 수정자에 대한 MYSQL_TYPE_INT8/16/24/32/64는 각각 UINT8/16/32/32/64로 매핑).

> ?
> - `DATE`，`TIME`，`DATETIME` 유형은 시간대를 지원하지 않습니다.
> - `TIMESTAMP` 유형은 시간대를 지원합니다. 이 유형의 필드에 대해 시스템은 저장할 때 현재 시간대를 UTC(Universal Time Coordinated)로 변환하고 쿼리할 때 UTC를 다시 현재 시간대로 변환합니다.
> - "MYSQL_TYPE_TIMESTAMP" 및 "MYSQL_TYPE_TIMESTAMP_NEW" 필드에는 시간대 정보가 있으며, 데이터 소비 시 직접 변환할 수 있습니다. 예를 들어, DTS에서 출력되는 시간 데이터의 형식은 "2021-05-17 07:22:42 +00:00"과 같이 시간대가 포함된 문자열이며 여기서 "+00:00"은 UTC 시간을 나타냅니다. 데이터를 구문 분석하고 변환할 때 시간대 정보를 고려해야 합니다.

| MySQL 필드 유형(TDSQL는 MySQL과 동일한 유형 지원) | 해당 Protobuf DataType 열거 값 |
| ------------------------------------------- | ----------------------------- |
| MYSQL_TYPE_NULL                             | NIL                           |
| MYSQL_TYPE_INT8                             | INT8                          |
| MYSQL_TYPE_INT16                            | INT16                         |
| MYSQL_TYPE_INT24                            | INT32                         |
| MYSQL_TYPE_INT32                            | INT32                         |
| MYSQL_TYPE_INT64                            | INT64                         |
| MYSQL_TYPE_BIT                              | INT64                         |
| MYSQL_TYPE_YEAR                             | INT64                         |
| MYSQL_TYPE_FLOAT                            | FLOAT32                       |
| MYSQL_TYPE_DOUBLE                           | FLOAT64                       |
| MYSQL_TYPE_VARCHAR                          | STRING                        |
| MYSQL_TYPE_STRING                           | STRING                        |
| MYSQL_TYPE_VAR_STRING                       | STRING                        |
| MYSQL_TYPE_TIMESTAMP                        | STRING                        |
| MYSQL_TYPE_DATE                             | STRING                        |
| MYSQL_TYPE_TIME                             | STRING                        |
| MYSQL_TYPE_DATETIME                         | STRING                        |
| MYSQL_TYPE_TIMESTAMP_NEW                    | STRING                        |
| MYSQL_TYPE_DATE_NEW                         | STRING                        |
| MYSQL_TYPE_TIME_NEW                         | STRNG                         |
| MYSQL_TYPE_DATETIME_NEW                     | STRING                        |
| MYSQL_TYPE_ENUM                             | STRING                        |
| MYSQL_TYPE_SET                              | STRING                        |
| MYSQL_TYPE_DECIMAL                          | DECIMAL                       |
| MYSQL_TYPE_DECIMAL_NEW                      | DECIMAL                       |
| MYSQL_TYPE_JSON                             | BYTES                         |
| MYSQL_TYPE_BLOB                             | BYTES                         |
| MYSQL_TYPE_TINY_BLOB                        | BYTES                         |
| MYSQL_TYPE_MEDIUM_BLOB                      | BYTES                         |
| MYSQL_TYPE_LONG_BLOB                        | BYTES                         |
| MYSQL_TYPE_GEOMETRY                         | BYTES                         |

