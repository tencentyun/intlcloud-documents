## 개요

CAM(Cloud Access Management)을 통해 COS(Cloud Object Storage) 버킷 또는 객체에 대해 서로 다른 작업 권한을 설정할 수 있으므로 서로 다른 회사 또는 부서의 서로 다른 팀 또는 사용자가 서로 더 잘 협업할 수 있습니다.

먼저 루트 계정, 서브 계정(사용자), 사용자 그룹 등 몇 가지 핵심 개념을 이해하고 있어야 합니다. CAM과 관련된 용어 및 설정에 대한 자세한 설명은 CAM [Glossary](https://intl.cloud.tencent.com/document/product/598/18564)를 참조하십시오.

#### 루트 계정
루트 계정은 개발사라고도 합니다. 사용자가 Tencent Cloud 계정을 신청하면 시스템은 Tencent Cloud 서비스에 로그인할 루트 계정 정보를 생성합니다. 루트 계정은 Tencent Cloud 리소스의 사용 용량 계산 및 과금의 기본 주체입니다.

루트 계정은 기본적으로 해당 계정의 모든 리소스에 대해 청구서 정보 확인, 사용자 비밀번호 변경, 사용자 및 사용자 그룹 생성, 기타 클라우드 서비스 리소스 액세스 등을 포함한 완전한 액세스 권한을 보유하고 있습니다. 기본 설정 시 리소스는 루트 계정만 액세스할 수 있으며 다른 사용자는 루트 계정에서 권한을 부여해야만 액세스할 수 있습니다.

#### 서브 계정(사용자) 및 사용자 그룹
- 서브 계정은 루트 계정에서 생성하는 엔터티로, 확실한 ID 및 자격 증명을 가지고 있으며 Tencent Cloud 콘솔에 로그인할 수 있는 권한을 가지고 있습니다.
- 서브 계정은 기본적으로 리소스를 보유하고 있지 않으며, 반드시 소속된 루트 계정에서 권한을 부여해야 합니다.
 - 하나의 루트 계정은 여러 개의 서브 계정(사용자)을 생성할 수 있습니다.
 - 하나의 서브 계정은 여러 개의 루트 계정에 소속될 수 있으며, 각각의 루트 계정과 협업하여 루트 계정별 클라우드 리소스를 관리할 수 있습니다. 단, 하나의 서브 계정이 동시에 여러 루트 계정에 로그인할 수는 없으며, 하나의 루트 계정 소속으로 로그인하여 해당 루트 계정의 클라우드 리소스만 관리할 수 있습니다.
- 서브 계정은 콘솔을 통해 개발사(루트 계정)를 전환할 수 있으며, 하나의 루트 계정에서 다른 루트 계정으로 전환할 수 있습니다.
 - 서브 계정은 콘솔에 로그인할 때 자동으로 기본 루트 계정으로 전환되며, 기본 루트 계정에서 부여한 액세스 권한을 가집니다.
 - 개발사를 전환하면 서브 계정은 전환된 루트 계정이 부여한 액세스 권한을 가지며, 전환 전의 루트 계정이 부여한 액세스 권한은 즉시 효력이 사라집니다.
- 사용자 그룹은 동일한 직무의 여러 사용자(서브 계정)가 모인 집합체입니다. 업무 필요에 따라 서로 다른 사용자 그룹을 생성할 수 있으며, 사용자 그룹에 적합한 정책을 연결하여 각 권한을 할당할 수 있습니다.

## 작업 단계
서브 계정에 COS 액세스 권한을 부여하는 순서는 서브 계정 생성, 서브 계정에 권한 부여, 서브 계정으로 COS 리소스에 액세스, 해당 세 단계로 나뉩니다.

### 1단계: 서브 계정 생성
CAM 콘솔에서 서브 계정을 생성하고 액세스 권한을 설정할 수 있습니다. 자세한 작업 방법은 다음과 같습니다.
1. [CAM 콘솔](https://console.cloud.tencent.com/cam)에 로그인합니다.
2. **사용자 > 사용자 목록 > 사용자 생성**을 선택하여 사용자 생성 페이지로 이동합니다.
3. **사용자 정의 생성**을 선택하고 **리소스 액세스 및 메시지 수신**을 설정한 후 **다음**을 클릭합니다.
4. 필요에 따라 사용자 관련 정보를 입력합니다.
 - **사용자 정보**: 서브 계정의 사용자 이름(예: Sub_user) 및 이메일 주소를 설정합니다. 이메일 주소는 서브 계정을 WeChat 계정과 연결하기 위해 Tencent Cloud에서 보낸 이메일을 수신하는 데 필요합니다.
 - **액세스 방식**: 프로그래밍 액세스 및 Tencent Cloud 콘솔 액세스를 선택하고, 다른 설정은 필요에 따라 선택합니다.
4. 사용자 정보를 모두 작성한 후, **다음 단계**를 클릭하여 자격을 인증합니다.
5. 서브 계정에 권한을 부여합니다. 제공된 정책 옵션으로 서브 계정에 COS 버킷 목록에 대한 액세스 권한 또는 읽기 전용 권한을 부여하는 것과 같은 간단한 정책을 구성할 수 있습니다. 보다 복잡한 정책을 설정하려면 [2단계: 서브 계정에 권한 부여](#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E5.AF.B9.E5.AD.90.E8.B4.A6.E5.8F.B7.E6.8E.88.E4.BA.88.E6.9D.83.E9.99.90)를 진행하십시오.
6. 사용자 태그를 선택적으로 설정하고 **다음 단계**을 클릭합니다.
7. **완료**를 클릭하면 서브 계정이 생성됩니다.


<span id="서브 계정에 권한 부여"></span>
### 2단계: 서브 계정에 권한 부여


사용자 지정 정책을 생성하거나 기존 정책을 선택하고 서브 계정과 연결합니다.

1. [CAM 콘솔](https://console.cloud.tencent.com/cam)에 로그인합니다.
2. **정책 > 사용자 정의 정책 생성 > 정책 구문 생성**을 선택하여 정책 생성 페이지로 이동합니다.
3. 실제 필요에 따라 **빈 템플릿**을 선택하여 권한 부여 정책을 사용자 정의하거나 COS와 연결할 **시스템 템플릿**을 선택하고 **다음**을 클릭합니다.
4. 기억하기 쉬운 정책 이름을 입력합니다. **빈 템플릿**을 선택한 경우 정책 구문을 입력해야 합니다. 자세한 내용은 [정책 예시](#정책 예시)를 참고하십시오. 정책 내용을 복사하여 **정책 내용** 상자에 붙여넣고 입력한 정보가 정확한지 확인한 후 **완료**를 클릭합니다.
5. 생성 완료 후, 방금 생성한 정책을 서브 계정에 연결합니다.
![](https://main.qcloudimg.com/raw/1495c8b19dfff2aad622b794d8f5bc6a.png)
6. 서브 계정을 선택하고 **확인**을 클릭해 권한을 부여하면, 서브 계정을 이용해 한정된 COS 리소스에 액세스할 수 있습니다.
![](https://main.qcloudimg.com/raw/3667de5320e99321a78c5d1c22a49157.png)

### 3단계: 서브 계정으로 COS 리소스에 액세스

위 1단계에서 설정한 프로그래밍 액세스 및 Tencent Cloud 콘솔 액세스 방법을 다음과 같이 소개합니다.

(1) 프로그래밍 액세스

서브 계정을 사용하여 프로그램(예: API, SDK, 툴 등)으로 COS 리소스에 액세스할 때에는 루트 계정의 APPID와 서브 계정의 SecretId, SecretKey 정보가 필요합니다. CAM 콘솔에서 서브 계정의 SecretId와 SecretKey를 생성할 수 있습니다.

1. 루트 계정으로 [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인합니다.
2. **사용자 리스트**를 선택하여 사용자 리스트 페이지로 이동합니다.
3. 서브 계정의 사용자 이름을 클릭하여 서브 계정 정보 상세 페이지로 이동합니다.
4. **API Keys** 탭을 클릭하고 **키 생성**을 클릭하여 서브 계정에 SecretId와 SecretKey를 생성합니다.

이제 서브 계정의 SecretId와 SecretKey, 루트 계정의 APPID를 사용해 COS 리소스에 액세스할 수 있습니다. 
>!서브 계정은 XML API 또는 XML API 기반의 SDK를 통해 COS 리소스에 액세스할 수 있습니다.


#### XML 기반의 Java SDK를 통한 액세스 예시

XML 기반의 Java SDK 명령 라인 예시이며, 다음과 같이 매개변수를 입력해야 합니다.
```
// 사용자 인증 정보 초기화
COSCredentials cred = new BasicCOSCredentials("<루트 계정 APPID>", "<서브 계정 SecretId>", "<서브 계정 SecretKey>");
```

인스턴스는 다음과 같습니다.
```
String secretId = System.getenv("secretId");//서브 계정의 SecretId. 리스크를 줄이기 위해 최소 권한 원칙을 따릅니다. 서브 계정 키를 얻는 방법에 대한 자세한 내용은 다음을 참고하십시오. https://cloud.tencent.com/document/product/598/37140
String secretKey = System.getenv("secretKey");//서브 계정의 SecretKey. 리스크를 줄이기 위해 최소 권한 원칙을 따릅니다. 서브 계정 키를 얻는 방법에 대한 자세한 내용은 다음을 참고하십시오. https://cloud.tencent.com/document/product/598/37140
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);

// 사용자 인증 정보 초기화
COSCredentials cred = new BasicCOSCredentials("<루트 계정 APPID>", secretId, secretKey);
```

#### COSCMD TCCLI를 이용한 액세스 예시

COSCMD의 명령어 설정 예시이며, 다음과 같이 매개변수를 입력해야 합니다.
```sh
coscmd config -u <루트 계정 APPID> -a <서브 계정 SecretId> -s <서브 계정 SecretKey>  -b <루트 계정 bucketname> -r <루트 계정  bucket의 소속 리전>
```
인스턴스는 다음과 같습니다.
```sh
coscmd config -u 1250000000 -a AKIDasdfmRxHPa9oLhJp**** -s e8Sdeasdfas2238Vi**** -b examplebucket -r ap-beijing
```


(2) Tencent Cloud 콘솔 액세스

서브 계정는 권한 부여 후 [서브 계정 로그인](https://www.tencentcloud.com/account/login/subAccount) 페이지에서 루트 계정 아이디, 서브 계정 이름, 서브 계정 비밀번호를 입력하여 콘솔에 로그인할 수 있습니다. 그런 다음 **제품**에서 **Cloud Object Storage**를 클릭하여 루트 계정에서 스토리지 리소스에 액세스할 수 있습니다.

<span id="정책 예시"></span>
## 정책 예시
다음과 같은 일반적인 샘플 정책이 여기에서 제공됩니다. 정책을 구성할 때 아래 코드를 참고하여 **정책 내용** 란에 복사 붙여넣기 하시고 필요에 따라 수정하시면 됩니다. 다른 일반적인 COS 시나리오에 대한 자세한 정책 구문은 [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023) 또는 [CAM 제품 문서](https://www.tencentcloud.com/document/product/598)의 **비즈니스 사용 사례** 부분을 참고하십시오.

### 예시1: 서브 계정에 COS 전체 읽기 및 쓰기 권한 설정

>!본 정책의 권한 부여 범위가 넓습니다. 설정 시 유의하십시오.

자세한 정책 설정 구문은 다음과 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action":[
                "name/cos:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        }
    ]
}
```

### 예시2: 서브 계정에 읽기 전용 권한 설정
서브 계정에 읽기 전용 권한을 부여하는 자세한 정책 설정 구문은 다음과 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action":[
                "name/cos:List*",
                "name/cos:Get*",
                "name/cos:Head*",
                "name/cos:OptionsObject"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        }
    ]
}
```


### 예시3: 서브 계정에 쓰기 전용 권한 설정(삭제 제외)

자세한 정책 설정 구문은 다음과 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action":[
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload",
                "cos:ListMultipartUploads"
            ],
            "resource": "*"
        }
    ]
}
```


### 예시4: 특정 IP 범위에 대한 서브 계정 읽기/쓰기 권한 부여
다음 예시는 `192.168.1.0/24` 및 `192.168.2.0/24` 주소 범위에 대해서만 읽기/쓰기 권한을 부여합니다.
더 많은 조건을 입력하려면 [조건](https://www.tencentcloud.com/document/product/598/10608)을 참고하십시오.
```
{
    "version": "2.0",
    "statement": [
        {
            "action":[
    "cos:*"
            ],
            "resource": "*",
            "effect": "allow",
            "condition":{
                "ip_equal":{
                    "qcs:ip": ["192.168.1.0/24", "192.168.2.0/24"]
                }
            }
        }
    ]
}
```

