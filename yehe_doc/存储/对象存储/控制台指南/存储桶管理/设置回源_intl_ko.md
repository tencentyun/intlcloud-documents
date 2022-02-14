## 소개

COS(Cloud Object Storage) 콘솔에서 버킷의 Origin-pul 규칙을 설정할 수 있습니다. 요청한 객체가 버킷에 존재하지 않거나 특정 요청을 리디렉션해야 할 때, Origin-pul 규칙을 통해 COS에서 대상 데이터로 액세스할 수 있습니다. Origin-pul 설정은 데이터의 라이브 마이그레이션, 특정 요청 리디렉션 등과 같은 사용 시나리오에 적용되며, 실제 요구사항에 맞춰 설정할 수 있습니다.

>?
>- Origin-pul에 의한 데이터 풀링 성공률은 네트워크 환경과 관련이 있습니다. China Telecom, China Mobile, China Unicom 등의 IP를 우선적으로 사용하십시오.
>

<img src="https://main.qcloudimg.com/raw/f63a74cf70a9f6582e52e13a2b16e72a.png" width="90%">


## 작업 단계

1. [객체 버킷 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭하여 버킷 리스트 페이지로 이동합니다.
3. Origin-pull 설정이 필요한 버킷을 클릭하여 버킷 상세 페이지로 이동합니다.
4. 왼쪽 사이드바에서 **기본 설정 > Origin-pull 설정**을 선택하고 **Origin-pull 규칙 추가**를 클릭합니다.
![](https://main.qcloudimg.com/raw/69fc0f3042e59c3e9c2667d06aa068fa.png)
5. 팝업 창에서 다음 정보를 설정하고 **다음 단계**를 클릭합니다.

 - **Origin-pul 조건**: 요구사항에 따라 Origin-pul를 트리거할 조건을 선택합니다. Origin-pul를 트리거하려면 설정된 Origin-pul의 모든 조건을 동시에 충족해야 합니다.
    - **HTTP 상태 코드 404**: HTTP 상태 코드가 404일 때 Origin-pul를 트리거하는 것이 유일한 조건인 경우, 해당 항목은 필수 항목으로서 취소할 수 없습니다.
    - **파일명 접두사**: 요청한 파일명 접두사가 매칭되면 Origin-pul 규칙을 트리거할 수 있습니다. 예를 들어, 파일명 접두사를 prefix로 설정하여 `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`에 액세스하고 반환된 HTTP 상태 코드가 404이면 Origin-pul 규칙이 트리거됩니다.
 - **Origin-pul 프로토콜**: COS에서 지정한 원본 서버에 액세스할 때 사용하는 HTTP 프로토콜 옵션에는 강제 HTTPS, "강제 HTTP, 요청 프로토콜을 따름이 있습니다.
    - 강제 HTTPS/HTTP를 선택할 경우, COS는 HTTPS/HTTP 프로토콜로 원본 서버에 액세스합니다.
    - 요청 프로토콜을 따름을 선택할 경우, COS는 COS에 요청할 때 사용한 프로토콜로 원본 서버에 액세스합니다.
 - **요청 매개변수**: COS에 액세스할 때 가져오는 queryString 요청 매개변수를 원본 서버로 패스스루 여부.
 - **지정된 요청 헤더 통과**: 여기에 원본 서버로 패스스루할 요청의 헤더 정보를 추가할 수 있습니다.
 - **추가 요청 헤더**: 여기에 원본 사이트 Origin-pull 시 전달되는 요청 헤더를 추가할 수 있습니다.
6. 다음 정보를 설정하고 **다음 단계**를 클릭합니다.

 - **원본 주소**: 도메인이나 IP 주소를 입력하면 도메인이나 IP 주소 뒤에 포트 번호가 추가됩니다. 접두사 `http://` 또는 `https://`를 별도로 입력하지 않아도 됩니다.

정확한 주소의 예시는 다음과 같습니다.
```shell
abc.example.com
abc.example.com:8080
202.96.128.86
202.96.128.86:8080
```

원본 주소의 주소를 설정할 수 있습니다. 다음과 같이 설정 가능합니다:
 - **파일 고정**: Origin-pul 규칙을 트리거할 때 고정된 파일을 전부 기본값으로 리디렉션합니다.
 - **접두사 지정**: Origin-pul 규칙을 트리거할 때 지정한 접두사와 매치되는 파일로 리디렉션합니다. 예를 들어, 지정한 접두사가 `test`이고, `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`에 액세스할 때 Origin-pul 규칙이 트리거되면 `<원본 주소>/test/prefix123.jpg`로 리디렉션됩니다.
 - **확장자명 지정**: Origin-pul 규칙을 트리거할 때 지정한 확장자명과 매치되는 파일로 리디렉션합니다. 예를 들어, 지정한 확장자명이 `.jpg`이고, `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123`에 액세스할 때 Origin-pul 규칙이 트리거되면 `<원본 주소>/prefix123.jpg`로 리디렉션됩니다.

>!
>- 파일 고정을 선택하면 기본적으로 다른 두 개 유형은 선택할 수 없습니다.
>- 접두사와 접미사는 동시에 지정하여 적용할 수 있습니다.

 - **Origin-pull 주소 백업**: 이 기능을 활성화한 후 백업 원본 서버를 추가할 수 있으며 프라이머리 원본 서버가 5xx와 같은 에러 코드를 반환하면 COS는 해당 백업 원본 서버를 요청합니다.

 - **Origin-pul 동기화**: Origin-pul 동기화를 활성화하면 COS에서 원본 서버의 데이터를 풀링할 때 3XX 상태 코드를 반환하지 않습니다. 해당 설정 항목은 현재 베이징, 상하이, 싱가포르, 뭄바이 리전의 버킷에 한해 지원합니다.

 - **3XX 종속 정책**: 이 정책을 활성화하면 원본 서버가 3XX 리디렉션 상태 코드를 반환할 때, COS는 3XX를 종속하여 다른 원본 서버에서 데이터를 풀링하는 정책을 기본으로 적용합니다. **비활성화**를 선택하면 리소스를 풀링하지 않습니다.

7. 설정된 Origin-pull 규칙이 정확한지 확인하고 **확인**을 클릭합니다.
규칙 추가를 완료하면 신규 규칙에 최상위 우선순위가 할당됩니다. COS는 최상위 우선순위의 규칙에 따라 Origin-pul를 실행하며, 규칙 리스트 페이지에서 수정 버튼을 클릭하여 우선순위를 변경할 수 있습니다.
![](https://main.qcloudimg.com/raw/3fa148b2e43f30fb891adee75ff255db.png)


## 예시

**배경**
APPID가 1250000000인 사용자가 이름이 examplebucket-1250000000인 버킷을 생성하고, CDN 가속 액세스 도메인을 활성화한 경우입니다.

```shell
examplebucket-1250000000.file.myqcloud.com
```

다음은 설정한 버킷의 원본 주소입니다.

```shell
abc.example.com
```

원본 서버 `http://abc.example.com`에 이미지 picture.jpg를 저장합니다.

**클라이언트가 서버에 처음 액세스한 경우입니다(Origin-pul 동기화 비활성화)**.

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

COS가 객체에 적중할 수 없음을 인식하면 클라이언트로 302 HTTP 상태 코드가 반환되고, 다음의 주소로 이동합니다.

```shell
http://abc.example.com/picture.jpg
```

**클라이언트가 서버에 처음 액세스한 경우입니다(Origin-pul 동기화 활성화)**.

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

COS가 객체에 적중할 수 없음을 인식하면 클라이언트로 200 HTTP 상태 코드가 반환되고, 다음의 주소로 이동합니다.

```shell
http://abc.example.com/picture.jpg
```

이때 액세스를 보장하기 위해 원본 서버에서 클라이언트로 객체를 제공합니다. 또한 COS는 원본 서버에서 picture.jpg를 복사하여 버킷 example의 루트 디렉터리에 저장합니다.

**2차 액세스**

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

COS가 루트 디렉터리에 저장된 picture.jpg 객체에 직접 적중하여 클라이언트에 반환합니다.
