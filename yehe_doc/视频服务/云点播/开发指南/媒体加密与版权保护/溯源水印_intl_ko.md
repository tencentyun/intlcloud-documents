유료 동영상 플랫폼이 직면한 가장 큰 문제는 일부 사용자가 동영상을 다양한 방식으로 다운로드하여 승인 없이 다른 플랫폼에 공유하거나 판매할 수 있다는 것입니다. 이는 저작권자의 이익을 심각하게 손상시킵니다. 무단 비디오 녹화는 비디오 불법 복제의 주요 형태입니다. 해적들은 종종 화면 녹화 소프트웨어를 사용하여 비디오를 녹화하고 카메라를 사용하여 직접 화면을 녹화하는 경우도 있습니다. 이는 방지하기 어렵습니다. 무단 비디오 녹화를 억제하는 가장 효과적인 방법 중 하나는 불법 복제 및 기타 수단을 통해 저작권 콘텐츠를 보호하고 불법 복제를 방지하며 보상을 요구하는 것입니다. VOD의 디지털 워터마크 기능은 낮은 비용으로 높은 보안 수준을 보장하며, 무단으로 녹화된 영상을 쉽게 추적할 수 있도록 도와줍니다.

## 기존 워터마크의 단점

무단 비디오 녹화에 대한 기존의 대응책은 비디오 이미지에 시청자의 사용자 ID를 추가하는 것입니다. 크게 두 가지 방법이 있습니다. **일반 이미지 및 텍스트 워터마크**를 추가하거나 **플레이어 플로팅 워터마크**를 추가하는 것입니다.

<table>
   <tr>
      <th width="0px" style="text-align:center">일반 이미지 및 텍스트 워터마크</td>
      <th width="0px" style="text-align:center">플레이어 플로팅 워터마크</td>
   </tr>
   <tr>
      <td><img src="https://qcloudimg.tencent-cloud.cn/raw/82766338aee9f4f9715427e337babd25.png" width=500>트랜스 코딩 중에 비디오 이미지에 인코딩된 이미지 또는 텍스트 워터마크입니다. 텍스트 내용은 사용자 ID입니다.

</td>
      <td><img src="https://qcloudimg.tencent-cloud.cn/raw/69dbaf292d144094854efca31e51d922.png" width=500>
			플레이어에서 재생하는 동안 비디오 레이어를 덮는 워터마크. 일반적으로 비디오 이미지의 뉴스 티커처럼 움직입니다.</td>
   </tr>
</table>
이 두 가지 유형의 워터마크에는 다음과 같은 특성이 있습니다.

|  | 일반 이미지 및 텍스트 워터마크 | 플레이어 플로팅 워터마크 |
| -- | -- | -- |
| 보안성 | 높음: 워터마크가 비디오에 인코딩되어 제거할 수 없습니다 | 낮음: 워터마크가 비디오 플레이어에 나타나지만 비디오에 인코딩되지 않습니다 |
| 비용 | 높음: 각 고유 사용자 ID 워터마크는 한 번 트랜스코딩되고 저장되어야 합니다 | 낮음: 플레이어에 포함됩니다 |
| 견고성 | 낮음: 워터마크가 고정된 위치에 있으며 쉽게 잘리거나 가려집니다 | 낮음: 워터마크가 보이고 쉽게 가려집니다 |
| 가시성 | 부족: 워터마크가 표시되며 방해가 될 수 있습니다 | 부족: 워터마크가 표시되며 방해가 될 수 있습니다 |


상기와 같이 두 가지 유형의 기존 워터마크는 몇 가지 단점이 있습니다.

## VOD 디지털 워터마크

VOD 디지털 워터마크는 저렴한 비용으로 높은 보안성을 제공할 수 있습니다.

