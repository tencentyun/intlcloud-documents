Tencent Cloud 루트 계정은 [CAM(Cloud Access Management)](https://console.cloud.tencent.com/cam/overview) 콘솔에서 CAM 사용자를 생성하고 정책을 연결하여 CAM 사용자에게 Tencent Cloud 리소스 사용 권한을 부여할 수 있습니다.

## 개요

사용자는 [CAM](https://intl.cloud.tencent.com/document/product/598/10583)에서 루트 계정에 속한 다양한 유형의 사용자에게 여러 가지 권한을 부여할 수 있습니다. 이러한 권한은 액세스 정책 언어로 설명되고 사용자를 시작점으로 권한이 부여되므로 **사용자 정책**이라고 합니다.

#### 사용자 정책과 버킷 정책의 차이점

사용자 정책과 버킷 정책의 가장 큰 차이점은 사용자 정책은 효력(Effect), 작업(Action), 리소스(Resource), 조건(Conditon, 옵션)만 설명하며 자격(Principal)은 설명하지 않는다는 점입니다. 이 때문에 사용자 정책 작성이 완료되면 다시 서브 계정, 사용자 그룹 또는 역할 관련 작업을 실행해야 합니다. 따라서 사용자 정책의 사용 방법은 다음과 같습니다.
- 사용자 정책 작성이 완료된 후, 서브 계정, 사용자 그룹 또는 역할에 대한 관련 작업을 수행합니다.
- 사용자 정책은 **익명 사용자에게 작업 및 리소스 권한 부여를 지원하지 않습니다**.

#### 사전 설정 정책 및 사용자 정의 정책

사용자 정책에는 [사전 설정 정책 및 사용자 정의 정책](https://intl.cloud.tencent.com/document/product/598/10601)의 두 가지 유형이 있으며, [연결 인증을 위한 사전 설정 정책](https://intl.cloud.tencent.com/document/product/598/10602)을 사용하거나 [직접 사용자 정책 작성](https://intl.cloud.tencent.com/document/product/598/35596) 후 연결 인증을 수행할 수도 있습니다. 자세한 내용은 CAM의 [인증 가이드](https://intl.cloud.tencent.com/document/product/598/32668)를 참고하십시오.

## 적용 시나리오
사용자가 무엇을 할 수 있는지 궁금하거나 사용자 정책을 추천할 때, CAM 사용자를 찾고 그들이 속한 사용자 그룹의 권한을 확인하여 사용자가 할 수 있는 일을 알아보십시오. 권장 시나리오는 다음과 같습니다.
- 버킷 생성(PutBucket) 및 버킷 나열(GetService)과 같은 COS(Cloud Object Storage) 서비스 수준 권한을 설정합니다.
- 루트 계정의 모든 COS 버킷 및 객체를 사용해야 합니다.
- 루트 계정의 다수의 CAM 사용자에게 동일한 권한을 부여합니다.

## 사용자 정책 구문

### 정책 구문

버킷 정책과 마찬가지로 사용자 정책은 JSON 언어로 설명되며 [액세스 정책 언어](https://intl.cloud.tencent.com/document/product/436/18023)의 통합 표준(위탁자, 효과, 작업, 리소스, 조건 등)을 따릅니다. 그러나 사용자 정책은 사용자/사용자 그룹에 직접 연결되므로 사용자 정책은 위탁자(Principal)를 입력할 필요가 없습니다.

다음 표에서는 사용자 정책과 버킷 정책 간의 차이점 비교입니다.

| 요소|사용자 정책 |버킷 정책 |
|---|---|---|
|위탁자 |**입력하지 않음**|필수 입력|
|효과 |필수 입력 |필수 입력 |
|작업 |필수 입력 |필수 입력 |
|리소스 |필수 입력 |**버킷 리소스**|
|조건 |옵션 |옵션 |

### 정책 예시

다음은 다음은 일반적인 사용자 정책의 예시이며, 정책의 의미는 광저우에 위치한 버킷 examplebucket-1250000000의 모든 COS 작업에 권한 위임을 한 정책입니다. 정책을 저장한 후 [CAM](https://intl.cloud.tencent.com/document/product/598/10583)의 서브 계정, 사용자 그룹 또는 적용 가능한 역할과 연결해야 합니다.

```
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["cos:*"],
      "Resource": [
          "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*",
          "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ],
  "Version": "2.0"
}
```

## 사용자 정책을 통해 서브 계정에 COS 액세스 인증

### 전제 조건

CAM 서브 계정이 생성되어야 합니다. 생성 방법은 [서브 계정 생성](https://intl.cloud.tencent.com/document/product/436/11714)을 참고하십시오.

<span id="사용자 정의 정책"></span>
### 설정 단계

CAM은 [사전 설정 정책 및 사용자 정의 정책](https://intl.cloud.tencent.com/document/product/598/10601)을 제공합니다. 사전 설정 정책은 CAM에서 제공하는 시스템 사전 설정 정책으로, COS 관련 정책은 [사전 설정 정책](#사전 설정 정책)을 참고하십시오. 사용자 정의 정책은 사용자 정의 리소스, 작업 등 요소를 지원하여 보다 효율적으로 만듭니다. 서브 계정을 인증하는 사용자 정의 정책 생성 방법은 다음과 같습니다.

1. [CAM 콘솔](https://console.cloud.tencent.com/cam)에 로그인합니다.
2. **정책 > 사용자 정의 정책 생성 > 정책 구문 생성**을 선택하여 정책 생성 페이지로 이동합니다.
3. **빈 템플릿**을 선택하여 실제 필요에 따라 인증 정책을 사용자 정의하거나 COS와 연결된 **시스템 템플릿**을 선택할 수 있습니다. 다음은 **빈 템플릿**을 선택하는 예시입니다.

4. **빈 템플릿**을 선택하여 정책 구문을 입력합니다.다음과 같은 기본 요소가 포함되어야 합니다.
 - **resource: 권한 부여 리소스**.
     - 모든 리소스(`"*"`)
     - 버킷 지정(`"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"`)
     - 버킷의 지정된 디렉터리 또는 객체(`"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/test/*"`)
 - **action: 권한 부여 작업**.
 - **effect: 효력**. `"allow"`(허용) 또는`"deny"`(거절)을 선택합니다.
 - **condition: 적용 조건**. 옵션 항목.

 COS는 사용자 정책의 예시를 제공하고 있으며, 다음 문서를 참고하여 정책 콘텐츠를 직접 복사하여 **정책 콘텐츠** 편집 상자에 붙여넣을 수 있습니다. 입력이 올바른지 확인한 후 **완료**를 클릭하십시오.
 - [서브 계정 COS 액세스 인증](https://intl.cloud.tencent.com/document/product/436/11714)
 - [COS API 인증 정책 사용 가이드](https://intl.cloud.tencent.com/document/product/436/30580)
5. 생성이 완료되면 [CAM 콘솔](https://console.cloud.tencent.com/cam)의 **정책 > 사용자 정의 정책**에서 생성된 사용자 정의 정책을 확인하고 정책을 서브 계정과 연결할 수 있습니다.

6. 서브 계정을 선택하고 **확인**을 클릭해 권한을 부여하면, 서브 계정을 이용해 한정된 COS 리소스에 액세스할 수 있습니다.


<span id="사전 설정 정책"></span>
## 사전 설정 정책
1. CAM은 몇 가지 사전 설정 정책을 제공합니다. [CAM 콘솔](https://console.cloud.tencent.com/cam)의 **정책 > 사전 설정 정책**에서 ‘COS’를 검색하여 필터링할 수 있습니다.


2. 정책 이름을 클릭하고 **정책 구문 > JSON**으로 이동하여 특정 정책 콘텐츠를 확인합니다. 사전 설정된 정책의 리소스(`resource`)는 COS의 모든 리소스(`"*"`)로 설정되며 수정은 지원되지 않습니다. 일부 COS 버킷 및 객체에 인증을 부여해야 하는 경우 JSON 사전 설정 정책을 복사하여 [사용자 정의 정책](#사용자 정의 정책)을 생성할 수 있습니다.



표1과 표2는 CAM에서 제공하는 COS 관련 사전 설정 정책 및 설명을 나열합니다.

**표1: COS 사전 설정 정책**

<table>
<tr>
	<th>사전 설정 정책</th>
	<th>설명</th>
	<th>JSON 정책</th>
</tr>
<tr>
	<td>QcloudCOS<br>Bucket<br>ConfigRead</td>
	<td>이 권한이 있는 사용자는 COS 버킷 설정 읽기 가능</td>
	<td>
	<pre>
	<code>
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:GetBucket*",
                "cos:HeadBucket"
            ],
            "resource": "*"
        }
    ]
}
	</code>
	</pre>
	</td>
</tr>
<tr>
	<td>QcloudCOS<br>Bucket<br>ConfigWrite</td>
	<td>이 권한이 있는 사용자는 COS 버킷 설정 수정 가능</td>
	<td>
	<pre>
	<code>
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:PutBucket*"
            ],
            "resource": "*"
        }
    ]
}
	</code>
	</pre>
	</td>
</tr>
<tr>
	<td>QcloudCOS<br>Data<br>FullControl</td>
	<td>COS 버킷의 데이터 읽기, 쓰기, 삭제 및 나열할 수 있는 액세스 권한 포함</td>
	<td>
	<pre>
	<code>
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:GetService",
                "cos:GetBucket",
                "cos:ListMultipartUploads",
                "cos:GetObject*",
                "cos:HeadObject",
                "cos:GetBucketObjectVersions",
                "cos:OptionsObject",
                "cos:ListParts",
                "cos:DeleteObject",
                "cos:PostObject",
                "cos:PostObjectRestore",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload",
                "cos:DeleteMultipleObjects",
                "cos:AppendObject"
            ],
            "resource": "*"
        }
    ]
}
	</code>
	</pre>
	</td>
</tr>

</table>

**표2: COS 작업과 사전 설정 정책 간의 관계**

|설명 |작업 |QcloudCOS<br>Bucket<br>ConfigRead |QcloudCOS<br>Bucket<br>ConfigWrite |QcloudCOS<br>Data<br>FullControl |QcloudCOS<br>Data<br>ReadOnly |QcloudCOS<br>Data<br>WriteOnly |QcloudCOS<br>Full<br>Access |QcloudCOS<br>GetService<br>Access |QcloudCOS<br>ListOnly |QcloudCOS<br>Read<br>OnlyAccess |
|---|---|---|---|---|---|---|---|---|---|---|
|버킷 나열 |GetService |❌ |❌ |✅ |❌ |❌ |✅ |✅ |✅ |✅ |
|버킷 생성 |PutBucket |❌ |✅ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
|버킷 삭제 |DeleteBucket |❌ |❌ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
|기본 버킷 정보 가져오기 |HeadBucket |✅ |❌ |❌ |❌ |❌ |✅ |❌ |✅ |✅ |
|버킷 설정 항목 가져오기 |GetBucket* |✅ |❌ |❌ |❌ |❌ |✅ |❌ |❌ |✅ |
|버킷 설정 항목 수정 |GetBucket* |❌ |✅ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
|버킷 액세스 권한 가져오기 |GetBucketAcl |✅ |❌ |❌ |❌ |❌ |✅ |❌ |❌ |✅ |
|버킷 액세스 권한 수정 |PutBucketAcl |❌ |✅ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
|버킷의 객체 나열 |GetBucket |✅ |❌ |✅ |❌ |❌ |✅ |❌ |✅ |✅ |
|버킷의 모든 버전 객체 나열 |GetBucketObjectVersions |✅ |❌ |✅ |❌ |❌ |✅ |❌ |✅ |✅ |
|객체 업로드 |PutObject |❌ |❌ |✅ |❌ |✅ |✅ |❌ |❌ |❌ |
|멀티파트 업로드 |ListParts<br>InitiateMultipartUpload<br>UploadPart<br>UploadPartCopy<br>CompleteMultipartUpload<br>AbortMultipartUpload<br>ListMultipartUploads |❌ |❌ |✅ |❌ |✅ |✅ |❌ |❌ |❌ |
|객체 추가 |AppendObject |❌ |❌ |✅ |❌ |❌ |✅ |❌ |❌ |❌ |
|객체 다운로드 |GetObject |❌ |❌ |✅ |✅ |❌ |✅ |❌ |❌ |❌ |
|객체 메타데이터 조회 |HeadObject |❌ |❌ |✅ |✅ |❌ |✅ |❌ |❌ |✅ |
|CORS 사전 인증 |OptionsObject |❌ |❌ |✅ |✅ |❌ |✅ |❌ |❌ |✅ |


## 더 많은 사용자 정책 예시

- [COS 액세스 서브 계정 인증](https://intl.cloud.tencent.com/document/product/436/11714)
- [COS API 인증 정책 사용 가이드](https://intl.cloud.tencent.com/document/product/436/30580)

