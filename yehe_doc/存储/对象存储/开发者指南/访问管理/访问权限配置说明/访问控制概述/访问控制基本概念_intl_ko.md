**기본적으로 Tencent Cloud COS(Cloud Object Storage)의 리소스(버킷 및 객체)는 비공개입니다**. Tencent Cloud 루트 계정(리소스 소유자)만 버킷과 객체에 액세스하고 수정할 수 있으며, 다른 사용자(서브 계정, 익명 사용자 등)는 권한 없이 URL을 통해 객체에 직접 액세스할 수 없습니다.

Tencent Cloud 서브 계정을 생성한 후 액세스 정책을 통해 서브 계정에 권한을 부여할 수 있으며, Tencent Cloud가 아닌 사용자에게 리소스를 공개해야 하는 경우 리소스(버킷, 객체, 디렉터리)에 대한 공개 권한(공개 읽기)을 설정하여 구현할 수 있습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/90b71308a1e1e6f1a842d0c7bd8c44d6.png)

## 액세스 제어 요소

액세스 권한 부여는 누가, 어떤 조건 하에서, 어떤 리소스에 대해, 구체적인 작업을 실행할 제어 능력을 가질지에 대한 조합을 결정하는 것을 의미합니다. 따라서 액세스 권한에는 일반적으로 **자격, 리소스, 작업, 조건(선택 사항)** 총 네 가지 요소가 포함됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/76920126347974448795fd58f7b8d26d.png)

## 액세스 권한 요소

#### Tencent Cloud 자격(Principal)

