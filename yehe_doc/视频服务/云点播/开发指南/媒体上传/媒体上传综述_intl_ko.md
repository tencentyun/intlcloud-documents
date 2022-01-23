미디어 업로드란 비디오, 오디오, 커버 이미지 등의 미디어 파일을 VOD 스토리지에 업로드하여 추가적으로 처리 및 배포할 수 있도록 하는 기능입니다.

## 업로드 방식

VOD는 다음과 같은 업로드 방식을 지원합니다.

- [콘솔 로컬 업로드](https://console.cloud.tencent.com/vod/media/upload)
VOD 콘솔 업로드 페이지에서 로컬 미디어 파일을 VOD로 업로드합니다. 개발자가 직접 소량의 미디어를 관리하는 시나리오에 적용되며, 빠르고 간편하며 기술적 난이도가 높지 않아 접근하기 쉬운 장점이 있습니다.
- [콘솔 풀링 업로드](https://console.cloud.tencent.com/vod/media/upload)
VOD 콘솔 업로드 페이지에서 업로드 대기 중인 미디어의 URL을 지정하고 VOD 백그라운드에서 오프라인으로 풀링을 진행합니다.
- [서버로 업로드](https://intl.cloud.tencent.com/document/product/266/33912)
개발자가 해당 백그라운드 서버에 저장된 미디어 파일을 VOD로 업로드합니다. 자동화, 시스템화된 생산 환경에 적합합니다. VOD는 다음 프로그래밍 언어의 서버 업로드 SDK를 제공합니다.
    - [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)
    - [C# SDK](https://intl.cloud.tencent.com/document/product/266/33915)
    - [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916)
    - [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917)
    - [Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918)
    - [Golang SDK](https://intl.cloud.tencent.com/document/product/266/33919)
- [클라이언트 업로드](https://intl.cloud.tencent.com/document/product/266/33921)
단말 사용자가 클라이언트 로컬 비디오를 VOD에 업로드합니다. UGC, PGC 등의 시나리오에 적합합니다. VOD는 다음 플랫폼 클라이언트 업로드 SDK를 제공합니다.
    - [Android 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33925)
    - [iOS 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33926)
    - [Web 업로드 SDK](https://intl.cloud.tencent.com/document/product/266/33924)
- [API 풀링업로드](https://intl.cloud.tencent.com/document/product/266/34118)
VOD에서 제공하는 서버 API를 사용해 업로드 인터페이스를 풀링하고 업로드 예정 미디어의 URL을 지정하면 VOD 백그라운드에서 오프라인으로 풀링을 진행합니다. 대량 또는 자동화된 미디어 파일의 마이그레이션 시나리오에 적합합니다.
- [라이브 방송 녹화](https://intl.cloud.tencent.com/document/product/267/31563)
CSS 녹화 기능을 통해 라이브 방송 스트림의 비디오 콘텐츠를 VOD로 저장하여 보관, 편집 및 검토합니다.

## 스토리지 리전
[](id:Storage)
### 지원되는 리전 리스트

VOD는 전세계 여러 리전에 스토리지 노드가 있으며, 미디어 업로드 과정에서 그 중 한 리전을 선택해 저장합니다. VOD는 현재 다음의 스토리지 리전을 지원합니다.

<table>
    <tr>
        <th>
            스토리지 리전                
        </th>
        <th>
            리전 영문 약칭                
        </th>
    </tr>
    <tr>
        <td>
            베이징             
        </td>
        <td>
			ap-beijing
        </td>
    </tr>
    <tr>
        <td>
            상하이             
        </td>
        <td>
			ap-shanghai
        </td>
    </tr>
    <tr>
        <td>
            충칭             
        </td>
        <td>
			ap-chongqing
        </td>
    </tr>
    <tr>
        <td>
            톈진             
        </td>
        <td>
			ap-beijing-1
        </td>
    </tr>
    <tr>
        <td>
            중국홍콩             
        </td>
        <td>
			ap-hongkong
        </td>
    </tr>
    <tr>
        <td>
            싱가포르             
        </td>
        <td>
			ap-singapore
        </td>
    </tr>
    <tr>
        <td>
            인도 뭄바이             
        </td>
        <td>
			ap-mumbai
        </td>
    </tr>
    <tr>
        <td>
            한국 서울             
        </td>
        <td>
			ap-seoul
        </td>
    </tr>
    <tr>
        <td>
            태국 방콕             
        </td>
        <td>
			ap-bangkok
        </td>
    </tr>
    <tr>
        <td>
            일본 도쿄             
        </td>
        <td>
			ap-tokyo
        </td>
    </tr>
    <tr>
        <td>
            미국 실리콘밸리(미국 서부)            
        </td>
        <td>
			na-siliconvalley
        </td>
    </tr>
    <tr>
        <td>
            미국 버지니아 (미국 동부)             
        </td>
        <td>
			na-ashburn
        </td>
    </tr>
    <tr>
        <td>
            캐나다 토론토             
        </td>
        <td>
			na-toronto
        </td>
    </tr>
    <tr>
        <td>
            독일 프랑크푸르트             
        </td>
        <td>
			eu-frankfurt
        </td>
    </tr>
    <tr>
        <td>
            러시아 모스크바             
        </td>
        <td>
			eu-moscow
        </td>
    </tr>
</table>

### 스토리지 리전 활성화

여러 스토리지 리전을 활성화하는 주된 목적 중 하나는 미디어 업로드 품질 향상(성공률 및 속도)입니다. 업로더와 스토리지 노드의 거리는 업로드 품질에 영향을 주며, 일반적으로 거리가 가까울수록 업로드 품질이 좋습니다.

개발자가 VOD 서비스를 활성화하면 VOD는 자동으로 **싱가포르** 스토리지 리전을 할당합니다. 개발자는 비즈니스 니즈에 따라 다른 스토리지 리전을 활성화할 수 있습니다. 자세한 내용은 [업로드 스토리지 설정](https://intl.cloud.tencent.com/document/product/266/18874)을 참고하십시오. **스토리지 리전은 한번 활성화하면 비활성할 수 없습니다**.

### 기본 스토리지 리전

개발자가 보유한 스토리지 리전 중 하나만 기본 스토리지 리전으로 사용됩니다. 만약 개발자가 1개의 스토리지 리전(싱가포르)만 보유한 경우, 이것이 기본 스토리지 리전이 됩니다. 개발자가 여러 스토리지 리전을 활성화한 경우에는 콘솔에서 다른 리전을 기본 스토리지 리전으로 선택할 수 있습니다. 자세한 작업 방식은 [스토리지 리전 설정](https://intl.cloud.tencent.com/document/product/266/18874#.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F.E6.AD.A5.E9.AA.A4)을 참고하십시오.

기본 스토리지 리전의 기능: 일부 시나리오에서는 해당 리전이 우선적으로 미디어 업로드 타깃 리전으로 선택됩니다. 자세한 설명은 다음을 참고하십시오.

### 스토리지 리전 선택

미디어 업로드 시 하나의 스토리지 리전을 선택해야 합니다. 기본적으로 VOD 백그라운드에서 자동으로 선택하나 개발자가 업로드 요청에서 지정할 수도 있습니다.

- VOD 백그라운드에서 자동으로 스토리지 리전을 선택하는 경우.
  - 개발자가 1개의 스토리지 리전(싱가포르)만 보유한 경우, 모든 업로드 미디어가 해당 리전에 저장됩니다.
  - 개발자가 여러 스토리지 리전을 활성화한 경우, 각 업로드 방식에 대한 선택 정책은 다음과 같습니다.
 <table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th> 업로드 방식</th>
<th>리전 선택 정책</th>
</tr>
</thead>
<tbody>
<tr>
<td>콘솔 로컬 업로드</td>
<td >업로더와 가장 가까운 스토리지 리전 선택</td>
</tr>
<tr>
<td>콘솔 풀링 업로드</td>
<td>기본 스토리지 단지 고정 선택</td>
</tr>
<tr>
<td>서버로 업로드</td>
<td>업로더와 가장 가까운 스토리지 리전 선택</td>
</tr>
<tr>
<td>클라이언트 업로드</td>
<td>업로더와 가장 가까운 스토리지 리전 선택</td>
</tr>
<tr>
<td>API 풀링 업로드</td>
<td>기본 스토리지 단지 고정 선택</td>
</tr>
<tr>
<td>라이브 방송 녹화</td>
<td>라이브 방송 푸시 스트리밍 소재 리전과 가장 가까운 스토리지 리전 선택</td>
</tr>
</tbody></table>
- 개발자는 스토리지 리전을 지정할 때, 다음과 같은 방법으로 여러 업로드 방식을 지정할 수 있습니다.
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th> 업로드 방식</th>
<th>리전 지정 방법</th>
</tr>
</thead>
<tbody>
<tr>
<td>콘솔 로컬 업로드</td>
<td >미지원</td>
</tr>
<tr>
<td>콘솔 풀링 업로드</td>
<td>미지원</td>
</tr>
<tr>
<td>서버로 업로드</td>
<td><ul style="margin:0;"><li><a href="https://intl.cloud.tencent.com/document/product/266/33914">Java SDK</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">C# SDK</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">PHP SDK</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">Python SDK</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">Node.js SDK</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">Go SDK</a></li> </ul>  </td>
</tr>
<tr>
<td>클라이언트 업로드</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/33922">클라이언트 업로드 서명 매개변수</a></td>
</tr>
<tr>
<td>API 풀링 업로드</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/34118">업로드 인터페이스 StorageRegion 매개변수 풀링</a> </td>
</tr>
<tr>
<td>라이브 방송 녹화</td>
<td>미지원</td>
</tr>
</tbody></table>

## 기능 및 제한

### 미디어 유형

VOD는 다음 유형의 미디어 파일 업로드를 지원합니다.

- 비디오: WMV, RM, MOV, MPEG, MP4, 3GP, FLV, AVI, RMVB, TS, ASF, MPG, WEBM, MKV, M3U8, WM, ASX, RAM, MPE, VOB, DAT, MP4V, M4V, F4V, MXF, QT, OGG.
- 오디오: MP3, M4A, FLAC, OGG, WAV, RA, AAC, AMR.
- 커버 이미지: JPG, JPEG, PNG, GIF, BMP, TIFF, AI, CDR, EPS, TIF.

### 이벤트 공지

미디어 업로드가 완료되면 VOD 백그라운드가 해당 이벤트를 개발자에게 공지합니다. 이벤트 알림 원리는 [이벤트 알림](https://intl.cloud.tencent.com/document/product/266/33948)를, 설정 방법은 [이벤트 알림 설정](https://intl.cloud.tencent.com/document/product/266/14055)을 참고하십시오.
각 업로드 방식별 이벤트 공지 유형은 다음과 같습니다.

| 업로드 방식                                                                                                  | 이벤트 공지 유형                                       |
| --------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| <ul style="margin:0;"><li>콘솔 로컬 업로드</li><li>서버로 업로드</li><li>클라이언트 업로드</li><li>라이브 방송 녹화</li></ul> | [비디오 업로드 완료](https://intl.cloud.tencent.com/document/product/266/33950)         |
| <ul style="margin:0;"><li>콘솔 풀링 업로드</li><li>API 풀링 업로드  </li>                                      | [URL 풀링 비디오 업로드 완료](https://intl.cloud.tencent.com/document/product/266/33951) |

### 부속 기능

VOD 미디어 업로드는 미디어 자원 관리, 비디오 처리 및 이벤트 공지, 업로드 제어 등과 관련한 다양한 부속 기능을 제공합니다.

#### 미디어 자원 관리 관련

- 커버 첨부: 비디오를 업로드하면서 이미지 한 장을 함께 첨부할 수 있으며 해당 이미지는 VOD 미디어 자원 시스템에서 자동으로 해당 비디오의 커버로 설정됩니다.
- 만료 시간 지정: 업로드 시 해당 미디어 파일의 만료 시간을 지정하면 지정 시간이 되었을 때 VOD 백그라운드에서 해당 미디어 파일 및 그 부속 파일(예: 트랜스 코딩 파일, 캡처 등)을 자동으로 삭제합니다.
- 카테고리 지정: 업로드 후 해당 미디어 파일의 카테고리를 설정합니다.

각 업로드 방식의 지원 상황 및 사용 방법은 다음 표와 같습니다.

| 기능         | 콘솔 로컬 업로드                                               | 콘솔 풀링 업로드 | 서버로 업로드                                                   | 클라이언트 업로드                                                   | API 풀링 업로드                                                 | 라이브 방송 녹화                                                     |
| ------------ | ------------------------------------------------------------ | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 커버 첨부     | 미지원                                                                                        | 미지원         | <ul style="margin:0;"><li>[Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2) | <ul style="margin:0;"><li> [Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926)</li> | [업로드 인터페이스 CoverUrl 매개변수 풀링](https://intl.cloud.tencent.com/document/product/266/34118) | 미지원                                                       |
| 만료 시간 지정 | 미지원                                                    | 미지원         | <ul style="margin:0;"><li>[Java SDK 인터페이스 ExpireTime 매개변수](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDK 인터페이스 ExpireTime 매개변수](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[PHP SDK 인터페이스 ExpireTime 매개변수](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Python SDK 인터페이스 ExpireTime 매개변수](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Node.js SDK 인터페이스 ExpireTime 매개변수](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Go SDK 인터페이스 ExpireTime 매개변수](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) | 미지원 | [업로드 인터페이스 ExpireTime 매개변수 풀링](https://intl.cloud.tencent.com/document/product/266/34118) | [녹화 설정](https://intl.cloud.tencent.com/document/product/267/34223) |
| 카테고리 지정     | [카테고리 지정](https://intl.cloud.tencent.com/document/product/266/33890) | 미지원         | <ul style="margin:0;"><li> [Java SDK 인터페이스 ClassId 매개변수](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDK 인터페이스 ClassId 매개변수](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[PHP SDK 인터페이스 ClassId 매개변수](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Python SDK 인터페이스 ClassId 매개변수](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Node.js SDK 인터페이스 ClassId 매개변수](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Go SDK 인터페이스 ClassId 매개변수](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) | [클라이언트 업로드 서명 classId 매개변수](https://intl.cloud.tencent.com/document/product/266/33922) | [업로드 인터페이스 ClassId 매개변수 풀링](https://intl.cloud.tencent.com/document/product/266/34118) | 미지원                                  |

#### 비디오 처리 및 이벤트 공지 관련

- 자동 비디오 처리: 미디어를 업로드하는 동시에 [태스크 플로우](https://intl.cloud.tencent.com/document/product/266/33931)를 지정하면 업로드가 완료된 후 VOD가 자동으로 해당 태스크 플로우를 실행합니다. 일반적인 시나리오에서는 비디오 첫 프레임 이미지를 절취하여 커버, 트랜스 코딩 및 콘텐츠 스마트 인식 등에 사용합니다.
- 비디오 처리 이벤트 공지 통과 필드: 자동 비디오 처리를 활성화하면 처리 완료 후 VOD 백그라운드에서 이벤트 공지 전송 시 해당 필드를 개발자에게 전송합니다.
- 업로드 이벤트 공지 통과 필드: 업로드가 완료되면 VOD 백그라운드가 이벤트 공지 전송 시 해당 필드를 개발자에게 전송합니다.

각 업로드 방식의 지원 상황 및 사용 방법은 다음 표와 같습니다.

| 기능                     | 콘솔 로컬 업로드                                                                                              | 콘솔 풀링 업로드 | 서버로 업로드                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | 클라이언트 업로드                                                                                                                                                   | API 풀링 업로드                                                    | 라이브 방송 녹화 |
| ------------------------ | ----------------------------------------------------------------------------------------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------- | -------- |
| 자동 비디오 처리             | [업로드 후 자동 비디오 처리](https://intl.cloud.tencent.com/document/product/266/33890) | 미지원         | <ul style="margin:0;"><li>[Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)                                                                                                                                             | [클라이언트 업로드 서명 procedure 매개변수](https://intl.cloud.tencent.com/document/product/266/33922)     | [인터페이스 Procedure 매개변수 풀링 업로드](https://intl.cloud.tencent.com/document/product/266/34118)      | 미지원   |
| 비디오 처리 이벤트 알림 통과 필드 | 미지원                                                                                                      | 미지원         | 미지원                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | 클라이언트 업로드 서명 sessionContext 매개변수                                                                                                                           | [인터페이스 SessionContext 매개변수 풀링 업로드](https://intl.cloud.tencent.com/document/product/266/34118) | 미지원   |
| 업로드 이벤트 알림 통과 필드     | 미지원                                                                                                      | 미지원         | <ul style="margin:0;"><li>[Java SDK 인터페이스 SourceContext 매개변수](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDK 인터페이스 SourceContext 매개변수](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[PHP SDK 인터페이스 SourceContext 매개변수](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Python SDK 인터페이스 SourceContext 매개변수](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Node.js SDK 인터페이스 SourceContext 매개변수](https://cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[Go SDK 인터페이스 SourceContext 매개변수](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) | [클라이언트 업로드 서명 sourceContext 매개변수](https://intl.cloud.tencent.com/document/product/266/33922) | 미지원                                                          | 미지원   |

#### 업로드 제어 관련

- 중단 지점부터 업로드 재개: 업로드가 예기치 않게 중단되어(예: 네트워크 연결 끊김, 브라우저 종료 등) 동일한 파일을 다시 업로드 하는 경우, 중단된 지점부터 이어서 업로드가 재개되어 파일 전체를 다시 업로드하지 않아도 됩니다.
- 업로드 일시 정지/재개: 업로드 중에 사용자는 스스로 업로드를 일시 정지 및 재개할 수 있습니다.
- 업로드 취소: 업로드 중에 사용자는 스스로 해당 업로드를 중단할 수 있습니다.
- 업로드 진행률 가져오기: VOD에 업로드된 미디어 파일의 크기 비율을 확인할 수 있습니다.
- 멀티파트 업로드: 업로드 시 미디어 파일을 여러 개의 작은 멀티 파트로 나누어 업로드합니다. 이를 통해 약한 네트워크 환경에서 네트워크 오류로 인한 업로드 중단을 줄일 수 있고, 높은 대역폭 환경에서 네트워크 대역폭을 최대한 활용하여 여러 멀티파트를 동시에 업로드할 수 있습니다.

각 업로드 방식의 지원 상황 및 사용 방법은 다음 표와 같습니다.

| 기능           | 콘솔 로컬 업로드       | 콘솔 풀링 업로드 | 서버로 업로드                                                   | 클라이언트 업로드                                                   | API 풀링 업로드 | 라이브 방송 녹화                                                     |
| -------------- | -------------------- | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------ | ------------------------------------------------------------ |
| 중단 지점부터 업로드 재개       | 미지원               | N/A         | 미지원                                                       | <ul style="margin:0;"><li>[Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926)</li> | N/A       | N/A                                                       |
| 업로드 일시 정지 및 재개 | 미지원               | N/A         | 미지원                                                       | <ul style="margin:0;"><li>[Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li> | N/A       | N/A                                                       |
| 업로드 취소       | 브라우저 페이지 새로고침 또는 종료 | N/A         | 미지원                                                       | <ul style="margin:0;"><li>[Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li> | N/A       | [녹화 작업 중단](https://intl.cloud.tencent.com/document/product/267/30837) |
| 업로드 진행률 가져오기   | 페이지 기본 진행률 표시     | 미지원         | 미지원                                                       | <ul style="margin:0;"><li>[Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926)</li> | 미지원       | N/A                                                        |
| 멀티파트 업로드       | 활성화               | N/A          | <ul style="margin:0;"><li> [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0)</li><li>[PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0)</li><li>[Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0)</li><li>[Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918)</li><li>[Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0) | <ul style="margin:0;"><li> Web SDK 기본 활성화</li><li>Android SDK 기본 활성화</li><li>iOS SDK 기본 활성화</li> | N/A       | N/A                                                       |

### 제한

- 미디어 파일 크기 제한은 다음과 같습니다.
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th> 업로드 방식</th>
<th>미디어 크기 제한</th>
</tr>
</thead>
<tbody>
<tr>
<td><ul style="margin:0;"><li>콘솔 로컬 업로드</li><li>클라이언트 업로드 - Web SDK</td>
<td >60GB</td>
</tr>
<tr>
<td><ul style="margin:0;"><li>서버로 업로드</li><li>콘솔 풀링 업로드</li><li> API 풀링 업로드</td>
<td>48.82TB（50,000GB）</td>
</tr>
<tr>
<td><ul style="margin:0;"><li>클라이언트 업로드 - Android SDK</li><li>클라이언트 업로드 - iOS SDK </td>
<td>10GB </td>
</tr>
<tr>
<td>라이브 방송 녹화</td>
<td><ul style="margin:0;"><li>MP4/FLV 포맷은 48.82TB(50,000GB)</li><li>HLS 포맷 전체 크기 제한 없음</li><li> 기타 제한 사항은<a href="https://intl.cloud.tencent.com/document/product/267/31563">라이브 방송 녹화</a>를 따름</td>
</tr>
</tbody></table>
- 파일 수량: 제한 없음.

