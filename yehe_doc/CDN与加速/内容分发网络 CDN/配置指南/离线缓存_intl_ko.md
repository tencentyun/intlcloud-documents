## 구성 시나리오

원본 서버에 장애 발생 시, 즉, Origin-pull이 정상적으로 리소스를 풀링 할 수 없을 때 오프라인 캐시가 활성화된 경우 CDN을 사용하여 콘텐츠를 캐시할 수 있습니다.
- 노드에 캐시된 콘텐츠가 있으면 반환됩니다. 히트 콘텐츠가 만료된 경우에도 원본 서버가 복구되어 정상적인 Origin-pull을 재개할 때까지 반환됩니다.
- 노드에 캐시된 콘텐츠가 없으면 원본 서버가 실패했음을 나타내는 오류 메시지가 반환됩니다.

>!
>- 오프라인 캐시는 일시적으로 중국 내 가속 도메인만 지원합니다.
>- 일부 플랫폼은 업그레이드 중으로, 현재 해당 구성 기능을 지원하지 않을 수 있습니다.

## 구성 가이드

### 구성 조회

기본적으로 오프라인 캐시는 비활성화 상태이며 실제 필요에 따라 활성화/비활성화할 수 있습니다.
![]()







