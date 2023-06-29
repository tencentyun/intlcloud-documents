## 설정 시나리오

만약 비즈니스 시나리오에서 리소스 URL 경로의 대소문자 차이가 리소스 콘텐츠와 연관이 없다면, 대소문자를 구분하지 않는 캐시 설정을 활성화하여 히트율을 일정 수준 높일 수 있습니다.

## 설정 가이드

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴에서 [Domain Management]를 선택하고 도메인 오른쪽의 [Manage]를 클릭하면, 도메인 설정 페이지의 세 번째 메뉴인 [캐시 설정]의 최하단에서 [대소문자를 구분하지 않는 캐시]를 확인할 수 있습니다. 해당 항목은 비활성화 상태로 기본 설정되어 있습니다.
![](https://main.qcloudimg.com/raw/95ccb4da3a7589d085658e3965572dee.png)

## 설정 예시

CDN 노드가 리소스를 캐싱할 때 Key-Value 형식에 따라 인덱스를 생성하며, 그중 Key는 CDN 노드의 캐시 키(Cache Key)를 의미합니다. 필터링 매개변수 설정을 통한 최적화 외에도, 대소문자를 구분하지 않는 캐시를 설정하여 최적화를 진행할 수 있습니다.
가속 도메인이 `cloud.tencent.com`이며, 사용자의 액세스 시나리오는 아래와 같다고 가정합니다.

- 사용자 A의 액세스 리소스: `http://cloud.tencent.com/abc.JPG`
- 사용자 B의 액세스 리소스: `http://cloud.tencent.com/abc.jpg`
  
사용자 A/B가 모두 CDN 노드 X에 액세스하며, 노드 X에는 상기 두 리소스의 캐시가 없다고 가정할 때, 대소문자를 구분하지 않는 캐시는 비활성화 상태로 기본 설정되어 있으므로, 액세스 과정은 다음과 같습니다.
- 사용자 A가 액세스한 원본 서버가 `http://cloud.tencent.com/abc.JPG` 이미지를 가져와 CDN 노드 X에 캐싱하며, 이에 대응하는 캐시 키는 `http://cloud.tencent.com/abc.JPG`가 됩니다.
- 사용자 B가 액세스한 원본 서버가 `http://cloud.tencent.com/abc.jpg` 이미지를 가져와 CDN 노드 X에 캐싱하며, 이에 대응하는 캐시 키는 `http://cloud.tencent.com/abc.jpg`가 됩니다.
  
대소문자를 구분하지 않는 캐시 설정을 활성화하면 상기 시나리오의 액세스 과정은 다음과 같습니다.
- 사용자 A가 액세스한 원본 서버가 `http://cloud.tencent.com/abc.JPG` 이미지를 가져와 CDN 노드 X에 캐싱하며, 이에 대응하는 캐시 키는 `http://cloud.tencent.com/abc.jpg`가 됩니다.
- 사용자 B의 액세스는 CDN 노드 X에서 리소스에 히트하여, 필요한 콘텐츠를 바로 가져옵니다.
