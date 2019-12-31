CND은 비즈니스 필요에 따라 캐싱 시 사용자 요청 URL에서 **”?”** 다음의 파라미터가 필터링 여부를 제어할 수 있는 필터링 파라미터 스위치를 제공합니다.필터링 파라미터를 사용하여 버전을 제어하거나 Token으로 리소스를 인증 할 수 있습니다.
>  리소스 URL의 파라미터가 동일한 내용을 나타내는 경우, 캐시 히트율을 효과적으로 향상하기 위해 필터링 파라미터를 활성화하는 것이 좋습니다.

## 구성 안내
1. [CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 왼쪽 디렉터리 [도메인 관리]를 클릭합니다. 관리 페이지로 이동하여 목록에서 편집해야 하는 도메인 이름을 찾아 작업표시줄에서 [관리]를 클릭하십시오.
2. [액세스 제어] 탭을 클릭하여 필터링 파라미터 구성 모듈에서 필터링 파라미터를 구성하십시오.
![img](https://main.qcloudimg.com/raw/696b14c83d40fc433bef12f199dd8e5a.jpg)

>?가속 유형이 다운로드 또는 리퀘스트 경우 기본적으로 필터링 파라미터가 활성화되며, 액세스할 때 가속 유형을 정적으로 선택하면 필터링 파라미터가 기본적으로 비활성화 상태입니다.

## 구성 사례
CDN은 노드 스토리지 구조에서 리소스를 캐시할 때, cache_key를 인덱스로 하여 저장된 리소스를 찾습니다.
1. 구성이 다음과 같은 경우
   ![img](https://main.qcloudimg.com/raw/e720e78f96e74ad7bfbde09b4de6a219.png)
   - 사용자 A가 URL을 `http://www.test.com/1.jpg?version=1.1`로 요청하여 노드가 리소스를 저장할 때, 해당 `cache_key`를 `www.test.com/1.jpg `하여, "?" 뒤의 파라미터를 생략합니다.
   - 사용자 B 또한 URL을 'http://www.test.com/1.jpg?version=1.2'로 요청하여 'cache_key'를 `www.test.com/1.jpg`에 따라 리소스를 찾으면, 사용자 A가 요청한 것과 동일한 내용으로 간주하여 도달할 수 있습니다.
2. 구성이 다음과 같은 경우
   ![img](https://main.qcloudimg.com/raw/696b14c83d40fc433bef12f199dd8e5a.jpg)
   - 사용자 A가 URL을`http://www.test.com/1.jpg?version=1.1`로 요청하여 노드가 리소스를 저장할 때, 해당 `cache_key`를 `www.test.com/1.jpg로 하여 ? version = 1.1`, "?" 뒤의 파라미터가 생략되지 않습니다.
   - 사용자 B는 또한 URL이`http://www.test.com/1.jpg?version=1.2` 인 리소스를 요청하여 `cache_key`를 `www.test.com/1.jpg?version=1.2` 에 따라 리소스를 찾습니다. 도달하지 못할 경우, 다시 원본 서버로 돌아가 해당 콘텐츠를 가져와서 캐시합니다.

