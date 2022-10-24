## 작업 시나리오 
MPS(Media Processing Service)는 COS(Cloud Object Storage) 버킷에서 비디오를 다운로드하고 트랜스 코딩 후 COS 버킷에 파일을 업로드하려면 COS에 대한 읽기 및 쓰기 액세스 권한이 필요합니다. 따라서 MPS에 COS 액세스 권한을 부여하려면 서비스 역할을 생성해야 합니다.

## 작업 단계
1. [MPS 콘솔](https://console.cloud.tencent.com/mps)에 로그인한 후 왼쪽 사이드바의 [**일반 설정** > **액세스 관리**](https://console.cloud.tencent.com/mps/auth)를 클릭하고 **CAM(Cloud Access Management)**으로 이동합니다. CAM 콘솔에서 **권한 부여**를 클릭하여 사전 설정된 서비스 역할을 만들고 필요한 권한을 부여합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7eede4a6eb36a65a4d26b49f4e7b59af.png)
>! 권한을 부여하기 전에는 MPS 콘솔에서 추가 작업을 수행할 수 없습니다.
2. 권한 부여 후 **액세스 관리** 페이지로 돌아가면 역할이 성공적으로 생성된 것을 볼 수 있습니다. 부여된 권한을 취소하려면 **권한 취소**를 클릭하고 **CAM** 콘솔에서 생성된 [서비스 역할](https://intl.cloud.tencent.com/document/product/598/19388)을 찾아 삭제를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a4972ed47afa9acc4b8e1ca3bd5035b7.png)