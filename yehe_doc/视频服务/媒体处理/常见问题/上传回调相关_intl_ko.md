[](id:q1)
### 콜백을 받는 방법은 무엇입니까?
MPS 서비스는 메시지 큐, SCF 및 HTTP 푸시를 기반으로 하는 콜백 알림 방식을 지원합니다.

[](id:q2)
### 콜백을 받지 못한 경우 어떻게 해야 합니까?
파일을 성공적으로 업로드한 후 일정 시간 내에 파일의 트랜스코딩 결과 콜백 메시지를 받지 못하면, 가능한 이유는 다음과 같습니다.
- 워크플로 정보가 올바르게 설정되지 않았습니다. 워크플로가 올바르게 설정되었는지 확인하십시오.
- API를 통해 시작된 트랜스코딩 작업이며, 성공적으로 반환된 경우, [Querying Task](https://intl.cloud.tencent.com/document/product/1041/33497)를 통해 작업 처리 진행 상황을 확인할 수 있습니다.
- 작업 큐가 과부하되어 처리 시간이 오래 걸리거나, 기타 서비스 이상이 발생할 수 있습니다. [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 큐 상태를 확인할 수 있습니다.

[](id:q3)
### 콜백 설정은 어떻게 합니까?
- **메시지 큐:**
MPS 서비스는 Tencent Cloud CMQ를 사용하여 트랜스코딩 결과의 콜백 메시지를 전송합니다. 트랜스코딩 콜백 알림을 수신하기 위한 메시지 큐를 생성하려면 CMQ 서비스를 미리 활성화해야 합니다. 동시에 메시지 큐의 쓰기 권한이 MPS 서비스에 승인되어야 메시지 큐에 데이터를 쓸 수 있습니다. 그런 다음 [MPS 콘솔](https://console.cloud.tencent.com/mps)에서 워크플로를 생성할 때 해당 메시지 큐 매개변수를 설정할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5584b4ca5a552a92ce66c974fab16aa8.png)
- **SCF:**
MPS 서비스는 사용자가 사용할 수 있도록 SCF에 템플릿을 구성합니다. SCF 서비스를 미리 활성화하고, SCF 함수 생성 및 트리거를 구성해야 합니다. 자세한 내용은 [비디오 작업 콜백 알림](https://intl.cloud.tencent.com/document/product/1041/40337) 모범 사례를 참고하십시오.
- **HTTP 푸시:**
MPS 서비스는 지정된 URL에 대한 HTTP 푸시 콜백을 지원합니다. 인터페이스 호출 시 [작업 이벤트 알림 설정-TaskNotifyConfig](https://intl.cloud.tencent.com/document/product/1041/33690)의 NotifyType 매개변수를 URL로 지정하고 NotifyUrl 매개변수에 HTTP 콜백 주소를 입력합니다.

[](id:q4)
### 콜백 사용은 유료입니까?
- CMQ 관련 사용 및 요금 정보는 [CMQ 요금 안내](https://intl.cloud.tencent.com/document/product/406/38676)를 참고하십시오.
- SCF 관련 사용 및 요금 정보는 [SCF 요금 안내](https://intl.cloud.tencent.com/document/product/583/17299)를 참고하십시오.
- 현재 HTTP 푸시는 무료입니다.

[](id:q5)
### 비디오 파일은 어떻게 업로드합니까?
MPS 서비스는 다음 비디오 업로드 방법을 지원합니다.

- **콘솔 업로드**: [COS 콘솔](https://console.cloud.tencent.com/cos5) 로그인 후 로컬 비디오를 COS Bucket에 [업로드](https://intl.cloud.tencent.com/document/product/436/13321)합니다. 비디오 소량 업로드에 적합합니다.
 **클라이언트 업로드**: COS SDK를 통해 로컬 비디오를 COS Bucket에 업로드하고, 작은 파일 간편 업로드와 큰 파일의 멀티파트 업로드를 지원합니다. 업로드 과정에서 UGC, PGC와 같은 시나리오에 적합한 검사점 재시작, 일시 중지 및 재개, 취소와 같은 작업을 지원합니다. 업로드 방법은 다음과 같습니다.
  - [간편 업로드](https://intl.cloud.tencent.com/document/product/436/14113)
  - [멀티파트 업로드](https://intl.cloud.tencent.com/document/product/436/14112)

[](id:q6)
### 업로드된 비디오의 자동 트랜스코딩을 구성하는 방법은 무엇입니까?
태스크 플로우 생성 및 해당 트랜스코딩 템플릿을 선택하고, 워크플로를 활성화합니다. 콘솔 설정 매개변수 설명의 자세한 내용은 [워크플로 설정](https://intl.cloud.tencent.com/document/product/1041/33492)을 참고하십시오.

[](id:q7)
### ps 형식으로 파일을 업로드할 수 있습니까? 
안됩니다. 업로드할 수 있는 파일 형식은 아래 표를 참고하십시오.

| 파일 형식 | 비디오 인코딩 유형            | 오디오 인코딩 유형        |
| -------- | ----------------------- | ------------------- |
| MP4      | H.264, H.265            | AAC                 |
| FLV      | H.264, H.265            | AAC                 |
| MOV      | H.264, H.265, MPEG4     | AAC                 |
| WMV      | WMV1, WMV2              | WMA1, WMA2          |
| MKV      | H264, VP8, MPEG4        | AAC                 |
| AVI      | H264, WMV1, WMV2, MPEG4 | AAC, WMA1, WMA2     |
| RMVB     | RV 시리즈                 | RAAC, RACP          |
| TS       | H.264, MP1V, MP4V       | MP1, MP2, MP3, MP4A |
| MPG      | MPEG1, MPEG2            | MP2                 |
| 3GP      | H263, MPEG4             | AMR, AAC            |

[](id:q8)
### 비디오 트랜스코딩이 지정된 비트레이트로 출력되지 않습니다.
기본적으로 MPS는 시각적 경험에 영향을 주지 않는 전제 하에, 불필요한 프레임의 품질을 낮추고 특정 출력 비트레이트를 따르지 않아, 비트레이트를 줄이는 효과가 있습니다.
지정된 비트레이트에 따라 출력해야 하는 경우, 해당 트랜스코딩 템플릿 id를 제공하여 설정을 변경할 수 있습니다.

[](id:q9)
### COS에 저장된 비디오를 미리보기할 때, 미리보기를 압축할 수 있습니까?
현재 COS는 비디오 미리보기 자동 압축 기능을 지원하지 않습니다. Cloud Infinite에는 비디오 트랜스코딩 기능이 있으므로, 파일을 다시 생성하여 원본 비트 스트림의 인코딩 포맷, 해상도 및 비트레이트와 같은 매개변수를 변경할 수 있습니다.

