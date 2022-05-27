동영상의 보안을 보호하고 핫링크 및 무단 다운로드 및 배포를 방지하기 위해, VOD는 동영상 콘텐츠 보안을 위한 다중 보호 메커니즘을 제공하여 다방면의 불법 침해로부터 동영상 저작권을 보호합니다.

<table class="table auto-table">
  <tr>
	  <td>카테고리</td>
	  <td>기능</td>
		<td>특징</td>
		<td>보안 수준</td>
	</tr>
	<tr>
	  <td rowspan="2">링크 도용 방지</td>
	  <td>Referer 링크 도용 방지</td>
		<td>재생 요청 Header의 'Referer' 필드를 통해 요청 소스를 식별하고, 차단 리스트 또는 허용 리스트를 통해 요청 소스를 제어합니다.</td>
		<td>낮음</td>
	</tr>
	<tr>
	  <td>Key 링크 도용 방지</td>
		<td>재생 URL에 제어 매개변수를 추가하고 Key를 서명으로 사용하여 URL 유효 기간, 미리 보기 지속 시간, 재생이 허용된 IP 수 등을 제어합니다.</td>
		<td>중간</td>
	</tr>
	<tr>
	  <td rowspan="2">동영상 암호화</td>
	  <td>HLS 공통 암호화</td>
		<td><li>HLS 기반 <a href=https://tools.ietf.org/html/draft-pantos-http-live-streaming-23?spm=a2c4g.11186623.2.31.409c6a6aYf9Rn8>AES encryption </a>방식</li><li>이며, 일부 브라우저 플러그 인 및 회색 시장 툴은 암호화 방법을 해독할 수 있습니다.</li></td>
		<td>높음</td>
	</tr>
	<tr>
	  <td>HLS 개인 암호화</td>
		<td>HLS 일반 암호화의 불충분한 보안성을 고려하여 VOD는 암호화 체계를 업그레이드하고 다양한 브라우저 플러그 인 및 회색 시장 툴의 크랙을 효과적으로 방지할 수 있는 고유한 개인 암호화 체계를 출시했습니다.</td>
		<td>매우 높음</td>
	</tr>
</table>
<dx-alert infotype="notice" title="">
**HLS 일반 암호화는 낮은 보안성으로 인해 더 이상 권장되지 않습니다**.
</dx-alert>

* [링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33984)는 주로 동영상 재생 요청 소스의 유효성을 제어하는 데 사용되지만, 동영상 콘텐츠를 암호화하지 않으므로 사용자가 2차 배포를 위해 동영상을 다운로드할 수 있습니다. 따라서 저작권 보호의 보안 수준이 낮습니다.
* 동영상 암호화는 동영상 콘텐츠 자체를 키로 암호화하는 수단으로, 다른 사람이 획득한 후 바로 재생할 수 없습니다. 단말 장치가 비즈니스 백엔드의 인증을 통과하고 암호 해독 키를 얻은 경우에만 콘텐츠를 재생할 수 있습니다. [HLS 개인 암호화](https://intl.cloud.tencent.com/document/product/266/46780)를 사용하여 동영상 콘텐츠에 더 높은 수준의 보안성을 부여하는 것이 좋습니다.
