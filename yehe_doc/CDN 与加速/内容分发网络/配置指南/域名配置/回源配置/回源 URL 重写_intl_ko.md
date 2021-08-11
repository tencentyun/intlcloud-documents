## 설정 시나리오

원본 요청 URL을 원본 서버와 매칭되는 URL로 변경해야 하는 경우, Tencent Cloud CDN은 Origin-pull URL 재작성 설정 기능을 지원합니다.

>! ECDN 도메인은 현재 이 기능 설정을 지원하지 않습니다.


## 설정 가이드

### 설정 조회

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인한 뒤 왼쪽 메뉴바에서 [도메인 관리]를 선택하고, 도메인 작업 열의 [관리]를 클릭하면 도메인 설정 페이지로 이동합니다. Tab을 [Origin-pull 설정]으로 전환하면 [Origin-pull URL 재작성 설정]을 찾을 수 있습니다.
![](https://main.qcloudimg.com/raw/e6721b8c8d3ebcb9b5a27fb36e6c6782.png)



### 규칙 추가

필요에 따라 [규칙 추가]를 클릭하여 재작성 규칙을 추가할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/5f7d6907976fb0696f633af29321c99c.jpg" style="height:300px"/>


**설정 제약**

- 도메인당 최대 100개의 재작성 규칙을 추가할 수 있습니다.
- 다수의 규칙에 대한 우선 순위 변경 지원: 하단 우선순위가 상단 우선순위보다 높습니다.
- 재작성할 Origin-pull URL： `/`로 시작하고，기본적으로 접두사와 매칭되도록 설정되어 있으며 전체 경로 매칭(예:/test/a.jpg)과 와일드카드 부호 `*` 매칭(예: /test/\*/\*.jpg)을 지원합니다. 파일 디렉터리를 지정하는 경우, “/”로 끝날 수 없습니다(예:/test).
- 타깃 Origin-pull Host: 기본적으로 현재 도메인이 설정되어 있습니다. 수정이 가능하며 `http://` 또는 `https://` 헤더를 포함하지 않습니다.
- 타깃 Origin-pull path: `/`로 시작하고(예: /newtest/b.jpg），와일드카드 부호 `*` 는 `$n`을 통해 캡처 가능하며（n=1,2,3...，예: /newtest/$1/$2.jpg).파일 디렉터리를 지정하는 경우 “/”로 끝날 수 없습니다(예: /test).
- 와일드카드 부호 `*`는 최대 5개까지 입력할 수 있으며, 캡처 위치 고정 부호 `$n`은 최대 10개까지 입력할 수 있습니다.
- 중국어 콘텐츠 제출을 지원하지 않으며 타깃 호스트 헤더는 250자를 초과할 수 없습니다. 기타 입력창 콘텐츠는 최대 1024자까지 입력할 수 있습니다.



## 설정 예시:

가속 도메인이 `www.test.com`인 경우 **Origin-pull URL 재작성 설정**은 다음과 같습니다. 
![](https://main.qcloudimg.com/raw/c255f4e4643a15e2e47a29a608a9fd01.png)

위와 같이 설정하면 실제 Origin-pull 상황은 다음과 같습니다.
- `www.test.com/images/1.jpg` 원본 요청 시 규칙 1과 3이 히트되면 하단 우선순위가 가장 높으므로 실제 원본 요청은 `www.test.com/index.html`이 됩니다.
- `www.test.com/images` 원본 요청 시 규칙 1, 2, 3이 히트되면 하단 우선순위가 가장 높으므로 실제 원본 요청은 `www.test.com/index.html`이 됩니다.
