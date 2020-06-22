### HTTPS란 무엇인가요?
HTTPS는 HTTP 프로토콜을 기반으로 암호화된 보안 프로토콜 전송을 진행하여 데이터 전송 보안을 보장하는 하이퍼 텍스트 전송 보안 프로토콜(Hypertext Transfer Protocol Secure)을 의미합니다. HTTPS 설정 시 도메인에 대응하는 인증서가 필요하며, 이를 전체 네트워크 CDN 노드에 배포하여 전체 네트워크의 데이터 암호화 전송 기능을 구현할 수 있습니다.

### CDN은 HTTPS 설정을 지원하나요?
Tencent Cloud CDN은 현재 HTTPS 설정을 지원하고 있습니다. 사용자는 보유 중인 인증서를 업로드 하여 배포하거나, [인증서 관리 콘솔](https://console.cloud.tencent.com/ssl)에서 Trust Asia가 무료로 제공하는 3rd party 인증서를 신청할 수 있습니다.

### HTTPS 인증서는 어떻게 설정하나요?
CDN 콘솔에서 HTTPS 인증서를 설정할 수 있습니다. 자세한 내용은 [HTTPS 설정](https://intl.cloud.tencent.com/document/product/228/35213)을 참조 바랍니다.

### 원본 서버의 HTTPS 인증서를 업데이트한 후 CDN에서 업데이트를 동기화해야 하나요?
사용자의 Origin-pull 방식에 따라 달라집니다.
HTTP Origin-pull: 동기화가 필요하지 않습니다.
HTTPS Origin-pull: 원본 서버에서 인증서를 업데이트할 경우, CDN에서도 해당 업데이트를 동기화해야 합니다. 클라이언트에서 노드, 노드에서 원본 서버까지 인증서가 일치하지 않을 경우 Origin-pull 오류가 발생할 수 있습니다.

### CDN에서 사용자의 HTTPS 액세스만 허용하고, HTTP 액세스는 차단할 방법이 있나요?
HTTPS 강제 기능을 사용하세요. 인증서 설정을 완료하면 "강제 리디렉션" 옵션이 표시되며, 옵션 활성화 시 사용자가 HTTP 요청을 보내더라도 HTTPS 액세스로 강제 리디렉션 됩니다.
![](https://main.qcloudimg.com/raw/0352df67305e2e7f4c6df51b0b1afc09.png)


### CDN을 설정했으나 HTTPS에 액세스할 수 없습니다.

웹 사이트의 HTTPS 인증서를 CDN에 업로드해야 합니다. 방법은 아래와 같습니다.
1. [CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인한 뒤, 왼쪽 메뉴의 [Domain Management]를 클릭해 도메인 관리 페이지에 들어갑니다. 이후 도메인 오른쪽의 [manage] 버튼을 클릭하여 관리 페이지에 들어갑니다.
![이미지 설명](https://main.qcloudimg.com/raw/9f5202ff57eb14f40dee3b15e4a37cdf.png)
2. [Advanced Configuration]을 클릭하여 HTTPS 설정 모듈을 찾습니다. 해당 모듈에서 [Configure Now]를 클릭하여 인증서 관리 페이지에 접속해 인증서를 설정합니다. 설정 방법은 [Certificate](https://intl.cloud.tencent.com/document/product/228/35213#.E5.9F.9F.E5.90.8D.E9.85.8D.E7.BD.AE)를 참조 바랍니다. ![이미지 설명](https://main.qcloudimg.com/raw/f8c4570d1a4847aab84c30ff0dc2e22d.png)
3. 인증서 설정을 완료하면 [HTTPS 강제 리디렉션] 옵션이 표시되며, 옵션 활성화 시 사용자가 HTTP 요청을 보내더라도 HTTPS 액세스로 강제 리디렉션 됩니다:
![이미지 설명](https://main.qcloudimg.com/raw/da5fb8ee7294231e27d65cd177dfd992.png)



