
데이터 구독 Kafka 버전에서는 0.11 버전 이상의 Kafka 클라이언트를 통해 구독 데이터를 직접 소비할 수 있습니다. 본 문서에서는 Java, Go, Python 세 가지 언어의 클라이어트 소비자 Demo를 제공합니다.

## 소비자 Demo 다운로드(TencentDB for MySQL, MariaDB)
다음 표를 참조하여 데이터 구독 Kafka 버전 클라이언트의 소비자 Demo 코드를 다운받으십시오.

| Demo 언어 | 다운로드 주소                                                     |
| ------------- | ------------------------------------------------------------ |
| Go            | [주소](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_go_demo_1.1.1.zip) |
| Java          | [주소](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_java_demo_1.1.1.zip) |
| Python3       | [주소](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_python_demo_1.1.1.zip) |

## 소비자 Demo 다운로드(TDSQL MySQL 버전)
다음 표를 참조하여 데이터 구독 Kafka 버전 클라이언트의 소비자 Demo 코드를 다운받으십시오.

| Demo 언어 | 다운로드 주소                                                     |
| ------------- | ------------------------------------------------------------ |
| Go          | [주소](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_subscribe_kafka_go_demo_1.0.0.zip) |
| Java        | [주소](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_subscribe_kafka_java_demo_1.0.1.zip)  |
| Python   | [주소](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_subscribe_kafka_python_demo_1.0.1.zip) |

## Protobuf 프로토콜 파일 다운로드
| 프로토콜 파일 | 다운로드 주소                                             |
| ------------- | ------------------------------------------------------------ |
| Protobuf      | [주소](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe.proto) |


## 매개변수 설정 설명
| 매개변수       | 설명                        |
| ---------- | --------------------------- |
| brokerlist | 데이터 구독 Kafka의 내부 네트워크 액세스 주소 |
| topic      | 데이터 구독 채널의 구독 topic     |
| group      | 소비자 그룹 명칭                  |
| user        | 소비자 그룹 계정 이름                |
| password   | 소비자 그룹 비밀번호 변경                  |
| trans2sql  |  SQL 명령으로의 전환 여부    |


## [Demo 핵심 로직 설명](id:dgxljjj)
### 로직 생성
다음은 소비 로직 관련 사용자의 이해를 돕기 위해 메시지 생성 로직에 대한 간략한 설명입니다.
Protobuf 직렬화 방식을 적용하였으며, 모든 언어 Demo에 Protobuf 정의 파일을 첨부하였습니다. 파일에서는 몇 가지 핵심 구조에 대해 다음과 같이 정의하고 있습니다. Envelope는 최종 전송되는 Kafka 메시지 구조이고, Entry는 단일 구독 이벤트 구조이며, Entries는 여러 Entry의 집합입니다.

