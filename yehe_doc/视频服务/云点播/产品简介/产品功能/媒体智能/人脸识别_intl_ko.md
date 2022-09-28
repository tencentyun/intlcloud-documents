## 소개
Tencent의 업계 최고의 AI 기술을 기반으로 하는 얼굴 인식 기능은 사람이 등장하는 프레임과 얼굴 영역의 좌표를 포함한 얼굴 정보를 비디오에서 빠르게 식별할 수 있도록 지원합니다. VOD의 퍼블릭 인물 라이브러리를 직접 이용하거나 나만의 커스텀 인물 라이브러리를 이용 및 관리할 수 있습니다. 퍼블릭 라이브러리에는 영화, 음악, 스포츠, 학계 등 다양한 분야의 유명 인사들이 있습니다.
## 적용 시나리오
미디어 콘텐츠의 얼굴 인식은 비디오 제작, 미디어 검색 및 맞춤형 추천 등에 널리 사용되고 있습니다.

<table>
    <tr>
        <th style="width:150px">
            시나리오               
        </th>
				<th>
           설명
        </th>
    </tr>
 <tr>
        <td>
            비디오 제작
        </td>
				<td>
            얼굴 인식 기능을 사용하면 사용자는 많은 수의 기존 비디오에서 타깃 얼굴이 나타나는 시점, <br/>화면 영역 및 지속 시간을 빠르게 찾을 수 있습니다. 이를 통해 관련 소재를 빠르게 찾고 콘텐츠 창작 효율을 높일 수 있습니다.
        </td>
 </tr>
 <tr>
        <td>
            이벤트 리플레이
        </td>
				<td>
				스포츠 및 e스포츠 이벤트 중 특정 선수가 등장하는 시점에 대한 타임스탬프를 추가하여 사용자가 해당 시점을 빠르게 찾을 수 있습니다. 또한 특정 유명인이 비디오에 등장하는 시점을 찾고 비디오 프레임을 캡처하여 하이라이트 릴을 쉽게 만들거나 애니메이션 이미지를 썸네일로 생성하여 더 많은 시청자를 유입할 수 있습니다.
        </td>
 </tr>
  <tr>
        <td>
            비디오 웹 사이트
        </td>
				<td>
            사용자는 사람의 이름으로 관련 동영상을 검색할 수 있습니다. 또한 사용자가 팔로우하는 사람 목록을 기반으로 관련 비디오를 자동으로 추천할 수 있습니다.
        </td>
 </tr>
</table>



## 사용 방법
다음과 같이 [비디오 콘텐츠 인식](https://intl.cloud.tencent.com/document/product/266/33946)에 설명된 **Face Recognition** 기능을 통해 얼굴 인식을 구현할 수 있습니다.
1. [멀티미디어 콘텐츠 인식 템플릿](https://intl.cloud.tencent.com/document/product/266/33946#.E9.9F.B3.E8.A7.86.E9.A2.91.E5.86.85.E5.AE.B9.E8.AF.86.E5.88.AB.E6.A8.A1.E6.9D.BF)을 준비합니다.
[사전 설정 멀티미디어 콘텐츠 인식 템플릿](https://intl.cloud.tencent.com/document/product/266/33932)을 직접 사용하여 모든 퍼블릭 인물 라이브러리에 있는 사람들을 인식할 수 있습니다.
또한 [CreateAIRecognitionTemplate](https://intl.cloud.tencent.com/document/product/266/37568) API의 얼굴 인식 구성 항목('FaceConfigure')을 사용하여 특정 유형의 사람을 인식하도록 퍼블릭 및 사용자 지정 인물 라이브러리\*의 특정 레이블을 지정할 수 있습니다. 예를 들어 다음 코드 샘플은 퍼블릭 인물 라이브러리에서 스포츠 유명인만 인식하도록 합니다.
```
{
	"FaceConfigure": {
		"Switch": "ON",
		"DefaultLibraryLabelSet": ["sport"]
	}
}
```
응답에서 템플릿 ID를 가져옵니다.
\* 사용자 지정 인물 라이브러리는 [API Category](https://intl.cloud.tencent.com/document/product/266/34110)에 설명된 **소재 샘플 생성/수정/삭제/획득** API를 통해 관리됩니다.

2. 1단계에서 획득한 템플릿 ID로 [작업 시작](https://intl.cloud.tencent.com/document/product/266/33946#.E4.BB.BB.E5.8A.A1.E5.8F.91.E8.B5.B7)의 안내에 따라 얼굴 인식 작업을 시작합니다.
3. [결과 가져오기](https://intl.cloud.tencent.com/document/product/266/33946#.E7.BB.93.E6.9E.9C.E8.8E.B7.E5.8F.96)의 안내에 따라 작업 결과를 가져옵니다.
