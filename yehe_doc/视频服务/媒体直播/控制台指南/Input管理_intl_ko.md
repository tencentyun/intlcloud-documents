입력은 StreamLive 채널의 스트림 소스입니다. 입력은 일반적으로 1개의 보안 그룹 및 1개의 StreamLive 채널과 연결됩니다.

## 전제 조건
- [StreamLive](https://www.tencentcloud.com/products/mdl)가 활성화되어 있어야 합니다. 
- [StreamLive 콘솔](https://console.intl.cloud.tencent.com/mdl/input)에 로그인되어 있어야 합니다.

## Input 관리
왼쪽 사이드바에서 **Input Management**를 선택합니다. 이 페이지에서 생성된 input 이름, 유형, 상태 및 ID를 볼 수 있습니다. 각 input은 일반적으로 하나의 보안 그룹 및 하나의 StreamLive 채널과 연결됩니다. 채널과 연결된 input의 상태는 attached입니다. 각 input에는 데이터 가용성을 보장하기 위해 동시에 스트림을 푸시할 수 있는 두 개의 독립적인 파이프라인(A, B)이 있습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/19becd1c0a3678da5db222a4723ae5b6.png)


## Input 생성
PULL 또는 PUSH 입력을 생성할 수 있습니다. Input 관리 페이지에서 [Create Input]을 클릭하고 팝업 창에서 다음 설정을 완료합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0a58997dcc3241c77a07a05a458569c4.png)

- **Name**: 1-32자 길이의 Input 이름으로 숫자, 대소문자 및 언더바‘_’를 포함할 수 있습니다.
- **Type**: Input 유형입니다. 현재 RTMP_PUSH, RTP_PUSH, RTP-FEC_PUSH, UDP_PUSH, SRT_PUSH, RTMP_PULL, HLS_PULL, MP4_PULL, RTSP_PULL 및 SRT_PULL이 지원됩니다.
- **Security Group**: PUSH 입력을 생성하는 경우 Input 보안 그룹과 연결해야 합니다.

##### Type: RTMP_PUSH
입력 Type이 RTMP_PUSH인 경우 Destination에 대한 application name과 stream name을 입력해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0f449d8038bed66bcada1faa0481c92c.png)

##### Type: SRT_PUSH
입력 Type이 SRT_PUSH인 경우 Destination에 대한 streamid를 입력할 수 있습니다(선택 사항).
![](https://qcloudimg.tencent-cloud.cn/raw/f4a9ec18c0de6d127fce99d8c91aad89.png)

##### Type: PULL
입력 Type이 PULL인 경우 PULL 입력의 소스로 사용되는 InputAddress를 입력해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/28291755993b3efb3b3bdd4b63bfd40d.png)


## Input 수정
Input을 수정하려면 Input 관리 페이지에서 찾아, 오른쪽 **Edit**를 클릭합니다. 팝업 창에서 설정을 수정하고 **Confirm**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/45f415840a5b45d0a97baa965f05a45c.png)

## Input 삭제
Input을 삭제하려면 Input 관리 페이지에서 찾아, 오른쪽 **Delete**를 클릭하고 팝업 창에서 **Confirm**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/19becd1c0a3678da5db222a4723ae5b6.png)


>! 
>- 기본적으로 최대 5개의 input을 생성할 수 있습니다.
>- input 소스에는 적어도 하나의 비디오 파이프라인이 포함되어야 합니다.
>- MPEG-TS 다중화의 경우 최대 8개의 파이프라인이 동시에 데이터를 전송할 수 있습니다.

