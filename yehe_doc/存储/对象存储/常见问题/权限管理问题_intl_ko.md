## 키 관련 문제

### APPID, SecretId, SecretKey 등 키 정보는 어떻게 확인하나요?

버킷 이름의 뒷부분이 APPID 정보입니다. [COS 콘솔](https://console.cloud.tencent.com/cos5/bucket)에 로그인하여 확인할 수 있습니다. SecretId, SecretKey 등의 정보는 CAM 콘솔에 로그인하여 [API 키 관리](https://console.cloud.tencent.com/cam/capi)에서 확인할 수 있습니다.

### 임시 키의 유효 기간은 얼마나 되나요?

임시 키는 현재 루트 계정 최장 2시간(7200초), 서브 계정 최장 36시간(129600초)이며, 기본값은 30분(1800초)입니다. 임시 키 만료 후, 만료된 임시 키가 있는 요청은 거부됩니다. 임시 키 관련 소개는 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.

### SecretId, SecretKey 등과 같은 키 관련 정보가 유출된 경우 어떻게 해야 하나요?

유출된 키를 삭제하고 새로운 키를 생성할 수 있습니다. 자세한 내용은 [액세스 키](https://intl.cloud.tencent.com/document/product/598/34227)를 참고하십시오.

### 개인 읽기/쓰기 파일에 유효기간이 있는 액세스 링크는 어떻게 생성하나요?

[임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048) 문서를 참고하여 키 유효기간을 설정하십시오.

## 권한 관련 문제

### COS에서 서브 계정에 특정 폴더에 액세스할 수 있는 권한을 부여하는 방법은 무엇인가요?

[폴더 권한 설정](https://intl.cloud.tencent.com/document/product/436/35261)을 참고하여 서브 계정에 지정 폴더 액세스 권한을 부여할 수 있습니다. 서브 계정에 고급 권한을 부여하려는 경우, 문서 [권한 설정 관련 사례](https://intl.cloud.tencent.com/document/product/436/12514)를 참고하십시오.



### COS에서 AccessDenied 오류를 보고합니다. 어떻게 처리해야 하나요?

AccessDenied는 일반적으로 아직 권한이 없어서 보고되는 오류입니다. 다음 순서에 따라 문제를 진단하십시오.

1. BucketName, APPID, Region, SecretId, SecretKey 등의 정보가 정확하게 설정되어 있는지 확인합니다. 특히 빈 칸이 있는지 확인하십시오.
2. 위의 정보가 정확하다는 전제 하에 서브 계정을 사용하여 작업했는지 확인합니다. 서브 계정을 사용한 경우 루트 계정에서 서브 계정에 권한을 부여했는지 확인합니다. 권한을 부여하지 않은 경우 먼저 루트 계정으로 로그인하여 서브 계정에 권한을 부여합니다. 권한 부여 방법은 [CAM 권한 설정 관련 사례](https://intl.cloud.tencent.com/document/product/436/12514)를 참고하십시오.
3. 임시 키를 사용한 경우 현재 작업이 임시 키를 획득할 때 설정한 Policy에 부합하는지 확인하고, 부합하지 않으면 관련 Policy 설정을 변경합니다. 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.


### 버킷 액세스 권한이 최대 제한에 도달했습니다. 어떻게 해야 하나요?

루트 계정당(동일한 APPID) 버킷 ACL 규칙 수는 최대 1000개입니다. 설정한 버킷 ACL 수가 1000개를 초과하는 경우 해당 오류가 발생하므로 사용하지 않는 ACL 규칙을 삭제하시기 바랍니다.

>?파일 레벨별 ACL 또는 Policy 사용은 권장하지 않습니다. API 또는 SDK 호출 시 파일에 특별한 ACL 제어가 필요 없는 경우, ACL 관련 매개변수(예: x-cos-acl, ACL 등)는 비워 놓고 버킷 권한 상속을 유지하는 것을 권장합니다.

### 버킷 생성 시, 권한 설정이 올바르지 않다는 오류 메시지가 발생합니다. 어떻게 해야 하나요?

버킷에 공개 읽기/개인 쓰기 또는 공개 읽기/쓰기 권한을 설정하면 해당 권한은 루트 계정의 ACL 규칙 수를 차지합니다. 루트 계정의 ACL 규칙 수가 최댓값에 도달했고 관련 값을 조정할 수 없는 경우 오류 메시지가 발생할 수 있습니다. 

다음 2가지 솔루션을 참고하시기 바랍니다. 

솔루션 1: 버킷의 액세스 권한을 개인 읽기로 수정할 수 있습니다. 자세한 내용은 [버킷 액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13315)을 참고하십시오.
솔루션 2: [Policy 권한 설정]의 [정책 추가]에 상응하는 액세스 권한을 설정할 수 있습니다. 자세한 내용은 [버킷 정책 추가](https://intl.cloud.tencent.com/document/product/436/30927)를 참고하십시오.


### 서명 링크를 사용하여 공개 읽기 파일에 액세스하는 경우, 서명이 만료되어도 파일에 액세스할 수 있나요?

만료된 서명 링크로 공개 읽기 파일에 액세스하는 경우, COS는 권한 현황 검증을 통해 링크가 만료되었다고 판단하면 액세스를 거부하게 됩니다.

### 업로드 및 다운로드 시 '403 Forbidden', '권한 거부' 등 오류가 발생합니다. 어떻게 처리해야 하나요?

다음 순서에 따라 문제를 진단하십시오.

1. BucketName, APPID, Region, SecretId, SecretKey 등의 정보가 정확하게 설정되어 있는지 확인합니다.
2. 위의 정보가 정확하다는 전제 하에 서브 계정을 사용하여 작업했는지 확인합니다. 서브 계정을 사용한 경우 루트 계정에서 서브 계정에 권한을 부여했는지 확인합니다. 권한을 부여하지 않은 경우 먼저 루트 계정으로 로그인하여 서브 계정에 권한을 부여합니다. 권한 부여 방법은 [CAM 권한 설정 관련 사례](https://intl.cloud.tencent.com/document/product/436/12514)를 참고하십시오.
3. 임시 키를 사용한 경우 현재 작업이 임시 키를 획득할 때 설정한 Policy에 부합하는지 확인하고, 부합하지 않으면 관련 Policy 설정을 변경합니다. 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.


### COS에서 다른 사람이 로컬에 파일을 다운로드하는 것을 어떻게 제한하나요?

다른 사람이 로컬에 파일을 다운로드하는 것을 제한하려면 다음 몇 가지 시나리오를 구분해야 합니다.

1. 서브 계정의 데이터 다운로드를 제한하려면 [서브 계정에 COS 액세스 권한 부여](https://intl.cloud.tencent.com/document/product/436/11714)를 참고하십시오.
2. 익명 사용자의 데이터 다운로드를 제한하려면, 버킷을 개인 읽기/쓰기로 설정하거나 버킷 정책에서 `deny anyone Get Object` 작업을 설정할 수 있습니다.

### COS에서 기타 계정의 서브 계정에 어떻게 권한을 설정하나요?

루트 계정 A의 버킷에서 루트 계정 B의 서브 계정 B0에 작업 권한을 부여한다고 가정합니다. 사용자는 먼저 루트 계정 B에게 A에게 있는 버킷을 작업할 권한을 부여한 후, 루트 계정 B를 통해 서브 계정 B0에 A에게 있는 버킷을 작업할 권한을 부여해야 합니다. 자세한 내용은 [기타 루트 계정의 서브 계정에 관련 버킷 작업 권한 부여](https://intl.cloud.tencent.com/document/product/436/32971)를 참고하십시오.

### COS에서 서브 계정/협업 파트너가 파일을 삭제하지 못하고 업로드만 할 수 있도록 어떻게 설정하나요?

[CAM 콘솔](https://console.cloud.tencent.com/cam/policy)을 통해 사용자 정의 정책을 생성하여 서브 계정에 특정 권한을 설정할 수 있습니다. 작업 절차에 대한 자세한 내용은 [사용자 정의 정책 생성](https://intl.cloud.tencent.com/document/product/598/35596)을 참고하십시오.

>? 사용자 정의 정책을 생성할 때 읽기 작업 권한을 부여해야 합니다. 쓰기 작업에서는 업로드 권한만 선택합니다. **관련 권한 삭제를 선택하지 마십시오**.
>
![](https://main.qcloudimg.com/raw/578ae1960f7f8b182503cef5653dc829.png)

### 버킷의 기본 도메인을 사용한 공개 읽기 버킷 액세스 시 파일 리스트가 반환됩니다. 파일 리스트 정보를 숨기려면 어떻게 해야 하나요?

해당 버킷에 deny anyone의 Get Bucket 권한을 설정하면 됩니다. 작업 방법은 다음과 같습니다.

[COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인한 후 버킷 리스트를 선택해 해당 버킷의 **권한 관리** 페이지로 이동합니다.

#### 방법 1:

1. **Policy 권한 설정 항목**을 찾아 [그래픽 설정]에서 [정책 추가]를 클릭합니다.
2. 다음 이미지와 같이 해당 작업 권한을 추가하고 [확인]을 클릭해 저장합니다.
   ![Policy 그래픽 설정](https://main.qcloudimg.com/raw/60e17e3473bfb309376a6e54327a41b0.png)

#### 방법 2:

**Policy 권한 설정 항목**을 찾아 [정책 구문]>[편집]을 클릭하고 다음 표현식을 입력합니다.

```
{
 "Statement": [
   {
     "Action": [
       "name/cos:GetBucket",
       "name/cos:GetBucketObjectVersions"
     ],
     "Effect": "Deny",
     "Principal": {
       "qcs": [
         "qcs::cam::anyone:anyone"
       ]
     },
     "Resource": [
       "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"
     ]
   }
 ],
 "version": "2.0"
}
```

>!
>`qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`의 관련 정보를 다음과 같이 변경합니다.
>
> - 'ap-beijing'을 사용자의 버킷 리전으로 변경합니다.
> - '1250000000'을 사용자의 APPID 정보로 변경합니다.
> - 'examplebucket-1250000000'을 사용자의 버킷 이름으로 변경합니다.
>
> 버킷 이름의 뒷부분이 APPID입니다. [COS 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 버킷 이름을 확인할 수 있습니다.

### COS의 ACL 제한 타깃은 버킷인가요, 아니면 계정인가요? 파일 업로드 시 권한을 지정할 수 있나요?

계정에 대한 ACL 제한입니다. 파일 레벨별 ACL 또는 Policy 사용은 권장하지 않습니다. API 또는 SDK 호출 시 파일에 특별한 ACL 제어가 필요 없는 경우 ACL 관련 매개변수(예: x-cos-acl, ACL 등)는 비워 놓고 버킷 권한 상속을 유지하는 것을 권장합니다.

### 협업 파트너에게 지정된 버킷의 액세스 권한을 어떻게 부여하나요?

협업 파트너 계정은 일종의 특수 서브 계정입니다. 자세한 내용은 [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023)를 참고하십시오.

### 여러 비즈니스에서 버킷 작업이 필요한 경우, 버킷 또는 다른 차원으로 권한을 격리할 수 있나요?

[CAM 콘솔](https://console.cloud.tencent.com/cam/overview)에 로그인한 후 사용자 관리 페이지로 이동해 비즈니스별로 서브 계정을 활성화하고 각각의 권한을 부여할 수 있습니다.

### 자회사 또는 직원에게 서브 계정을 생성하고 특정 버킷의 액세스 권한을 부여하는 방법은 무엇인가요?

자세한 내용은 [서브 계정에 COS 액세스 권한 부여](https://intl.cloud.tencent.com/document/product/436/11714)를 참고하여 서브 계정을 생성하고 권한을 부여하십시오.

### 일부 특정 서브 계정에 특정 버킷에 대해서만 작업 권한을 부여하려는 경우 어떻게 해야 하나요?

서브 계정에 특정 버킷에 대해서만 작업 권한을 부여하려는 경우 서브 계정을 사용해 경로를 추가할 수 있습니다. 자세한 내용은 [서브 계정으로 버킷 리스트 액세스](https://intl.cloud.tencent.com/document/product/436/17061)를 참고하십시오.

## 기타 문제

### COS 리소스 액세스 오류는 어떻게 처리하나요?

[리소스 액세스 오류](https://intl.cloud.tencent.com/document/product/436/40167) 문서를 참고하여 진단 및 처리하십시오.

### CDN 도메인으로 COS 액세스 시 HTTP ERROR 403가 반환됩니다. 어떻게 처리해야 하나요?

CDN 가속 도메인의 비활성화 상태가 원인일 수 있습니다. [CDN 도메인으로 COS 액세스 시 HTTP ERROR 403 반환](https://intl.cloud.tencent.com/document/product/436/40175) 문서를 참고하여 처리하십시오.

### CDN 도메인으로 COS 액세스 시 이전 파일로 액세스됩니다. 어떻게 처리해야 하나요?

캐시가 원인일 수 있습니다. [동일 링크 액세스 시 파일 오류](https://intl.cloud.tencent.com/document/product/436/40170) 문서를 참고하십시오.

### 프런트 엔드 작업은 CDN과 임시 키 방식으로 COS의 콘텐츠에 액세스할 수 있나요?

COS 개인 읽기/쓰기 상황에서 CDN Origin-pull COS 인증을 구현해야 할 경우 [CDN Origin-pull 인증](https://intl.cloud.tencent.com/document/product/436/18670)을 참고하십시오.
