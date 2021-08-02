라이브 방송 도메인은 간단한 HTTP 프로토콜을 사용합니다. HTTP는 SSL/TLS 프로토콜을 이용해 HTTPS로 캡슐화되어 데이터 암호화 전송을 실현합니다. 다수의 도메인 일괄 관리 및 SSL 인증서를 설정해야 할 경우, [인증서 관리]를 통해 일괄 조회 및 SSL 인증서 일괄 설정이 가능합니다.

## 설정 원리
도메인의 SSL 인증서 설정은 전송 과정에서 사용자의 핵심 정보를 암호화하기 위한 것입니다. SSL 인증서를 기반으로 웹 사이트를 HTTP(Hypertext Transfer Protocol)에서 HTTPS(Hyper Text Transfer Protocol over Secure Socket Layer)로 전환할 수 있습니다. 즉, 보안 소켓 계층(SSL)을 기반으로 안전하게 데이터를 전송하는 암호화 버전 HTTP 프로토콜입니다. 

[](id:c_ssl)
## 인증서 구성
1. CSS 콘솔의 [도메인 이름 관리](https://console.cloud.tencent.com/live/domainmanage)에 들어가 [인증서 관리]를 클릭해 인증서 관리 설정 페이지로 들어갑니다.
![](https://main.qcloudimg.com/raw/e39413b101a445ed747d78c8c9e7c8ac.png)
2. [인증서 구성]을 클릭하여 새 인증서 설정을 생성합니다.
![](https://main.qcloudimg.com/raw/5aeee06ba8b978b823be16e9191bf705.png)
3. 인증서 설정 팝업 창에서 인증서 업로드 방식을 선택합니다. 이중 Tencent Cloud는 두 종류의 인증서 소스를 지원합니다.
  - **자체 인증서**: 인증서 비고를 작성하고 인증서 내용과 인증서 키를 입력해야 합니다. 해당 인증서가 저장되면 [SSL 인증서 관리](https://console.cloud.tencent.com/ssl)로 동기화되어 여기서 인증서를 확인할 수 있습니다. 인증서 내용 및 인증서 키 입력 작업은 [HTTPS 설정](https://intl.cloud.tencent.com/document/product/267/31066)을 참고하십시오.
![](https://main.qcloudimg.com/raw/998de2fdadf6ed9ab52e7fdcef288f51.png)
  - **Tencent Cloud 호스팅 인증서**: Tencent Cloud의 SSL 인증서 관리에서 구매한 인증서를 선택하면 인증서 리스트를 통해 인증서에 적합한 가속 도메인을 선택할 수 있습니다.
![](https://main.qcloudimg.com/raw/4f36c491c7392798bc81410ecc65ae6e.png)
4. 인증서 검사 후, [다음]을 클릭하여 도메인 설정 페이지로 들어갑니다.
5. '연결 도메인'에서 인증서 도메인에 따라 일치하는 재생 도메인을 선택합니다(다중 선택 가능). 현재 도메인이 이미 기타 인증서로 바인딩 되어 있을 경우, 덮어쓰기로 인증서를 업데이트합니다.
6. 선택 후 우측 '선택됨' 란에 선택된 도메인과 바인딩 된 상태 효과가 표시됩니다.
![](https://main.qcloudimg.com/raw/bc1a0c51023d295120b8c94420b7b628.png)
7. 선택한 도메인에 HTTPS 구성 활성화 여부 선택
  >? 
  >- [HTTPS 설정 동시 활성화] 버튼은 HTTPS 활성화 설정 선택을 지원합니다. 활성화하면 HTTP 와 HTTPS를 동시에 지원하며, 비활성화하면 HTTP만 지원합니다.
  >- [HTTPS 설정 동시 활성화] 버튼은 기본적으로 활성화되어 있으므로 저장 후 업데이트된 도메인은 모두 HTTPS 설정이 활성화 되고, 비활성화하면 하면 새 인증서만 업데이트되고 HTTPS의 활성화/비활성화는 수정되지 않습니다.
6. [확인]을 클릭해 인증서 설정을 완료합니다.


[](id:check)
## 인증서 설정 조회
[인증서 구성](#c_ssl) 완료 후, [인증서 관리](https://console.cloud.tencent.com/live/common/certificate)의 설정 목록에서 생성된 설정 정보를 조회할 수 있습니다. 확인 가능한 데이터 패키지는 인증서 설정의 도메인, 인증서 비고, 인증서 출처, HTTPS 설정 및 만료 기간을 포함합니다.
![](https://main.qcloudimg.com/raw/e4012e075b695afc912840462e0c5694.png)

[](id:update)
## 인증서 설정 업데이트
1. [인증서 관리](https://console.cloud.tencent.com/live/common/certificate)의 설정 목록에서, **업데이트**가 필요한 설정 열 우측에 있는 [업데이트]를 클릭합니다.
![](https://main.qcloudimg.com/raw/bfad71179c2ab41cd3c35e23e47e0224.png)
2. 인증서 설정 페이지에 들어가 [인증서 구성](#c_ssl) 정보를 재설정 합니다.
3. [확인]을 클릭해 다시 제출하면 인증서가 바로 업데이트됩니다.

[](id:delete)
## 인증서 바인딩 삭제
1. [인증서 관리](https://console.cloud.tencent.com/live/common/certificate)의 설정 목록에서, **삭제**가 필요한 설정 정보 우측에 있는 [삭제]를 클릭합니다.
![](https://main.qcloudimg.com/raw/a5d8f92c8aa7f2264c56e5ef6bf1f15b.png)
2. 인증서 바인딩 삭제 여부를 확인하고 [확인]을 클릭하면 바로 삭제됩니다.
![](https://main.qcloudimg.com/raw/10305e0609cfcda523505cbcf8a099c8.png)
>! 삭제 후 해당 도메인은 HTTPS 구성을 사용할 수 없습니다.


