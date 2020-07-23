
## 설정 시나리오
일반적으로 CDN에 배포된 콘텐츠는 기본적으로 오픈 소스로, 사용자가 URL을 획득하여 액세스할 수 있습니다. referer 블랙리스트/화이트리스트, IP 블랙리스트/화이트리스트, IP 액세스 빈도 제한 등의 액세스 제어 외에도, 고급 타임스탬프 인증 설정을 통해 악성 사용자의 도용을 방지할 수 있습니다.

>타임스탬프 링크 도용 방지 설정 후에는, 클라이언트가 요청을 보낼 때 설정에 따라 서명을 계산하고 서버에 가져옵니다. CDN 노드가 서버를 검증하여 통과한 후에만 통과 허가를 계속할 수 있습니다.

## 설정 가이드
### 설정 조회
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴에서 [도메인 관리]를 선택한 후, 오른쪽의 [관리]를 클릭하면 도메인 설정 페이지로 이동할 수 있습니다. [보안 설정]에서 인증 설정을 확인할 수 있으며 비활성화 상태로 기본 설정되어 있습니다.
![](https://main.qcloudimg.com/raw/77831beaa25a77dd26b60e1f401c8dd3.png)

### 설정 수정
#### 1. 설정 수정
CDN은 4가지 인증 서명 계산 방식을 제공하며, 위의 [인증 계산기]를 통해 각각의 인증 모드 및 설정 후의 효과를 조회할 수 있습니다. 자세한 설명은[TypeA](https://intl.cloud.tencent.com/document/product/228/35222), [TypeB](https://intl.cloud.tencent.com/document/product/228/35223), [TypeC](https://intl.cloud.tencent.com/document/product/228/35224), [TypeD](https://intl.cloud.tencent.com/document/product/228/35225) 등 알고리즘 설명 문서를 참조 바랍니다.
![](https://main.qcloudimg.com/raw/ffd60184fa759b4c7a82a5a49634b8c3.png)

#### 2. 설정 비활성화
인증 설정 스위치를 통해 원클릭으로 설정을 비활성화할 수 있습니다. on-off 스위치가 비활성화 상태일 때 아래쪽에 기존 설정이 존재하더라도 현재 네트워크에 적용되지 않습니다. 이후에 활성화 클릭 시 전체 네트워크에 적용되도록 즉시 배포하지 않고 설정에 대해 2차 확인을 먼저 진행합니다.
![](https://main.qcloudimg.com/raw/5bb10025c5887793807e6b41dbea48a6.png)

#### 3. 지역 특수 설정
사용자의 가속 도메인 서비스 지역이 글로벌 가속이고 중국 내, 중국 외 지역의 인증 설정을 다르게 하길 원한다면 설정 아래의 [특수 설정 추가]를 클릭하여 설정할 수 있습니다.
![](https://main.qcloudimg.com/raw/391372dbf734e813c45640dace716793.png)

>지역 특수 설정을 추가한 후 현재로서는 직접 삭제할 수 없으니 사용자는 설정 비활성화를 통해 사용 안 함으로 설정할 수 있습니다.

## 설정 예시
도메인이 'cloud.tencent.com'인 글로벌 가속 도메인의 인증 설정이 아래와 같을 경우:
![](https://main.qcloudimg.com/raw/6f432b21603b61e4a1d9c17048a675bf.png)
실제 적용 시나리오는 다음과 같습니다.

1. 중국 내 사용자가 실제로 리소스 'http://cloud.tencent.com/1.jpg'에 액세스하는 경우, 바로 요청을 보낼 수 있습니다.
2. 중국 외 사용자가 실제로 리소스 'http://cloud.tencent.com/1.jpg'에 액세스하는 경우, 요청 URL 형식은 'http://cloud.tencent.com/509301d10da7b862052927ed7a947f43/5e561139/1.jpg' 입니다.

