## SMTP 전송 기능 활성화
## 작업 단계
### 1단계: 발신자 주소 페이지로 이동
[SES 콘솔](https://console.cloud.tencent.com/ses)에 로그인하고 왼쪽 사이드바에서 이메일 설정-발신자 주소를 클릭하여 발신자 주소 페이지로 이동합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/fa124df0a9c52d8712e203e25866a389.png)

### 2단계: SMTP 비밀번호 설정
1. 발신자 주소 목록에서 SMTP 전송을 활성화할 주소를 찾고 작업 열에서 SMTP 비밀번호 설정을 클릭합니다.
2. 팝업 창에 SMTP 비밀번호를 입력하고 **확인**을 클릭합니다.



## SMTP API를 통해 이메일 전송
SMTP 예시 코드 및 특정 요청 매개변수, 응답 매개변수 및 오류 코드는 [Sample Call for Java](https://intl.cloud.tencent.com/document/product/1084/44456)를 참고하십시오.
>?첨부 파일이 있는 이메일은 [Sending Email with Attachment](https://intl.cloud.tencent.com/document/product/1084/44454)에 따라 보낼 수 있습니다.

## SMTP 전송 빈도
현재 SMTP API 호출 속도는 동일한 Tencent Cloud 계정 appId에서 20/1s로 제한됩니다. 또한 동일한 발신자가 동일한 수신자에게 최대 10/1h의 이메일을 보낼 수 있습니다.

당사는 이메일 수신 후 최대한 빨리 전달할 것입니다. 그러나 이메일 시스템마다 트래픽 조절 및 평판 보호 정책이 다르기 때문에 이메일 전송 성공률을 높이려면 이메일 전송 빈도를 낮추는 것이 좋습니다.


