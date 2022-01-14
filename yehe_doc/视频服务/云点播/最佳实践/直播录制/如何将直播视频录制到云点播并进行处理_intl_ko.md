라이브 레코딩은 원본 스트림(오디오/비디오 데이터, 타임스탬프 및 기타 정보 수정 없이)에서 리먹싱된 파일을 VOD로 저장한 후, 녹화된 파일을 처리, 배포, 재생하는 솔루션입니다. 자세한 내용은 [라이브 방송 녹화 솔루션](https://intl.cloud.tencent.com/document/product/1082)을 참고하십시오.

## 제품 특징
- CSS의 기능을 기반으로 라이브 스트리밍 콘텐츠를 VOD 플랫폼에 빠르게 녹화 및 저장하여 2차 제작 및 배포를 진행합니다.
- 오디오 및 비디오 분야에서 Tencent Cloud의 선도적인 AI 기술과 전 세계적으로 배포된 캐시 노드를 기반으로 전문적이고 안정적인 라이브 푸시, 트랜스코딩, 배포 그리고 초저지연, 초고화질, 초고성능에 대한 요구 사항을 완벽하게 충족하는 재생을 통해 대량의 동시 요청을 지원합니다.
- 라이브 스트리밍 이벤트를 다양한 시나리오와 애플리케이션에 빠르게 배포할 수 있습니다.
- 기업 라이브 스트리밍, 라이브 커머스 및 교육용 라이브 스트리밍과 같은 다양한 산업별 시나리오에 적합합니다. Tencent Video와 같은 많은 채널을 통해 동영상 콘텐츠를 배포할 수 있습니다.

## 전제 조건
- Tencent Cloud 계정에 [가입](https://intl.cloud.tencent.com/register) 및 [로그인](https://intl.cloud.tencent.com/login)하고, 실명 인증을 완료해야 합니다. 실명 인증되지 않은 사용자는 중국 본토의 라이브 레코딩 VOD 전환 인스턴스를 구매할 수 없습니다.
- Tencent Cloud CSS 및 VOD 서비스가 활성화되어 있어야 합니다. 서비스가 활성화되어 있지 않은 경우 [CSS 서비스](https://console.cloud.tencent.com/live/livestat)와 [VOD 서비스](https://console.cloud.tencent.com/vod/overview)를 통해 서비스를 활성화하십시오.

## 실행 순서
### 1단계: 녹화 템플릿 생성
라이브 레코딩 기능을 사용하려면 먼저 녹화 템플릿을 만들어야 합니다. 라이브 레코딩 설정은 녹화 템플릿에 저장됩니다. 다양한 구성으로 녹화 템플릿을 생성하여 다양한 녹화 파일 형식 및 길이 등의 효과를 얻을 수 있습니다.
- **콘솔에서 생성**:
   1. [CSS 콘솔](https://console.cloud.tencent.com/live/config/record)에 로그인하고 **기능 설정**> [**라이브 레코딩**](https://console.cloud.tencent.com/live/config/record)을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2c70d96915ff91297434a1415aea49d0.png)

   2. **녹화 템플릿 생성**을 클릭하고 원하는 녹화 파일 형식을 선택합니다(하나 이상 선택). 구성 항목에 대한 자세한 내용은 [녹화 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/34223)을 참고하십시오.
	![](https://qcloudimg.tencent-cloud.cn/raw/af659794c5324cec4ed060377d74f04b.png)
		
   3. **저장**을 클릭하여 템플릿 생성을 완료합니다.
- **API를 통해 생성**:
[CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845)을 호출하여 녹화 템플릿을 생성할 수 있습니다. 템플릿이 성공적으로 생성되면 해당 템플릿 ID가 반환됩니다.

### 2단계: 녹화 방식 선택
CSS는 다양한 시나리오에서 라이브 레코딩 기능을 호출하기 위해 다음과 같은 체계를 제공합니다.

#### 방안1: 지정 도메인명 글로벌 레코딩
[CSS 콘솔](https://console.cloud.tencent.com/live/config/record) 또는 API 호출을 통해 라이브 녹화 템플릿을 푸시 도메인에 바인딩할 수 있으며 도메인을 통해 푸시된 스트림은 자동으로 녹화됩니다.

- **적용 시나리오**: 라이브 스트리밍, 라이브 커머스, 온라인 강의실 및 동영상 모니터링 등 전체 레코딩 시나리오.
- **작업 단계**:
	1. 녹화 템플릿 생성 후 [도메인 바인딩](https://console.cloud.tencent.com/live/config/record) 팝업창이 나타납니다. **도메인 바인딩**을 클릭하고 푸시 도메인을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5286148ae522898575744fe54b16938a.png)

   2. [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage에서 [라이브 푸시 도메인](https://console.cloud.tencent.com/live/domainmanage)을 클릭하여 푸시 세부 정보 페이지로 들어갑니다. **템플릿 구성**>**녹화 구성**을 선택하고 **편집**을 클릭하여 푸시 도메인 이름을 바인딩합니다. 자세한 내용은 [녹화 템플릿 바인딩](https://intl.cloud.tencent.com/document/product/267/34224)을 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/c74c5d420b6ed296859532e887541e7c.png)

   3. [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846) API를 통해 녹화 템플릿의 템플릿 ID와 푸시 도메인을 전달합니다.

#### 방안2: 지정된 스트림 녹화
녹화용 API를 통해 라이브 녹화 템플릿을 지정된 라이브 스트림에 바인딩할 수 있습니다.

- **적용 시나리오**: 이벤트 라이브 스트리밍, 전시 라이브 스트리밍, 스포츠 라이브 스트리밍 및 공동 앵커링을 통한 라이브 스트리밍.
- **작업 과정**: 녹화 템플릿의 템플릿 ID와 대상 도메인, 경로 및 StreamName을 전달하여 [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846) API를 통해 녹화 규칙을 생성할 수 있습니다(정확한 일치 필요). 이렇게 하면 녹화 템플릿을 지정된 라이브 스트림에 바인딩할 수 있습니다.

#### 방안3: 지정된 기간 녹화
API 호출을 통해 시작 시간과 종료 시간을 설정하여 지정된 시간 내에 녹화 작업을 시작할 수 있습니다.

- **적용 시나리오**: 뉴스 라이브 스트리밍 및 이벤트 라이브 스트리밍.
- **작업 과정**: 녹화 템플릿의 템플릿 ID와 대상 도메인, 경로, StreamName(정확히 일치해야 함), 녹화 시작 시간 및 종료 시간을 전달하여 [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API를 통해 녹화 작업을 생성할 수 있습니다.
- **녹화 예시**:
 1. 가장 간단한 상황입니다. 지정된 StreamName, DomainName, AppName, EndTime 매개변수만 입력하면 됩니다.
예: 2020년 08월 10일 오전 8시부터 10시까지 진행되는 녹화 작업, 형식은 FLV, 동영상 녹화, 분할 간격 30분, 영구 저장.
입력 예시:
```
https://live.tencentcloudapi.com/?Action=CreateRecordTask&AppName=live&DomainName=mytest.live.push.com&StreamName=livetest&StartTime=1597017600&EndTime=1597024800&TemplateId=0&<공통 요청 매개변수>
```
 2. 녹화 포맷, 녹화 유형 및 저장 매개변수 등을 구체적으로 지정할 수 있습니다.
예: 2020년 08월 10일 오전 8시부터 10시까지 진행되는 녹화 작업, 형식은 MP4, 분할 간격 1시간, 영구 저장.
 3. [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845)을 호출하여 먼저 템플릿을 생성합니다.
 입력 예시:
 ```
 https://live.tencentcloudapi.com/?Action=CreateLiveRecordTemplate&TemplateName=templat&Description=test&Mp4Param.Enable=1&Mp4Param.RecordInterval=3600&Mp4Param.StorageTime=0&<공통 요청 매개변수>
 ```
 출력 예시:
 ```
 {"Response": {"RequestId": "839d12da-95a9-43b2-a9a0-03366d01b532","TemplateId": 17016}}
 ```
 4. [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)를 호출하여 녹화 작업을 생성합니다.
 입력 예시:
 ```
 https://live.tencentcloudapi.com/?Action=CreateRecordTask&StreamName=livetest&AppName=live&DomainName=mytest.live.push.com&StartTime=1597017600&EndTime=1597024800&TemplateId=17016&<공통 요청 매개변수>
 ```

#### 방안4: 하이라이트 녹화(혼합 스트림 기반 녹화 지원)
라이브 스트리밍의 하이라이트 순간을 API 호출을 통해 라이브 레코딩할 수 있습니다.

- **적용 시나리오**: 스포츠 라이브 스트리밍 및 게임 라이브 스트리밍과 같이 세그먼트만 녹화(또는 글로벌 녹화 후 클리핑)해야 하는 시나리오.
- **작업 단계**: 녹화 템플릿의 템플릿 ID와 대상 도메인, 경로, StreamName(정확히 일치해야 함) 및 녹화 종료 시간을 전달하여 [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API를 통해 녹화 작업을 생성할 수 있습니다.
- **녹화 예시**:
 ```
 https://live.tencentcloudapi.com/?Action=CreateRecordTask&StreamName=test&AppName=live&DomainName=mytest.live.push.com&EndTime=1597024800&<공통 요청 매개변수>
 ```

#### 방안5: 퓨어 오디오 녹화
푸시 스트리밍이 퓨어 오디오일 경우, AAC를 퓨어 오디오 레코딩으로 설정할 수 있습니다.

- **적용 시나리오**: 오디오 라이브 스트리밍 및 오디오 마이크 연결.
- **작업 단계**: 녹화 파일 형식으로 .ACC 형식을 선택하고 녹화 템플릿을 만들 때 해당 푸시 주소를 바인딩할 수 있습니다.
>!바인딩 규칙은 생성 후 약 5 - 10분 후에 적용됩니다. 바인딩 규칙의 변경 사항은 푸시 중인 라이브 스트림에 영향을 미치지 않으며 새 라이브 스트림에만 적용됩니다.

### 3단계: 실시간 스트림 푸시
[2단계](#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E9.80.89.E6.8B.A9.E5.BD.95.E5.88.B6.E6.96.B9.E6.A1.88)에서 설명한 대로 푸시 도메인으로 녹화 템플릿을 바인딩한 후 푸시 주소에서 해당 푸시 도메인을 생성하고 [라이브 푸시](https://intl.cloud.tencent.com/document/product/267/31558)를 시작합니다.

라이브 스트리밍 종료 후 녹화 파일은 [VOD](https://console.cloud.tencent.com/vod/overview) 플랫폼에 저장됩니다.

>?
>- 녹화 템플릿에서 서브 애플리케이션에 녹화를 선택한 경우 녹화 파일은 해당 서브 애플리케이션에 저장됩니다.
>- 녹화 파일의 주소 정보를 콜백하려면 푸시 전에 콜백 템플릿을 생성하고 녹화 콜백 주소를 입력하여 저장하고 대상 푸시 도메인 이름을 바인딩해야 합니다. 자세한 내용은 [녹화 이벤트 알림](https://intl.cloud.tencent.com/document/product/267/38082)을 참고하십시오.

### 4단계: 녹화 파일 가져오기
다음을 통해 녹화 파일을 조회하고 가져올 수 있습니다.
- **녹화 콜백을 통해 가져오기**: 라이브 스트림을 푸시하기 전에 콜백 템플릿을 구성해야 합니다(템플릿에는 [녹화 콜백 주소 설정](https://console.cloud.tencent.com/live/config/callback)필요). 파일은 녹화 파일이 생성되면 콜백을 통해 콜백 서버로 전송됩니다. 자세한 내용은 [녹화 이벤트 알림](https://intl.cloud.tencent.com/document/product/267/38082)을 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/137836f99132f0619ca4ccb6ca128fed.png)
- **VOD 콘솔**: VOD 콘솔에서 녹화 파일을 조회할 수 있습니다. 자세한 내용은 [비디오 보기](https://intl.cloud.tencent.com/document/product/266/33895)를 참고하십시오.
- **VOD API를 통해 가져오기**: [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179) API를 호출하여 파일을 조회할 수 있습니다.

### 5단계: 녹화 파일 처리
#### 방안1: 라이브 레코딩 + 자동 트랜스코딩 + 동영상 재생 가속
- **적용 시나리오**: 실시간 스트림의 녹화 파일을 즉시 트랜스코딩하고 시청자가 요청 시 재생할 수 있도록 자동으로 가속화할 수 있습니다. 이는 비디오 처리가 필요하지 않은 대부분의 라이브 스트리밍 시나리오에 적합합니다.
- **작업 단계**:
	1. 라이브 스트리밍을 녹화하기 전에 녹화 템플릿을 만들고 **고급 설정**을 클릭하여 태스크 플로우를 설정합니다.
	![](https://qcloudimg.tencent-cloud.cn/raw/643aa06605824bab31016d95a5607099.png)
	2. VOD 콘솔에서 생성된 태스크 플로우 템플릿을 미리 바인딩합니다.
	![](https://qcloudimg.tencent-cloud.cn/raw/f2c1fdb36cee77be20e9fa366b1994ca.png)
	3. 고객이 라이브 스트리밍을 진행하는 경우, 자세한 내용은 [라이브 방송 푸시 스트림](https://intl.cloud.tencent.com/document/product/267/31558)을 참고하십시오.
	4. 라이브 레코딩이 완료된 후 VOD FileId를 가져옵니다.
	![](https://qcloudimg.tencent-cloud.cn/raw/8a70ec2190bde5eb95401ad27b71f9fa.png)
	5. 재생할 재생 주소를 가져옵니다.

#### 방안2: 라이브 레코딩 + 수동 트랜스코딩 + 동영상 재생 가속
- **적용 시나리오**: 라이브 스트림의 녹화 파일을 바로 트랜스코딩하지 않고 VOD로 저장하고 싶다면 다른 작업을 추가하지 않고 녹화 작업을 생성할 수 있습니다. 나중에 동영상을 트랜스코딩하려면 트랜스코딩 작업을 수동으로 트리거하고 온클라우드 클리핑 기능을 함께 사용하여 더 나은 결과를 얻을 수 있습니다.

- **작업 단계**:
	1. 고객이 라이브 스트리밍을 진행하는 경우, 자세한 내용은 [라이브 방송 푸시 스트림](https://intl.cloud.tencent.com/document/product/267/31558)을 참고하십시오.
	2. 파일이 자동으로 녹화됩니다.
	3. VOD FileId를 가져옵니다.
	4. 트랜스코딩 템플릿을 설정하거나 수동으로 태스크 플로우를 트랜스코딩합니다. 자세한 내용은 [템플릿 설정](https://intl.cloud.tencent.com/document/product/266/14059)을 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/fef42635495040b17e98868ad9cd911a.png)
	5. 2차 동영상 편집을 선택할 수 있습니다.
	6. 트랜스코딩 및 처리가 완료된 후 후속 재생을 위한 동영상 주소를 가져옵니다.

#### 방안3: 라이브 레코딩 + 어댑티브 비트레이트 스트리밍 + 동영상 전송 가속 + Superplayer

- **적용 시나리오**: HLS 암호화를 통해 충족할 수 없는 높은 보안 요구 사항이 있는 경우, 어댑티브 및 Superplayer를 함께 사용하여 비디오 보안을 더욱 강화할 수 있습니다. 온라인 교육 및 기업 교육에 매우 적합합니다.

- **작업 단계**:
	1. 고객이 라이브 스트리밍을 진행하는 경우, 자세한 내용은 [라이브 방송 푸시 스트림](https://intl.cloud.tencent.com/document/product/267/31558)을 참고하십시오.
	2. 파일이 자동으로 녹화됩니다.
	3. VOD FileId를 가져옵니다.
	4. 어댑티브 비트 레이트 스트리밍을 수행하도록 트랜스코딩 템플릿 또는 태스크 플로우를 구성합니다. 자세한 내용은 [태스크 플로우 설정](https://intl.cloud.tencent.com/document/product/266/14058)을 참고하십시오.
	![](https://qcloudimg.tencent-cloud.cn/raw/461b55df5d688b52d94210f173368ddc.png)
	5. Superplayer 구성을 설정하고 재생을 위해 생성된 어댑티브 비트 스트림을 선택합니다.
		![](https://qcloudimg.tencent-cloud.cn/raw/4fe2cb6836caad6861798bc38cde60cd.png)
	6. FileId를 통해 동영상을 재생합니다.

