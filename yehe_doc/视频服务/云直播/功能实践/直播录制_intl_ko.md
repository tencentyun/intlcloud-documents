라이브 방송 녹화는 라이브 방송 원본 스트림이 트랜스 멀티미디어 캡슐화(오디오, 비디오 데이터 및 대응하는 타임스탬프 등 정보를 수정하지 않음)를 거쳐 얻은 비디오 파일을 VOD 플랫폼에 저장합니다.

##  주의 사항
- [녹화 작업 생성](https://intl.cloud.tencent.com/document/product/267/37309)과 [녹화 템플릿 생성 설정](https://intl.cloud.tencent.com/document/product/267/34223)은 두 가지 녹화 요청 방식으로, 실제 사용 시 필요에 따라 하나만 선택하면 됩니다. 동일한 라이브 방송 스트리밍에서 녹화 템플릿을 설정한 동시에 녹화 작업을 생성한 경우 중복 녹화될 수 있습니다.
- 푸시 스트림 시작 후 녹화 작업을 실행하면 약간의 딜레이가 발생하여 푸시 스트림 시간이 너무 짧으면 녹화 파일이 생성되지 않을 수 있습니다. 녹화 파일의 품질 보장을 위해 녹화별 푸시 스트림 시간을 10초 이상 유지하시기 바랍니다.

## 녹화 저장
라이브 방송 녹화는 파일을 VOD 플랫폼에 저장합니다. 라이브 방송 녹화 서비스를 이용할 경우 먼저 [VOD 서비스](https://intl.cloud.tencent.com/product/vod) 활성화를 신청해야 합니다.
>? 생성된 녹화 파일 이름 생성 규칙에 대한 자세한 내용은 [녹화 템플릿 매개변수-VodFileName](https://intl.cloud.tencent.com/document/product/267/30767#RecordParam)를 참조하십시오.

## 녹화 포맷

녹화 파일 지원 포맷: FLV/HLS/MP4/AAC. AAC는 순수 오디오 녹화입니다.

## 녹화 사용 시나리오

<table>
<thead>
<tr>
<th width="20%">사용 시나리오</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<th>푸시 스트림 도메인, 스트림 이름 등급별 녹화</th>
<td>푸시 스트림 도메인, 스트림 이름 등급 설정에서 녹화 여부를 설정할 수 있습니다.</td>
</tr>
<tr>
<th>지정 시간대별 녹화</th>
<td>API 호출을 통해 녹화 시작 및 종료 시간을 제어할 수 있으며, 지정한 시간 동안 녹화를 진행할 수 있습니다.</td>
</tr>
<tr>
<th>하이라이트 비디오 녹화</th>
<td>푸시 스트림 중 하이라이트 화면이 방송되는 경우 API를 호출하여 실시간으로 녹화할 수 있습니다.</td>
</tr>
<tr>
<th>순수 오디오 녹화</th>
<td>푸시 스트림이 순수 오디오인 경우 AAC 순수 오디오 녹화를 설정할 수 있습니다.</td>
</tr>
</tbody></table>

## 지정한 푸시 스트림 도메인의 모든 라이브 방송 스트리밍 녹화

녹화 매개변수를 템플릿 형식으로 관리할 수 있으며, 비즈니스 시나리오별로 녹화 설정 템플릿을 생성할 수 있습니다. 또한 템플릿 설정을 통해 다른 푸시 스트림 도메인 및 스트림 이름과 연결하여 녹화 설정을 효율적으로 관리할 수 있습니다.
VOD 서비스 활성화 후 특정 푸시 스트림 도메인의 라이브 방송 스트리밍을 녹화하고 싶은 경우, 두 가지 구현 방법이 있습니다.

### 라이브 방송 콘솔
1. [기능 템플릿]>[녹화 설정](https://console.cloud.tencent.com/live/config/record)으로 이동해 녹화 설정 템플릿을 추가합니다.
2. [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)에서 푸시 스트림 도메인을 추가하고 [관리]를 클릭하여 해당 도메인과 녹화 템플릿을 연결합니다. 자세한 작업 방법은 [녹화 설정](https://intl.cloud.tencent.com/document/product/267/34224)을 참조하십시오.

### API 호출

1. [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845)을 호출하여 하나 이상의 녹화 포맷(예: FlvParam)을 설정합니다.
2. [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846)을 호출하여 매개변수 푸시 스트림 도메인 DomainName과 TemplateId(1단계에서 리턴된 항목)를 설정합니다. AppName 및 StreamName에 공백 문자열을 입력하면 해당 도메인의 모든 푸시 스트림을 포함한다는 의미입니다.

이와 유사하게 녹화 템플릿을 다른 스트림 이름과 연결할 경우 일부 라이브 방송 스트리밍에 대한 녹화 효과가 활성화됩니다.
이외에도 동일한 녹화 템플릿을 다른 푸시 스트림 도메인 및 스트림 이름과 연결할 수 있어 동일한 라이브 방송 스트림이 여러 개의 녹화 템플릿에 동시에 매칭되는 상황이 있을 수 있습니다. 단, 가장 마지막에 매칭되는 템플릿이 우선 순위가 가장 높은 템플릿입니다. 템플릿 매칭 규칙에는 다음과 같은 우선 순위(복잡한 시나리오에만 적용되며, 대다수의 사용자는 생략 가능)가 존재합니다.

| DomainName | StreamName | 우선 순위 |
| ---------- | ---------- | ------ |
| &#10003;   | &#10003;   | 0      |
| 공백         | &#10003;   | 1      |
| &#10003;   | 공백         | 2      |
| 공백         | 공백         | 3      |

다음을 참고하십시오. [공백]: 와일드카드, [&#10003;]: 정확히 매칭, [0]: 우선 순위 가장 높음. 우선 순위가 가장 높은 템플릿에 매칭되면 매칭을 중지하고 해당 우선 순위 템플릿을 리턴합니다.


## 동일한 푸시 스트림 도메인의 일부 스트리밍에 대해 녹화 비활성화
특정 푸시 스트림에 녹화를 설정하고, 해당 도메인에 존재하는 개별 푸시 스트림에 대해 업무상의 이유로 녹화가 필요 없는 경우 다음과 같이 설정할 수 있습니다.

1. [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845)을 호출하여 어떠한 녹화 포맷도 지정하지 않습니다.
```
   https://live.tencentcloudapi.com/?Action=CreateLiveRecordTemplate
   &TemplateName=norecord
   &Description=test
   &<공통 요청 매개변수>
```
2. 콘솔 또는 API [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846)를 통해 DomainName과 StreamName 매개변수를 설정하고, 위 녹화 템플릿을 지정 푸시 스트림 도메인 및 스트림 이름과 연결합니다.

> ! 위 방법은 개별 푸시 스트림에 대해 녹화가 필요 없는 상황에만 적용됩니다. 녹화 기능을 활성화하지 않을 라이브 방송 스트리밍 수가 비교적 많은 경우 별도의 푸시 스트림 도메인을 사용하여 독립적으로 관리하는 것을 권장하며, 다음 주요 사항을 고려해야 합니다.
> - 녹화 템플릿 및 녹화 규칙에는 최대 수량(50개)이 존재합니다.
> - 푸시 스트림 도메인 차원으로 관리하는 것이 더욱 효율적입니다. 즉, 비즈니스가 변경되어도 녹화 템플릿 및 규칙을 수정할 필요가 없습니다.

## 지정 시간대 녹화

일부 푸시 스트림에 대해 시작 시간과 종료 시간을 지정하여 녹화하고 싶은 경우 API 방식을 통해 녹화를 지정할 수 있습니다. 녹화 템플릿 설정 방법과는 상이하며, 구체적인 녹화 매개변수는 API를 통해 지정해야 합니다. 또한 해당 방식은 일반적으로 모든 녹화 방식을 활성화하지 않은 상태에서 사용됩니다.

### API 호출
녹화 작업 생성 API에 대한 자세한 설명은 [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)를 참조하십시오.


### 녹화 예시
- 가장 간단한 시나리오에서는 StreamName, DomainName, AppName, EndTime 매개변수만 입력하면 됩니다.
예시: 2020년 8월 10일 오전 8시부터 10시까지, FLV 포맷, 비디오 녹화, 멀티파트 단위 30분, 영구 저장의 녹화 작업을 생성하는 경우
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
- 자세한 녹화 포맷, 녹화 유형, 저장 매개변수 등도 지정할 수 있습니다.
예시: 2020년 8월 10일 오전 8시부터 10시까지, MP4 포맷, 멀티파트 단위 1시간, 영구 저장의 녹화 작업을 생성하는 경우
	1. [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845)을 호출하여 먼저 템플릿을 생성합니다.
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
>- 동일한 라이브 방송 스트리밍의 예약 작업 간 및 예약 작업과 기타 형식의 녹화 작업 간에는 충돌이 발생하지 않습니다. 즉, 생성한 여러 예약 작업에서 지정한 시간 범위는 중복될 수 있으며, 녹화 설정을 활성화한 상태에서 다시 API를 호출하여 녹화 작업을 생성할 수 있습니다.
> - 또한 사전에 녹화 작업(예: 1시간 전 또는 당일 새벽에 작업 생성)을 생성하고 작업 시작 시간을 이벤트 시간보다 조금 빠르게 지정하는 것을 권장합니다.


## 하이라이트 비디오 녹화

푸시 스트림 중 하이라이트 비디오 화면이 방송될 때 즉시 녹화를 시작하고 하이라이트 비디오를 생성해 편집하여 이후에 계속 사용하고 싶은 경우, API를 호출해 하이라이트 비디오 녹화를 지정하여 실현할 수 있습니다.

```
https://live.tencentcloudapi.com/?Action=CreateRecordTask
&StreamName=test
&AppName=live
&DomainName=mytest.live.push.com
&EndTime=1597024800
&<공통 요청 매개변수>
```

하이라이트 비디오 녹화에 대한 설명은 다음과 같습니다.
- 녹화 생성 시 현재 푸시 스트림 상태여야 합니다.
- 쇼트클립 녹화에 적합하며 녹화 시간은 최대 30분까지 지원합니다.
- API [StopRecordTask](https://intl.cloud.tencent.com/document/product/267/37307)를 호출하여 작업을 사전에 종료할 수 있습니다.
- 해외 푸시 스트림을 지원합니다.

## 혼합 스트림 녹화

먼저 혼합 스트림 작업에 대한 이해가 필요합니다. [클라우드 혼합 스트림](https://intl.cloud.tencent.com/document/product/267/37665)을 참조하십시오.

라이브 방송 클라우드 혼합 스트림을 이용한 비즈니스 시나리오에서의 녹화는 혼합 스트림 매개변수 OutputStreamType(출력 스트림 유형)에 따라 혼합 스트림을 두 종류로 나눌 수 있습니다.

- OutputStreamType이 `0`인 경우, 출력 스트림이 입력 스트림 리스트에 표시됩니다. 즉, 새로운 스트림을 생성하지 않습니다.
- OutputStreamType이 `1`인 경우 출력 스트림이 입력 스트림 리스트에 표시됩니다. 즉, 새로운 스트림이 생성됩니다.

푸시 스트림 A, B가 있고, 혼합 스트림을 거쳐 C 출력 스트림이 발생한다고 가정할 때,

- OutputStreamType이 `0`이고 C 스트림이 A 스트림인 경우(스트림 이름이 동일하지만 혼합 스트림 후의 화면인 경우), 녹화 설정 활성화 후 기본적으로 A 스트림(혼합 스트림 화면)과 B 스트림 녹화 파일이 생성됩니다. 동일한 스트림 ID를 중복 사용할 경우 A 스트림 원본 푸시 스트림에 녹화가 발생하지 않으므로 주의해야 합니다.
- OutputStreamType이 `1`인 경우, 녹화 설정 활성화 후 기본적으로 A 스트림, B 스트림, C 스트림(혼합 스트림 화면) 녹화 파일이 생성됩니다.

혼합 스트림 화면만 녹화하고 싶은 경우 API [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)를 통해 구현할 수 있습니다. OutputStreamType이 `1`인 혼합 스트림 유형은 위 API 호출 시 StreamType 매개변수를 `1`로 설정해야 합니다.

>! 혼합 스트림 녹화는 중국대륙 및 글로벌/홍콩, 마카오, 대만의 라이브 방송 혼합 스트림은 지원하지 않아 녹화 파일에 오류가 발생할 수 있으며 정상적인 재생에 영향을 미칠 수 있습니다.


## 자동 연결 녹화(여러 푸시 스트림의 스트림 계속 녹화)

푸시 스트림 측에 네트워크 지터 등이 발생하여 푸시 스트림이 몇 초간 끊겨 여러 녹화 파일이 생성되는 경우 라이브 방송 재생 및 시청이 불편해집니다. 이에 따라 녹화 서비스에서는 자동 연결 녹화 방식으로 짧은 시간 동안 중단된 여러 푸시 스트림을 하나의 파일로 녹화하는 기능을 제공합니다.

원리는 다음과 같습니다. HLS 녹화 포맷에 HLS의 **#EXT-X-DISCONTINUITY** 태그를 사용하여 여러 푸시 스트림의 멀티미디어 데이터를 분할합니다. 해당 태그로 전, 후 멀티 미디어 데이터의 타임스탬프, 비디오 인코딩, 오디오 인코딩 샘플링 등의 서로 다를 수 있는 정보를 식별하고, 플레이어가 디코더를 업데이트해 매끄럽게 정상적으로 재생합니다. 따라서 해당 기능 사용 시 **#EXT-X-DISCONTINUITY** 태그를 지원하는 플레이어가 필요하며 iOS 자체 플레이어(또는 Safari 직접 재생), Android의 ExoPlayer, Web의 hls.js 플레이어는 해당 태그를 지원하지만, VLC 등의 플레이어는 해당 태그를 지원하지 않습니다.

해당 기능 사용 후 푸시 스트림 중단 시 자동 연결 시간(최대 30분까지 설정 가능, 즉 중단 시간이 최대 30분인 푸시 스트림을 하나의 파일로 연결)을 설정하면 가장 마지막에 정상적으로 푸시 스트림이 종료된 후 자동으로 스트림 중단 시간 내의 콘텐츠를 연결하여 HLS 녹화 파일을 생성합니다.

자동 연결 녹화는 현재 HLS 포맷만 지원하며 [녹화 설정](https://intl.cloud.tencent.com/document/product/267/34223)에서 계속 녹화 만료 시간을 설정할 수 있습니다.

> !
> - 자동 연결은 오디오가 없는 데이터의 라이브 방송 스트리밍은 지원하지 않습니다.
> - 비디오 통합 기능은 VOD의 비디오 합성 인터페이스를 호출하여 구현할 수 있으며, 이에 대한 자세한 내용은 [비디오 합성](https://intl.cloud.tencent.com/document/product/266/34127)을 참조하십시오.

## 녹화 파일 획득

녹화 파일이 생성되면 자동으로 VOD 시스템에 저장되며, 녹화 파일은 다음 방법으로 얻을 수 있습니다.

### VOD 콘솔

[VOD 콘솔](https://console.cloud.tencent.com/vod/media)에 로그인하여 **비관리자** 페이지에서 [멀티미디어 리소스 관리]>[비디오 관리]를 선택하면 녹화 생성된 모든 파일을 확인할 수 있습니다.

![](https://main.qcloudimg.com/raw/66bde9882dab60099bed8013a3d8c521.png)

### 녹화 이벤트 알림

콘솔 또는 API 호출을 통해 녹화 콜백 주소를 설정할 수 있으며, 녹화 파일 생성 후 메시지 방식으로 해당 콜백 주소에 통지합니다. 메시지를 수신한 후 녹화 [콜백 이벤트 정보 알림](https://intl.cloud.tencent.com/document/product/267/38079)에 따라 작업을 처리합니다.

이벤트 알림 메커니즘은 효율 및 신뢰도, 실시간성이 높습니다. 녹화 파일 획득 시 콜백 방식 사용을 권장합니다.

### VOD API 조회

자세한 사용 방법은 VOD API [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179) 인터페이스를 참조하여 녹화 파일을 필터링해 조회하십시오.



## 설정 업데이트 주의 사항
녹화 설정 업데이트 완료 후에는 다시 푸시 스트림을 진행하여 설정을 확인하시기 바랍니다. 설정 적용 규칙은 다음과 같습니다.
- 기본적인 설정 적용 시간은 10분입니다.
- 설정이 적용되는 시간은 라이브 방송 푸시 스트림이 시작되는 시간으로, 녹화 중에는 설정이 업데이트되지 않습니다.
- 푸시 스트림 지속 녹화 시간이 비교적 긴 시나리오(예: 모니터링 카메라)의 경우 스트리밍을 중단하고 설정을 다시 푸시해야만 적용됩니다.
