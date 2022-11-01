## 시나리오 설명
라디오, TV, OTT 미디어 서비스는 사용자의 가정에서 TV가 제공하는 스트리밍 미디어 서비스를 기반으로 합니다. 이 사용 사례에는 일반적으로 다음과 같은 핵심 요구 사항이 포함됩니다.
<table>
    <tr>
        <th>
            핵심 요구 사항              
        </th>
				<th>
           설명
        </th>
    </tr>
		<tr>
        <td>
            고해상도 비디오
        </td>
				<td>
			라디오, TV, OTT 플랫폼 사용자는 일반적으로 스마트 TV와 같은 대화면 장치에서 미디어를 재생하므로 동영상 이미지의 미묘하고 생생한 디테일이 먼저 필요합니다. 따라서 UHD 동영상 재생은 가장 기본적인 요구 사항입니다.
        </td>
	</tr>
	<tr>
        <td>
            여러 해상도 간의 스마트 전환
        </td>
				<td>
			 라디오, TV 및 OTT 플랫폼은 네트워크 조건이 크게 다른 대규모 사용자 기반을 보유하고 있습니다. 다른 네트워크 환경에 적응하기 위해 플랫폼은 일반적으로 비디오 리소스에 대해 여러 해상도를 준비해야 장치가 네트워크 조건에 따라 가장 적절한 비트 레이트로 미디어 스트림을 자동으로 선택하고 재생할 수 있습니다.
        </td>
	</tr>
	<tr>
        <td>
            저작권 보호
        </td>
				<td>
			 라디오, TV, OTT 플랫폼에는 영화, 스포츠 경기, 애니메이션, 예능 등 다양한 미디어 리소스 콘텐츠가 있습니다. 대화면 소비가 계속 증가함에 따라 이러한 콘텐츠도 불법 복제에 취약해지고 있습니다.
        </td>
	</tr>
	<tr>
        <td>
            스마트 미디어 조정
        </td>
				<td>
			라디오, TV, OTT 플랫폼은 다양한 시청자층을 보유하고 있습니다. 비준수 콘텐츠의 배포로 인한 심각한 영향과 막대한 손실을 방지하려면 효율적인 조정 기능이 필요합니다. 일반적으로 이러한 플랫폼에 있는 대부분의 비디오는 길이가 길기 때문에 수동 조정 프로세스가 길고 비효율적이며 오류가 발생하기 쉽습니다. 기계 기반 스마트 조정을 사용하면 많은 수의 호환 비디오를 먼저 필터링할 수 있으므로 수동 조정 비용이 크게 줄어듭니다.
        </td>
	</tr>
	<tr>
        <td>
            미디어 재생 차단
        </td>
				<td>
				미디어 플랫폼은 조정 중에 비준수 콘텐츠가 누락된 경우 특정 비디오의 재생을 빠르게 차단할 수 있어야 합니다.
        </td>
	</tr>
		<tr>
        <td>
            Psuedo 라이브 스트리밍
        </td>
				<td>
				유사(Pseudo) 라이브 스트리밍(실시간 스트리밍과 유사한 효과를 얻기 위해 미리 녹화된 영상을 방송하는 것)은 라디오, TV, OTT 플랫폼에 널리 존재합니다. 예능, 버라이어티 쇼, 인터뷰 등은 미리 녹화, 편집하고 미리보기 페이지에 URL을 올려놓아 시청자가 미리 즐겨찾기에 등록해 재생 시간에 시청할 수 있도록 했습니다.
        </td>
	</tr>
	<tr>
        <td>
            효율적인 콘텐츠 목록화
        </td>
				<td>
				라디오 및 TV 산업에는 많은 수의 비디오가 있으며 대부분이 긴 비디오입니다. 모든 콘텐츠를 목록화해야 하지만 기존의 수동 목록화 방식은 비효율적입니다.
        </td>
	</tr>
</table>




## 솔루션
<table>
    <tr>
        <th>
            핵심 요구 사항              
        </th>
				<th>
           VOD 추천 기능
        </th>
    </tr>
	<tr>
        <td>
            고해상도 비디오
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/49254" title="Audio/Video Transcoding" target="_blank">Audio/Video Transcoding</a></br>VOD는 HDR 화질은 물론 2K, 4K, 8K 등의 고해상도 트랜스코딩을 지원하여 OTT TV와 같은 UHD 및 HD 콘텐츠용 대화면 기기의 요구 사항을 충족합니다.</li>
        </td>
	</tr>
	<tr>
        <td>
            여러 해상도 간의 스마트 전환
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/49263" title="Smart Multi-Bitrate Switch" target="_blank">Smart Multi-Bitrate Switch</a></br>복잡한 가족 네트워크 환경에서 다양한 장치의 재생 요구를 충족시키기 위해 하나의 입력 파일에 대해 여러 비트스트림이 출력됩니다.</li>
        </td>
	</tr>
	 <tr>
        <td>
            저작권 보호
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49274" title="Hotlink Protection" target="_blank">Hotlink Protection</a></br>VOD의 링크 도용 방지 기능은 Referer 및 Key를 기반으로 핫링크를 방지할 수 있습니다.
				</li>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49275" title="Encryption and DRM" target="_blank">Encryption and DRM</a></br>VOD는 HLS 개인 암호화와 상용 DRM을 모두 지원하여 다양한 크랙 행위를 효과적으로 방지하고 저작권이 있는 미디어를 보호합니다.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            스마트 미디어 조정
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49271" title="Smart Moderation" target="_blank">Smart Moderation</a></br>VOD의 스마트 조정 기능은 대량의 비준수 데이터에 대한 트레이닝 및 모델링을 지속적으로 수행하여 업계 최고의 인식 정확도 및 회수율을 달성하여 라디오, TV 및 OTT 플랫폼의 미디어 콘텐츠 보안을 포괄적이고 효과적으로 보장합니다.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            미디어 재생 차단
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/49272" title="Media Blocking" target="_blank">Media Blocking</a></br>미디어 재생 차단을 통해 플랫폼은 비준수 미디어 콘텐츠를 즉시 차단하여 추가 확산을 방지할 수 있으므로 플랫폼에 대한 보안 위험과 브랜드 이미지 손상을 줄일 수 있습니다.</li>
        </td>
	</tr>
	<tr>
        <td>
            Psuedo 라이브 스트리밍
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/49281" title="VOD to Live Streaming" target="_blank">VOD to Live Streaming</a></br>VOD의 액세스 제어 기능을 기반으로 VOD 파일을 유사(Psuedo) 라이브 스트림으로 재생할 수 있습니다. 라디오, TV 및 OTT 플랫폼은 VOD 파일을 저렴한 비용으로 유사(Psuedo) 라이브 스트림으로 신속하게 전달할 수 있으며, 플랫폼으로 더 많은 트래픽을 끌어들이기 위해 고부가가치 녹음 콘텐츠를 최대한 활용할 수 있습니다.</li>
        </td>
	</tr>
	<tr>
        <td>
            효율적인 콘텐츠 목록화
        </td>
				<td>
					<li><a href="https://intl.cloud.tencent.com/document/product/266/49268" title="Tagging" target="_blank">Tagging</a></br>VOD의 태그 및 분류 기능은 방대한 양의 비디오 콘텐츠에 태그와 카테고리를 효율적으로 추가하여 수동 분류의 낮은 효율성 문제를 해결합니다. 인식된 태그 및 카테고리 정보를 기반으로 동영상을 빠르게 보관, 태그 추가 및 검색할 수 있습니다.</li>
        </td>
	</tr>
</table>
