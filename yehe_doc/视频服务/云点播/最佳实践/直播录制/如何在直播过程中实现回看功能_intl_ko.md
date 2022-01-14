라이브 스트리밍의 타임 시프트 재생은 라이브 녹화, 라이브 스트리밍 타임 시프팅 및 VOD 가속 배포를 기반으로 합니다. 라이브 스트리밍이 시작된 후 시청자는 현재 시간이 아닌 이전 시점을 선택하여 시청을 시작할 수 있습니다. 이는 일반적으로 스포츠 이벤트에서 하이라이트를 재생하는 데 사용됩니다. 사용자는 라이브 스트리밍이 끝날 때까지 기다리지 않고 현재 시간보다 이전에 생성된 콘텐츠를 볼 수 있도록 진행률 표시줄을 변경할 수 있습니다. 동시에 라이브 스트리밍은 동일하게 유지되며 사용자는 라이브 스트리밍으로 다시 전환할 수 있습니다.

## 기능 특징
- 사용자는 재생에 허용되는 타임 시프트 지속 시간(재생 시작 시간과 현재 시간의 차이)을 지정할 수 있습니다.
- 사용자는 라이브 스트림이 다중 비트레이트로 녹화될 때 타임 시프팅을 위해 특정 비트레이트로 동영상 스트림을 지정할 수 있습니다.

