## WebRTC 푸시 스트림

[TXLivePusher 푸시 스트림 SDK](https://intl.cloud.tencent.com/document/product/267/41620)는 주로 LEB(초저지연 라이브 방송) 푸시 스트림에 사용되며, 브라우저에서 수집한 오디오 및 비디오를 WebRTC를 통해 라이브 스트리밍 서버로 푸시할 수 있습니다. 현재 카메라, 화면 또는 로컬 미디어 파일 푸시 스트림을 지원합니다.

>? WebRTC 푸시 스트림 오디오 인코딩 방식은 opus 코덱입니다. 재생에 LVB 프로토콜(RTMP, FLV, HLS)을 사용하는 경우 시스템이 자동으로 aac 코덱으로 변환하므로 오디오 트랜스 코딩 요금이 발생합니다. 자세한 내용은 [오디오 트랜스 코딩 과금 설명](https://intl.cloud.tencent.com/document/product/267/39604)을 참고하십시오.

