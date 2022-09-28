## 소개
VOD의 스마트 미디어 자산 콜드 스토리지 기능은 맞춤형 콜드 스토리지 정책을 기반으로 합니다. 파일 생성 시간, 파일 유형 및 액세스 빈도를 기반으로 비용이 저렴한 콜드 파일을 스토리지 유형으로 자동 전환합니다. VOD에는 STANDARD, STANDARD_IA, ARCHIVE 및 DEEP ARCHIVE와 같은 스토리지 유형이 있습니다. 다음은 스토리지 유형별 비용 및 액세스 성능입니다.

<table>
    <tr>
        <th style="width:150px">
            속성              
        </th>
				<th>
           순위(최고에서 최저)
        </th>
    </tr>
		 <tr>
        <td>
            스토리지 비용
        </td>
				<td>
				STANDARD > STANDARD_IA > ARCHIVE > DEEP_ARCHIVE.
        </td>
		</tr>
		<tr>
        <td>
            액세스 성능
        </td>
				<td>
				STANDARD > STANDARD_IA. ARCHIVE 및 DEEP_ARCHIVE 스토리지 유형은 직접 액세스를 지원하지 않습니다. 액세스하려면 먼저 <a href="https://intl.cloud.tencent.com/document/product/266/43051#.E6.95.B0.E6.8D.AE.E5.8F.96.E5.9B.9E.E5.8F.8A.E5.8F.96.E5.9B.9E.E6.A8.A1.E5.BC.8F.3Ca-id.3D.22retake.22.3E.3C.2Fa.3E" title="데이터 검색" target="_blank">데이터 검색</a>해야 합니다.
        </td>
		</tr>
</table>

VOD 파일의 스토리지 유형을 비즈니스 특성에 따라 특정 <a href="https://intl.cloud.tencent.com/document/product/266/43051#.E7.AD.96.E7.95.A5.E7.AE.A1.E7.90.86.3Ca-id.3D.22strategy.22.3E.3C.2Fa.3E" title="콜드 스토리지 정책">콜드 스토리지 정책</a>에 따라 STANDARD에서 STANDARD_IA, ARCHIVE 또는 DEEP_ARCHIVE로 변경하여 스토리지 비용을 효과적으로 줄일 수 있습니다.

### 스마트 콜드 스토리지 정책
VOD는 유연한 스마트 콜드 스토리지 정책과 생성 시간, 파일 카테고리, 재생 횟수를 포함한 다양한 콜드 스토리지 차원을 지원합니다.

<table>
    <tr>
        <th style="width:150px">
            영역              
        </th>
				<th>
           설명
        </th>
    </tr>
		 <tr>
        <td>
            파일 생성 시간
        </td>
				<td>
				업로드 시간과 저장 시간을 지정할 수 있습니다.
				<ul>
					<li>업로드 시간 지정: 시점 또는 기간을 지정하여 콜드 스토리지 정책을 구성할 수 있습니다.
						<ul>
						<li>기간 지정: 시작 시점을 지정하지 않으면 기본적으로 가장 오래된 저장 동영상 파일이 콜드 스토리지 유형으로 전환됩니다. 종료 시점을 지정하지 않으면 시작 시점 이후의 모든 비디오 파일이 전환됩니다. 둘 다 지정하지 않으면 VOD의 모든 비디오 파일이 전환됩니다.</li>
							</ul>
					</li>
					<li>저장 시간 지정: 미디어 자산은 입력된 시간이 경과한 후 자동으로 콜드 스토리지 유형으로 전환됩니다.</li>
				</ul>
        </td>
		</tr>
		<tr>
        <td>
            파일 카테고리
        </td>
				<td>
				카테고리 ID별 콜드 스토리지가 지원됩니다. 여러 카테고리 ID/이름을 설정할 수 있습니다.
        </td>
		</tr>
		<tr>
        <td>
            파일 소스
        </td>
				<td>
				다양한 미디어 소스에 대해 콜드 스토리지가 지원됩니다. 여러 미디어 소스를 설정할 수 있습니다.
        </td>
		</tr>
		<tr>
        <td>
            재생 통계
        </td>
				<td>
				콜드 스토리지 정책은 지정된 시간 동안 비디오가 재생된 횟수에 따라 다릅니다.  콜드 스토리지 정책은 하나의 액세스 정책만 지원합니다.
        </td>
		</tr>
		<tr>
        <td>
            미디어 유형
        </td>
				<td>
				콜드 스토리지 로직 수행 여부는 미디어 유형에 따라 결정됩니다. 콜드 스토리지 정책은 하나의 미디어 유형만 지원합니다.
        </td>
		</tr>
