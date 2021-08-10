## Web에서의 푸시 스트리밍

- CSS 콘솔에 로그인 후, 좌측 메뉴에서 [라이브 방송 툴박스]>[Web 푸시] (https://intl.cloud.tencent.com/login)]를 선택하여 진행할 수 있으며, 자세한 내용은 [Web에서의 푸시 스트리밍](https://intl.cloud.tencent.com/document/product/267/31558)을 참고하십시오.
- TXLivePusher 푸시 스트리밍 SDK를 통해 푸시 스트리밍을 진행할 수 있습니다. 자세한 내용은 [WebRTC 푸시 스트림](https://intl.cloud.tencent.com/document/product/267)을 참고하십시오.

>? WebRTC 푸시 스트림의 오디오 인코딩 방식은 opus로，Live Video Broadcasting(LVB) 프로토콜（RTMP, FLV, HLS)을 사용하여 재생하는 경우, 시스템에서 자동으로 aac 인코딩으로 전환하며, 오디오 트랜스 코딩 요금이 발생합니다. 자세한 내용은 [오디오 트랜스 코딩 과금 설명]을 참고하십시오(https://intl.cloud.tencent.com/document/product/267/39604).



#### Web 재생

SDK의 [TCPlayerLite](https://cloud.tencent.com/document/product/881/20207)로 재생할 것을 권장합니다. 해당 플레이어는 Tencent Cloud의 강력한 백그라운드 능력과 AI 기술을 기반으로 비디오 라이브 방송 및 VOD에 대해 강력한 재생 능력을 제공합니다. Player+는 Tencent CSS 및 VOD 서비스와 연동되어 원활하고 안정적인 재생 성능을 보유하고 있으며, 광고 삽입, 데이터 모니터링 등의 기능이 탑재되어 있습니다.

>? 현재 시중의 대다수 모바일 브라우저는 HTTP-FLV 재생을 지원하지 않으므로, Tencent Cloud는 Web에서의 라이브 스트리밍 재생 시 PC 브라우저는 HTTP-FLV 프로토콜을, 모바일 브라우저는 HLS 프로토콜을 사용할 것을 권장합니다.





