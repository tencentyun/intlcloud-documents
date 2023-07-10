## 기본 개념

정적 웹 사이트는 정적 콘텐츠(예: HTML) 또는 클라이언트 스크립트를 포함하는 웹 사이트입니다. 콘솔을 통해 사용자 지정 도메인 이름이 있는 버킷에 대한 정적 웹 사이트를 구성할 수 있습니다. 동적 웹 사이트에는 PHP, JSP 또는 ASP.NET과 같은 서버 스크립트가 포함되어 있으며 서버에서 처리되어야 합니다. Tencent Cloud COS(Cloud Object Storage)에서 정적 웹사이트를 호스팅할 수 있지만 서버 스크립트를 작성할 수는 없습니다. 동적 웹 사이트 배포의 경우 서버 코드 배포용 CVM(Cloud Virtual Machine)을 사용하는 것이 좋습니다.

## 예시

사용자가 examplebucket-1250000000라는 이름의 버킷을 생성하여 다음과 같은 파일을 업로드하였습니다. 

```shell
index.html
404.html
403.html
test.html
docs/a.html
images/
```

### 정적 웹 사이트

**활성화 전**: 다음 기본 액세스 도메인으로 버킷에 액세스하여 다운로드 알림을 팝업하면 `index.html` 파일을 로컬에 저장할 수 있습니다.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/index.html
```

**활성화 후**: 다음 액세스 노드로 버킷에 액세스하면 브라우저에서 `index.html`의 페이지 콘텐츠를 조회할 수 있습니다.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/index.html
```

### 강제 HTTPS

**활성화 전**: HTTP로부터 요청이 온 경우 노드 URL에 액세스하여 HTTP의 암호화가 되지 않은 전송 프로토콜을 유지합니다.

```shell
http://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
```

**활성화 후**: HTTP나 HTTPS로부터 요청이 온 경우 노드에 액세스하여 HTTPS의 암호화 된 전송 프로토콜을 계속 유지합니다.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
```

### 인덱스 문서

정적 웹 사이트의 첫 페이지인 인덱스 문서는 사용자가 웹 페이지의 루트 디렉터리 혹은 서브 디렉터리에 요청을 보낼 때 반환되는 웹 페이지로 `index.html`로 불립니다.
사용자가 버킷 액세스 도메인(예시로 `https://examplebucketbucket-1250000000.cos-website.ap-guangzhou.myqcloud.com`)으로 정적 웹 사이트에 액세스할 경우 특정 웹 페이지가 요청되지 않으며 웹 서버는 첫 화면을 반환합니다.

사용자가 버킷의 임의 디렉터리(루트 디렉터리를 포함)에 액세스하고 URL 주소가 `/`로 끝나면 자동으로 그 디렉터리 인덱스 문서가 먼저 매칭됩니다. URL의 `/`은 선택 사항이며 아래 URL 모두 인덱스 문서를 반환합니다.

```shell
http://www.examplebucket.com/
http://www.examplebucket.com
```

> !버킷에 폴더가 생성되면 폴더의 각 레벨에 인덱스 파일을 추가해야 합니다.

### 오류 문서

오류 문서를 설정하기 전이라고 가정한 후 아래 페이지에 액세스하면 404 상태 코드가 반환되며 페이지에 기본 오류 페이지 정보가 보입니다.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/webpage.html
```

오류 문서를 설정한 후 아래 페이지에 액세스하면 똑같이 404 상태 코드가 반환되지만 페이지에 특정 오류 페이지 정보가 보입니다.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/webpage.html
```

### 리디렉션 규칙

>?호스팅된 정적 웹 사이트에 대한 리디렉션 규칙을 구성하려면 대체 파일의 경로가 버킷의 객체 경로여야 합니다.

#### 에러 코드 리디렉션 설정하기

webpage.html 문서로 **개인 읽기/쓰기** 공개 액세스 권한을 설정하고 사용자가 이 문서에 액세스할 경우 403 오류가 반환됩니다.
403 에러 코드가 403.html에 리디렉션되면 브라우저는 403.html 콘텐츠를 반환합니다.
403.html 문서를 설정하지 않으면 브라우저는 오류 문서 혹은 기본 오류 정보를 반환합니다.
![](https://main.qcloudimg.com/raw/f728aec922e088f45889349f31bcdc08.png)

#### 접두사 매칭 설정

>!접두사 매칭은 와일드카드를 지원하지 않습니다. 접두사가 index1/ 및 index2/인 두 폴더를 리디렉션하려면 `index*/`를 매칭 규칙으로 사용할 수 없으며 각각 해당하는 매칭 규칙을 생성해야 합니다.

1. 폴더 이름을 `docs/`에서 `documents/`로 변경한 후 사용자가 `docs/`폴더에 액세스하면 오류가 발생하므로 접두사 `docs/` 요청을 ` documents/`에 리디렉션 하십시오.
![](https://main.qcloudimg.com/raw/9e8bbe91d902b46146c207a61e092e1d.png)
2. `images/` 폴더를 삭제하면(즉 접두사 `images/`를 가진 모든 객체를 삭제), 리디렉션 규칙을 추가하여 접두사 `images/`를 가진 임의의 객체 요청을 `test.html` 페이지에 리디렉션할 수 있습니다.
![](https://main.qcloudimg.com/raw/ceb0d796e1330c1b203578a1472532e6.png)

