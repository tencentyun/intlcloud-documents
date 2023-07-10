COS(Cloud Object Storage)는 액세스 빈도 및 재해 복구 수준이 다른 객체에 대해 MAZ_STANDARD, MAZ_STANDARD_IA, MAZ_INTELLIGENT TIERING, INTELLIGENT TIERING, STANDARD, STANDARD_IA, ARCHIVE 및 DEEP ARCHIVE 스토리지 클래스를 제공합니다. 활성 객체가 COS에 있는 방법을 나타내며 액세스 빈도, 내구성, 가용성, 대기 시간 등이 서로 다릅니다. 필요에 따라 객체를 업로드할 스토리지 클래스를 선택할 수 있습니다.

> !
> - 객체를 업로드할 때, 스토리지 유형을 설정하지 않으면 기본적으로 **STANDARD**에 업로드됩니다.
> - 다중 AZ에 대한 자세한 내용은 [Overview of Multi-AZ Feature](https://intl.cloud.tencent.com/document/product/436/35208)를 참고하십시오.
> 

## MAZ_STANDARD/STANDARD

MAZ_STANDARD 및 STANDARD 스토리지 클래스는 모두 핫 데이터용으로 설계된 매우 안정적이고 사용 가능하며 강력한 객체 스토리지 서비스이며 낮은 대기 시간과 높은 처리량을 특징으로 합니다.

MAZ_STANDARD는 STANDARD보다 데이터 내구성과 서비스 가용성이 높습니다. 동일한 리전의 다른 데이터 센터에 데이터를 저장하기 위해 다른 스토리지 메커니즘을 사용하여 한 데이터 센터의 장애가 전체 서비스에 영향을 미치지 않도록 방지하고 비즈니스 안정성을 더욱 보장합니다.

**적용 시나리오**

인기 동영상, 소셜 이미지, 모바일 앱, 게임 프로그램 및 정적 웹사이트를 포함하여 많은 핫스팟 파일 또는 빈번한 데이터 액세스와 관련된 시나리오에 적합합니다.

STANDARD 스토리지 클래스는 일반적인 사용을 위해 설계되었으며 대부분의 사용 사례를 다룹니다. MAZ_STANDARD보다 비용 효율적입니다.

그러나 MAZ_STANDARD는 데이터 내구성과 서비스 가용성이 더 높기 때문에 키 파일, 상업 데이터 및 민감한 정보를 포함하여 요구 사항이 더 높은 비즈니스 시나리오에 적합합니다.

## MAZ_STANDARD_IA/STANDARD_IA

MAZ_STANDARD_IA 및 STANDARD_IA 스토리지 클래스는 스토리지 비용과 액세스 대기 시간이 낮은 매우 안정적인 객체 스토리지 서비스입니다. 저렴한 가격으로 밀리초 단위로 첫 번째 바이트에 액세스할 수 있으므로 기다리지 않고 신속하게 데이터를 검색할 수 있습니다. STANDARD와 달리 데이터에 액세스할 때 데이터 검색 요금이 부과됩니다.

MAZ_STANDARD_IA는 STANDARD_IA와 다른 스토리지 메커니즘을 사용하여 동일한 리전의 다른 데이터 센터에 데이터를 저장하여 한 데이터 센터의 장애가 전체 서비스에 영향을 미치지 않도록 방지하고 비즈니스 안정성을 한층 더 보장합니다.

**적용 시나리오**

클라우드 디스크 데이터, 빅데이터 분석, 정부 및 기업 데이터, 빈도가 낮은 아카이브, 모니터링 데이터 등 액세스 빈도가 낮은(예: 월 1 - 2회) 시나리오에 적합합니다.

>! MAZ_STANDARD_IA 및 STANDARD_IA 모두 최소 스토리지 요구 사항이 있습니다. 보관 기간이 30일 미만인 경우 청구서는 30일로 계산됩니다. 마찬가지로 파일 크기가 64KB 미만인 경우 요금은 64KB로 계산됩니다(파일 크기가 64KB보다 크거나 같으면 실제 파일 크기를 기준으로 요금이 계산됨). 자세한 내용은 [가격 | Cloud Object Storage](https://buy.cloud.tencent.com/price/cos?lang=en&pg=)를 참고하십시오.
>

## MAZ_INTELLIGENT TIERING/INTELLIGENT TIERING

MAZ_INTELLIGENT TIERING 스토리지 클래스의 객체는 MAZ_STANDARD 및 MAZ_STANDARD_IA의 두 스토리지 레이어에 저장할 수 있습니다. INTELLIGENT_TIERING 스토리지 클래스의 객체는 STANDARD 및 STANDARD_IA의 두 스토리지 클래스에도 저장할 수 있습니다. COS는 데이터 검색 요금 발생 없이 객체의 액세스 빈도에 따라 스토리지 클래스 간에 자동으로 전환하므로 스토리지 요금이 절감됩니다. 자세한 내용은 [INTELLIGENT TIERING 개요](https://intl.cloud.tencent.com/document/product/436/38305)를 참고하십시오.

MAZ_INTELLIGENT TIERING은 INTELLIGENT TIERING과 다른 스토리지 메커니즘을 사용하여 동일한 리전의 여러 데이터 센터에 데이터를 저장하여 한 데이터 센터의 장애가 전체 서비스에 영향을 미치지 않도록 방지하고 비즈니스 안정성을 더욱 보장합니다.

**적용 시나리오**

데이터 액세스 패턴이 불확실한 시나리오에 적합합니다. 비즈니스에서 비용을 엄격하게 제어하고 파일 읽기 성능에 덜 민감한 경우 MAZ_INTELLIGENT TIERING 또는 INTELLIGENT TIERING을 사용하여 비용을 줄일 수 있습니다.

>! MAZ_INTELLIGENT TIERING 및 INTELLIGENT_TIERING의 경우 객체는 실제 크기를 기준으로 요금이 과금됩니다. 가격 책정에 대한 자세한 내용은 [가격 | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)를 참고하십시오.
>

## ARCHIVE

COS ARCHIVE는 콜드 데이터용으로 설계된 매우 안정적인 객체 스토리지 서비스로 스토리지 비용이 매우 낮고 데이터 장기 보존이 가능합니다. 이 스토리지 클래스의 최소 스토리지 기간은 90일입니다. ARCHIVE에 저장된 데이터를 읽기 위해서는 먼저 STANDARD로 복원해야 합니다.

COS는 ARCHIVE에 대해 다음 세 가지 복구 모드를 지원합니다.

- 고속 검색 모드: 1-5분 이내에 객체를 복구합니다.
- 일반 검색 모드: 3 - 5시간 이내에 객체를 복구합니다.
- 대량 검색 모드: 5 - 12시간 이내에 여러 객체를 복구합니다.                      

>? 
> - 객체 복구에 대한 자세한 내용은 [아카이브 객체 복구](https://intl.cloud.tencent.com/document/product/436/30961)를 참고하십시오.
> - 데이터 복구 요청에는 QPS 제한이 있으며, 100회/초로 제한됩니다.
> 

**적용 시나리오**

보관 데이터, 의료 영상, 과학 데이터 등 컴플라이언스 파일 보관, 라이프사이클 파일 보관, 작업 로그 보관, 원격 재해 복구 등 데이터를 장기간 저장해야 하는 시나리오에 적합합니다.

>! ARCHIVE에는 최소 스토리지 요구 사항이 있습니다. 보관 기간이 90일 미만인 경우 청구서는 90일로 계산됩니다. 마찬가지로 파일 크기가 64KB 미만인 경우 요금은 64KB로 계산됩니다(파일 크기가 64KB보다 크거나 같으면 실제 파일 크기를 기준으로 요금이 계산됨). 자세한 내용은 [가격 | Cloud Object Storage](https://buy.cloud.tencent.com/price/cos?lang=en&pg=)를 참고하십시오.
>

## DEEP ARCHIVE

COS DEEP ARCHIVE는 가장 낮은 스토리지 비용과 장기 데이터 보관을 제공하는 매우 안정적인 객체 스토리지 서비스입니다. 이 스토리지 클래스의 최소 보관 기간은 180일입니다. DEEP ARCHIVE에 저장된 데이터를 읽으려면 먼저 STANDARD로 복구해야 합니다. 자세한 내용은 [DEEP ARCHIVE 소개](https://intl.cloud.tencent.com/document/product/436/38304)를 참고하십시오.

COS는 DEEP ARCHIVE에 대해 다음 두 가지 복구 모드를 지원합니다.

- 일반 검색 모드: 12 - 24시간 이내에 객체를 복구합니다.
- 대량 검색 모드: 24 - 48시간 이내에 여러 객체를 복구합니다. 

>? 데이터 복구 요청에는 QPS 제한이 있으며, 100회/초로 제한됩니다.
>

**적용 시나리오**

의료 영상, 뷰 데이터, 로그 데이터와 같은 장기 저장이 필요한 비즈니스 시나리오에 사용됩니다.

>! DEEP ARCHIVE는 최소 스토리지 요구 사항이 있습니다. 보관 기간이 180일 미만인 경우 청구서는 180일로 계산됩니다. 마찬가지로 파일 크기가 64KB 미만인 경우 요금은 64KB로 계산됩니다(파일 크기가 64KB보다 크거나 같으면 실제 파일 크기를 기준으로 요금이 계산됨). 자세한 내용은 [가격 | Cloud Object Storage](https://buy.cloud.tencent.com/price/cos?lang=en&pg=)를 참고하십시오.
>

## 스토리지 유형 비교

| 비교 항목           | MAZ_STANDARD<br>    | MAZ_STANDARD_IA<br>     |  MAZ_INTELLIGENT TIERING<br>    | INTELLIGENT TIERING<br>                                        | STANDARD           | STANDARND_IA                     | ARCHIVE                                     | DEEP ARCHIVE                                                 |
| ---------------- | ------------------------ | ------------------------ | ---------------- | ------------------------------------------------------- | ------------------ | ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
|   스토리지 클래스 매개변수   |   MAZ_STANDARD    |  MAZ_STANDARD_IA  |  MAZ_INTELLIGENT_TIERING  |  INTELLIGENT_TIERING  |  STANDARD  |  STANDARD_IA  |  ARCHIVE  | DEEP_ARCHIVE   |
| 데이터 내구성       | 99.9999999<br>999%       | 99.9999999<br>999%           | 99.9999999<br>999%           |    99.9999999<br>99%                                       | 99.9999999<br>99%  | 99.9999999<br>99%            | 99.9999999<br>99%                                            | 99.9999999<br>99%                                            |
| 서비스 가용성       | 99.995%                   | 99.995%                       |  99.995%                       |  99.99%                                                  | 99.95%             | 99.9%                        | 99.9%                                                        | 99.9%                                                        |
| 응답             | 밀리초                   | 밀리초            | 밀리초              | 밀리초                                                  | 밀리초             | 밀리초                       | 다음 세 가지 복구 모드 중 하나를 사용하여 미리 복구해야 합니다. <ul  style="margin: 0;"><li>고속 검색 모드: 1 - 5분 이내에 객체를 복구합니다. </li><li>일반 검색 모드: 3 - 5시간 이내에 객체를 복구합니다. </li><li>대량 검색 모드: 5 - 12시간 이내에 여러 객체를 복구합니다. </li></ul> | 두 가지 복원 모드 중 하나를 사용하여 미리 복원해야 합니다. <ul  style="margin: 0;"><li>일반 검색 모드, 12 - 24시간 이내에 객체를 복구합니다.</li><li>대량 검색 모드, 24 - 48시간 내에 여러 객체를 복구합니다.</li></ul> |
| 과금 가능한 최소 객체 크기 | 실제 객체 크기로 계산       | 64KB               | 실제 객체 크기로 계산            | 실제 객체 크기로 계산 | 실제 객체 크기로 계산 | 64KB                         | 64KB                                                         | 64KB                                                         |
| 최소 보관 기간     | 제한 없음                   | 30일             | 제한 없음                 | 제한 없음                                                    | 제한 없음             | 30일                         | 90일                                                         | 180일                                                        |
| 지원 리전         | 베이징, 상하이, 광저우, 중국홍콩, 싱가포르만 해당 | 베이징, 상하이, 광저우, 중국홍콩, 싱가포르만 해당    | 베이징, 상하이, 광저우, 싱가포르만 해당     | 베이징, 난징, 상하이, 광저우, 청두, 충칭, 도쿄, 싱가포르만 해당                    | 모든 리전           | 모든 리전                     | 자카르타를 제외한 모든 공유 클라우드 리전                                           | 베이징, 난징, 상하이, 광저우, 청두, 충칭, 도쿄, 싱가포르만 해당                         |
| 스토리지 요금         | 비교적 높음                     | 비교적 높음                | 인텔리전트 티어링 후 스토리지 클래스에 따라 다름            | 인텔리전트 티어링 후 스토리지 클래스에 따라 다름                                  | 표준               | 낮음                           | 매우 낮음                                                         | 매우 낮음                                                         |
| 데이터 검색 요금     | 없음                       | 비교적 낮음, 실제 읽은 데이터 양에 따라 과금   | 없음       | 없음                                                      | 없음                 | 비교적 낮음, 실제 읽은 데이터 양에 따라 과금 | 비교적 높음, 복구 모드에 따라 실제 복구된 데이터 양으로 과금           | 높음, 복구 모드에 따라 실제 복구된 데이터 양으로 과금             |
| 요청 요금         | 일반                     | 비교적 높음                 | 비교적 높음, 또한 INTELLIGENT TIERING 객체 모니터링 요금이 과금됨               | 비교적 높음, 또한 INTELLIGENT TIERING 객체 모니터링 요금이 과금됨                    | 표준               | 비교적 높음                         | 일반(데이터를 먼저 STANDARD로 복구해야 함)                                 | 높음(데이터를 먼저 STANDARD로 복구해야 함). DEEP ARCHIVED 데이터를 검색하려면 데이터 검색에 대한 요청 요금이 발생함 |
| 데이터 처리         | 지원                     | 지원            | 지원                  | 지원                                                    | 지원               | 지원                         | 지원(먼저 데이터 복구 필요)                                             | 지원(먼저 데이터 복구 필요)                                             |

## 스토리지 유형의 전환

COS는 활성 객체가 COS에 있는 방식을 나타내는 다양한 스토리지 유형을 제공합니다. 여전히 필요에 따라 객체의 스토리지 유형을 변경하거나 객체를 STANDARD_IA, ARCHIVE 또는 DEEP ARCHIVE와 같은 덜 활성화된 스토리지 유형으로 전환할 수 있습니다.

>?
> - 객체를 전환할 때 객체가 상주하는 리전에 대해 대상 스토리지 유형이 지원되는지 확인하십시오.
> - **ARCHIVE/DEEP ARCHIVE**에 저장된 객체의 스토리지 유형을 수정하려면 먼저 STANDARD로 복구해야 합니다. 자세한 내용은 [아카이브된 객체 복구](https://intl.cloud.tencent.com/document/product/436/30961)를 참고하십시오.
> 

각 스토리지 유형을 전환하는 방법은 다음과 같습니다.

| 스토리지 유형              | 변경 가능한 스토리지 유형                                             | 전환 가능한 스토리지 유형과 전환 우선순위                                 |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| MAZ_STANDARD     | MAZ_STANDARD_IA, MAZ_INTELLIGENT TIERING                    | MAZ_STANDARD > MAZ_STANDARD_IA > MAZ_INTELLIGENT TIERING |
| MAZ_STANDARD_IA     | MAZ_STANDARD, MAZ_INTELLIGENT TIERING                     | MAZ_STANDARD_IA > MAZ_INTELLIGENT TIERING                                                     |
| MAZ_INTELLIGENT TIERING | MAZ_STANDARD, MAZ_STANDARD_IA                         | 없음                                                           |
| INTELLIGENT TIERING          | STANDARD, STANDARD_IA, ARCHIVE, DEEP ARCHIVE                   | INTELLIGENT TIERING > ARCHIVE > DEEP ARCHIVE                       |
| STANDARD              | INTELLIGENT TIERING, STANDARD_IA, ARCHIVE, DEEP ARCHIVE               | STANDARD > STANDARD_IA > INTELLIGENT TIERING > ARCHIVE > DEEP ARCHIVE |
| STANDARD_IA              | INTELLIGENT TIERING, STANDARD, ARCHIVE, DEEP ARCHIVE               | STANDARD_IA > INTELLIGENT TIERING > ARCHIVE > DEEP ARCHIVE            |
| ARCHIVE              | INTELLIGENT TIERING, STANDARD, STANDARD_IA, DEEP ARCHIVE (복구 후) | ARCHIVE > DEEP ARCHIVE                                      |
| DEEP ARCHIVE          | INTELLIGENT TIERING, STANDARD, STANDARD_IA, ARCHIVE (복구 후)   | 없음                                                           |


구체적인 작업 가이드는 다음 문서를 참고하십시오.

- [스토리지 유형 수정](https://intl.cloud.tencent.com/document/product/436/30930) 
- [라이프사이클 설정](https://intl.cloud.tencent.com/document/product/436/14605) 



