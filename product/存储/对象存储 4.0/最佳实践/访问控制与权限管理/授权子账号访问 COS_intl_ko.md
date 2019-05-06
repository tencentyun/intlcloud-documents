Tencent Cloud COS 리소스는 서로 다른 기업이나 같은 기업 내 여러 그룹 사이에서 서로 다른 그룹 또는 인원에게 접근 권한을 다르게 할당합니다. CAM(접근 관리를 CAM이라고 함)을 통해 할당할 수 있으며, 서로 다른 그룹이나 인원에 대해 버킷/객체 세분화로 다르게 작업할 수 있는 권한을 설정합니다.
전반적으로 구성은 서브 계정 생성, 서브 계정 권한 부여, 하위계정 접근 3단계로 나뉩니다.

먼저, 몇 가지 핵심 개념을 이해해야 합니다.
## 용어집
CAM 용어, 구성과 관련된 세부 설명은 [CAM 개요](/doc/product/598/10583)에서 확인하십시오.
### 루트 계정
루트 계정은 개발업체라고도 합니다. 사용자가 Tencent Cloud 계정을 신청할 때 시스템에서 Tencent Cloud 서비스에 로그인하기 위한 루트 계정 ID를 생성합니다. 루트 계정은 Tencent Cloud 리소스 사용량 계량 및 요금 계산의 기본 주체입니다.
청구서 정보 접근, 사용자 비밀번호 수정, 사용자와 사용자 그룹 생성 및 다른 클라우드 서비스 리스소 접근 등이 포함된 루트 계정은 기본적으로 그 명의 아래 보유한 리소스에 대해 완전한 접근 권한을 가집니다. 기본적으로 리소스는 루트 계정에 의해 접근할 수 있으며, 다른 사용자가 접근하기 위해서는 루트 계정의 접근 권한을 획득해야 합니다.

### 서브 계정(사용자)와 사용자 그룹
- 서브 계정은 루트 계정에 의해 생성된 엔터티로 확정된 신분 ID 및 ID 자격증명을 가지고 있으며 Tencent Cloud 콘솔에 로그인할 수 권한을 가지고 있습니다.
- 서브 계정은 기분적으로 리소스를 가지고 있지 않으며, 반드시 소속 루트 계정에 의해 권한을 부여 받습니다.
 - 하나의 루트 계정으로 여러 개의 서브 계정(사용자)을 생성할 수 있습니다.
 - 하나의 서브 계정은 여러 루트 계정에 속할 수 있으며, 여러 개의 루트 계정이 각각의 클라우드 리소스를 관리할 수 있도록 도와줍니다. 단, 동시에 하나의 서브 계정은 하나의 루트 계정에만 로그인하여, 해당 루트 계정의 클라우드 리소스를 관리합니다.
- 서브 계정은 콘솔을 통해 개발업체(루트 계정)를 변경하여, 루트 계정에서 다른 루트 계정으로 전환할수 있습니다.
 - 서브 계정으로 콘솔에 로그인할 경우, 자동으로 기본 루트 계정으로 전환할 수 있으며, 기본 루트 계정에 부여된 접근 권한을 가지게 됩니다.
 - 개발업체 변경 후, 서브 계정은 전환된 루트 계정에 접근 권한을 가지며, 기존 루트 계정의 접근 권한은 즉시 효력을 상실합니다.
- 사용자 그룹은 동일한 기능을 가진 여러 사용자(서브 계정)의 모음입니다. 비즈니스 요구 사항에 따라 다른 사용자 그룹을 생성하고 사용자 그룹에 적절한 정책을 연결하여 각기 다른 권한을 할당할 수 있습니다.

