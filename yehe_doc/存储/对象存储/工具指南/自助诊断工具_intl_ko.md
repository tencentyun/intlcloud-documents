## 기능 개요
Cloud Object Storage(COS) 자가 진단 툴은 Tencent Cloud COS가 제공하는 Web 툴로, 오류 요청의 자가 진단 및 문제 해결에 사용됩니다. 툴 페이지에 요청 RequestId (획득 방법은 [RequestId 획득 작업 가이드](https://intl.cloud.tencent.com/document/product/436/41230)참고)를 입력하고, 진단을 클릭하면 해당 요청에 대해 스마트 진단이 진행되고 요청 기본 정보 및 도움말 가이드와 진단 알림도 표시하여 COS API의 오류 문제를 신속하게 해결할 수 있게 도와줍니다. 

## 툴 주소
[COS 자가 진단 툴](https://console.cloud.tencent.com/cos5/diagnose)을 클릭하여 이동합니다. 

## 사용 방법

1. [COS 자가 진단 툴](https://console.cloud.tencent.com/cos5/diagnose)을 클릭하여 ‘COS 자가 진단 툴’ 페이지로 이동합니다.


2. 상단의 RequestId 입력창에, 진단할 RequestId를 입력하고, [진단 시작]을 클릭합니다.

3. 잠시 후 스마트 진단 결과를 보실 수 있습니다. 

진단 결과는 진단 결과와 요청 정보 두 부분으로 구성됩니다. 
 - 진단 결과는 진단 요청에 대한 권장 사항과 도움말로 이를 기반으로 COS API의 오류 문제를 빠르게 파악할 수 있습니다.
 - 요청 정보는 해당 RequestId에 상응하는 기본 정보입니다.

4. 진단 결과에 대한 피드백 보내기
진단 결과 하단의 [도움이 됨] 또는 [도움이 안 됨]을 클릭하면 해당 진단 결과에 대한 피드백을 보내주시면 툴 최적화 작업에 도움이 됩니다.


## FAQ

RequestId를 통한 진단 기능 외에도, 본 툴은 다양한 FAQ 예시와 이에 대한 솔루션을 제공하므로, 사용자는 더욱 편리하게 COS API 사용하고 관련 문제를 해결할 수 있습니다. 더 궁금하신 내용은 [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하시기 바랍니다.


## 주의 사항

표준 COS 요청 RequestId는 다음과 같은 특징이 있습니다.
1. 대문자 N으로 시작. 
2. 길이는 30자를 초과할 수 없음. 
3. Base64 기준 준수.
