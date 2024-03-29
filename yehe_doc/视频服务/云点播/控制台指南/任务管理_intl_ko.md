## 작업 시나리오

작업 관리를 통해 사용자는 VOD에서 작업 처리의 진행 상황을 확인하고 작업 진행률 및 세부 사항을 조회할 수 있습니다. 작업 관리는 실행된 작업의 내역만 표시하며, 72시간 작업 처리 상태 및 작업 상세 내역만 지원됩니다.

### 작업 기본 정보

VOD 콘솔에 로그인하여 [[작업 관리](https://console.cloud.tencent.com/vod/task)]를 선택하면 기본적으로 ‘작업 관리’ 페이지로 이동됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/21f4bcbaf40ed173d1ad4444dd7ba36b.png)
기본 작업 정보:

| 필드         | 설명                     |
| ---------- | ---------------------- |
| 작업ID       | 작업이 실행된 후 생성되는 고유 작업 ID |
| 작업 상태       |  <li>대기 중: 작업이 아직 대기열에 있음을 나타냅니다.</li><li>완료됨: 작업이 완료되었음을 나타냅니다. 작업 실패 및 작업 완료는 완료됨 상태에 속합니다.</li><li>처리 중: 작업이 처리 중임을 나타냅니다.</li>     |
| 작업 생성 시간     | 작업이 생성된 시간           |
| 작업 실행 시간     | 작업의 실제 실행 시간         |
| 작업 완료 시간| 작업이 완료된 시간           |
| 작업         | 작업의 서브 작업 유형 및 작업 상태    |

### 서브 작업의 기본 정보
서브 작업의 기본 정보를 클릭하면 작업의 서브 작업 세부 정보를 쿼리할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/91599f6f274cdb336499d524c727446e.png)
서브 작업의 기본 정보:

| 필드      | 설명                                      |
| ------- | --------------------------------------- |
| FileId  | 해당 작업에서 작업을 수행하는 미디어 자산의 FileId                |
| 파일 이름    | FileId에 해당하는 파일 이름                      |
| 작업 유형    | 이 FileId의 작업 유형으로 비디오 처리, 비디오 심사, 콘텐츠 분석 및 콘텐츠 인식 포함 |
| 작업 상태    | <li>처리 중</li><li>완료</li>                                 |
| 서브 작업|  작업에 속한 FileId의 서브 작업 이름               |
