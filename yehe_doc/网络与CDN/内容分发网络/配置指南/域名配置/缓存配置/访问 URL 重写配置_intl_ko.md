## 설정 시나리오

실제 액세스 URL을 원본 서버와 매칭되는 URL로 변경해야 하는 경우, Tencent Cloud CDN은 액세스 URL 재작성 설정 기능을 지원합니다.

사용자 정의 액세스 URL 재작성 설정을 통해 URL 302를 타깃 URL로 리디렉션할 수 있습니다.

## 설정 가이드

### 설정 조회

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인한 후, 왼쪽 메뉴바에서 [Domain Management]를 선택한 뒤 도메인 작업 열의 [Manage]를 클릭하여 도메인 설정 페이지로 들어갑니다. Tab을 [Cache Configuration]으로 전환하면 [Access URL Rewrite Configuration]을 찾을 수 있습니다.

기본적으로 액세스 URL 재작성 설정은 비활성화되어 있습니다.
![](https://main.qcloudimg.com/raw/01f93aaa70c523ae0bb1ab5debae8558.png)


### 규칙 추가

필요에 따라 [Add Rewrite Rule]을 클릭하여 재작성 규칙을 추가할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/97ea8713395f3af8654c39be97f124d3.png"  style="height:300px"></img>

**설정 제한**
+ 도메인당 최대 100개의 재작성 규칙을 추가할 수 있습니다.
+ 다수 규칙에 우선순위 변경 지원: 하위 우선순위가 상위 우선순위보다 높습니다.
+ 재작성할 URL: /로 시작하며, 전체 경로 매칭(예: /test/a.jpg)과 와일드카드 부호 `*` 매칭(예: /test/\*/\*.jpg)을 지원합니다. 파일 디렉터리를 지정하는 경우에는 “/”가 마지막에 올 수 없습니다(예: /test).
+ 타깃 Host: 기본적으로 현재 도메인(기본적으로 http 헤더 존재)으로 설정되어 있으며, 다른 도메인으로 수정할 수 있습니다. 반드시 `http://` 또는 `https://` 헤더가 포함되어야 합니다.
+ 타깃 Path: /로 시작하며(예: /newtest/b.jpg) 와일드카드 부호 `*`는 `$n`으로 캐치(n=1,2,3..., 예: /newtest/$1/$2.jpg)할 수 있습니다. 파일 디렉터리를 지정하는 경우에는 “/”가 마지막에 올 수 없습니다(예: /test).
+와일드카드 부호 `*`는 최대 5개까지 입력할 수 있으며, 캐치 위치 고정 부호 `$n`은 최대 10개까지 입력할 수 있습니다.
+ 중국어 콘텐츠 제출을 지원하지 않으며, 입력창 콘텐츠 길이는 최대 1024자까지 입력할 수 있습니다.




## 설정 예시

가속 도메인이 `www.test.com`인 경우 **액세스 URL 재작성 설정**을 다음과 같이 설정합니다.
![](https://main.qcloudimg.com/raw/214b034e578d5eaac0a63cacd49f1e2d.png)

실제 액세스 상황은 다음과 같습니다.

+ 클라이언트에서 `www.test.com/test/a.jpg` 요청 시, CDN 노드가 `www.test.com/newtest/b.jpg` 콘텐츠 반환
+ 클라이언트에서 `www.test.com/test/a.png` 요청 시, CDN 노드가 `www.newtest.com/newtest/a.png` 콘텐츠 반환



