## 작업 시나리오
다중 사이트 활성-활성 IDC 아키텍처는 서로 다른 리전에 배포되어 동시에 서비스를 제공하는 여러 IDC를 나타냅니다. 데이터는 실시간으로 그들 사이에서 동기화될 수 있습니다. IDC에서 재해가 발생하면 해당 트래픽을 다른 IDC로 라우팅하여 빠른 리전 간 장애 조치를 구현하고 비즈니스 연속성을 보장할 수 있습니다.

다중 사이트 활성-활성 IDC 아키텍처는 각각 두 개의 단방향 동기화 작업으로 구성된 여러 양방향 동기화 작업을 생성하여 구현됩니다. 따라서 단방향 동기화 및 관련 작업에 대한 제한 사항을 따라야 합니다. 자세한 내용은 [데이터 동기화](https://intl.cloud.tencent.com/document/product/571/42579)에서 적절한 동기화 시나리오를 참고하십시오.

## 주의 사항
- 전체 데이터 동기화 중에 DTS는 특정 원본 데이터베이스 리소스를 사용하므로 원본 데이터베이스의 로드와 압력이 증가할 수 있습니다. 데이터베이스 구성이 낮으면 사용량이 적은 시간에 데이터를 동기화하는 것이 좋습니다.
- 데이터 중복을 방지하려면 동기화할 테이블에 기본 키 또는 null이 아닌 고유 키가 있어야 합니다.
- 데이터를 미리 계획해야 합니다. 각 IDC는 기본 키 충돌 및 동일한 기본 키로 데이터의 상호 덮어쓰기와 같은 문제를 방지하기 위해 서로 다른 기본 키로 데이터를 업데이트(추가, 삭제 및 수정)할 책임이 있습니다. 비즈니스 상의 이유로 여러 원본 데이터베이스에 중복 기본 키가 있는 경우 적절한 충돌 해결 방법을 선택하여 동기화 동작과 데이터가 기대치를 충족하도록 합니다.

## 제한
- 여러 동기화 작업의 구성에서 DDL 문은 원형 링크를 형성하지 않아야 합니다.
- 현재 MySQL, TDSQL-C(MySQL 버전 호환) 또는 양자 간의 양방향 동기화 작업만 지원됩니다.

## DDL 설정 원칙
본문은 구체적인 시나리오를 통해 DDL 문을 구성하는 방법을 더 쉽게 설명합니다. 예시 중 다중 사이트 활성-활성-활성 IDC 아키텍처에서 A<->B, B<->C 및 C<->A의 세 가지 양방향 동기화 작업이 데이터베이스 A(베이징 리전), B(상해 리전) 및 C(광저우 리전) 간에 생성됩니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/bddef945c4316f902bfe5da564c827c7.png" style="zoom:40%;" />

- 여러 동기화 작업의 구성에서 DDL 문은 원형 링크를 형성해서는 안 됩니다. 그렇지 않으면 시스템에서 반복되어 오류가 발생합니다.
  예시: 아래 그림의 파란색 라인 1, 3, 5의 3가지 동기화 작업 중 DDL은 최대 2개의 동기화 작업에서만 선택할 수 있으며, 3개를 선택하면 원형 링크가 형성됩니다.

- 동일한 DB 테이블 객체는 여러 데이터 센터에서 DDL 동기화를 수신할 수 없습니다. 여러 데이터 센터의 DDL이 타깃에서 충돌하여 오류가 발생할 수 있기 때문입니다.
  예시: 인스턴스 A와 C의 동일한 이름을 가진 테이블은 인스턴스 B와 동기화해야 합니다. 동기화 작업 1과 4에서 하나의 작업에서만 DDL을 선택할 수 있습니다.
  
- 확인하는 동안 동기화 시스템은 생성 중인 동기화 작업이 다른 모든 동기화 작업을 기반으로 DDL 루프 또는 충돌을 일으킬 것인지 판단하고 참고를 위한 프롬프트를 제공합니다.

## 일반적인 사용 사례를 위한 권장 구성
다중 사이트 활성-활성 IDC 아키텍처는 각각 두 개의 단방향 동기화 작업으로 구성된 여러 양방향 동기화 작업을 생성하여 구현됩니다. 따라서 이러한 아키텍처에서 각 동기화 작업의 동작 단계는 기본적으로 일반적인 단방향 동기화 작업의 단계와 동일합니다. 다음 구성에서만 다릅니다.
<dx-fold-block title="동기화 옵션 설정 차이">
<img src="https://qcloudimg.tencent-cloud.cn/raw/448645a136cbac9f8d499493cefd0a57.png" style="zoom:80%;" />
</dx-fold-block>


<br>본문은 참고용으로 일반적인 다중 사이트 활성-활성 IDC 아키텍처에 대해 다음 구성을 권장합니다.

예를 들어, 다중 사이트 활성-활성-활성 IDC 아키텍처에서 데이터베이스 A(베이징 리전), B(상하이 리전) 및 C(광저우 리전) 간에 세 가지 양방향 동기화 작업이 생성됩니다. A<->B (작업1 및 2), B<->C(작업3 및 4) 및 C<->A(작업5 및 6).

<table>
<tr><th width="16%">시나리오</th> <th width="17%">시간 요건</th> <th width="9%">동기화 작업</th><th width="14%">초기화 유형</th><th width="14%">대상이 이미 있는 경우</th><th width="16%">충돌 해결 방법</th><th width="18%">동기화 작업 유형</th></tr>
<tr>
<td rowspan="6">시나리오1: 데이터베이스 A에는 데이터베이스/테이블 구조와 데이터가 있고 데이터베이스 B와 C는 비어 있습니다.</td><td rowspan="2">작업2는 작업1이 ‘증분 동기화’ 단계에 들어간 후에만 생성할 수 있습니다.</td><td>작업1</td><td>구조 초기화 + 전체 데이터 초기화</td><td>사전 확인 및 오류 보고</td><td rowspan="7">필요에 따라 옵션을 선택합니다. 충돌 해결 방법은 기본 키 충돌이 있는 데이터에만 적용됩니다.</td><td rowspan="7">DDL은 설정 원칙을 참고하여 선택하며 다른 작업 유형은 다른 여러 작업 간에 일관성을 유지하십시오.</td></tr>
<tr>
<td>작업2</td><td>선택하지 않음</td><td>무시하고 실행</td></tr>
<tr>
<td rowspan="2">작업4는 작업3이 ‘증분 동기화’ 단계에 들어간 후에만 생성할 수 있습니다.</td><td>작업3</td><td>구조 초기화 + 전체 데이터 초기화</td><td>사전 확인 및 오류 보고</td></tr>
<tr>
<td>작업4</td><td>선택하지 않음</td><td>무시하고 실행</td></tr>
<tr>
<td rowspan="2">작업6은 작업5가 "증분 동기화" 단계에 들어간 후에만 생성할 수 있습니다.</td><td>작업5</td><td>구조 초기화 + 전체 데이터 초기화</td><td>사전 확인 및 오류 보고</td></tr>
<tr>
<td>작업6</td><td>선택하지 않음</td><td>무시하고 실행</td></tr>
 <tr>
<td>시나리오2: 데이터베이스 A, B 및 C에 모두 데이터베이스/테이블 구조 및 데이터가 있습니다.</td><td>없음</td><td>작업1-6</td><td>전체 데이터 초기화</td><td>무시하고 실행</td></tr>
</table>

## 작업 단계
다중 사이트 활성-활성 IDC 아키텍처를 만드는 것은 여러 양방향 동기화 작업을 만드는 것입니다. 자세한 지침은 [양방향 동기화 데이터 구조 생성](https://intl.cloud.tencent.com/document/product/571/42605)을 참고하십시오.
