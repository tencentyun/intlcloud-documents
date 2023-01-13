## 소개
객체의 HTTP 헤더(메타데이터 헤더)는 서버가 HTTP 프로토콜로 HTML 자료를 브라우저에 전송하기 전 보내는 문자열입니다. HTTP 헤더(메타데이터 헤더) 수정을 통해서 페이지의 응답 형식이나 설정 정보를 전달할 수 있습니다. 캐시 시간 수정이 그 예입니다. 객체의 HTTP 헤더 수정으로 객체 자체를 수정할 수 없습니다.

예시: Header의 Content-Encoding을 gzip으로 수정해도 파일 자체는 이전에 gz를 이용해 압축한 적이 없어 복호화 에러가 나타날 수 있습니다.

>? 아카이브 유형의 객체는 사용자 정의 Headers를 지원하지 않습니다.
>

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭합니다.
3. 객체가 속한 버킷을 찾아 해당 버킷 이름을 클릭합니다.
4. 왼쪽 사이드바에서 **파일 리스트**를 클릭합니다.
5. 헤더를 사용자 지정할 객체를 찾고 오른쪽 작업 열에서 **추가 작업 > 사용자 지정 헤더**를 클릭합니다. 여러 객체의 헤더를 사용자 정의하려면 여러 객체를 선택하고 상단의 **추가 작업 > 사용자 지정 헤더**를 클릭합니다.
6. 팝업 창에서 설정할 메타데이터 헤더 매개변수 유형을 선택하고 해당 메타데이터 값을 입력한 후 **확인**을 클릭합니다.
COS는 설정을 위해 다음 6개의 객체 HTTP 헤더 식별자를 제공합니다. 헤더 설정 설명은 다음과 같습니다.
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
      <td>gzip</td>
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


## License 요청 예시

APPID 1250000000으로 examplebucket-1250000000이라는 이름의 버킷을 생성하고 객체 exampleobject.txt를 버킷 루트 디렉터리에 업로드하였다고 가정해봅니다.

객체의 HTTP 헤더가 사용자 정의되지 않은 경우 브라우저나 클라이언트에 다운로드할 때 얻는 객체 헤더 예시는 아래와 같습니다.

#### 요청

```plaintext
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:35:16 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511316;1586518516&q-key-time=1586511316;1586518516&q-header-list=date;host&q-url-param-list=&q-signature=1bd1898e241fb978df336dc68aaef4c0acae****
Connection: close
```

#### 응답

```plaintext
HTTP/1.1 200 OK
Content-Type: text/plain
Content-Disposition: attachment; filename*="UTF-8''exampleobject.txt"
Access-Control-Allow-Origin: *
Last-Modified: Fri, 10 Apr 2020 09:35:05 GMT 
```

아래 설정 추가:

요청을 다시 보내는 경우 브라우저나 클라이언트에서 얻을 수 있는 객체 헤더 예시는 아래와 같습니다.

#### 요청

```plaintext
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:35:16 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511316;1586518516&q-key-time=1586511316;1586518516&q-header-list=date;host&q-url-param-list=&q-signature=1bd1898e241fb978df336dc68aaef4c0acae****
Connection: close
```

#### 응답

```plaintext
HTTP/1.1 200 OK
Cache-Control: no-cache
Content-Type: image/jpeg
Content-Disposition: attachment; filename*="abc.txt"
x-cos-meta-md5: 1234
Access-Control-Allow-Origin: *
Last-Modified: Fri, 10 Apr 2020 09:35:05 GMT 
```

