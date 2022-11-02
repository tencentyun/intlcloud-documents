StreamLink 콘솔의 [Flow Management](https://console.tencentcloud.com/mdc/flow) 페이지로 이동합니다. 세부 정보를 보려면 Flow를 클릭합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/8761f3d6e89cd2ef43c7a1531baceeb0.png)

## 기본 정보(Information)
![](https://qcloudimg.tencent-cloud.cn/raw/849236bd82f00c864ec0ba5a4a8e03bc.png)
**Information** 탭에서 Flow ID, Flow Name, Input Region, 플로우 상태 및 최대 대역폭을 볼 수 있습니다.

## 입력 소스 정보(Input Source)
![](https://qcloudimg.tencent-cloud.cn/raw/08335f06efbb8d4699a50b1acd7f86b5.png)
**Input Source** 탭에서 Input Source Name, Input Source 주소, 얼로우리스트 및 프로토콜 설정을 볼 수 있습니다.

## 출력 정보(Output)
![](https://qcloudimg.tencent-cloud.cn/raw/900b528fbc1d55552c7c520d74c18a7a.png)
**Output** 탭에서 Flow의 Output 정보를 볼 수 있습니다.

- **Name**: Output의 이름입니다.
- **Output ID**: Output의 ID입니다.
- **Output Region**: 스트림이 전송되는 영역인 Output 영역입니다.
- **Output IP**: Output이 전송되는 IP 주소입니다.
- **Protocol**: Output의 프로토콜입니다.
- **URL**: 재생 URL(Output이 재생을 지원하는 경우)입니다.

이 페이지에서 Output을 생성, 편집 또는 삭제할 수 있습니다.

## 로그 정보(Log)
![](https://qcloudimg.tencent-cloud.cn/raw/2ed506e30a7bf706805ae2d29986454b.png)
**Log** 탭에서 Flow가 실행되는 동안 발생한 이벤트(예시: 스트림 푸시, 스트림 중단, IP 주소 차단)를 볼 수 있습니다.

## 상태 정보(Health)
상태 탭에서 프레임 레이트 및 비트 레이트와 같은 스트림 성능 지표를 볼 수 있습니다.
### 입력 소스(Input Source)
지난 1시간 동안의 전송 품질을 볼 수 있습니다. 또한 지정된 시간 범위의 품질 데이터를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f4f10f4d37873fce43c3d88def9eaef0.png)

Video/Audio 섹션에서 해당 탭을 선택하여 스트림의 비트 레이트 및 프레임 레이트를 볼 수 있습니다. 스트림에 둘 이상의 오디오 트랙이 있는 경우 드롭다운 목록에서 선택하여 특정 오디오 트랙의 정보를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ef3502d0afb338f4c64b673379dd25cf.png)

입력 프로토콜이 SRT인 경우 페이지 하단에서 SRT 전송의 성능 표시기를 볼 수도 있습니다.
- **Paket Loss rate**: SRT 전송의 패킷 손실률입니다. 이것은 변속기의 안정성을 측정합니다. 일반적으로 원활한 전송을 위해서는 패킷 손실률이 20% 미만이어야 합니다.
- **Retransmission Rate**: SRT 전송의 재전송 속도. 패킷 손실률보다 현저히 낮은 재전송률은 일반적으로 끊김 현상 또는 스트림 중단을 나타냅니다.
- **RTT**: RTT는 전송 대기 시간을 측정합니다. 높은 RTT는 높은 Latency를 나타내며, 이는 SRT Latency 값도 높게 설정해야 함을 의미합니다. 권장 SRT 대기 시간 값은 RTT의 4배입니다. RTT가 급격하게 변경되면 전송이 불안정하다는 것을 나타내며 경우에 따라 심각한 패킷 손실이 발생할 수 있습니다.
- **Number Of Dropped Packtes**: SRT 스택에 의해 삭제된 패킷 수입니다. SRT 스택은 전송 Latency가 구성된 SRT Latency를 초과하면 패킷을 삭제합니다. 이는 푸시 또는 높은 RTT에 대한 대역폭이 충분하지 않음을 나타내며 일반적으로 픽셀화가 발생합니다. Latency 값을 늘려야 합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/720784ac0a25685da1c75d8a1aeeaea1.png)

### 출력(Output)
Output 탭에 표시되는 정보는 Input 소스 탭에 표시되는 정보와 대체로 동일합니다. 흐름에는 여러 Output이 있을 수 있습니다. Output을 선택하거나 검색하여 해당 정보를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2563d297d6ee371f8f31b3010578a8b9.png)