## 서브 계정 권한 구성
### 단계 1: 서브 계정 생성
CAM 콘솔에서 서브 계정을 생성할 수 있으며, 서브 계정에 접근 권한을 부여할 수 있습니다. 구체적인 실행방법은 다음과 같습니다.
1. [CAM 콘솔](https://console.cloud.tencent.com/cam)에 로그인 하여, 왼쪽 메뉴에 있는 [사용자 관리]를 클릭하십시오. 페이지에서 [사용자 생성]을 클릭하십시오.
 ![서브 계정1](//mc.qcloudimg.com/static/img/5d9194888617f10bfde81afa01c69e0b/image.png)
 
2. 요청에 따라 사용자 정보를 기입십시오.
 ![서브 계정2](//mc.qcloudimg.com/static/img/97dbdb848557f0195f90e1a78561eb37/image.png)
>!“로그인 계정”은 Tencent Cloud에 로그인 할 수 있는 계정으로, 3가지 유형의 계정을 서브 계정으로 추가할 수 있습니다. 추가 방식은 다음과 같습니다.
 - 이메일: Tencent Cloud에 등록된 이메일 또는 해당 계정 ID를 입력하십시오.
 - WeChat Official Account: Tencent Cloud에 있는 계정 ID를 입력하십시오.
 - QQ 번호: QQ번호 또는 계정 ID를 입력하십시오.

3. 시스템이 제공하는 정책 선택에 따라, COS에 대한 읽기/쓰기 권한, 읽기 전용 권한 등 간단한 정책을 구성할 수 있습니다. 복잡한 정책을 구성하려면 [절차 2: 서브 계정에 권한 부여](#서브 계정에 권한 부여)를 참조하십시오.
![서브 계정3](//mc.qcloudimg.com/static/img/8c3be83e576d892c99b90190d5f5c0b2/image.png)

<span id="서브 계정에 권한 부여"></span>
### 절차 2: 서브 계정에 권한 부여
서브 계정에 부여한 권한은 CAM을 통해, 서브 계정(사용자) 또는 사용자 그룹에 정책을 배치할 수 있습니다.
1. [CAM 콘솔](https://console.cloud.tencent.com/cam)에 로그인 하여, 왼쪽 메뉴에 있는 [정책 관리]를 클릭하십시오. [사용자 지정 정책] 탭을 클릭하고, [사용자 지정 정책 생성]을 클릭하십시오.
![4](//mc.qcloudimg.com/static/img/c1edfdc87bc078d8bc8f0fb052313d28/image.png)
2. [정책 구문에 따른 생성]을 선택하여, 생성 페이지로 들어갑니다.
![5](//mc.qcloudimg.com/static/img/94801671fcdff7b80dc973d9ee0e1165/image.png)
3. 선택한 템플릿으로 공백 템플릿과 기존의 COS 템플릿을 선택할 수 있으니, 실제 상황에 따라 선택하십시오.
![6](//mc.qcloudimg.com/static/img/8ee0f66634765849bb90a1a2d60806a5/image.png)
4. 정책 편집, COS 일반 시나리오에 대한 정책은 [CAM 제품 문서](/doc/product/598)의 상용 사례 섹션을 참조하십시오. 정책 내용을 복사하여 [정책 내용 편집]의 입력칸에 붙여넣을 수 있습니다.
![7](//mc.qcloudimg.com/static/img/2a5ce2ce4863f1a537dc74d45284ee5d/image.png)
5. 생성 후, 정책을 서브 계정과 연결할 수 있습니다.
![8](//mc.qcloudimg.com/static/img/3517b05ee79c818883d1ecf96dbbad89/image.png)
서브 계정에 권한을 부여하면, 즉시 권한 범위에 따라 COS 리소스에 접근할 수 있습니다.
![9](//mc.qcloudimg.com/static/img/606cdbcdccb90cf65dbc8826bc7d92da/image.png)
 

본 문서는 또한 다음과 같은 정책 예시를 통해 몇 가지 전형적인 시나리오를 설명합니다. 세부 정보는 [정책 예시](#策略示例)를 참조하십시오.
- COS를 사용하는 경우, 서브 계정에 읽기/쓰기 권한을 어떻게 할당하나요?
- COS를 사용하는 경우, 서브 계정에 읽기 전용 권한을 어떻게 할당하나요?
- COS를 사용하는 경우, IP 단락에 대해서만 읽기 전용 권한을 어떻게 설정하나요?

### 단계 3: 서브 계정으로 루트 계정 COS 리소스에 접근하기
COS 접근(API 또는 SDK)하기 위해서는 다음과 같은 리소스가 필요합니다. 예: APPID, SecretId, SecretKey.
서브 계정으로 COS 리소스에 접근할 경우, 루트 계정의 APPID, 서브 계정의 SecretId와 SecretKey를 사용해야 합니다. CAM 콘솔에서 서브 계정의 SecretId와 SecretKey를 생성할 수 있습니다.
1. 서브 계정으로 [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인 할 경우, 해당 루트 계정(개발사 계정)을 선택해야 합니다.
![10](//mc.qcloudimg.com/static/img/7f109890f04a9f57f3b8c924b3788e2d/image.png)
2. 로그인 후, [키 생성]을 클릭하면, 서브 계정을 생성할 수 있는 SecretID와 SecretKey, APPID는 루트 계정에서 제공됩니다.
![11](//mc.qcloudimg.com/static/img/294e294ef54662dedf57af975b7bea75/image.png)


>!
- 서브 계정은 XML API 또는 XML API 를 기반으로 한 SDK를 통해 COS 리소스에 접근해야 합니다.
- 서브 계정이 COS 리소스에 접근할 경우, 루트 계정의 APPID, 서브 계정의 SecretId와 SecretKey를 사용해야 합니다.

#### XML에 기반한 Java SDK 접근 예시
XML에 기반한 Java SDK 명령행 예시로, 매개변수를 다음과 같이 입력하십시오.
```
// 1 신분 정보 초기화
COSCredentials cred = new BasicCOSCredentials("<기본 계정 APPID>", "<서브 계정 SecretId>", "<서브 계정 SecretKey>");
```

인스턴스는 다음과 같습니다.
```
// 1 신분 정보 초기화
COSCredentials cred = new BasicCOSCredentials("1250000011", "AKIDasdfmRxHPa9oLhJp9wqwraCdtzvfPasdfaqW", "e8Sdeasdfas2238ViAXjpkU6XloeN2Wpxue");
```

#### COSCMD 명령행 도구 접근 예시
COSCMD `config` 명령행 작업 예시로, 매개변수를 다음과 같이 기입하십시오.
```
coscmd config -u <기본 계정 APPID> -a <서브 계정 SecretId> -s <서브 계정 SecretKey>  -b <기본 계정 bucketname> -r <기본 계정 bucketname 지역>
```
인스턴스는 다음과 같습니다.
```
coscmd config -u 1250000011 -a AKIDasdfmRxHPa9oLhJp9wqwraCdtzvfPasdfaqW -s e8Sdeasdfas2238ViAXjpkU6XloeN2Wpxue -b bucket1 -r ap-beijing
```
<span id="정책 예시"></span>
## 정책 예시
사용자 지정 정책을 할당할 때, 다음과 같이 참고 정책을 [정책 내용 편집]의 입력 창에 복사하여 붙여놓고, 실제 구성에 따라 수정할 수 있습니다.

### 서브 계정에 읽기/쓰기 권한 구성하기
서브 계정에 읽기/쓰기 권한만 구성하며, 구체적인 정책은 다음과 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
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
### 서브 계정에 읽기 전용 권한 구성하기
서브 계정에 읽기 전용 권한만 구성하며, 구체적인 정책은 다음과 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
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
### 서브 계정에 IP 단락의 읽기/쓰기 권한 할당하기
본 예시에서 IP 네트워크 세그먼트인 `192.168.1.0/24`와 `192.168.2.0/24`의 주소만 다음과 같이 읽기/쓰기 권한을 보유합니다.
더 많은 효력 조건을 입력하려면, [효력 조건](/doc/product/598/10608)을 확인하십시오.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
	"cos:*"
            ],
            "resource": "*",
            "effect": "allow",
            "condition": {
                "ip_equal": {
                    "qcs:ip": ["192.168.1.0/24", "192.168.2.0/24"]
                }
            }
        }
    ]
}
```

