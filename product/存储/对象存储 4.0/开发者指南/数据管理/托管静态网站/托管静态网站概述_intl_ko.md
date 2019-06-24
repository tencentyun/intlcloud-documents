## 기본 개념

정적 웹사이트란 정적 내용(예: HTML)이나 클라이언트 스크립트를 포함하는 웹사이트입니다. 사용자는 콘솔을 통해 바인딩된 사용자 지정 도메인 이름의 버킷에 대해 정적 웹사이트를 구성합니다. 이 반면에 동적 웹사이트의 내용은 PHP, JSP 또는 ASP.NET 등과 같은 서버 측 스크립트를 포함하여 서버에 의해 처리해야 합니다. Tencent Cloud COS는 정적 웹사이트의 호스팅을 지원하는데 서버 측 스크립트의 프로그래밍을 지원하지 않습니다. 동적 웹사이트를 배포하고자 할 경우, CVM을 사용하여 서버 코드의 배포를 진행할 것을 권장합니다.

## 예시

사용자가 examplebucket-1250000000이라는 버킷을 생성하여 아래와 같은 파일을 업로드하였습니다. 

```shell
index.html
404.html
403.html
test.html
docs/a.html
images/
```

### 정적 웹사이트

**오픈 전**: 아래와 같은 기본 접근 도메인 이름으로 버킷을 접근하면 다운로드 알림이 팝업되어 `index.html` 파일을 로컬에 저장할 수 있습니다.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/index.html
```

**오픈 후**: 아래와 같은 접근 노드로 버킷에 접근하면 브라우저에서 직접 `index.html`의 페이지 내용을 확인할 수 있습니다.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/index.html
```

### 강제 HTTPS

**오픈 전**: 요청 출처가 HTTP일 경우, 접근 노드 URL은 HTTP로 암호화되지 않는 전송 프로토콜을 유지합니다.

```shell
http://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
```

**오픈 후**: 요청 출처가 HTTP이나 HTTPS일 경우, 접근 노드는 HTTPS로 암호화된 전송 프로토콜을 유지합니다.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
```

### 인덱스 문서

인덱스 문서는 정적 웹사이트의 홈페이지로서, 사용자가 웹사이트의 루트 디렉터리 또는 모든 서브 디렉터리에 요청을 발송할 때 반환하는 웹사이트이며, 일반적으로 이 페이지는 `index.html`로 명명됩니다.
사용자가 버킷 접근 도메인 이름(예: `https://examplebucketbucket-1250000000.cos-website.ap-guangzhou.myqcloud.com`)으로 정적 웹사이트에 접근하고 특정 페이지를 요청하지 않았을 경우 Web 서버는 홈페이지로 돌아갑니다.

사용자 접근 버킷은 루트 디렉터리를 포함한 모든 디렉터리를 포함하고 URL 주소는 `/`로 끝날 경우, 우선적으로 해당 디렉터리의 인덱스 문서를 자동으로 매칭합니다. 루트 주순 URL의 `/`는 선택 가능하며 아래에 모든 URL은 인덱스 문서를 반환합니다.

```shell
http://www.examplebucket.com/
http://www.examplebucket.com
```

>! 버킷에 폴더를 생성했을 경우 모든 폴더 수준에 인덱스 문서를 추가해야 합니다.

### 오류 문서

오류 문서를 구성하기 전에 아래 페이지에 접근하면 404 코드를 반환하고 페이지에는 기본 오류 정보가 나타납니다.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/webpage.html
```

오류 문서를 구성한 후에 아래 페이지에 접근하면 404 코드도 반환합니다. 하지만 페이지에는 지정한 오류 정보가 나타납니다.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/webpage.html
```

### 리디렉션 규칙

#### 오류 코드 리디렉션 구성

webpage.html이라는 문서에 **비공개 읽기/쓰기**의 공통 접근 권한을 설정하였다면 사용자가 해당 파일에 접근 시 403 오류를 반환합니다.
403 오류 코드를 403.html로 리디렉션을 구성한 후 브라우저는 403.html의 내용을 반환합니다.
403.html 문서를 구성하지 않았을 경우, 브라우저는 오류 문서 또는 기본 오류 정보를 반환합니다.
![](https://main.qcloudimg.com/raw/7dc917ba95af42438b6ab2c7604666d3.png)

#### 접두사 매칭 구성

1. 폴더를 `docs/`에서 `documents/`로 이름을 변경할 경우, 사용자가 `docs/` 폴더에 접근 시 오류가 발생할 수 있습니다. 그러므로 접두사 `docs/`의 요청을 `documents/`로 리디렉션할 수 있습니다.
![](https://main.qcloudimg.com/raw/e3b5c9004a67d020928bd0035b820715.png)
2. `Images/` 폴더를 삭제했을 경우(즉, 접두사 `images/`를 가진 모든 객체를 삭제했을 경우), 리디렉션 규칙을 추가하여 접두사 `images/`를 가진 모든 객체의 요청을 `test.html` 페이지로 리디렉션할 수 있습니다.
![](https://main.qcloudimg.com/raw/b6672acf43149267a837027911923f9b.png)

