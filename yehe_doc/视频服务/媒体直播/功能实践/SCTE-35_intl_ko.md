SCTE-35 메시지를 통과하도록 StreamLive를 구성할 수 있습니다.

SCTE-35 메시지는 MPEG-2 TS 입력에 의해서만 전달됩니다. 따라서 StreamLive는 RTP_PUSH, UDP_PUSH 또는 SRT_PUSH 입력에 대한 SCTE-35 메시지만 전달할 수 있습니다.

대상 Channel을 찾고 편집을 클릭하여 **Output Group Setting** 페이지로 이동합니다. SCTE-35 통과를 구성하려는 Outputs을 찾고 **Scte 35 Setting**을 켭니다.

![](https://qcloudimg.tencent-cloud.cn/raw/d55fb61889552e9b005f23908c0fa0dc.png)

SCTE-35 통과를 활성화하는 것만으로는 충분하지 않습니다. SCTE-35 메시지가 출력에 표시되려면 SCTE-35 메시지의 PES 페이로드도 입력에 포함해야 합니다.

통과를 활성화한 후 SCTE-35 메시지를 사용하여 다른 출력에 광고를 삽입할 수 있습니다.


