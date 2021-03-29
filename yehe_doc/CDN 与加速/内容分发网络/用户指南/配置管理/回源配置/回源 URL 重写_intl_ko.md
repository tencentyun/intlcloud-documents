## 설정 시나리오

원본 요청 URL을 원본 서버와 매칭되는 URL로 변경해야 하는 경우, Tencent Cloud CDN은 Origin-pull URL 재작성 설정 기능을 지원합니다.



## 설정 가이드

### 설정 조회

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인한 후, 왼쪽 메뉴바에서 [Domain Management]를 선택한 뒤 도메인 작업 열의 [Manage]를 클릭하여 도메인 설정 페이지로 들어갑니다. Tab을 [Origin Configuration]으로 전환하면 [Origin URL Rewrite Configuration]을 찾을 수 있습니다.
![](https://main.qcloudimg.com/raw/e6721b8c8d3ebcb9b5a27fb36e6c6782.png)



### 규칙 추가

필요에 따라 [규칙 추가]를 클릭하여 재작성 규칙을 추가할 수 있습니다.
![](https://main.qcloudimg.com/raw/5f7d6907976fb0696f633af29321c99c.jpg)


**설정 제한**

- 도메인당 최대 100개의 재작성 규칙을 추가할 수 있습니다.
- 다수 규칙에 우선순위 변경 지원: 하위 우선순위가 상위 우선순위보다 높습니다.
- 재작성할 Origin-pull URL: `/`로 시작하며, 전체 경로 매칭(예: /test/a.jpg)과 와일드카드 부호 `*` 매칭(예: /test/\*/\*.jpg)을 지원합니다. 파일 디렉터리를 지정하는 경우에는 “/”가 마지막에 올 수 없습니다(예: /test).
- 타깃 호스트 헤더: 기본적으로 현재 도메인이 설정되어 있으며 수정할 수 있고, `http://` 또는 `https://` 헤더가 포함되지 않습니다.
- 타깃 Origin-pull Path: `/`로 시작하며(예: /newtest/b.jpg) 와일드카드 부호 `*`는 `$n`으로 캐치(n=1,2,3..., 예: /newtest/$1/$2.jpg)할 수 있습니다. 파일 디렉터리를 지정하는 경우에는 “/”가 마지막에 올 수 없습니다(예: /test).
- 와일드카드 부호 `*`는 최대 5개까지 입력할 수 있으며, 캐치 위치 고정 부호 `$n`은 최대 10개까지 입력할 수 있습니다.
- 중국어 콘텐츠 제출을 지원하지 않으며 타깃 호스트 헤더는 250자를 초과할 수 없습니다. 기타 입력창 콘텐츠는 최대 1024자까지 입력할 수 있습니다.



## 설정 예시:

가속 도메인이 `www.test.com`인 경우 **Origin-pull URL 재작성 설정**을 다음과 같이 설정합니다.
![](https://main.qcloudimg.com/raw/4797e184e62c1abd5ed3cf1d1091f3fb.png)

실제 Origin-pull 상황은 다음과 같습니다.

- `www.test.com/test/` 원본 요청 시, 실제로는 `www.test.com/newtest/` 원본 요청
- `www.test.com/test/a.jpg` 원본 요청 시, 실제로는 `www.newtest.com/newtest/a.jpg` 콘텐츠 원본 요청
