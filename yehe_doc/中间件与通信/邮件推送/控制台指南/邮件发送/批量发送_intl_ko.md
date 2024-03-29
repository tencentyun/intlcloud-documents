## 작업 시나리오
본 문서는 콘솔에서 이메일을 일괄 발송하는 방법을 설명합니다. 일괄 발송은 대규모 이메일 시나리오에 적합하며 다양한 수신자에 대해 다양한 변수 값 구성을 지원합니다. 수신자는 이메일의 ‘수신자’ 필드에서 자신만 볼 수 있습니다.

## 작업 단계
1. [SES 콘솔](https://console.cloud.tencent.com/ses/send)에 로그인하여 **이메일 발송** > **일괄 발송**을 클릭하면 발송 작업 목록을 볼 수 있습니다. 목록에는 발송 진행률, 작업 유형, 작업 상태 및 요청 수를 포함한 각 발송 작업의 세부 정보가 표시됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/03e8a8f74f5d0ab785bb016427712502.png)
2. **발송 작업 생성**을 클릭하고 작업 유형에 대해 **일괄 발송**을 선택한 다음 작업에 필요한 모든 필드를 설정하여 이메일을 일괄 발송합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bd85315b7f512173a687f6c0ea4f706c.png)
>?발송 작업 페이지에서 선택한 수신자 목록의 변수 수 및 이름은 선택한 템플릿의 변수와 동일해야 합니다.

### 예약 발송
1. [SES 콘솔](https://console.cloud.tencent.com/ses/send)에서 **이메일 발송** > **일괄 발송**을 선택하고 **발송 작업 생성**을 클릭한 다음 **발송 예약**을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7e4f2dcdca1e2f11ba55e7d03861489e.png)
2. **작업 시작 시간**을 선택하면 지정된 시간에 이메일이 자동으로 발송됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/55482b11771bbe336023ca840d346234.png)

### 반복 발송
1. [SES 콘솔](https://console.cloud.tencent.com/ses/send)에서 **이메일 발송** > **일괄 발송**을 선택하고 **발송 작업 생성**을 클릭한 다음 **반복 발송**을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/972566ee846e6629d9518f67686cec99.png)
2. **작업 시작 시간** 및 **반복 빈도**를 포함한 작업 필드를 설정합니다. 콘솔은 지정된 반복 빈도에 따라 자동으로 이메일을 보냅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e5ca62b26bbbfc467855d04d4e9c088e.png)

>?
>
>- 콘솔의 일괄 발송 기능은 마케팅 또는 알림 이메일 일괄 발송에 적합합니다. 트리거 기반 이메일(예시: 인증 및 트랜잭션 이메일)을 보내려면 API- SendEmail을 호출하는 것이 좋습니다.
>- 자동 Warm Up은 일괄 발송 기능에 내장되어 있습니다. Warm Up 기능에 대한 자세한 내용은 [시작하기 > Warm Up이란?](https://intl.cloud.tencent.com/document/product/1084/42368)을 참고하십시오.
>- 여러 발송 작업에 단일 도메인을 사용할 수 있습니다. 총 이메일 수량이 하루에 허용되는 최대 수량을 초과하면 추가 이메일이 캐시 대기열에 들어가 다음 날 발송됩니다.
>- 작업이 캐시 대기열에 들어가면 해당 상태는 일시 중지되고 발송 진행률 표시줄은 정적 상태로 유지됩니다. 다음 날 작업을 다시 시작하면 상태가 발송 중이 되고 진행률 표시줄이 업데이트 됩니다.
