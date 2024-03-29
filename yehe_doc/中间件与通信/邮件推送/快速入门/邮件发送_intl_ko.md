Simple Email Service(SES)는 템플릿을 사용한 이메일 발송만 지원합니다.

## 작업 단계
### 1단계: 템플릿 구성[](id:Step1)
1. 이메일 콘솔의 개요 페이지로 이동하여 **[이메일 템플릿](https://console.cloud.tencent.com/ses/template)**을 클릭합니다.
2. 이메일 템플릿 페이지에서 **생성**을 클릭합니다.
3. 다음 매개변수를 설정합니다.
	- 템플릿 이름: 예시 `test`.
	- 템플릿 유형: **HTML 서식 있는 텍스트**를 선택합니다.
	- 이메일 요약: 예시 `알림 이메일 템플릿`.
	- 이메일 본문: **파일 선택**을 클릭하고 이메일 본문으로 HTML 파일을 선택합니다.
>?이메일의 내용은 일반 텍스트 또는 서식 있는 텍스트 형식일 수 있으며 서식 있는 텍스트 형식은 HTML 코드를 미리 준비해야 합니다.

4. **미리보기**를 클릭하여 이메일 템플릿을 미리보기 합니다.
5. **제출**을 클릭하여 템플릿 구성을 완료하고, 심사를 기다립니다.
>?템플릿 제출 후 심사 단계에 들어가며, 영업일 기준 1일 이내에 담당자가 심사를 완료하며, 심사가 통과된 후 템플릿을 사용하여 이메일을 보낼 수 있습니다.

### 2단계: 이메일 발송[](id:Step2)
SES를 사용하여 이메일을 보내는 3가지 방법이 있습니다.
- 콘솔 발송
- API 발송
- SMTP 발송

‘콘솔 발송’ 방법은 본 챕터의 시작하기에서 간략히 소개할 예정이며 자세한 내용은 ‘콘솔 가이드’를 참고하십시오. 나머지 2가지 발송 방법은 [API 개요](https://intl.cloud.tencent.com/document/product/1084/39387), [SMTP 이메일 전송 가이드](https://intl.cloud.tencent.com/document/product/1084/44458)를 참고하시기 바랍니다.

1. **[이메일 발송 - 일반 발송](https://console.cloud.tencent.com/ses/send)**을 클릭하여 **이메일 발송** 페이지로 이동합니다.
>?이 페이지는 소규모 이메일 발송만 지원하며, 1회 최대 발송 가능 주소는 20개입니다. 대량 발송은 콘솔 [Batch sending](https://intl.cloud.tencent.com/document/product/1084/47542)을 참고하시거나 API 발송, SMTP 발송을 이용하시기 바라며, 자세한 내용은 [API 개요](https://intl.cloud.tencent.com/document/product/1084/39387), [SMTP 이메일 전송 가이드](https://intl.cloud.tencent.com/document/product/1084/44458)를 참고하십시오.
2. 다음 매개변수를 설정합니다.
 - 템플릿 선택: 심사 통과된 이메일 템플릿을 선택합니다.
 - 제목: 해당 이메일 제목을 입력합니다.
 - 발신자 선택: 설정된 발신자 주소를 선택합니다.
 - 수신자: 발송할 이메일 주소를 입력합니다. 각 이메일 주소는 엔터 키로 구분합니다.
 - 변수 설정: 해당 변수를 입력합니다. 템플릿에 변수 매개변수가 포함되어 있지 않으면 이 항목을 작성하지 않아도 됩니다.
 - 수신 거부 관리: 이 옵션을 활성화하면 이메일 끝 부분에 수신 거부 링크가 자동 삽입됩니다.
3. 이메일이 성공적으로 발송되면 [**데이터 통계**](https://console.cloud.tencent.com/ses/stats) 인터페이스에서 확인할 수 있으며, 이메일의 상황을 추적해야 하기 때문에 데이터에 지연이 발생하게 됩니다.