</table>

콜드 스토리지 정책을 구성하는 것 외에도 VOD를 사용하면 한 번에 여러 파일을 수동으로 전환할 수 있습니다. [콜드 스토리지](https://intl.cloud.tencent.com/document/product/266/42092)의 지침에 따라 콘솔에서 직접 수행하거나 [ModifyMediaStorageClass](https://intl.cloud.tencent.com/document/product/266/46008) API를 호출하여 이 작업을 수행할 수 있습니다.

## 적용 시나리오
<table>
    <tr>
        <th style="width:160px">
            배경              
        </th>
				<th>
           설명
        </th>
    </tr>
		 <tr>
        <td>
            이커머스 라이브 스트리밍
        </td>
				<td>
				중국 국가 시장 규제 관리국에서 발행한 <a href="https://gkml.samr.gov.cn/nsjg/fgs/202103/t20210315_326936.html" title="온라인 거래의 감독 및 관리 방법" target="_blank">온라인 거래의 감독 및 관리 방법</a>에서 요구하는 바에 따라, 라이브 스트리밍 서비스 제공자는 라이브 스트리밍이 종료된 후 최소 3년 동안 온라인 거래의 라이브 비디오를 보관해야 합니다. 이러한 비디오는 일반적으로 VOD에 STANDARD 저장 유형으로 저장되며, 그 중 일부는 거의 또는 전혀 재생되지 않으며 해당 기관의 검토용으로만 사용됩니다. 스마트 콜드 스토리지 기능은 이러한 미디어 자산의 스토리지 비용을 효과적으로 줄이는 데 도움이 될 수 있습니다.
        </td>
		</tr>
		<tr>
        <td>
            저빈도 액세스 미디어 콜드 스토리지
        </td>
				<td>
				비디오 포털, 스트리밍 미디어 플랫폼 및 UGC 관리 플랫폼의 경우 사용자가 자주 액세스하거나 시청하지 않는 미디어 자산은 여러 가지 이유로 플랫폼에서 직접 제거할 수 없으며 종종 불필요하게 높은 스토리지 비용이 발생합니다. VOD의 스마트 콜드 스토리지 기능은 액세스 빈도에 따라 콜드 스토리지 유형에 미디어 파일을 저장할 수 있어 미디어 자산의 저장 비용을 효과적으로 줄이면서 저빈도 시청 요구 사항을 충족할 수 있습니다.
        </td>
		</tr>
		<tr>
        <td>
            미디어 자산 아카이브
        </td>
				<td>
				뉴스, 미디어, 라디오 및 TV 산업에서 일부 미디어 파일은 짧은 기간 동안만 관련이 있지만 일반적으로 장기간 보관되므로 나중에 가끔 재생할 수 있습니다. 이러한 재생은 일반적으로 첫 번째 프레임까지의 시간에 대한 요구 사항이 높지 않습니다. 이러한 자산을 VOD의 ARCHIVE 또는 DEEP_ARCHIVE 스토리지에 저장하여 스토리지 비용을 줄일 수 있습니다.
        </td>
		</tr>
</table>

## 사용 방법
참고 사항:
- [VOD 미디어 파일을 스마트 콜드 스토리지하는 방법](https://intl.cloud.tencent.com/document/product/266/43051).
- [미디어 자산 콜드 스토리지](https://intl.cloud.tencent.com/document/product/266/42092).
- [ModifyMediaStorageClass](https://intl.cloud.tencent.com/document/product/266/46008).
- [RestoreMedia](https://intl.cloud.tencent.com/document/product/266/48378)(서버 API). 이 API는 ARCHIVE 또는 DEEP ARCHIVE 스토리지 유형에 저장된 파일에 대해 일시적으로 액세스할 수 있는 미디어 파일을 생성하는 데 사용할 수 있습니다.
