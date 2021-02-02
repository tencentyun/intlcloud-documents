
## 설정 시나리오

Tencent Cloud CDN 캐시 리소스가 트리거 방식이고 사용자가 특정 리소스에 액세스하는 경우, 요청을 받은 CDN 노드에서 해당 리소스를 캐시하지 않으면 사용자 원본 서버로 돌아와 리소스를 가져옵니다. 리소스(2XX 상태 코드) 가져오기에 성공하면 노드에서 캐시하고 사용자에게 반환합니다.

CDN 노드에 캐시하는 리소스는 직접 관리할 수 없습니다. 원본 서버 리소스가 변경되었는데도 CDN 노드가 기존 리소스를 캐시해 사용자에게 반환하는 것이 우려되는 경우, 노드 캐시 규칙 설정을 통해 일정 수준의 제어가 가능합니다.


## 설정 가이드

### 설정 조회

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인한 후, 왼쪽 메뉴바에서 [Domain Management]를 선택한 뒤 도메인 작업 열의 [Manage]를 클릭하여 도메인 설정 페이지로 들어갑니다. Tab을 [Cache Configuration]로 전환하면 [Node Cache Validity Configuration]을 찾을 수 있습니다.

가속 도메인 액세스 시, 서비스 유형별로 CDN에서 기본 노드 캐시 만료 규칙을 추가하며, 필요에 따라 변경할 수 있습니다.
- 정적 가속 서비스 유형을 선택하는 경우 일반적인 동적 파일(예: php, jsp, asp, aspx)은 기본적으로 캐시하지 않으며, 기타 모든 문서는 원본 서버를 따릅니다.
![](https://main.qcloudimg.com/raw/5f48bc5246397975544baadf5ac81f4e.png)
- 가속 다운로드, 스트림 미디어 VOD 서비스 유형을 선택하는 경우 모든 파일의 기본 캐시 만료 시간은 30일입니다.
![](https://main.qcloudimg.com/raw/cdd00154330b8cb217287874f4f40693.png)

### 규칙 추가

파일 유형/폴더/전체 경로 파일을 지정하여 노드 캐시를 설정할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/5454a77683dca1cfb491eccdae839aa4.png" height="207" width="408" />


- 원본 서버 준수: 원본 서버의 Cache-Control 헤더를 따릅니다.
 - 원본 서버에 해당하는 HTTP Response Header에 Cache-Control 필드가 있는 경우,
 Cache-Control 필드가 max-age면 CDN 노드에서 리소스를 캐시하는 시간은 max-age 값을 따릅니다.
 Cache-Control 필드가 no-cache/no-store/private면 CDN 노드는 리소스를 캐시하지 않습니다.
 - 원본 서버의 상응하는 HTTP Response Header에 Cache-Control 필드가 없는 경우, CDN 노드는 리소스를 캐시하지 않습니다.
**참고:** 해당 경우 일부 플랫폼에는 다음과 같은 정책이 있습니다. 첫 번째 요청은 원본을 불러와 CDN 노드에서 해당 리소스를 캐시하고, 재요청이 노드 캐시에 히트되는 경우 CDN은 기본적으로 Cache-Control: max-age=600 헤더를 추가합니다.
- 캐시: CDN 노드에서의 리소스 캐시 시간을 설정합니다.
- 강제 캐시: “캐시”로 선택하는 경우 강제 캐시 여부를 추가 설정(즉, 원본 서버의 Cache-Control: no-cache/no-store/private 생략 여부)할 수 있으며, 기본적으로 “아니오”로 설정되어 있습니다.
**참고:** “강제 캐시”를 “예”로 선택하는 경우 CDN 노드에서의 리소스 캐시 시간은 해당 설정 시간을 따릅니다.
　　“강제 캐시”를 “아니오”로 선택하고 원본 서버의 Cache-Control 필드가 no-cache/no-store/private인 경우, 캐시 시간을 설정했다 하더라도 CDN 노드는 리소스를 캐시하지 않습니다.
- 캐시하지 않음: CDN 노드에서 리소스를 캐시하지 않습니다.




#### 설정 제한

- 도메인당 최대 20개까지 캐시 규칙을 추가할 수 있습니다.
- 다수 규칙에 우선순위 변경 지원: 하위 우선순위가 상위 우선순위보다 높습니다.
**참고:** 모든 파일 - max-age 규칙 없음이 기본적으로 우선순위가 가장 낮으며 우선순위는 변경할 수 없습니다.
- 단일 파일 유형/폴더/전체 경로 파일 규칙에는 최대 100개까지 콘텐츠를 입력할 수 있으며, 각 콘텐츠 사이에 “;” 부호를 사용하여 분리합니다. 예: 파일 유형 - jpg;png


>! 인벤토리가 노드 캐시 만료 설정(Old)(즉, 기본 모드)인 경우 고급 모드 설정에 따라 제출 후 전체 업그레이드하며, 기존의 기본 모드로 복구할 수 없습니다.





## 설정 예시

가속 도메인 `www.test.com`의 [노드 캐시 만료 설정]이 다음과 같은 경우,
![](https://main.qcloudimg.com/raw/c1402003c4549d2e6035420921f67bd0.png)

실제 캐시 상황은 다음과 같습니다.

- 원본 서버의 Cache-Control 필드가 no-cache/no-store/private로 설정되어 있어도 `www.test.com/abc.jpg` 리소스 노드 캐시 시간은 10일이 됩니다.
- `www.test.com/def.php` 리소스가 노드에 캐시되지 않습니다.



