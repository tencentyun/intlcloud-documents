## 소개

COS(Cloud Object Storage) 콘솔에서 버킷에 대한 Origin-pull 규칙을 구성할 수 있습니다. 요청한 객체가 버킷에 없거나 특정 요청을 리디렉션해야 하는 경우 COS를 통해 해당 데이터에 액세스하도록 Origin-pull 규칙을 구성할 수 있습니다. Origin-pull 구성은 주로 핫 데이터 마이그레이션, 특정 요청 리디렉션 및 기타 관련 시나리오에 사용됩니다.

>?
>- Origin-pul에 의한 데이터 풀링 성공률은 네트워크 환경과 관련이 있습니다. China Telecom, China Mobile, China Unicom 등의 IP를 우선적으로 사용하십시오.
>

<img src="https://main.qcloudimg.com/raw/f63a74cf70a9f6582e52e13a2b16e72a.png" width="90%">

## Origin-pull 규칙

### 트리거 조건

- 비동기 및 동기화 origin-pull 모드에서 origin-pull은 요청이 404 오류를 반환하는 경우에만 트리거됩니다.
- 리디렉션 모드에서 400~599 사이의 HTTP 상태 코드를 사용자 지정하여 origin-pull을 트리거할 수 있습니다.

### 원본 액세스

- 비동기화 및 동기화 origin-pull 모드에서 COS 액세스 요청의 QueryString 및 Header 정보를 원본에 전달할지 여부를 설정하고, 원본 요청 시 추가 Header 정보를 전달하도록 구성할 수 있습니다. 리디렉션 모드에서는 QueryString 통과 여부만 설정할 수 있습니다.
- GET 연산 중에 GET range가 지정되면 COS는 완전한 객체 데이터를 가져와 COS에 저장하기 위해 원래 요청 외에 range가 없는 비동기 요청을 보냅니다.

### 응답 및 저장

- 원본은 chunked 인코딩으로 데이터를 반환할 수 있습니다.
- 원본이 404 상태 코드를 반환하면 COS로 전달되어 사용자에게 반환됩니다. **3XX 팔로우 정책**이 활성화된 경우 원본이 3XX 상태 코드를 반환하면 COS는 다른 원본에서 데이터를 가져옵니다. 원본이 3XX가 아닌 다른 상태 코드를 반환하면 COS는 424 상태 코드를 반환합니다.
- origin-pull에 의해 반환된 파일은 원본 요청 시 사용한 파일명으로 COS에 저장됩니다. 예를 들어 사용자가 요청한 example.jpg 파일이 버킷에 존재하지 않는 경우, COS는 구성된 origin-pull 주소 `http://origin.com/example.jpg`에서 파일을 풀링하고 example.jpg 버킷에 저장된 파일의 이름을 바꾸는 origin-pull 메커니즘을 트리거합니다.
- COS에 저장된 새 객체에는 다음 메타데이터가 포함되며 데이터 콘텐츠는 원본 값을 따릅니다.
```shell
cache-control
content-disposition
content-encoding
content-type
expires
x-cos-meta-*
```


## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭합니다.
3. Origin-pull 설정이 필요한 버킷을 클릭하여 버킷 상세 페이지로 이동합니다.
4. 왼쪽 사이드바에서 **기본 설정 > Origin-pull 설정**을 선택하고 **Origin-pull 규칙 추가**를 클릭합니다.
![](https://main.qcloudimg.com/raw/69fc0f3042e59c3e9c2667d06aa068fa.png)
5. 팝업 창에서 다음 정보를 설정하고 **다음 단계**를 클릭합니다.

 - **Origin-pull 모드**: Origin-pull 모드는 실제 필요에 따라 선택할 수 있습니다.
    - **Origin-pull 비동기화**: 요청된 파일이 COS에 없으면 COS는 지정된 원본에서 파일을 찾아 클라이언트로 반환하지 않고 버킷에 업로드합니다.
    >?비동기식 Origin-pull은 파일을 직접 반환하지 않습니다. 대신 먼저 클라이언트에 302 상태 코드를 반환한 다음 파일을 COS에 비동기식으로 업로드합니다.
    >1. 원본에서 데이터를 가져오려면 Follow 302를 활성화하는 것이 좋습니다.
    >2. 파일 업로드 시간은 여러 요인에 따라 달라지며 SLA는 약속할 수 없습니다. **비즈니스가 지연에 민감한 경우 Origin-pull 동기화를 선택하는 것이 좋습니다**.
    - **Origin-pull 동기화**: 요청한 파일이 COS에 없는 경우, COS는 지정된 원본에서 파일을 검색하여 클라이언트에 반환하고 버킷에 업로드합니다.
    - **리디렉션**: 버킷에 액세스할 때 지정된 오류가 보고되면 COS는 클라이언트에 리디렉션 주소를 반환하지만 원본에서 파일을 저장하지 않습니다. 클라이언트는 리디렉션 주소의 원본에서 리소스를 요청할 수 있습니다.
 - **Origin-pul 조건**: Origin-Pull을 트리거하기 위해 동시에 충족되어야 하는 모든 조건을 지정합니다.
    - **HTTP 상태 코드 404**: 비동기화 Origin-pull 또는 동기화 Origin-pull을 선택하는 경우 이 매개변수는 필수이며 취소할 수 없으며 HTTP가 연결될 때 origin-pull이 트리거됩니다. 상태 코드는 404입니다. 리디렉션을 선택하면 400~599 범위의 HTTP 상태 코드를 입력할 수 있습니다.
    - **파일명 접두사**: 요청된 파일이 접두사와 일치하면 origin-pull 규칙이 트리거됩니다. 예를 들어 이 옵션을 prefix로 설정하면 `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`에 액세스하고 반환된 HTTP 상태 코드가 404일 때 origin-pull 규칙이 트리거됩니다.
 - **Origin-pul 프로토콜**: COS가 지정된 원본에 액세스하는 데 사용하는 프로토콜입니다. 옵션에는 Force HTTPS, Force HTTP 및 Follow 요청 프로토콜이 포함됩니다.
    - Force HTTPS 또는 Force HTTP를 선택할 경우, COS는 각각 HTTPS 또는 HTTP를 사용하여 원본에 액세스합니다.
    - Follow 요청 프로토콜을 선택할 경우, COS는 요청에 사용된 프로토콜로 원본에 액세스합니다.
 - **요청 매개변수**: COS에 액세스할 때 가지고 다니는 queryString 요청 매개변수를 원본으로 전달할지 여부를 지정합니다.
 - **패스스루는 요청 헤더를 지정함**: 원본으로 전달하려는 요청 헤더를 지정합니다. Origin-pull 모드로 리디렉션을 선택한 경우 이 매개 변수를 설정하지 마십시오.
 - **새 요청 헤더**: COS가 원본에 액세스할 때 전달할 추가 요청 헤더를 추가합니다. 이 항목은 리디렉션 Origin-pull 유형이 선택된 경우 설정되지 않습니다.
6. 선택한 Origin-pull 모드에 따라 다음 정보를 구성하도록 선택하고 **다음 단계**를 클릭합니다.

<dx-tabs>
::: Origin-pull 비동기화

 - **Origin-pull 주소**: `http://` 또는 `https://` 접두사 없이 도메인 이름 또는 IP 주소를 입력합니다. 도메인 이름이나 IP 주소 뒤에 포트 번호를 추가할 수도 있습니다.
정확한 주소의 예시는 다음과 같습니다.

```shell
abc.example.com
abc.example.com:8080
202.96.128.86
202.96.128.86:8080
```

 - **대기 포워딩 주소**: 아래와 같이 구성된 도메인 이름 또는 IP 주소를 입력할 수 있습니다.
    - **고정 파일**: origin-pull 규칙이 트리거될 때 모든 요청이 리디렉션되는 고정 파일을 지정합니다.
    - **지정된 접두사**: Origin-pul 규칙이 트리거될 때 요청이 리디렉션되는 파일의 접두사를 지정합니다. 예를 들어, 접두사가 `test`로 지정된 경우 `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`에 액세스하면 요청이 `<Origin-pull 주소>/test/prefix123.jpg`로 리디렉션되고 origin-pull 규칙이 트리거됩니다.
    - **지정된 접미사**: Origin-pul 규칙을 트리거될 때 요청이 리디렉션되는 파일의 접미사를 지정합니다. 예를 들어, 접미사가 `.jpg`로 지정된 경우, `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123`에 액세스하면 요청이 `<Origin-pull 주소>/prefix123.jpg`로 리디렉션되고 origin-pull 규칙이 트리거됩니다.

<b>Note:</b>
         - 고정 파일을 선택하면 다른 필드를 사용할 수 없습니다.
         - 지정된 접두사와 지정된 접미사를 동시에 사용할 수 있습니다.

 - **3XX 종속 정책**: 이 정책이 활성화된 경우 원본이 3xx 리디렉션을 반환하면 COS가 이를 따라 다른 원본에서 데이터를 가져옵니다. **비활성화**를 선택하면 리소스를 풀링하지 않습니다.
:::
::: Origin-pull 동기화

 - **Origin-pull 주소**: `http://` 또는 `https://` 접두사 없이 도메인 이름 또는 IP 주소를 입력합니다. 도메인 이름이나 IP 주소 뒤에 포트 번호를 추가할 수도 있습니다.
정확한 주소의 예시는 다음과 같습니다.

```shell
abc.example.com
abc.example.com:8080
202.96.128.86
202.96.128.86:8080
```

 - **대기 포워딩 주소**: 아래와 같이 구성된 도메인 이름 또는 IP 주소를 입력할 수 있습니다.
    - **고정 파일**: origin-pull 규칙이 트리거될 때 모든 요청이 리디렉션되는 고정 파일을 지정합니다.
    - **지정된 접두사**: Origin-pul 규칙이 트리거될 때 요청이 리디렉션되는 파일의 접두사를 지정합니다. 예를 들어, 접두사가 `test`로 지정된 경우 `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`에 액세스하면 요청이 `<Origin-pull 주소>/test/prefix123.jpg`로 리디렉션되고 origin-pull 규칙이 트리거됩니다.
    - **지정된 접미사**: Origin-pul 규칙을 트리거될 때 요청이 리디렉션되는 파일의 접미사를 지정합니다. 예를 들어, 접미사가 `.jpg`로 지정된 경우, `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123`에 액세스하면 요청이 `<Origin-pull 주소>/prefix123.jpg`로 리디렉션되고 origin-pull 규칙이 트리거됩니다.

<b>Note:</b>
         - 고정 파일을 선택하면 다른 필드를 사용할 수 없습니다.
         - 지정된 접두사와 지정된 접미사를 동시에 사용할 수 있습니다.

 - **3XX 종속 정책**: 이 정책이 활성화된 경우 원본이 3xx 리디렉션을 반환하면 COS가 이를 따라 다른 원본에서 데이터를 가져옵니다. **비활성화**를 선택하면 리소스를 풀링하지 않습니다.
 - **원본 사이트의 패킷**: 이 기능이 활성화되면 상태 코드 및 기타 정보를 포함하여 원본의 패킷이 직접 반환됩니다.
:::
::: 리디렉션

 - **Origin-pull 주소**: `http://` 또는 `https://` 접두사 없이 도메인 이름 또는 IP 주소를 입력합니다. 도메인 이름이나 IP 주소 뒤에 포트 번호를 추가할 수도 있습니다.
정확한 주소의 예시는 다음과 같습니다.

```shell
abc.example.com
abc.example.com:8080
202.96.128.86
202.96.128.86:8080
```

 - **대기 포워딩 주소**: 아래와 같이 구성된 도메인 이름 또는 IP 주소를 입력할 수 있습니다.
    - **고정 파일**: origin-pull 규칙이 트리거될 때 모든 요청이 리디렉션되는 고정 파일을 지정합니다.
    - **지정된 접두사**: Origin-pul 규칙이 트리거될 때 요청이 리디렉션되는 파일의 접두사를 지정합니다. 예를 들어, 접두사가 `test`로 지정된 경우 `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`에 액세스하면 요청이 `<Origin-pull 주소>/test/prefix123.jpg`로 리디렉션되고 origin-pull 규칙이 트리거됩니다.
    - **지정된 접미사**: Origin-pul 규칙을 트리거될 때 요청이 리디렉션되는 파일의 접미사를 지정합니다. 예를 들어, 접미사가 `.jpg`로 지정된 경우, `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123`에 액세스하면 요청이 `<Origin-pull 주소>/prefix123.jpg`로 리디렉션되고 origin-pull 규칙이 트리거됩니다.

<b>Note:</b>
         - 고정 파일을 선택하면 다른 필드를 사용할 수 없습니다.
         - 지정된 접두사와 지정된 접미사를 동시에 사용할 수 있습니다.

 - **리디렉션 Code**: 301, 302, 307을 선택할 수 있으며, 기본값은 301입니다.
:::
</dx-tabs>

7. 설정된 Origin-pull 규칙이 정확한지 확인하고 **확인**을 클릭합니다.
기본적으로 COS는 origin-pull을 수행하는 가장 최근 규칙에 항상 가장 높은 우선 순위를 부여합니다. 우선 순위를 수동으로 변경하려면 규칙 목록의 우선 순위 열에서 편집 아이콘을 클릭하면 됩니다.
![](https://main.qcloudimg.com/raw/3fa148b2e43f30fb891adee75ff255db.png)


## 예시

**배경**
APPID가 1250000000인 사용자가 examplebucket-1250000000이라는 버킷을 생성하고, CDN 가속 엔드포인트 도메인 이름을 활성화했습니다.

```shell
examplebucket-1250000000.file.myqcloud.com
```

버킷의 origin-pull 주소를 다음과 같이 구성합니다.

```shell
abc.example.com
```

원본 `http://abc.example.com`에 이미지 picture.jpg를 저장합니다.

**클라이언트가 서버에 처음 액세스한 경우입니다(Origin-pul 동기화 비활성화)**:

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

COS는 객체를 적중할 수 없음을 확인하면 클라이언트에 HTTP 상태 코드 302를 반환하고 다음 주소로 리디렉션합니다.

```shell
http://abc.example.com/picture.jpg
```

**클라이언트가 서버에 처음 액세스한 경우입니다(Origin-pul 동기화 활성화)**:

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

COS는 객체를 적중할 수 없음을 확인하면 클라이언트에 HTTP 상태 코드 200을 반환하고 다음 주소로 리디렉션합니다.

```shell
http://abc.example.com/picture.jpg
```

그런 다음 원본은 액세스를 보장하기 위해 클라이언트에 객체를 제공하고 COS는 원본에서 picture.jpg를 복사하여 example 버킷의 루트 디렉터리에 저장합니다.

**2차 액세스**:

```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```

COS가 루트 디렉터리에 저장된 picture.jpg 객체에 직접 적중하여 클라이언트에 반환합니다.

