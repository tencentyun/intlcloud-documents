
## 설정 시나리오

Tencent Cloud CDN의 리소스 캐시는 트리거 형식으로 이루어지는데 사용자가 어떤 리소스에 액세스하기 위해 요청을 보냈을 때, 이 요청이 히트한 CDN 노드에 해당 리소스가 캐시되어 있지 않았다면 사용자의 원본 서버로 돌아가 리소스를 가져옵니다. 리소스를 성공적으로 가져온(2XX 상태 코드) 다음에는 노드에 캐시하고 사용자에게 반환합니다.

CDN 노드에 캐시된 리소스를 직접적으로 관리할 수 없는 상황에서, 원본 서버 리소스에 변동이 있음에도 CDN 노드에서 오래된 리소스를 캐시하여 사용자에게 반환할 우려가 있다면, 노드 캐시 규칙을 설정함으로써 이를 일정 수준 제어할 수 있습니다.

>! 가속 도메인의 서비스 지역이 글로벌 가속일 경우 [캐시 규칙 설정]은 글로벌 범위로 적용되며, 중국 내와 중국 외를 다르게 설정할 수 없습니다.

## 설정 가이드

### 설정 조회

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인한 뒤, 왼쪽 메뉴에서 [Domain Management]를 선택하고 도메인 작업 열의 [Manage]를 클릭하여 도메인 설정 페이지로 이동하면 [캐시 설정] 탭에서 [캐시 규칙 설정]을 확인할 수 있습니다.

가속 도메인 액세스 시,

- 정적 가속 서비스 유형을 선택했을 경우, 일반 동적 파일(예: php, jsp, asp, aspx)의 캐시 시간 기본값은 0초(캐시하지 않음)이며, 다른 모든 파일 유형의 기본 캐시 시간은 30일입니다.
- 다운로드 가속, 스트리밍 미디어 VOD 가속 서비스 유형을 선택했을 경우, 모든 파일의 캐시 만료 시간 기본값은 30일입니다.

![](https://main.qcloudimg.com/raw/43e457600f1d0036c23dff9d091da34d.png)

### 신규 규칙

필요에 따라 캐시 규칙을 추가할 수 있습니다. 규칙은 기본 모드와 고급 모드로 나뉘며, 기본 모드로 기본 설정되어 있습니다.

>! 고급 모드 설정을 제출하면 전면적으로 업그레이드되며, 기본 모드로 다시 복구할 수 없습니다.

### 기본 모드

CDN 노드에 캐시된 모든 리소스에는 '만료 시간'이라는 개념이 있습니다. 요청한 캐시 리소스가 이미 만료되었을 경우, 노드에 캐시되어 있더라도 유효하지 않은 것으로 간주하고 다시 Origin-pull하여 가져오게 됩니다. 기본 모드에서는 특정 파일 유형의 노드 캐시 시간을 설정할 수 있습니다.
![](https://main.qcloudimg.com/raw/b9be3726c932508d5705a773816cea26.png)


#### 플랫폼 정책

사용자로부터 특정 서비스의 리소스를 요청받았을 때, 원본 서버와 상응하는 HTTP Response Header에 Cache-Control 필드가 존재할 경우 기본 플랫폼 정책은 다음과 같습니다.

- Cache-Control 필드가 max-age인 경우, 해당 리소스의 캐시 시간은 설정된 노드 캐시 만료 시간을 기준으로 하며 Max-age로 지정된 시간을 따르지 않습니다.
- Cache-Control 필드가 no-Cache, no-store 혹은 private인 경우, CDN 노드에서 해당 리소스를 캐시하지 않습니다.
- Cache-Control 필드가 없는 경우, 요청이 CDN 캐시에 히트할 때 CDN은 'Cache-Control:max-age = 600' 헤더를 추가하도록 기본 설정되어 있습니다.

#### 고급 캐시 만료 설정

고급 캐시 만료 설정을 활성화하면 원본 서버의 HTTP Response Header Cache-Control에서 Max-Age 값을 조정하여 노드의 캐시 시간을 동적으로 조정할 수 있습니다.

활성화한 후에는, CDN이 이미 설정한 노드 캐시 시간과 Max-Age 값을 대조하여 더 작은 쪽을 실제 노드 캐시 시간으로 적용합니다.

- 사용자의 원본 서버에서 `/index.html`의 Max-Age는 200초로 설정되어 있고, CDN에 설정된 캐시 시간은 600초라면, 노드 내 파일의 실제 만료 시간은 200초가 됩니다.
- 사용자의 원본 서버에서 `/index.html`의 Max-Age는 800초로 설정되어 있고, CDN에 설정된 캐시 시간은 600초라면, 노드 내 파일의 실제 만료 시간은 600초가 됩니다.

> ! 고급 캐시 만료 설정을 활성화할 때 원본 서버에서 Last-Modified 필드를 반환하지 않는다면, CDN은 Last-Modified 필드를 추가하고 10분마다 변경하도록 기본 설정되어 있습니다.

### 고급 모드

고급 모드에서는 특정 파일 유형에 대해 더 다양한 노드 캐시 작업을 설정할 수 있습니다.

- 원본 서버 따르기: 원본 서버의 Cache-Control 헤더를 따릅니다.
- 캐시: 리소스의 노드 캐시 시간을 설정합니다. 강제 캐시 여부, 즉 원본 서버의 Cache-Control: no-store/no-cache/private를 무시할지의 여부도 설정할 수 있습니다.
- 캐시하지 않음: Origin-pull하여 리소스를 획득합니다.

![](https://main.qcloudimg.com/raw/b9be3726c932508d5705a773816cea26.png)


#### 설정 제한

- 단일 도메인에는 최대 20개의 캐시 규칙을 추가할 수 있습니다.
- 여러 규칙 간의 우선순위를 변경할 수 있으며 아래쪽의 우선순위가 위쪽보다 높습니다.
- 파일 유형/폴더/전체 경로 파일은 최대 100그룹까지 입력할 수 있습니다.
- 기본 모드&고급 모드: 캐시 시간은 365일을 초과할 수 없습니다.
- 고급 모드: 캐시 행위를 "캐시"으로 선택했을 때, 강제 캐시 여부를 "네"로 설정하면 CDN은 설정된 캐시 규칙에 따라 캐시을 진행합니다. 강제 캐시 여부를 "아니요"로 설정하면 원본 서버가 Cache-Control: no-store/no-cache/private일 때 CDN은 리소스를 노드로 캐시하지 않고, Origin-pull하여 리소스를 획득합니다.

### 규칙 수정

이미 추가한 캐시 규칙을 수정할 수 있는데, 캐시 키 규칙 작업 열의 [수정]을 클릭하면 됩니다.

### 규칙 삭제

이미 추가한 캐시 규칙을 삭제할 수 있는데, 캐시 규칙 작업 열의 [삭제]를 클릭하면 됩니다.





## 설정 예시

가속 도메인 `www.test.com`의 [캐시 규칙 설정]이 아래와 같을 경우,

![](https://main.qcloudimg.com/raw/36a6bfe2001e73c0a8a24e669c1b3a52.png)

실제 캐시 상황은 다음과 같습니다.

- `www.test.com/abc.jpg` 리소스의 노드 캐시 시간은 10일입니다.
- `www.test.com/def.php` 리소스는 노드로 캐시되지 않습니다.



