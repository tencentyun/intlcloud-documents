## 설정 시나리오

Tencent Cloud CDN은 User-Agent 블랙리스트/화이트리스트 규칙 설정을 통한 액세스 제어를 지원합니다.
사용자의 HTTP 요청 헤더에 있는 User-Agent에 대한 규칙을 판단하여, 필요에 따라 사용자 액세스를 통과 허가 또는 거부합니다.

## 설정 가이드

### 설정 제한

- 블랙리스트 전체 설정 또는 화이트리스트 전체 설정만 지원하며, 블랙리스트/화이트리스트 동시 설정 규칙은 지원하지 않습니다.
- 블랙리스트 또는 화이트리스트 규칙을 최대 10개까지 설정할 수 있습니다.
- 규칙에서 와일드카드 `*`를 지원하며, 값이 여러 개인 경우 `|`로 구분합니다.
- 적용 유형은 모든 파일, 파일 유형, 파일 디렉터리, 지정 파일 경로의 4가지 모드를 지원하며, 정규식 매칭은 지원하지 않습니다.

### 설정 설명

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴바에서 [Domain Management]를 선택하고, 도메인 오른쪽의 [Manage]를 클릭하면 도메인 설정 페이지로 이동합니다. 두 번째 탭인 [Access Control]에 UA 블랙리스트/화이트리스트 설정이 존재하며 기본값은 비활성화 상태입니다.
![](https://main.qcloudimg.com/raw/07914bd30b3d422fb4bddf3a323d92f2.png)
비활성화 상태에서 [Add Rule]을 클릭하여 필요에 따라 블랙리스트/화이트리스트를 하나씩 추가할 수 있습니다.
![](https://main.qcloudimg.com/raw/66d3fc72f575efaa4ae42382d8fde179.png)

>!
>1. 와일드카드 `*`만 지원하며 기타 정규식은 지원하지 않습니다.
>2. `*`가 없는 경우 기타 문자는 모두 완전히 매칭됩니다.
 
규칙 추가가 완료되면 전체 설정이 비활성화 상태로 되어, 현재 네트워크 서비스에 영향을 미치지 않습니다.
![](https://main.qcloudimg.com/raw/679129885ec36329178e87af671d6743.png)
[ON] 버튼을 클릭해 설정한 블랙리스트/화이트리스트를 현재 네트워크에 배포할 수 있습니다.
![](https://main.qcloudimg.com/raw/fd85de8e702b24e7d2eaaf8b34667c95.png)

## 설정 예시

가속 도메인이 `cloud.tencent.com`인 UA 블랙리스트/화이트리스트 설정은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/c7e06060bc627aab2e4939b53460951d.png)
HTTP Request Header에서 User-Agent는 다음과 같습니다.

```
user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.61 Safari/537.36
```

블랙리스트에 부합하면 403을 반환합니다.

