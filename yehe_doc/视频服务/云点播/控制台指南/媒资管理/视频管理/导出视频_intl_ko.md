VOD 콘솔을 통해 비디오 목록을 표시 필드를 사용자 정의하고 비디오 파일을 내보내기 할 수 있습니다. 본문에서는 목록 필드를 사용자 정의하고 비디오 파일을 내보내는 방법을 소개합니다.

## 사용자 정의 목록 필드


1. VOD 콘솔에 로그인하여 [미디어 자산 관리]>[[비디오 관리]](https://console.cloud.tencent.com/vod/media)를 선택하면 ‘업로드 완료’ 페이지로 이동합니다.
2. 목록 우측 상단의 ![](https://main.qcloudimg.com/raw/f4d3608e1d8319051883e90226a86f50.png) 클릭 후 표시해야 하는 목록 필드를 체크하고 [확인]을 클릭합니다. 최대 14개의 필드를 선택할 수 있습니다. 기본적으로 비디오 이름/ID 및 동작이 선택되어 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/473896085055dc9a382e363cec4db9dc.png)



## 비디오 파일 내보내기

1. VOD 콘솔에 로그인하여 [미디어 자산 관리]>[[비디오 관리]](https://console.cloud.tencent.com/vod/media)를 선택하고 기본적으로 ‘업로드 완료’ 페이지로 이동합니다. 사용자가 내보낼 미디어 자산을 선택한 후 선택한 미디어 자산 정보를 내보내기 합니다.
2. 목록 우측 상단의 ![](https://main.qcloudimg.com/raw/e530c6f8adeb603d98e1bc7e0ae8e255.png) 클릭 후, [내보내기 형식]과 [데이터 내보내기]를 선택하고 [확인]을 클릭합니다. 사용자가 선택하지 않으면 모든 VOD 미디어 정보를 내보내기 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c390702b9e17fb783cae7e8047873e22.png)
3. VOD는 CSV 및 JSONLINES 형식의 파일 내보내기를 지원하므로, 선택된 파일 정보 또는 모든 파일 정보를 내보내도록 선택할 수 있습니다.
 1. CSV 형식 파일은 문자 구분 값 파일입니다. 파일은 테이블 데이터를 일반 텍스트로 저장합니다. 파일 내용의 미리보기는 다음과 같습니다.
 ![](https://qcloudimg.tencent-cloud.cn/raw/858c2dac0136337f560d52833921ff00.png)
<table>
   <tr>
      <th width="120px" style="text-align:center">파일 형식</td>
      <th width="0px" style="text-align:center">필드 이름(다음 순서로 표시)</td>
   </tr>
   <tr>
      <td>CSV 형식</td>
      <td>미디어 파일 이름, 생성 시간, 업데이트 시간, 만료 시간, 미디어 파일 카테고리 ID, 미디어 파일 카테고리 이름, 미디어 파일 카테고리 경로, 커버 이미지 URL, 미디어 파일 소스, 미디어 파일 저장 공간, 미디어 파일 레이블, 라이브 방송 대상 녹화 파일(VID), 비디오 주소, 파일 ID, 파일 크기, 길이</td>
   </tr>
</table>
 2. JSONLINES 형식은 한 번에 하나의 레코드를 처리할 수 있는 구조화된 데이터를 저장하는 데 사용됩니다. 비디오에서 내보낸 JSONLINES 형식 파일에는 다음 필드가 포함됩니다.
 <table>
   <tr>
      <th width="120px" style="text-align:center">파일 형식</td>
      <th width="0px" style="text-align:center">필드 이름</td>
      <th width="0px"  style="text-align:center">설명</td>
   </tr>
   <tr>
      <td rowspan='12'>JSONLINES 형식</td>
      <td>BasicInfo</td>
      <td>기본 정보. 영상 이름, 카테고리, 재생 주소, 커버 이미지 등을 포함합니다.</td>
   </tr>
   <tr>
      <td>MetaData</td>
      <td>메타 정보. 크기, 길이, 비디오 스트림 정보, 오디오 스트림 정보 등을 포함합니다.</td>
   </tr>
   <tr>
      <td>TranscodeInfo</td>
      <td>결과 정보를 트랜스코딩합니다. 비디오 트랜스코딩에 의해 생성된 다양한 비트레이트로 비디오의 URL, 사양, 비트레이트, 해상도 등을 포함합니다.</td>
   </tr>
   <tr>
      <td>AnimatedGraphicsInfo</td>
      <td>애니메이션 이미지 결과 정보.</td>
   </tr>
   <tr>
      <td>SampleSnapshotInfo</td>
      <td>샘플 스냅샷 정보.</td>
   </tr>
   <tr>
      <td>ImageSpriteInfo</td>
      <td>스프라이트 이미지 정보.</td>
   </tr>
   <tr>
      <td>SnapshotByTimeOffsetInfo</td>
      <td>지정 시점의 스냅샷 정보.</td>
   </tr>
   <tr>
      <td>KeyFrameDescInfo</td>
      <td>비디오 키 프레임 정보.</td>
   </tr>
   <tr>
      <td>AdaptiveDynamicStreamingInfo</td>
      <td>어댑티브 다이나믹 스트리밍 정보.</td>
   </tr>
   <tr>
      <td>SubtitleInfo</td>
      <td>자막 정보.</td>
   </tr>
   <tr>
      <td>FileId</td>
      <td>미디어 파일의 고유 ID.</td>
   </tr>
</table>
