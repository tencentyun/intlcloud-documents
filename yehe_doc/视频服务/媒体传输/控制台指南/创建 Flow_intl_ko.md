StreamLink 콘솔의 [Flow Management](https://console.tencentcloud.com/mdc/flow) 페이지로 이동하고 **Create Flow**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b7ea1765ad2384f3b2c5ceeef2a76ce7.png)

Flow Name을 입력하고 최대 비트 레이트를 지정하고 Input 정보를 입력합니다.
- **Name**: Flow를 식별하는 데 도움이 되는 Flow 이름입니다.
- **Max Bandwidth**: 스트림의 최대 비트 레이트를 선택합니다. 네트워크 리소스 할당은 이 값을 기반으로 합니다.
- **Source Name**: 출처를 식별하는 데 도움이 되는 소스 이름입니다.
- **Protocol Type**: 푸시 프로토콜입니다. 현재 RTMP, SRT, RTP 및 RTSP가 지원됩니다.

## RTMP
RTMP를 선택하면 스트림을 StreamLink에서 생성한 입력 주소로 푸시해야 합니다. Flow Management 페이지에서 주소를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/74cf0e4bb392f4474261703eec7974ea.png)

- **Failover**: 재해 복구를 활성화하면 StreamLink는 두 개의 입력 주소를 생성합니다. 스트림을 두 주소로 푸시할 수 있습니다. 먼저 도착한 스트림이 기본 소스로 사용됩니다. 기본 소스가 다운되면 StreamLink는 자동으로 백업 스트림으로 전환합니다.
- **CIDR IP Allowlist**: 스트림을 푸시할 수 있는 IP 주소(예시: 203.3.3.3/28)를 지정하는 IP 얼로우리스트입니다. 이를 통해 보안이 향상됩니다. 203.3.3.3/28;202.3.3.3/28과 같이 여러 주소를 세미콜론으로 구분합니다.


## RTMP_PULL
RTMP_PULL을 선택하면 StreamLink는 지정한 주소에서 스트림을 가져옵니다.
![](https://qcloudimg.tencent-cloud.cn/raw/751d78b56498ba5d9eafaddb8bdccf57.png)

- **Source Address**: rtmp://example.com/live와 같은 RTMP Url입니다.
- **Source Key**: e18c3c4dd05aef020946e6afbf9e04ef와 같은 RTMP 스트림 키입니다.
- **Failover**: 현재 이 프로토콜 유형에는 재해 복구가 아직 지원되지 않습니다. 향후 제공될 예정입니다.

## SRT Listener
![](https://qcloudimg.tencent-cloud.cn/raw/30760bb8411f2a14bb630b3eb3cd8637.png)
- **Mode**: Listener를 선택합니다. 이 모드에서는 SRT Caller 모드를 사용하여 스트림을 StreamLink Input 주소로 보내도록 요청해야 합니다. Flow Management 페이지에서 Input 주소를 볼 수 있습니다.
- **Latency Setting**: SRT Latency. 푸시 엔드가 StreamLink 가용존과 동일한 국가에 있는 경우 120ms로 설정하는 것이 좋습니다. 푸시 엔드가 StreamLink 가용존과 동일한 국가에 있지 않은 경우 200ms로 설정하는 것이 좋습니다. 푸시 엔드가 StreamLink 가용존과 동일한 대륙에 있지 않은 경우 1000ms로 설정하는 것이 좋습니다. 할당된 IP 주소를 기반으로 이 매개변수의 값을 결정할 수 있습니다.
- **Decryption Settings**: 전송 보안을 향상시키려면 이 기능을 켤 수 있습니다. Decryption Key 및 Key Length를 지정합니다. 푸시 엔드에 동일한 암호화 KEY 및 kEY 길이를 구성해야 합니다. 그렇지 않으면 스트림 푸시에 실패합니다.
  - **Decryption Key**: 암호화/복호화 key입니다. 푸시 엔드에서 동일한 key를 구성해야 합니다.
  - **Key Length**: 키 길이입니다. 푸시 엔드에서 동일한 key 길이를 지정해야 합니다.
- **Failover**: 현재 이 프로토콜 유형에는 재해 복구가 아직 지원되지 않습니다. 향후 제공될 예정입니다.
- **CIDR IP Allowlist**: 스트림을 푸시할 수 있는 IP 주소(예시: 203.3.3.3/28)를 지정하는 IP 얼로우리스트입니다. 이를 통해 보안이 향상됩니다. 203.3.3.3/28;202.3.3.3/28과 같이 여러 주소를 세미콜론으로 구분합니다.

## SRT Caller
![](https://qcloudimg.tencent-cloud.cn/raw/b8a8ae4e50e6375b635795c4d60e2577.png)
- **Mode**: Caller를 선택합니다. 이 모드에서 StreamLink는 호출자 모드를 사용하여 제공한 주소에서 소스 스트림을 요청합니다.
- **Source IP**: 소스 스트림의 IP 주소 또는 도메인입니다.
- **Source Port**: 소스 IP 주소의 포트 번호입니다.
- **Latency Setting**: SRT Latency. 소스 주소가 StreamLink 가용존과 동일한 국가에 있는 경우 이를 120ms로 설정하는 것이 좋습니다. 소스 주소가 StreamLink 가용존과 동일한 국가에 있지 않은 경우 이를 200ms로 설정하는 것이 좋습니다. 소스 주소가 StreamLink 가용존과 동일한 대륙에 있지 않은 경우 이를 1000ms로 설정하는 것이 좋습니다. 할당된 IP 주소를 기반으로 이 매개변수의 값을 결정할 수 있습니다.
- **Decryption Settings**: 소스 스트림에 대한 암호화를 활성화하는 경우 이 기능을 켜고 Decryption Key와 Key Length를 지정해야 합니다. 그렇지 않으면 StreamLink가 스트림을 가져오지 못합니다.
  - **Decryption Key**: 복호화 key입니다. 이는 소스 스트림에 대한 암호화를 활성화하는 경우 필요합니다.
  - **Key Length**: Key 길이로, 소스 스트림에 대해 구성된 것과 동일해야 합니다.
- **Failover**: 현재 이 프로토콜 유형에는 재해 복구가 아직 지원되지 않습니다. 향후 제공될 예정입니다.

## RTP
RTP를 선택하면 스트림을 StreamLink에서 생성한 입력 주소로 푸시해야 합니다. Flow Management 페이지에서 주소를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1e91a938d681e46e48ec8bb7405df2c4.png)

- **Failover**: 현재 이 프로토콜 유형에는 재해 복구가 아직 지원되지 않습니다. 향후 제공될 예정입니다.
- **CIDR IP Allowlist**: 스트림을 푸시할 수 있는 IP 주소(예시: 203.3.3.3/28)를 지정하는 IP 얼로우리스트입니다. 이를 통해 보안이 향상됩니다. 203.3.3.3/28;202.3.3.3/28과 같이 여러 주소를 세미콜론으로 구분합니다.