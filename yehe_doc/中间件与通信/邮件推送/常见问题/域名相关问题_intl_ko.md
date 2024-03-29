[](id:que1) 
###  DNS를 어떻게 구성해야 합니까?
- Tencent Cloud DNS 서비스를 사용하는 경우 [Tencent Cloud 콘솔](https://console.cloud.tencent.com/cns)에 로그인하여 구성합니다.
- 다른 도메인 서비스 제공업체에서 제공하는 DNS 서비스를 사용하는 경우 DNS 확인을 위해 도메인을 Tencent Cloud로 이전할 수 있습니다.
- 이 밖의 경우에는 도메인 서비스 제공업체에서 구성하십시오.


[](id:que2) 
### 필요에 따라 DNS를 구성한 후 유효성 검사가 실패하는 이유는 무엇입니까?
 DNS를 동기화하는 데 일반적으로 10분이 걸립니다. 그러나 TTL에 따라 약간의 지연이 있을 수 있습니다. 툴을 사용하여 구성된 DNS가 올바른지 확인하십시오. 문제가 없으면 기다려 주시기 바랍니다.

[](id:que3) 
### SES를 사용하려면 내 도메인에 대한 ICP 비안을 받아야 합니까?
- 이메일을 보내는 데만 도메인을 사용하는 경우에는 필요하지 않습니다.
- 도메인의 A 레코드가 중국 본토 서버를 가리키는 경우 도메인에 대한 ICP 비안을 완료해야 합니다.

[](id:que4) 
### 엔터프라이즈 이메일 도메인을 SES 이메일 도메인으로 사용할 수 있습니까?
SPF와 MX 레코드 간의 충돌을 방지하려면 엔터프라이즈 이메일 도메인을 SES 이메일 도메인으로 사용하지 마십시오.
함께 사용해야 하는 경우 SPF 레코드를 병합해야 합니다. 기존 발신자 도메인 아래에 레벨2 도메인을 만들고 사용할 수도 있습니다.

[](id:que5) 
### 동일한 기본 도메인 아래의 서브 도메인을 SES에서 사용할 수 있습니까?
네. 사용할 수 있습니다.

[](id:que6) 
### 다른 서브 도메인이 다른 이메일 서비스를 사용하는 경우 영향이 있습니까?
아니요. 영향이 없습니다.
