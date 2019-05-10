## 소개
객체의 HTTP 헤더(Header)는 서버가 브라우저에 HTTP 프로토콜로 HTML 자료를 전송하기 전 보낸 문자열입니다. HTTP 헤더(Header) 수정으로 페이지의 응답 형식을 바꾸거나 구성 정보를 전달합니다. 예: 캐시 시간 수정. 객체의 HTTP 헤더 수정은 객체 자체를 수정하지 않습니다.
예: Header의 Content-Encoding을 gzip으로 수정하였지만, 파일 자체가 사전에 gz를 사용하여 압축한 적이 없으므로 해제 코드 오류가 나타납니다.

## 작업 절차
1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하고 좌측 메뉴 [버킷 리스트]를 선택한 후 버킷 리스트에 접근합니다. 객체 가 위치한 버킷을 한번 클릭한 후 해당 버킷에 접근합니다.
  ![접근 권한1](https://main.qcloudimg.com/raw/b90ad17947a0ec530db87210f4b9027d.png)
2. 헤더를 설정할 객체를 찾아 객체 우측의 [세부 정보]를 한번 클릭합니다.
  ![HTTP 헤더1 설정](https://main.qcloudimg.com/raw/4282ea6ea80d720a6f76604f1c2bf62f.png)
3. 파일 리스트 하단에서 [사용자 지정 Header]를 찾은 후 [Header 추가]를 한번 클릭하여 설정할 매개변수 유형(사용자 지정 콘텐츠는 사용자 지정 이름을 입력해야 함)을 선택하고 대응하는 값을 입력합니다. COS는 구성을 위해 다음 6가지 객체 HTTP 헤더 식별을 제공합니다. 헤더 구성 설명은 다음과 같습니다. 구성 완료 후, [저장]을 한번 클릭하면 됩니다.

|        HTTP 헤더        |          설명          |              예시               |
| :---------------------: | :--------------------: | :-----------------------------: |
|      Content-Type       |    파일의 MIME 정보    |           image/jpeg            |
|      Cache-Control      |     파일의 캐시 메커니즘    |      no-cache;max-age=200       |
|   Content-Disposition   |    MIME 프로토콜의 확장     | attachment;filename="fname.ext" |
|    Content-Encoding     |     파일의 코딩 형식     |              UTF-8              |
|         Expires         | 캐시의 무효 날짜를 제어하는데 사용 |  Wed, 21 Oct 2015 07:28:00 GMT  |
| x-cos-meta-[사용자 지정 내용] |       사용자 지정 내용       |           사용자 지정 내용            |

![](https://main.qcloudimg.com/raw/ce52b4ffee10a75eb12b1e780f678768.png)


## 예시

APPID는 1250000000이며 생성한 버킷 이름은 examplebucket-1250000000입니다. 버킷의 루트 디렉터리에 객체 exampleobject.txt를 업로드하였습니다.

객체의 HTTP 헤더를 사용자가 지정하지 않았을 경우, 브라우저 또는 클라이언트에서 다운로드할 때 획득하는 객체 헤더 예시는 다음과 같습니다.
#### 요청
```http
GET /exampleobject.txt HTTP/1.1
Host: examplebucket-1250000000.file.myqcloud.com
Accept: */*
```

#### 응답
```http
HTTP/1.1 200 OK
Content-Language:zh-CN
Content-Type: text/plain
Content-Disposition: attachment; filename*="UTF-8''exampleobject.txt"
Access-Control-Allow-Origin: *
Last-Modified: Tue, 11 Jul 2017 15:30:35 GMT
```

다음 구성 추가:
![HTTP 헤더3 설정](//mc.qcloudimg.com/static/img/bcba7754ca585143371935a9f4f0228a/image.png)
다시 요청을 보낼 경우, 브라우저 또는 클라이언트에서 획득하는 객체 헤더 예시는 다음과 같습니다.
#### 요청
```http
GET /exampleobject.txt HTTP/1.1
Host: examplebucket-1250000000.file.myqcloud.com
Accept: */*
```

#### 응답
```http
HTTP/1.1 200 OK
Content-Language:zh-CN
Cache-Control: no-cache
Content-Type: image/jpeg
Content-Disposition: attachment; filename*="abc.txt"
x-cos-meta-md5: 1234
Access-Control-Allow-Origin: *
Last-Modified: Tue, 11 Jul 2017 15:30:35 GMT
```