* 저렴한 비용: 단 한 번의 트랜스코딩 및 스토리지 비용으로 수십억 명의 시청자를 태깅 및 추적합니다.
* 높은 보안성: 워터마크가 비디오 이미지에 인코딩되므로 비디오 데이터를 획득하더라도 제거할 수 없습니다.
* 높은 견고성: 리샘플링, 압축, 디더링, 크롭, 스케일링, 회전, 필터링 등 다양한 공격에 강합니다.
* 세련된 효과: 워터마크는 사람의 눈에는 보이지 않으며 비디오 품질에 영향을 미치지 않습니다.

>! VOD 디지털 워터마크는 현재 공개 베타 단계에 있으며 다음과 같은 사용 관련 제안 사항이 있습니다.
>1. **30분이 넘는** 동영상에 디지털 워터마크를 추가하십시오.
>2. 현재 라디오, TV, OTT 시나리오의 **영화, TV 시리즈 및 버라이어티 쇼**에서 워터마크 추출은 상대적으로 더 나은 성능을 보입니다.
>3. **온라인 교육** 영상의 워터마크 추출 효과는 현재 최적화 중 입니다. 공식 출시 후에 이 기능을 테스트하고 통합하시기 바랍니다.

## 사용 방법

### 디지털 워터마크 추가

[ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) API를 호출하여 비디오에 디지털 워터마크를 추가하는 작업을 시작합니다. 처리 유형으로 트랜스코딩 또는 어댑티브 비트레이트 스트리밍을 선택합니다.

#### 트랜스 코딩:
* STD-H264-HLS-720P(템플릿 ID 100230)와 같이 컨테이너 형식이 HLS인 트랜스코딩 템플릿을 선택합니다. 템플릿 ID를 MediaProcessTask.TranscodeTaskSet.Definition=100230에 전달합니다.
* MediaProcessTask.TranscodeTaskSet.TraceWatermark.Switch=ON을 전달하여 디지털 워터마크를 활성화합니다.

#### 어댑티브 비트레이트 스트리밍
* 어댑티브-HLS(템플릿 ID 10)와 같이 컨테이너 형식이 HLS인 어댑티브 비트레이트 스트리밍 템플릿을 선택합니다. 템플릿 ID를 MediaProcessTask.AdaptiveDynamicStreamingTaskSet.Definition=10에 전달합니다.
* MediaProcessTask.AdaptiveDynamicStreamingTaskSet.TraceWatermark.Switch=ON을 전달하여 디지털 워터마크를 활성화합니다.

### 비디오 재생

6자리 16진수 정수인 uv를 모든 유료 사용자와 연결해야 합니다. uv는 뷰어 추적 가능성에 대한 증거로 사용됩니다.