## 전제 조건
- Tencent Cloud 계정에 [가입](https://intl.cloud.tencent.com/register) 및 [로그인](https://intl.cloud.tencent.com/login)하고, 실명 인증을 완료해야 합니다. 실명 인증되지 않은 사용자는 중국 본토의 라이브 스트리밍 타임 시프팅 인스턴스를 구매할 수 없습니다.
- Tencent Cloud CSS 서비스를 활성화하고 [푸시 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가된 상태여야 합니다.

## 주의사항:
- 타임 시프트 재생을 사용하려면 먼저 [타임 시프트 리뷰](#time)기능을 활성화해야 합니다.
- 가장 작은 타임 시프트 지속 시간은 90초로, 라이브 스트리밍 콘텐츠에 비해 재생 콘텐츠에서 90초 이상의 대기 시간이 있음을 의미합니다.
- 현재 타임 시프트 기능 내부 테스트는 별도로 청구되지 않으나, 타임 시프팅을 활성화하면 VOD 트래픽과 스토리지 비용이 발생합니다. 자세한 내용은 [라이브 방송 녹화 요금](https://intl.cloud.tencent.com/document/product/267/39605), [VOD 스토리지 요금 및 비디오 재생 요금](https://intl.cloud.tencent.com/document/product/266/2838)을 참고하십시오.

## 실행 순서
### 1단계: VOD 서비스 활성화[](id:step1)
1. [VOD 콘솔](https://console.cloud.tencent.com/vod/overview)로 이동하여 [즉시 활성화]를 클릭합니다.
2. 서비스 활성화 프로토콜을 선택하고 [확인]을 클릭하면 VOD 서비스가 활성화되며, VOD 콘솔에 액세스할 수 있습니다.


### 2단계: 타임 시프트 재생의 도메인 이름 추가[](id:step2)
타임 시프트 재생에 사용할 VOD 도메인을 추가합니다. 방법은 다음과 같습니다.
1. [VOD 콘솔](https://console.cloud.tencent.com/vod/overview)에 로그인하고 왼쪽 사이드바에서 [배포 및 재생 관리]>[도메인 관리]를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f3a42999b551357b871b8b3381953ba1.png)
2. [도메인 추가]를 클릭하고 ICP 비안을 받은 VOD 도메인을 입력합니다. 자세한 방법은 [재생 배포 설정](https://intl.cloud.tencent.com/document/product/266/35572)을 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/167658ece2ff8138b1e3efdc53c5ebbc.png)

3. 추가 도메인의 CNAME 설정 작업을 완료합니다.

### 3단계: 녹음 템플릿 바인딩[](id:step3)
1. [CSS 콘솔](https://console.cloud.tencent.com/live/config/record)에 로그인하고 [기능 구성]>[[라이브 녹화](https://console.cloud.tencent.com/live/config/record)]를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/712036b264c79e34f02655fa83488e0a.png)

2. [녹화 템플릿 생성]을 클릭하여 녹화 템플릿을 만듭니다. 자세한 내용은 [녹화 템플릿 설정](https://intl.cloud.tencent.com/document/product/267/34223)을 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/f3a89ef4c5b4ffded769dfcca0bb654b.png)
>!
>- 녹화 파일 유형을 HLS 포맷으로 선택하고 HLS 녹화를 활성화합니다.
>- [타임 시프트 시간](https://intl.cloud.tencent.com/document/product/267/31565) 보다 긴 파일 스토리지 시간을 설정합니다.
2. 녹화 템플릿을 설정할 푸시 스트림 도메인에 연결합니다. 자세한 방법은 [녹화 설정](https://intl.cloud.tencent.com/document/product/267/34224)을 참고하십시오.

### 4단계: 타임 시프트 기능 활성화[](id:time)
[티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=39&source=0&data_title=%E4%BA%91%E7%9B%B4%E6%92%AD%20%20CSS&step=1)에서 문의 제품을 ‘CSS’로 선택한 다음 타임 시프트 활성화를 요청하고 다음 매개변수를 제공합니다.
- [2단계](#step2)에서 추가한 VOD 타임 시프트 재생 도메인
- [3단계](#step3)에서 설정한 녹화 템플릿 ID
- 사용자 정의 타임 시프트 시간 timeshift_dur. 단위: 초
- 
>?
>- 타임 시프트 시간: 타임 시프트로 볼 수 있는 콘텐츠의 시간 길이(현재 최대 7일 이내의 콘텐츠 보기 설정 가능).
>- 해당 항목은 정확성이 보장되지 않으므로, 필요에 따른 설정값에 약간의 시간을 더 추가하여 설정하시기 바랍니다.
>- 7200(2시간)으로 설정하는 경우: 2시간 전부터 지금까지의 타임 시프트 콘텐츠를 표시할 수 있습니다(즉, delay의 상대적인 타임 시프트 길이가 90초 -2시간). 타임 시프트가 2시간 이전을 초과하는 콘텐츠는 라이브 방송 콘텐츠가 존재해도 HTTP 404가 반환됩니다.

## 재생 요청
### 요청 URL 포맷
```
http://[Domain]/timeshift/[AppName]/[StreamName]/timeshift.m3u8?delay=xxx
```

### 매개변수 설명
| 매개변수 | 설명 |
|---------|---------|
| [Domain] | 사용자가 등록한 타임 시프트 서비스 연결 도메인, 즉 VOD 콘솔에 추가한 타임 시프트 재생 도메인입니다. |
| timeshift | 수정이 필요 없는 고정 필드|
| [AppName] | 애플리케이션 이름. 애플리케이션 이름이 live라고 가정할 때, live를 입력합니다.|
| [StreamName] | 스트림 이름. 요청의 스트림 이름을 입력합니다.|
| timeshift.m3u8 | 수정이 필요 없는 고정 필드|
| delay | 90 이상인 타임 시프트 지속 시간(초)입니다. 값이 90보다 작으면 기본적으로 90으로 조정됩니다.|

### 예시
현재 타임 시프트 도메인을 `testtimeshift.com`, 타임 시프트 애플리케이션 이름을 `live`, 스트림 이름을 `SLPUrIFzGPE`라고 가정합니다. 5분 전에 생성된 라이브 콘텐츠를 재생하려면 요청 URL은 다음과 같습니다.

`http://testtimeshift.com/timeshift/live/SLPUrIFzGPE/timeshift.m3u8?delay=300`
