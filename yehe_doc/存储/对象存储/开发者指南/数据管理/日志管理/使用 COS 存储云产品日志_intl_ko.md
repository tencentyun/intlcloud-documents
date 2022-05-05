## 소개

Tencent Cloud 서비스를 사용할 때 대량의 로그가 생성되는데, 이 로그들은 귀하의 업무 상황을 기록해 업무 상황을 분석하는 데 도움이 되며 귀하의 업무 발전과 의사 결정에 도움을 줍니다. COS 스토리지 기능을 이용해 클라우드 서비스 로그를 지속적으로 저장할 수 있으며, API, SDK 또는 툴 등을 통해 COS로부터 로그를 쉽게 얻고 분석할 수 있습니다.

COS 스토리지 클라우드 서비스 로그를 사용하면 다음 문제를 해결할 수 있습니다.

- **영구 스토리지**: COS는 안정된 영구 스토리지 서비스를 제공하므로 낮은 비용으로 로그를 COS로 저장해 영속화 저장이 가능합니다. 업무 필요에 의해 로그를 기반으로 분석 또는 의사 결정 시, COS를 통해 언제 어디서나 임의 시간대의 로그를 얻을 수 있습니다.
- **데이터 인덱스**: COS는 Select 기능을 제공하므로 해당 기능으로 COS에 저장된 로그에 대한 간단한 인덱스 및 추출이 가능합니다. 로그의 필드를 결합하면 필요한 정보를 인덱스하고 데이터 다운로드 트래픽을 줄일 수 있습니다.
- **데이터 분석**: Sparkling 제품을 사용하여 COS에 저장된 로그를 분석할 수 있으며, 하나 이상의 로그 파일을 선택하고 Sparkling을 사용하여 로그를 분석하고 분석 결과를 기반으로 의사 결정을 내릴 수 있습니다.

## 로그 전송 방식

두 가지 방식으로 Tencent Cloud 서비스의 로그를 COS에 저장할 수 있습니다.

- 클라우드 서비스 자체 로그 전송 기능 사용: 예를 들어 COS, CA 등 제품은 로그를 COS로 직접 전송할 수 있습니다.
- 로그 서비스 CLS의 전송 기능 사용: CLS로 전송된 클라우드 서비스 로그는 CLS를 통해 COS로 전송돼 영구 저장됩니다.

현재 Tencent Cloud 서비스의 이 두 가지 방식에 대한 지원 상황은 다음과 같습니다.

