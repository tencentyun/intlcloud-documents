데이터 구독(Kafka Edition)에서는 [DOWNLOAD](http://kafka.apache.org/downloads)에서 제공되는 Kafka 0.11 이상을 통해 구독 데이터를 사용할 수 있습니다. 이 문서는 데이터 소비 프로세스를 빠르게 테스트하고 데이터 구문 분석 방법을 이해할 수 있도록 Java, Go 및 Python용 클라이언트 소비 Demo 예시를 제공합니다.

구독 작업을 구성할 때 ProtoBuf, Avro 및 Json을 포함하여 구독 데이터의 다른 형식을 선택할 수 있습니다. ProtoBuf와 Avro는 소비 효율성이 높은 이진법 형식을 채택하고 Json은 사용하기 쉬운 경량 텍스트 형식을 채택합니다. 참고용 Demo는 선택한 데이터 형식에 따라 다릅니다.

이 문서는 Json 형식의 Demo를 제공합니다. Demo에는 Json 프로토콜 파일이 이미 포함되어 있으므로 별도로 다운로드할 필요가 없습니다.

> ?
>
> 현재 Json 프로토콜을 통한 데이터 소비는 MySQL 및 TDSQL-C for MySQL에서만 지원됩니다.

## 주의 사항
- **Demo는 소비된 데이터만 출력하지만 그러한 데이터의 사용 지침은 포함되지 않습니다. Demo를 기반으로 고유한 데이터 처리 로직을 작성해야 합니다**. 다른 언어의 Kafka 클라이언트를 사용하여 데이터를 사용하고 구문 분석할 수도 있습니다.
- 현재 사용을 위한 Kafka에 대한 데이터 구독은 Tencent Cloud 사설망을 통해 구현할 수 있지만 공중망에서는 구현할 수 없습니다. 또한 구독된 데이터베이스 인스턴스와 데이터 소비자는 동일한 리전에 있어야 합니다.
- DTS에 내장된 Kafka는 개별 메시지 처리에는 일정한 상한선이 있습니다. 원본 데이터베이스의 단일 데이터 행이 10MB를 초과하면 이 행이 삭제될 수 있습니다.
- DTS에서 Kafka 메시지 구독의 전달 의미는 적어도 한 번(at least once) 메시지를 전달하는 것입니다. 따라서 특별한 경우에 소비된 데이터가 중복될 수 있습니다. 예를 들어 구독 작업이 다시 시작되면 다시 시작한 후 중단 오프셋 전에 원본 Binlog가 당겨져 메시지가 반복적으로 전달됩니다. 등록된 객체 수정 및 비정상 작업 복원과 같은 콘솔 작업은 중복 메시지를 유발할 수 있습니다. 비즈니스가 중복 데이터에 민감한 경우 소비 Demo에서 비즈니스 데이터를 기반으로 중복 제거 로직을 추가해야 합니다.
- 如果您使用过或者熟悉开源订阅工具 Canal，可以选择将这里消费出来的 Json 格式数据转换成 Canal 工具兼容的数据格式，再进行后续处理，我们的 Demo 中已经提供了相关支持，在启动 Demo 的参数中添加参数 trans2canal 即可实现。目前该功能仅限 Java 语言支持。  


## 소비자 Demo 다운로드
| Demo 언어 | TencentDB for MySQL, TDSQL-C for MySQL           |
| ------------- | ------------------------------------------------------------ |
| Go            | [주소](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/consumerDemo-json-go.zip) |
| Java          | [주소](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/consumerDemo-json-java-1.0.1.zip) |
| Python3       | [주소](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/consumerDemo-json-python.zip) |

## Java Demo 사용 설명
컴파일 환경: Maven 및 JDK 8. 원하는 패키지 관리 툴을 선택할 수 있습니다. 다음은 Maven을 예로 들어 설명합니다.
실행 환경: Tencent CVM(구독 인스턴스와 같은 리전이어야만 Kafka 서버의 내부 네트워크 주소에 액세스 가능), JRE8 설치.
작업 순서:
1. 신규 데이터 구독 작업을 생성합니다. 자세한 내용은 [데이터 구독 Kafka 버전](https://intl.cloud.tencent.com/document/product/571/47354)을 참고하십시오.
2. 하나 이상의 소비자 그룹을 생성합니다. 자세한 내용은 [소비자 그룹 추가](https://intl.cloud.tencent.com/document/product/571/39534)를 참조하십시오.
3. Java Demo를 다운로드하고 파일의 압축을 해제합니다.
4. 압축을 푼 디렉터리에 액세스합니다. Maven 모델 및 pom.xml 파일은 필요에 따라 사용할 수 있도록 디렉터리에 배치됩니다.
    Maven을 사용한 패키징: mvn clean package.
5. Demo 실행.
    Maven을 사용하여 패키징 후 대상 폴더 target으로 이동하여 다음 코드를 실행합니다.
    `java -jar consumerDemo-json-1.0-SNAPSHOT.jar --brokers xxx --topic xxx --group xxx --user xxx --password xxx --trans2sql --trans2canal`.
 - 'broker'는 Kafka 데이터 구독을 위한 사설망 액세스 주소이고, 'topic'은 구독 topic이며, [구독 상세 조회](https://intl.cloud.tencent.com/document/product/571/42660)의 안내에 따라 구독 상세페이지에서 확인할 수 있습니다.
 - `group`, `user`, `password`는 소비자 그룹의 이름, 계정, 비밀번호로, [소비자 그룹 관리](https://intl.cloud.tencent.com/document/product/571/39535)의 안내에 따라 소비 관리 페이지에서 확인할 수 있으며,
 - `trans2sql`은 SQL 문으로의 변환 여부를 나타냅니다. java 코드에서 이 매개변수가 전달되면 변환이 활성화됩니다.
 - `trans2canal` 表示是否转换为 Canal 格式打印出来，携带该参数表示转换为 Canal 格式，不携带则不转换。 
6. 소비 상황을 관찰합니다.
![](https://main.qcloudimg.com/raw/fffa3de2a6e38b3752512183e1ffe785.png)

## Golang Demo 사용 설명
컴파일 환경: Golang 1.12 버전 이상, Go Module 환경 설정.
실행 환경: Tencent CVM(구독 인스턴스와 같은 리전이어야만 Kafka 서버의 내부 네트워크 주소에 액세스 가능).
작업 순서:
1. 신규 데이터 구독 작업을 생성합니다. 자세한 내용은 [데이터 구독 Kafka 버전](https://intl.cloud.tencent.com/document/product/571/47354)을 참고하십시오.
2. 하나 이상의 소비자 그룹을 생성합니다. 자세한 내용은 [소비자 그룹 추가](https://intl.cloud.tencent.com/document/product/571/39534)를 참조하십시오.
3. Golang Demo를 다운로드하고 파일의 압축을 해제합니다.
4. 압축을 해제한 디렉터리로 들어가 `go build -o subscribe ./main/main.go`을 실행하여 subscribe 실행 파일을 생성합니다.
5. `./subscribe --brokers=xxx --topic=xxx --group=xxx --user=xxx --password=xxx --trans2sql=true`를 실행합니다.
 - 'broker'는 Kafka 데이터 구독을 위한 사설망 액세스 주소이고, 'topic'은 구독 topic이며, [구독 상세 조회](https://intl.cloud.tencent.com/document/product/571/42660)의 안내에 따라 구독 상세페이지에서 확인할 수 있습니다.
 - `group`, `user`, `password`는 소비자 그룹의 이름, 계정, 비밀번호로, [소비자 그룹 관리](https://intl.cloud.tencent.com/document/product/571/39535)의 안내에 따라 소비 관리 페이지에서 확인할 수 있습니다.
 - `trans2sql`은 SQL 문으로의 변환 여부를 나타냅니다.
6. 소비 상황을 관찰합니다.
![](https://main.qcloudimg.com/raw/c94d9cfe2a62e903a6593e22ce2c60bf.png)

## Python3 Demo 사용 설명
컴파일 실행 환경: Tencent CVM(구독 인스턴스와 같은 리전이어야만 Kafka 서버의 내부 네트워크 주소에 액세스 가능), Python3 설치, pip3(종속 패키지 설치에 사용).
pip3를 사용해 설치하는 종속 패키지:
```
pip install flag
pip install kafka-python
```
작업 순서:
1. 신규 데이터 구독 작업을 생성합니다. 자세한 내용은 [데이터 구독 Kafka 버전](https://intl.cloud.tencent.com/document/product/571/47354)을 참고하십시오.
2. 하나 이상의 소비자 그룹을 생성합니다. 자세한 내용은 [소비자 그룹 추가](https://intl.cloud.tencent.com/document/product/571/39534)를 참조하십시오.
3. Python3 Demo를 다운로드하고 파일의 압축을 해제합니다.
4. `python main.py --brokers=xxx --topic=xxx --group=xxx --user=xxx --password=xxx --trans2sql=1`을 실행합니다.
 - 'broker'는 Kafka 데이터 구독을 위한 사설망 액세스 주소이고, 'topic'은 구독 topic이며, [구독 상세 조회](https://intl.cloud.tencent.com/document/product/571/42660)의 안내에 따라 구독 상세페이지에서 확인할 수 있습니다.
 - `group`, `user`, `password`는 소비자 그룹의 이름, 계정, 비밀번호로, [소비자 그룹 관리](https://intl.cloud.tencent.com/document/product/571/39535)의 안내에 따라 소비 관리 페이지에서 확인할 수 있습니다.
 - `trans2sql`은 SQL 문으로의 변환 여부를 나타냅니다.
5. 소비 상황을 관찰합니다.
![](https://main.qcloudimg.com/raw/6055041985904335b43d7df8f4e75561.png)

## [프로토콜 파일 설명](id:dgxljjj)
Demo 中我们采用 Json 进行序列化，各语言 Demo 中均附带有 Record 定义文件。
Java Demo 中的定义文件路径为 `consumerDemo-json-java\src\main\java\json\FlatRecord.java`。

### Record 中字段类型

| Record 필드      | 설명                                                   |
| ------------------------ | ------------------------------------------------------------ |
| id                       | 전역 증분 ID.                                                 |
| version                  | 프로토콜 버전.                                                   |
| messageType              | 메시지 유형.                                                   |
| fileName                 | binlog 파일 이름.                                              |
| position                 | binlog 오프셋.                                                |
| safePosition             | 트랜잭션이 시작된 binlog 오프셋.                                     |
| timestamp                | binlog의 타임스탬프.                                          |
| gtid                     | 트랜잭션 gtid.                                                  |
| transactionId            | 트랜잭션 ID.                                                    |
| serverId                 | 소스 데이터베이스의 serverId.                                              |
| threadId                 | 소스 데이터베이스의 스레드 ID.                                                |
| sourceType               | 소스 데이터베이스 유형.                                           |
| sourceVersion            | `select version();`과 동일한 소스 데이터베이스 버전.                      |
| schemaName               | 데이터베이스 이름.                                                       |
| tableName                | 테이블 이름.                                                       |
| objectName               | 데이터베이스 이름. 테이블 이름의 값.                                                  |
| columns                  | 열 메타데이터.                                                   |
| oldColumns               | DML 前的列值。输出字符串。如果是 binary、geometry 等类型，则输出16进制。 |
| newColumns               | DML 后的列值。输出字符串。如果是 binary、geometry 等类型，则输出16进制。 |
| sql                      | SQL 문.                                                   |
| executionTime            | DDL 실행 기간.                                                |
| heartbeatTimestamp       | heartbeat 이벤트에서만 유효한 하트비트 메시지의 타임스탬프.                  |
| syncedGtid               | 리졸브된 GTID의 컬렉션.                                           |
| fakeGtid                 | 현재 GTID가 위조되었는지 여부.                                        |
| pkNames                  | 기본 키 필드. DML 문만 이 값을 가질 수 있습니다.                                  |
| readerTimestamp          | 백엔드가 현재 데이터 레코드를 처리하는 데 걸리는 시간(밀리초)입니다.                       |
| tags                     | 일부 추가 필드.                                             |
| tags.lowerCaseTableNames | 테이블 이름의 대소문자 구분.                                             |
| total                    | 메시지가 분할된 경우 총 메시지 세그먼트 수. 이 필드는 현재 버전(version=1)에서 유효하지 않으며 확장을 위해 예약되어 있습니다. |
| index                    | 메시지가 분할된 경우 총 메시지 세그먼트 수. 이 필드는 현재 버전(version=1)에서 유효하지 않으며 확장을 위해 예약되어 있습니다. |

### Record 中 MySQL 列属性
- name: 열 이름.
- dataTypeNumber: binlog에 기록된 데이터의 유형. 값은 [MySQL](https://dev.mysql.com/doc/internals/en/com-query-response.html)을 참고하십시오.
- isKey: 현재 키가 기본 키인지 여부.
- originalType: DDL에 정의된 유형.

### MySQL 数据类型转换逻辑
在 Json 协议中，将 MySQL 类型全部转换成了字符串。
- 对于 varchar 等字符串类型，全部转成了 UTF8 编码。
- 对于数值类型，全部转成了与值相同的字符串，如 "3.0"。
- 对于时间类型，格式为：yyyy-dd-mm hh:MM:ss.milli。
- 对于时间戳类型，输出为毫秒数。
- 对于 binary、blob 等二进制类型，输出为与16进制值相同的字符串，如 "0xfff"。


