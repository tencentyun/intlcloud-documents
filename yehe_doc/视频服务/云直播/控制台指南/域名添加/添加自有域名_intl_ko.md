CSS 서비스 이용 시, 푸시 스트리밍 도메인과 재생 도메인을 포함하는 최소 **2개**의 도메인이 필요하며, 푸시 스트리밍과 재생은 동일한 도메인을 사용할 수 없습니다.

## 전제 조건
[Tencent Cloud CSS 서비스](https://intl.cloud.tencent.com/product/css)가 활성화된 상태여야 합니다.

## 작업 절차
[](id:step1)
### 1단계: 자체 도메인 추가
1. [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인하여 **Domain Management**를 선택합니다.
2. **Add Domain**을 클릭하여 도메인 추가 페이지로 이동해 다음과 같이 설정합니다.
    1. **푸시 스트리밍 도메인**을 추가하려는 경우: 도메인을 입력하고 도메인 유형을 **Push Domain**으로 선택한 후 **Confirm**을 클릭합니다.
    2. **재생 도메인**을 추가할 경우: 도메인을 입력하고 도메인 유형을 **Playback Domain**으로 선택한 후 가속 리전을 선택합니다. 가속 리전은 기본적으로 **Chinese Mainland**으로 설정되어 있습니다. 마지막으로 **Confirm**을 클릭합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/bde55a20b40da9d2d0fe2eda9613b63b.png)

>! 
>- 도메인은 45바이트로 제한되며 현재 대문자 도메인은 지원하지 않습니다. **45바이트** 이하의 알파벳 소문자로 된 도메인 주소를 입력하십시오.
>- 계정별로 도메인은 기본적으로 100개까지 관리할 수 있습니다. 비즈니스 사용량이 이를 초과하는 경우, [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 최대 도메인 수 확장을 신청할 수 있습니다. 
>- 외부 도메인 추가가 완료되면 도메인 관리 목록을 통해 수정할 도메인 또는 우측 **관리**를 클릭하여 도메인 상세 페이지로 이동합니다. **고급 설정** 선택 및 **리전 설정** 태그를 조회하고, **편집**을 클릭하면 리전 설정 변경 페이지로 이동합니다. 가속 리전을 재선택하고 **저장**을 클릭합니다.

[](id:step2)
### 2단계: 도메인 CNAME 완성
도메인 추가가 완료되면 시스템은 자동으로 CNAME 도메인(확장자: `.liveplay.myqcloud.com`) 이름을 할당합니다. CNAME 도메인은 직접 액세스할 수 없으므로 도메인 서비스 제공 업체에서 CNAME 설정을 완료해야 합니다. 설정이 적용되면 바로 CSS 서비스를 이용할 수 있으며, 자세한 내용은 [CNAME 설정](https://intl.cloud.tencent.com/document/product/267/31057)을 참고하십시오.

>? 이미 추가된 도메인의 관리가 필요한 경우 [도메인 관리](https://intl.cloud.tencent.com/document/product/267/31056)를 참고하십시오.

## FAQ
- [CSS 재생 도메인은 어떤 요구사항이 있습니까?](https://intl.cloud.tencent.com/document/product/267/7968)
- [라이브 방송에서 액세스하는 재생 도메인과 푸시 스트리밍 도메인이 동일해도 됩니까? 서브 도메인을 사용할 수 있습니까?](https://intl.cloud.tencent.com/document/product/267/7968)
