## 소개

Cloud Object Storage(COS) 콘솔에서 버킷에 대한 글로벌 가속을 활성화하면 업로드 및 다운로드가 가속화되어 전 세계의 최종 사용자가 버킷에 빠르게 액세스할 수 있습니다. 이를 통해 비즈니스 액세스 성공률과 비즈니스 안정성이 향상됩니다. 자세한 내용은 [개요](https://intl.cloud.tencent.com/document/product//436/33409)를 참고하십시오.

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭합니다.
3. 글로벌 가속 기능을 활성화할 버킷을 찾습니다. 버킷 이름을 클릭하여 세부 정보 페이지로 들어갑니다.
4. 왼쪽 사이드바에서 **도메인 및 전송 > 글로벌 가속**을 선택하고 **편집**을 클릭하여 기능을 활성화합니다.
![](https://main.qcloudimg.com/raw/e26fe8fd79c9bbc0d0ad1f9fe9088169.png)
5. 모든 것이 올바른지 확인한 후 **저장**을 클릭합니다.
![](https://main.qcloudimg.com/raw/1c6a7197c77a1555a91ad83fd29c8264.png)
글로벌 가속을 활성화한 후 `<BucketName-APPID>.cos.accelerate.myqcloud.com` 형식의 글로벌 가속 도메인 이름에서 버킷에 빠르게 액세스할 수 있습니다.
>? 글로벌 가속을 활성화해도 기존 기본 버킷 도메인 이름에는 영향을 미치지 않습니다. 여전히 사용할 수 있습니다.
>

