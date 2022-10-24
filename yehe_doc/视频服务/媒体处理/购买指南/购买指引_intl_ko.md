## Tencent Cloud 가입
Media Processing Service(MPS)를 이용하기 전에 [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985)해야 합니다.

## MPS 신청
### 1단계: 가입 및 로그인
Tencent Cloud 공식 홈페이지에서 **클라우드 서비스** > **비디오 서비스** > [**MPS**](https://console.cloud.tencent.com/mps)를 클릭하여 MPS 콘솔로 이동합니다.

### 2단계: 권한 관리
MPS(Media Processing Service)는 COS(Cloud Object Storage) 버킷에서 비디오를 다운로드하고 트랜스 코딩 후 COS 버킷에 파일을 업로드하려면 COS에 대한 읽기 및 쓰기 액세스 권한이 필요합니다. 따라서 MPS에 COS 액세스 권한을 부여하려면 서비스 역할을 생성해야 합니다.
[MPS 콘솔](https://console.cloud.tencent.com/mps)로 이동한 후, 아직 권한 부여를 진행하지 않은 경우 **CAM으로 이동**을 클릭하여 콘솔의 통합 권한 관리 페이지로 이동한 후, 권한 부여 작업을 진행합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b5cf2f61dfd652dbd4af57abe13b06d3.png)

>! 권한을 부여하기 전에는 MPS 콘솔에서 추가 작업을 수행할 수 없습니다.

## MPS 이용
MPS 신청 후 콘솔에서 **클라우드 서비스** > **비디오 서비스** > [**MPS**](https://console.cloud.tencent.com/mps) 선택 후, MPS를 사용할 수 있습니다.

## MPS 과금
현재 지원되는 MPS 과금 방식은 [**Pay-As-You-Go**](https://intl.cloud.tencent.com/document/product/1041/33478) 및 [**Prepaid Resource Packs**](https://intl.cloud.tencent.com/document/product/1041/48810)입니다.
- **종량제 과금-일 결산**: 먼저 사용한 후 결제하는 과금 방식입니다. 사전에 Tencent Cloud 계정에 [충전](https://console.cloud.tencent.com/expense/recharge)해야 하며, 시스템은 전일 실제 사용량을 기준으로 매일 청구서를 푸시하고 요금을 정산하며, 계정 잔액에서 실제 사용량을 차감합니다.
-  **종량제 과금-월 결산**: 먼저 사용한 후 결제하는 과금 방식입니다. 사전에 Tencent Cloud 계정에 [충전](https://console.cloud.tencent.com/expense/recharge)해야 하며, 시스템은 월 단위로 매월 1일에 전월 발생 비용을 정산하고 청구서 발급 및 비용 공제를 진행합니다.
-  **선불 리소스 팩**: 팩으로 판매되는 MPS 리소스 팩입니다. [리소스 팩 구매](https://buy.cloud.tencent.com/mps) 후 리소스를 사용해야 하며, 매일 소모되는 MPS 리소스는 리소스 팩에 포함된 부분에 대해서는 과금되지 않고 초과 부분은 일 단위로 과금됩니다. 자세한 내용은, [Prepaid Resource Packs](https://intl.cloud.tencent.com/document/product/1041/48810)를 참고하십시오.
