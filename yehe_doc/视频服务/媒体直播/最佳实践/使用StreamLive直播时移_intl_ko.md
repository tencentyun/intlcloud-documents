StreamLive 라이브 방송을 통한 서비스 타임 시프트 이전에, 사용자는 CSS 및 StreamLive를 활성화해야 합니다. CSS는 타임 시프트 도메인을 재생 도메인으로 사용하며, 도메인 프로세스에 따라 추가합니다.



### StreamLive 라이브 방송 타임 시프트 기능 활성화

[티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 StreamLive 타임 시프트 기능 활성화를 신청합니다. 사용자 계정 APPID 및 타임 시프트 도메인이 필요합니다.


### StreamLive 라이브 방송 타임 시프트 설정

티켓에 타임 시프트를 설정한 후 콘솔 또는 API를 통해 StreamLive의 OutputGroup에 타임 시프트 기능을 활성화할 수 있습니다. 타임 시프트 도메인을 바인딩합니다.

>! HLS_ARCHIVE 및 DASH_ARCHIVE만 타임 시프트를 활성화할 수 있습니다.

1. StreamLive 콘솔의 **Channel Management** 페이지로 이동합니다.
2. Channel을 생성하거나 타임 시프트를 설정할 채널을 선택하고 ‘**edit channel**’을 클릭합니다.
3. ‘**Output settings page**’페이지에서 ‘**Basic Information**’-‘**Out put Group Type**’을 **HLS_ARCHIVE / DASH_ARCHIVE**로 설정합니다. 
4. **TimeShift Information**열에서 타임 시프트 스위치를 활성화하고 타임 시프트 시간을 입력합니다.

>! 타임시프트 시간은 300초에서 1209600초 사이여야 합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/46388651f1047edb0a1a8b8128ae2e02.png)
