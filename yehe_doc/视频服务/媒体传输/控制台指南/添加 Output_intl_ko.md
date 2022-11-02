## Output 관리
StreamLink 콘솔의 [Flow Management](https://console.tencentcloud.com/mdc/flow) 페이지에서 Flow를 클릭하여 세부 정보를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6e157c3ffc610bcf01c247a441a538cd.png)
Flow 세부 정보 페이지의 **Output** 탭에서 Output을 생성, 삭제 또는 편집할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ddfed18e28122e9198549541d3ebfd70.png)


## Output 생성
**Create Output**하려면 Output 생성을 클릭하고 팝업 창에서 필요한 설정을 완료한 후 **Confirm**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e9b1da7a805b27d5dcfa452775e7461d.png)

- **Output Name**: Output 이름입니다. Output 이름은 Output 관리를 용이하게 합니다.
- **Output Region**: 스트림을 보내려는 리전인 Output 리전입니다.
- **Output Protocol**: Output 프로토콜입니다. 프로토콜마다 다른 설정이 필요합니다.

  | Input 프로토콜 | Output 프로토콜 옵션 |
  | -----------| ---------------|
  | RTMP, RTMP_PULL       | RTMP , RTMP_PUSH, RTMP_PULL|
  | SRT         | SRT, RTMP_PUSH|
  | RTP         | RTP        |
  | RTSP        | RTSP       |
  

### RTMP_PUSH
이 프로토콜을 선택하면 스트림이 지정한 주소로 릴레이됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1a379f8a32e9ca1bd5341ade3a24912b.png)

- **Destination URL**: rtmp://example.com/live와 같은 RTMP 대상 Url입니다.
- **Flow Key**: e18c3c4dd05aef020946e6afbf9e04ef와 같은 RTMP 스트림 키입니다.


### RTMP_PULL
Output에서 스트림을 재생하려면 이 프로토콜을 선택합니다. RTMP_PULL Output을 생성한 후 Output 목록에서 재생 URL을 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/678b8da18059dec35579f1515c91e1ff.png)

- **CIDR IP AllowList**: 스트림을 푸시할 수 있는 IP 주소(예시: 203.3.3.3/28)를 지정하는 IP 얼로우리스트입니다. 이를 통해 보안이 향상됩니다. 203.3.3.3/28;202.3.3.3/28과 같이 여러 주소를 세미콜론으로 구분합니다.

### SRT Listener
![](https://qcloudimg.tencent-cloud.cn/raw/13071f72fe033f1a82b1bba87c7b7a56.png)
- **Mode**: Listener를 선택합니다. 이 모드에서는 수신 측에서 SRT Caller 모드를 사용하여 StreamLink에서 스트림을 요청해야 합니다. Output 목록에서 재생 URL을 볼 수 있습니다.
- **Latency Setting**: SRT Latency입니다. 푸시 엔드가 StreamLink 가용존과 동일한 국가에 있는 경우 120ms로 설정하는 것이 좋습니다. 푸시 엔드가 StreamLink 가용존과 동일한 국가에 있지 않은 경우 200ms로 설정하는 것이 좋습니다. 푸시 엔드가 StreamLink 가용존과 동일한 대륙에 있지 않은 경우 1000ms로 설정하는 것이 좋습니다. 할당된 IP 주소를 기반으로 이 매개변수의 값을 결정할 수 있습니다.
- **Enable Encryption**: 이 옵션을 켜면 수신 측에서도 암호화를 활성화하고 Encryption Key와 Key Length를 지정해야 합니다. 그렇지 않으면 스트림을 가져오지 못합니다.
  - **Encryption Key**: 암호화 key입니다.
  - **Key Length**: Key 길이입니다.
- **Failover**: 현재 이 프로토콜 유형에는 재해 복구가 아직 지원되지 않습니다. 향후 제공될 예정입니다.
- **CIDR IP Allowlist**: 스트림을 푸시할 수 있는 IP 주소(예시: 203.3.3.3/28)를 지정하는 IP 얼로우리스트입니다. 이를 통해 보안이 향상됩니다. 203.3.3.3/28;202.3.3.3/28과 같이 여러 주소를 세미콜론으로 구분합니다.

### SRT Caller
![](https://qcloudimg.tencent-cloud.cn/raw/254cb4af2ca2e3d27be2f0ff724b02f4.png)
- **Mode**: Caller를 선택합니다. 이 모드에서 StreamLink는 SRT Caller 모드를 사용하여 지정한 주소로 스트림을 보냅니다.
- **Destination**: SRT 스트림이 전송되는 IP 주소 또는 도메인입니다.
- **Port**: 대상 IP 주소의 포트 번호입니다.
- **Latency Setting**: SRT Latency입니다. 소스 주소가 StreamLink 가용존과 동일한 국가에 있는 경우 이를 120ms로 설정하는 것이 좋습니다. 소스 주소가 StreamLink 가용존과 동일한 국가에 있지 않은 경우 이를 200ms로 설정하는 것이 좋습니다. 소스 주소가 StreamLink 가용존과 동일한 대륙에 있지 않은 경우 이를 1000ms로 설정하는 것이 좋습니다. 할당된 IP 주소를 기반으로 이 매개변수의 값을 결정할 수 있습니다.
- **Enable Encryption**: 수신 측에서 암호화를 활성화하는 경우 이 기능을 켜고 Encryption Key와 Key Length를 지정해야 합니다. 그렇지 않으면 스트림을 푸시할 수 없습니다.
  - **Encryption Key**: 암호화 key입니다.
  - **Key Length**: Key 길이로, 수신측에서 구성된 것과 동일해야 합니다.
- **Failover**: 현재 이 프로토콜 유형에는 재해 복구가 아직 지원되지 않습니다. 향후 제공될 예정입니다.


### RTP
이 프로토콜을 선택하면 스트림이 지정한 주소로 푸시됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/4cca576a3a1da76f0e2a2a4ab7d80b48.png)

- **Destination**: 스트림을 보낼 주소입니다.
- **Port**: 드롭다운 목록은 사용된 Input 프로토콜에 따라 변경됩니다.