## 시나리오 설명
온라인 교육 플랫폼을 통해 학생과 교사는 네트워크를 통해 수업에 참석하고 의사 소통할 수 있습니다. 이러한 플랫폼에는 일반적으로 등록된 교사가 녹화하고 업로드하는 오디오/비디오 교육 자료가 많습니다. 온라인 교육에는 일반적으로 다음과 같은 핵심 요구 사항이 포함됩니다.

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
            다양한 플랫폼에서 재생
        </td>
				<td>
				학생들은 Web 및 모바일 클라이언트를 포함하여 다양한 장치와 플랫폼을 사용하며 장치에서 유료 비디오를 볼 수 있어야 합니다.
        </td>
	</tr>
	<tr>
        <td>
            스마트 자막
        </td>
				<td>
				교사의 억양과 말하는 속도가 다르고 학생의 이해 수준이 다르기 때문에 모든 학생이 쉽게 학습할 수 있도록 교육 비디오에 자막을 추가해야 합니다. 하지만 강의 영상은 길고 수동 자막은 비효율적입니다.
        </td>
	</tr>
 <tr>
        <td>
           저작권 보호
        </td>
				<td>
교육 콘텐츠는 일반적으로 전용 장소, 전문 장비 및 전문 교사를 필요로 하므로 제작 비용이 많이 듭니다. 이처럼 교육용 영상은 플랫폼의 중요한 디지털 자산이 되며, 이에 대한 저작권을 효과적으로 보호하여 유출되지 않도록 해야 합니다. 
        </td>
	</tr>
	<tr>
        <td>
            타임 시프트
        </td>
				<td>
				라이브 강의실에 입장하는 학생들은 현재 교육 내용의 맥락을 이해하지 못할 수 있으며 맥락을 파악하기 위해 이전 시점의 콘텐츠를 시청해야 합니다.
        </td>
	</tr>
	<tr>
        <td>
            Psuedo 라이브 스트리밍
        </td>
				<td>
				플랫폼은 실시간 스트리밍 비용(장소, 장비 및 교사 비용)과 위험(녹화 영상 콘텐츠 사전 조정 가능)을 줄이면서 학생과 학부모가 수업에 더 많은 관심을 기울이도록 장려하기 위해 지정된 시간에 사전 녹화된 강의를 라이브 스트리밍할 수 있어야 합니다.
        </td>
	</tr>
	<tr>
        <td>
            스마트 조정
        </td>
				<td>
				교육용 영상의 부적절한 말, 행동, 이미지는 학생들에게 좋지 않은 영향을 미치고 플랫폼에 법적 위험과 부정적인 의견을 초래할 수 있습니다. 따라서 비디오 콘텐츠는 조정되어야 합니다. 그러나 대부분의 교육 비디오는 긴 비디오로, 기존의 수동 조정은 비준수 콘텐츠를 놓치는 경향이 있으며 조정 품질과 효율성이 낮은 긴 프로세스가 수반됩니다.
        </td>
	</tr>
	<tr>
        <td>
            미디어 재생 차단
        </td>
				<td>
				교육 동영상은 주로 미성년자를 대상으로 하기 때문에 규정을 준수하지 않는 동영상 콘텐츠는 매우 민감할 수 있습니다. 그러나 이러한 콘텐츠는 조정 서비스의 성능이 충분하지 않아 감지되지 않을 수 있으며, 사후에 발견된 경우 즉시 신속하게 차단되어야 합니다.
        </td>
	</tr>
	<tr>
        <td>
            비용 절감
        </td>
				<td>
				학생들은 높은 비디오 재생 부드러움과 선명도를 요구합니다. 그러나 HD 비디오가 많으면 저장 비용이 많이 듭니다.
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
           다양한 플랫폼에서 재생
        </td>
				<td>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49263" title="Smart Multi-Bitrate Switch" target="_blank">Smart Multi-Bitrate Switch</a></br>하나의 입력 파일에 대해 여러 비트스트림이 출력되므로 학생들의 다양한 네트워크 조건에서의 재생 요구 조건을 충족합니다.</li>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49265" title="Multi-Terminal Player" target="_blank">Multi-Terminal Player</a></br>Multi-Terminal Player는 iOS, Android, Web(Flash/HTML5) 및 Flutter에서 사용할 수 있으므로 다양한 장치에서 고품질 비디오 재생에 대한 학생들의 요구를 충족합니다. 또한 재생 품질 통계 수집도 지원합니다.</li>
        </td>
	</tr>
	 <tr>
        <td>
           스마트 자막
        </td>
				<td>
				<li><a href="https://intl.cloud.tencent.com/document/product/266/49267" title="Smart Subtitles" target="_blank">Smart Subtitles</a></br>VOD는 오디오 콘텐츠를 효율적이고 정확하게 인식하고 표준 형식의 자막 파일을 자동으로 생성하여 학생들이 더 잘 공부할 수 있도록 도와줍니다.</li>
        </td>
	</tr>
	<tr>
        <td>
            저작권 보호
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49274" target="_blank">Hotlink Protection</a></br>VOD의 링크 도용 방지 기능은 Referer 및 Key를 기반으로 핫링크를 방지할 수 있습니다.
				</li>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49275" title="Encryption and DRM" target="_blank">Encryption and DRM</a></br>VOD는 HLS 개인 암호화와 상용 DRM을 모두 지원하여 다양한 크랙 행위를 효과적으로 방지하고 저작권이 있는 미디어를 보호합니다.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            타임 시프트
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49279" title="Time Shifting" target="_blank">Time Shifting</a></br>VOD를 통해 학생들은 라이브 스트리밍 중 이전 시점의 콘텐츠를 시청하여 컨텍스트를 더 잘 이해하고 언제든지 최신 라이브 콘텐츠로 다시 전환할 수 있습니다.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            Psuedo 라이브 스트리밍
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49281" title="VOD to Live Streaming" target="_blank">VOD to Live Streaming</a></br>VOD to Live Streaming은 라이브 스트리밍 비용을 줄이고 학생의 집중도와 학습 효과를 향상시킬 수 있습니다.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            스마트 조정
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49271" title="Smart Moderation" target="_blank">Smart Moderation</a></br>VOD는 교육 비디오에서 비준수 콘텐츠를 지능적으로 감지하여 건강한 학습 경험을 보장하고 플랫폼 콘텐츠의 보안 위험을 방지합니다.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            미디어 재생 차단
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49272" title="Media Blocking" target="_blank">Media Blocking</a></br>플랫폼은 더 이상 확산되는 것을 방지하기 위해 비준수 비디오의 재생을 신속하게 금지할 수 있습니다.
				</li>
        </td>
	</tr>
	<tr>
        <td>
            비용 절감
        </td>
				<td>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49251" title="Media Deletion" target="_blank">Media Deletion</a></br>미디어 리소스는 부분적으로 삭제할 수 있습니다. 오래된 동영상은 LD 동영상만 유지되며, HD 동영상은 저장 비용을 줄이기 위해 삭제됩니다. 미디어 리소스는 만료 시 자동으로 삭제될 수 있습니다.
				</li>
				<li>
					<a href="https://intl.cloud.tencent.com/document/product/266/49252" title="Smart Cold Storage" target="_blank">Smart Cold Storage</a></br>생성 시간, 파일 카테고리, 보기 등 다양한 차원에서 스마트 콜드 스토리지 정책을 구성하여 조건에 맞는 미디어 리소스를 저렴한 비용으로 스토리지 클래스로 자동 전환할 수 있습니다.
				</li>
        </td>
	</tr>
</table>
