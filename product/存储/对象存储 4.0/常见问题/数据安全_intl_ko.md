### APPID, SecretId 및 SecretKey 등 키 정보는 어디에서 조회할 수 있니까?

버킷 이름의 후반부는 APPID 정보이며 [COS 콘솔](https://console.cloud.tencent.com/cos5/bucket)에 로그인하여 확인할 수 있습니다. SecretId 및 SecretKey와 같은 정보를 확인하려면 접근 관리 콘솔의 [API 키 관리](https://console.cloud.tencent.com/cam/capi)에 로그인하여 확인하십시오.

### 임시 키의 유효 기간은 얼마입니까?

임시 키는 최대 2 시간, 즉, 7200 초 동안 유효합니다. 임시 키에 대한 자세한 내용은 [임시 키 생성 및 사용 설명서](https://cloud.tencent.com/document/product/436/14048)를 참조하십시오.

### APPID 및 SecretId와 같은 키에 관한 정보가 누출되면 어떻게 처리해야 합니까?

누출된 키를 삭제하고 새 키를 생성할 수 있습니다. 자세한 내용은 [키 관리](https://cloud.tencent.com/document/product/436/10074)를 참조하십시오.

### COS는 파일 암호화를 지원합니까?

COS는 서버측에서 파일 암호화를 지원합니다. 자세한 내용은 [서버 암호화](https://cloud.tencent.com/document/product/436/18145)를 참조하십시오.

### COS의 표준 스토리지, 저빈도 스토리지 및 보관 스토리지 데이터에 모두 백업이 있습니까?

COS의 데이터는 다중 복제본 또는 삭제 코드 방식으로 하위 계층에 저장됩니다. 분산형 스토리지 엔진은 한 지역의 여러 가용 영역에 분산되어 있어 99.999999999 %의 신뢰성을 가지고 있습니다. 다중 복제본 및 삭제 코드 스토리지는 하위 계층 로직이며 사용자가 볼 수 없습니다.

### 동일한 계정 아래 어떤 버킷의 요청이 너무 많은 것은 다른 버킷의 접근에 영향을 미칩니까?

버킷에 대한 많은 요청은 영향을 미치지 않지만 주파수가 너무 빠르면 영향을 미칩니다. 자세한 내용은 [요청 속도 및 성능 최적화](https://cloud.tencent.com/document/product/436/13653)를 참조하십시오.

### 업로드, 다운로드 및 기타 작업을 실행할 때 "403 Forbidden" 오류가 발생하거나 권한이 거부되면 어떻게 처리해야 합니까?

아래 단계에 따라 문제를 해결하십시오.

1. BucketName, APPID, Region, SecretId, SecretKey 등 구성 정보가 정확한지 확인하십시오.
2. 위의 정보가 정확하면 서브 계정을 사용하여 조작되는지 확인하십시오. 그렇다면 서브 계정이 루트 계정에 의해 권한을 부여받았는지 확인하십시오. 그렇지 않은 경우 루트 계정에 로그인하여 서브 계정에 권한을 부여하십시오.
   권한 부여에 대한 자세한 내용은 [접근관리 권한 설정 관련 예시](https://cloud.tencent.com/document/product/436/12514)를 참조하십시오.
3. 임시 키로 조작할 경우 현재 작업은 임시 키 획득 시 설정한 정책에 있는지 확인하십시오. 그렇지 않으면 관련 정책 설정을 수정하십시오.
4. 위의 모든 단계를 완료한 후에도 문제가 지속되면 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&step=1)로 연락하십시오.

### 기본 도메인 이름을 사용하여 공개 읽기 및 비공개 쓰기 버킷에 접근할 때 버킷의 모든 파일 정보가 반환됩니다. 파일 목록 정보를 숨기려면 어떻게 해야 합니까?

다음 단계에 따라 대응 버킷을 위한 deny anyone의 Get Bucket 권한을 설정할 수 있습니다.

[COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하고 버킷 목록을 선택하여 대응 버킷의 **권한 관리** 페이지로 이동하십시오.

#### 방법 1:

1. **Policy 권한 설정 옵션**을 찾아 [도형 설정] 아래의 [정책 추가]를 한번 클릭하십시오.
2. 아래에 표시된 대로 대응 권한 설정을 추가하고 [확인]을 한번 클릭하여 저장하십시오.
   ![Polcy 도형 설정](https://main.qcloudimg.com/raw/c739d31636d117757449c7e0e106ad84.png)

#### 방법 2:

**Policy 권한 설정 옵션**을 찾아 [정책 어법]>[편집]을 한번 클릭하여 다음 식을 입력하십시오.

```
{
	"version": "2.0",
	"Statement": [{
		"Principal": {
			"qcs": [
				"qcs::cam::anyone:anyone"
			]
		},
		"Effect": "deny",
		"Action": [
			"name/cos:GetBucket"
		],
		"Resource": [
			"qcs::cos:ap-beijing:uid/125000000:testbucket-125000000/*"
		]
	}]
}
```

>
>!"qcs::cos:ap-beijing:uid/125000000:testbucket-125000000/*"에 있는 관련 정보를 다음과 같이 교체하십시오.
>- "ap-beijing"을 버킷이 위치하는 지역으로 교체하십시오.
>- "125000000"을 APPID 정보로 교체하십시오.
>- "testbucket-125000000"을 버킷 이름으로 교체하십시오.
>
> 그중, APPID는 버킷 이름의 후반 부분입니다. [COS 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 버킷 이름을 확인할 수 있습니다.

### 공동 작업자가 지정된 버킷에 접근하도록 권한을 부여하려면 어떻게 해야 합니까?

공동 작업자 계정은 일종의 특별한 서브 계정입니다. 자세한 내용은 [접근 정책 언어 개요](https://cloud.tencent.com/document/product/436/18023)를 참조하십시오.

### 여러 비즈니스가 버킷에 대해 작업을 실행할 경우 버킷 또는 기타 위도에 따라 권한을 격리할 수 있습니까?

[접근 관리 콘솔](https://console.cloud.tencent.com/cam/overview)에 로그인하여 사용자 관리 페이지에 들어가면 서로 다른 비즈니스에 대한 서브 계정을 활성화하고 서로 다른 권한을 부여할 수 있습니다

### 파일을 업로드하거나 버킷을 생성할 때 "your policy or acl has reached the limit (Status Code: 400; Error Code: PolicyFull)" 오류가 발생하면 어떻게 처리해야 합니까?

COS의 ACL + Policy 수량 제한은 1000개입니다. 관련 ACL 또는 Policy 정책이 1000보다 크게 설전하면 이 오류가 발생하므로 쓸모없는 ACL이나 Policy 정책을 삭제하는 것을 권장합니다.

>!파일 수준 ACL 또는 Policy을 사용하지 않는 것을 권장합니다. API 또는 SDK를 호출할 때 파일에 대한 특별한 ACL 제어가 필요하지 않은 경우 ACL 관련 매개변수(예: x-cos-acl, ACL 등)를 비워 두어 버킷 권한의 상속을 유지하십시오.

### 자회사 또는 직원을 위한 서브 계정을 생성하고 특정 버킷에 접근 권한을 부여하려면 어떻게 해야 합니까?

자세한 내용은 [서브 계정 접근 권한 부여 COS](https://cloud.tencent.com/document/product/436/11714)를 참조하십시오.

### 비공개 읽기/쓰기 파일에 대한 시효성 있는 접근 링크를 생성하려면 어떻게 해야 합니까?

자세한 내용은 [임시 키 생성 및 사용 설명서](https://cloud.tencent.com/document/product/436/14048) 문서를 참조하여 키의 유효 기간을 설정하십시오.

### COS의 ACL 제한은 버킷에 적용됩니까? 계정에 적용됩니까? 파일을 업로드할 때 권한을 지정할 수 있습니까?

ACL 제한은 계정에 적용됩니다. 파일을 업로드할 때 권한을 지정하지 않는 것을 권장합니다. 왜냐하면 ACL + Policy 정책 수량이 1000 개를 초과하여 오류를 발생시킬 수 있기 때문입니다.

### 특정 서브 계정이 특정 버킷에만 조작 권한을 부여하려면 어떻게 해야 합니까?

서브 계정이 특정 버킷에 대한 조작 권한을 부여하려면 서브 계정을 사용하여 경로를 추가할 수 있습니다. 자세한 내용은 [버킷 리스트 접근](https://cloud.tencent.com/document/product/436/17061)을 참조하십시오.

### 계정 A를 사용하여 계정 B에 대해 계정 A에 속한 버킷의 쓰기 권한을 부여하려면 어떻게 해야 합니까?

자세한 내용은 [ACL 접근 제어 실천](https://cloud.tencent.com/document/product/436/12470) 및 [CAM 접근 관리 실천](https://cloud.tencent.com/document/product/436/12469)을 참조하여 권한을 부여하십시오.
