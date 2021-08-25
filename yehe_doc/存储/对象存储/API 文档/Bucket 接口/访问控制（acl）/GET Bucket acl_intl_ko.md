## 기능 설명

GET Bucket acl 인터페이스는 버킷의 ACL 조회에 사용됩니다. 해당 API의 요청자는 버킷에 ACL 읽기 권한을 보유하고 있어야 합니다.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer 사용 권장
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=GetBucketAcl&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>디버깅 클릭</a>
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
GET /?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com, 이 중 &lt;BucketName-APPID> 는 APPID 확장자를 가진 버킷 이름입니다. 예: examplebucket-1250000000. [버킷 개요 > 기본 정보](https://intl.cloud.tencent.com/document/product/436/38493) 및 [버킷 개요 > 버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312) 문서를 참고하십시오.&lt;Region> 는 COS의 가용 리전입니다. [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224) 문서를 참고하십시오.
> - Authorization: Auth String(자세한 내용은 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참고하십시오).
> 

#### 요청 매개변수 

본 인터페이스는 요청 매개변수가 없습니다.

#### 요청 헤더

본 인터페이스는 공용 요청 헤더만 사용합니다. 자세한 내용은 [공용 요청 헤더](https://intl.cloud.tencent.com/document/product/436/7728) 문서를 참고하십시오.

#### 요청 본문
해당 요청의 요청 본문은 공란입니다.

## 응답

#### 응답 헤더

본 인터페이스는 공용 응답 헤더만 반환합니다. 자세한 내용은 [공용 응답 헤더](https://intl.cloud.tencent.com/document/product/436/7729) 문서를 참고하십시오.

#### 응답 본문

쿼리 성공 시, 버킷 소유자 및 전체 권한 부여 정보를 포함한 **application/xml** 데이터가 반환됩니다.

```shell
<AccessControlPolicy>
	<Owner>
		<ID>string</ID>
		<DisplayName>string</DisplayName>
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
				<DisplayName>string</DisplayName>
			</Grantee>
			<Permission>Enum</Permission>
		</Grant>
	</AccessControlList>
</AccessControlPolicy>
```

구체적인 노드 설명은 다음과 같습니다.

노드 이름(키워드)|부모 노드|설명|유형
---|---|---|---
AccessControlPolicy|없음|GET Bucket acl 결과의 모든 정보 저장|Container

**Container 노드 AccessControlPolicy 의 내용:**

노드 이름(키워드)|부모 노드|설명|유형
---|---|---|---
Owner|AccessControlPolicy|버킷 소유자 정보|Container
AccessControlList|AccessControlPolicy|권한 수여자 정보 및 권한 정보|Container

**Container 노드 Owner 의 내용:**

노드 이름(키워드)|부모 노드|설명|유형
---|---|---|---
ID|AccessControlPolicy.Owner|버킷 소유자의 완전한 ID로, 형식: `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`，예: `qcs::cam::uin/100000000001:uin/100000000001`|string
DisplayName|AccessControlPolicy.Owner|버킷 소유자의 이름|string

**Container 노드 AccessControlList 의 내용:**

노드 이름(키워드)|부모 노드|설명|유형
---|---|---|---
Grant|AccessControlPolicy.AccessControlList|단일 권한 부여 정보|Container

**Container 노드 AccessControlList.Grant 의 내용:**

노드 이름(키워드)|부모 노드|설명|유형
---|---|---|---
Grantee|AccessControlPolicy.AccessControlList.Grant|수여자 정보, `xsi:type`은 Group 또는 CanonicalUser이며, Group인 경우 자식 노드는 URI만 포함하고 CanonicalUser로 지정하는 경우 자식 노드에는 ID와 DisplayName만 포함합니다. |Container
Permission|AccessControlPolicy.AccessControlList.Grant|부여된 권한 정보, 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서 중의 버킷 작업 부분을 참고하십시오. 예: WRITE, FULL_CONTROL 등|Enum

**Container 노드 AccessControlList.Grant.Grantee 의 내용:**

노드 이름(키워드)|부모 노드|설명|유형
---|---|---|---
URI|AccessControlPolicy.AccessControlList.Grant.Grantee|사전 설정 사용자 그룹은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서 중의 사전 설정 사용자 부분을 참고하십시오. 예: `http://cam.qcloud.com/groups/global/AllUsers` 또는 `http://cam.qcloud.com/groups/global/AuthenticatedUsers`|string
ID|AccessControlPolicy.AccessControlList.Grant.Grantee|권한 수여자의 전체 ID, 형식: `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`. 예: `qcs::cam::uin /100000000001 :uin/100000000001`|string
DisplayName|AccessControlPolicy.AccessControlList.Grant.Grantee|권한 수여자의 이름|string

#### 오류 코드

이 인터페이스는 통일된 오류 응답 및 오류 코드를 따르며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오.

## 실제 사례

#### 요청

```shell
GET /?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 17 Jun 2019 08:37:35 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1560760655;1560767855&q-key-time=1560760655;1560767855&q-header-list=date;host&q-url-param-list=acl&q-signature=24b9d377eac860917a33c8c298042ce5b1a5****
Connection: close
```

#### 응답

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1035
Connection: close
Date: Mon, 17 Jun 2019 08:37:36 GMT
Server: tencent-cos
x-cos-request-id: NWQwNzUxNTBfMzdiMDJhMDlfOWM0Nl85NDFk****

<AccessControlPolicy>
	<Owner>
		<ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>qcs::cam::uin/100000000001:uin/100000000001</DisplayName>
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
				<DisplayName>qcs::cam::uin/100000000002:uin/100000000002</DisplayName>
			</Grantee>
			<Permission>WRITE</Permission>
		</Grant>
		<Grant>
			<Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
				<ID>qcs::cam::uin/100000000002:uin/100000000002</ID>
				<DisplayName>qcs::cam::uin/100000000002:uin/100000000002</DisplayName>
			</Grantee>
			<Permission>READ_ACP</Permission>
		</Grant>
	</AccessControlList>
</AccessControlPolicy>
```
