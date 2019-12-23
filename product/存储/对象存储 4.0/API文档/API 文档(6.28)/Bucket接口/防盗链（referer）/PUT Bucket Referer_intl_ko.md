## 기능 설명

PUT Bucket Referer API는 버킷에 Referer 화이트리스트 또는 블랙리스트를 설정하는 데 사용됩니다.

## 요청

### 요청 예제

```shell
PUT /?referer HTTP 1.1
Host:<BucketName-APPID>.<Region>.myqcloud.com
Date:GMT Date
Authorization: Auth String
Content-Length:length
Content-MD5:MD5
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조).

### 요청 헤더

#### 공통 헤더

해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 문서를 참조하십시오.

#### 비공통 헤더

**필수 헤더**

<table>
   <tr>
      <th>이름</th>
      <th>설명</th>
      <th>유형</th>
      <th>필수 여부</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Content-Length</td>
      <td>RFC 2616에서 정의한 HTTP 요청 내용 길이(바이트)입니다.</td>
      <td>String</td>
      <td>예</td>
   </tr>
   <tr>
      <td>Content-MD5</td>
      <td>RFC 1864에서 정의한 Base64로 인코딩된 128-bit 내용 MD5 검사값입니다. 이 헤더는 파일 내용에 변화가 발생했는지를 검사하는 데 사용됩니다.</td>
      <td>String</td>
      <td>예</td>
   </tr>
</table>

해당 요청 작업은 특별한 요청 헤더 정보가 없습니다.

### 요청체

해당 요청 본문의 구체적인 노드 내용은 다음과 같습니다.

```shell
<RefererConfiguration>
  <Status></Status>
  <RefererType></RefererType>
  <DomainList>
    <Domain></Domain>
    <Domain></Domain>
  </DomainList>
  <EmptyReferConfiguration></EmptyReferConfiguration>
</RefererConfiguration>
```

구체적인 내용 설명은 다음과 같습니다.

| 이름                    | 부모 노드               | 설명                                                         | 유형      | 필수 선택 여부 |
| ----------------------- | -------------------- | ------------------------------------------------------------ | --------- | ---- |
| RefererConfiguration    | 없음                   | 핫 링크 보호 구성 정보                                               | Container | 예   |
| Status                  | RefererConfiguration | 핫 링크 보호 활성화 여부, 열거형 값: Eabled, Disabled                | String    | 예   |
| RefererType             | RefererConfiguration | 핫 링크 보호 유형, 열거형 값: Black-List, White-List               | String    | 예   |
| DomainList              | RefererConfiguration | 적용 도메인 이름 리스트입니다. 여러 개의 도메인 이름을 지원하며 접두사 매칭입니다. 포트를 자진 도메인 이름과 IP, 와일드카드 `*`를 지원하여 2단계 도메인 이름 또는 여러 단계 도메인 이름의 와일드카드로 합니다. | Container | 예   |
| Domain                  | DomainList           | 단일 적용 도메인 이름입니다. 예: `www.qq.com/example`, `192.168.1.2:8080`, `*.qq.com` | String    | 예   |
| EmptyReferConfiguration | RefererConfiguration | 비어 있는 Refer 접근 허가 여부, 열거형 값: Allow, Deny, 기본값: Deny | String    | 아니요   |


## 응답

### 응답 헤더

#### 공통 응답 헤더

해당 응답은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 문서를 참조하십시오.

#### 고유의 응답 헤더

해당 응답은 특별한 응답 헤더가 없습니다.

### 응답 본문

해당 응답 본문은 비어 있습니다.

### 오류 코드

해당 요청 작업은 특별한 오류 정보가 없습니다. 흔히 볼 수 있는 오류 정보는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.

## 실제 사례

### 요청

```shell
PUT /?referer HTTP 1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 25 Feb 2017 04:10:22 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1547105134;32526689134&q-key-time=1547105134;32620001134&q-header-list=content-md5;content-type;host&q-url-param-list=referer&q-signature=0f7fef5b1d2180deaf6f92fa2ee0cf87ae83f0cd\
Content-MD5: kOz7g54LMJZjxKs070V9jQ==
Content-Type: application/xml

<RefererConfiguration>
  <Status>Enabled</Status>
  <RefererType>White-List</RefererType>
  <DomainList>
    <Domain>*.qq.com</Domain>
    <Domain>*.qcloud.com</Domain>
  </DomainList>
  <EmptyReferConfiguration>Allow</EmptyReferConfiguration>
</RefererConfiguration>
```

### 응답

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: keep-alive
Date: Fri, 25 Feb 2017 04:10:22 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjFjMmJfOWIxZjRlXzZmNDhfMjIw
```
