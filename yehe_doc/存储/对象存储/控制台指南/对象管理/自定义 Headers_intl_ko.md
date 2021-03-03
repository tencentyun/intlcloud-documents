## 소개
객체의 HTTP 헤더(Header)는 서버가 HTTP 프로토콜로 HTML 자료를 브라우저에 전송하기 전 보내는 문자열입니다. HTTP 헤더(Header) 수정을 통해서 페이지의 응답 형식이나 설정 정보를 전달할 수 있습니다. 캐시 시간 수정이 그 예입니다. 객체의 HTTP 헤더 수정으로 객체 자체를 수정할 수 없습니다.

예시: Header의 Content-Encoding을 gzip으로 수정해도 파일 자체는 이전에 gz를 이용해 압축한 적이 없어 복호화 에러가 나타날 수 있습니다.

>?CAS 유형의 객체는 사용자 정의 Headers를 지원하지 않습니다.

## 작업 순서
1. [객체 버킷 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하고 왼쪽 메뉴바의 [버킷 리스트]를 선택하여 버킷 리스트 페이지로 이동합니다. 객체가 속한 버킷을 클릭하여 버킷으로 이동합니다.
2. 버킷의 “파일 리스트” 모듈에서 사용자 정의 헤더가 필요한 단일 객체를 찾고 오른쪽 작업 바에서 [더 많은 조작] > [사용자 정의 헤더]를 클릭하여 설정을 진행합니다. 여러 객체에 대한 사용자 정의 헤더가 필요할 경우 여러 객체를 선택하고 [더 많은 조작] 메뉴에서 슬라이드 바를 내린 후 [사용자 정의 헤더]를 선택하십시오.
![](https://main.qcloudimg.com/raw/88779600818f3670df2f7df62fd1b3a0.png)
3. **사용자 정의 Headers**팝업창에서 [Header 추가]를 클릭하여 설정이 필요한 매개변수 유형을 선택하고 해당 값을 입력합니다. COS에서 다음 6가지의 객체 HTTP 헤더 식별자로 설정이 가능합니다. 헤더 설정에 관한 설명은 아래와 같습니다. 설정 완료 후 [저장]을 누릅니다.
![](https://main.qcloudimg.com/raw/191fbd1b903069b5e546bb237b050ee2.png)
<table>
   <tr>
      <th>HTTP 헤더</th>
      <th>설명</th>
      <th>예시</th>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>파일의 MIME 정보</td>
      <td>image/jpeg</td>
   </tr>
   <tr>
      <td>Cache-Control</td>
      <td>파일의 캐시 메커니즘</td>
      <td>no-cache;max-age=200</td>
   </tr>
   <tr>
      <td>Content-Disposition</td>
      <td>MIME 프로토콜 확장</td>
      <td>attachment;filename="fname.ext"</td>
   </tr>
   <tr>
      <td>Content-Encoding</td>
      <td>파일 인코딩 포맷</td>
      <td>UTF-8</td>
   </tr>
   <tr>
      <td>Expires</td>
      <td>캐시 제어에 사용되는 만료일</td>
      <td>Wed, 21 Oct 2015 07:28:00 GMT</td>
   </tr>
   <tr>
      <td>x-cos-meta-[사용자 정의 접미사]</td>
      <td>사용자 정의 콘텐츠</td>
      <td>x-cos-meta-via: homepage</td>
   </tr>
</table>


## 예시

APPID 1250000000으로 examplebucket-1250000000이라는 이름의 버킷을 생성하고 객체 exampleobject.txt를 버킷 루트 디렉터리에 업로드하였다고 가정해봅시다.

객체의 HTTP 헤더가 사용자 정의되지 않은 경우 브라우저나 클라이언트에 다운로드할 때 얻는 객체 헤더 예시는 아래와 같습니다.
#### 요청
```sh
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

아래 설정 추가:
![](https://main.qcloudimg.com/raw/2474d24e7d1d365e0c736572aae8f652.png)
요청을 다시 보내는 경우 브라우저나 클라이언트에서 얻을 수 있는 객체 헤더 예시는 아래와 같습니다.

#### 요청
```sh
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

