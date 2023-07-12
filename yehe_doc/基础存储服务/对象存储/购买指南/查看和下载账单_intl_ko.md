## 소개
Tencent Cloud 콘솔의 **과금 센터**에서 계정의 COS 사용으로 인해 발생하는 요금을 확인할 수 있습니다.


>!
>- COS 청구서 결제 시 **무료 한도 > 종량제**의 순서로 결제됩니다.
> - 기본적으로 시스템은 정산을 위해 종량제 과금 방식을 사용합니다. 즉, 시스템은 먼저 무료 한도(있는 경우)를 차감한 후 종량제 방식으로 초과 사용량을 과금합니다.
>- 무료 한도, 과금 항목 설명 및 주의 사항은 [무료 한도](https://intl.cloud.tencent.com/document/product/436/6240) 및 [과금 개요](https://intl.cloud.tencent.com/document/product/436/16871)를 참고하십시오.



## 인스턴스별 청구서/청구 명세서 보기


콘솔의 [과금 센터](https://console.cloud.tencent.com/expense/overview)에서 인스턴스별 청구서 및 청구 명세서를 확인할 수 있습니다.

- 인스턴스별 청구: 인스턴스별 청구서(L2) 파일과 동일한 리소스 ID별 청구 금액을 표시합니다. 자세한 내용은 [Bill Management](https://www.tencentcloud.com/document/product/555/7430)를 참고하십시오.
- 청구 명세서: 상세 내역은 집계되지 않으며, 각 요금 입력 내역은 상세 내역입니다. 세부 사항은 청구 명세서(L3) 파일의 세부 사항과 동일합니다. 자세한 내용은 [Bill Management](https://www.tencentcloud.com/document/product/555/7430)를 참고하십시오.





<span id="XBZD"></span>



#### 조회 방법
1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com)에 로그인합니다.
2. 오른쪽 상단의 **요금**에서, **과금 센터**를 클릭하여 과금 센터 개요 페이지로 이동합니다.
3. 왼쪽 사이드바에서 **요금 청구서 > 청구서 세부 사항**을 클릭하여 인스턴스별 청구서 및 현재 계정의 청구서 세부 사항을 확인합니다.
>? 청구 요금 동향 및 요약을 보려면 **청구서 개요**를 선택하십시오.
>
4. ‘인스턴스별 청구서’ 탭의 드롭다운 목록에서 **COS**를 선택하여 리전, 과금 방식, 트랜잭션 유형 등의 COS 사용량을 확인합니다. 0 위안 항목 숨기기를 선택하면 청구 센터에서 0USD 항목의 청구서를 자동으로 숨깁니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d57e860dc2e1c482c6ba421c84cffb05.png)
‘청구 명세서’ 탭의 드롭다운 목록에서 **COS**를 선택하면 집계되지 않은 사용량 세부 정보를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0e158dd0cf06ac91b4bbe30dfee2ca58.png)
>? 
>- **버킷**별 청구 가능 항목별 사용량 내역 및 버킷 또는 리전별 요금 할당을 조회하려면 왼쪽 사이드바의 [사용량 내역 다운로드](https://console.cloud.tencent.com/expense/bill/dosageDownload)를 클릭하여 COS 사용량 내역 리포트를 다운로드하십시오.
>- 현재 COS는 얼로우리스트를 통해 제공되는 버킷별 청구를 지원합니다. 계정이 얼로우리스트에 있으면 인스턴스별 청구서 및 청구 명세서에서 리소스 ID로 **버킷 이름**별로 요금이 표시되는 것을 볼 수 있습니다.
>
구성 옵션은 다음과 같습니다.
 - **리전:** 리전별 청구서 세부 정보를 보려면 리전 드롭다운 목록에서 다른 리전을 선택합니다.
 - **과금 방식:** 종량제 과금 방식에서 청구 세부 정보를 보려면 과금 방식 드롭다운 목록에서 다른 과금 방식을 선택합니다
 - **거래 유형:** 거래 유형 드롭다운 목록에서 다른 거래 유형을 선택하여 종량제 거래 유형의 세부 정보를 볼 수 있습니다.





<span id="download"></span>

## 청구서 다운로드

[청구서 다운로드 센터](https://console.cloud.tencent.com/expense/overview)에서 대상 청구서를 다운로드할 수 있습니다. 현재 사용 가능한 청구서 유형에는 PDF 청구서(L0), 청구서 요약(L1), 인스턴스별 청구서(L2) 및 청구 명세서(L3)가 있습니다.

>?
>- 청구서 및 청구서 필드에 대한 자세한 내용은 각각 [Bill Management](https://www.tencentcloud.com/document/product/555/7430) 및 [Fields in Bills](https://intl.cloud.tencent.com/document/product/555/37506)를 참고하십시오.
>- 청구서 다운로드 방법에 대한 자세한 안내는 [Bill Download Center](https://intl.cloud.tencent.com/document/product/555/44357)를 참고하십시오.

