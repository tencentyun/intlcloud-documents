## 작업 시나리오
[VOD 콘솔](https://console.cloud.tencent.com/vod/pics)을 통해 이미지 처리 작업을 수행할 수 있습니다. 본문은 이미지 처리 템플릿을 통해 실시간 이미지 처리를 수행하는 방법을 소개합니다. URL 매핑 방식을 통해 이미지 처리 효과를 빠르게 얻을 수 있습니다.

## 작업 단계
### 1단계: 이미지 업로드
1. [VOD 콘솔](https://console.cloud.tencent.com/vod/pics)에서 비관리자(메인 애플리케이션)를 선택한 후 [미디어 자산 관리]>[[이미지 관리](https://console.cloud.tencent.com/vod/pics)]에서 [이미지 업로드]를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/fed2ab4f8f9b94f15bae2c3c734a0f41.png)
2. 업로드할 이미지을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/592b99b27e42cb3734132ee8acc5f51e.png)
3. [업로드 시작]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/300743187dc0a04f37bfdbb839074a63.png)
4. 업로드를 마칩니다. [관리]를 클릭하면 업로드된 이미지의 가속 URL 주소를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ac55111bc39488563f7abc3412cd9a54.png)

### 2단계: 템플릿 만들기

VOD API 및 보다 자세한 API 구성을 통해 이미지 처리 템플릿을 생성할 수 있습니다.

1. 240 x 240 썸네일 템플릿 생성 예시:
```shell
https://vod.tencentcloudapi.com/?Action=CreateImageProcessingTemplate
&Operations.0.Type=Scale
&Operations.0.Scale.Type=ShortEdgeFirst
&Operations.0.Scale.ShortEdge=240
&Operations.1.Type=CenterCut
&Operations.1.CenterCut.Type=Rectangle
&Operations.1.CenterCut.Width=240
&Operations.1.CenterCut.Height=240
&<공통 요청 매개변수>
```
2. 이미지 처리 템플릿 번호 1009 반환 요청.
```javascript
{
  "Response": {
    "Definition": 1009,
    "RequestId": "12ae8d8e-dce3-4151-9d4b-5594145287e1"
  }
}
```

### 3단계: 이미지 처리

이미지 처리는 URL 매핑으로 수행되며 공식은 다음과 같습니다.
#### 처리된 이미지 URL = 원본 이미지 URL + 간격 식별자 + 이미지 템플릿 번호 + ‘.’ + 출력 이미지 형식
  - 이미지 원본 URL: [VOD](https://console.cloud.tencent.com/vod/pics)에 이미지 파일 업로드 후 가속 URL 주소가 생성됩니다.
  - 간격 식별자: !
  - 출력 이미지 형식: JPG, JPEG, PNG.


### 4단계: 처리 유형
이미지 처리는 확대/축소 및 자르기 두 가지 유형을 지원합니다.

<Table>
<tbody>
<tr>
<th>작업 유형</th>
<th>세부 작업</th>
</tr>

<tr>
<td rowspan=5>약칭</td>
<td>너비를 지정하고 비율에 따라 높이가 조정됩니다.</td>
</tr>

<tr>
<td>높이를 지정하고 비율에 따라 너비가 조정됩니다.</td>
</tr>

<tr>
<td>긴 변을 지정하고 비율에 따라 짧은 변이 조정됩니다.</td>
</tr>

<tr>
<td>짧은 변을 지정하고 비율에 따라 긴 변이 조정됩니다.</td>
</tr>

<tr>
<td>너비와 높이를 지정하고 비율이 강제 고정됩니다.</td>
</tr>

<tr>
<td rowspan=2>자르기</td>
<td>내접원 자르기. 자르기할 반경을 지정합니다.</td>
</tr>

<tr>
<td>직사각형 자르기. 자르기의 너비와 높이를 지정합니다.</td>
</tr>

</tbody>
</Table>

#### 유형1. 썸네일

- **너비를 지정하고 비율에 따라 높이 조정**
 - 템플릿 생성: 10033, 지정 너비: 700, 출력 형식: PNG
 - 처리된 이미지 링크: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10033.PNG`
 - 최종 효과:
![](https://main.qcloudimg.com/raw/abf6f0699647efe9bef7f22d8f3fb939.png)

- **높이를 지정하고 비율에 따라 너비 조정**
 - 템플릿 생성: 10034, 지정 높이: 700, 출력 형식: PNG
 - 처리된 이미지 링크: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10034.PNG`
 - 최종 효과:
![](https://main.qcloudimg.com/raw/df5c784021a55910a67bd3fcf1be1ac8.png)

- **긴 변을 지정하고 비율에 따라 짧은 변 조정**
 - 템플릿 생성: 10035, 긴 변 지정: 300, 출력 형식: PNG
 - 처리된 이미지 링크: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10035.PNG`
 - 최종 효과:
![](https://main.qcloudimg.com/raw/fca36a5152c013ec9f111923f1f37b97.png)

- **짧은 변을 지정하고 비율에 따라 긴 변 조정**
 - 템플릿 생성: 10036, 짧은 변 지정: 300, 출력 형식: PNG
 - 처리된 이미지 링크: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10036.PNG`
 - 최종 효과:
![](https://main.qcloudimg.com/raw/e3f9bd39fe92b57758d8954d44715d93.png)

- **너비와 높이를 지정하고 비율 강제 고정**
 - 템플릿 생성: 10037, 지정 높이: 300, 지정 너비: 300, 출력 형식: PNG
 - 처리된 이미지 링크: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10037.PNG`
 - 최종 효과:
![](https://main.qcloudimg.com/raw/4225aa7986ac5f2f58b6cf061b51f64d.png)

#### 유형2. 자르기
- **내접원 자르기**
 - 템플릿 생성: 10038, 출력 이미지 반경 지정: 300, 출력 형식: PNG
 - 처리된 이미지 링크: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10038.PNG`
 - 최종 효과:
![](https://main.qcloudimg.com/raw/e62ef7791ff9b129259bd3fa04afd6d2.png)

- **직사각형 자르기**
 - 템플릿 생성: 10039, 출력 이미지 너비: 300, 출력 이미지 높이: 300, 출력 형식: PNG
 - 처리된 이미지 링크: `http://1500003022.vod2.myqcloud.com/6c99162fvodcq1500003022/8215ff285285890811169205193/FcbdNXl2pswA.jpg!10039.PNG`
 - 최종 효과:
![](https://main.qcloudimg.com/raw/433ea68294a8b8af47bae088e7a89508.png)

