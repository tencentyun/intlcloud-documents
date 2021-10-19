[](id:q1)
### HTTPS란 무엇인가요?
HTTPS는 HTTP 프로토콜을 기반으로 암호화된 보안 프로토콜 전송을 진행하여 데이터 전송 보안을 보장하는 하이퍼 텍스트 전송 보안 프로토콜(Hypertext Transfer Protocol Secure)을 의미합니다. HTTPS 설정 시 도메인에 대응하는 인증서가 필요하며, 이를 전체 네트워크 CDN 노드에 배포하여 전체 네트워크의 데이터 암호화 전송 기능을 구현할 수 있습니다.

[](id:q2)
### CDN은 HTTPS 설정을 지원하나요?
Tencent Cloud CDN은 현재 HTTPS 설정을 지원하고 있습니다. 사용자는 보유 중인 인증서를 업로드하여 배포하거나, [인증서 관리 콘솔](https://console.cloud.tencent.com/ssl)에서 Trust Asia가 무료로 제공하는 3rd party 인증서를 신청할 수 있습니다.

[](id:q3)
### HTTPS 인증서는 어떻게 설정하나요?
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에서 HTTPS 인증서를 설정할 수 있습니다. 자세한 내용은 [HTTPS 설정](https://intl.cloud.tencent.com/document/product/228/35213)을 참조하십시오.

[](id:q4)
### 원본 서버의 HTTPS 인증서를 업데이트한 후 CDN에서 업데이트를 동기화해야 하나요?
동기화하지 않아도 됩니다. 원본 서버의 HTTPS 인증서가 업데이트되면 CDN의 HTTPS 인증서에 영향을 미치지 않습니다. CDN에서 설정한 HTTPS 인증서 기한이 곧 만료되거나 이미 만료된 경우에는 CDN에서 HTTPS 인증서를 업데이트해야 합니다.


[](id:q5)
### CDN에서 사용자의 HTTPS 액세스만 허용하고, HTTP 액세스는 차단할 방법이 있나요?
[강제 리디렉션 기능](https://intl.cloud.tencent.com/document/product/228/35214)을 사용하십시오. HTTPS 인증서 설정을 완료하면 Http->Https 기능을 활성화할 수 있으며, 기능 활성화 시 사용자가 HTTP 요청을 보내더라도 HTTPS 액세스로 강제 리디렉션됩니다.
![](https://main.qcloudimg.com/raw/c562127135d558445481ab97973b1ebe.png)


[](id:q6)
### CDN을 설정했으나 HTTPS에 액세스할 수 없습니다.

HTTPS로 액세스하는 방법은 다음과 같습니다.
1. [CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인한 뒤, 왼쪽 메뉴의 [도메인 관리]를 클릭해 도메인 관리 페이지에 들어갑니다. 이후 도메인 오른쪽의 [관리] 버튼을 클릭하여 관리 페이지에 들어갑니다.
![](https://main.qcloudimg.com/raw/33ea31c11bfac2022ea5753b6d849042.png)
2. [Https 설정]을 클릭하면 HTTPS 설정 모듈을 찾을 수 있습니다. [설정하기]를 클릭하여 인증서 관리 화면으로 이동한 뒤 인증서를 설정합니다. 설정 프로세스는 [인증서 설정](https://intl.cloud.tencent.com/document/product/228/35213#.E8.AF.81.E4.B9.A6.E9.85.8D.E7.BD.AE)을 참조하십시오.
![](https://main.qcloudimg.com/raw/67be1f3b42a411613c0500afa97e06b5.png)
인증서 설정이 완료되면 HTTPS 액세스를 활성화할 수 있습니다.



