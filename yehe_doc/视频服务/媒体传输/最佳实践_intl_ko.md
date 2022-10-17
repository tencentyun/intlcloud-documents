# 리전 간 전송

## 시나리오 설명
중국 청두에서 열리는 행사를 생중계한다고 가정합니다. 라이브 스트림은 중국 상하이로 전송되어 처리되며, 처리된 동영상은 중국, 유럽 및 북미의 라이브 스트리밍 플랫폼으로 전송됩니다.

## 솔루션
![](https://qcloudimg.tencent-cloud.cn/raw/62fd6a79371347984aa53930a465bcd0.jpeg)
- 현장에서 SRT 프로토콜을 사용하여 상하이의 스튜디오로 전송합니다.
- 스튜디오는 동영상을 처리하고 SRT 프로토콜을 사용하여 라이브 스트리밍 플랫폼에 배포합니다.
- 라이브 스트리밍 플랫폼은 StreamLink에서 스트림을 가져오거나 StreamLink는 스트림을 라이브 스트리밍 플랫폼으로 푸시합니다.


## StreamLink 구성 설명
라이브 스트림을 상하이에 있는 스튜디오로 보내야 한다고 가정합니다. 동영상을 처리한 후 스튜디오는 스트림을 다른 라이브 스트리밍 플랫폼으로 보내야 합니다.


### 1. 현장에서 스튜디오까지의 Flow 구성
라이브 이벤트의 저지연 요구 사항을 감안할 때 SRT 프로토콜이 사용됩니다. 소스 가용성을 보장하기 위해 라이브 스트림을 스튜디오로 전송하는 두 개의 Flow가 생성됩니다.

#### SRT Main Flow 생성
이벤트가 청두에서 진행되기 때문에 Input 주소가 같은 리전에 있도록 청두를 Region으로 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c8e72acfc3666277ca4686e74feba235.png)
![](https://qcloudimg.tencent-cloud.cn/raw/51e1c324d0da25db355060a4ad7b89e5.png)

- **Name**: 플로우의 이름은 chengdu_main_ori_stream입니다.
- **Max Bandwidth**: 원본 영상의 비트레이트가 높기 때문에 20Mbps가 선택됩니다.
- **Protocol**: SRT를 선택합니다.
- **Mode**: Listener를 선택합니다. 현장에서 StreamLink로 직접 전송됩니다.
- **Latency**: 푸시 끝은 사용된 StreamLink AZ(가용존)에 있습니다. 중국에서 동일 도시 전송에 대한 RTT는 일반적으로 10ms 미만입니다. 따라서 Latency는 60ms로 설정됩니다. 실제 RTT가 예상보다 높으면 푸시 엔드에서 Latency를 늘릴 수 있습니다.
- **Decryption Settings**: 푸시 엔드에서 암호화가 아닌 고정 IP 주소를 사용하므로 보안을 위해 IP 얼로우리스트를 사용합니다.
- **CIDR IP Allowlist**: 푸시 엔드에서 사용하는 IP 주소를 입력합니다. 이렇게 하면 이벤트의 장치만 스트림을 Flow에 푸시할 수 있습니다.

***Create**를 클릭합니다.

#### Output 추가
스튜디오가 상하이에 있기 때문에 상하이에서 Output을 만들어야 합니다. 레이턴시를 낮게 유지하기 위해 Output에도 SRT가 사용됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/57276bf97bce0d5032fd4d2691df7beb.png)

- **Output Name**: 출력 이름은 shanghai_main_output입니다.
- **Output Region**: 대기 시간을 낮게 유지하기 위해 상하이를 선택합니다.
- **Output Protocol**: SRT를 선택합니다.
- **Mode**: Listener를 선택합니다. 스튜디오는 StreamLink에서 스트림을 가져옵니다.
- **Latency Setting**: 스튜디오는 사용된 StreamLink AZ에 있습니다. 중국에서 동일 도시 전송에 대한 RTT는 일반적으로 10ms 미만입니다. 따라서 Latency는 60ms로 설정됩니다. 실제 RTT가 예상보다 높으면 푸시 엔드에서 Latency를 늘릴 수 있습니다.
- **Enable Encryption**: 스튜디오는 고정 IP 주소를 사용하므로 암호화 대신 IP 얼로우리스트를 사용하여 보안을 보장합니다.
- **CIDR IP AllowList**: 스튜디오의 IP 주소를 입력합니다. 이렇게 하면 스튜디오의 장치만 StreamLink에서 스트림을 가져올 수 있습니다.

**Confirm**을 클릭하여 output 구성을 저장합니다.

#### SRT Backup Flow 생성
백업 플로우를 만드는 단계는 Main Flow와 동일합니다.


