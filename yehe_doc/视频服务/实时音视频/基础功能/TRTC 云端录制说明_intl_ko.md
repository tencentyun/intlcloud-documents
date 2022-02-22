온라인 교육, 라이브 쇼, 화상 회의, 온라인 의료, 원격 은행 등의 응용 시나리오에서 콘텐츠 심사, 비디오 보관 및 비디오 재생 등의 필요성 때문에 전체 영상 통화 또는 인터랙션 라이브 방송 프로세스를 녹화하고 저장해야 하는 경우가 많습니다. 이는 클라우드 녹화 기능을 통해 구현할 수 있습니다.

## 기능 개요
TRTC의 클라우드 녹화 기능을 통해 REST API 인터페이스를 호출하여 녹화할 멀티미디어 스트림을 구독하는 클라우드 녹화 작업을 실행하고 실시간으로 효율적인 제어를 진행할 수 있습니다. 또한 개발자가 직접 서버 및 녹화 관련 모듈을 배치할 필요가 없으므로 보다 편리합니다.

- 녹화 모드: 단일 스트림 녹화는 방에 있는 각 사용자의 멀티미디어 스트림을 독립된 파일로 녹화할 수 있습니다. 혼합 스트림 녹화는 같은 방의 멀티미디어 스트림을 하나의 파일로 믹싱하여 녹화합니다.

* 구독 스트림: 구독 사용자의 블록리스트/얼로우리스트 방식으로 구독할 사용자 미디어 스트림 지정 지원
* 트랜스 코딩 매개변수: 혼합 스트림 시나리오에서 코덱 매개변수를 설정하여 비디오 녹화 파일의 품질 지정 지원
* 혼합 스트림 매개변수: 혼합 스트림 시나리오에서 다양한 유연하고 가변적인 자동 다중 화면 레이아웃 템플릿 및 사용자 정의 레이아웃 템플릿 지원
* CFS: 지정된 녹화 파일을 클라우드 스토리지/VOD로 저장 지원, 현재 클라우드 스토리지 벤더는 Tencent Cloud의 COS 스토리지 지원, VOD 벤더는 Tencent Cloud VOD 지원
  (향후 다른 클라우드 벤더의 스토리지 및 VOD 서비스를 지원할 예정이며, 이 때 클라우드 서비스 계정이 필요하고, 클라우드 스토리지 서비스는 스토리지 매개변수를 제공해야 함)
* 콜백 공지: 콜백 공지 능력 지원, 콜백 도메인을 설정하여 클라우드 녹화의 이벤트 상태를 귀하의 콜백 서버로 공지

### 단일 스트림 녹화

