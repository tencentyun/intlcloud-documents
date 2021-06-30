## 소개

파일을 INTELLIGENT TIERING 유형으로 지정하여 보관하면, COS에서 데이터의 액세스 모드에 따라 데이터의 핫/콜드 티어링 레이어를 자동 전환하며, 스토리지 비용을 절감할 수 있습니다.

INTELLIGENT TIERING은 액세스 모드가 가변적이거나 데이터의 액세스 모드를 예측할 수 없는 경우에 활용할 수 있습니다. 표준 스토리지와 동일한 수준의 낮은 딜레이와 높은 처리량을 제공하지만, 비용은 표준 스토리지보다 저렴합니다. 비즈니스 요구사항에 맞춰 액세스 모드가 가변적인 데이터를 표준 스토리지 유형에서 INTELLIGENT TIERING 유형으로 전환하여 클라우드 내 스토리지 비용을 절약할 수 있습니다.

INTELLIGENT TIERING의 소개와 지원 리전에 대한 자세한 내용은 [INTELLIGENT TIERING 소개](https://intl.cloud.tencent.com/document/product/436/38305) 문서를 참조하십시오.

>!
>
>- INTELLIGENT TIERING 유형 데이터의 스토리지 요금은 두 가지 상황으로 구분됩니다.
 - 데이터가 고빈도 액세스 레이어에 속하는 경우, 스토리지 요금은 표준 스토리지 정가와 동일합니다.
 - 데이터가 저빈도 액세스 레이어에 속하는 경우, 스토리지 요금은 표준IA 스토리지 정가와 동일합니다.
>- INTELLIGENT TIERING의 요청 요금은 표준 스토리지의 가격과 동일하며, 트래픽, 관리 기능 요금의 가격은 지원 리전의 다른 스토리지 유형과 동일하고, 데이터 검색 요금은 부과되지 않습니다. 이외에도 INTELLIGENT TIERING 데이터는 객체 모니터링 요금이 별도로 부과됩니다. 자세한 과금 정보는 [제품 가격](https://buy.cloud.tencent.com/price/cos)을 참조하십시오.



## 작업 순서

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인한 뒤, 왼쪽 메뉴바에서 [버킷 리스트]를 클릭하여 버킷 리스트 페이지로 이동합니다.
2. INTELLIGENT TIERING 설정이 필요한 버킷을 찾아 이름을 클릭하여 버킷 관리 페이지로 이동합니다.
3. [기본설정]>[INTELLIGENT TIERING]을 클릭하여 INTELLIGENT TIERING 설정 항목을 찾은 다음 [편집]을 클릭하여 현재 상태를 열고, 아래의 설정 항목 설명에 따라 설정하십시오.
   **전환 기간**: 해당 매개변수는 저빈도 액세스 레이어로 전환하는 기간 지정에 사용됩니다. 30일, 60일, 90일을 선택할 수 있습니다. 예를 들어 30일을 선택한 경우, 연속 30일간 액세스하지 않으면 고빈도 액세스 레이어에서 저빈도 액세스 레이어로 객체가 이동됩니다.
    ![](https://main.qcloudimg.com/raw/97f9f450c62c3f914235019c08a604fe.png)
4. 설정 정보를 확인한 후 저장을 클릭합니다. 주의: **INTELLIGENT TIERING 설정을 완료한 후에는 해당 설정을 비활성화 또는 일시 중지할 수 없습니다**.
<img src="https://main.qcloudimg.com/raw/77f8f6416d5929025fe2d1e46afcc630.png" width="30%"></img>
5. INTELLIGENT TIERING 설정을 활성화한 후 [파일 리스트]를 클릭합니다. 리디렉션 인터페이스에서 [파일 업로드]를 클릭한 후 업로드할 파일을 선택합니다.
6. [다음 단계]를 클릭하여 객체 속성을 설정합니다. 스토리지 유형 설정 항목에서 **INTELLIGENT TIERING**을 선택한 뒤 [업로드]를 클릭하면 객체가 INTELLIGENT TIERING 유형으로 업로드되며, COS에서 데이터 스토리지 레이어를 자동 전환합니다. 업로드와 관련된 설정 항목에 대한 내용은 [객체 업로드](https://intl.cloud.tencent.com/document/product/436/13321)를 참조하십시오.



