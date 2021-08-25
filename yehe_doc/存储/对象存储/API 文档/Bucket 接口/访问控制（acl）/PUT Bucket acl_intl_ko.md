## 기능 설명

PUT Bucket acl 인터페이스는 버킷의 ACL을 작성하는 데 사용되며 요청 헤더 `x-cos-acl` 및 `x-cos-grant-*`를 통해 ACL 정보를 전달하거나 요청 본문을 통해 XML 형식으로 ACL 정보를 전달할 수 있습니다.
>!
>- 요청 헤더를 통해 ACL을 설정하는 방법과 요청 본문을 통해 ACL을 설정하는 두 가지 방법 중 하나만 선택할 수 있습니다.
>- PUT Bucket acl은 덮어쓰기 작업입니다. 신규 ACL이 전달되면 기존 ACL을 덮어씁니다.
>- Tencent Cloud CAM 루트 계정 또는 익명 사용자에게만 권한 부여가 가능하며, 서브 계정 또는 사용자 그룹에 권한 부여는 [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) 인터페이스를 사용하십시오. ACL에 대한 자세한 설명은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583)를 참고하시기 바랍니다.
>- 해당 API의 요청자는 버킷에 대한 ACL 쓰기 권한이 있어야 합니다.
>

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer 사용 권장
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutBucketAcl&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>디버깅 클릭</a>
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

