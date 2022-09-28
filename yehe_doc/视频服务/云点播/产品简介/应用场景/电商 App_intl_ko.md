## 시나리오 설명
이커머스 App은 기업과 개인이 제품을 마케팅하고 판매할 수 있는 온라인 거래 플랫폼입니다. 판매자는 일반적으로 제품을 더 잘 보여주기 위해 제품 이미지와 동영상을 제작하고 업로드합니다. 소비자는 이미지와 비디오를 업로드하여 쇼핑 경험에 대한 피드백을 공유하거나 제품 리뷰를 작성할 수도 있습니다. 이커머스 App에는 일반적으로 다음과 같은 핵심 요구 사항이 포함됩니다.
<table>
    <tr>
        <th>
            핵심 소구점              
        </th>
				<th>
           설명
        </th>
    </tr>
		<tr>
        <td>
            여러 해상도 간의 스마트 전환
        </td>
				<td>
			 동영상 재생 시 원활한 재생 경험을 위해 사용자의 네트워크 환경 변화에 따라 최적의 동영상 해상도를 지능적으로 선택해야 합니다.
        </td>
	</tr>
		<tr>
        <td>
            화면 캡처 기능
        </td>
				<td>
				플랫폼은 더 많은 판매자를 유치하기 위해 제품을 선보일 다양한 방법을 제공해야 합니다. 예를 들어, 플랫폼은 판매자가 홈페이지에서 사용할 정적 썸네일을 생성하고 비디오 미리보기를 위한 애니메이션 썸네일을 생성하여 제품 콘텐츠를 보다 빠르고 직접적으로 표시할 수 있도록 해야 합니다.
        </td>
	</tr>
	<tr>
        <td>
            낮은 비트 레이트로 고화질 구현
        </td>
				<td>
				판매자는 비디오를 HD로 제공하고 빠르게 로딩하여 제품 비디오를 통해 더 많은 소비자가 제품을 검색하고 구매할 수 있기를 원합니다.
        </td>
	</tr>
 <tr>
        <td>
           고품질 클라이언트 업로드
        </td>
				<td>
소비자는 다양한 모바일 장치 모델을 사용할 수 있으며 열악한 네트워크 조건에서도 빠르고 안정적인 비디오 업로드를 원합니다. 업로드 경험이 좋지 않으면 소비자가 업로드를 포기하고 플랫폼에 대한 부정적인 의견을 형성하여 플랫폼 이미지를 손상시킬 수 있습니다.
        </td>
	</tr>
	<tr>
        <td>
            타임 시프트
        </td>
				<td>
				라이브 스트리밍 중 라이브 쇼핑룸에 입장하여 이전 제품 정보를 놓친 소비자는 더 많은 제품 정보를 얻기 위해 더 이전 시점부터 시청하기를 원할 수 있습니다.
        </td>
	</tr>
	<tr>
        <td>
            스마트 제품 추천
        </td>
				<td>
				플랫폼은 제품 비디오의 클릭 수를 지능적으로 분석하고 관심 있는 제품의 카테고리와 태그를 기반으로 사용자에게 추천하여 구매율을 높여야 합니다.
        </td>
	</tr>
	<tr>
        <td>
            비용 절감
        </td>
				<td>
				많은 라이브 쇼핑 비디오 녹화는 해당 당국의 감사를 위해서만 보관되어야 하며, 그 중 일부는 재생되지 않거나 거의 재생되지 않지만 저장 비용의 상당 부분을 차지합니다.
        </td>
	</tr>
</table>

## 솔루션
<table>
    <tr>
        <th>
            핵심 니즈              
        </th>
				<th>
           추천 VOD 기능
        </th>
    </tr>
		<tr>
        <td>
           여러 해상도 간의 스마트 전환
        </td>
				<td>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49263" title="Smart Multi-Bitrate Switch" target="_blank">Smart Multi-Bitrate Switch</a></br>하나의 입력 파일에 여러 비트스트림이 출력되므로 다양한 네트워크 조건에서 원활하게 재생할 수 있습니다.</li>
        </td>
	</tr>
 <tr>
        <td>
           화면 캡처 기능
        </td>
				<td>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49257" title="Video Screencapturing" target="_blank">Video Screencapturing</a></br>판매자는 특정 시점 스크린샷, 샘플 스크린샷, 썸네일, 이미지 스프라이트, 애니메이션 이미지 생성을 포함한 다양한 화면 캡처 작업을 수행하여 다양한 방식으로 제품을 선보일 수 있습니다.</li>
        </td>
	</tr>
	<tr>
        <td>
            낮은 비트 레이트로 고화질 구현
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49255" title="TSC Transcoding" target="_blank">TSC Transcoding</a></br>VOD의 TSC 트랜스코딩 기능을 통해 소비자는 부드럽고 선명한 동영상 재생 경험을 즐길 수 있습니다.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            고품질 클라이언트 업로드
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49247" title="Multi-End Upload" target="_blank">Multi-End Upload</a></br>VOD는 Android/iOS/Web과 같은 다양한 플랫폼의 클라이언트에서 업로드를 지원합니다.
				</li>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49149" title="Upload Acceleration" target="_blank">Upload Acceleration</a></br>VOD는 스케쥴링 최적화와 같은 일련의 기술적 방법을 사용하여 업계 최고의 업로드 품질(업로드 성공률 99.5% 이상)을 제공합니다. 우수한 업로드 경험은 소비자가 구매 경험을 공유하도록 장려하고 플랫폼의 평판을 향상시킵니다.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            타임 시프트
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49279" title="Time Shifting" target="_blank">Time Shifting</a></br>이커머스 라이브 스트림이 진행 중일 때 라이브 룸에 입장하는 소비자는 진행률 표시줄을 수동으로 끌어 더 이른 시점의 콘텐츠를 시청하여 제품에 대한 자세한 정보를 얻을 수 있습니다.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            스마트 제품 추천
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49268" title="Tagging" target="_blank">Tagging</a></br>VOD의 태그 기능은 동영상에 자동으로 태그를 붙이고 분류할 수 있으므로 플랫폼은 제품 동영상 클릭수와 재생 완료율을 기반으로 소비자에게 관련 제품을 추천할 수 있습니다.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            비용 절감
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49252" title="Smart Cold Storage" target="_blank">Smart Cold Storage</a></br>VOD를 사용하면 거의 재생되지 않고 주로 감사 목적으로 보관되는 라이브 비디오 녹화에 대한 스마트 콜드 스토리지 정책을 구성할 수 있으므로 필요한 비디오를 저장하는 비용을 효과적으로 줄이는 데 도움이 됩니다.
				</li>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49251" title="Media Deletion" target="_blank">Media Deletion</a></br>감사 목적으로만 저장되는 녹화 파일의 만료 시간을 설정할 수 있습니다. 이러한 미디어 파일은 만료 시 자동으로 삭제되므로 저장 비용을 효과적으로 줄이는 데 도움이 됩니다.
				</li>
        </td>
	</tr>
</table>
