Live Video Broadcasting(LVB)은 일반 라이브 방송 시나리오를 위해 CSS에서 제공하는 전문적이고 안정적이며 빠른 라이브 방송 클라우드 서비스로 [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071))와 함께 사용하면 App 및 Web을 포함한 여러 플랫폼에서 빠르게 구현할 수 있습니다.

[](id:app)

## App 액세스	
iOS 및 Android의 애플리케이션은 MLVB SDK를 통합하여 App에서의 라이브 방송 푸시 스트림/재생 기능을 구현할 수 있습니다.

- **App 라이브 방송 푸시 스트림**:카메라 화면 수집 또는 휴대폰 인터페이스 수집을 지원하며, RTMP 프로토콜을 통해 CSS에 스트림을 빠르게 푸시할 수 있습니다. 자세한 내용은 [카메라 푸시 스트림](https://intl.cloud.tencent.com/document/product/1071/38157) 및 [화면 녹화 푸시 스트림](https://intl.cloud.tencent.com/document/product/1071/41878)을 참고하십시오.
- **App 라이브 방송 재생**:RTMP, FLV, HLS 등 형식의 재생 프로토콜을 지원하고 CSS와 연동하여 라이브 방송 APP를 빠르게 구축합니다. 자세한 내용은 [LVB 풀 스트림](https://intl.cloud.tencent.com/document/product/1071/38159)을 참고하십시오.

>? MLVB SDK는 CSS, 인스턴트 메시지 IM, TRTC 및 기타 서비스를 통해 다중 사용자 멀티미디어 저지연 상호 연결 및 통신 효과를 구현하였으며, 다중 인터렉티브 마이크 연결 효과를 구현하였습니다. 마이크를 연결하지 않는 시청자도 라이브 방송 서비스를 통해 시청할 수 있습니다. 자세한 내용은 [라이브 방송 마이크 연결 인터랙션](https://intl.cloud.tencent.com/document/product/1071/39888)을 참고하십시오.



[](id:web)

## Web 구현
라이브 방송 푸시 스트림 및 재생이 필요한 웹 사이트가 있는 경우 다음 방법을 사용하여 구현하는 것을 권장합니다.
- **Web 라이브 방송 푸시 스트림**:브라우저의 범용 WebRTC 표준을 기반으로 설계 및 캡슐화되었으며, 코드 스니펫을 도입하여 브라우저에서 라이브 방송 푸시 스트림을 구현할 수 있습니다. 자세한 내용은 [WebRTC 푸시 스트림](https://intl.cloud.tencent.com/document/product/267/41620)을 참고하십시오.
> WebRTC 푸시 스트림 오디오 인코딩은 opus 인코딩만 지원합니다. LVB의 재생 프로토콜(RTMP, FLV, HLS)을 사용하여 재생하는 경우, 정상적인 시청을 보장하기 위해 CSS 백그라운드는 자동으로 오디오 트랜스 코딩을 aac 인코딩으로 전환합니다. 이로 인해 오디오 트랜스코딩 요금이 발생되며, 자세한 내용은 [오디오 트랜스코딩 과금 설명](https://intl.cloud.tencent.com/document/product/267/39604)을 참고하십시오.


