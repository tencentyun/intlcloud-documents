CSS는 타임시프트 기능을 업그레이드했습니다. 콘솔에서 타임시프트 템플릿을 생성하면 이제 새로운 타임시프트 기능을 활성화하게 됩니다. 필요한 형식으로 URL을 생성하고 URL을 사용하여 이전 시점의 콘텐츠를 재생할 수 있습니다. API 3.0은 이제 타임시프트 기능에도 사용할 수 있습니다. 자세한 내용은 [Time Shifting APIs](https://intl.cloud.tencent.com/document/product/267/30760)를 참고하십시오. 본문은 타임시프트 기능의 작동 방식과 재생 요청 방법을 보여줍니다.

## 참고
- 새로운 타임시프트 기능은 현재 동시 시청자 3만명을 지원합니다. 더 높은 동시성이 필요한 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)하십시오.
- 재생 도메인에 대한 인증을 활성화하고 만료 시간을 구성한 경우 타임시프트 URL은 지정된 시간 이후에 만료됩니다.
- VOD 도메인에서 콘텐츠를 가져오는 [구버전 타임시프트 기능](https://intl.cloud.tencent.com/document/product/267/31565)을 사용하려면 티켓을 제출해야 합니다. 더 나은 경험을 위해 새로운 타임시프트 기능을 사용하는 것이 좋습니다.

## 타임시프트 원리
CSS는 라이브 스트림을 TS 세그먼트로 저장하고 각 TS 세그먼트의 재생 시간에 대한 정보를 클라우드에 저장하여 타임시프트를 가능하게 합니다. 이 기능은 종종 TV 프로그램이나 스포츠 이벤트의 하이라이트를 재생하는 데 사용됩니다. 콘텐츠는 HLS를 통해 클라이언트에 배포됩니다. M3U8 요청 매개변수를 설정하여 정확한 재생 시간을 지정할 수 있습니다(자세한 내용은 [재생 요청](#play) 참고).

[](id:play)
## 재생 요청
타임시프트 URL의 형식은 `http://domain/appname/stream.m3u8`입니다. 타임시프트에는 두 가지 유형이 있습니다.
- 특정 시간 동안 재생합니다. 스포츠 이벤트의 하이라이트를 재생하는 데 적합합니다.
- 특정 시간 이전부터 재생합니다. 라이브 스트림의 재생을 지연하려는 경우에 적합합니다.

### 특정 시간 재생 매개변수 요청
<table id="setmess">
<tr><th width="14%">매개변수</th><th>설명</th><th>필수 여부</th><th>예시</th>
</tr><tr>
<td>txTimeshift</td>
<td>새로운 타임시프트 기능 활성화 여부(on: 활성화)</td>
<td>Yes</td>
<td>txTimeshift=on</td>
</tr><tr>
<td>tsStart</td>
<td>타임시프트 시작 시간</td>
<td>Yes</td>
<td>tsStart=20121010010101</td>
</tr><tr>
<td>tsEnd</td>
<td>타임시프트 종료 시간</td>
<td>Yes</td>
<td>td>tsEnd=20121010010102</td>
</tr><tr>
<td>tsFormat</td>
<td><ul style="margin:0">
<li>tsStart 및 tsEnd의 형식입니다. 이 매개변수의 값은 <code>{timeformat}_{unit}_{zone}</code>형식입니다.</li>
<li>timeformat의 유효한 값:<ul>
<li/>UNIX - UNIX 타임스탬프. 이 형식을 사용하는 경우 zone을 지정할 필요가 없습니다
<li/>human - 20121010010101과 같이 사람이 읽을 수 있는 시간입니다</ul></li>
<li>unit: s|ms</li>
<li>단위 s 및 ms</li>
  <li>zone: 시간대는 동부와 서부 지역으로 구분:<ul style="margin:0"><li>동부 시간대 범위: 1~12<li>서부 시간대 범위: -12~-1</ul></li>
</ul></td>
<td>Yes</td>
<td>tsFormat=unix_s
tsFormat=human_s_8</td>
</tr><tr>
<td>tsCodecname</td>
<td>트랜스코딩된 스트림의 경우 이 매개변수를 트랜스코딩 템플릿의 ID로 설정합니다. 원본 스트림이나 워터마크가 있는 스트림의 경우 이 매개변수를 생략하십시오.</td>
<td>No</td>
<td>tsCodecname=hd</td>
</tr></table>



#### 요청 예시1(Unix 타임스탬프)
```
http://example.domain.com/live/stream.m3u8?txTimeshift=on&tsFormat=unix_s&tsStart=1675302995&tsEnd=1675303025&tsCodecname=test
```
#### 요청 예시2(human이 읽을 수 있는 시간)
```
http://example.domain.com/live/stream.m3u8?txTimeshift=on&tsFormat=unix_s_8&tsStart=20230202095635&tsEnd=20230202095705&tsCodecname=test
```

### 특정 시간 이전부터 재생하기 위한 매개변수 요청

| 매개변수    | 설명                    | 필수 여부 | 예시                                |
| ----------- | ----------------------- | ---------- | ----------------------------------- |
| txTimeshift | 새로운 타임시프트 기능 활성화 여부(on: 활성화) | Yes         | txTimeshift=on                      |
| tsDelay     | 재생을 지연할 시간(초)    | Yes         | tsDelay=30은 재생이 30초 전부터 시작됨을 나타냅니다 |
| tsCodecname | 트랜스코딩된 스트림의 경우 이 매개변수를 트랜스코딩 템플릿의 ID로 설정합니다  | No         | tsCodecname=2000                    |

#### 요청 예시
```
http:://example.domain.com/live/stream.m3u8?txTimeshift=on&tsDelay=30&tsCodecname=test
```
### 타임시프트 인증 매개변수
타임시프트를 위한 인증 매개변수는 재생 시와 동일합니다. 자세한 내용은 [재생 인증 설정](https://intl.cloud.tencent.com/document/product/267/31060)을 참고하십시오(콘솔에서 생성된 HLS URL은 하루 동안만 유효함).

### 타임시프트 스트림 쿼리
콘솔의 타임시프트-타임시프트 세부 정보 페이지에는 타임시프트된 스트림 목록이 표시됩니다. 세부 정보를 클릭하면 타임시프트 스트림의 세부 정보를 볼 수 있습니다.
API를 사용하여 타임시프트 스트림과 스트림의 구체적인 세부 정보를 쿼리할 수도 있습니다. 자세한 내용은 다음 문서를 참고하십시오.
- [CSS DescribeTimeShiftStreamList-API 문서-문서 센터-Tencent Cloud](https://www.tencentcloud.com/document/product/267/53719)
- [CSS DescribeTimeShiftRecordDetail-API 문서-문서 센터-Tencent Cloud](https://www.tencentcloud.com/document/product/267/53720)