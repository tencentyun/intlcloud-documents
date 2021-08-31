데이터 구독 Kafka 버전에서는 0.11 버전 이상의 Kafka 클라이언트를 통해 구독 데이터를 직접 소비할 수 있습니다. 본 문서에서는 Java와 Go 두 가지 언어의 클라이어트 소비자 Demo를 제공합니다.

## 소비자 Demo 다운로드
다음 표를 참조하여 데이터 구독 Kafka 버전 클라이언트의 소비자 Demo 코드를 다운받으십시오.

| Demo 언어 | 주소 다운로드                                                     |
| -------- | ------------------------------------------------------------ |
| Go       | [주소](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_go_demo.zip)  |
| Java     | [주소](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_java_demo.zip)  |

## 매개변수 설정 설명

| 매개변수       | 설명                        |
| ---------- | --------------------------- |
| brokerlist | 데이터 구독 Kafka의 내부 네트워크 액세스 주소 |
| topic      | 데이터 구독 채널의 구독 topic     |
| group      | 소비자 그룹 명칭                  |
| user        | 소비자 그룹 계정 이름                |
| password   | 소비자 그룹 비밀번호 변경                  |
