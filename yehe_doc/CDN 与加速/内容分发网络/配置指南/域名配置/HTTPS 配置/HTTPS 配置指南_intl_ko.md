## 설정 시나리오
Tencent Cloud CDN은 HTTPS 가속 서비스를 지원합니다. 인증서 업로드를 통해 배포하거나 Tencent Cloud SSL 인증서 관리에 호스팅된 인증서를 CDN 플랫폼에 바로 배포하여 HTTPS 가속 서비스를 활성화하고 전체 네트워크의 데이터 암호화 전송을 구현할 수 있습니다.

## 설정 가이드
### 설정 조회

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴바에서 [도메인 관리]를 선택하고 도메인 오른쪽의 [관리]를 클릭하면 도메인 설정 페이지의 [Https 설정]에서 지정 도메인의 HTTPS 설정 상황을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/df6c4966cfee58661251f88550214576.png)
왼쪽 메뉴바의 [인증서 관리] 페이지로 이동하여 계정에서 HTTPS 가속을 설정한 모든 도메인 리스트를 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/91335ed0a426118b76ad6b27a53d5197.png)

### 인증서 설정
#### 1. 도메인 선택
[인증서 관리] 메뉴바에서 [인증서 설정]를 클릭하여 인증서를 설정할 가속 도메인을 선택합니다:
+ 가속 도메인은 '배포 중' 또는 '활성화' 상태여야 하며, 비활성화 상태인 가속 도메인은 HTTPS 가속 설정을 할 수 없습니다.
+ `.file.myqcloud.com` 확장명은 Tencent Cloud COS의 기본 가속 도메인이며, 인증서 설정 없이 바로 HTTPS 가속을 진행할 수 있습니다.
+ `.image.myqcloud.com` 확장명은 Tencent Cloud CI의 기본 가속 도메인이며, 인증서 설정 없이 바로 HTTPS 가속 서비스를 진행할 수 있습니다.

![](https://main.qcloudimg.com/raw/13c71dc1fc13576620768f7ae61d6c9e.png)

#### 2. 인증서 선택
인증서가 있는 경우, PEM 포맷의 인증서 콘텐츠와 개인키를 바로 해당하는 위치에 붙여 넣으면 됩니다.
+ Tencent Cloud CDN은 ECC 인증서 배포를 지원합니다.
+ 인증서 콘텐츠는 PEM 포맷이어야 하며, 다른 포맷의 인증서일 경우 [PEM 포맷으로 변환](https://intl.cloud.tencent.com/document/product/228/35212)을 참조하십시오.
+ Tencent Cloud 호스팅 인증서를 선택하여 일괄 배포할 수 있습니다.

![](https://main.qcloudimg.com/raw/d847eb87f076b972808b8e680705f706.png)



### 일괄 설정
상단의 [일괄 설정]을 클릭한 후 인증서 업로드를 통해 해당하는 도메인을 자동으로 매칭하여 일괄 설정합니다.
#### 1. 인증서 선택
인증서가 있는 경우, PEM 포맷의 인증서 콘텐츠와 개인키를 바로 해당하는 위치에 붙여 넣으면 됩니다.
+ Tencent Cloud CDN은 ECC 인증서 배포를 지원합니다.
+ 인증서 콘텐츠는 PEM 포맷이어야 하며, 다른 포맷의 인증서일 경우 [PEM 포맷으로 변환](https://intl.cloud.tencent.com/document/product/228/35212)을 참조하십시오.
+ Tencent Cloud 호스팅 인증서를 선택하여 일괄 배포할 수 있습니다.

![](https://main.qcloudimg.com/raw/fcadb92849ebd780acbbc5b35f343478.png)

#### 2. 도메인 선택
업로드/선택한 인증서에 따라 CDN이 설정 가능한 도메인 리스트를 자동으로 매칭하며, 필요에 따라 설정을 선택합니다.
![](https://main.qcloudimg.com/raw/04a8ad1088655f24282201da7b5ebd74.png)



### 인증서 변경
#### 인증서 수정
인증서 오른쪽의 [편집]을 클릭한 후 도메인을 지정하여 인증서를 업데이트할 수 있으며, 다시 일괄 설정하여 기존의 인증서 설정을 덮어쓸 수도 있습니다.
![](https://main.qcloudimg.com/raw/bb2ed5ec740aa67abf2750dc58baae0d.png)
업데이트된 인증서는 전체 네트워크의 노드에 적용되며, 기존 네트워크의 HTTPS 서비스에 영향을 주지 않고 매끄럽게 전환됩니다. 또한 [삭제]를 클릭하여 HTTPS 가속 서비스를 취소할 수도 있습니다.

#### 인증서 만료
인증서 만료 30일 전, 15일 전, 7일 전, 만료 당일에 Tencent Cloud에서 SMS, 이메일, 내부 메시지 형태로 사용자 계정에 만료 알림을 보냅니다. 현재 SSL 인증서 사용자 정의 알람 수신자 기능이 지원되며, [메시지 구독](https://console.cloud.tencent.com/message/subscription)에서 설정할 수 있습니다.

### 리전 특수 설정
가속 도메인 서비스 지역이 글로벌인 경우, 설정한 HTTPS 인증서가 중국 내외에 똑같이 적용되지만 현재 중국 내외에서 설정한 다른 인증서는 지원하지 않습니다.

도메인에 중국 내외의 인증서 설정과 다른 특수 시나리오가 있는 경우, [인증서 관리] 페이지에서 중국 내외 등의 식별 정보를 확인할 수 있습니다. 이는 해당 도메인에 남아 있는 지역에 대한 특수 설정이 존재한다는 것을 의미합니다.
![](https://main.qcloudimg.com/raw/23192c43c0611c34d07490f19ea7dfb0.png)
도메인 [고급 설정]에서 다음 두 가지 설정을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/febb17a67f10eb81941013895e67913f.png)


