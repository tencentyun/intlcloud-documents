## 소개

Cloud Object Storage(COS)는 태그별로 버킷을 필터링하는 기능을 제공합니다. 이 기능은 Tencent Cloud 태그 서비스에 종속됩니다.

엔터프라이즈 계정 CompanyExample(OwnerUin: 100000000001, Owner_appid: 1250000000)에 서브 계정 Developer가 있으며, CompanyExample이 태그가 지정된 객체 목록을 가져오기 위해 서브 계정 권한을 부여해야 한다고 가정합니다. 다음은 권한 부여 방법을 설명합니다.



## 관련 설명
서브 계정을 통해 콘솔에서 버킷 태그별로 버킷 리스트를 필터링할 경우, 서브 계정에 GetResourceTags, GetResourcesByTags, GetTags 작업 권한이 필요합니다. [CAM 콘솔](https://console.cloud.tencent.com/cam/policy)에서 사용자 정의 정책 생성 방식을 통해 서브 계정에 해당 권한을 부여할 수 있습니다.



## 작업 단계

1. 엔터프라이즈 계정 CompanyExample을 사용해 [CAM 콘솔](https://console.cloud.tencent.com/cam/policy)에 로그인하여 정책 설정 페이지로 이동합니다.
2. 서브 계정 Developer에 **정책 생성기** 또는 **정책 구문**을 통해 태그가 지정된 객체 목록을 가져올 수 있는 권한을 부여합니다.
<dx-tabs>
::: 정책 생성기 사용
1. CAM 콘솔의 [정책](https://console.cloud.tencent.com/cam/policy) 페이지로 이동합니다.
2. **사용자 정의 정책 생성 > 정책 생성기에서 생성**을 클릭합니다.
3. 권한 구성 페이지로 이동하여 다음과 같이 정보를 구성합니다.
 - **태그**:
    - **효과**: 허용이 선택되어 있으며, 기본값에서 변경하지 않습니다.
    - **서비스**: 태그를 선택합니다.
    - **작업**: 비즈니스 요구 사항에 따라 선택할 수 있으며, 본 예시에서는 GetResourceTags, GetResourcesByTags, GetTags의 세 작업 권한을 선택합니다.
    - **리소스**: **모든 리소스**를 선택합니다.
 - **권한 추가**: 비즈니스 요구 사항에 따라 구성합니다.
5. **다음**을 클릭하고 정책 이름을 입력합니다.
6. **완료**를 클릭합니다.
:::
::: 정책 구문 사용
1. CAM 콘솔의 [정책](https://console.cloud.tencent.com/cam/policy) 페이지로 이동합니다.
2. **사용자 정의 정책 생성 > 정책 구문으로 생성**을 클릭합니다.
3. 빈 템플릿 또는 기존 태그 템플릿을 선택하여 생성할 수 있습니다. 본 예시에서는 **QcloudTAGFullAccess** 템플릿을 선택합니다.
4. **다음 단계**를 클릭하면 템플릿 정책이 기본적으로 `tag:*`로 설정되어 있는 것을 볼 수 있습니다. 본 예시에서는 action을 `name/tag:GetResourceTags`, `name/tag:GetResourcesByTags` 및 `name/tag:GetTags`로 수정하여 작업 권한을 설정합니다. 정책 구문 예시는 다음과 같습니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action":[
                "name/tag:GetResourceTags",
                "name/tag:GetResourcesByTags",
                "name/tag:GetTags"
            ],
            "resource":[
                "*"
            ]
        }
    ]
}
```
5. **완료**를 클릭합니다.
:::
</dx-tabs>
3. 정책 페이지에서 2단계에서 생성한 정책을 찾고 오른쪽에서 **사용자/그룹/역할 연결**을 클릭하여 정책을 서브 계정 Developer와 연결합니다.
4. 팝업 창에서 Developer 서브 계정을 선택하고 **확인**을 클릭합니다.
5. Developer 서브 계정으로 콘솔에 로그인한 후 [버킷 리스트](https://console.cloud.tencent.com/cos5/bucket) 페이지에서 **태그**를 선택하고 **태그 키**를 입력하여 지정된 태그가 있는 버킷을 검색합니다.

