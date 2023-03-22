본문은 사용자 지정 녹음 방식으로 **GME 서버 녹음** 기능을 빠르게 통합할 수 있도록 도와줍니다.



## 시나리오

GME는 실시간 음성 채팅 스트림을 위한 **서버 녹음** 기능을 제공하여 개발자가 콘텐츠 보관, 콘텐츠 관리 및 콘텐츠 재생산과 같은 시나리오를 구현할 수 있도록 지원합니다. 전체 녹음: 애플리케이션 내 전체 음성 녹음과 방별 혼합 스트림, 사용자별 단일 스트림을 지원합니다. 사용자 지정 녹음: 지정된 방의 방별 혼합 스트림, 사용자별 단일 스트림을 지원합니다. 녹음된 오디오 파일은 귀하의 계정에 있는 **COS** 서비스에 저장됩니다.

본문은 **사용자 지정 녹음**의 개발 및 통합 방법에 대해서만 설명합니다. 애플리케이션에 전체 녹음을 활성화하려면 [개발 가이드 - 전체 녹음](https://www.tencentcloud.com/ko/document/product/607/53747)을 참고하십시오.

>! 
>- GME 서버 녹음 기능을 사용하면 녹음 과정에서 GME에서 녹음 서비스 요금이 발생합니다. GME 글로벌 포털 녹음 서비스는 2023년 4월 1일부터 정식 과금될 예정이며, 자세한 내용은 [GME 구매 가이드](https://www.tencentcloud.com/ko/document/product/607/50009?lang=ko&pg=)에 공지됩니다.
>- 녹음된 파일은 Tencent Cloud 계정의 **COS** 서비스에 저장되며 저장 용량, 저장 기간 및 액세스 빈도 등 고객의 구체적인 사용 방식에 따라 **COS** 청구서가 발행됩니다. 자세한 내용은 [COS 과금 개요](https://www.tencentcloud.com/ko/document/product/436/16871?lang=ko&pg=)를 참고하십시오.

## 전제 조건

- **실시간 음성 채팅 서비스 활성화 완료**: [서비스 활성화](https://www.tencentcloud.com/ko/document/product/607/10782?lang=ko&pg=)를 참고하십시오.
- **서버 녹음 서비스 활성화 완료**: 현재 서버 녹음 기능은 얼로우리스트에 있는 사용자에게 제공됩니다. 얼로우리스트를 활성화하려면 당사에 문의하십시오.
- **GME SDK 통합 완료**: 핵심 API 및 실시간 음성 채팅 API 통합을 포함합니다. 자세한 내용은 [Native SDK 빠른 통합](https://www.tencentcloud.com/ko/document/product/607/40858?lang=ko&pg=), [Unity SDK 빠른 통합](https://www.tencentcloud.com/ko/document/product/607/44544?lang=ko&pg=), [Unreal SDK 빠른 통합](https://www.tencentcloud.com/ko/document/product/607/44545?lang=ko&pg=)을 참고하십시오.


## 서비스 아키텍처

![](https://staticintl.cloudcachetci.com/yehe/backend-news/zUFy538_PRELIM__%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8E_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-2.png)

## 기능 설명

### 1. 녹음 범위
서버 API를 통해 녹음할 방 ID 혼합 스트림 또는 단일 사용자 스트림을 지정할 수 있습니다.
녹음할 지정된 방 ID에 대해 서버 API 매개변수를 통해 녹음할 플레이어를 얼로우리스트로 또는 녹음하지 않을 플레이어를 블록리스트로 지정할 수 있습니다.

### 2. 관련 API

- [ ***StartRecord()*** ](https://www.tencentcloud.com/ko/document/product/607/53736)  **녹음 시작**
이 API 매개변수에서 단일 스트림 또는 혼합 스트림 녹음 정의, 녹음할 RoomID 지정, 얼로우리스트 또는 블록리스트의 사용자 ID를 지정할 수 있습니다.

- [ ***StopRecord()***](https://www.tencentcloud.com/ko/document/product/607/53735)  **녹음 종료**
이 API를 통해 taskid에 대한 녹음을 중지할 수 있습니다. taskid를 기록하지 않은 경우 DescribeTaskInfo()를 통해 지정된 방에서 진행 중인 녹음 작업의 taskid를 가져와야 합니다.

- [***ModifyRecordInfo()***](https://www.tencentcloud.com/ko/document/product/607/53737)  **녹음 정보 업데이트**
이 API를 통해 taskid의 녹음 유형 업데이트, 얼로우리스트 사용자 ID 또는 블록리스트 사용자 ID 업데이트 등 녹음 정보를 업데이트할 수 있습니다. taskid를 기록하지 않은 경우 DescribeTaskInfo()를 통해 지정된 방에서 진행 중인 녹음 작업의 taskid를 가져와야 합니다.

- [***DescribeTaskInfo()***](https://www.tencentcloud.com/ko/document/product/607/53738) **방 녹음 정보 쿼리**
이 API를 통해 지정된 방의 진행 중인 녹음 작업의 taskid, 얼로우리스트/블록리스트 사용자의 ID 등 녹음 정보를 쿼리할 수 있습니다.

- [***DescribeRecordInfo()***](https://www.tencentcloud.com/ko/document/product/607/53739) **녹음 작업 정보 쿼리**
이 API를 통해 taskid의 녹음 유형, 녹음 방 ID, 녹음 사용자 ID, 녹음 파일 정보 등 작업 정보를 쿼리할 수 있습니다.


### 3. 녹음 메커니즘

#### 녹음 작업 실행 메커니즘
- [***StartRecord()***](https://www.tencentcloud.com/document/product/607/53736)*** API를 호출하면 지정된 방 녹음 작업이 시작됩니다

#### 녹음 작업 종료 메커니즘
- [***StopRecord()***](https://www.tencentcloud.com/document/product/607/53735)*** API를 호출하면 지정된 방 녹음 작업이 종료됩니다


#### 녹음 파일 생성 타이밍
- 방 혼합 스트림 녹음 파일: 방 녹음 작업이 실행된 후 이미 방에 사용자가 있는 경우 혼합 스트림 오디오 파일이 즉시 생성되기 시작합니다. 방에 사용자가 없는 경우 첫 번째 사용자가 방에 들어온 직후 혼합 스트림 오디오 파일이 생성됩니다.
- 사용자 단일 스트림 녹음 파일: 방 녹음 작업이 시작된 후 녹음 범위 내의 사용자가 방에 들어오면 사용자의 단일 스트림 오디오 파일이 즉시 생성되기 시작합니다.


#### 녹음 작업 분할 메커니즘

- 단일 오디오 파일 길이가 2시간이 되면 자동으로 오디오 파일을 분할합니다
- 사용자가 마이크를 끄면 사용자의 단일 스트림 녹음이 자동으로 분할되고 사용자가 마이크를 켜면 새로운 세그먼트가 시작됩니다
- 녹음 작업이 비정상적으로 중단된 경우 작업이 자동으로 재연결된 후 새로운 파일이 시작됩니다


#### 녹음 작업 이벤트 알림 메커니즘

- 녹음 작업 이벤트는 콜백 메커니즘을 통해 설정한 콜백 주소로 알림됩니다. **녹음 시작**, **녹음 중지**, **녹음 파일 업로드 완료** 이벤트가 발생하면 콜백 알림을 받게 됩니다.
- 콜백 정보에 대한 자세한 내용은 [녹음 콜백](https://www.tencentcloud.com/ko/document/product/607/53749)을 참고하십시오


### 4. 저장 위치

GME 서버 녹음 파일은 귀하의 계정에 있는 **COS** 서비스의 지정된 버킷에 저장됩니다. 버킷의 리전은 귀하가 지정합니다. 선택 가능한 리전 목록은 [리전 및 액세스 도메인](https://www.tencentcloud.com/ko/document/product/436/6224?lang=ko&pg=)을 참고하십시오.


### 5. 녹음 파일 형식

- .mp3


### 6. 녹음 파일 이름 생성 규칙

- 사용자 단일 스트림 녹음 파일: bizid_roomid_userid/${작업 시작 시간}_${id}_audio.mp3
- 방 혼합 스트림 녹음 파일: bizid_roomid/${taskid}_${작업 시작 시간}_${id}_audio.mp3

 ***bizid:*** GME 애플리케이션 ID입니다. [GME 콘솔](https://console.tencentcloud.com/gamegme)에서 가져올 수 있습니다.
 ***roomid:*** 음성 방 ID입니다. 실시간 음성 채팅 서비스 이용 시 정의되어 GME SDK로 전달됩니다.
 ***userid:*** 플레이어 ID입니다. 실시간 음성 채팅 서비스 이용 시 정의되어 GME SDK로 전달됩니다.
 ***taskid:*** GME 녹음 서비스에서 생성한 녹음 작업 ID입니다. 각 녹음 작업에는 고유한 작업 ID가 있습니다.
 ***id:*** 녹음 작업을 위한 세그먼트의 일련 번호입니다. 초기 일련 번호는 0입니다.



## 통합 단계

<dx-steps>
-<dx-tag-link link="#StartRealTimeASR" tag="비즈니스">콘솔에서 녹음 서비스 구성 완료</dx-tag-link>
-<dx-tag-link link="#StartRealTimeASR" tag="비즈니스">서버 API를 호출하여 녹음 범위 정의</dx-tag-link>
-<dx-tag-link link="#callback" tag="비즈니스">녹음 작업 콜백 수신(선택 사항)</dx-tag-link> 
-<dx-tag-link link="#result" tag="비즈니스"> 녹음 파일 조회/관리</dx-tag-link>
</dx-steps>


### 1단계: 콘솔에서 녹음 서비스 구성 완료

[GME 콘솔](https://console.tencentcloud.com/gamegme)에 로그인하여 [서비스 관리] 메뉴로 들어가 녹음 서비스를 활성화할 애플리케이션의 [설정]을 클릭하여 애플리케이션 상세 페이지로 이동합니다.
- #### 녹음 서비스 활성화/비활성화

![](https://qcloudimg.tencent-cloud.cn/raw/4d72f57ae8f4463bc009d8ef8048232e.png)


페이지의 [음성 녹음 서비스]에서 **수정**을 클릭하고 녹음 스위치를 **ON**으로 설정합니다.

녹음 서비스를 처음 시작할 때 GME는 귀하의 **COS 서비스**에 액세스하기 위해 귀하에게 서비스 승인을 신청합니다. 팝업 창 페이지에서 권한 부여에 동의해주셔야 정상적으로 서버 녹음 서비스를 이용하실 수 있습니다.


![](https://qcloudimg.tencent-cloud.cn/raw/5e38302c5e3b0013ba53bd29af14fab2.png)

- #### 녹음 파일 저장 구성

**녹음 파일 버킷**에서 **바인딩**을 클릭합니다.
**스토리지 버킷 바인딩** 팝업 창에서 기존 COS 스토리지 버킷([COS 콘솔](https://console.tencentcloud.com/cos/bucket)에서 사전에 생성한 버킷)을 바인딩하거나 새로운 스토리지 버킷을 생성할 수 있습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/30faa09353cdd31c537803f72bca25b2.png)

- #### 녹음 이벤트 콜백 설정(선택 사항)
녹음 서비스의 이벤트 콜백을 받으려면 콜백 주소를 설정합니다. 작업 경로: 애플리케이션 세부 정보 페이지 이동 후 해당 페이지의 [음성 녹음 서비스] **수정**을 클릭하고, **콜백 주소**에서 **수정** 클릭한 후 팝업 창에 콜백을 받을 url 주소를 입력합니다. 현재 녹음 작업 완료 상태 이벤트 콜백 메시지만 푸시됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/cbc0275b887b6bd402f41f9f5c325a5b.png)

- #### 녹음 범위 구성
녹음 범위는 사용자 지정 녹음 또는 전체 녹음 중에서 선택할 수 있습니다. 사용자 지정 녹음을 선택해야 합니다. 그렇지 않으면 서버에서 관련 API를 호출할 수 없습니다.


상기 구성을 완료한 후 **저장**을 클릭하면 녹음 서비스가 시작됩니다. 더 이상 녹음 서비스를 사용할 필요가 없으면 예기치 않은 요금이 발생되지 않도록 콘솔에서 녹음 서비스 스위치를 **OFF**로 설정하십시오.



### 2단계: 녹음 작업 콜백 수신(선택 사항)

**1단계**에서 콜백 주소를 설정한 경우 녹음 작업 이벤트 콜백을 받을 수 있습니다.


### 3단계: 서버 API 호출 및 녹음 범위 정의
비즈니스 시나리오의 실제 요구 사항에 따라 관련 API를 호출합니다. 호출 순서 및 프로세스 설계 시 다음 사항에 주의하십시오.
- (1) 이미 존재하는 RoomId에만 녹화 시작 요청을 전송할 수 있습니다. RoomId가 없으면 녹음 작업이 생성되지 않습니다.
- (2) 직접 녹음 중지를 호출하지 않는 한 방에 사용자가 있으면 녹음 프로세스가 지속됩니다. 방에 있는 모든 사용자가 퇴장한 경우 기존 녹음 작업 프로세스는 12시간 동안 지속됩니다. 이 시간 동안 사용자가 방에 다시 입장하면 녹음이 자동으로 시작됩니다. 녹음 프로세스의 지속 시간이 끝난 후에 사용자가 방에 입장하면 녹음이 자동으로 시작되지 않습니다.



### 4단계: 녹음 파일 조회/관리

녹음 작업이 끝난 후 몇 분 안에 오디오 파일이 생성됩니다. [COS 콘솔](https://console.tencentcloud.com/cos/bucket)에 로그인하여 녹음된 파일을 조회 및 관리할 수 있습니다.







