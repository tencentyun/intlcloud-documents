라이브 방송 타임 시프트는 CSS 녹화 능력을 기반으로 하며, TS(Transport Stream)의 멀티파트 주소와 TS 파일을 VOD 시스템에 단독으로 저장합니다. 클라이언트는 타임 시프트 재생 도메인을 통해 시간 매개변수를 전송하여 현재 시간 이전의 하이라이트 비디오 콘텐츠를 재생할 수 있습니다.

## 타임 시프트의 원리

자주 볼 수 있는 HLS 비디오 라이브 방송에서 푸시 스트림 비디오 콘텐츠가 여러 개의 TS 멀티파트로 전환됩니다. 사용자는 시청 시 m3u8 파일 요청을 통해 TS 멀티파트 주소를 연결할 수 있으며, TS 파일을 획득하여 라이브 방송 스트리밍 콘텐츠를 시청할 수 있습니다. 해당 상황에서 TS 파일 콘텐츠는 지속적으로 저장되지 않아 사용자는 현재 시간 이전의 라이브 방송 비디오 콘텐츠를 되감기할 수 없습니다.

## 주의 사항

타임 시프트 기능을 활성화하면 VOD 트래픽 및 VOD 스토리지 비용이 발생합니다.
## 타임 시프트 사용

### 전제 조건

- [Tencent Cloud 계정에 가입](https://intl.cloud.tencent.com/document/product/378/17985)이 완료된 상태여야 합니다. 
- Tencent CSS 서비스를 활성화하고 [푸시 스트림 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가된 상태여야 합니다. 

<span id="step1"></span>
### 1단계: VOD 서비스 활성화

1. [VOD 콘솔](https://console.cloud.tencent.com/vod/overview)로 이동하여 [즉시 활성화]를 클릭합니다.
2. 서비스 활성화 프로토콜을 선택하고 [확인]을 클릭하면 VOD 서비스가 활성화되며, VOD 콘솔에 액세스할 수 있습니다.
<span id="step2"></span>
### 2단계: 타임 시프트 재생 도메인 추가

타임 시프트 재생에 사용할 VOD 도메인을 추가합니다. 방법은 다음과 같습니다.

1. [VOD 콘솔]>[재생 배포 관리]>[도메인 관리]로 이동합니다.
2. [도메인 추가]를 클릭하고 ICP비안을 받은 VOD 도메인을 입력합니다. 자세한 방법은 [재생 배포 설정](https://intl.cloud.tencent.com/document/product/266/35572)을 참조하십시오.
3. 추가 도메인의 CNAME 설정 작업을 완료합니다.
<span id="step3"></span>
### 3단계: 녹화 템플릿 연결

1. [CSS 콘솔]>[기능 템플릿]<[녹화 설정](https://console.cloud.tencent.com/live/config/record)으로 이동합니다.
2. [+]를 클릭하여 녹화 템플릿을 생성합니다. 자세한 방법은 [녹화 템플릿 설정](https://intl.cloud.tencent.com/document/product/267/34223)을 참조하십시오.
   > ! 
   > - 녹화 파일 유형을 **HLS** 포맷으로 선택하고 HLS 녹화를 활성화합니다.
   > - 파일 저장 기간을 설정할 수 있으며, 해당 기간은 [타임 시프트 시간](#step4)보다 짧을 수 없습니다.
3. 녹화 템플릿을 설정할 푸시 스트림 도메인에 연결합니다. 자세한 방법은 [녹화 설정](https://intl.cloud.tencent.com/document/product/267/34224)을 참조하십시오.

<span id="step4"></span>
### 4단계: 타임 시프트 서비스 활성화

[티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=39&source=0&data_title=%E4%BA%91%E7%9B%B4%E6%92%AD%20%20css&step=1)에서 문의 제품을 "CSS"로 선택하고 다음 매개변수와 함께 타임 시프트 활성화 신청을 제출합니다.

- [2단계](#step2)에서 추가한 VOD **타임 시프트 재생 도메인**
- [3단계](#step3)에서 설정한 녹화 템플릿 ID
- 사용자 정의 타임 시프트 시간 `timeshift_dur`, 단위: 초
  > ? 
  > - 타임 시프트 시간: 타임 시프트로 볼 수 있는 콘텐츠의 시간 길이(현재 최대 7일 이내의 콘텐츠 보기 설정 가능)
  > - 해당 항목은 정확성을 보장하지 않으며, 필요에 따른 설정값에 약간의 시간을 더 추가하여 설정하시기 바랍니다.
  > - 7200(2시간)으로 설정하는 경우: 2시간 전부터 지금까지의 타임 시프트 콘텐츠를 표시할 수 있습니다(즉, delay의 상대적인 타임 시프트 길이가 90초 -2시간). 타임 시프트가 2시간 이전을 초과하는 콘텐츠는 라이브 방송 콘텐츠가 존재해도 `HTTP 404`를 리턴합니다. 



## 재생 요청

### 요청 URL 포맷

```
http://[Domain]/timeshift/[AppName]/[StreamName]/timeshift.m3u8?delay=xxx
```

### 매개변수 설명

| 매개변수           | 설명                                                         |
| -------------- | ------------------------------------------------------------ |
| [Domain]       | 사용자가 등록한 타임 시프트 서비스 연결 도메인, 즉 VOD 콘솔에 추가한 [타임 시프트 재생 도메인](#step2)입니다.     |
| timeshift      | 고정 필드로 수정할 필요 없습니다.                                           |
| [AppName]      | 애플리케이션 이름으로, 애플리케이션 이름이 `live`인 경우 `live`를 입력합니다.           |
| [StreamName]   | 스트림 이름으로, 요청에 대응하는 스트림 이름을 입력합니다.                                 |
| timeshift.m3u8 | 고정 필드로, 수정할 필요 없습니다.                                           |
| delay          | 상대적인 타임 시프트 시간을 표시하며 단위는 초입니다. 현재 해당 값이 90 이하인 경우 백그라운드에서 90으로 조정합니다.  |

### 예시

현재 타임 시프트 도메인을 `testtimeshift.com`, 타임 시프트 애플리케이션 이름을 `live`, 스트림 이름을 `SLPUrIFzGPE`으로 설정한 상태에서 타임 시프트의 해당 주소의 5분 전 라이브 방송 콘텐츠가 필요한 경우 요청 URL은 다음과 같습니다.

```
http://testtimeshift.com/timeshift/live/SLPUrIFzGPE/timeshift.m3u8?delay=300
```