**예시 1**
```shell
PUT /?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: 0
Authorization: Auth String
```
**예시 2**
```shell
PUT /?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String

[Request Body]
```
>? 
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com，이 중 &lt;BucketName-APPID> 는 APPID 확장자를 가진 버킷 이름입니다. 예: examplebucket-1250000000. [버킷 개요 > 기본 정보](https://intl.cloud.tencent.com/document/product/436/38493) 및 [버킷 개요 > 버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312) 문서를 참고하십시오. &lt;Region>은 COS의 가용 리전입니다. [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224) 문서를 참고하십시오.
> - Authorization: Auth String(자세한 내용은 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참고하십시오).
> 

#### 요청 매개변수 

본 인터페이스는 요청 매개변수가 없습니다.

#### 요청 헤더

본 인터페이스는 공통 요청 헤더 뿐만 아니라, 아래의 요청 헤더도 지원합니다. 공통 요청 헤더 관련 자세한 내용은 [공통 요청 헤더](https://intl.cloud.tencent.com/document/product/436/7728) 문서를 참고하십시오.

이름|설명|유형|필수 선택 여부
---|---|---|---
x-cos-acl|버킷의 ACL 속성을 정의합니다. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583#.E9.A2.84.E8.AE.BE.E7.9A.84-acl)를 참고하십시오. private, public-read 등과 같이 문서에 있는 버킷의 사전 설정 ACL 부분의 기본값은 private입니다.|Enum| 아니요
x-cos-grant-read|승인된 자에게 버킷 읽기 권한을 부여합니다. 형식: id="[OwnerUin]", 예: id="100000000001". 쉼표(,)를 사용하여 여러 권한 수여자 그룹을 구분할 수 있습니다. 예: `id="100000000001",id="100000000002"`|string|아니요
x-cos-grant-write|승인된 자에게 버킷 쓰기 권한을 부여합니다. 형식: id="[OwnerUin]", 예: id="100000000001"). 쉼표(,)를 사용하여 여러 권한 수여자 그룹을 구분할 수 있습니다. 예: `id="100000000001",id="100000000002"`|string|아니요
x-cos-grant-read-acp|승인된 자에게 버킷의 ACL 읽기 권한을 부여합니다. 형식: id="[OwnerUin]", 예: id="100000000001". 쉼표(,)를 사용하여 여러 권한 수여자 그룹을 구분할 수 있습니다. 예: `id="100000000001",id="100000000002"`|string|아니요
x-cos-grant-write-acp|승인된 자에게 버킷의 ACL 쓰기 권한을 부여합니다. 형식: id="[OwnerUin]", 예: id="100000000001". 쉼표(,)를 사용하여 여러 권한 수여자 그룹을 구분할 수 있습니다. 예: `id="100000000001",id="100000000002"`|string|아니요
x-cos-grant-full-control|승인된 자에게 버킷 작업의 모든 권한을 부여합니다. 형식: id="[OwnerUin]", 예: id="100000000001". 쉼표(,)를 사용하여 여러 권한 수여자 그룹을 구분할 수 있습니다. 예: `id="100000000001",id="100000000002"`|string|아니요

#### 요청 본문

버킷 소유자 및 전체 권한 부여 정보를 포함한 **application/xml** 요청 데이터를 제출합니다.

```shell
<AccessControlPolicy>
	<Owner>
		<ID>string</ID>
	</Owner>
	<AccessControlList>
		<Grant>
			<Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
				<URI>string</URI>
			</Grantee>
			<Permission>Enum</Permission>
		</Grant>
		<Grant>
			<Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
				<ID>string</ID>
			</Grantee>
			<Permission>Enum</Permission>
		</Grant>
	</AccessControlList>
</AccessControlPolicy>
```

구체적인 노드 설명은 다음과 같습니다.

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
AccessControlPolicy|None|PUT Bucket acl 작업을 포함한 모든 요청 정보|Container|예

**Container 노드 AccessControlPolicy의 내용:**

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
Owner|AccessControlPolicy|버킷 소유자 정보|Container|예
AccessControlList|AccessControlPolicy|권한 수여자 정보 및 권한 정보|Container|예

**Container 노드 Owner 의 내용:**

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
ID|AccessControlPolicy.Owner|버킷 소유자의 완전한 ID로, 형식:  `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`，예: `qcs::cam::uin/100000000001:uin/100000000001`|string|예

**Container 노드 AccessControlList 의 내용:**

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
Grant|AccessControlPolicy.AccessControlList|단일 권한 부여 정보. 하나의 AccessControlList는 최대 100개의 Grant만 가질 수 있습니다. |Container|예

**Container 노드 AccessControlList.Grant 의 내용:**

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
Grantee|AccessControlPolicy.AccessControlList.Grant|권한 수여자 정보, `xsi:type`은 Group 또는 CanonicalUser로 지정할 수 있습니다. Group으로 지정하면 자식 노드에는 URI만 포함 허용되며, CanonicalUser로 지정하면 자식 노드에는 ID만 포함 허용됩니다.|Container|예
Permission|AccessControlPolicy.AccessControlList.Grant|부여된 권한 정보. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583#.E6.93.8D.E4.BD.9C-permission)문서 중의 버킷 작업 부분을 참고하십시오. 예: WRITE, FULL_CONTROL 등|Enum|예

**Container 노드 AccessControlList.Grant.Grantee 의 내용:**

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
URI|AccessControlPolicy.AccessControlList.Grant.Grantee|사전 설정 사용자 그룹. [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583#.E8.BA.AB.E4.BB.BD-grantee) 문서 중의 사전 설정 사용자 부분을 참고하십시오. 예: `http://cam.qcloud.com/groups/global/AllUsers` 또는 `http://cam.qcloud.com/groups/global/AuthenticatedUsers`|string|`Grantee`의 `xsi:type`을 `Group`으로 지정할 경우 필수 사항
ID|AccessControlPolicy.AccessControlList.Grant.Grantee|권한 수여자의 전체 ID, 형식:  `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`，예: `qcs::cam::uin/100000000001:uin/100000000001`|string|`Grantee` 의 `xsi:type`을 `CanonicalUser`로 지정할 경우 필수 사항

## 응답

#### 응답 헤더

본 인터페이스는 공통 응답 헤더만 반환합니다. 자세한 내용은 [공통 응답 헤더](https://intl.cloud.tencent.com/document/product/436/7729) 문서를 참고하십시오.

#### 응답 본문

해당 요청의 응답 본문은 공란입니다.

#### 오류 코드

이 인터페이스는 통일된 오류 응답 및 오류 코드를 따르며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오.


## 실제 사례

#### 사례 1: 요청 헤더를 통한 ACL 설정

#### 요청

```shell
PUT /?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 17 Jun 2019 08:30:12 GMT
x-cos-acl: public-read
x-cos-grant-write: id="100000000002"
x-cos-grant-read-acp: id="100000000002"
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1560760212;1560767412&q-key-time=1560760212;1560767412&q-header-list=content-length;date;host;x-cos-acl;x-cos-grant-read-acp;x-cos-grant-write&q-url-param-list=acl&q-signature=5b10c6ea4e6c9630c085e1f85476c76d8c4e****
Connection: close
```

#### 응답

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Mon, 17 Jun 2019 08:30:13 GMT
Server: tencent-cos
x-cos-request-id: NWQwNzRmOTRfODhjMjJhMDlfMWRlYl81Mzc0****
```

#### 사례 2: 요청 본문을 통한 ACL 설정

#### 요청

```shell
PUT /?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 17 Jun 2019 08:30:13 GMT
Content-Type: application/xml
Content-Length: 812
Content-MD5: 1qS+8SqnivarcO6Z11R0nw==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1560760213;1560767413&q-key-time=1560760213;1560767413&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=acl&q-signature=70f96b91823f3715905df125d96fe447554e****
Connection: close

<AccessControlPolicy>
	<Owner>
		<ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
	</Owner>
	<AccessControlList>
		<Grant>
			<Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
				<URI>http://cam.qcloud.com/groups/global/AllUsers</URI>
			</Grantee>
			<Permission>READ</Permission>
		</Grant>
		<Grant>
			<Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
				<ID>qcs::cam::uin/100000000002:uin/100000000002</ID>
			</Grantee>
			<Permission>WRITE</Permission>
		</Grant>
		<Grant>
			<Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
				<ID>qcs::cam::uin/100000000002:uin/100000000002</ID>
			</Grantee>
			<Permission>READ_ACP</Permission>
		</Grant>
	</AccessControlList>
</AccessControlPolicy>
```

#### 응답

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Mon, 17 Jun 2019 08:30:13 GMT
Server: tencent-cos
x-cos-request-id: NWQwNzRmOTVfMzBjMDJhMDlfOTM3MF8yNzdj****
```
