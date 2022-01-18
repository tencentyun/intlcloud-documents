## Tencent Cloud 가입
Media Processing Service(MPS) 서비스를 이용하기 전에 [Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985) 계정이 필요합니다.

## MPS 서비스 신청
### 1단계: 가입 및 로그인

Tencent Cloud 공식 홈페이지에서 **클라우드 서비스** >**비디오 서비스**>[**MPS**](https://console.cloud.tencent.com/mps) 클릭하여 MPS 콘솔로 진입합니다.

### 2단계: 권한 관리
MPS는 COS 버킷에 업로드된 파일에 다운로드, 트랜스 코딩, 업로드 등의 읽기 및 쓰기 작업을 수행해야 하므로, 서비스 역할을 생성하고 MPS에 COS 관련 작업 권한을 부여해야 합니다.

[MPS 콘솔](https://console.cloud.tencent.com/mps)로 이동한 후, 아직 권한 부여를 진행하지 않은 경우 **CAM으로 이동**을 클릭하여 콘솔의 통합 권한 관리 페이지로 이동한 후, 권한 부여 작업을 진행합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e001187c224f239c596ccc4343e03be7.png)
>!권한 부여가 완료되지 않은 경우, MPS 콘솔에서 다른 작업을 수행할 수 없습니다.


## MPS 서비스 이용
MPS 서비스 신청 후 콘솔에서 **클라우드 서비스**>**비디오 서비스**>[**MPS**](https://console.cloud.tencent.com/mps) 선택 후, MPS 서비스를 사용할 수 있습니다.

## MPS 서비스 과금
현재 지원되는 MPS 과금 방식은 **일 결산(후불)**, **월 결산(후불)**이며, 자세한 사항은 [과금 방식](https://intl.cloud.tencent.com/document/product/1041/33478)을 참고하십시오.

- **일 결산 과금**: 먼저 사용한 후 결제하는 과금 방식입니다. 사전에 Tencent Cloud 계정에 [충전](https://console.cloud.tencent.com/expense/recharge)해야 하며, 시스템은 전일 실제 사용량을 기준으로 매일 청구서를 푸시하고 요금을 정산하며, 계정 잔액에서 실제 사용량을 공제합니다.
-  **월 결산 과금**: 먼저 사용한 후 결제하는 과금 방식입니다. 사전에 Tencent Cloud 계정에 [충전](https://console.cloud.tencent.com/expense/recharge)해야 하며, 시스템은 월 단위로 매월 1일에 전월 발생 비용을 정산하고 청구서 발급 및 비용 공제를 진행합니다.
