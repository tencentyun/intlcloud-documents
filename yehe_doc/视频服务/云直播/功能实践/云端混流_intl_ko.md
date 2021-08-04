CSS 서비스는 라이브 방송 혼합 스트림 기능을 제공하며, 설정한 혼합 스트림 레이아웃 동기화에 따라 각 입력 원본 혼합 스트림을 새로운 스트리밍으로 만들어 라이브 방송 인터랙션 효과를 구현합니다. 또한 CSS 라이브 방송 혼합 스트림 기능은 API 3.0 인터페이스와도 연결할 수 있습니다. 자세한 내용은 [라이브 방송 혼합 스트림 인터페이스](https://intl.cloud.tencent.com/document/product/267/35997)를 참조하십시오. 본 문서에서는 각 시나리오에서 라이브 방송 혼합 스트림을 구현하는 방법에 대해 예시와 함께 설명합니다.

## 주의 사항
- 클라우드 혼합 스트림 기능을 사용하는 경우 표준 트랜스 코딩 비용이 발생합니다.
- 혼합 스트림 자르기 기능을 사용하는 경우 해당 매개변수는 원본 스트리밍 매개변수보다 클 수 없습니다.


## 기능 지원
- 동시에 최대 **16**개의 혼합 스트림을 지원합니다.
- **5**가지 입력 원본 유형(멀티미디어, 순수 오디오, 순수 비디오, 이미지, 캔버스)의 혼합 입력을 지원합니다.
- 혼합 스트림을 새로운 스트림으로 통합할 수 있습니다.
- 자르기, 워터마크 기능을 제공합니다.
- 템플릿 설정을 제공합니다.
- 혼합 스트림 녹화를 지원합니다.
- 자동 혼합 스트림을 지원합니다.
- 실시간 혼합 스트림 종류 및 위치 전환을 제공합니다.
- 혼합 스트림 실행과 취소가 무결성으로 매끄럽게 진행됩니다.


## 자주 사용하는 레이아웃 템플릿
자주 사용하는 템플릿으로는 10, 30, 40, 310, 390, 410, 510, 610이 있습니다. 해당 8가지의 템플릿 사용 시 입력 스트림에 위치 및 길이 매개변수를 입력할 필요 없이 **원본 화면과 동일한 비율로 축소/확대**되며, 템플릿 ID만 전달하면 됩니다.

**가장 자주 사용하는 레이아웃 템플릿 효과 이미지:**
<table>
<style>#m_img{width:90%;height:auto;display:block;margin-left:auto;margin-right:auto; }</style>
<thead><tr><th>템플릿 10</th><th >템플릿 30</th></tr></thead><tr>
<td><img src="https://main.qcloudimg.com/raw/a6b395f6fc7c1d07e4325836a3b725e6.jpg" id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/05fbe1c32bec1aed0624785d51b8a2ef.jpg"  id="m_img"></td>
</tr>
<thead><tr><th >템플릿 40</th><th>템플릿 310</th></tr></thead><tr>
<td><img src="https://main.qcloudimg.com/raw/06cd40976b29452fa297d52db0d3435c.jpg"  id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/e1f4aa6f198856c47d8175302c649448.jpg"  id="m_img"></td>
</tr>
<thead><tr><th>템플릿 390</th><th >템플릿 410</th></tr></thead><tr>
<td><img src="https://main.qcloudimg.com/raw/50157bb0b01d511c10b3637c13b1471a.png"  id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/6a420d03e7921453cbc461d1f1176f6c.jpg"  id="m_img"></td>
</tr>
<thead><tr><th>템플릿 510</th><th>템플릿 610</th></tr></thead>
<td><img src="https://main.qcloudimg.com/raw/c0e5bd29f275a6f055af9830ceea0a02.jpg"  id="m_img"></td>
<td><img src="https://main.qcloudimg.com/raw/5ca8ba33cc08e80d6aeb403645e75aac.jpg"  id="m_img"></td>


</tr>
</tbody></table>	



## 혼합 스트림 생성
### 매개변수 설명
자세한 내용은 [라이브 방송 혼합 스트림](https://intl.cloud.tencent.com/document/product/267/35997)을 참조하십시오.



### 시나리오1: 혼합 스트림-템플릿 20 사용 신청
사전 설정된 템플릿을 이용한 혼합 스트림

#### 입력 예시
```
https://live.tencentcloudapi.com/?Action=CreateCommonMixStream
&MixStreamSessionId=test_room
&MixStreamTemplateId=20
&OutputParams.OutputStreamName=test_stream1
&InputStreamList.0.InputStreamName=test_stream1
&InputStreamList.0.LayoutParams.ImageLayer=1
&InputStreamList.1.InputStreamName=test_stream2
&InputStreamList.1.LayoutParams.ImageLayer=2
&<공통 요청 매개변수>
```

#### 출력 예시
```
{
  "Response": {
    "RequestId": "e8fa8015-0892-40d5-95c4-12a4bc06ed31"
  }
}
```

#### 호스트 마이크 연결 혼합 스트림 효과
![img](https://main.qcloudimg.com/raw/a9bdfd2622e3152e61d8cb15a1b21aa1.jpg)


### 시나리오2: 혼합 스트림-템플릿 390 사용 신청
사전 설정된 템플릿을 이용한 혼합 스트림

#### 입력 예시

```
https://live.tencentcloudapi.com/?Action=CreateCommonMixStream
&MixStreamSessionId=test_room
&MixStreamTemplateId=390
&OutputParams.OutputStreamName=test_stream2
&InputStreamList.0.InputStreamName=test_stream1
&InputStreamList.0.LayoutParams.ImageLayer=1
&InputStreamList.0.LayoutParams.InputType=3
&InputStreamList.0.LayoutParams.ImageWidth=1920  (캔버스 너비)
&InputStreamList.0.LayoutParams.ImageHeight=1080 （캔버스 높이）
&InputStreamList.0.LayoutParams.Color=0x000000
&InputStreamList.1.InputStreamName=test_stream2
&InputStreamList.1.LayoutParams.ImageLayer=2
&InputStreamList.2.InputStreamName=test_stream3
&InputStreamList.2.LayoutParams.ImageLayer=3
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
  "Response": {
    "RequestId": "9d8d5837-2273-4936-8661-781aeab9bc9c"
  }
}
```

#### 호스트 PK 혼합 스트림 효과
![img](https://main.qcloudimg.com/raw/cad10f080a239725893e5221faa21c17.jpg)



###  시나리오3: 사용자 정의 혼합 스트림 예시
사용자 정의 레이아웃을 사용한 예시로, 위치 매개변수 LocationX와 LocationY는 작은 화면의 왼쪽 상단 꼭지점과 배경 화면 왼쪽 상단 꼭지점의 픽셀 절대 거리입니다.
![](https://main.qcloudimg.com/raw/e1f81cd4a9b08af4ad7e4658fc643f0d.png)

#### 입력 예시
```
https://live.tencentcloudapi.com/?Action=CreateCommonMixStream
&MixStreamSessionId=test_room
&OutputParams.OutputStreamName=test_stream2
&InputStreamList.0.InputStreamName=test_stream1
&InputStreamList.0.LayoutParams.ImageLayer=1
&InputStreamList.0.LayoutParams.InputType=3
&InputStreamList.0.LayoutParams.ImageWidth = 1920
&InputStreamList.0.LayoutParams.ImageHeight= 1080
&InputStreamList.0.LayoutParams.Color=0x000000
&InputStreamList.1.InputStreamName=test_stream2
&InputStreamList.1.LayoutParams.ImageLayer=2
&InputStreamList.1.LayoutParams.ImageWidth = 640
&InputStreamList.1.LayoutParams.ImageHeight= 360
&InputStreamList.1.LayoutParams.LocationX= 50
&InputStreamList.1.LayoutParams.LocationY= 720
&InputStreamList.2.InputStreamName=test_stream3
&InputStreamList.2.LayoutParams.ImageLayer=3
&InputStreamList.2.LayoutParams.ImageWidth = 640
&InputStreamList.2.LayoutParams.ImageHeight= 360
&InputStreamList.2.LayoutParams.LocationX= 740
&InputStreamList.2.LayoutParams.LocationY= 720
&<공통 요청 매개변수>
```


#### 출력 예시
```
{
  "Response": {
    "RequestId": "8c443359-ba07-4b81-add8-a6ff54f9bf54"
  }
}
```


#### 사용자 정의 혼합 스트림 효과
![](https://main.qcloudimg.com/raw/db6a87baba1f1891f514d4bea9b38ee4.png)

## 혼합 스트림 취소
### 매개변수 설명
자세한 내용은 [범용 혼합 스트림 취소](https://intl.cloud.tencent.com/zh/document/product/267/35998)를 참조하십시오.

### 시나리오 예시
session id에 따른 혼합 스트림 취소
#### 입력 예시
```
https://live.tencentcloudapi.com/?Action=CancelCommonMixStream
&MixStreamSessionId=test_room
```

#### 출력 예시
```
{
  "Response": {
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```

>! 
>- 혼합 스트림을 신청하고 최소 5초 후에 취소할 수 있습니다.
>- 혼합 스트림을 취소하고 30초 후에 동일한 session id의 혼합 스트림을 신청할 수 있습니다.


## 에러 코드
클라우드 혼합 스트림 API 3.0 인터페이스에서 자주 발생하는 에러 코드 대부분은 이미 [API 3.0 에러 코드](https://intl.cloud.tencent.com/document/product/267/35997#6.-.E9.94.99.E8.AF.AF.E7.A0.81) 스타일에 마이그레이션 되었습니다. 그러나 일부 커버되지 않는 에러 코드가 여전히 존재하며, 해당 에러 코드는 InvalidParameter 에러로 표시되어 Message에 `err_code [ $code ],msg [ $message ]` 형식으로 제공됩니다. 해당 code의 자세한 원인은 다음과 같습니다.

<table>
<thead><tr><th>에러 코드</th><th>원인</th><th>권장 진단 방법</th></tr></thead>
<tbody><tr>
<td>-1</td>
<td>입력 매개변수 리졸브 오류</td>
<td><ul style="margin:0">
    <li>요청 본문 body json 포맷이 정확한지 확인합니다.</li>
    <li>InputStreamList가 비어 있는지 확인합니다.</li>
    </ul></td>
</tr><tr>
<td>-2</td>
<td>입력 매개변수 오류</td>
<td> 화면 매개변수의 오버플로우 여부를 확인합니다.</td>
</tr><tr>
<td>-3</td>
<td>스트림 개수 오류</td>
<td>입력 스트림 개수가 [1, 16] 범위 내에 있는지 확인합니다.</td>
</tr><tr>
<td>-4</td>
<td>스트림 매개변수 오류</td>
<td><ul style="margin:0">
    <li>입출력 길이가 (0, 3000) 범위 내에 있는지 확인합니다.</li>
    <li>입력 스트림 개수가 (0, 16) 범위 내에 있는지 확인합니다.</li>
    <li>입력 스트림에 LayoutParams가 있는지 확인합니다.</li>
    <li>InputType 지원 여부를 확인합니다. (적합한 값: 0, 2, 3, 4, 5)</li>
    <li>스트림 ID 길이가 (1, 80)을 만족하는지 확인합니다.</li>
    </ul></td>
</tr><tr>
<td>-11</td>
<td>이미지 레이어 오류</td>
<td><ul style="margin:0">
    <li>이미지 레이어 개수 및 입력 스트림 개수가 일치하는지 확인합니다.</li>
    <li>이미지 레이어 ID가 중복되었는지 확인합니다.</li>
    <li>이미지 레이어 ID가 (0, 16) 범위에 있는지 확인합니다.</li>
    </ul></td>
</tr><tr>
<td>-20</td>
<td>입력 매개변수와 인터페이스가 매칭되지 않음</td>
<td><ul style="margin:0">
    <li>입력 스트림 개수가 템플릿 ID와 매칭되어 있는지 확인합니다.</li>
    <li> 컬러 매개변수가 정확한지 확인합니다.</li>
    </ul></td>
</tr><tr>
<td>-21</td>
<td>혼합 스트림의 입력 스트림 개수 오류</td>
<td>입력 스트림 개수가 2개 이상인지 확인합니다.</td>
</tr><tr>
<td>-28</td>
<td>배경 길이 획득 실패</td>
<td><ul style="margin:0">
    <li>캔버스를 설정한 경우, 캔버스 길이를 설정했는지 확인합니다.</li>
    <li>배경 스트림이 있는지 확인합니다. (푸시 스트림 후 5초 후에 다시 혼합 스트림을 진행해야 함)</li>
    </ul></td>
</tr><tr>
<td>-29</td>
<td>자르기 매개변수 오류</td>
<td>자르기 위치가 스트림 길이를 초과했는지 확인합니다.</td>
</tr><tr>
<td>-33</td>
<td>워터마크 이미지 ID 오류</td>
<td>입력 이미지 ID가 설정되었는지 확인합니다.</td>
</tr><tr>
<td>-34</td>
<td>워터마크 이미지 URL 획득 실패</td>
<td>이미지 업로드가 완료되었는지, URL이 생성되었는지 확인합니다.</td>
</tr><tr>
<td>-111</td>
<td>OutputStreamName 매개변수와 OutputStreamType이 매칭되지 않음</td>
<td><ul style="margin:0">
    <li>OutputStreamType이 0인 경우, 반드시 OutputStreamName이 InputStreamList에 존재해야 합니다.</li>
    <li>OutputStreamType이 1인 경우, OutputStreamName이 InputStreamList에 없어야 합니다.</li>
    </ul></td>
</tr><tr>
<td>-300</td>
<td>출력 스트림 ID가 이미 사용됨</td>
<td>해당 출력 스트림이 다른 혼합 스트림의 출력 스트림인지 확인합니다.</td>
</tr><tr>
<td>-505</td>
<td>입력 스트림을 upload에서 찾을 수 없음</td>
<td>푸시 스트림을 완료하고 5초 후에 혼합 스트림을 진행했는지 확인하고, 재생 가능한지 확인합니다.</td>
</tr><tr>
<td>-507</td>
<td>스트림 길이 매개변수 조회 실패</td>
<td><ul style="margin:0">
    <li>캔버스 너비, 높이를 설정했는지 확인합니다.</li>
    <li>푸시 스트림이 완료되었는지 확인하고, 푸시 스트림 후 5초 후에 다시 혼합 스트림을 진행하기 바랍니다.</li>
    </ul></td>
</tr><tr>
<td>-508</td>
<td>출력 스트림 ID 오류</td>
<td>동일한 MixStreamSessionId에서 서로 다른 출력 스트림 ID를 사용했는지 확인합니다.</td>
</tr><tr>
<td>-10031</td>
<td>혼합 스트림 트리거 실패</td>
<td>푸시 스트림 후 5초 후에 다시 혼합 스트림을 진행하시기 바랍니다.</td>
</tr><tr>
<td>-30300<br>-31001<br>-31002</td>
<td>혼합 스트림 취소 시 sessionid 없음</td>
<td>MixStreamSessionId가 있는지 확인합니다.</td>
</tr><tr>
<td>-31003</td>
<td>출력 스트림 ID와 session의 출력 스트림 ID가 매칭되지 않음</td>
<td>혼합 스트림 취소 시 입력한 출력 스트림 ID를 확인합니다.</td>
</tr><tr>
<td>-31004</td>
<td>출력 스트림 비트레이트 부적합</td>
<td>출력 스트림 비트레이트가 [1, 50000] 범위에 있는지 확인합니다.</td>
</tr><tr>
<td>기타</td>
<td>기타 오류입니다. <a href="https://intl.cloud.tencent.com/contact-sales">고객 서비스</a>에 문의하여 기술 지원을 받으십시오.</td>
<td>-</td>
</tr>
</tbody></table>

## FAQ
- [푸시 스트림 후 혼합 스트림 시 -505 에러 코드가 리턴되는 이유는 무엇인가요?](https://intl.cloud.tencent.com/document/product/267/38255#que1)
- [혼합 스트림 신청 후 혼합 스트림을 취소하지 않을 경우 어떻게 되나요?](https://intl.cloud.tencent.com/document/product/267/38255#que5)
- [혼합 스트림의 보조 호스트 화면이 예상 위치와 다른 이유는 무엇인가요?](https://intl.cloud.tencent.com/document/product/267/38255#que9)

>? 클라우드 혼합 스트림 관련 자세한 문제는 [클라우드 혼합 스트림 관련](https://intl.cloud.tencent.com/document/product/267/38255)을 참조하십시오.