### 2. 스튜디오에서 라이브 스트리밍 플랫폼으로 스트림을 보내도록 Flow 구성
동영상을 처리한 후 스튜디오는 이를 라이브 스트리밍 플랫폼에 배포해야 합니다. 라이브 스트리밍 플랫폼은 일반적으로 레이턴시에 대한 요구 사항이 높지 않기 때문에 RTMP가 전송에 사용됩니다.

#### RTMP Failover Flow 생성
스튜디오가 상하이에 있으므로 Input 주소가 같은 리전에 있도록 하기 위해 상하이를 Region으로 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3f2cc6be8882b2ef9f7ea3c2efa8a285.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0ece7d6ebe0c1062f3210c8354d2b3cf.png)

- **Name**: 플로우의 이름은 pgm_main입니다.
- **Max Bandwidth**: 처리된 영상의 비트레이트가 낮기 때문에 10Mbps가 선택됩니다.
- **Protocol**: RTMP를 선택합니다.
- **Failover**: 이 기능을 켭니다.
- **CIDR IP Allowlist**: 스튜디오의 IP 주소를 입력합니다. 이렇게 하면 스튜디오의 디바이스만 스트림을 Flow로 푸시할 수 있습니다.

**Create**을 클릭하여 Flow 구성을 저장합니다.

#### Output 추가
미국, 유럽 및 중국에 배포되어야 하므로 세 리전 각각에 대해 하나 이상의 Output을 만들어야 합니다. Output 프로토콜로 RTMP_PULL을 선택합니다. 즉, 라이브 스트리밍 플랫폼은 StreamLink에서 스트림을 가져와야 합니다. 각 Output은 동시에 4개의 스트림을 가져올 수 있습니다. 한 리전의 둘 이상의 플랫폼이 StreamLink에서 동시에 스트림을 가져오는 경우 여러 Output을 만드는 것이 좋습니다. 예를 들어 유럽의 두 라이브 스트리밍 플랫폼이 동시에 StreamLink에서 스트림을 가져오는 경우 두 플랫폼이 별도의 URL을 사용할 수 있도록 두 개의 Output을 생성합니다. 다음은 그러한 Output을 생성하는 방법을 보여줍니다.
![](https://qcloudimg.tencent-cloud.cn/raw/edf53f502063c2f3c93ef8170256a1dc.png)

- **Output Name**: 출력 이름은 eu_pgm_platform_a입니다.
- **Output Region**: Frankfurt, Germany를 선택합니다.
- **Output Protocol**: RTMP_PULL을 선택합니다. 라이브 스트리밍 플랫폼은 StreamLink에서 스트림을 가져와야 합니다.
- **CIDR IP Allowlist**: 라이브 스트리밍 플랫폼의 IP 주소를 입력합니다. 이렇게 하면 플랫폼의 장치만 StreamLink에서 스트림을 가져올 수 있습니다.

**Confirm**을 클릭하여 output 구성을 저장합니다.

### 3. 재생 URL 가져오기
#### 푸시 URL
Flow Management 페이지 또는 Input Source Information 페이지에서 스트림을 라이브 스트리밍 플랫폼으로 푸시하기 위한 URL을 볼 수 있습니다.
Flow Management에서:
![](https://qcloudimg.tencent-cloud.cn/raw/685dd9818b72280ffc9d84cec9ab8c0a.png)
Input Source Information에서:
![](https://qcloudimg.tencent-cloud.cn/raw/2098e9e325b6673ded79ab6843b7ad75.png)

#### 재생 URL
Output 목록에서 재생 URL을 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5f760430afe012ee26531294510de0bf.png)

### 4. Flow 실행
![](https://qcloudimg.tencent-cloud.cn/raw/d4e543da4000175587ec2d4d74e4775e.png)
이벤트가 시작되면 StreamLink 콘솔에서 Flow를 시작합니다.

### 5. Flow 설정을 동적으로 변경
라이브 스트리밍 중에 Flow를 중지하지 않고 Flow의 설정을 변경할 수 있습니다.
Input CIDR Allowiplist 수정:
![](https://qcloudimg.tencent-cloud.cn/raw/c4c642e542beed25a7cd134600a3ba62.png)
Output CIDR Allowiplist 수정:
![](https://qcloudimg.tencent-cloud.cn/raw/de4ce1df26d2bff4b0ca9ca7312a70ba.png)
Output 삭제:
![](https://qcloudimg.tencent-cloud.cn/raw/13b2a0fe21b9d528bdee155135da9b5d.png)
Output 추가:
![](https://qcloudimg.tencent-cloud.cn/raw/026591b6497dc6aa8411f3e19a2e42db.png)