StreamLive를 사용하면 지정된 기간 동안 라이브 스트림을 녹화할 수 있습니다. 이 기능은 Tencent Cloud COS(Cloud Object Storage)와 함께 사용해야 합니다.

구성 단계는 다음과 같습니다:

1. COS 콘솔로 이동하여 녹음 파일의 스토리지를 구성합니다. 버킷을 생성하거나 기존 버킷을 선택할 수 있습니다. 버킷이 StreamLive 채널과 동일한 리전에 있는지 확인하십시오. 예를 들어 StreamLive 채널이 뭄바이에 있으면 버킷도 뭄바이에 있어야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/15154bc8dfecc79a6d59a913cbd0741a.png)

2. 버킷 이름을 클릭하여 구성 페이지로 이동하고 왼쪽 사이드바에서 **파일 목록**을 선택합니다. **폴더 생성**을 클릭하여 녹화 파일을 저장할 폴더를 만듭니다.
![](https://qcloudimg.tencent-cloud.cn/raw/077dfa198a68ac0f77bc6716e65c41a7.png)

3. 폴더 이름을 입력하고 버킷의 엔드포인트 URL에 연결합니다. 결과는 StreamLive 녹화 파일이 저장될 주소입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/474ebe6587dec1f4172d94226f8fc142.png)

버킷 **개요 페이지**의 **도메인 정보**에서 버킷의 **엔드포인트 URL**을 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3133262319ef5735ae287ef2821a5af0.png)

상기 예시에서 StreamLive 녹화 파일을 저장할 주소는 https://${your-bucket-name}-${appid}.cos.ap-mumbai.myqcloud.com/streamlive-scheduled-record입니다. 나중에 사용할 수 있도록 기록해 두십시오.

4. StreamLive 콘솔로 이동합니다. 예약 녹화를 설정할 채널 이름을 클릭하고 **Plan** 탭을 선택하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/e87cbf8e8ff1042941c99c5c946b4dc1.png)

5. **Create Event**을 클릭하고 다음 설정을 완료합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2ae655ad72824ca958a87fe1461d5ba2.png)
- **Event Type**: Time Record를 선택합니다.
- **Event Name**: 녹화 이벤트의 이름을 입력합니다.
- **OutputGroupName**: 드롭다운 목록에서 채널에 추가된 출력 그룹을 선택합니다.
- **ManifestName**: 재생 목록 파일의 이름입니다. HLS 출력의 경우 파일 형식은 m3u8입니다. DASH 출력의 경우 파일 형식은 mpd입니다.
- **DestinationUrl1**: 녹화 파일을 저장할 전체 COS 경로(버킷 이름 포함)를 입력하십시오.
- **Timing**: 스트림을 녹화할 기간을 지정합니다.

6. **Confirm**을 클릭합니다. 이것으로 구성을 마칩니다. 채널은 지정된 시간 동안 수신한 스트림을 녹화하고 녹화 파일을 지정된 대상에 저장합니다.