사용자가 Tencent Cloud 계정을 신청하면 시스템에서는 Tencent Cloud 서비스에 로그인할 수 있는 루트 계정 자격을 생성합니다. Tencent Cloud 루트 계정은 사용자 관리 기능을 통해 다양한 유형의 사용자를 분류하여 관리합니다. 사용자 유형은 **협업 파트너, 정보 수신자, 서브 계정, 역할** 등으로 나뉘며, 자세한 정의는 CAM의 [사용자 유형](https://intl.cloud.tencent.com/document/product/598/32633) 및 [용어집](https://intl.cloud.tencent.com/document/product/598/18564) 문서를 참고하십시오.

>?기업의 동료에게 권한을 부여하려면 먼저 [CAM 콘솔](https://console.cloud.tencent.com/cam)에서 서브 계정을 생성하고 [버킷 정책](버킷 정책 문서로 리디렉션), [ACL](ACL 문서로 리디렉션) 또는 [사용자 정책](사용자 정책 문서로 리디렉션)의 방법 중 하나 이상을 선택하여 서브 계정에 대한 특정 권한을 설정합니다.

#### COS 리소스(Resource)

Bucket과 Object는 COS의 기본 리소스이며, 그 중 폴더는 특별한 객체이며, 폴더를 통해 폴더 아래의 객체에 권한을 부여할 수 있습니다. 자세한 내용은 [폴더 권한 설정](https://intl.cloud.tencent.com/document/product/436/35261)을 참고하십시오.

또한 버킷과 객체 모두에 관련된 서브 리소스가 있습니다.

버킷의 서브 리소스는 다음을 포함합니다.

- acl과 policy: 버킷의 액세스 제어 정보
- website: 버킷의 정적 웹 사이트 호스팅 설정
- tagging: 버킷의 태그 정보
- cors: 버킷의 크로스 도메인 설정 정보
- lifecycle: 버킷의 라이프사이클 설정 정보

객체 서브 리소스는 다음을 포함합니다.

- acl: 객체의 액세스 제어 정보
- restore: 보관 유형 객체의 복구 설정

#### COS 작업(Action)

COS는 리소스에 대한 다양한 API 작업을 제공합니다. 자세한 내용은 [작업 리스트](https://intl.cloud.tencent.com/document/product/436/10111) 문서를 참고하십시오.

#### COS 조건(Condition, 옵션)

옵션 항목, 예시로 vpc, vip 등은 권한이 적용되기 위한 조건입니다. 자세한 사항은 CAM의 [적용 조건](https://intl.cloud.tencent.com/document/product/598/10608)을 참고하십시오.

## 개인 소유 원칙

>?Tencent Cloud COS의 리소스는 기본적으로 모두 비공개로 지정되어 있습니다.

- 리소스 소유자(버킷 리소스를 생성하는 Tencent Cloud 루트 계정)는 해당 리소스에 대한 최고 권한을 가지고 액세스 정책을 편집 및 수정할 수 있으며, 기타 사용자 또는 익명 사용자에게 액세스 권한을 부여할 수 있습니다.
- Tencent Cloud [CAM(Cloud Access Management)](https://intl.cloud.tencent.com/document/product/598/10583) 계정을 이용해 버킷을 생성하거나 객체를 업로드할 경우, 그 상위 루트 계정이 리소스 소유자가 됩니다.
- 버킷 소유자의 루트 계정은 다른 Tencent Cloud 루트 계정에 객체를 업로드할 수 있는 권한(교차 계정 업로드)을 부여할 수 있습니다. 이때 객체의 소유자는 여전히 버킷 소유자의 루트 계정입니다.

## 다양한 액세스 제어 경로

COS는 버킷 ​​정책, 사용자 정책(CAM 정책), 버킷 ACL 및 객체 ACL을 포함하여 액세스 제어를 구현하기 위한 여러 권한 설정 방법을 제공합니다.

정책 설정의 시작점에 따라 리소스 기반과 사용자 기반의 두 가지 방법으로 나눌 수 있으며, 권한 부여 방법에 따라 정책과 ACL의 두 가지 방법으로 나눌 수 있습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/332efdd73dc362ef889257cdfbd4d686.png)

**분류 방법1: 리소스 기반 vs 사용자 기반**
![](https://qcloudimg.tencent-cloud.cn/raw/fdc1f3434c0e75425f2a650a4ece79ec.png)
- 리소스를 시작점으로: 버킷 정책, 버킷 ACL 및 객체 ACL을 포함한 특정 리소스와 권한을 연결하여 COS 콘솔에서 또는 COS API를 통해 설정합니다.
- 사용자를 시작점으로: 사용자와 권한을 연결하는 사용자 정책(CAM 정책)은 정책 작성 시 사용자를 입력할 필요가 없으며, 리소스, 작업, 조건 등을 지정하고 [CAM 콘솔](https://console.cloud.tencent.com/cam)에서 설정해야 합니다.

**분류 방법2: 정책 vs ACL**
![](https://qcloudimg.tencent-cloud.cn/raw/5949e32de545aad4e878400e42dfef4c.png)
- 정책: 사용자 정책(CAM 정책) 및 버킷 정책은 완전한 정책 구문을 기반으로 권한이 부여되며, 권한 작업은 각 API에 해당하는 작업으로 세분화되며 허용/거부 효과 지정을 지원합니다.
- ACL: 버킷 ACL과 객체 ACL은 모두 액세스 제어 리스트(ACL)를 기반으로 구현됩니다. ACL은 정리되고 추상적인 권한에 해당하는 리소스와 관련된 지정된 피권한자 및 부여된 권한의 리스트입니다. 지정된 허용 효과만 지원합니다.


### 리소스 기반 정책

리소스 기반 정책에는 버킷 정책, 버킷 ACL 및 객체 ACL의 세가지가 포함됩니다. 액세스 제어는 **버킷** 및 **객체** 차원에서 지원됩니다. 자세한 내용은 다음 표를 참고하십시오.

| 규모   | 유형                   | 설명 방식 | 지원 자격                                       | 지원 리소스 데이터 분할 정도       | 지원 작업         | 지원 효력    |
| ------ | ---------------------- | -------- | ------------------------------------------------ | -------------------- | ------------------ | ------------- |
| Bucket | 액세스 정책 언어(Policy) | JSON     | 서브 계정, 역할, Tencent Cloud 서비스, 기타 루트 계정, 익명 사용자 등 | 버킷, 객체, 접두사 등 | 각각의 구체적인 작업   | 허용/명시적 거부 |
| Bucket | 액세스 제어 리스트(ACL)    | XML      | 기타 루트 계정, 익명 사용자                             | 버킷               | 정리된 읽기/쓰기 권한 | 허용만 가능        |
| Object | 액세스 제어 리스트(ACL)    | XML      | 기타 루트 계정, 익명 사용자                             | 객체                 | 정리된 읽기/쓰기 권한 | 허용만 가능        |

<span id="버킷 정책"></span>
#### 버킷 정책(Bucket Policy)

버킷 정책(Bucket Policy)은 JSON 언어를 사용하며 익명 자격이나 Tencent Cloud의 [CAM](https://intl.cloud.tencent.com/document/product/598/10583) 계정에 버킷, 버킷 작업, 객체, 객체 작업에 대한 권한을 부여할 수 있습니다. Tencent Cloud COS의 버킷 정책은 버킷의 거의 모든 작업을 관리할 수 있습니다. 버킷 정책을 사용해 ACL로 나타낼 수 없는 액세스 정책을 관리하십시오. 자세한 내용은 [버킷 정책](여기에서 ‘권한 제어 방법 소개’ 폴더 아래의 ‘버킷 정책’ 문서에 링크) 문서를 참고하십시오.

>!Tencent Cloud 루트 계정은 그에 속한 리소스(버킷 포함)에 대해 가장 큰 권한을 가집니다. 버킷 정책이 거의 모든 작업을 제한하더라도, 루트 계정은 PUT Bucket Policy 작업 권한을 계속 가지고 있으므로, 해당 작업을 호출하여 버킷 정책을 점검하지 않도록 할 수 있습니다.


다음은 광저우 버킷 examplebucket-1250000000의 모든 객체에 대한 익명 사용자의 액세스를 허가하는 정책입니다. 서명 인증할 필요 없이 버킷의 모든 객체(GetObject)를 다운로드할 수 있고, URL을 아는 익명 사용자는 모두 객체를 다운로드할 수 있습니다(공개 읽기 방식과 유사).

```json
{
  "Statement": [
    {
      "Principal": "*",
      "Effect": "Allow",
      "Action": ["cos:GetObject"],
      "Resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"]
    }
  ],
  "Version": "2.0"
}
```

<span id="액세스 제어 리스트"></span>
#### 액세스 제어 리스트(ACL)

액세스 제어 리스트(ACL)는 XML 언어를 사용하며, 리소스와 관련된 권한 부여자 및 권한 수여자 리스트입니다. 각각의 버킷과 객체에는 모두 이와 관련된 ACL이 있으며, 익명 사용자나 다른 Tencent Cloud의 루트 계정에 기본적인 읽기 및 쓰기 권한을 부여합니다. 자세한 내용은 [ACL](여기에서 ‘권한 제어 방법 소개’ 폴더 아래의 ‘ACL’에 링크) 문서를 참고하십시오.

>! 리소스 소유자는 전달한 ACL 중 항목 설명 여부에 상관없이 항상 리소스에 대한 FULL_CONTROL 권한을 가집니다.
>

다음은 버킷 ACL의 예시이며 버킷 소유자(사용자 UIN: 100000000001)의 전체 제어 권한을 설명합니다.

```xml
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

다음은 객체 ACL의 예시입니다. 객체 소유자(사용자 UIN: 100000000001)의 완전한 권한 제어를 설명하며 모든 사용자에게 읽기 권한(익명 사용자는 공개 읽기)을 부여합니다.

```xml
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
        <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee>
        <URI>http://cam.qcloud.com/groups/global/AllUsers</URI>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```


<span id="사용자 정책"></span>
#### 사용자 정책

사용자는 [CAM](https://intl.cloud.tencent.com/document/product/598/10583)에서 루트 계정에 속한 다양한 유형의 사용자에게 여러 가지 권한을 부여할 수 있습니다.

사용자 정책과 버킷 정책의 가장 큰 차이점은 사용자 정책은 효력(Effect), 작업(Action), 리소스(Resource), 조건(Conditon, 옵션)만 설명하며 자격(Principal)은 설명하지 않는다는 점입니다. 이 때문에 사용자 정책 작성이 완료되면 다시 서브 계정, 사용자 그룹 또는 역할 관련 작업을 실행해야 합니다. 사용자 정책은 익명 사용자에게 작업 또는 리소스 권한을 부여할 수 없습니다.

[사전 설정 정책을 이용해 관련 권한 부여 진행](https://intl.cloud.tencent.com/document/product/598/10602)을 할 수 있으며 [사용자 정책 자체 기입](https://intl.cloud.tencent.com/document/product/598/10603)한 후, 지정된 자격에 연결하여 사용자의 CAM을 관리할 수 있습니다. 자세한 내용은 [사용자 정책](여기에서 ‘권한 제어 방법 소개’ 폴더 아래의 ‘사용자 정책’에 링크) 문서를 참고하십시오.

다음은 광저우에 위치한 버킷 examplebucket-1250000000의 모든 COS 작업에 권한 위임을 한 정책입니다. 정책을 저장한 후 [CAM](https://intl.cloud.tencent.com/document/product/598/10583)의 서브 계정, 사용자 그룹 또는 적용 가능한 역할과 연결해야 합니다.

```json
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


