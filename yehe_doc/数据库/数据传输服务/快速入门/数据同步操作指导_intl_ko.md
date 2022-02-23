## 관련 정보

- [데이터 동기화 개요](https://intl.cloud.tencent.com/document/product/571/42667).
- [데이터 동기화에서 지원하는 데이터베이스](https://intl.cloud.tencent.com/document/product/571/42579).

## 전체 프로세스

| **작업 프로세스**              | **설명**                                                     |
| ------------------------- | ------------------------------------------------------------ |
| 1. 준비 작업               | 데이터 동기화 작업을 생성하기 전에 환경 요구 사항을 충족하도록 원본 및 대상 데이터베이스와 네트워크 환경을 [준비](https://intl.cloud.tencent.com/document/product/571/42652)해야 합니다. |
| 2. 데이터 동기화 작업 만들기       | 이 섹션에서는 기본 동기화 작업 예시만 제공합니다. 더 많은 시나리오는 [데이터 동기화](https://intl.cloud.tencent.com/document/product/571/42624)를 참고하십시오. |
| 3. 동기화 진행률 조회 또는 기타 작업 수행 | <li>전체 동기화 진행률을 확인하고 [작업 관리](https://intl.cloud.tencent.com/document/product/571/42620)의 지침에 따라 확인 및 재시도와 같은 작업을 수행할 수 있습니다.<li>[모니터링 메트릭 조회](https://intl.cloud.tencent.com/document/product/571/42606)에 따라 다양한 데이터 동기화 메트릭를 조회할 수 있습니다.</li> |
| 4. 동기화 항목 비교 및 작업 중지   | 동기화 작업 완료 후 원본 데이터베이스와 대상 데이터베이스의 내용이 동일한지 확인하고 작업 중지의 지침에 따라 수동으로 동기화 [작업 중지](https://intl.cloud.tencent.com/document/product/571/42616)합니다. |

## 데이터 동기화 작업 예시

1. [데이터 동기화 구매 페이지](https://buy.cloud.tencent.com/dts)에 로그인하여 알맞은 설정을 선택하고 **즉시 구매**를 클릭합니다.
2. 구매 성공 후 [데이터 동기화 목록](https://console.cloud.tencent.com/dts/replication)으로 돌아가면 새로 생성된 데이터 동기화 작업을 볼 수 있습니다. 사용하기 전에 설정해야 합니다.
3. 데이터 동기화 목록의 **작업** 열에서 **설정**을 클릭하여 동기화 작업 설정 페이지로 들어갑니다.
![](https://qcloudimg.tencent-cloud.cn/raw/afe583b0dd3569cad36da0f3f19acba0.png)
4. 동기화 작업 설정 페이지에서 원본 인스턴스와 대상 인스턴스를 설정하고 해당 계정 및 비밀번호를 설정한 뒤 연결성 테스트를 하고 **다음 단계**를 클릭합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/dcad48b082c4bfc8bc25b2aff7a0f579.png"  style="margin:0;">
5. 동기화 옵션 및 객체 설정 페이지에서 데이터 초기화, 데이터 동기화 및 객체 동기화 옵션을 설정하고 **저장 후 다음으로 이동**을 클릭합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/a8df8150f387ffd56e11f60a6384adba.png"  style="margin:0;">
<strong>데이터베이스/테이블 매핑</strong>: 선택한 객체의 우측에 마우스를 대면 편집 아이콘이 표시됩니다. 클릭 후 팝업창에 매핑 이름을 입력합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/fb3dfa032310e444729a805b503e019b.png"  style="margin:0;">
6. 확인 작업 페이지에서 확인을 완료하고 모든 점검 항목이 통과되면 **작업 실행**을 클릭합니다.
>?확인 결과에 알람이 표시되면 작업 시작에 영향을 미치지 않지만 **세부 정보 보기**를 클릭하여 조정 제안을 받는 것이 좋습니다.
>
![](https://qcloudimg.tencent-cloud.cn/raw/898e1d8ced68446dfd3e889fb77d7011.png)
7. 데이터 동기화 작업 리스트로 돌아가면 작업이 **실행 중** 상태가 됩니다.
>?**작업** 열에서 **더보기** > **중지**를 클릭하여 동기화 작업을 중지할 수 있습니다. 작업을 중지하기 전에 데이터 동기화가 완료되었는지 확인해야 합니다.
>
![](https://qcloudimg.tencent-cloud.cn/raw/058cf11d354d64ae32e881a421e0d686.png)

