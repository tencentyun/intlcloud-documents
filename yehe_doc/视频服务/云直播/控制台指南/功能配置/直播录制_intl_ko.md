라이브 방송 녹화는 라이브 방송 원본 스트림이 트랜스 멀티미디어 캡슐화(오디오, 비디오 데이터 및 해당 타임스탬프 등의 정보를 수정하지 않음)를 거쳐 얻은 파일을 VOD 플랫폼에 저장하는 서비스입니다.

##  주의 사항
- [녹화 작업 생성](https://intl.cloud.tencent.com/document/product/267/37309)과 [녹화 템플릿 생성 설정](https://intl.cloud.tencent.com/document/product/267/34223)의 두 가지 녹화 요청 방식으로, 실제 사용 시 필요에 따라 한 가지만 선택하면 됩니다. 동일한 라이브 방송 스트리밍에서 녹화 템플릿을 설정하는 것과 동시에 녹화 작업을 생성한 경우, 중복 녹화될 수 있습니다.
- 푸시 스트리밍이 시작되면 녹화 작업이 지연되기 때문에 푸시 스트리밍 시간이 너무 짧은 경우에는 녹화 파일이 생성되지 않습니다. 녹화 파일의 품질을 보장하기 위해 매 녹화 시 푸시 스트리밍 시간을 10초 이상으로 설정할 것을 권장합니다.

## 녹화 저장
라이브 방송 녹화 시 파일은 VOD 플랫폼에 저장됩니다. 라이브 방송 녹화 서비스를 사용하려면 먼저 [VOD 서비스](https://intl.cloud.tencent.com/product/vod)를 신청 및 활성화해야 합니다.
>? 생성된 녹화 파일의 이름 규칙은 [녹화 템플릿 매개변수-VodFileName](https://intl.cloud.tencent.com/document/product/267/30767)을 참고하십시오.

## 녹화 형식

녹화 파일 포맷은 FLV/HLS/MP4/AAC를 지원하며, 이 중 AAC는 퓨어 오디오 녹음 파일 포맷입니다.

## 녹화 사용 시나리오

<table>
<thead>
<tr>
<th width="20%">사용 시나리오</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<th>푸시 도메인, 스트림 이름에 따라 단계별 녹화</th>
<td>푸시 도메인, 스트림 이름 단계에서 녹화 여부를 설정할 수 있습니다.</td>
</tr>
<tr>
<th>지정된 시간대에 녹화</th>
<td>API 호출을 통해 녹화 시작 및 종료 시간을 제어할 수 있어 지정된 시간에 녹화를 진행할 수 있습니다.</td>
</tr>
<tr>
<th>하이라이트 영상 녹화</th>
<td>푸시 스트리밍 도중 하이라이트 영상이 재생되면 API 호출을 통해 실시간으로 녹화를 생성할 수 있습니다.</td>
</tr>
<tr>
<th>퓨어 오디오 녹음</th>
<td>푸시 스트리밍이 퓨어 오디오일 경우, AAC를 퓨어 오디오 녹음으로 설정할 수 있습니다.</td>
</tr>
</tbody></table>

## 지정된 푸시 도메인의 모든 라이브 방송 스트리밍을 녹화합니다.

당사는 녹화 매개변수를 템플릿 형식으로 관리하므로 다양한 비즈니스 시나리오에 따라 녹화 설정 템플릿을 생성할 수 있습니다. 템플릿 설정을 통해 다양한 푸시 도메인, 스트림 이름을 연결하여 녹화 설정을 빠르고 간편하게 관리할 수 있습니다.
VOD 서비스를 개통하고 난 이후에 특정 푸시 도메인에서 라이브 방송 스트리밍을 녹화하고자 할 경우, 두 가지 방법으로 이를 실현할 수 있습니다.

### 라이브 방송 콘솔
1. **기능 설정**>[**라이브 방송 녹화**](https://console.cloud.tencent.com/live/config/record) 페이지로 이동해 녹화 설정 템플릿을 추가합니다.
2. [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage)에서 도메인 이름을 추가한 후, **관리**를 클릭하여 해당 도메인을 녹화 템플릿과 연결합니다. 자세한 작업 방식은 [녹화 설정](https://intl.cloud.tencent.com/document/product/267/34224)을 참고하십시오.

### API 호출

1. [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845)을 호출하여 최소 하나 이상의 녹화 형식(예: FlvParam)을 설정합니다.
2. [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846)을 호출하여 매개변수 푸시 도메인 DomainName과 TemplateId를 설정합니다(1단계로 돌아가기). AppName 및 StreamName에 빈 문자열을 입력하면, 해당 도메인 이름의 모든 푸시 스트리밍을 녹화합니다.

이와 유사하게, 녹화 템플릿을 다양한 스트림 이름과 연결하여 특정 라이브 방송 스트리밍에 녹화 효과를 적용할 수 있습니다.

또한, 동일한 녹화 템플릿을 다른 푸시 도메인, AppName, StreamName과 연결할 수 있지만 동일한 푸시 도메인, AppName, StreamName을 여러 템플릿과 연결할 수 없습니다. 한 라이브 스트림이 동시에 여러 녹화 템플릿과 매칭되는 경우, 다음 순서에 따라 가장 높은 우선 순위를 가진 녹화 템플릿과 최종 매칭됩니다(복잡한 시나리오에서만 해당되며 대부분의 사용자는 무시해도 됩니다).

| 우선순위 | DomainName | AppName  | StreamName |
| ---- | ---------- | -------- | ---------- |
| 1    | &#10003;   | &#10003; | &#10003;   |
| 2    | &#10003;   | ×        | &#10003;   |
| 3    | &#10003;   | &#10003; | ×          |
| 4    | &#10003;   | ×        | ×          |

&#10003;은 녹화 템플릿의 해당 매개변수에 값이 있음을 의미하며, × 는 해당 매개변수 값이 비어 있음을 의미합니다.


## 동일한 푸시 도메인의 하위 스트리밍은 녹화가 시작되지 않습니다.
특정 푸시 도메인에 이미 녹화가 설정되어 있더라도, 해당 도메인에 개별 스트리밍이 존재하므로 비즈니스상 이유로 인해 녹화할 필요가 없습니다. 다음과 같이 작업을 진행하실 수 있습니다.

1. [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845)을 호출한 후 어떤 녹화 형식도 지정하지 않습니다.
```
   https://live.tencentcloudapi.com/?Action=CreateLiveRecordTemplate
   &TemplateName=norecord
   &Description=test
   &<공통 요청 매개변수>
```
2. [CSS 콘솔](https://intl.cloud.tencent.com/document/product/267/34223#conect) 또는 클라우드 API [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846)을 통해 DomainName과 StreamName 매개변수를 설정하여 앞서 언급한 녹화 템플릿과 지정된 푸시 도메인, 스트림 이름을 연결합니다.

> ! 앞서 언급한 방안은 푸시 스트리밍을 개별적으로 녹화할 필요가 없는 상황에 한합니다. 작업을 해야 하는 라이브 방송 스트리밍이 많을 경우, 또 다른 푸시 도메인을 사용하여 독립적으로 관리할 것을 권장합니다. 주요 사항은 다음과 같습니다.
> - 녹화 템플릿과 녹화 규칙 모두 최대 개수의 제한이 존재합니다(50개).
> - 푸시 도메인 차원 관리가 더욱 원활해지며, 업무 변화가 발생하더라도 녹화 템플릿과 규칙을 변경할 필요가 없습니다.

## 지정된 시간에 녹화

일부 스트리밍의 경우, 지정된 시간에 녹화를 시작하고 지정된 시간에 녹화를 종료한다면 API 방식을 통한 녹화 지정이 가능합니다. 녹화 템플릿을 매칭하는 방법과 달리, API를 통해 정확한 녹화 매개변수를 지정해야 합니다. 이 방식은 일반적으로 어떤 녹화 방식도 열리지 않은 상황에서 사용됩니다.

### API 호출
녹화 작업 API 생성에 대한 설명입니다. 세부 사항은 [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)를 참고하십시오.


### 녹화 예시
- 가장 간단한 상황입니다. 지정된 StreamName, DomainName, AppName, EndTime 매개변수만 입력하면 됩니다.
예: 2020년 08월 10일 오전 8시부터 10시까지 진행되는 녹화 작업, 형식은 FLV, 비디오 녹화, 분할 간격 30분, 영구 저장.
**입력 예시:**
```
https://live.tencentcloudapi.com/?Action=CreateRecordTask
&AppName=live
&DomainName=mytest.live.push.com
&StreamName=livetest
&StartTime=1597017600
&EndTime=1597024800
&TemplateId=0
&<공통 요청 매개변수>
```
- 녹화 포맷, 녹화 유형 및 저장 매개변수 등을 구체적으로 지정할 수 있습니다.
예: 2020년 08월 10일 오전 8시부터 10시까지 진행되는 녹화 작업, 형식은 MP4, 분할 간격 1시간, 영구 저장.
	1. [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845)을 호출하여 먼저 녹화 템플릿을 생성합니다.
**입력 예시:**
```
https://live.tencentcloudapi.com/?Action=CreateLiveRecordTemplate
&TemplateName=templat
&Description=test
&Mp4Param.Enable=1
&Mp4Param.RecordInterval=3600
&Mp4Param.StorageTime=0
&<공통 요청 매개변수>
```
**출력 예시:**
```
{
  "Response": {
    "RequestId": "839d12da-95a9-43b2-a9a0-03366d01b532",
    "TemplateId": 17016
  }
}
```
	2. [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)를 호출하여 녹화 작업을 생성합니다.
**입력 예시:**
```
https://live.tencentcloudapi.com/?Action=CreateRecordTask
&StreamName=livetest
&AppName=live
&DomainName=mytest.live.push.com
&StartTime=1597017600
&EndTime=1597024800
&TemplateId=17016
&<공통 요청 매개변수>
```


> ?
>- 동일한 라이브 방송 스트리밍의 경우, 예약된 작업과 다른 예약된 작업, 그리고 예약된 작업과 다른 형식의 녹화 작업은 충돌하지 않습니다. 즉, 각 작업의 시간 범위가 겹칠 수 있습니다. 또한 활성화된 녹화 설정을 사용하여 API 호출을 통해 녹화 작업을 생성할 수도 있습니다.
>- 녹화 작업을 사전에 생성(예: 1시간 일찍 또는 새벽에 당일 작업 생성)하고, 지정된 작업의 시간의 시작 시간을 이벤트 시간보다 빠르게 설정할 것을 권장합니다.


## 하이라이트 영상 녹화

푸시 스트리밍 도중 하이라이트 영상을 발견하는 경우, 사용자는 즉시 녹화를 시작하고 이후 사용을 위해 하이라이트 영상을 편집하려 할 것입니다. API 호출 및 하이라이트 영상 녹화 지정을 통해 이를 실현할 수 있습니다.

```
https://live.tencentcloudapi.com/?Action=CreateRecordTask
&StreamName=test
&AppName=live
&DomainName=mytest.live.push.com
&EndTime=1597024800
&<공통 요청 매개변수>
```

하이라이트 영상 녹화에 관한 몇 가지 중요한 사항이 있습니다.
- 녹화 생성 시 푸시 스트리밍이 진행 중이어야 합니다.
- API [StopRecordTask](https://intl.cloud.tencent.com/document/product/267/37307)를 호출하여 작업을 조기 종료할 수 있습니다.
- 해외 푸시 스트리밍을 지원합니다.

## 혼합 스트리밍 녹화

먼저 [클라우드 혼합 스트리밍](https://intl.cloud.tencent.com/document/product/267/37665)을 확인하시고, 혼합 스트리밍 비즈니스에 대해 이해하십시오.

라이브 방송 클라우드 혼합 스트리밍 비즈니스를 사용하는 시나리오와 녹화의 경우, 혼합 스트림 매개변수 OutputStreamType(출력 스트림 유형)에 따라 혼합 스트리밍이 두 종류로 구분됩니다.

- OutputStreamType이 ‘0’일 경우, 출력 스트리밍이 입력 스트리밍 리스트 안에 있음을 나타내므로 신규 스트리밍이 생성되지 않습니다.
- OutputStreamType이 ‘1’일 경우, 출력 스트리밍이 입력 스트리밍 리스트 안에 있지 않음을 나타내므로 신규 스트리밍이 생성됩니다.

푸시 스트리밍 A와 B가 있다고 가정했을 때, 혼합 스트리밍을 통해 나온 출력 스트리밍은 C입니다.

- OutputStreamType이 ‘0’일 경우, C 스트리밍은 A 스트리밍이라고 가정합니다(스트리밍 이름은 동일하나 혼합 스트리밍 이후의 화면). 설정된 녹화를 활성화하면 기본적으로 A 스트리밍(혼합 스트리밍 화면)과 B 스트리밍 녹화 파일이 생성됩니다. 이때 동일한 스트리밍 ID를 사용하므로, A 스트리밍의 기존 푸시 스트리밍은 녹화가 되지 않습니다.
- OutputStreamType이 ‘1’일 경우, 설정된 녹화를 활성화하면 기본적으로 A 스트리밍, B 스트리밍, C 스트리밍(혼합 스트리밍 화면) 녹화 파일이 생성됩니다.

혼합 스트리밍 화면만 녹화하고 싶을 경우에는 API [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)를 호출하면 됩니다. 여기서 중요한 점은 OutputStreamType이 ‘1’인 혼합 스트리밍 유형의 경우에는 앞서 언급한 API를 호출할 때 StreamType 매개변수를 ‘1’로 설정해야 한다는 것입니다.

>! 혼합 스트리밍 녹화는 중국 내륙(대륙)과 국제/중국홍콩, 중국마카오, 중국대만의 라이브 방송 혼합 스트리밍을 지원하지 않으므로, 녹화 파일에 오류가 발생하거나 정상적인 시청 및 리플레이에 영향이 발생할 수 있습니다.


## 자동 접합 녹화(다회차 푸시 스트리밍 연속 녹화)

푸시 스트리밍 클라이언트 네트워크 지터 등의 원인으로 푸시 스트리밍 순간 끊김 현상 및 다수의 녹화 파일 생성이 발생하여 라이브 방송 리플레이 시 불편함이 초래되는 문제를 해결하기 위해, 녹화 서비스는 중도 끊김 현상으로 생성된 여러 개의 푸시 스트리밍 녹화 파일을 하나로 만드는 기능을 제공합니다.

해당 기능의 원리는 HLS 녹화 포맷에 HLS의 **`#EXT-X-DISCONTINUITY`** 태그를 사용하여 푸시 스트림이 여러 번 이루어진 멀티미디어 데이터를 분할하는 것으로, 해당 태그의 역할은 다음과 같습니다. 태그 전후 멀티미디어 데이터의 타임스탬프와 비디오 코딩, 오디오 코딩 샘플링 등의 정보가 다를 수 있으므로 끊김없이 정상적으로 재생하기 위해서는 플레이어가 디코더를 업데이트해야 합니다. 그렇기 때문에 해당 기능을 사용할 경우 플레이어는 **#`EXT-X-DISCONTINUITY`** 태그를 지원해야 합니다. iOS 자체 플레이어(또는 Safari 직접 재생), Android의 ExoPlayer, Web의 hls.js 플레이어는 모두 해당 태그를 지원하나, VLC 등의 플레이어는 해당 태그를 지원하지 않습니다.

해당 기능을 사용할 경우, 푸시 스트리밍 중단 시 자동 연결 시간(최대 30분까지 설정, 즉 30분까지 중단된 푸시 스트리밍을 하나의 파일로 연결)을 설정해야 합니다. 마지막 정상 푸시 스트리밍이 종료되고 나면 설정된 시간 내의 콘텐츠를 자동으로 연결하여 HLS 녹화 파일을 생성하게 됩니다.

현재 자동 연결 녹화 기능은 HLS 포맷을 지원합니다. [라이브 방송 녹화](https://intl.cloud.tencent.com/document/product/267/34223)에서 녹화 재개 타임아웃 시간을 설정할 수 있습니다.

> !
>- 자동 연결은 오디오 데이터가 없는 라이브 방송 스트리밍을 지원하지 않습니다.
>- 비디오 접합 기능을 사용하려면 VOD 내의 비디오 합성 인터페이스를 호출해야 합니다. 관련 문서 설명은 [비디오 합성](https://intl.cloud.tencent.com/document/product/266/34127)을 참고하십시오.
>- HLS 연속 녹화 기능을 설정하면 중간에 스트림이 끊겨도 콜백하지 않으며, 기본적으로 연속 녹화 후 최종 생성된 파일만 콜백합니다.

## 녹화 파일 획득

생성된 녹화 파일은 자동으로 VOD 시스템에 저장됩니다. 다음과 같은 방식으로 녹화 파일을 획득할 수 있습니다.

### VOD 콘솔

[VOD 콘솔](https://console.cloud.tencent.com/vod/media)에 로그인한 후, **비관리자** 화면에서 **미디어 자산 관리** > **오디오/비디오 관리**를 클릭하면 녹화 기능으로 생성된 모든 파일을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/66bde9882dab60099bed8013a3d8c521.png)

### 녹화 이벤트 알림

콘솔 또는 API 호출을 통해 녹화 콜백 주소를 설정할 수 있습니다. 녹화 파일이 생성되면 메시지 형식으로 해당 콜백 주소에 알림이 전달됩니다. 메시지를 수신하고 나면 녹화 [콜백 이벤트 메시지 알림](https://intl.cloud.tencent.com/document/product/267/38080)에 따라 업무 처리가 진행됩니다.

이벤트 알림 매커니즘은 높은 효율성과 신뢰성 및 실시간성을 지니므로 콜백 방식으로 녹화 파일을 획득할 것을 권장합니다.

### VOD API 조회

구체적인 사용 방법은 VOD API [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179)의 인터페이스를 참고하여 녹화 파일을 필터링 하여 조회하십시오.
>! CSS API로 [녹화 작업 생성](https://intl.cloud.tencent.com/document/product/267/37309)을 진행할 경우, 녹화 콜백은 사용자 푸시 스트리밍 URL의 [stream_param](#message) 매개변수로 리턴하지 않으며 다른 녹화 방식은 리턴됩니다.


## 업데이트 설정 주의 사항
녹화 설정 업데이트 완료 후 푸시 스트리밍 재실행 및 설정 검증을 진행할 것을 권장합니다. 설정 적용 규칙은 다음과 같습니다.
- 설정 적용 시간의 기본값은 10분입니다.
- 설정 작용 시간은 라이브 방송 푸시 스트리밍이 시작되는 시각이며, 녹화 중에는 설정이 업데이트되지 않습니다.
- 푸시 스트리밍 지속 시간이 비교적 긴 시나리오(감시 카메라 등)에서는 스트리밍을 중단한 이후에 다시 설정해야 적용됩니다.