![단일 스트림 녹화](https://qcloudimg.tencent-cloud.cn/raw/cd843d26b27ed6f4179ebbff401ae6e3.png)

이미지는 단일 스트림 녹화 시나리오를 보여줍니다. 방 1234에서 호스트 1과 호스트 2 모두 멀티미디어를 업스트림 했습니다. 호스트 1과 호스트 2의 멀티미디어 스트림을 구독하고 녹화 모드를 단일 스트림 녹화로 설정한다고 가정합니다. 녹화 백그라운드는 각각 호스트 1 및 호스트 2의 멀티미디어 스트림을 풀링해 다음을 포함한 독립 미디어 파일에 녹화합니다.

1. 호스트 1의 비디오 M3U8 인덱스 파일;
2. 호스트 1의 여러 비디오 TS 슬라이스 파일;
3. 호스트 1의 오디오 M3U8 인덱스 파일;
4. 호스트 1의 여러 오디오 TS 슬라이스 파일;
5. 호스트 2의 비디오 M3U8 인덱스 파일;
6. 호스트 2의 여러 비디오 TS 슬라이스 파일;
7. 호스트 2의 오디오 M3U8 인덱스 파일;
8. 호스트 2의 여러 오디오 TS 슬라이스 파일;

녹화 백그라운드는 이 파일을 지정한 클라우드 스토리지 서버에 업로드합니다. 귀하의 업무 백그라운드는 이러한 녹화 파일을 풀링하고 업무 요구에 따라 이러한 파일을 병합 트랜스 코딩해야 합니다. [멀티미디어 병합 트랜스 코딩 스크립트](https://intl.cloud.tencent.com/zh/document/product/647/45169#.E5.8D.95.E6.B5.81.E6.96.87.E4.BB.B6.E5.90.88.E5.B9.B6.E8.84.9A.E6.9C.AC)를 제공합니다.

### 혼합 스트림 녹화

![혼합 스트림 녹화](https://qcloudimg.tencent-cloud.cn/raw/3a29f4527601abe3ac981759bf44ad07.png)

이미지는 혼합 스트림 녹화 시나리오를 보여줍니다. 방 1234에서 호스트 1과 호스트 2 모두 멀티미디어를 업스트림 했습니다. 호스트 1과 호스트 2의 멀티미디어 스트림을 구독하고 설정한다고 가정합니다. 녹화 모드를 혼합 스트림 녹화로 설정하면 녹화 백그라운드는 각각 호스트 1 및 호스트 2의 멀티미디어 스트림을 풀링하고 설정한 다중 화면 템플릿에 따라 비디오 스트림을 혼합하고 오디오 스트림을 혼합합니다. 마지막으로 미디어 스트림은 다음을 포함하여 하나의 미디어 파일로 혼합됩니다.

1. 혼합 스트림 후 비디오 M3U8 인덱스 파일;
2. 혼합 스트림 후 여러 비디오 TS 슬라이스 파일;

녹화 백그라운드는 이 파일을 지정한 클라우드 스토리지 서버에 업로드합니다. 귀하의 업무 백그라운드는 이러한 녹화 파일을 풀링하고 업무 요구에 따라 이러한 파일을 병합 트랜스 코딩해야 합니다. [멀티미디어 병합 트랜스 코딩 스크립트](https://intl.cloud.tencent.com/zh/document/product/647/45169#.E5.8D.95.E6.B5.81.E6.96.87.E4.BB.B6.E5.90.88.E5.B9.B6.E8.84.9A.E6.9C.AC)를 제공합니다.

> !
>- 녹화 인터페이스의 호출 주파수: 20qps로 제한
>- 단일 인터페이스 시간 초과: 6초
>- 기본 동시 녹화는 100개 채널을 지원합니다. 더 많은 채널이 필요한 경우 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category?step=0&source=14)을 통해 문의해주십시오.
>- 단일 녹화 작업은 동시에 구독할 수 있는 단일 방에서 최대 25개의 멀티미디어 스트림을 지원합니다.

## 호출 프로세스
### 1. 녹화 실행

백그라운드 서비스를 통해 REST API(CreateCloudRecording)를 호출하여 클라우드 녹화를 실행하며 주의해야 할 매개변수는 다음과 같습니다.

#### 작업 ID(TaskId)

이 매개변수는 녹화 작업의 고유 식별자입니다. 녹화 작업 인터페이스에서 후속 작업을 위해 작업 ID를 입력 매개변수로 저장해야 합니다.

#### 녹화 모드(RecordMode)
- 단일 스트림 녹화, 구독한 호스트의 오디오 및 비디오 파일을 방에 별도로 녹화하고 녹화된 파일(M3U8/TS)을 클라우드 스토리지에 업로드합니다.
- 혼합 스트림 녹화, 방에서 구독하는 모든 호스트의 멀티미디어 스트림을 하나의 멀티미디어 파일로 혼합하고 녹화 파일 [M3U8/TS]를 클라우드 스토리지에 업로드합니다.

#### 사용자 블록리스트/얼로우리스트 녹화(SubscribeStreamUserIds)
기본적으로 클라우드 녹화는 방의 모든 미디어 스트림(최대 25개 채널)을 구독합니다. 이 매개변수를 통해 호스트 사용자의 블록리스트/얼로우리스트 구독을 지정할 수도 있으며, 물론 녹화 중 업데이트 작업도 지원합니다.

#### 클라우드 스토리지 매개변수(StorageParams)
클라우드 스토리지 매개변수를 지정하여 귀하가 활성화한 지정된 클라우드 스토리지/VOD 서비스에 녹화된 파일을 업로드합니다. 클라우드 스토리지/VOD 공간 매개변수의 유효성에 주의하고 연체되지 않도록 주의하십시오. 녹화 파일 이름은 고정 규칙이 있습니다.

##### 녹화 파일명 이름 생성 규칙

* 단일 스트림 녹화 M3U8 파일 이름 규칙:
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>.m3u8

* 단일 스트림 녹화 TS 파일 이름 규칙:
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>\_\<UTC>.ts

* 단일 스트림 녹화 mp4 파일 이름 규칙:
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Index>.mp4

* 혼합 스트림 녹화 M3U8 파일 이름 규칙:
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>.m3u8

* 혼합 스트림 녹화 TS 파일 이름 규칙:
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\<UTC>.ts

* 혼합 스트림 녹화 mp4 파일 이름 규칙:
\<Prefix>/\<TaskId>/\<SdkAppId>\_\<RoomId>\_\<Index>.mp4

* 고가용성 풀업 후 파일 이름 규칙
데이터 센터에서 클라우드 녹화 서비스 장애 시 고가용성 솔루션을 통해 녹화 작업을 복구합니다. 이 경우 원본 녹화 파일을 덮어쓰기하지 않기 위해 풀업 후 접두사 ha<1/2/3>를 추가하여 발생한 고가용성의 횟수를 나타냅니다. 녹화 작업에 허용되는 최대 풀업 횟수는 3회입니다.

* 단일 스트림 녹화 M3U8 파일 이름 규칙:
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>.m3u8

* 단일 스트림 녹화 TS 파일 이름 규칙:
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>\_\_UserId\_s\_\<UserId>\_\_UserId\_e\_\<MediaId>\_\<Type>\_\<UTC>.ts

* 혼합 스트림 녹화 M3U8 파일 이름 규칙:
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>.m3u8

* 혼합 스트림 녹화 TS 파일 이름 규칙:
\<Prefix>/\<TaskId>/ha\<1/2/3>\_\<SdkAppId>\_\<RoomId>\_\<UTC>.ts

#### 필드 의미 설명:
\<Prefix>: 녹화 매개변수에 설정된 파일 이름 접두사는 설정되지 않은 경우 존재하지 않습니다.
\<TaskId>: 녹화된 작업 ID는 전역 고유하며 녹화 실행 후 반환된 매개변수에 있습니다.
\<SdkAppId>: 녹화 작업의 SdkAppId;
\<RoomId>: 녹화 방 번호;
\<UserId>: 특수 base64 처리 후 녹화 스트림의 사용자 ID, 아래 주의사항 참고;
\<MediaId>: 메인/서브스트림 식별, main 또는 aux
\<Type>: 녹화 스트림 유형, audio 또는 video;
\<UTC>: 파일이 시작된 UTC 녹화 시간, 시간대 UTC+0, 년, 월, 일, 시, 분, 초 및 밀리초로 구성;
\<Index>: mp4 슬라이스 로직이 트리거되지 않으면(크기가 2GB를 초과하거나 지속 시간이 24시간을 초과하는 경우) 이 필드가 없습니다. 그렇지 않으면 슬라이스의 인덱스 번호가 1부터 증가;
ha\<1/2/3>: 고가용성 풀업 접두사, 예를 들어 첫 번째 풀업은\<Prefix>/\<TaskId>/ha1\_\<SdkAppId>\_\<RoomId>.m3u8로 변환
>! \<RoomId>가 문자열 방 ID인 경우 먼저 방 ID에 대해 base64 작업을 수행하고 base64 다음 문자열에서 '/' 기호를 '-'(하이픈)으로 변경하고, 기호 '='를 '.'로 변경;
녹화 스트림의 \<UserId>는 먼저 base64 작업을 수행하고 base64 다음 문자열에서 '/' 기호를 '-'(하이픈)으로 변경하고 '=' 기호를 '.'로 변경합니다.

#### 녹화 시작 시간 가져오기
녹화가 시작되는 시간은 서버가 호스트로부터 처음으로 멀티미디어 데이터를 수신하고 첫 번째 파일 녹화를 시작하는 unix 시간으로 정의됩니다.
녹화 시작 타임스탬프를 가져오는 3가지 방법:

* 녹화 파일 인터페이스(DescribeCloudRecording)에서 BeginTimeStamp 필드 쿼리

예를 들어 다음 쿼리 인터페이스에서 반환된 정보는 BeginTimeStamp가 1622186279144ms임을 보여줍니다.

```json
{
  "Response":{
    "Status": "xx",
    "StorageFileList": [
      {
        "TrackType": "xx",
        "BeginTimeStamp": 1622186279144,
        "UserId": "xx",
        "FileName": "xx"
      }
    ],
    "RequestId": "xx",
    "TaskId": "xx"
  }
}
```

* M3U8 파일에서 해당 태그 항목 읽기(\#EXT-X-TRTC-START-REC-TIME)

예를 들어 다음 M3U8 파일은 녹화 시작의 unix 타임스탬프가 1622425551884ms임을 표시합니다.

```m3u8
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-ALLOW-CACHE:NO
#EXT-X-MEDIA-SEQUENCE:0
#EXT-X-TARGETDURATION:70
#EXT-X-TRTC-START-REC-TIME:1622425551884
#EXT-X-TRTC-VIDEO-METADATA:WIDTH:1920 HEIGHT:1080
#EXTINF:12.074
1400123456_12345__UserId_s_MTY4NjExOQ..__UserId_e_main_video_20330531094551825.ts
#EXTINF:11.901
1400123456_12345__UserId_s_MTY4NjExOQ..__UserId_e_main_video_20330531094603825.ts
#EXTINF:12.076
1400123456_12345__UserId_s_MTY4NjExOQ..__UserId_e_main_video_20330531094615764.ts
#EXT-X-ENDLIST
```

* 녹화 콜백 이벤트 수신

콜백 구독을 통해 이벤트 유형 307의 BeginTimeStamp 필드에서 녹화 파일에 해당하는 녹화 시작 타임스탬프 가져오기
예를 들어 다음 콜백 이벤트에서 이 파일의 녹화 시작에 대한 unix 타임스탬프가 1622186279144ms임을 읽을 수 있습니다.

```json
{
        "EventGroupId": 3,
        "EventType":    307,
        "CallbackTs":   1622186289148,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186289",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "FileName":     "xx.m3u8",
                        "UserId":       "xx",
                        "TrackType":    "audio",
                        "BeginTimeStamp":       1622186279144
                }
        }
}
```

#### 혼합 스트림 녹화 워터마크 매개변수(MixWatermark)
혼합 스트림 녹화에서 이미지 추가 워터마크를 지원하며 최대 개수는 25개이며 워터마크는 캔버스의 어느 곳에나 추가할 수 있습니다.

|필드 이름|설명|
|---|---|
|Top|왼쪽 상단 모서리에 대한 워터마크의 수직 변위|
|Left|왼쪽 상단 모서리에 대한 워터마크의 수평 변위|
|Width|워터마크의 너비|
|Height|워터마크의 높이|
|url|워터마크 파일의 저장 url|

#### 혼합 스트림 녹화 레이아웃 모드 매개변수(MixLayoutMode)
3x3 그리드 레이아웃(기본값), 플로팅 레이아웃, 화면 공유 레이아웃 및 사용자 정의 레이아웃 4가지 레이아웃을 지원합니다.

##### 3x3 그리드 레이아웃:

호스트 수에 따라 각 화면의 크기가 자동으로 조절되며, 각 호스트의 화면 크기는 동일하며 최대 25개의 화면을 지원합니다.

* 1개의 서브 화면이 있는 경우:
각 작은 화면의 너비와 높이는 각각 전체 캔버스 너비와 높이;

* 2개의 서브 화면이 있는 경우:
각 작은 화면의 너비는 전체 캔버스 너비의 1/2;
각 작은 화면의 높이는 전체 캔버스 높이;

* 4개 이하의 서브 화면이 있는 경우:
각 작은 화면의 너비와 높이는 각각 전체 캔버스 너비와 높이의 1/2;

* 9개 이하의 서브 화면이 있는 경우:
각 작은 화면의 너비와 높이는 각각 전체 캔버스 너비와 높이의 1/3;

* 16개 이하의 서브 화면이 있는 경우:
각 작은 화면의 너비와 높이는 각각 전체 캔버스 너비와 높이의 1/4;

* 16개 이상의 서브 화면이 있는 경우:
각 작은 화면의 너비와 높이는 각각 전체 캔버스 너비와 높이의 1/5;

 다음 이미지와 같이 구독 서브 화면이 증가함에 따라 3x3 그리드의 레이아웃 변경:

![3x3 그리드 레이아웃1](https://qcloudimg.tencent-cloud.cn/raw/9d989363167bd9231a1ebf3097b8fb5c.jpg)
![3x3 그리드 레이아웃2](https://qcloudimg.tencent-cloud.cn/raw/cd5437606f3a5dceb723d6e63eb283ee.jpg)
![3x3 그리드 레이아웃3](https://qcloudimg.tencent-cloud.cn/raw/98295756807b1aba1457f668f85d7fd9.jpeg)
![3x3 그리드 레이아웃4](https://qcloudimg.tencent-cloud.cn/raw/87b3d8d21d3e22704c379a534faf37b8.jpeg)
![3x3 그리드 레이아웃5](https://qcloudimg.tencent-cloud.cn/raw/3418887536457bfa607ecdfb34a71b7f.jpeg)
![3x3 그리드 레이아웃6](https://qcloudimg.tencent-cloud.cn/raw/ae3aa97ee2cbe5678f1672b34a610d20.jpeg)

##### 플로팅 레이아웃:
기본적으로 방에 입장하는 첫 번째 호스트(호스트를 지정 가능)의 영상 화면이 전체 화면을 채웁니다. 다른 호스트들의 영상 화면은 왼쪽 하단 모서리부터 방에 들어가는 순서대로 가로로 배열되어 작은 화면으로 표시되고 작은 화면은 큰 화면 위에 플로팅됩니다. 화면 수가 17개 이하일 경우 1줄에 4개(4 x 4 배열). 화면 개수가 17개 이상일 경우 작은 화면을 한 줄에 5개(5 x 5)로 다시 레이아웃합니다. 최대 25개의 화면을 지원하며 사용자가 오디오만 보내는 경우 여전히 사진 위치를 차지합니다.

* 17개 이하의 서브 화면이 있는 경우:
       각 작은 화면의 너비와 높이는 각각 전체 캔버스 너비와 높이의 0.235;
       인접한 작은 화면의 왼쪽과 오른쪽, 위쪽과 아래쪽 거리는 각각 전체 캔버스 너비와 높이의 0.012;
       캔버스에서 작은 화면의 가로 및 세로 여백도 전체 캔버스 너비와 높이의 0.012;

* 17개 이상의 서브 화면이 있는 경우:
       각 작은 화면의 너비와 높이는 각각 전체 캔버스 너비와 높이의 0.188;
       인접한 작은 화면의 왼쪽과 오른쪽, 위쪽과 아래쪽 거리는 각각 전체 캔버스 너비와 높이의 0.01;
       캔버스에서 작은 화면의 가로 및 세로 여백도 전체 캔버스 너비와 높이의 0.01;

  플로팅 레이아웃은 다음 이미지와 같이 구독된 서브 화면이 증가함에 따라 변경:
   ![플로팅 레이아웃1](https://qcloudimg.tencent-cloud.cn/raw/96a531ba9f6a69297ea4f1a5a365794a.jpg)
   ![플로팅 레이아웃2](https://qcloudimg.tencent-cloud.cn/raw/be91b17b6b557fcd7d1d76c589e15917.jpg)


##### 화면 공유 레이아웃:
화면 왼쪽에 있는 호스트의 큰 화면 위치를 지정하고(지정하지 않으면 큰 화면 위치가 배경색이 됨) 다른 호스트는 오른쪽에서 위에서 아래로 세로로 정렬됩니다. 화면 수가 17개 미만인 경우 오른쪽의 각 컬럼은 최대 8명까지 가능하며, 최대 2개의 컬럼을 차지합니다. 화면 개수가 17개 이상일 경우, 17개 이상의 화면이 있는 호스트는 왼쪽 하단 모서리부터 수평으로 정렬됩니다. 최대 24개의 화면을 지원하며 호스트가 오디오만 보내는 경우에도 화면 위치를 차지합니다.

* 5개 이하의 서브 화면이 있는 경우:
오른쪽 작은 화면의 너비는 전체 캔버스 너비의 1/5이고 오른쪽 작은 화면의 높이는 전체 캔버스 높이의 1/4;
왼쪽의 큰 화면의 너비는 전체 캔버스 너비의 4/5이고 왼쪽의 큰 화면의 높이는 전체 캔버스의 높이;

* 5보다 크고 7보다 작은 서브 화면이 있는 경우:
오른쪽 작은 화면의 너비는 전체 캔버스 너비의 1/7이고 오른쪽 작은 화면의 높이는 전체 캔버스 높이의 1/6;
왼쪽의 큰 화면의 너비는 전체 캔버스 너비의 6/7이고 왼쪽의 큰 화면의 높이는 전체 캔버스의 높이;
* 7보다 크고 9보다 작은 서브 화면이 있는 경우:
오른쪽 작은 화면의 너비는 전체 캔버스 너비의 1/9이고 오른쪽 작은 화면의 높이는 전체 캔버스 높이의 1/8;
왼쪽의 큰 화면의 너비는 전체 캔버스 너비의 8/9이고 왼쪽의 큰 화면의 높이는 전체 캔버스의 높이;

* 9보다 크고 17보다 작은 서브 화면이 있는 경우:
오른쪽 작은 화면의 너비는 전체 캔버스 너비의 1/10이고 오른쪽 작은 화면의 높이는 전체 캔버스 높이의 1/8;
왼쪽의 큰 화면의 너비는 전체 캔버스 너비의 4/5이고 왼쪽의 큰 화면의 높이는 전체 캔버스의 높이;

* 17개 이상의 서브 화면이 있는 경우:
오른쪽(아래) 쪽의 작은 화면의 너비는 전체 캔버스 너비의 1/10이고 오른쪽(아래) 쪽의 작은 화면의 높이는 전체 캔버스 높이의 1/8;
왼쪽의 큰 화면의 너비는 전체 캔버스 너비의 4/5이고 왼쪽의 큰 화면의 높이는 전체 캔버스의 높이의 7/8;

아래와 같이 구독된 서브 화면이 증가함에 따라 화면 공유 레이아웃 변경:
   ![화면 공유 레이아웃1](https://qcloudimg.tencent-cloud.cn/raw/d64e7e705060d21ec24d7392f8d43728.png)
   ![화면 공유 레이아웃2](https://qcloudimg.tencent-cloud.cn/raw/695683aecb62c29976f16124d6e9b29b.png)
   ![화면 공유 레이아웃3](https://qcloudimg.tencent-cloud.cn/raw/8423e777eb1a5bfb80e384e7b97db49d.png)
   ![화면 공유 레이아웃4](https://qcloudimg.tencent-cloud.cn/raw/538faeb7d2f993427b7ab1db548cb633.png)
   ![화면 공유 레이아웃4](https://qcloudimg.tencent-cloud.cn/raw/f911eb5a849da0aa22ed9b69ebe2f63a.png)

##### 사용자 정의 레이아웃:
업무 요구에 따라 MixLayoutList에서 각 호스트 화면의 레이아웃 정보를 사용자 정의합니다.

### 2. 녹화 쿼리(DescribeCloudRecording)
필요한 경우 이 인터페이스를 호출하여 녹화 서비스의 상태를 쿼리할 수 있습니다. 정보는 녹화 작업이 있는 경우에만 쿼리할 수 있으며, 녹화 작업이 종료되면 오류가 반환됩니다.
녹화된 파일 목록(StorageFile)에는 이번에 녹화된 모든 M3U8 인덱스 파일과 녹화의 시작 Unix 타임스탬프 정보가 포함됩니다. VOD 업로드 작업인 경우 이 인터페이스에서 반환된 StorageFile이 비어 있습니다.

### 3. 녹화 업데이트(ModifyCloudRecording)
필요한 경우 이 인터페이스를 호출하여 SubscribeStreamUserIds(단일 스트림 및 혼합 스트림 녹화에 유효) 및 녹화된 템플릿 매개변수 MixLayoutParams(혼합 스트림 녹화에 유효)와 같은 녹화 서비스의 매개변수를 수정할 수 있습니다. 업데이트 작업은 증분 업데이트 작업이 아닌 전체 적용 작업입니다. 템플릿 매개변수 MixLayoutParams 및 블록리스트/얼로우리스트인 SubscribeStreamUserIds를 포함하여 업데이트할 때마다 전체 정보를 전달해야 합니다. 따라서 녹화를 실행하거나 전체 녹화 관련 매개변수를 다시 계산하려면 이전 매개변수를 저장해야 합니다.

### 4. 녹화 중지(DeleteCloudRecording)
녹화 종료 후에는 녹화 중지(DeleteCloudRecording) 인터페이스를 호출하여 녹화 작업을 종료해야 하며, 그렇지 않으면 사전 설정된 시간 초과 MaxIdleTime에 도달하면 녹화 작업이 자동으로 종료됩니다. MaxIdleTime의 정의는 방에 호스트가 없는 상태가 MaxIdleTime의 지속시간을 초과하는 것으로, 여기서 방에 호스트가 있지만 호스트에 업스트림 데이터가 없으면 타임아웃 카운트다운 상태에 들어가지 않습니다. 녹화가 종료되면 서비스에서 이 인터페이스를 호출하여 녹화 작업을 종료하는 것이 좋습니다.

## 고급 기능

### 녹화 mp4 파일

출력 파일 형식을 mp4 형식으로 녹화하려면 매개변수(OutputFormat)에 녹화 파일의 출력 형식을 hls+mp4로 지정하여 녹화를 실행할 수 있습니다. hls 파일은 기본적으로 계속 녹화됩니다. hls 녹화가 완료되면 mp4 변환 작업이 즉시 트리거되고 hls가 있는 cos에서 mp4 캡슐화 풀 스트림 후 클라이언트의 cos에 업로드합니다.
여기서 COS의 파일 풀다운 권한을 제공해야 합니다. 그렇지 않으면 hls 파일 풀다운이 실패하여 mp4 작업으로 전송이 종료됩니다.
mp4 파일은 다음과 같은 경우 강제로 샤드됩니다.

1. 녹화 시간이 24시간을 초과하는 경우;
2. 단일 mp4 파일의 크기가 2GB에 도달;
   <br>특정 프로세스는 이미지 참고
   <br>![출력 MP4](https://qcloudimg.tencent-cloud.cn/raw/d3a3f5121e9832cc8a39b8d9ec6f7b1a.png)

### 녹화 VOD 업로드

녹화된 출력 파일을 VOD 플랫폼에 업로드하려면 녹화를 실행하기 위한 스토리지 매개변수(StorageParams)에 CloudVod 참석자 매개변수를 지정할 수 있습니다. 녹화 백그라운드는 녹화가 끝난 후 지정한 방식으로 녹화된 mp4 파일을 VOD 플랫폼에 업로드 하고, 콜백 형태로 재생 주소를 보내드립니다. 녹화 모드가 단일 스트림 녹화 모드인 경우 구독된 각 호스트에는 해당 재생 주소가 있고 녹화 모드가 혼합 스트림 녹화 모드인 경우 혼합 스트림 미디어의 재생 주소는 하나만 있습니다. VOD 작업 업로드에는 다음과 같은 주의 사항이 있습니다. 

1. 스토리지 매개변수의 CloudVod 및 CloudStorage 중 하나만 동시에 지정할 수 있습니다. 그렇지 않으면 녹화 실패;
2. VOD 작업을 업로드하는 과정에서 DescribeCloudRecording을 사용하여 쿼리한 작업 상태에는 녹화된 파일의 정보 불포함;
   <br>구체적인 과정을 이미지로 나타내었는데, 여기에서 클라우드 스토리지는 녹화를 위한 내부 클라우드 스토리지이며 클라이언트는 관련 매개변수를 입력할 필요가 없습니다.
   <br>![출력vod](https://qcloudimg.tencent-cloud.cn/raw/28da00ba87fc1b9be2030f96d2dfd820.png)



### 단일 스트림 파일 병합 스크립트

단일 스트림 녹화 멀티미디어 파일을 MP4 파일로 병합하는 데 사용되는 [단일 스트림 멀티미디어 파일 병합 스크립트]()를 제공합니다.

>? 두 슬라이스 사이의 시간 간격이 15초 이상이고 간격에 오디오/비디오 정보가 없는 경우(서브스트림이 비활성화된 경우 서브스트림 정보는 무시됨) 두 슬라이스를 두 개의 다른 세그먼트로 처리합니다. 녹화 시간이 더 빠른 슬라이스는 이전 세그먼트의 끝 슬라이스로 간주되고, 녹화 시간이 더 늦은 슬라이스는 다음 세그먼트의 시작 슬라이스로 간주됩니다.

 - 세그먼트 모드(-m 0)
이 모드에서 스크립트는 각 UserId 아래의 녹화 파일을 세그먼트별로 병합하고 UserId 아래의 세그먼트는 독립적으로 파일에 병합됩니다.
 - 병합 모드(-m 1)
동일한 UserId 아래의 모든 세그먼트를 하나의 멀티미디어 파일로 결합합니다. -s 옵션은 세그먼트 사이의 간격을 채울지 여부를 선택하는 데 사용할 수 있습니다.

#### 종속 환경

Python3

-   Centos: sudo yum install python3
-   Ubuntu: sudo apt-get install python3

Python3 종속 패키지

-	sortedcontainers：pip3 install sortedcontainers

#### 사용 방법

 1. 병합 스크립트 실행: python3 TRTC_Merge.py [option]
 2. 녹화 파일 디렉터리에 병합된 mp4 파일 생성
예시: python3 TRTC_Merge.py -f /xxx/file -m 0

선택적 매개변수와 해당 기능은 다음 표 참고:

|매개변수| 기능 |
|---|---|
|-f | 병합할 파일의 저장 경로를 지정합니다. UserId 녹화 파일이 여러 개인 경우 스크립트는 파일을 별도로 병합합니다. |
|-m   | 0: 세그먼트 모드(기본 설정), 이 모드에서 스크립트는 세그먼트별로 각 UserId 아래의 녹화 파일을 병합하고 각 UserId는 여러 파일을 생성할 수 있습니다. <br>1: 병합 모드에서는 UserId 아래의 모든 멀티미디어 파일이 하나의 파일로 병합됩니다.|
|-s|저장 모드. 이 매개변수가 설정되면 병합 모드에서 세그먼트 사이의 공백이 삭제되고 파일의 실제 시간은 물리적 일반 시간보다 작습니다.|
|-a|0: 주요 스트림 병합(기본 설정), 동일한 UserId의 주요 스트림 오디오와 병합되고 서브 스트림은 오디오와 병합되지 않습니다. <br>1: 자동 병합, 주요 스트림이 있으면 주요 스트림과 오디오가 병합되고, 주요 스트림이 없으면 서브 스트림과 오디오가 병합됩니다. <br>2: 서브 스트림 병합, 동일한 UserId의 서브 스트림과 오디오가 병합되고 주요 스트림은 오디오와 병합되지 않습니다.|
|-p|출력 비디오의 fps를 지정합니다. 기본값은 15 fps이고 유효한 범위는 5-120 fps이며 5 fps 미만은 5 fps로, 120 fps 이상은 120 fps로 계산합니다.|
|-r|출력 비디오의 해상도를 지정합니다. 예를 들어 -r 640 360은 출력 비디오의 너비가 640이고 높이가 360임을 의미합니다.|

**파일 이름 규칙**

- 멀티미디어 파일 이름 규칙: UserId\_timestamp\_av.mp4
- 퓨어 오디오 파일 이름 규칙: UserId\_timestamp.m4a

>? 여기서 UserId는 녹화 스트림의 사용자 ID의 특수한 base64 값입니다. 자세한 내용은 실행 녹화 파일 이름 명명 규칙에 대한 설명을 참고하십시오. timestamp는 각 세그먼트의 첫 번째 ts 슬라이스에 대해 녹화가 실행된 시간입니다.



## 콜백 인터페이스

콜백을 수신하는 Http/Https 서비스 게이트웨이를 제공하여 콜백 메시지를 구독할 수 있습니다. 관련 이벤트가 발생하면 클라우드 녹화 시스템이 이벤트 공지를 메시지 수신 서버로 다시 콜백합니다.

### 이벤트 콜백 메시지 포맷

이벤트 콜백 메시지는 HTTP/HTTPS POST 요청 형식으로 사용자의 서버에 전송됩니다.
문자 인코딩 포맷: UTF-8.
요청: body 포맷은 JSON.
응답: HTTP STATUS CODE = 200, 서버가 응답 패키지의 세부 콘텐츠를 무시합니다. 원활한 프로토콜 연결을 위해 클라이언트 응답 콘텐츠에 JSON: {"code":0} 추가를 권장합니다.

### 매개변수 설명

이벤트 콜백 메시지의 header는 다음과 같은 필드 포함:


| 필드 이름       | 값                 |
| ------------ | ------------------ |
| Content-Type | application/json   |
| Sign         | 서명 값             |
| SdkAppId     | sdk application id |

이벤트 콜백 메시지의 body는 다음과 같은 필드 포함:

| 필드 이름       | 유형       | 의미                                                         |
| ------------ | ----------- | ------------------------------------------------------------ |
| EventGroupId | Number      | 이벤트 그룹 ID, 클라우드 녹화를 위해 3으로 고정                                  |
| EventType    | Number      | 콜백 공지의 이벤트 유형                                           |
| CallbackTs   | Number      | 이벤트 콜백 서버에서 귀하의 서버로 보낸 콜백 요청의 Unix 타임스탬프, 단위: 밀리초 |
| EventInfo    | JSON Object | 이벤트 정보                                                     |

이벤트 유형 설명

| 필드 이름                                                | 유형 | 의미                                                    |
| ----------------------------------------------------- | ---- | ------------------------------------------------------- |
| EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_START        | 301  | 클라우드 녹화 녹화 모듈 실행                                   |
| EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_STOP         | 302  | 클라우드 녹화 녹화 모듈 종료                                   |
| EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_START          | 303  | 클라우드 녹화 업로드 모듈 실행                                   |
| EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_INFO             | 304  | 클라우드 녹화 m3u8 인덱스 파일 생성, 첫 번째 생성 및 업로드 완료 후 콜백 |
| EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_STOP           | 305  | 클라우드 녹화 업로드 종료                                       |
| EVENT\_TYPE\_CLOUD\_RECORDING\_FAILOVER               | 306  | 클라우드 녹화 마이그레이션이 발생, 기존 녹화 작업이 새 부하로  마이그레이션될 때 트리거 |
| EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_SLICE            | 307  | 클라우드 녹화 M3U8 파일 생성(첫 번째 ts 샤드 잘라내기) 생성 후 콜백      |
| EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_ERROR          | 308  | 클라우드 녹화 업로드 모듈에서 오류 발생                               |
| EVENT\_TYPE\_CLOUD\_RECORDING\_DOWNLOAD\_IMAGE\_ERROR | 309  | 클라우드 녹화 디코딩된 이미지 파일 다운로드 시 오류 발생                      |
| EVENT\_TYPE\_CLOUD\_RECORDING\_MP4\_STOP              | 310  | 클라우드 녹화 mp4 녹화 작업이 종료되고 콜백에 녹화된 mp4 파일 이름 포함       |
| EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_COMMIT            | 311  | 클라우드 녹화 vod 녹화 작업 업로드 미디어 리소스 완료                    |
| EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_STOP              | 312  | 클라우드 녹화 vod 녹화 작업 종료                                |


이벤트 정보 설명

| 필드 이름  | 유형          | 의미                                 |
| ------- | ------------- | ------------------------------------ |
| RoomId  | String/Number | 방 이름(유형이 클라이언트 방 번호 유형과 일치) |
| EventTs | Number       | 이벤트 발생 시간의 Unix 타임스탬프, 단위: 초    |
| UserId  | String        | 녹화 로봇의 사용자 ID                  |
| TaskId  | String        | 녹화 ID, 클라우드 녹화 작업의 고유 ID     |
| Payload | JsonObject    | 다양한 이벤트 유형에 대한 다양한 정의             |

이벤트 유형이 301 EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_START일 때 Payload 정의

| 필드     | 유형   | 의미                                                         |
| ------ | ------ | -------------------------------------------------- |
| Status | Number | 0: 녹화 모듈 실행 성공, 1: 녹화 모듈 실행 실패. |

```json
{
        "EventGroupId": 3,
        "EventType":    301,
        "CallbackTs":   1622186275913,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186275",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

이벤트 유형이 302 EVENT\_TYPE\_CLOUD\_RECORDING\_RECORDER\_STOP일 때 Payload 정의

| 필드     | 유형   | 의미                                                         |
| --------- | ------ | ------------------------------------------------------------ |
| LeaveCode | Number | 0: 녹화 모듈은 일반적으로 녹화를 중지하고 종료하도록 호출됨;<br>1: 녹화 로봇은 클라이언트에 의해 방에서 퇴장;<br>2: 클라이언트가 방을 해산;<br>3: 서버가 녹화 로봇을 퇴장시킴;<br>4: 서버가 방 해산;<br>99: 방에 녹화 로봇 외에 다른 사용자 스트림이 없으며 지정된 시간 후에 퇴장;<br>100: 방 시간 초과로 퇴장;<br>101: 같은 사용자가 같은 방에 반복적으로 입장하면 로봇이 퇴장됨 |

```json
{
        "EventGroupId": 3,
        "EventType":    302,
        "CallbackTs":   1622186354806,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186354",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "LeaveCode":    0
                }
        }
}
```

이벤트 유형이 303 EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_START일 때 Payload 정의

| 필드     | 유형   | 의미                                                         |
| ------ | ------ | ------------------------------------------------------ |
| Status | Number | 0: 업로드 모듈이 정상적으로 실행<br>1: 업로드 모듈 초기화 실패. |

```json
{
        "EventGroupId": 3,
        "EventType":    303,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

이벤트 유형이 304 EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_INFO일 때 Payload 정의

| 필드   | 유형   | 의미             |
| -------- | ------ | ---------------- |
| FileList | String | 생성된 M3U8 파일 이름 |

```json
{
        "EventGroupId": 3,
        "EventType":    304,
        "CallbackTs":   1622191965350,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "FileList":     "xx.m3u8"
                }
        }
}
```


이벤트 유형이 305 EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_STOP일 때 Payload 정의

| 필드     | 유형   | 의미                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| Status | Number | 0: 녹화 및 업로드 작업이 완료되었으며 모든 파일이 지정된 타사 클라우드 스토리지에 업로드 됨<br>1: 녹화 및 업로드 작업이 완료되었지만 적어도 하나의 파일이 서버 또는 백업 저장소에 남아 있음<br>2: 서버 또는 백업 스토리지에 멈춘 파일이 복구되어 지정된 타사 클라우드 스토리지에 업로드 |

```json
{
        "EventGroupId": 3,
        "EventType":    305,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

이벤트 유형이 306 EVENT\_TYPE\_CLOUD\_RECORDING\_FAILOVER일 때 Payload 정의

| 필드 | 유형   | 의미                    |
| ------ | ------ | ----------------------- |
| Status | Number | 0: 마이그레이션 완료됨 |

```json
{
        "EventGroupId": 3,
        "EventType":    306,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```

이벤트 유형은 307 EVENT\_TYPE\_CLOUD\_RECORDING\_FILE\_SLICE일 때 Payload 정의

| 필드         | 유형   | 의미                                |
| -------------- | ------ | ----------------------------------- |
| FileName       | String | m3u8 파일 이름                          |
| UserId         | String | 이 녹화 파일에 해당하는 사용자 ID              |
| TrackType      | String | audio/video/audio_video             |
| BeginTimeStamp | Number | 녹화 시작 시 서버 Unix 타임스탬프(밀리초) |


```json
{
        "EventGroupId": 3,
        "EventType":    307,
        "CallbackTs":   1622186289148,
        "EventInfo":    {
                "RoomId":       "xx",
                "EventTs":      "1622186289",
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "FileName":     "xx.m3u8",
                        "UserId":       "xx",
                        "TrackType":    "audio",
                        "BeginTimeStamp":       1622186279144
                }
        }
}
```

이벤트 유형은 308 EVENT\_TYPE\_CLOUD\_RECORDING\_UPLOAD\_ERROR일 때 Payload 정의

| 필드  | 유형   | 의미                       |
| ------- | ------ | -------------------------- |
| Code    | String | 타사 클라우드 스토리지의 반환 code     |
| Message | String | 타사 클라우드 스토리지의 메시지 콘텐츠 반환 |


```json
{
  "Code": "InvalidParameter",
  "Message": "AccessKey invalid"
}

{
        "EventGroupId": 3,
        "EventType":    308,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Code":       "xx",
                        "Message":    "xx"
                }
        }
}
```

이벤트 유형은 309 EVENT\_TYPE\_CLOUD\_RECORDING\_DOWNLOAD\_IMAGE\_ERROR일 때 Payload 정의

| 필드 | 유형   | 의미          |
| ------ | ------ | ------------- |
| Url    | String | 다운로드 실패 url |


```json
{
        "EventGroupId": 3,
        "EventType":    309,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Url":       "http://xx",
                }
        }
}
```

이벤트 유형은 310 EVENT\_TYPE\_CLOUD\_RECORDING\_MP4\_STOP일 때 Payload 정의

| 필드     | 유형   | 의미                                                         |
| -------- | ------ | ------------------------------------------------------------ |
| Status   | Number | 0: mp4 녹화 작업이 정상적으로 종료되었으며 모든 파일이 지정된 타사 클라우드 스토리지에 업로드되었음<br>1: mp4 녹화 작업이 정상적으로 종료되었지만 적어도 하나의 파일이 서버 또는 백업 스토리지에 남아 있음<br>2: mp4 녹화 작업의 비정상 종료(예상 원인은 cos의 hls 파일 풀링 실패) |
| FileList | String | 생성된 M3U8 파일 이름                                             |


```json
{
        "EventGroupId": 3,
        "EventType":    310,
        "CallbackTs":   1622191989674,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191989,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0,
                        "FileList": ["xxxx1.mp4", "xxxx2.mp4"]
                }
        }
}
```

이벤트 유형은 311 EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_COMMIT일 때 Payload 정의

| 필드     | 유형   | 의미                                                         |
| --------- | ------ | ------------------------------------------------------------ |
| Status    | Number | 0: 녹화 파일은 VOD 플랫폼에 정상적으로 업로드 됨<br>1: 이 녹화 파일은 서버 또는 백업 스토리지에 남아있음<br>2: 이 녹화 파일을 업로드하는 VOD 작업이 비정상 |
| UserId    | String | 이 녹화 파일에 해당하는 사용자 ID(녹화 모드가 혼합 스트림 모드인 경우 이 필드는 비어 있음) |
| TrackType | String | audio/video/audio_video                                      |
| MediaId   | String | main/aux                                                     |
| FileId    | String | VOD 플랫폼에서 이 녹화 파일의 고유 id                                 |
| VideoUrl  | String | VOD 플랫폼에서 이 녹화 파일의 재생 주소                               |
| CacheFile | String | 이 녹화 파일에 해당하는 mp4 파일 이름(VOD 업로드 전)                  |
| Errmsg    | String | statue가 0이 아닌 경우, 해당 오류 메시지                                |


성공적인 콜백 업로드:

```json
{
        "EventGroupId": 3,
        "EventType":    311,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0,
                        "TencentVod":   {
                            "UserId":       "xx",
                            "TrackType":    "audio_video",
                            "MediaId":      "main",
                            "FileId":       "xxxx",
                            "VideoUrl":     "http://xxxx"
                        }
                }
        }
}
```

업로드 실패 콜백:

```json
{
        "EventGroupId": 3,
        "EventType":    311,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       1,
                        "Errmsg":       "xxx",
                        "TencentVod":   {
                            "UserId":       "123",
                            "TrackType":    "audio_video",
                            "CacheFile":    "xxx.mp4"
                        }
                }
        }
}
```

이벤트 유형은 312 EVENT\_TYPE\_CLOUD\_RECORDING\_VOD\_STOP일 때 Payload 정의

| 필드     | 유형   | 의미                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| Status | Number | 0: 이번 vod 업로드 작업이 정상적으로 종료됨<br>1: vod 업로드 작업이 비정상적으로 종료 |


```json
{
        "EventGroupId": 3,
        "EventType":    312,
        "CallbackTs":   1622191965320,
        "EventInfo":    {
                "RoomId":       "20015",
                "EventTs":      1622191965,
                "UserId":       "xx",
                "TaskId":       "xx",
                "Payload":      {
                        "Status":       0
                }
        }
}
```



## 모범 사례

녹화의 고가용성을 보장하기 위해 Restful API를 통합할 때 다음 사항을 주의하십시오.

1. CreateCloudRecording 요청을 호출한 후 http response에 주의를 기울이고, 요청이 실패할 경우 특정 상태 코드에 따라 해당 재시도 정책을 채택해야 합니다.

   에러 코드는 ‘InvalidParameter.SdkAppId’와 같이 ‘1차 에러 코드’와 ‘2차 에러 코드’로 구성됩니다.

   - 반환된 Code가 InValidParameter.xxxxx이면 입력 매개변수가 잘못된 것이므로 프롬프트에 따라 매개변수를 확인하십시오.
   - 반환된 Code가 InternalError.xxxxx이면 서버 측 오류가 발생했음을 의미합니다. taskid를 얻을 때까지 반환이 정상이 될 때까지 동일한 매개변수를 사용하여 여러 번 재시도할 수 있습니다. 첫 번째 3초 재시도, 두 번째 6초 재시도, 세 번째 12초 재시도 등과 같은 백오프 재시도 정책을 사용하는 것이 좋습니다.
   - 반환된 Code가 FailedOperation.RestrictedConcurrency인 경우 클라이언트의 동시 녹화 작업 수가 백그라운드에서 예약된 리소스(기본적으로 100개 채널)를 초과한다는 의미이므로 최대 동시 채널 제한을 조정하려면 Tencent Cloud 기술 지원에 문의하십시오. 

2. CreateCloudRecording 인터페이스 호출 시 지정된 UserId/UserSig는 별도의 로봇 사용자로 방에 참여하는 기록된 사용자의 ID이므로 TRTC 방의 다른 사용자와 중복하지 마십시오. 동시에, TRTC 클라이언트에 의해 추가된 방 유형은 녹화 인터페이스에서 지정한 방 유형과 동일해야 합니다. 예를 들어 SDK가 문자열 방 번호를 사용하여 방을 생성하는 경우 클라우드에 녹화된 방 유형은 또한 그에 따라 문자열 방 번호로 설정해야 합니다.

3. 녹화 상태 쿼리를 위해 클라이언트는 다음과 같은 방법으로 녹화의 해당 파일 정보를 얻을 수 있습니다.

   - CreateCloudRecording 작업이 성공적으로 제안된 후 약 15초 후에 DescribeCloudRecording 인터페이스를 호출하여 녹화 파일에 해당하는 정보를 쿼리합니다. 상태가 idle인 경우 멀티미디어 스트림이 업스트림에 업로드되고 있지 않음을 의미하므로 방에 업스트림 호스트가 있는지 확인하십시오.
   - CreateCloudRecording을 성공적으로 제안된 후, 방에 업스트림 멀티미디어가 있는지 확인하면서 녹화 파일 이름 생성 규칙에 따라 녹화 파일 이름을 스티칭할 수 있습니다. 특정 파일 이름 규칙에 대해서는 위를 참고하십시오(여기에 파일 이름 규칙에 대한 링크가 있습니다).
   - 녹화 파일의 상태는 콜백을 통해 클라이언트의 서버로 전송되며, 해당 콜백을구독하면 녹화 파일의 상태 정보를 받아볼 수 있습니다(여기에 콜백 페이지 링크가 있습니다).
   - Cos를 통해 녹화 파일 쿼리, 클라우드 녹화 제안 시 cos의 스토리지 디렉터리를 지정할 수 있으며, 녹화 작업 종료 후 해당 디렉터리를 찾아 녹화 파일을 찾을 수 있습니다.

