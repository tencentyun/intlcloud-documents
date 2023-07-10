## 소개

COS 콘솔에서는 버킷 리스트를 버킷 태그별로 필터링하는 기능을 제공하며, 해당 기능은 Tencent Cloud 태그 서비스에 종속되어 있습니다.

기업 계정 CompanyExample(OwnerUin: 100000000001, Owner_appid: 1250000000)에 서브 계정 jason.read가 있으며, 기업 계정 CompanyExample에서 해당 서브 계정에 태그 리스트 풀링 작업 권한을 부여할 경우를 예시로, 다음과 같이 권한 부여 작업에 대한 자세한 방법을 소개합니다.



## 관련 설명
서브 계정을 통해 콘솔에서 버킷 태그별로 버킷 리스트를 필터링할 경우, 서브 계정에 GetResourceTags, GetResourcesByTags, GetTags 작업 권한이 필요합니다. [CAM](https://console.cloud.tencent.com/cam/policy) 콘솔에서 사용자 정의 정책 생성 방식을 통해 서브 계정에 해당 권한을 부여할 수 있습니다.



## 작업 순서

1. 기업 계정 CompanyExample을 사용해 [CAM](https://console.cloud.tencent.com/cam/policy) 콘솔에 로그인하여 정책 설정 페이지로 이동합니다.
2. 서브 계정 jason.read에 태그 리스트 풀링 권한 부여는 **정책 생성기** 또는 **정책 구문**을 통해 실현할 수 있습니다.
 - **정책 생성기 사용**
(1) [CAM](https://console.cloud.tencent.com/cam/policy) 정책 설정 페이지로 이동합니다.
(2) [사용자 정의 정책 생성]>[정책 생성기에서 생성]을 클릭합니다.
(3) 권한 설정 페이지로 이동하여 다음과 같이 정보를 설정합니다.
    - **효과**: 허용이 선택되어 있으며, 기본값에서 변경하지 않습니다.
    - **서비스**: 태그를 선택합니다.
    - **작업**: 업무 수요에 따라 선택할 수 있으며, 본 예시에서는 GetResourceTags, GetResourcesByTags, GetTags의 세 작업 권한을 선택합니다.
    - **리소스**: 본 예시에서는 `*`를 입력하며, 실제 환경에 따라 작성할 수 있습니다. 자세한 내용은 [리소스 설명 방법](https://intl.cloud.tencent.com/document/product/598/10606)을 참조하십시오.
![](https://main.qcloudimg.com/raw/6ef8573a92f3c59b7c0f633b935273da.png)
(4) [선언 추가]를 클릭하면 아래에서 설정한 권한을 확인할 수 있습니다.
(5) [다음 단계]를 클릭하고 정책 이름을 입력한 후 [정책 생성]을 클릭하면 생성이 완료됩니다.
 - **정책 구문 사용**
(1) [CAM](https://console.cloud.tencent.com/cam/policy) 정책 설정 페이지로 이동합니다.
(2) [사용자 정의 정책 생성]>[정책 구문에 따른 생성]을 클릭합니다.
(3) 빈 템플릿 또는 기존 태그 템플릿을 선택하여 생성할 수 있습니다. 본 예시에서는 [QcloudTAGFullAccess] 템플릿을 선택합니다.
![](https://main.qcloudimg.com/raw/b5117e831228f59427f03d91a6fdf646.png)
（4）[다음 단계]를 클릭하면 템플릿 정책이 기본적으로 `tag:*`로 설정되어 있는 것을 확인할 수 있습니다. 본 예시에서는 action을 `name/tag:GetResourceTags`, `name/tag:GetResourcesByTags`, `name/tag:GetTags`로 수정하여 작업 권한을 설정합니다. 정책 구문 예시는 다음과 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/tag:GetResourceTags",
                "name/tag:GetResourcesByTags",
                "name/tag:GetTags"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```
(5) [정책 생성]을 클릭하면 생성이 완료됩니다.
3.정책을 서브 계정 jason.read에 연결합니다. 정책 페이지에서 2단계에서 생성한 정책을 찾아 해당 정책 오른쪽에 있는 [사용자/그룹 연결]을 클릭합니다.
4. 사용자/그룹 연결 창에서 서브 계정 jason.read를 선택하고 [확인]을 클릭하면 서브 계정 jason.read이 해당 정책과 연결됩니다.
![](https://main.qcloudimg.com/raw/4818cbb813fce18bc8d6fd6062e35e55.png)
5. 서브 계정 jason.read로 콘솔에 로그인한 후 [버킷 리스트](https://console.cloud.tencent.com/cos5/bucket) 페이지에서 **태그**를 선택하고 **태그 키**를 입력하여 검색하면 다음과 같이 해당 태그를 가진 버킷 리스트가 조회됩니다.
![](https://main.qcloudimg.com/raw/3f31b5273da16e7728ab40209cfedfa9.png)
