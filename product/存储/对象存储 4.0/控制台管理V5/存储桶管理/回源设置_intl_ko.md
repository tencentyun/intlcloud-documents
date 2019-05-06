## 소개
COS 콘솔을 통해 버킷에 오리진 요청 규칙을 설정할 수 있습니다. 요청한 객체가 버킷에 존재하지 않거나 지정 요청에 리디렉션해야 할 경우, 오리진 요청 규칙을 통해 COS에서 해당하는 데이터에 접근할 수 있습니다. 오리진 요청 설정은 주로 데이터의 핫 마이그레이션, 지정 요청의 리디렉션 등 시나리오에 사용되며 자체의 실제 수요에 따라 설정할 수 있습니다.

>?오리진 요청의 데이터 풀링 성공율은 네트워크 환경에 의존합니다. 우선 China Telecom, China Mobile, China Unicom 등 IP 주소 범위를 사용하십시오.

![](https://main.qcloudimg.com/raw/10f9f4a6c04cb95cfe0429fb30d091a3.png)
## 작업 절차
1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하여 좌측 메뉴 [버킷 리스트]를 선택하고 버킷 리스트 페이지에 액세스합니다. 오리진 요청을 설정할 버킷을 한번 클릭합니다.
![](https://main.qcloudimg.com/raw/b90ad17947a0ec530db87210f4b9027d.png)
2. [기본 설정]을 한번 클릭하고 오리진 요청 설정을 찾은 다음 현재 상태를 활성화로 수정한 후, 오리진 요청 주소를 입력하고 마지막에 [저장]을 한번 클릭하면 됩니다. 구성 항목에 대한 설명은 다음과 같습니다.
 **오리진 요청 주소**: 도메인 이름 또는 IP 주소만 입력하면 됩니다. 도메인 이름 또는 IP 주소 뒤에 포트 번호 추가를 지원합니다. 접두사 `http://` 또는 `https`를 추가하지 않아도 됩니다(잠시 지원하지 않음)
올바른 예시 주소는 다음과 같습니다.
```shell
abc.example.com
abc.example.com:8080
10.10.10.10
10.10.10.10:8080
```


## 예시
**배경**
APPID가 1250000000인 사용자가 이름이 examplebucket-1250000000인 버킷을 생성하고 CDN 가속 접근 도메인을 활성화하였습니다.
```shell
examplebucket-1250000000.file.myqcloud.com
```

버킷 오리진 요청 주소를 다음과 같이 설정합니다.
```shell
abc.example.com
```
오리진 서버 `http://abc.example.com`에 사진 picture.jpg을 저장합니다.

**클라이언트의 첫 번째 접근**:
```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```
COS는 적중할 수 없는 객체를 발견했을 경우, 클라이언트에 302 HTTP 상태 코드를 반환하고 다음 주소로 리디렉션합니다.
```shell
http://abc.example.com/picture.jpg
```
이때 객체는 오리진 서버로부터 클라이언트에 제공하여 접근을 보장합니다. 동시에 COS는 오리진 서버에서 picture.jpg 를 복사하고 버킷 example의 루트 디렉터리에 저장합니다.

**두 번째 접근**:
```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```
COS에서 직접 루트 디렉터리의 picture.jpg 객체에 적중하고 클라이언트에 반환합니다.
