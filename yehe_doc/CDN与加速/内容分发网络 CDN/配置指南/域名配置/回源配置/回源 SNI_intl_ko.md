
## 구성 시나리오

원본 서버 IP에 여러 도메인이 바인딩된 경우 CDN 노드가 HTTPS 프로토콜로 원본 서버에 액세스할 때 특정 액세스 도메인을 지정하도록 Origin-pull SNI를 설정할 수 있습니다.

>!
>- Origin-pull SNI는 현재 중국 내 가속 도메인만 지원합니다.
>- 일부 플랫폼은 업그레이드 중으로, 현재 해당 구성 기능을 지원하지 않을 수 있습니다.

## 구성 가이드

### 구성 조회

기본적으로 Origin-pull SNI는 비활성화 상태이며 실제 필요에 따라 활성화할 수 있습니다.
![]()



### 구성 편집

활성화한 후에는 Origin-pull SNI를 설정하고 구체적인 액세스 도메인을 구성해야 합니다. 구성을 다시 비활성화할 수도 있습니다. 비활성화 상태일 때 아래에 구체적인 구성이 존재해도 현재 네트워크에는 적용되지 않습니다. 활성화 상태일 때만 현재 네트워크에 배포됩니다.
![]()





