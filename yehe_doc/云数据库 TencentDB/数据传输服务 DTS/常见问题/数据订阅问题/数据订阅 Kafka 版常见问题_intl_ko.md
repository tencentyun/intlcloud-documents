### 데이터를 소비할 수 없는 이유는 무엇입니까?
- 네트워크 문제를 확인하십시오. Kafka 서버 주소가 Tencent Cloud 내부 내트워크 주소이고 Tencent Cloud 및 구독 인스턴스와 같은 리전의 사설 네트워크 내에서만 액세스할 수 있습니다.
- 구독 topic, 내부 네트워크 주소, 소비자 그룹 이름, 계정, 비밀번호 등이 올바른지 확인하십시오. [데이터 구독 콘솔](https://console.cloud.tencent.com/dts/dss)에서 구독명을 클릭하여 구독 상세 보기 페이지로 들어간 뒤 소비자 관리 페이지를 확인합니다.
- [Kafka에서 사용하는 인증 메커니즘](#faq3)을 참조하여 암호화 매개변수가 올바른지 확인하십시오.

### 데이터 포맷은 무엇입니까?
데이터 구독 Kafka 버전은 Protobuf 직렬화 방식을 사용합니다. Protobuf 프로토콜 파일은 [여기](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe.proto)에서 다운로드할 수 있으며, Demo 프로젝트에도 프로토콜 파일이 포함되어 있습니다. 자세한 내용은 [생산 및 소비 로직 설명](https://intl.cloud.tencent.com/document/product/571/39538)을 참조하십시오.

### [Kafka에서 사용하는 인증 메커니즘은 무엇입니까?] (id:faq3)
인증 메커니즘은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/83aa8f6122ee106f57568b6f25a1bd08.png)

### Kafka commit은 언제 진행하나요?
우선 Kafka의 enable_auto_commit 매개변수를 false로 설정하여 자동 commit을 비활성화하십시오. 메시지의 무결성을 보증하기 위하여 생산자가 메시지 시퀀스의 적절한 위치에 Checkpoint 메시지를 삽입하고, 소비자가 Checkpoint 메시지를 소비하면 commit을 진행합니다.

### 서버 메시지는 얼마동안 보관되며 소비 offset은 어떻게 설정합니까?
서버 메시지는 1일 동안 보관됩니다. 필요에 따라 Kafka의 auto_offset_reset 매개변수를 earliest 또는 latest로 설정할 수 있습니다. 특정 offset에서 소비를 시작해야 하는 경우, Kafka Client에서 제공하는 seek 기능을 사용해 소비 offset을 재설정 할 수 있습니다.
