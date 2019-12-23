## 기능 설명
POST Object restore API는 COS를 통해 archive 유형으로 보관한 개체를 복구할 수 있습니다. 복구한 읽기 가능 개체는 임시적이기 때문에 읽기 가능을 유지하고 해당 임시 복제본을 삭제하는 시간을 설정할 수 있습니다. Days 매개 변수를 사용하여 임시 개체의 만료 시간을 지정할 수 있으며, 해당 시간을 초과한 기간 동안 복제, 연장 등 어떠한 작업도 개시하지 않을 경우, 해당 임시 개체는 자동적으로 삭제됩니다. 임시 개체는 archive 유형 개체의 복제본이므로 보관된 소스 개체는 이 기간 동안 줄곧 존재하게 됩니다.

## 요청
### 요청 예제

```shell
POST /<ObjectKey>?restore HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조하십시오.).


### 요청 헤더
#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 문서를 참조하십시오.
#### 비공통 헤더
해당 요청 작업은 특별한 요청 헤더 정보가 없습니다.

### 요청체
해당 요청 작업을 구현하려면 다음과 같이 요청체가 필요합니다.

```shell
<RestoreRequest>
   <Days>2</Days>
   <CASJobParameters>
       <Tier>Bulk</Tier>
   </CASJobParameters>
</RestoreRequest>
```

구체적인 데이터 설명은 다음과 같습니다.
<table>
   <tr>
      <th nowrap="nowrap">노드 이름(키워드)</th>
      <th>부모 노드</th>
      <th>설명</th>
      <th>유형</th>
      <th>필수 여부</th>
   </tr>
   <tr>
      <td>RestoreRequest</td>
      <td>없음</td>
      <td>데이터 복구에 사용되는 컨테이너</td>
      <td>Container</td>
      <td>예</td>
   </tr>
   <tr>
      <td>Days</td>
      <td>없음</td>
      <td>임시 복제본의 만료 시간 설정</td>
      <td>integer</td>
      <td>예</td>
   </tr>
   <tr>
      <td>CASJobParameters</td>
      <td>없음</td>
      <td>작업 매개변수 컨테이너 보관 저장</td>
      <td>Container</td>
      <td>예</td>
   </tr>
   <tr>
      <td>Tier</td>
      <td>없음</td>
      <td>데이터를 복구할 때, Tier는 CAS가 지원하는 세 가지 복구 모드로 지정할 수 있으며, 이는 Standard(표준 모드, 복구 임무는 35시간 내 완료), Expedited(급속 모드, 복구 임무는 15분 내 완료) 및 Bulk(배치 모드, 복구 임무는 5-12시간 내 완료)를 포함합니다.</td>
      <td>Enum</td>
      <td>예</td>
   </tr>
</table>



## 응답
### 응답 헤더

#### 공통 응답 헤더
해당 응답은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 문서를 참조하십시오.
#### 고유의 응답 헤더
해당 응답은 특별한 응답 헤더가 없습니다.

### 응답 본문
해당 응답 본문은 비어 있습니다.

### 오류 코드
해당 요청 작업은 다음 오류 정보가 나타날 수 있으며, 흔히 볼 수 있는 오류 정보는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.

오류 코드|설명|HTTP 상태 코드
---|---|---
None|복구 성공|202 [Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)
RestoreAlreadyInProgress|객체가 이미 복구 중입니다.|409 [Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)


## 실제 사례

### 요청

```shell
POST /exampleobject?restore HTTP/1.1
Accept: */*
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 105
Content-Type: application/x-www-form-urlencoded

<RestoreRequest>
   <Days>2</Days>
   <CASJobParameters>
       <Tier>Bulk</Tier>
   </CASJobParameters>
</RestoreRequest>
```

### 응답

```shell
HTTP/1.1 202 Accepted
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-cos
x-cos-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=
```
