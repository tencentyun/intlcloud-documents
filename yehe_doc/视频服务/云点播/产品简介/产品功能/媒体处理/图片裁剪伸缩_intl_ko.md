## 기능 소개
VOD의 실시간 이미지 처리 기능은 아래와 같이 스케일링 및 크롭핑 작업을 지원합니다.
<melo-data data-src="" data-version="2.1.0"></melo-data><table ><colgroup><col  width="301px"><col  width="301px"></colgroup>
<tbody>
<tr>
<th   colspan="1" rowspan="1" align="" valign=""><p>작업 유형</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>상세 작업</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="5" align="" valign=""><p>스케일링</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>너비를 지정하면 높이는 비율에 따라 변경됩니다.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>높이를 지정하면 너비는 비율에 따라 변경됩니다.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>긴 변을 지정하면 짧은 변은 비율에 따라 변경됩니다.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>짧은 변을 지정하면 긴 변은 비율에 따라 변경됩니다.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>이미지가 지정된 너비와 높이로 강제 조정됩니다.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="2" align="" valign=""><p>크롭핑</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>내접원 자르기. 자르기할 반경을 지정합니다.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>직사각형 자르기. 자르기할 너비와 높이를 지정합니다.</p></td>
</tr>
</tbody>
</table>

 VOD의 실시간 영상 처리 기능은 기존의 영상 편집에 비해 다음과 같은 장점이 있습니다.
<melo-data data-src="{}" data-version="2.1.0"></melo-data><table ><colgroup><col  width="201px"><col  width="201px"><col  width="201px"></colgroup>
<tbody>
<tr>
<th   colspan="1" rowspan="1" align="" valign=""><p>차원</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>기존 이미지 편집</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>VOD의 실시간 이미지 처리</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>처리 프로세스</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>다운로드, 편집 및 업로드를 포함한 여러 단계의 작업이 필요하며 시간과 노력이 많이 듭니다.</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>이미지를 업로드 및 다운로드할 필요 없이 클라우드에서 모든 이미지 편집 프로세스를 직접 완료할 수 있습니다.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>작업 방법</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>이미지 편집 소프트웨어는 사용하기 어렵고 특정 이미지 편집 기술에 숙달되어야 합니다.</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>URL에서 실시간으로 이미지 편집 매개변수를 지정할 수 있어 시작하기 쉽습니다.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>액세스 속도</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>클라우드 스토리지 URL을 통한 이미지 액세스 및 다운로드 속도가 느려 사용자 경험에 영향을 미칩니다.</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>VOD는 CDN을 사용하여 글로벌 이미지 전송을 가속화하므로 매우 짧은 시간에 처리된 이미지를 얻을 수 있습니다.</p></td>
</tr>
</tbody>
</table>

## 적용 시나리오
<melo-data data-src="{}" data-version="2.1.0"></melo-data><table ><colgroup><col  width="301px"><col  width="301px"></colgroup>
<tbody>
<tr>
<th   colspan="1" rowspan="1" align="" valign=""><p>사용 사례</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>설명</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>사용자 프로필 사진</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>사용자 프로필 사진은 일반적으로 동일한 해상도의 원형 또는 정사각형 이미지입니다. 크기 조정 및 자르기를 사용하여 생성할 수 있습니다.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>신분증 사진</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>신분증 사진을 촬영할 때 문서의 신원 정보 부분만 유지하기 위해 잘라야 할 수 있습니다.</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>이미지 클로즈업</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>이미지의 핵심 부분에 클로즈업이 필요한 경우 이미지에서 잘라내야 합니다.</p></td>
</tr>
</tbody>
</table>

## 사용 방법
자세한 내용은 [실시간 이미지 처리](https://intl.cloud.tencent.com/document/product/266/42094)를 참고하십시오.

