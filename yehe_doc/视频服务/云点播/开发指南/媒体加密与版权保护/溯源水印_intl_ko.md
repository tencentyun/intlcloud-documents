유료 비디오 플랫폼이 직면한 가장 큰 문제 중 하나는 비디오의 무단 다운로드 및 공유입니다. 이는 저작권자의 이익을 심각하게 손상시킵니다. 비디오 무단 녹화는 비디오 불법 복제의 가장 일반적인 형태입니다. 해적들이 화면 녹화 소프트웨어를 사용하여 비디오를 녹화하거나 물리적 카메라를 사용하여 화면을 직접 녹화하는 것은 방지하기 어렵습니다.

무단 비디오 녹화를 억제하는 효과적인 방법은 불법 복제 추적 및 기타 수단을 통해 저작권 콘텐츠를 보호하고 불법 복제를 방지하며 보상을 요구하는 것입니다. VOD의 디지털 워터마크는 낮은 비용으로 높은 보안 수준을 보장하며, 무단으로 녹화된 영상을 쉽게 추적할 수 있도록 도와줍니다.

## 기존 워터마크의 단점

무단 비디오 녹화에 대한 기존의 대응책은 비디오 이미지에 시청자의 사용자 ID를 추가하는 것입니다. 크게 두 가지 방법이 있습니다. **일반 이미지 및 텍스트 워터마크**를 추가하거나 **플레이어 플로팅 워터마크**를 추가하는 것입니다.

<table>
   <tr>
      <th width="0px" style="text-align:center">일반 이미지 및 텍스트 워터마크</td>
      <th width="0px" style="text-align:center">플레이어 플로팅 워터마크</td>
   </tr>
   <tr>
      <td><img src="https://qcloudimg.tencent-cloud.cn/raw/82766338aee9f4f9715427e337babd25.png" width=500>

</td>
      <td><img src="https://qcloudimg.tencent-cloud.cn/raw/69dbaf292d144094854efca31e51d922.png" width=500>
			플레이어에서 재생하는 동안 비디오 레이어를 덮는 워터마크. 일반적으로 비디오 이미지의 뉴스 티커처럼 움직입니다.</td>
   </tr>
</table>
이 두 가지 유형의 워터마크는 보안 및 비용 측면에서 다음과 같은 특성을 가지고 있습니다.

| 워터마크 메소드 | 보안 | 비용 |
| -- | -- | -- |
| 일반 이미지 및 텍스트 워터마크 | 높음: 워터마크가 비디오에 인코딩되어 제거할 수 없음 | 높음: 각 고유 사용자 ID 워터마크는 한 번 트랜스코딩되어 저장되어야 함 |
| 플레이어 플로팅 워터마크 | 낮음: 워터마크가 비디오 플레이어에 나타나지만 비디오에 인코딩되지 않음 | 낮음: 플레이어에 내장됨 |

상기 내용 처럼 이 두 가지 유형의 기존 워터마크 중 어느 것도 높은 보안과 낮은 비용을 동시에 제공할 수 없습니다.

## VOD 디지털 워터마크

### 원리
<img src="https://qcloudimg.tencent-cloud.cn/raw/ccfa5b05ef291a3a115ca336e8a9cbab.jpg" width=999>

VOD의 디지털 워터마크는 AB 스트림 기반 기술을 사용합니다:

* 스트림 A와 B는 소스 비디오에서 트랜스 코딩되고 분할됩니다(스트림 A와 B의 차이는 워터마크 위치임).
* CDN은 각 최종 사용자에 대해 고유한 AB 결합 스트림을 출력합니다.
* 불법 복제 영상에서 AB 워터마크 시퀀스를 추출한 후 워터마크에서 사용자 ID를 추출합니다.

### 장점

AB 스트림 기반 디지털 워터마크는 저렴한 비용으로 높은 보안성을 제공할 수 있습니다.

* 저렴한 비용: 비디오에 대해 스트림 A와 B만 트랜스 코딩하면 됩니다. 즉, 수십억 명의 시청자를 표시하고 추적하는 데 두 개의 스트림을 트랜스 코딩하고 저장하는 비용만 소요됨을 의미합니다.
* 높은 보안성: 워터마크가 비디오 이미지에 인코딩되므로 비디오 데이터를 획득하더라도 제거할 수 없습니다.

## 사용 방법

### 디지털 워터마크 추가

콘솔에서 또는 API를 통해 이미지 워터마크 템플릿을 생성합니다.
[ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) API를 호출하여 320초 이상 비디오에 디지털 워터마크를 추가하는 작업을 시작합니다.
* 트랜스 코딩의 출력 비디오에 디지털 워터마크를 추가하려면 워터마크 템플릿 ID를 MediaProcessTask.TranscodeTaskSet.TraceWatermark.Definition에 전달합니다.
* 어댑티브 비트 레이트 스트리밍의 출력 비디오에 디지털 워터마크를 추가하려면 워터마크 템플릿 ID를 MediaProcessTask.AdaptiveDynamicStreamingTaskSet.TraceWatermark.Definition에 전달합니다.

### 비디오 재생

8자리 16진법 정수인 uid를 모든 유료 사용자와 연결해야 합니다. uid는 뷰어 추적 가능성에 대한 증거로 사용됩니다.

