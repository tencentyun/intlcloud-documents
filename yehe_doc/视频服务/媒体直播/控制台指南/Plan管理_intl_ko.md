채널 Plan에 이벤트를 추가하여 실행 중인 채널에 대한 이벤트를 실행할 수 있습니다. StreamLive는 지정된 시간에 지정된 작업을 수행합니다.

## 이벤트 보기
**Channel Management** 페이지에서 이벤트를 구성하려는 채널의 이름을 클릭하고 **Plan** 탭을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1dd3eebf1e4e7714c29a1302d65a514b.png)
![](https://qcloudimg.tencent-cloud.cn/raw/907a629dac8736d4780d411f2988d33f.png)

## 이벤트 생성
**Create Event**를 클릭합니다. 현재 다음 이벤트 유형이 지원됩니다.
- Input Switch: 실행 중인 채널의 입력을 변경합니다.
- Time Record: 실행 중인 채널 출력의 특정 세그먼트를 레코드합니다.

### 입력 스위치 이벤트 생성
<img src="https://qcloudimg.tencent-cloud.cn/raw/8136ad53ef809a22070e80f29a86cf84.png" style="zoom:80%;" />

- **Event Type**: Input Switch를 선택합니다.
- **Input Attachment**: 채널에 바인딩된 Input 중 하나를 선택하여 변경할 수 있습니다.
- **Event Name**: 최대 32자 길이의 이벤트 이름을 입력합니다. 숫자, 언더바 및 대소문자를 포함할 수 있으며 채널 전체에서 고유해야 합니다.
- **Start Type**: Fixed Time 또는 Immediate를 선택합니다. Fixed Time: 지정된 시간(UTC)에 이벤트를 실행하며, 이벤트 구성 시간보다 10초 이상 늦어야 합니다. Immediate: 이벤트를 즉시 실행합니다.

### 타임 레코드 이벤트 생성
<img src="https://qcloudimg.tencent-cloud.cn/raw/395c7b5bc4023a9160ada53913eea58c.png" style="zoom:80%;" />

- **Event Type**: Time Record를 선택합니다.
- **Event Name**: 최대 32자 길이의 이벤트 이름을 입력합니다. 숫자, 언더바 및 대소문자를 포함할 수 있으며 채널 전체에서 고유해야 합니다.
- **OutputGroupName**: 레코드할 OutputGroup을 선택합니다. Output Group Setting 페이지에서 채널의 출력 그룹을 볼 수 있습니다.
- **ManifestName**: 생성된 Mainfest 파일의 이름을 입력합니다(이름에 .m3u8 또는 .mpd를 포함할 필요는 없습니다).
- **DestinationUrl**: 파일을 저장할 COS 주소를 입력합니다.
- **Timing**: 레코드할 기간(UTC)을 입력합니다.

## 이벤트 삭제
삭제할 이벤트를 찾아 **Operation** 열에서 **Delete**를 클릭한 후 팝업 창에서 **Confirm**을 클릭합니다. 실행되지 않았거나 완료된 Event는 삭제할 수 있지만 실행 중인 Event는 삭제할 수 없습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/dae329be1090cbeb1b1705fe98fdef3d.png)