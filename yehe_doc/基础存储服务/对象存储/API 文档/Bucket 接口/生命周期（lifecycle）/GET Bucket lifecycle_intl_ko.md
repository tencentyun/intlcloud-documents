## 기능 설명
GET Bucket lifecycle은 Bucket의 라이프사이클 설정을 조회하는 데 사용됩니다. 만약 이 Bucket에 라이프사이클 규칙이 설정되지 않았다면 NoSuchLifecycleConfiguration이 반환됩니다.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer 사용 권장
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=GetBucketLifecycle&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>디버깅 클릭</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 검색 인터페이스 등의 기능을 제공합니다. 각 호출의 요청 내용 및 반환 결과를 확인하고 SDK 호출 예시를 자동으로 생성할 수 있습니다.
            </div>
        </div>
    </div>
</div>




## 요청
#### 요청 예시

```shell
GET /?lifecycle HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com，이 중 &lt;BucketName-APPID> 는 APPID 확장자를 가진 버킷 이름입니다. 예: examplebucket-1250000000. [버킷 개요 > 기본 정보](https://intl.cloud.tencent.com/document/product/436/38493) 및 [버킷 개요 > 버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312) 문서를 참고하십시오. &lt;Region>은 COS의 가용 리전입니다. [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224) 문서를 참고하십시오.
> - Authorization: Auth String(자세한 내용은 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참고하십시오).
> 

#### 요청 헤더

본 인터페이스는 공용 요청 헤더만 사용합니다. 자세한 내용은 [공용 요청 헤더](https://intl.cloud.tencent.com/document/product/436/7728) 문서를 참고하십시오.

#### 요청 본문
해당 요청의 요청 본문은 공란입니다.

## 응답

#### 응답 헤더

본 인터페이스는 공통 응답 헤더만 반환합니다. 자세한 내용은 [공통 응답 헤더](https://intl.cloud.tencent.com/document/product/436/7729) 문서를 참고하십시오.


#### 응답 본문
응답 본문에 있는 각 요소의 내용과 의미는 PUT Buket lifecycle 요청 본문과 일치합니다. 자세한 내용은 [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) 문서의 요청 본문 노드에 대한 설명을 참고하십시오.

#### 오류 코드

이 인터페이스는 통일된 오류 응답 및 오류 코드를 따르며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오.

## 실제 사례

#### 요청
```shell
GET /?lifecycle HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 16 Aug 2017 12:23:54 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1502857357;1502937357&q-key-time=1502857357;1502937357&q-header-list=host&q-url-param-list=lifecycle&q-signature=da155cda3461bee7422ee95367ac8013ef84****

```

#### 응답
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 312
Date: Wed, 16 Aug 2017 12:23:54 GMT
Server: tencent-cos
x-cos-request-id: NTk5NDM5NWFfMjQ4OGY3Xzc3NGRf****

<LifecycleConfiguration>
  <Rule>
    <ID>id1</ID>
    <Filter>
       <Prefix>documents/</Prefix>
    </Filter>
    <Status>Enabled</Status>
    <Transition>
      <Days>100</Days>
      <StorageClass>STANDARD_IA</StorageClass>
    </Transition>
  </Rule>
  <Rule>
    <ID>id2</ID>
    <Filter>
       <Prefix>logs/</Prefix>
    </Filter>
    <Status>Enabled</Status>
    <Expiration>
      <Days>10</Days>
    </Expiration>
  </Rule>
</LifecycleConfiguration>
```
