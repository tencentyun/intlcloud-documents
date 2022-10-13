StreamLive를 사용하면 HLS/DASH 스트림을 Tencent Cloud COS(Cloud Object Storage)에 저장할 수 있습니다.

**Channel**의 **Output Group Setting** 페이지에서 **Output Group Type**으로 HLS_ARCHIVE/DASH_ARCHIVE를 선택하고 COS URL 주소를 입력하여 **COS Destination**에 스트림을 저장합니다. Channel이 시작된 후 라이브 스트림은 실시간으로 COS에 보관됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2d18dc7f0100da76ffc40df26ea7e158.png)

아카이브와 릴레이의 차이점은 아카이브의 경우 Manifest 파일에 채널의 처음부터 끝까지 모든 오디오/비디오 파일이 포함되지만 릴레이의 경우 Manifest 파일이 지속적으로 업데이트되고 최신 오디오/비디오 파일만 포함된다는 점입니다.

HLS 및 DASH 스트림의 기본 Manifest 파일 형식은 다음과 같습니다.
- HLS：${COS Desination}/${region}/${ChannelId}-${p0 or p1}/${OutputGroupName}/${OutputGroupName}.m3u8
- DASH：${COS Desination}/${region}/${ChannelId}-${p0 or p1}/${OutputGroupName}/${OutputGroupName}.mpd



