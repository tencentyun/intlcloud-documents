## 소개

COS(Cloud Object Storage) 콘솔에서 버킷에 대한 Origin-pull 규칙을 구성할 수 있습니다. 요청한 객체가 버킷에 없거나 특정 요청을 리디렉션해야 하는 경우 COS를 통해 해당 데이터에 액세스하도록 Origin-pull 규칙을 구성할 수 있습니다. Origin-pull 구성은 주로 핫 데이터 마이그레이션, 특정 요청 리디렉션 및 기타 관련 시나리오에 사용됩니다.

>?
>- Origin-pul에 의한 데이터 풀링 성공률은 네트워크 환경과 관련이 있습니다. China Telecom, China Mobile, China Unicom 등의 IP를 우선적으로 사용하십시오.
>- 금융 클라우드 리전의 버킷은 Origin-pull 설정을 지원하지 않습니다.
>

<img src="https://main.qcloudimg.com/raw/f63a74cf70a9f6582e52e13a2b16e72a.png" width="90%">


## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭합니다.
3. Origin-pull 설정이 필요한 버킷을 클릭하여 버킷 상세 페이지로 이동합니다.
4. 왼쪽 사이드바에서 **기본 설정 > Origin-pull 설정**을 선택하고 **Origin-pull 규칙 추가**를 클릭합니다.
![](https://main.qcloudimg.com/raw/69fc0f3042e59c3e9c2667d06aa068fa.png)
5. 팝업 창에서 다음 정보를 설정하고 **다음 단계**를 클릭합니다.

 - **Origin-pull 모드**: Origin-pull 모드는 실제 필요에 따라 선택할 수 있습니다.
    - **Origin-pull 비동기화**: 요청된 파일이 COS에 없는 경우 COS는 지정된 원본 서버에서 파일을 검색하여 파일을 버킷에 업로드하지만 클라이언트에는 반환하지 않습니다.
    - **Origin-pull 동기화**: 요청한 파일이 COS에 없는 경우, COS는 지정된 원본 서버에서 파일을 검색하여 파일을 클라이언트에 반환하고 버킷에 업로드합니다.
    - **리디렉션**: 버킷 액세스 요청 시 지정된 오류가 보고되면, COS는 리디렉션 주소를 클라이언트에 반환하고 원본 서버의 파일을 저장하지 않습니다. 클라이언트는 리디렉션 주소를 통해 리소스에 액세스하도록 원본 서버에 요청합니다.
 - **Origin-pul 조건**: Origin-Pull을 트리거하기 위해 동시에 충족되어야 하는 모든 조건을 지정합니다.
    - **HTTP 상태 코드 404**: 비동기화 Origin-pull 또는 동기화 Origin-pull을 선택하면 HTTP 상태 코드가 404일 때 Origin-pull이 트리거됩니다. 이 항목은 필수 항목이며 취소할 수 없습니다. Origin-pull 모드를 선택할 때 400 - 599의 HTTP 상태 코드를 입력할 수 있습니다.
    - **파일명 접두사**: 요청한 파일명 접두사가 매칭되면 Origin-pul 규칙을 트리거할 수 있습니다. 예를 들어, 파일명 접두사를 prefix로 설정하여 `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`에 액세스하고 반환된 HTTP 상태 코드가 404이면 Origin-pul 규칙이 트리거됩니다.
 - **Origin-pul 프로토콜**: COS에서 지정한 원본 서버에 액세스할 때 사용하는 HTTP 프로토콜 옵션에는 강제 HTTPS, "강제 HTTP, 요청 프로토콜을 따름이 있습니다.
    - 강제 HTTPS/HTTP를 선택할 경우, COS는 HTTPS/HTTP 프로토콜로 원본 서버에 액세스합니다.
    - 요청 프로토콜을 따름을 선택할 경우, COS는 COS에 요청할 때 사용한 프로토콜로 원본 서버에 액세스합니다.
 - **요청 매개변수**: COS에 액세스할 때 가져오는 queryString 요청 매개변수를 원본 서버로 패스스루 여부.
 - **지정 요청 헤더 패스스루**: 원본에 패스스루할 요청 헤더를 지정합니다. 리디렉션 origin-pull 유형이 선택된 경우 이 항목이 설정되지 않습니다.
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
 - **스탠바이 포워딩 주소**: 도메인 이름 또는 IP 주소를 지원합니다. 특정 주소 설정을 지원합니다. 다음 구성 항목을 설정할 수 있습니다.
    - **파일 고정**: Origin-pul 규칙을 트리거할 때 고정된 파일을 전부 기본값으로 리디렉션합니다.
    - **지정된 접두사**: Origin-pul 규칙이 트리거될 때 요청이 리디렉션되는 파일의 접두사를 지정합니다. 예를 들어, 접두사가 `test`로 지정된 경우 `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`에 액세스하면 요청이 `<Origin-pull 주소>/test/prefix123.jpg`로 리디렉션되고 origin-pull 규칙이 트리거됩니다.
    - **지정된 접미사**: Origin-pul 규칙을 트리거될 때 요청이 리디렉션되는 파일의 접미사를 지정합니다. 예를 들어, 접미사가 `.jpg`로 지정된 경우, `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123`에 액세스하면 요청이 `<Origin-pull 주소>/prefix123.jpg`로 리디렉션되고 origin-pull 규칙이 트리거됩니다.
  <b>Note：</b>
      - 파일 고정을 선택하면 기본적으로 다른 두 개 유형은 선택할 수 없습니다.
      - 접두사와 접미사는 동시에 지정하여 적용할 수 있습니다.

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
 - **스탠바이 포워딩 주소**: 도메인 이름 또는 IP 주소를 지원합니다. 특정 주소 설정을 지원합니다. 다음 구성 항목을 설정할 수 있습니다.
    - **파일 고정**: Origin-pul 규칙을 트리거할 때 고정된 파일을 전부 기본값으로 리디렉션합니다.
    - **지정된 접두사**: Origin-pul 규칙이 트리거될 때 요청이 리디렉션되는 파일의 접두사를 지정합니다. 예를 들어, 접두사가 `test`로 지정된 경우 `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`에 액세스하면 요청이 `<Origin-pull 주소>/test/prefix123.jpg`로 리디렉션되고 origin-pull 규칙이 트리거됩니다.
    - **지정된 접미사**: Origin-pul 규칙을 트리거될 때 요청이 리디렉션되는 파일의 접미사를 지정합니다. 예를 들어, 접미사가 `.jpg`로 지정된 경우, `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123`에 액세스하면 요청이 `<Origin-pull 주소>/prefix123.jpg`로 리디렉션되고 origin-pull 규칙이 트리거됩니다.
  <b>Note：</b>
      - 파일 고정을 선택하면 기본적으로 다른 두 개 유형은 선택할 수 없습니다.
      - 접두사와 접미사는 동시에 지정하여 적용할 수 있습니다.

 - **3XX 종속 정책**: 이 정책이 활성화된 경우 원본이 3xx 리디렉션을 반환하면 COS가 이를 따라 다른 원본에서 데이터를 가져옵니다. **비활성화**를 선택하면 리소스를 풀링하지 않습니다.
 - **원본 서버 응답 패킷**: 이 기능이 활성화된 후 상태 코드 등 기타 정보를 포함한 원본 서버 응답 패킷을 직접 반환합니다.
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
 - **스탠바이 포워딩 주소**: 도메인 이름 또는 IP 주소를 지원합니다. 특정 주소 설정을 지원합니다. 다음 구성 항목을 설정할 수 있습니다.
    - **파일 고정**: Origin-pul 규칙을 트리거할 때 고정된 파일을 전부 기본값으로 리디렉션합니다.
    - **지정된 접두사**: Origin-pul 규칙이 트리거될 때 요청이 리디렉션되는 파일의 접두사를 지정합니다. 예를 들어, 접두사가 `test`로 지정된 경우 `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123.jpg`에 액세스하면 요청이 `<Origin-pull 주소>/test/prefix123.jpg`로 리디렉션되고 origin-pull 규칙이 트리거됩니다.
    - **지정된 접미사**: Origin-pul 규칙을 트리거될 때 요청이 리디렉션되는 파일의 접미사를 지정합니다. 예를 들어, 접미사가 `.jpg`로 지정된 경우, `https://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/prefix123`에 액세스하면 요청이 `<Origin-pull 주소>/prefix123.jpg`로 리디렉션되고 origin-pull 규칙이 트리거됩니다.
  <b>Note：</b>
      - 파일 고정을 선택하면 기본적으로 다른 두 개 유형은 선택할 수 없습니다.
      - 접두사와 접미사는 동시에 지정하여 적용할 수 있습니다.

 - **리디렉션 Code**: 301, 302, 307을 선택할 수 있으며, 기본값은 301입니다.
:::
</dx-tabs>

7. 설정된 Origin-pull 규칙이 정확한지 확인하고 **확인**을 클릭합니다.
기본적으로 COS는 항상 가장 최근의 규칙에 가장 높은 우선 순위를 부여하여 Origin-pull을 수행합니다. 우선 순위를 수동으로 변경하려면 규칙 목록의 우선 순위 열 아래에 있는 편집 아이콘을 클릭할 수 있습니다.

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

