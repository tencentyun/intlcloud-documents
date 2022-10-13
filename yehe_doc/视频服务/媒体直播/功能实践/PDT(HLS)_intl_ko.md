HLS 스트림의 출력 Media Manifest에 대해 EXT-X-PROGRAM-DATE-TIME 태그를 구성하여 첫 번째 미디어 세그먼트를 절대 날짜 및 시간과 연결할 수 있습니다. 형식은 다음과 같습니다.

```
1  #EXT-X-PROGRAM-DATE-TIME:<date-time-msec>
```

date-time-msec의 형식은 ISO/IEC 8601:2004 [ISO_8601](YYYY-MM-DDThh:mm:ss.SSSZ)입니다. 밀리초 단위까지 정확한 시간대를 지정해야 합니다.

HLS 스트림에 PDT 태그를 삽입합니다. 대상 **Channel**을 찾고 편집을 클릭하여 **Output Group Setting** 페이지로 이동합니다. **Output Group Type**이 HLS, HLS_ARCHIVE 또는 HLS_STREAM_PACKAGE인 경우에만 EXT-X-PROGRAM-DATE-TIME 태그를 구성할 수 있습니다.
**Segment Infomation** 영역에서 **PdtInsertion**을 켜고 태그를 삽입할 간격(초)을 지정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0863a6dc3e189d25d7c37c6e18d2af4d.png)
구성 후 채널을 시작합니다. 입력이 가능하면 600초마다 삽입되는 출력 M3u8 스트림에 PDT 태그가 표시됩니다.





