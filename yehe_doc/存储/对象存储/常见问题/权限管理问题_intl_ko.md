## 키 관련 문제

### APPID, SecretId, SecretKey 등 키 정보는 어떻게 확인하나요?

버킷 이름의 후반부는 APPID입니다. [COS 콘솔](https://console.cloud.tencent.com/cos5/bucket)에 로그인하면 볼 수 있습니다. SecretId, SecretKey 등의 정보를 보려면 CAM 콘솔에 로그인하여 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지로 이동하십시오.

### 임시 키의 유효 기간은 얼마나 되나요?

임시 키는 현재 루트 계정 최장 2시간(7200초), 서브 계정 최장 36시간(129600초)이며, 기본값은 30분(1800초)입니다. 임시 키 만료 후, 만료된 임시 키가 있는 요청은 거부됩니다. 임시 키 관련 소개는 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.

### SecretId, SecretKey 등과 같은 키 정보가 손상된 경우 어떻게 해야 합니까?

손상된 키를 삭제하고 새로운 키를 생성할 수 있습니다. 자세한 내용은 [Access Key](https://www.tencentcloud.com/document/product/598/34227)를 참고하십시오.

### 개인 읽기/쓰기 파일에 대한 시간 제한 액세스 URL을 생성하려면 어떻게 해야 합니까?

[임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048) 문서를 참고하여 키 유효기간을 설정하십시오.

## 권한 관련 문제

### COS에서 서브 계정에 특정 폴더에 액세스할 수 있는 권한을 부여하는 방법은 무엇인가요?

[폴더 권한 설정](https://intl.cloud.tencent.com/document/product/436/35261)을 참고하여 서브 계정에 지정 폴더 액세스 권한을 부여할 수 있습니다. 서브 계정에 고급 권한을 부여하려는 경우 [권한 설정 관련 사례](https://intl.cloud.tencent.com/document/product/436/12514)를 참고하십시오.

### COS가 403 오류를 반환합니다. 어떻게 해야 하나요?

COS 팀에서 제공하는 [진단 툴](https://console.cloud.tencent.com/cos/diagnose/)을 사용할 수 있습니다. 진단 툴은 RequestId를 사용하여 오류를 진단할 수 있습니다.

1. BucketName, APPID, Region, SecretId, SecretKey 등의 구성이 올바른지 확인합니다.
2. 상기 정보가 정확하다는 전제 하에 서브 계정 운영 여부를 확인하고, 서브 계정을 사용하는 경우에는 루트 계정이 서브 계정에 권한을 부여했는지 확인하십시오. 그렇지 않으면, 먼저 루트 계정에 로그인하여 권한을 부여하십시오.
3. 권한 부여 관련 자세한 내용은 [권한 설정 관련 사례](https://intl.cloud.tencent.com/document/product/436/12514)를 참고하십시오.
4. 임시 키를 사용하여 작업하는 경우 임시 키를 얻을 때 현재 작업이 Policy 설정에 있는지 확인하십시오. 그렇지 않다면 관련 Policy 설정을 수정하십시오.

### AccessDenied가 보고되면 어떻게 해야 합니까?

대부분의 경우 AccessDenied 오류는 무단 액세스 또는 권한 부족으로 인해 보고됩니다. 다음과 같이 문제를 해결할 수 있습니다.

1. BucketName, APPID, Region, SecretId, SecretKey 등의 구성이 올바른지 확인합니다. 공백이 있는지 여부도 확인해야 합니다.
2. 상기 설정이 맞다면 서브 계정으로 동작하는지 확인합니다. 그렇다면 서브 계정이 루트 계정에 의해 승인되었는지 확인하십시오. 아직 인증되지 않은 경우 루트 계정을 사용하여 로그인하여 서브 계정을 인증합니다. 권한에 대한 자세한 내용은 [권한 설정 관련 사례](https://intl.cloud.tencent.com/document/product/436/12514)를 참고하십시오.
3. 임시 키를 사용한 경우 현재 작업이 임시 키를 획득할 때 설정한 Policy에 부합하는지 확인하고, 부합하지 않으면 관련 Policy 설정을 변경합니다. 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.

COS 팀은 RequestId를 사용하여 오류를 해결하는 [진단 툴](https://console.cloud.tencent.com/cos/diagnose/)을 제공합니다.

### 버킷 권한 수가 상한에 도달하면 어떻게 해야 하나요?

각 루트 계정(즉, 각 APPID)에는 최대 1000개의 버킷 ACL이 있을 수 있습니다. 더 많은 버킷 ACL이 구성된 경우 오류가 보고됩니다. 따라서 불필요한 ACL은 삭제하는 것이 좋습니다.

>? 파일 레벨별 ACL 또는 Policy 사용은 권장하지 않습니다. API 또는 SDK 호출 시 파일에 특별한 ACL 제어가 필요 없는 경우, ACL 관련 매개변수(예: x-cos-acl, ACL 등)는 비워 놓고 버킷 권한 상속을 유지하는 것을 권장합니다.
>

### 버킷 생성 중에 오류가 보고되면 어떻게 해야 하나요?

버킷 생성 오류의 가능한 원인:
1. 동일한 이름의 버킷이 이미 존재합니다. 이 경우 버킷 이름을 다르게 지정해야 합니다.
2. 너무 많은 기존 버킷에 대해 공개 읽기/개인 쓰기 또는 공개 읽기/쓰기 권한이 설정되었으며 루트 계정에 대한 최대 ACL 규칙 수에 도달했습니다. 버킷을 생성할 때 이 최대 수를 조정할 수 없기 때문에 오류가 보고됩니다.

참고할 수 있는 두 가지 솔루션을 제공합니다.

솔루션1: 기존 버킷의 액세스 권한을 비공개 읽기/쓰기로 설정하고 버킷을 다시 생성해 보십시오. 자세한 내용은 [액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13315)을 참고하십시오.
솔루션2: **Policy 권한 설정**에서 **정책을 추가**하여 해당 액세스 권한을 설정할 수 있습니다. 자세한 내용은 [버킷 정책 추가](https://intl.cloud.tencent.com/document/product/436/30927)를 참고하십시오.


### 서명이 만료된 서명된 URL을 사용하여 공개 읽기 파일에 액세스할 수 있습니까?

만료된 서명된 URL을 사용하여 공개 읽기 파일에 액세스하는 경우 COS는 먼저 권한을 확인합니다. URL이 만료된 경우 액세스가 거부됩니다.

### 업로드, 다운로드 또는 기타 작업 중에 '403 Forbidden' 또는 '권한 거부됨'이 보고되면 어떻게 해야 하나요?

다음과 같이 문제를 해결할 수 있습니다.

1. BucketName, APPID, Region, SecretId, SecretKey 등의 구성이 올바른지 확인합니다.
2. 상기 설정이 맞다면 서브 계정으로 동작하는지 확인합니다. 그렇다면 서브 계정이 루트 계정에 의해 승인되었는지 확인하십시오. 아직 인증되지 않은 경우 루트 계정을 사용하여 로그인하여 서브 계정을 인증합니다. 권한에 대한 자세한 내용은 [권한 설정 관련 사례](https://intl.cloud.tencent.com/document/product/436/12514)를 참고하십시오.
3. 임시 키를 사용한 경우 현재 작업이 임시 키를 획득할 때 설정한 Policy에 부합하는지 확인하고, 부합하지 않으면 관련 Policy 설정을 변경합니다. 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.

COS 팀은 RequestId를 사용하여 오류를 해결하는 [진단 툴](https://console.cloud.tencent.com/cos/diagnose/)을 제공합니다.

### 사용자가 COS 데이터를 다운로드하지 못하게 하려면 어떻게 해야 합니까?

다음과 같이 사용 사례에 따라 사용자가 데이터를 다운로드하지 못하도록 방지할 수 있습니다.

1. 서브 계정의 데이터 다운로드를 제한하려면 [서브 계정에 COS 액세스 권한 부여](https://intl.cloud.tencent.com/document/product/436/11714)를 참고하십시오.
2. 익명 사용자의 데이터 다운로드를 제한하려면, 버킷을 개인 읽기/쓰기로 설정하거나 버킷 정책에서 `deny anyone Get Object` 작업을 설정할 수 있습니다.

### 다른 루트 계정의 서브 계정에 어떻게 권한을 부여할 수 있나요?

루트 계정 A의 버킷에서 루트 계정 B의 서브 계정 B0에 작업 권한을 부여한다고 가정합니다. 사용자는 먼저 루트 계정 B에게 A에게 있는 버킷을 작업할 권한을 부여한 후, 루트 계정 B를 통해 서브 계정 B0에 A에게 있는 버킷을 작업할 권한을 부여해야 합니다. 자세한 내용은 [기타 루트 계정의 서브 계정에 관련 버킷 작업 권한 부여](https://intl.cloud.tencent.com/document/product/436/32971)를 참고하십시오.

### 서브 계정/협업 파트너가 파일을 업로드만 가능하고 삭제는 불가능하도록 하려면 어떻게 해야 하나요?

[CAM 콘솔](https://console.cloud.tencent.com/cam/policy)을 통해 사용자 정의 정책을 생성하여 서브 계정에 특정 권한을 설정할 수 있습니다. 작업 절차에 대한 자세한 내용은 [Creating Custom Policy](https://intl.cloud.tencent.com/document/product/598/35596)를 참고하십시오.

>? 사용자 정의 정책을 생성할 때 읽기 권한을 부여하고 쓰기 작업에 대해서만 업로드를 설정하고 **삭제 권한을 부여하지 마십시오**.
>
![](https://main.qcloudimg.com/raw/578ae1960f7f8b182503cef5653dc829.png)

### 기본 도메인 이름을 사용하여 공개 읽기 버킷에 액세스할 때 반환된 파일 목록을 숨기려면 어떻게 해야 합니까?

아래 단계에 따라 버킷에 대한 deny someone 의 Get Bucket 작업 권한을 설정할 수 있습니다.

[COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하여 버킷 리스트를 클릭하고 원하는 버킷을 클릭한 후 **권한 관리**를 선택합니다.

#### 방법 1:

1. **Policy 권한 설정**을 클릭합니다. 그런 다음 **비주얼 편집기**에서 **정책 추가**를 클릭합니다.
2. 아래와 같이 권한을 설정한 후 **확인**을 클릭합니다.
   ![Policy 비주얼 편집기](https://main.qcloudimg.com/raw/60e17e3473bfb309376a6e54327a41b0.png)

#### 방법 2:

**Policy 권한 설정**을 클릭합니다. 그 다음 **JSON > 편집**을 클릭하고 다음 코드를 입력합니다.

```
{
 "Statement":[
   {
     "Action":[
       "name/cos:GetBucket",
       "name/cos:GetBucketObjectVersions"
     ],
     "Effect": "Deny",
     "Principal":{
       "qcs":[
         "qcs::cam::anyone:anyone"
       ]
     },
     "Resource":[
       "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"
     ]
   }
 ],
 "version": "2.0"
}
```

>! `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*`의 관련 정보를 다음과 같이 변경합니다.
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

서브 계정에 특정 버킷에 대한 액세스 권한을 부여하려면 루트 계정이 있는 서브 계정에 대한 버킷 정책을 추가할 수 있습니다. 자세한 내용은 [버킷 정책 추가](https://intl.cloud.tencent.com/document/product/436/30927)를 참고하십시오.


## Ranger 인증 및 검증

자세한 내용은 [FAQ](https://intl.cloud.tencent.com/document/product/1106/41958)를 참고하십시오.

## 기타 문제

### COS 리소스에 정상적으로 액세스할 수 없으면 어떻게 해야 합니까?

[리소스 액세스 오류](https://www.tencentcloud.com/document/product/436/40167)를 참고하여 문제를 해결할 수 있습니다.

### CDN 도메인을 사용하여 COS에 액세스할 때 HTTP ERROR 403이 반환되면 어떻게 해야 합니까?

이는 일반적으로 CDN 가속 도메인의 비활성화 상태가 원인일 수 있습니다. [CDN 도메인으로 COS 액세스 시 HTTP ERROR 403 반환](https://intl.cloud.tencent.com/document/product/436/40175)을 참고하여 문제를 해결할 수 있습니다.

### CDN 도메인 이름을 사용하여 COS에 액세스하지만 파일의 이전 버전에만 액세스하는 경우 어떻게 해야 합니까?

이는 일반적으로 기존 캐시 때문입니다. [URL이 잘못된 파일로 연결되는 오류](https://intl.cloud.tencent.com/document/product/436/40170)를 참고하여 문제를 해결할 수 있습니다.

### 프런트 엔드에서 CDN 및 임시 키를 사용하여 COS에 액세스할 수 있습니까?

개인 읽기/쓰기로 설정된 파일을 사용하여 CDN이 COS에서 가져올 때 인증이 필요한 경우 [CDN 가속 구성](https://intl.cloud.tencent.com/document/product/436/18670)을 참고하십시오.