* VOD의 [Player SDK](https://intl.cloud.tencent.com/document/product/266/33977) 또는 [Player Adapter](https://intl.cloud.tencent.com/document/product/266/42095)를 사용하는 경우 비즈니스 서버는 각 재생 요청에 대해 [Player 서명](https://intl.cloud.tencent.com/document/product/266/38099)을 배포해야 합니다. [서명 매개변수](https://intl.cloud.tencent.com/document/product/266/38099#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0)에 뷰어 uv를 uv로 입력해야 합니다.
* VOD Player SDK를 사용하지 않는 경우 [Key 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33986) 규칙에 따라 URL의 QueryString에 뷰어 uv를 추가해야 합니다.

### 워터마크 추출

자신의 동영상이 불법 복제된 사실을 알게 된 경우 [ExtractTraceWatermark API](https://www.tencentcloud.com/document/product/266/50423)를 호출하여 동영상을 불법 복제한 뷰어의 uv를 추출할 수 있습니다.

## 작업 단계
다음 단계에 따라 디지털 워터마크를 추가하고 뷰어 ID를 추출합니다.

[](id:step1)
### 1단계: 동영상 업로드

1. VOD 콘솔의 왼쪽 사이드바에서 **비디오 관리**>**오디오/비디오 관리**를 선택하고 **오디오/비디오 업로드**를 클릭하고 비디오를 업로드하십시오.
2. 동영상을 업로드한 후 동영상 ID를 기록해 둡니다.

[](id:step2)
### 2단계: 디지털 워터마크 추가

1. [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125)를 참고하고 [API Explorer](https://console.cloud.tencent.com/api/explorer)를 사용하여 어댑티브 비트 레이트 스트리밍 작업을 시작합니다.
 * FileId 에 **[1단계](#step1)**에서 업로드한 동영상의 ID를 입력합니다.
 * MediaProcessTask.AdaptiveDynamicStreamingTaskSet.0.Definition에 10을 입력합니다. 이는 어댑티브 비트 레이트 스트리밍 템플릿 10으로 코드 변환을 나타냅니다.
 * 디지털 워터마크를 활성화하는 MediaProcessTask.AdaptiveDynamicStreamingTaskSet.0.TraceWatermark.Switch에 대해 ON을 입력합니다.
2. 작업이 완료되면 콘솔의 왼쪽 사이드바에서 **비디오 관리**>**오디오/비디오 관리**를 선택하고 대상 비디오를 찾은 다음 **관리**를 클릭합니다. **어댑티브 비트 레이트 스트리밍 템플릿 목록**에서 템플릿 10의 어댑티브 비트스트림을 찾아 **URL 복사**를 클릭하고 재생 URL을 기록해 둡니다.

[](id:step3)
### 3단계: 동영상 재생

1. **[2단계](#step2)**에서 얻은 재생 URL에 uv(12abcd와 같은 6자리 16진수 정수)를 추가하여 `http://xxx.vod2.myqcloud.com/xxx/xxx/xxx.m3u8?uv=12abcd`와 유사한 새 URL을 얻습니다. URL을 복사하여 브라우저에 붙여넣어 동영상을 재생합니다.

[](id:step4)
### 4단계: 비디오 불법 복제 시뮬레이션

1. VOD 콘솔의 왼쪽 사이드바에서 **비디오 관리**>**오디오/비디오 관리**를 선택하고 **오디오/비디오 업로드**를 클릭하고 업로드 방법으로 **비디오 풀링**을 선택하고 행 추가를 클릭하고 3단계에서 얻은 비디오의 URL을 입력합니다.
2. 작업이 완료되면 VOD 콘솔에서 **비디오 관리**>**오디오/비디오 관리**를 선택하고 업로드된 영상을 찾아 **관리**를 클릭합니다. 재생 URL을 찾아 **URL 복사**를 클릭한 다음 재생 URL을 기록해 둡니다.

[](id:step5)
### 5단계: 워터마크 추출

1. [ExtractTraceWatermark](https://www.tencentcloud.com/document/product/266/50423)를 참고하고 [API Explorer](https://console.cloud.tencent.com/api/explorer)를 사용하여 워터마크 추출 작업을 시작합니다. URL에는 **[4단계](#step4)**에서 업로드한 동영상의 재생 URL을 입력합니다.
2. 작업이 완료되면 [DescribeTaskDetail](https://console.cloud.tencent.com/workorder/category)을 참고하여 [API Explorer](https://console.cloud.tencent.com/api/explorer)를 통해 작업 세부 정보를 확인합니다. **[3단계](#step3)**에서 얻은 uv는 작업 출력에서 찾을 수 있습니다.

## 요금 관련

디지털 워터마크 기능을 사용하면 다음과 같은 비용이 발생합니다.

* 트랜스 코딩 요금: 비디오에 디지털 워터마크를 추가할 때 트랜스 코딩 또는 어댑티브 비트레이트 스트리밍을 수행해야 하므로 트랜스 코딩 비용이 발생합니다.
* 워터마크 요금: 비디오에 디지털 워터마크를 추가할 경우 워터마크 요금이 발생합니다.
* 스토리지 요금: 트랜스 코딩 또는 어댑티브 비트 레이트 스트리밍의 출력 비디오는 스토리지 공간을 사용하므로 스토리지 요금이 발생합니다.
* 추출 요금: 불법 복제 발견 후 해적의 사용자 ID를 추출할 때 추출 요금이 발생합니다.

상기 과금 항목의 구체적인 단가는 [사용량 과금(후불 일 결산)](https://intl.cloud.tencent.com/document/product/266/14666)을 참고하십시오.
