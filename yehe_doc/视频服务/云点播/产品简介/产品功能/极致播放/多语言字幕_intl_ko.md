## 소개
VOD의 다국어 자막 기능을 사용하면 표준 다국어 자막 파일을 어댑티브 비트레이트 스트리밍의 출력 파일과 연결/연결 해제할 수 있습니다. 재생하는 동안 사용자는 자막을 다른 언어로 전환할 수 있습니다. 이 기능은 국경을 초월한 시청자 비율을 높이는 데 도움이 되며, 대상 지역의 더 많은 시청자가 비디오 콘텐츠를 이해하고 즐길 수 있도록 합니다.
다국어 자막은 영어, 중국어 간체, 중국어 번체, 프랑스어, 독일어, 스페인어, 포르투갈어, 러시아어, 일본어, 한국어, 태국어, 베트남어, 인도네시아어 등 다양한 언어를 지원합니다. 지원되는 모든 언어 및 해당 코드는 [RFC5646](https://datatracker.ietf.org/doc/html/rfc5646)을 참고하십시오.

## 적용 시나리오
<table>
    <tr>
        <th>
            시나리오              
        </th>
				<th>
           설명
        </th>
    </tr>
		<tr>
        <td>
            국제 기업 회의
        </td>
				<td>
				국제 기업은 종종 다른 언어를 사용하는 참석자가 참여하는 내부 회의를 개최합니다. 녹화된 회의에 다국어 자막을 추가하여 다른 국가 또는 지역의 직원이 비디오를 보고 동료와 공유할 수 있습니다.
        </td>
		</tr>
		<tr>
        <td>
            국제 회의/스포츠 이벤트
        </td>
				<td>
				국제 화상 회의 및 전 세계 e스포츠 및 스포츠 경기 녹화의 경우 다국어 자막을 추가하여 다양한 국가 및 지역의 시청자가 연사 및 스포츠 아나운서의 발언 내용을 이해할 수 있도록 할 수 있습니다.
        </td>
		</tr>
		<tr>
        <td>
            비디오 웹 사이트
        </td>
				<td>
				외국 영화/TV 시리즈에 여러 언어를 추가하여 다양한 지역의 시청자가 좋아하는 프로그램을 보고 친구와 공유할 수 있도록 합니다.
        </td>
		</tr>
		<tr>
        <td>
            온라인 교육 플랫폼
        </td>
				<td>
				강의 내용이 외국어 과정과 같이 외국어를 포함하거나 외국 전문가 및 학자와의 커뮤니케이션이 포함되는 경우 시청자가 비디오 내용을 배우고 이해할 수 있도록 다국어 자막을 추가할 수 있습니다.
        </td>
		</tr>
		<tr>
        <td>
            크로스-보더 이커머스 플랫폼
        </td>
				<td>
				제품 프레젠테이션 영상에 다국어 자막을 추가하여 다양한 국가/지역의 소비자들이 구매하고 싶은 제품에 더욱 친숙해질 수 있도록 합니다.
        </td>
		</tr>
		<tr>
        <td>
            네트워크 광고
        </td>
				<td>
				네트워크 광고에 다국어 자막을 표시하여 광고가 전 세계 여러 국가/지역의 사용자에게 전달될 수 있도록 합니다.
        </td>
		</tr>
</table>

## 사용 방법
다국어 자막은 출력 어댑티브 비트스트림에 대한 HLS 형식을 지원합니다. 이 기능을 사용하기 전에 미디어 파일에 자막을 추가하고 [ModifyMediaInfo](https://intl.cloud.tencent.com/document/product/266/37570) API를 호출하여 자막을 추가(`AddSubtitles.N` 매개변수 입력)하거나 자막을 삭제('DeleteSubtitleIds.N' 매개변수 입력)해야 합니다. 새 자막 목록(각 자막 세트의 ID가 포함된 `AddedSubtitleSet`)은 API에서 반환됩니다.

미디어 파일에 자막을 추가한 후 [AttachMediaSubtitles](https://intl.cloud.tencent.com/document/product/266/40004) API를 호출하여 어댑티브 비트레이트 스트리밍의 출력 파일과 자막을 연결/연결 해제할 수 있습니다. [어댑티브 비트레이트 스트리밍](https://intl.cloud.tencent.com/document/product/266/33942) 작업을 다시 시작할 수도 있습니다. 어댑티브 비트레이트 스트리밍 작업([MediaProcessTask](https://intl.cloud.tencent.com/document/product/266/34187#MediaProcessTaskInput) -> [AdaptiveDynamicStreamingTaskSet](https://intl.cloud.tencent.com/document/product/266/34187#AdaptiveDynamicStreamingTaskInput) -> 'SubtitleSet')의 입력 매개변수에 자막 ID 목록을 지정해야 합니다.
