## WebRTC 푸시 스트림

[TXLivePusher 푸시 스트리밍 SDK](https://intl.cloud.tencent.com/zh/document/product/267/) 주로 비디오 클라우드의 LEB(초저지연 라이브 방송) 푸시 스트리밍에 사용되며, 브라우저가 수집한 멀티미디어 화면을 WebRTC를 통해 라이브 방송 서버로 전송합니다. 현재 카메라 푸시 스트리밍, 화면 녹화 푸시 스트리밍 및 로컬 미디어 파일 푸시 스트리밍을 지원합니다.

>? WebRTC 푸시 스트림의 오디오 인코딩 방식은 opus로，Live Video Broadcasting(LVB) 프로토콜（RTMP, FLV, HLS)을 사용하여 재생하는 경우, 시스템에서 자동으로 aac 인코딩으로 전환하며, 오디오 트랜스 코딩 요금이 발생합니다. 자세한 내용은 [오디오 트랜스 코딩 과금 설명]을 참고하십시오(https://intl.cloud.tencent.com/document/product/267/39604).



#### WebRTC 재생

Tencent Cloud Web Player+ [TCPlayerLite](https://intl.cloud.tencent.com/zh/document/product/1071/39888) 모바일 브라우저 및 PC 브라우저에서의 **LEB WebRTC 프로토콜** 라이브 방송 스트리밍 재생을 지원합니다. 기존 라이브 방송 프로토콜보다 딜레이가 훨씬 적으며, 시청자에게 밀리 초 단위의 고성능 라이브 방송 경험을 제공합니다.

>? 
> - WebRTC를 지원하지 않는 브라우저 환경에서 플레이어에 전송된 WebRTC 주소는 자동으로 프로토콜 전환을 통해 미디어 재생을 지원하며, 기본적으로 모바일에서는 HLS로, PC에서는 FLV로 전환됩니다.
> - LEB 관련 요금 정보는 [LEB 서비스 요금](https://intl.cloud.tencent.com/document/product/267/39969)을 참고하시기 바랍니다.

