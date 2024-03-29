## 소개
태그 분류는 멀티미디어에서 인물, 동작, 음성, 텍스트, 사물 및 장면의 다차원 구조 분석을 통해 높은 정확도의 멀티미디어 태그, 프레임별 태그, 멀티미디어 분류 정보를 자동으로 생성합니다.
<table>
    <tr>
        <th style="width:130px">
            기능               
        </th>
				<th>
           설명
        </th>
    </tr>
 <tr>
        <td>
            멀티미디어 태그
        </td>
				<td>
            전체 멀티미디어에 지정할 수 있는 태그에 대한 제안 의견을 제공합니다. 현재 게임, 차량, 음악가, 경주차, 애완동물, 드럼, 자전거, 월드 오브 워크래프트, 컴퓨터, 학교 및 재킷 등 3000여 종의 태그를 지원하여 인물, 사건, 장면, 사물, 풍경, 음식, 동물 등의 카테고리를 커버하고, 일상에서 자주 볼 수 있는 사물의 각 정보 차원을 커버하여 비디오 콘텐츠의 태그 니즈를 완벽하게 충족합니다.
        </td>
 </tr>
 <tr>
        <td>
            프레임별 태그
        </td>
				<td>
            고객 사용자 지정 비디오 스크린샷 간격에 따라 스크린샷 화면 내 태그를 자동으로 인식해 태그가 위치한 비디오 위치를 특정할 수 있도록 지원하며, 프레임 태그는 인물, 풍경, 인공물, 건축, 동식물, 음식 등 9가지 카테고리를 커버합니다. 일상 생활의 다양한 정보 차원을 포함하고 있습니다.
        </td>
 </tr>
 <tr>
        <td>
            멀티미디어 분류
        </td>
				<td>
            멀티미디어 카테고리 분류에 대한 제안 의견을 제공합니다. 현재 자동차, 출산·유아, 패션 엔터테인먼트, 게임, 군사, 과학 기술, 시사, 동물, 음식, 스포츠, 여행, 애니메이션, 댄스, 음악, 영화 및 TV, 버라이어티 엔터테인먼트, 앵커, 시사 뉴스, 국제 뉴스, 사회 뉴스 등 20여 카테고리를 지원합니다.
        </td>
 </tr>
</table>
태그 분류는 사용자가 미디어 리소스를 효율적으로 관리할 수 있도록 도와주며 멀티미디어 맞춤형 추천과 같은 시나리오에서도 사용할 수 있습니다.

## 적합한 시나리오
<table>
    <tr>
        <th style="width:130px">
            배경               
        </th>
				<th>
           설명
        </th>
    </tr>
 <tr>
        <td>
            미디어 리소스 관리
        </td>
				<td>
            멀티미디어 플랫폼의 미디어 리소스는 카테고리 및 태그별로 검색되므로 검색 효율성이 크게 향상됩니다.
        </td>
 </tr>
  <tr>
        <td>
            멀티미디어 제작
        </td>
				<td>
           제작 시 특정 카테고리나 태그의 소재를 찾을 수 있어 제작 효율성을 높입니다.
        </td>
 </tr>
 <tr>
        <td>
            멀티미디어 맞춤형 추천
        </td>
				<td>
            쇼트 비디오 플랫폼, 이커머스, 소셜 애플리케이션 등의 시나리오에서 사용자의 니즈에 정확하게 맞춰 해당 미디어 콘텐츠를 푸시하면, 플랫폼 미디어 콘텐츠의 클릭률을 높이는 데 도움이 될 뿐만 아니라, 사용자가 콘텐츠를 필터링하는 데 할애하는 많은 시간을 절약할 수 있습니다.
        </td>
 </tr>
 <tr>
        <td>
            방송 분류
        </td>
				<td>
            방송 업계는 VOD 태그 분류 기능을 통해 방대한 비디오 콘텐츠 정보를 효율적으로 파악할 수 있어 기존의 비효율적인 수동 분류 작업을 떠나 식별된 태그 분류 정보를 통해 빠른 비디오 보관과 태그 검색이 가능합니다.
        </td>
 </tr>
</table>

## 사용 방법
멀티미디어 태그, 프레임별 태그, 멀티미디어 분류는 각각 [오디오/비디오 콘텐츠 분석](https://intl.cloud.tencent.com/document/product/266/33945)의 **지능형 태그**, **지능형 프레임별 태그**, **지능형 분류** 기능으로 구현됩니다. 자세한 사용 단계:
1. [CreateAIAnalysisTemplate](https://intl.cloud.tencent.com/document/product/266/34170), 지능형 태그 구성 항목('TagConfiguration'), 지능형 프레임별 태그 구성 항목('FrameTagConfiguration'), 지능형 분류('ClassificationConfiguration')는 필요에 따라 구성할 수 있습니다. 예를 들어 아래 인터페이스 요청은 태그 분류 기능이 모두 켜져 있음을 나타내며 프레임별 태그 스크린샷 간격을 3초로 설정합니다.
```
{
	"TagConfigure": {
		"Switch": "ON"
	},
	"FrameTagConfigure": {
		"Switch": "ON",
		"ScreenshotInterval": 3
	},
	"ClassificationConfigure": {
		"Switch": "ON"
	}
}
```
반환된 패키지에서 템플릿 ID를 얻습니다.
모든 태그 분류 기능을 사용하려면 [사전 설정 매개변수 템플릿 목록](https://intl.cloud.tencent.com/document/product/266/33932)에서 템플릿 ID 20을 직접 사용하십시오.
2. 1단계의 템플릿 ID를 사용하여 태그 분류 작업을 시작합니다. 자세한 내용은 [작업 시작](https://intl.cloud.tencent.com/document/product/266/33945#.E4.BB.BB.E5.8A.A1.E5.8F.91.E8.B5.B7)을 참고하십시오.
3. 태그 분류 작업 결과를 가져옵니다. 자세한 내용은 [결과 가져오기](https://intl.cloud.tencent.com/document/product/266/33945#.E7.BB.93.E6.9E.9C.E8.8E.B7.E5.8F.96)를 참고하십시오.
