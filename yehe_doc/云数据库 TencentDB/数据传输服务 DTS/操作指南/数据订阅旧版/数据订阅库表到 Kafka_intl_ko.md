
본 문서에서는 간단한 예시로 데이터 구독에서 상응하는 리스트를 Kafka로 읽어들이는 기능을 설명하며, 간단한 [KafkaDemo 다운로드](https://main.qcloudimg.com/raw/cf803ad5ddbb3f20534d98a5a0a23334/KafkaDemo.zip)를 제공합니다.

## 설정 환경
- 운영 체제: CentOS
- 관련 다운로드
 - [데이터 구독 SDK](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/binlogsdk-2.8.2-jar-with-dependencies.jar?_ga=1.22270587.1971922487.1581299091)
 - [SLF4J 컴포넌트](https://main.qcloudimg.com/raw/f8a577788af1d57cd269410fbe436a35/SLF4J.zip)
 - [Kafka-clients](https://main.qcloudimg.com/raw/a60f793a4eafe5f77e63615c5ce920e8/kafka-clients-1.1.0.jar)
- Java 환경 설정 
```
yum install java-1.8.0-openjdk-devel 
```

## Kafka 설치 
1. [Kafka 소개](http://kafka.apache.org/quickstart)를 참고하여 Kafka를 설치하십시오.
2. 실행 후 testtop 주제를 생성합니다.
```
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic testtop
Created topic "testtop".
```

## 키 획득
[액세스 관리 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인해 키를 획득합니다.

## 데이터 구독 선택
1. [DTS 콘솔](https://console.cloud.tencent.com/dtsnew/migrate/page)에 로그인해 왼쪽의 [데이터 구독]을 클릭해 데이터 구독 페이지로 이동합니다.
2. 구독 리스트에서 구독 이름을 클릭해 구독 상세 페이지로 이동하고, 상응하는 터널 ID, 서비스 IP, 서버 포트를 조회합니다.
3. 이전 키를 결합해 상응하는 KafkaDemo.java에 입력합니다.

```
import com.qcloud.dts.context.SubscribeContext;
import com.qcloud.dts.message.ClusterMessage;
import com.qcloud.dts.message.DataMessage;
import com.qcloud.dts.subscribe.ClusterListener;
import com.qcloud.dts.subscribe.DefaultSubscribeClient;
import org.apache.kafka.clients.producer.KafkaProducer;
import org.apache.kafka.clients.producer.Producer;
import org.apache.kafka.clients.producer.ProducerConfig;
import org.apache.kafka.clients.producer.ProducerRecord;
import org.apache.kafka.common.serialization.StringSerializer;
import org.apache.log4j.Logger;

import java.util.List;
import java.util.Properties;

public class KafkaDemo {
    public static void main(String[] args) throws Exception {
        //kafka producer 초기화
        final String TOPIC = "testtop";
        Properties props = new Properties();
        props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, "10.168.1.6:9092");
        props.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class);
        props.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class);

        final Producer<String, String> producer = new KafkaProducer<String, String>(props);

        // context 생성
        SubscribeContext context = new SubscribeContext();
        context.setSecretId("AKIDPko5fVtvTDE0WffffkCwd4NzKcdePt79uauy");
        context.setSecretKey("ECtY8F5e2QqtdXAe18yX0EBqK");
        // 터널 소재 region 구독
        context.setRegion("ap-beijing");
        final DefaultSubscribeClient client = new DefaultSubscribeClient(context);

        // 구독 listener 생성
        ClusterListener listener = new ClusterListener() {
            @Override
            public void notify(List<ClusterMessage> messages) throws Exception {
                System.out.println("--------------------:" + messages.size());
                for(ClusterMessage m:messages){
                    DataMessage.Record record = m.getRecord();


                    if(record.getOpt() != DataMessage.Record.Type.BEGIN && record.getOpt() != DataMessage.Record.Type.COMMIT){
                        List<DataMessage.Record.Field> fields = record.getFieldList();

                        //모든 리스트의 정보 출력
                        for (int i = 0; i < fields.size(); i++) {
                            DataMessage.Record.Field field = fields.get(i);
                            System.out.println("Database Name:" + record.getDbName());
                            System.out.println("Table Name:" + record.getTablename());
                            System.out.println("Field Value:" + field.getValue());
                            System.out.println("Field Value:" + field.getValue().length());
                            System.out.println("Field Encoding:" + field.getFieldEnc());
                        }

                        // 모든 record를 지정 kafka topic으로 발송
                        System.out.println("Record+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++");
                        producer.send(new ProducerRecord<String, String>(TOPIC, record.toString()));
                    }

                    m.ackAsConsumed();
                }
            }
            @Override
            public void onException(Exception e){
                System.out.println("listen exception" + e);
            }
        };
        // 리스너 추가
        client.addClusterListener(listener);
        client.askForGUID("dts-channel-p15e9eW9rn8hA68K");
        client.start();
    }

}
```


##  컴파일 작업과 검증
1. 클라이언트 프로그램 KafkaDemo.java을 편집합니다.
```
javac -classpath binlogsdk-2.9.1-jar-with-dependencies.jar:slf4j-api-1.7.25.jar:slf4j-log4j12-1.7.2.jar:kafka-clients-1.1.0.jar -encoding UTF-8 KafkaDemo.java 
```
2. 실행 시 오류가 없는 경우는 정상 서비스 중입니다.
```
java -XX:-UseGCOverheadLimit -Xms2g -Xmx2g  -classpath .:binlogsdk-2.9.1-jar-with-dependencies.jar:kafka-clients-1.1.0.jar:slf4j-api-1.7.25.jar:slf4j-log4j12-1.7.2.jar  KafkaDemo
```
3. 리스트의 alantest에 데이터를 삽입하면 Kafka 구독의 testtop 안에 이미 데이터가 있는 것을 볼 수 있습니다.
```
MySQL [test]> insert into alantest values(123456,'alan');
Query OK, 1 row affected (0.02 sec)
[root@VM_71_10_centos kafka_2.11-1.1.0]#  bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic testtop --from-beginning 
checkpoint:144251@3@1275254@1153089
record_id:00000100000000001198410000000000000001
record_encoding:utf8
fields_enc:latin1,utf8
gtid:4f21864b-3bed-11e8-a44c-5cb901896188:5552
source_category:full_recorded
source_type:mysql
table_name:alantest
record_type:INSERT
db:test
timestamp:1524649133
primary:id
Field name: id
Field type: 3
Field length: 6
Field value: 123456
Field name: name
Field type: 253
Field length: 4
Field value: alan
```

