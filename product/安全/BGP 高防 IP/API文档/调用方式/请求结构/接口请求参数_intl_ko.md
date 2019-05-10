

완전한 Tencent Cloud API 요청은 두 가지의 요청 매개변수, 즉 공용 요청 매개변수와 API 요청 매개변수가 필요합니다. 본 문서는 Tencent Cloud API 요청에 필요한 API 요청 매개변수를 소개합니다. 공용 요청 매개변수 관련 상세 설명은 [공용 요청 매개변수](https://cloud.tencent.com/document/api/377/4153)를 참조하십시오.
API 요청 매개변수는 구체적인 API와 관련이 있으며, API별 지원하는 API 요청 매개변수가 다릅니다. API 요청 매개변수의 이니셜은 소문자이며 공용 요청 매개변수와 구별됩니다.
>**주의:**
>본 문서 중 매개변수는 Tencent Cloud CVM을 예로 하며 기타 Tencent Cloud 제품별 실제 매개변수는 제품 API 매개변수 설명을 참조하십시오.

아래 매개변수 리스트는 Tencent Cloud CVM [인스턴스 리스트 조회](https://cloud.tencent.com/document/api/229/831) API(DescribeInstances)를 예로 하고 있으며, 해당 API가 지원하는 API 요청 매개변수는 다음과 같습니다.

| 매개변수 이름 |   설명 | 유형 | 필수 여부 |
|---------|---------|---------|---------|
| instanceIds.n  |조회할 CVM 인스턴스 ID 배열. 배열 첨자는 0부터 시작합니다. instanceId와 unInstanceId를 사용할 수 있으며 통일된 리소스 ID:unInstanceId를 사용하길 권장합니다.| String | 아니요 |  
| lanIps.n | 조회할 CVM의 사설 IP 배열입니다. | String | 아니요 | 
| searchWord | 사용자가 설정한 CVM 별칭입니다.| String | 아니요 |
| offset |오프셋으로 기본 0입니다. |   Int | 아니요 |
| limit | 1회 최대 조회할 수 있는 서버 수량으로 기본값은 20, 최대값은 100입니다.| Int | 아니요 | 
| status | 조회 대기 중인 CVM 상태입니다.| Int | 아니요 |
| projectId | 프로젝트 ID입니다. 이 매개변수를 전달하지 않으면 전체 프로젝트의 CVM 인스턴스를 조회합니다.| String | 아니요 |
| simplify | 비실시간 데이터를 가져오기 합니다. 매개변수 전달 시 simplify=1이면 비실시간 데이터를 가져오기 합니다.| Int | 아니요 |
| zoneId |가용 영역 ID입니다. 전달하지 않으면 모든 가용 영역의 CVM 인스턴스를 조회합니다. 가용 영역을 지정해야 할 경우, [가용 영역 조회](https://cloud.tencent.com/document/api/213/15707)(DescribeAvailabilityZones) API를 호출하여 인스턴스를 조회할 수 있습니다.|  Int | 아니요 |

각 필드 설명은 다음과 같습니다.

**매개변수 이름:**해당 API에서 지원하는 요청 매개변수 이름으로 사용자는 이 API를 호출할 때 API 요청 매개변수로 사용할 수 있습니다. 매개변수 이름이 `“.n”`으로 끝날 경우, 이 매개변수는 1개의 배열을 의미하며, 사용할 때 순서에 따라 배열 매개변수를 전달해야 합니다.
**필수 항목:**이 매개변수는 필수 여부를 표시합니다. "네"는 해당 API를 호출하려면 반드시 이 매개변수를 전달해야 하고, "아니요"는 잔달하지 않아도 됨을 의미합니다.
**유형:**이 API의 매개변수의 데이터 유형입니다.
**설명:**이 API 요청 매개변수에 대해 간략하게 설명합니다.

### 사용 사례
Tencent Cloud 제품 API 요청 링크에서 API 요청 매개변수 형식은 다음과 같습니다. Tencent Cloud CVM을 예로, 사용자가 조정 그룹 리스트를 조회해야 할 경우, 요청 링크 형식은 다음과 같습니다.

<pre>
https://cvm.api.qcloud.com/v2/index.php?
&<공용 요청 매개변수>
&instanceIds.0=ins-0hm4gvho
&instanceIds.1=ins-8oby8q00
&offset=0
&limit=20
&status=2
&zoneId=100003
</pre>


