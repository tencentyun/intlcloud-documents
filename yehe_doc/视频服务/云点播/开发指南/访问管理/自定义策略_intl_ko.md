>!본 문서는 **VOD** CAM 기능에 대한 내용을 소개합니다. 기타 제품의 CAM 관련 내용은 [CAM 지원 제품](https://intl.cloud.tencent.com/document/product/598/10588)을 참고하십시오.

CAM에서 [사전 설정된 정책](https://intl.cloud.tencent.com/document/product/266/33971)을 사용하여 권한 부여를 구현하는 것이 편리하지만 권한 제어의 단위가 크고 서브 애플리케이션 및 API 수준으로 세분화할 수 없습니다. 세분화된 권한 제어가 필요한 경우 사용자 정의 정책을 생성해야 합니다.


## 사용자 정의 정책 생성 방법

사용자 정의 정책 생성은 여러 가지 방법이 있으며, 하기 표는 여러 방법들의 비교표입니다. 구체적인 작업 프로세스는 다음을 참고하십시오.

| 생성 항목   | 생성 방법     | 효과<br/>(Effect) | 리소스<br/>(Resource) | 동작<br/>(Action) | 효율성 | 난이도 |
| ---------- | ------------ | ------------------- | --------------------- | ------------------- | ------ | ---- |
| 콘솔     | 정책 생성기   | 수동 선택            | 구문 설명              | 수동 선택            | Medium     | Medium   |
| 콘솔     | 정책 구문     | 구문 설명            | 구문 설명              | 구문 설명            | High     | High   |
| 서버 API | CreatePolicy | 구문 설명            | 구문 설명              | 구문 설명            | High     | High   |

>?
>- VOD는 제품 기능별 맞춤형 정책 생성을 지원하지 않습니다.
>- **수동 선택**은 콘솔에 표시되는 후보 목록에서 개체를 선택할 수 있음을 의미하고 **구문 설명**은 정책 구문을 통해 개체를 설명할 수 있음을 의미합니다.

<span id = "p1"></span>
## 리소스에 대한 정책 구문 설명

위에서 언급했듯이 VOD에서 권한 제어의 리소스 세분성은 서브 애플리케이션입니다. 정책 구문의 서브 애플리케이션 설명은 [CAM 규칙](https://intl.cloud.tencent.com/document/product/598/10606)을 따릅니다. 아래 예시에서 개발자의 루트 계정 ID는 12345678이고 APPID는 1250000001(기본 애플리케이션 ID와 동일)이며 개발자는 ID가 각각 1400000001 및 1400000002인 두 개의 VOD 서브 애플리케이션을 생성했습니다. 

- **모든 VOD 리소스에 대한 정책 구문 설명**
```
"resource": [
	"qcs::vod::uin/12345678:subAppId/*"
]
```
- **기본 애플리케이션에 대한 정책 구문 설명**
```
"resource": [
	"qcs::vod::uin/12345678:subAppId/1250000001"
]
```
- **단일 서브 애플리케이션에 대한 정책 구문 설명**
```
"resource": [
	"qcs::vod::uin/12345678:subAppId/1400000001"
]
```
- **기본 애플리케이션 및 단일 서브 애플리케이션에 대한 정책 구문 설명**
```
"resource": [
	"qcs::vod::uin/12345678:subAppId/1250000001",
	"qcs::vod::uin/12345678:subAppId/1400000001"
]
```

<span id ="p3"></span>
## 작업에 대한 정책 구문 설명

위에서 언급했듯이 VOD에서 권한 제어의 작업 단위는 서버 API입니다. 다음은 `DescribeMediaInfos`, `DescribeAllClass` 등의 서버 API 예시입니다.

- **모든 VOD 서버 API에 대한 정책 구문 설명**
```
"action": [
	"name/vod:*"
]
```
- **단일 서버 API에 대한 정책 구문 설명**
```
"action": [
	"name/vod:DescribeMediaInfos"
]
```
- **여러 서버 API에 대한 정책 구문 설명**
```
"action": [
	"name/vod:DescribeMediaInfos",
	"name/vod:DescribeAllClass"
]
```

## 사용자 정의 정책 사용 예시

### 정책 생성기 사용

아래 예시에서는 서버 API `ProcessMedia`를 제외한 모든 작업이 VOD 서브 애플리케이션 1400000001에서 수행되도록 허용하는 사용자 정의 정책을 만듭니다.

1. [루트 계정](https://intl.cloud.tencent.com/document/product/598/32633)으로 CAM 콘솔의 [[정책]](https://console.cloud.tencent.com/cam/policy)페이지에 액세스하고 [사용자 정의 정책 생성]을 클릭합니다.
2. [정책 생성기로 생성]을 선택하여 정책 생성 페이지로 이동합니다.
3. 서비스 및 작업을 선택합니다.
	- [효과(Effect)] 설정 항목은 [허용]을 선택합니다.
	- [서비스(Service)] 설정 항목은 [VOD]를 선택합니다.
	- [작업(Action)]에 대한 모든 항목을 선택합니다.
	- [리소스(Resource)] 설정 항목은 [리소스에 대한 구문 설명](#p1)에 따라 `qcs::vod::uin/12345678:subAppId/1400000001`을 입력합니다.
	- [조건(Condition)] 설정 항목은 설정할 필요가 없습니다.
	- [성명서 추가]를 클릭하면, 페이지 하단에 ‘VOD 서브 애플리케이션 1400000001에 대해 모든 작업이 허용됩니다’라는 문구가 나타납니다.
4. 같은 페이지에 다른 성명문을 계속 추가합니다.
	- [효과(Effect)] 설정 항목에서 [거부]를 선택합니다.
	- [서비스(Service)] 설정 항목은 [VOD]를 선택합니다.
	- [작업(Action)]에 대해 `ProcessMedia`(검색으로 선택할 수 있음)를 체크합니다.
	- [리소스(Resource)]설정 항목은 [리소스에 대한 구문 설명](#p1)에 따라 `qcs::vod::uin/12345678:subAppId/1400000001`을 입력합니다.
	- [조건(Condition)] 설정 항목은 설정할 필요가 없습니다.
	- [성명서 추가]를 클릭하면 페이지 하단에 ‘VOD 서브 애플리케이션 1400000001에서 `ProcessMedia` 작업이 거부되었습니다’라는 명령문이 표시됩니다.
     ![](https://main.qcloudimg.com/raw/1ac34ffafb9719e36e46d4a5e7ccf1cf.png)
5. [다음]을 클릭하고 필요에 따라 정책 이름을 수정합니다(또는 변경하지 않은 상태로 둡니다).
6. [완료]를 클릭하여 사용자 지정 정책을 생성합니다. 이후 [기존 서브 계정에 VOD의 전체 권한 부여](https://intl.cloud.tencent.com/document/product/266/33971#p2)하는 것과 동일한 방식으로 이 정책을 서브 계정에게 부여할 수 있습니다.


### 정책 구문 사용

아래 예시에서는 VOD 서브 애플리케이션 1400000001 및 1400000002에서 모든 작업을 수행할 수 있지만 서브 애플리케이션 1400000001에 대해 `ProcessMedia`를 거부하는 사용자 지정 정책을 만듭니다.

1. [루트 계정](https://intl.cloud.tencent.com/document/product/598/32633)으로 CAM 콘솔의 [[정책]](https://console.cloud.tencent.com/cam/policy)페이지에 액세스하고 [사용자 정의 정책 생성]을 클릭합니다.
2. [정책 구문으로 생성]을 선택하여 정책 생성 페이지로 이동합니다.
3. [템플릿 유형 선택] 상자에서 [빈 템플릿]을 선택합니다.
>?정책 템플릿은 기존 정책(사전 설정 또는 사용자 지정)을 복사한 다음 복사본을 조정하여 정책을 만드는 데 사용됩니다. 실제 사용 시 실제 상황에 따라 적절한 정책 템플릿을 선택하여 정책 내용 작성의 어려움과 작업량을 줄일 수 있습니다. 
5. [다음]을 클릭하고 필요에 따라 정책 이름을 수정합니다(또는 변경하지 않은 상태로 둡니다).
5. [정책 콘텐츠 편집] 상자에 정책 내용을 입력합니다. 본 예시의 정책 내용은 다음과 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/vod:*"
            ],
            "resource": [
                "qcs::vod::uin/12345678:subAppId/1400000001",
                "qcs::vod::uin/12345678:subAppId/1400000002"
            ]
        },
        {
            "effect": "deny",
            "action": [
                "name/vod:ProcessMedia"
            ],
            "resource": [
                "qcs::vod::uin/12345678:subAppId/1400000001"
            ]
        }
    ]
}
```

>? 정책 내용은 CAM [정책 구문](https://intl.cloud.tencent.com/document/product/598/10603) 규칙을 따라야 합니다. 여기서 리소스 및 작업의 구문은 위의 [리소스에 대한 정책 구문 설명](#p1) 및 [작업에 대한 정책 구문 설명](#p3)에 표시된 것과 같습니다.

6. [정책 생성]을 클릭하여 사용자 지정 정책을 만듭니다. 이후 [예시: 기존 서브 계정에 VOD의 전체 권한 부여](https://intl.cloud.tencent.com/document/product/266/33971#p2)와 동일하게 이 정책을 서브 계정에게 부여할 수 있습니다.

### 서버 API 사용

대부분의 개발자는 콘솔에서 권한 관리 작업을 수행하여 서비스 요구 사항을 충족할 수 있습니다. 그러나 권한 관리 기능을 자동화하고 체계화해야 하는 경우, 서버 API를 통해 실현할 수 있습니다.
정책 관련 서버 API는 CAM에 속하며, 자세한 사항은 [CAM 공식 홈페이지 문서](https://intl.cloud.tencent.com/zh/document/product/598)를 참고하시기 바랍니다. 다음은 몇 가지 주요 인터페이스 입니다.

- [정책 생성](https://intl.cloud.tencent.com/document/product/598/32248)
- [정책 삭제](https://intl.cloud.tencent.com/document/product/598/32247)
- [사용자에 정책 바인딩하기](https://intl.cloud.tencent.com/document/product/598/32249)
- [사용자에 정책 바인딩 해제하기](https://intl.cloud.tencent.com/document/product/598/32245)
