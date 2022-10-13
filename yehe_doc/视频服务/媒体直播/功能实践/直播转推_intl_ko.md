StreamLive를 사용하면 HTTP PUT 메소드를 사용하여 HLS/DASH 스트림을 HTTP 서버로 푸시할 수 있습니다.

**Output Group Setting** 페이지에서 **Output Group Type**으로 HLS/DASH를 선택하고 **Destination**에 HTTP 서버 주소를 입력합니다. Channel이 시작된 후 실시간 스트림은 실시간으로 대상 URL로 푸시됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f03e405e1b2ebd07285e28e6b5fd1f49.png)

아카이브와 릴레이의 차이점은 아카이브의 경우 Manifest 파일에 채널의 처음부터 끝까지 모든 오디오/비디오 파일이 포함되지만 릴레이의 경우 Manifest 파일이 지속적으로 업데이트되고 최신 오디오/비디오 파일만 포함된다는 점입니다.

HLS 및 DASH 스트림의 Manifest 파일 형식은 다음과 같습니다.
- HLS: ${Destination}/${OutputGroupName}.m3u8
- DASH: ${Destination}/${OutputGroupName}.mpd

릴레이는 HTTP 인증도 지원합니다. 활성화하려면 Destination 영역에서 **Authentication**을 켜고 인증 정보를 입력하십시오.
