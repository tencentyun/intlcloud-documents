## 설정 시나리오
Tencent Cloud CDN은 HTTPS 가속 서비스를 지원합니다. 사용자는 인증서 업로드를 통해 배포할 수 있고 이미 Tencent Cloud SSL 인증서 관리에 호스팅한 인증서는 바로 CDN 플랫폼에 배포하여 HTTPS 가속 서비스를 활성화함으로써 전체 네트워크의 데이터 암호화 전송을 실현할 수 있습니다.

## 설정 가이드
### 설정 조회

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴에서 [Domain Management]를 선택하고 도메인 오른쪽의 [Manage]를 클릭하면 도메인 설정 페이지의 마지막 탭인 [Advanced Configuration]에서 지정 도메인의 HTTPS 설정 상황을 조회할 수 있습니다:
![](https://main.qcloudimg.com/raw/df6c4966cfee58661251f88550214576.png)
왼쪽 메뉴 [Certificate]페이지로 이동하여 계정 아래 HTTPS 가속을 설정한 모든 도메인 목록을 조회할 수 있습니다:
![](https://main.qcloudimg.com/raw/91335ed0a426118b76ad6b27a53d5197.png)

### 도메인 설정
#### 1. 도메인 선택
[Certificate] 메뉴에서 [Configure Certificate]를 클릭하여 인증서 설정이 필요한 가속 도메인을 선택합니다:
+ 가속 도메인은 "배포중" 또는 "활성화" 상태여야 하고 비활성화 상태인 가속 도메인은 HTTPS 가속 설정을 할 수 없습니다.
+ `.file.myqcloud.com`확장자는 Tencent Cloud COS의 기본 가속 도메인으로 인증서 설정이 필요 없이 바로 HTTPS 가속을 진행할 수 있습니다.
+ `.image.myqcloud.com`확장자는 Tencent Cloud CI의 기본 가속 도메인으로 인증서 설정이 필요 없이 바로 HTTPS 가속을 진행할 수 있습니다.

![](https://main.qcloudimg.com/raw/13c71dc1fc13576620768f7ae61d6c9e.png)

#### 2. 인증서 선택
인증서가 있는 경우, PEM 형식의 인증서와 프라이빗 키를 바로 대응하는 위치에 붙여넣으면 됩니다:
+ Tencent Cloud CDN은 현재 ECC 인증서 배포를 지원합니다.
+ 인증서는 PEM 형식이어야 하며 이 형식이 아닌 인증서는 [PEM 형식 변환](https://intl.cloud.tencent.com/zh/document/product/228/35212)을 참조 바랍니다.
+ Tencent Cloud 호스팅 인증서를 선택하여 바로 원클릭 배포를 진행할 수 있습니다.

![](https://main.qcloudimg.com/raw/d847eb87f076b972808b8e680705f706.png)

#### 3. 원본 요청 방식

가속 도메인에 액세스하거나 원본 서버에서 모듈 설정 시 원본 요청 방식을 설정하는 것 외에도 인증서 설정 시 원본 요청 프로토콜을 조정할 수 있습니다. Tencent Cloud CDN은 아래와 같은 3가지 원본 요청 프로토콜을 지원합니다:
+ HTTP 원본 요청: 모든 요청은 HTTP를 통해 가져옵니다.
+ HTTPS 원본 요청: 모든 요청은 HTTPS를 통해 가져옵니다.
+ 프로토콜 따르기: 요청 프로토콜에 따라 원본을 가져오는데, HTTP 요청은 HTTP 를 통해 가져오고, HTTPS 요청은 HTTPS를 통해 가져옵니다.

![](https://main.qcloudimg.com/raw/62b122177e6ee043d0063c8e5328e1e5.png)

>
> + 프로토콜 따르기 또는 HTTPS 원본 요청을 설정할 때 원본 서버는 유효한 인증서를 배포해야 합니다. 그렇지 않으면 원본 요청에 실패합니다.
> + HTTPS 원본 요청은 현재 443 포트만 지원합니다. 사용자의 원본 서버가 기타 포트로 지정되면 설정에 실패합니다.

### 일괄 설정
상단 [Batch Configuration]을 클릭한 후 인증서 업로드를 통해 해당하는 도메인을 자동으로 매칭하여 일괄 설정합니다
#### 1. 인증서 선택
인증서가 있는 경우, PEM 형식의 인증서와 프라이빗 키를 바로 대응하는 위치에 붙여넣으면 됩니다:
+ Tencent Cloud CDN은 현재 ECC 인증서 배포를 지원합니다.
+ 인증서는 PEM 형식이어야 하며 이 형식이 아닌 인증서는 [PEM 형식 변환](https://intl.cloud.tencent.com/document/product/228/35212)을 참조 바랍니다.
+ Tencent Cloud 호스팅 인증서를 선택하여 바로 원클릭 배포를 진행할 수 있습니다.

![](https://main.qcloudimg.com/raw/fcadb92849ebd780acbbc5b35f343478.png)

#### 2. 도메인 선택
업로드 / 선택한 인증서에 따라 CDN은 설정이 허용된 도메인 목록을 자동 매칭하며 수요에 따라 설정을 선택할 수 있습니다:
![](https://main.qcloudimg.com/raw/04a8ad1088655f24282201da7b5ebd74.png)

#### 3. 원본 요청 방식
가속 도메인에 액세스하거나 원본 서버에서 모듈 설정 시 원본 요청 방식을 설정하는 이외에도 인증서 일괄 설정 시 원본 요청 프로토콜을 일괄 조정할 수 있습니다. Tencent Cloud CDN은 아래와 같은 3가지 원본 요청 프로토콜을 지원합니다:
+ HTTP 원본 요청: 모든 요청은 HTTP를 통해 가져옵니다.
+ HTTPS 원본 요청: 모든 요청은 HTTPS를 통해 가져옵니다.
+ 프로토콜 따르기: 요청 프로토콜에 따라 원본을 가져오는데, HTTP 요청은 HTTP 를 통해 가져오고, HTTPS 요청은 HTTPS를 통해 가져옵니다.

>
> + 일괄 설정 제출 후 선택한 도메인은 차례로 인증서를 배포합니다. 비정상 상황이 발생하면 목록 페이지는 "업데이트 실패" 상태가 되며 이때 기존 설정은 여전히 계속 적용됩니다.
> + 업데이트 실패 시, 오른쪽 [Edit]를 클릭하여 다시 설정할 수 있습니다.

### 인증서 변경
#### 인증서 수정
인증서 오른쪽 [Edit]를 클릭한 후 도메인을 지정하여 인증서를 업데이트할 수 있고 다시 일괄 설정하여 기존의 인증서 설정을 덮어씌울 수도 있습니다.
![](https://main.qcloudimg.com/raw/bb2ed5ec740aa67abf2750dc58baae0d.png)
업데이트된 인증서는 전체 네트워크에서 노드에 차례로 적용되고 매끄럽게 전환되어 현재 네트워크 HTTPS 서비스에 영향을 미치지 않습니다. [Delete]를 클릭하여 HTTPS 가속 서비스를 취소할 수도 있습니다.

#### 인증서 만료
인증서 만료 30일 전, 15일 전, 7일 전 및 만료 당일에 Tencent Cloud는 SMS, 메일, 내부 메시지 형태로 사용자 계정에 만료 알림을 보냅니다. 현재 이미 SSL 인증서 사용자 정의 수신자 알람이 지원되고 있으며 [메시지 구독](https://console.cloud.tencent.com/message/subscription) 설정으로 이동할 수 있습니다.

### 리전 특수 설정
가속 도메인의 서비스 지역이 글로벌인 경우, HTTPS 인증서 설정은 중국 내, 중국 외에 동일하게 적용되며 중국 내, 중국 외 다른 인증서를 설정하는 것을 지원하지 않습니다.

도메인에 중국 내, 중국 외의 인증서 설정이 다른 특수한 시나리오가 존재할 경우, [Certificate] 페이지에서 중국 내, 중국 외 등의 식별을 확인할 수 있으며 이는 해당 도메인이 남은 지역에서 특수 설정이 존재한다는 것을 의미합니다:
도메인 [Advanced Configuration]에서 두 가지 설정을 확인할 수 있습니다.
사용자의 가속 도메인에 이러한 특수 설정이 있고 그중 어느 한 인증서를 변경해야 할 경우, [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 수정 바랍니다.

