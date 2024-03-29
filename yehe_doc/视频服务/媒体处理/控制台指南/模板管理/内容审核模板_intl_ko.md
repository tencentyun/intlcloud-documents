1.  MPS(Media Processing Service)는 스킴에 직접 추가할 수 있는 사전 설정 심사 템플릿을 제공합니다. **템플릿 생성**을 클릭하여 자신만의 심사 템플릿을 맞춤 설정할 수도 있습니다.

	- 템플릿 이름: 중국어, 영어, 숫자, 스페이스, 언더바(\_), 대시(-), 마침표(.)만 지원되며, 최대 64자까지 입력할 수 있습니다.
	- 심사 항목: 심사 항목은 이미지 인식, 음성인식, 광학 문자 인식이 있으며, 선택하면 심사 서브 항목이 오른쪽 선택란에 표시됩니다.

<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th >심사 항목</th>
<th nowrap="nowrap">심사 항목</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan = 3 nowrap="nowrap">이미지 인식</td>
<td>반감을 일으키는 정보</td>
<td>반감을 일으키는 정보, 저속, 선정적, 성적 행위 항목 심사</td>
</tr>
<tr>
<td>테러 콘텐츠</td>
<td>유혈 장면, 폭발 및 화재</td>
</tr>
<tr>
<td>불쾌감을 일으키는 정보</td>
<td>금지된 아이콘, 스포츠 및 엔터테인먼트 업계의 유명인</td>
</tr>
<tr>
<td rowspan = 2>음성인식</td>
<td>반감을 일으키는 정보</td>
<td>금지된 아이콘, 반감을 일으키는 정보</td>
</tr>
<tr>
<td>불쾌감을 일으키는 정보</td>
<td>금지된 아이콘, 불쾌감을 일으키는 정보</td>
</tr>
<tr>
<td rowspan = 2>텍스트 인식</td>
<td>반감을 일으키는 정보</td>
<td>금지된 아이콘, 반감을 일으키는 정보</td>
</tr>
<tr>
<td>불쾌감을 일으키는 정보</td>
<td>금지된 아이콘, 불쾌감을 일으키는 정보</td>
</tr>
</tbody></table>

2. 각 서브 항목에 대해 **확인 임계값** 및 **의심 임계값**을 설정하여, 심사의 강도를 결정할 수 있습니다. 비워 두면 기본값이 사용됩니다.
 - **확인 임계값**: MPS는 업로드된 비디오를 분석하여 확인 점수를 부여합니다. 비디오의 점수가 확인 임계값을 초과하면 비디오가 확인된 것으로 표시됩니다. 임계값 범위는 0 - 100입니다. 기본값이 권장됩니다.
 - **의심 임계값**: MPS는 업로드된 비디오를 분석하여 의심 점수를 부여합니다. 비디오 점수가 의심 임계값을 초과하면 비디오가 의심스러운 것으로 표시됩니다. 비디오 심사 페이지에서 의심스러운 비디오에 대한 수동 심사를 시작할 수 있습니다. 임계값 범위는 0 - 100입니다. 기본값이 권장됩니다.
>? [MPS 콘솔 - 템플릿 설정](https://console.cloud.tencent.com/mps/templates?tab=audit)에서 **사전 설정**된 심사 템플릿을 볼 수 있습니다.

3. 생성된 템플릿은 심사 템플릿 목록에 표시되며 템플릿의 세부 정보를 보거나 편집하거나 삭제할 수 있습니다.