생성 프로세스는 다음과 같습니다.
1. Binlog 메시지를 풀링해 개별 Binlog Event를 하나의 Entry 구조체로 인코딩합니다.
![](https://main.qcloudimg.com/raw/5e956452e68b1fed8c2a32c0207dc887.png)
2. 메시지의 양을 줄이기 위해 여러 Entry를 병합합니다. Entry가 병합된 구조는 Entries이며, Entries.items 필드는 Entry 시퀀스 리스트입니다. 병합 수량은 병합 후 Kafka 단일 메시지 크기 제한을 넘지 않는 것을 기준으로 계산합니다. 단일 Event가 크기 제한을 초과한 경우에는 병합되지 않고 Entries 내의 유일한 단독 Entry가 됩니다.
![](https://main.qcloudimg.com/raw/79f305c3d844b580940636cd228b2299.png)
3. Protobuf를 사용하여 Entries를 이진 배열로 인코딩합니다.
4. Entries의 이진 배열을 Envelope의 data 필드에 삽입합니다. 단일 Binlog Event의 크기가 너무 커 이진 배열이 Kafka 단일 메시지 크기 제한을 초과할 경우, 이를 여러 세그먼트로 분할하여 Envelope에 로드합니다.
Envelope.index와 Evelope.total는 각각 총 세그먼트 수 및 현재 Envelope의 일련번호(0부터 시작)를 입력합니다.
![](https://main.qcloudimg.com/raw/15fbcfc17bdb217de520cb662f2ce52b.png)
5. 앞서 생성한 1개 또는 여러 개의 Envelope을 순서대로 Protobuf 인코딩한 뒤, Kafka 파티션으로 전달합니다. 동일한 Entries가 분할되어 만들어진 여러 개의 Envelope를 차례대로 같은 파티션으로 전달합니다.

### 소비 로직
다음은 소비 로직에 대한 간략한 설명입니다. Tencent Cloud에서 제공하는 3가지 언어의 Demo는 모두 동일한 프로세스를 따릅니다.
1. Kafka 소비자를 생성합니다.
2. 소비를 실행합니다.
3. 원본 메시지를 차례대로 소비하고 메시지의 파티션에 따라 파티션에 상응하는 partitionMsgConsumer 객체를 찾으면, 해당 객체가 메시지를 처리합니다.
4. partitionMsgConsumer는 원본 메시지를 Envelope 구조로 역직렬화 합니다.
![](https://main.qcloudimg.com/raw/15fbcfc17bdb217de520cb662f2ce52b.png)
5. partitionMsgConsumer는 Envelope에 기록된 index와 total에 따라 하나 또는 다수의 메시지를 Envlope.index가 Envelope.total-1(위의 소비 생산 로직을 참조하면 하나의 완전한 Entries를 수신했음을 의미)과 같아질 때까지 소비합니다.
6. 수신된 연속적인 여러 Envelope의 data 필드를 순서대로 조합합니다. 조합된 이진 배열을 Protobuf를 사용해 Entries로 디코딩합니다.
![](https://main.qcloudimg.com/raw/a5368cd3c3ef9ec800a25d97ce5c13e0.png)
7. Entries.items를 순서대로 처리하고 원본 Entry 구조를 출력하거나 SQL 명령으로 변환합니다.
![](https://main.qcloudimg.com/raw/5e956452e68b1fed8c2a32c0207dc887.png)

## Java Demo 사용 설명
컴파일 환경: Maven 또는 Gradle 패키지 관리 툴, JDK8.
실행 환경: Tencent CVM(구독 인스턴스와 같은 리전이어야만 Kafka 서버의 내부 네트워크 주소에 액세스 가능), JRE8 설치.
작업 순서:
1. 신규 데이터 구독 채널을 생성합니다. 자세한 내용은 [데이터 구독 Kafka 버전](https://intl.cloud.tencent.com/document/product/571/39531)을 참조하십시오.
2. 하나 이상의 소비자 그룹을 생성합니다. 자세한 내용은 [소비자 그룹 추가](https://intl.cloud.tencent.com/document/product/571/39534)를 참조하십시오.
3. Java Demo를 다운로드하고 파일의 압축을 해제합니다.
4. 압축 해제 후 디렉터리로 들어간 뒤 사용하기 쉽도록 디렉터리에 Maven 모델 파일, pom.xml 파일 및 Gradle 관련 구성 파일을 각각 세팅하여 사용자가 필요에 따라 선택하도록 합니다.
  - Maven을 사용한 패키징: mvn clean package.
  - Gradle을 사용한 패키징: gradle fatJar 패키징 및 모든 종속 포함, 또는 gradle jar 패키징.
5. 실행: Maven 패키징 후 target 디렉터리 폴더로 들어가 `java -jar sub_demo-1.0-SNAPSHOT-jar-with-dependencies.jar --brokers=xxx --topic=xxx --group=xxx--user=xxx --password=xxx --trans2sql`을 실행합니다.
Gradle 패키징 후 build/libs 폴더로 들어가 `java -jar sub_demo-with-dependencies-1.0-SNAPSHOT.jar --brokers=xxx --topic=xxx --group=xxx--user=xxx --password=xxx --trans2sql`을 실행합니다.
6. 소비 상황을 관찰합니다.
![](https://main.qcloudimg.com/raw/fffa3de2a6e38b3752512183e1ffe785.png)

사용자도 IDE를 사용해 컴파일 패키징을 할 수 있습니다. IntelliJ IDEA 소프트웨어를 예로 들면 다음과 같습니다.
1. IntelliJ IDEA 소프트웨어를 열고 [Open]을 클릭합니다.
![](https://main.qcloudimg.com/raw/9d199900b36a43840825dc52dfa2c567.png)
2. 팝업 대화창에서 Demo 압축 해제 디렉터리를 찾습니다. 아래 이미지를 참고하여 디렉터리에서 pom.xml 파일을 찾아 [Open]을 클릭합니다.
![](https://main.qcloudimg.com/raw/1747158bf764aa898468bfa2bdb22054.png)
3. 팝업 대화창에서 [Open as Project]를 클릭합니다.
![](https://main.qcloudimg.com/raw/6b169744f3529f362fb81bb86becf593.png)
4. 창이 열리면 우측 Maven 관리 창의 Lifecycle에서 package를 더블클릭하여 패키징을 진행합니다.
![](https://main.qcloudimg.com/raw/63d85885b88dce1d65483abea6b9d3d3.png)
패키징 완료 후. 프로젝트 루트 디렉터리 target 폴더의 sub_demo-1.0-SNAPSHOT-jar-with-dependencies는 필수 종속이 포함된 실행 가능한 jar 패키지입니다.
Gradle의 작업 프로세스도 이와 유사합니다.

## Golang Demo 사용 설명
컴파일 환경: Golang 1.12 버전 이상, Go Module 환경 설정.
실행 환경: Tencent CVM(구독 인스턴스와 같은 리전이어야만 Kafka 서버의 내부 네트워크 주소에 액세스 가능).
작업 순서:
1. 신규 데이터 구독 채널을 생성합니다. 자세한 내용은 [데이터 구독 Kafka 버전](https://intl.cloud.tencent.com/document/product/571/39531)을 참조하십시오.
2. 하나 이상의 소비자 그룹을 생성합니다. 자세한 내용은 [소비자 그룹 추가](https://intl.cloud.tencent.com/document/product/571/39534)를 참조하십시오.
3. Golang Demo를 다운로드하고 파일의 압축을 해제합니다.
4. 압축을 해제한 디렉터리로 들어가 `go build -o subscribe ./main`을 실행하여 subscribe 실행 파일을 생성합니다.
5. `./subscribe --brokers=xxx --topic=xxx --group=xxx --user=xxx \--password=xxx --trans2sql=true`를 실행합니다.
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
1. 신규 데이터 구독 채널을 생성합니다. 자세한 내용은 [데이터 구독 Kafka 버전](https://intl.cloud.tencent.com/document/product/571/39531)을 참조하십시오.
2. 하나 이상의 소비자 그룹을 생성합니다. 자세한 내용은 [소비자 그룹 추가](https://intl.cloud.tencent.com/document/product/571/39534)를 참조하십시오.
3. Python3 Demo를 다운로드하고 파일의 압축을 해제합니다.
4. `python main.py --brokers=xxx --topic=xxx --group=xxx --user=xxx \--password=xxx --trans2sql=1`을 실행합니다.
5. 소비 상황을 관찰합니다.
![](https://main.qcloudimg.com/raw/6055041985904335b43d7df8f4e75561.png)

## 필드 매핑 및 저장
구체적인 MySQL/TDSQL 필드값은 다음 이미지와 같은 Protobuf 프로토콜의 Data 구조를 통해 저장됩니다.
![](https://main.qcloudimg.com/raw/2d0af55b06c62f410e715f150391cb62.png)
여기에서 DataType 필드는 저장된 필드 유형을 의미하며 다음 이미지와 같은 열거 값을 얻을 수 있습니다.
![](https://main.qcloudimg.com/raw/b9b5b081d2f12f6bfda3c24a7043b8e7.png)
여기에서 bv 필드에는 STRING과 BYTES 유형의 이진법 표기가, sv 필드에는 INT8/16/32/64/UINT8/16/32/64/DECIMAL 유형의 문자열 표기가, charset 필드에는 STRING의 컴파일 유형이 저장됩니다.

MySQL/TDSQL의 원본 유형과 DataType의 매핑 관계는 다음과 같습니다(UNSIGNED 수정자에 대한 MYSQL_TYPE_INT8/16/24/32/64는 각각 UINT8/16/32/32/64로 매핑).

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

