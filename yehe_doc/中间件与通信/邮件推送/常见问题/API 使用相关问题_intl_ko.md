### ReplyToAddresses 매개변수는 무엇을 의미합니까?
회신 메시지가 전송되는 이메일 주소를 나타냅니다. 예를 들어, 누군가가 귀하의 이메일을 받고 ‘회신’을 클릭하면 회신 이메일이 귀하가 ReplyToAddresses에 지정한 주소로 전송됩니다.

### 이메일을 보내려고 하면 FailedOperation.ExceedSendLimit 일일 이메일 전송 한도 초과 오류가 발생합니다. 한도는 얼마입니까? 한도를 높일 수 있습니까?
각 계정은 기본적으로 하루에 최대 30만개의 이메일을 보낼 수 있습니다. 한도를 높이려면 [Tencent Cloud 기술 지원](https://console.cloud.tencent.com/workorder/category)에 문의하십시오.

### SendEmail API에 Template.TemplateData를 어떻게 입력해야 합니까?
“`{}`”는 전달된 변수가 없음을 의미합니다. 자세한 내용은 API 문서의 [TemplateData](https://intl.cloud.tencent.com/document/product/1084/39418#Template) 필드를 참고하십시오.