| 클라우드 서비스 이름          | COS로의 직접 전송 지원 여부 | CLS로의 전송 지원 여부    |
| ------------------- | ---------------------- | ---------------------- |
| CA           | 지원                     | 미지원                     |
| CLB        | 미지원                   | 지원                     |
| CKafka     | 지원                     | 미지원                     |
| API Gateway | 미지원                    | 지원                     |
| SCF      | 미지원                     | 지원                     |
| TKE        | 미지원                     | 지원                     |
| CSS          | 미지원                     | 지원                     |
| TCB          | 미지원                     | 지원(단, CLS를 통한 COS로의 전송은 지원하지 않음)|
| COS        | 지원                     |  얼로우리스트 활성화 신청을 지원합니다. [고객센터](https://intl.cloud.tencent.com/contact-sales)를 통해 얼로우리스트 활성화       |

### COS로 직접 로그 전송하기

다음 Tencent Cloud 서비스는 COS로 직접 로그를 전송하는 기능을 갖고 있습니다. 해당 제품 문서 가이드에 따라 로그 전송 규칙을 설정하여 로그를 COS로 전송할 수 있습니다.

| 클라우드 서비스 이름     | 로그 전달 문서                                                 | 로그 전달 간격        | 로그 전달 경로                                                 |
| --------------- | ------------------------------------------------------------ | -------------------- | ------------------------------------------------------------ |
|CA |[알아보기](https://intl.cloud.tencent.com/document/product/1021/30338) | 10-15분 |  cloudaudit/customprefix/timestamp|
| CKafka | [알아보기](https://intl.cloud.tencent.com/document/product/597) | 5분-60분<br>전송 간격 지정 가능 | instance id/topic id/timestamp                           |
| COS    | [알아보기](https://intl.cloud.tencent.com/document/product/436/17040) | 5분                | 경로 접두사는 자동 지정되며, 식별 가능한 경로 설정을 권장합니다. 예시: cos_bucketname_access_log/timestamp |

>?메시지 큐는 해당 제품에서 생성된 정보 데이터의 전송을 지원합니다. CKafka 인스턴스 생성 등 동작 로그를 얻어야 할 경우, CA 제품을 전송할 로그를 선택하십시오.

### CLS를 통해 COS로 로그 전송하기

다음 Tencent Cloud 서비스는 사용자가 인덱스 및 분석을 할 수 있도록 로그를 CLS로 전송하는 기능을 제공합니다. CLS는 COS로 전송하는 제품 기능도 동시에 제공하여, 사용자가 로그를 쉽게 영구 저장할 수 있게 합니다. CLS로의 로그 전송을 지원하는 제품도 CLS 밖에서 COS로 전송된 로그를 활성화하는 방식을 통해 데이터를 영구 저장해 스토리지 비용을 낮추고 보다 편리한 오프라인 분석이 가능합니다. 현재 CLS로의 직접 로그 전송을 지원하는 제품은 다음과 같습니다.

| 클라우드 서비스 이름           | 로그 전송 문서                                                 |
| -------------------- | ------------------------------------------------------------ |
| API Gateway | [알아보기](https://intl.cloud.tencent.com/document/product/628/34636) |
| TKE         | [알아보기](https://intl.cloud.tencent.com/document/product/457/32419) |
| LVB           | 알아보기|

CLS에서 COS로의 전송은 다음 세 가지 방식으로 지원됩니다.

- 세퍼레이터 포맷 전송: 데이터를 세퍼레이터 포맷에 따라 COS로 전송합니다. 자세한 내용은 [CSV Shipping](https://intl.cloud.tencent.com/document/product/614/31582)을 참고하십시오.
- JSON 포맷 전송: 데이터를 JSON 포맷에 따라 COS로 전송합니다. 자세한 내용은 [JSON Shipping](https://intl.cloud.tencent.com/document/product/614/31583)을 참고하십시오.
- 원문 포맷 전송: 데이터를 원문 포맷에 따라 전송합니다. 단일 행 텍스트, 다중 행 텍스트 전송을 지원하며, 부분적으로 CSV 포맷 전송을 지원합니다. 자세한 내용은 [Source Format Shipping](https://intl.cloud.tencent.com/document/product/614/31584)을 참고하십시오.

CLS를 통해 COS로 로그를 전송하려면 다음 작업을 수행해야 합니다.

1. 업무 필요에 따라 해당 제품을 선택하고, 위에서 제공한 제품 로그 전송 문서 링크 가이드에 따라 로그셋 및 로그 테마를 설정하면, 업무에서 발생한 데이터가 CLS로 연결됩니다.
2. 이후, 업무 필요에 따라 적합한 포맷을 선택해 데이터를 COS로 전송합니다. 로그를 COS로 보낼 때, 제품 이름을 경로 접두사로 삼아 서로 다른 제품 로그를 구분하길 권장합니다. 예를 들어, TKE 로그는 `TKE_tkeid_log/timestamp`로 이름을 생성합니다.
3. 전송 규칙 설정이 끝나면 별도로 SCF 제품 아래 파일 업로드 이벤트 공지를 설정할 수 있습니다. 로그 데이터가 COS로 전송되면 이벤트 공지에 따라 다음 단계 작업을 수행할 수 있습니다. 자세한 내용은 [이벤트 알림](https://intl.cloud.tencent.com/document/product/436/31648)을 참고하십시오.

## 로그 분석

### 로그를 로컬로 다운로드해 오프라인 분석하기

로그 데이터를 로컬로 다운로드해야 할 경우, 콘솔/SDK/API 또는 툴 등 다양한 방식으로 다운로드할 수 있습니다. 다음은 다운로드 방식에 대한 사용 문서 설명으로, 다음 문서를 참고해 코드에서 파일 경로와 관련된 부분을 로그 저장 경로로 바꾸면 로그 데이터를 로컬로 다운로드할 수 있습니다.

| 다운로드 방식     | 사용 설명                                                     |
| -------------- | ------------------------------------------------------------ |
| 콘솔         | [알아보기](https://intl.cloud.tencent.com/document/product/436/13322) |
| cosbrowser     | [알아보기](https://intl.cloud.tencent.com/document/product/436/32565) |
| coscmd         | [알아보기](https://intl.cloud.tencent.com/document/product/436/10976) |
| Android SDK    | [알아보기](https://intl.cloud.tencent.com/document/product/436/37675) |
| C SDK          | [알아보기](https://intl.cloud.tencent.com/document/product/436/31518) |
| C++ SDK        | [알아보기](https://intl.cloud.tencent.com/document/product/436/31522) |
| .NET SDK       | [알아보기](https://intl.cloud.tencent.com/document/product/436/30594) |
| Go SDK         | [알아보기](https://intl.cloud.tencent.com/document/product/436/31526) |
| iOS SDK        | [알아보기](https://intl.cloud.tencent.com/document/product/436/37684) |
| Java SDK       | [알아보기](https://intl.cloud.tencent.com/document/product/436/31534) |
| JavaScript SDK | [알아보기](https://intl.cloud.tencent.com/document/product/436/31538) |
| Node.js SDK    | [알아보기](https://intl.cloud.tencent.com/document/product/436/31710) |
| PHP SDK        | [알아보기](https://intl.cloud.tencent.com/document/product/436/31542) |
| Python SDK     | [알아보기](https://intl.cloud.tencent.com/document/product/436/31546) |
| 미니프로그램 SDK     | [알아보기](https://intl.cloud.tencent.com/document/product/436/32457) |
| API            | [알아보기](https://intl.cloud.tencent.com/document/product/436/7753) |

### COS Select를 사용해 로그 분석하기

COS Select 기능을 통해 COS에 저장된 로그 파일을 직접 인덱스 및 분석할 수 있습니다. 전제 조건은 로그 파일을 CSV 또는 JSON 포맷으로 저장하는 것입니다. COS Select 기능을 통해 필요한 로그 필드를 선택할 수 있으며, 이로써 COS에서 전송하는 로그 데이터양을 크게 줄여 사용 비용을 줄임과 동시에 데이터 획득 효율을 높이게 됩니다. COS Select 기능에 대한 자세한 내용은 [Select 개요](https://intl.cloud.tencent.com/document/product/436/32472)를 참고하십시오.

현재 콘솔 또는 API 방식을 통해 COS Select 기능을 사용할 수 있습니다.

| 사용 방식 | 사용 설명                                                     |
| -------- | ------------------------------------------------------------ |
| 콘솔         | [알아보기](https://intl.cloud.tencent.com/document/product/436/32538) |
| API            | [알아보기](https://intl.cloud.tencent.com/document/product/436/32360) |