* VOD의 [Player SDK](https://intl.cloud.tencent.com/document/product/266/33977) 또는 [타사 Player 플러그 인](https://intl.cloud.tencent.com/document/product/266/42095)을 사용하는 경우 비즈니스 서버는 각 재생 요청에 대해 [Player 서명](https://intl.cloud.tencent.com/document/product/266/38099)을 할당해야 합니다. [서명 매개변수](https://intl.cloud.tencent.com/document/product/266/38099#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0)에 시청자 uid를 uid로 입력해야 합니다.
* VOD Player SDK를 사용하지 않는 경우 [Key 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33986) 규칙에 따라 URL의 QueryString에 시청자 uid를 추가해야 합니다.

### 워터마크 추출

자신의 동영상이 불법 복제된 사실을 알게 되면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하여 불법 복제된 동영상 파일과 워터마크 템플릿 ID를 제공할 수 있습니다. VOD는 해당 영상을 불법 복제한 시청자의 uid를 추출할 것입니다.

## 작업 단계
다음 단계에 따라 디지털 워터마크를 추가하고 뷰어 ID를 추출합니다.
[](id:step1)
### 1단계: 워터마크 템플릿 생성
1. [VOD 콘솔](https://console.cloud.tencent.com/vod)에 로그인하고 왼쪽 사이드바에서 **비디오 처리 설정**>**템플릿 설정**을 선택한 후 **워터마크 템플릿** 탭을 선택한 후 **워터마크 템플릿 생성**을 클릭합니다.
2. **워터마크 유형**으로 이미지 워터마크를 선택합니다. 워터마크 이미지를 업로드한 후 **생성**을 클릭합니다.
3. 새로 생성된 워터마크 템플릿의 워터마크 템플릿 ID를 기록해 둡니다.

[](id:step2)
### 2단계: 동영상 업로드

1. VOD 콘솔의 왼쪽 사이드바에서 **미디어 자원 관리**>**오디오/비디오 관리**를 선택하고 **오디오/비디오 업로드**를 클릭한 다음 비디오를 업로드합니다(6분 이상 권장).
2. 동영상을 업로드한 후 동영상 ID를 기록해 둡니다.

[](id:step3)
### 3단계: 디지털 워터마크 추가

1. [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125)를 참고하고 [API Explorer](https://console.cloud.tencent.com/api/explorer)를 사용하여 어댑티브 비트 레이트 스트리밍 작업을 시작합니다.
 * FileId 에 **[2단계](#step2)**에서 업로드한 동영상의 ID를 입력합니다.
 * MediaProcessTask.AdaptiveDynamicStreamingTaskSet.Definition에 10을 입력합니다. 이는 어댑티브 비트 레이트 스트리밍 템플릿 10으로 코드 변환을 나타냅니다.
 * MediaProcessTask.AdaptiveDynamicStreamingTaskSet.TraceWatermark.Definition에 대해 **[1단계](#step1)**에서 만든 워터마크 템플릿의 ID를 입력합니다.
2. 작업이 완료되면 콘솔의 왼쪽 사이드바에서 **미디어 자원 관리**>**오디오/비디오 관리**를 선택하고 대상 비디오를 찾은 다음 **관리**를 클릭합니다. **어댑티브 비트 레이트 스트리밍 템플릿 목록**에서 템플릿 10의 어댑티브 비트스트림을 찾아 **URL 복사**를 클릭하고 재생 URL을 기록해 둡니다.

### 4단계: 동영상 재생 및 촬영

1. **[3단계](#step3)**에서 얻은 재생 URL에 QueryString으로 uid(1234abcd와 같은 8자리 16진법 정수)를 추가하여`http://xxx.vod2.myqcloud.com/xxx/xxx/xxx.m3u8?uid=1234abcd`와 유사한 새 URL을 얻습니다. URL을 복사하여 브라우저에 붙여넣어 동영상을 재생합니다.
2. 인증되지 않은 동영상 녹화를 시뮬레이션하려면 브라우저에서 재생되는 동안 휴대폰을 사용하여 동영상을 녹화한 다음 녹화된 동영상을 동영상 파일로 저장합니다.

### 5단계: 워터마크 추출

VOD에 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 시 **4단계**에서 획득한 영상과 **[1단계](#step1)**에서 생성한 워터마크 템플릿 ID를 제공합니다. VOD팀은 녹화된 영상 파일에서 영상을 재생(도용)하고 있는 사용자의 uid를 추출합니다.

## 요금 관련

디지털 워터마크 기능을 사용하면 다음과 같은 비용이 발생합니다.

* 트랜스 코딩 요금: 비디오에 디지털 워터마크를 추가할 때 트랜스 코딩 또는 어댑티브 비트레이트 스트리밍을 수행해야 하므로 트랜스 코딩 비용이 발생합니다.
* 스토리지 요금: 트랜스 코딩 또는 어댑티브 비트 레이트 스트리밍의 출력 비디오는 스토리지 공간을 사용하므로 스토리지 요금이 발생합니다.
* 추출 요금: 불법 복제 발견 후 해적의 사용자 ID를 추출하기 위해 VOD에 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 시 추출 요금이 발생합니다.

상기 과금 항목의 구체적인 단가는 [사용량 과금(후불 일 결산)](https://intl.cloud.tencent.com/document/product/266/14666)을 참고하십시오.
