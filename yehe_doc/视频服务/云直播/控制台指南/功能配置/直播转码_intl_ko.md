라이브 트랜스 코딩 기능(비디오 트랜스 코딩 및 오디오 트랜스 코딩 포함)은 라이브 스트리밍 사이트에서 푸시된 원본 스트림을 시청자에게 푸시하기 전에 클라우드에서 다양한 코덱, 해상도 및 비트 레이트의 스트림으로 변환하는 프로세스를 말합니다. 이는 서로 다른 장치의 다양한 네트워크 환경에서 재생 요구 사항을 충족합니다. 본 문서는 CSS 콘솔을 통해 트랜스 코딩 템플릿을 생성, 바인딩, 바인딩 해제, 수정 및 삭제하는 방법을 설명합니다.

**트랜스 코딩 템플릿을 생성하는 2가지 방법:**

- CSS 콘솔을 통해 트랜스 코딩 템플릿을 생성합니다. 자세한 작업 순서는 [표준 트랜스 코딩 템플릿 생성](#C_trans), [TSC 트랜스 코딩 템플릿 생성](#C_topspeed), [오디오 전용 트랜스 코딩 템플릿 생성](#C_audio)을 참고하십시오.
- API를 사용하여 라이브 채널용 트랜스 코딩 템플릿을 만듭니다. 구체적인 매개변수와 사례는 [CreateLiveTranscodeTemplate](https://www.tencentcloud.com/document/product/267/30790)을 참고하십시오.


## 참고 사항
- CSS는 표준 트랜스 코딩, TSC(Top Speed Codec) 트랜스 코딩 및 오디오 전용 트랜스 코딩을 지원합니다. 서비스를 사용하기 전에 과금 설명을 숙지하십시오.
   - 표준 트랜스 코딩: [표준 트랜스 코딩 패키지](https://www.tencentcloud.com/document/product/267/52220#standard_pag), [표준 트랜스 코딩 후불 과금 방식](https://intl.cloud.tencent.com/document/product/267/39604).
   - TSC 트랜스 코딩: [TSC 트랜스 코딩 패키지](https://www.tencentcloud.com/document/product/267/52220#topspeed_pag), [TSC 트랜스 코딩 후불 과금 방식](https://intl.cloud.tencent.com/document/product/267/39604).
- **표준 트랜스 코딩**과 비교할 때 **TSC 트랜스 코딩**은 낮은 비트 레이트에서 더 높은 비디오 품질을 제공합니다. 지능형 장면 인식, 동적 인코딩 및 CTU/라인/프레임 수준 비트 레이트 제어를 포함한 기술을 활용하는 TSC 트랜스 코딩을 통해, 낮은 비트 레이트(평균 50% 더 낮음)에서 고화질 스트리밍 서비스를 제공할 수 있습니다. 게임 스트리밍, 쇼룸 스트리밍, 이벤트 스트리밍 등에 널리 사용됩니다.
- 템플릿 생성 후 재생 도메인 이름으로 바인딩할 수 있습니다. 바인딩은 5 - 10분 후에 적용됩니다.
- 트랜스 코딩 템플릿을 바인딩한 후에는 해당 라이브 스트림 StreamName 뒤에 `_트랜스 코딩 템플릿 이름`을 추가하여 트랜스 코딩 스트림 주소를 생성할 수 있습니다. **트랜스 코딩 템플릿 이름**과 **StreamName** 접미사는 동일할 수 없습니다. 예를 들어, 트랜스 코딩 템플릿 이름이 `hd`인 경우, StreamName은 `test_a1_hd`일 수 없습니다. 그렇지 않으면 재생 중에 프로그램은 `test_a1`을 StreamName으로 인식하고 트랜스 코딩 템플릿 `hd`에 따라 스트림을 가져오므로 풀 스트림 예외가 발생할 수 있습니다.
- 트랜스 코딩된 스트림의 높이와 너비 또는 짧은 변과 긴 변을 지정한 경우, 이미지 왜곡을 방지하기 위해 원래 해상도를 가능한 한 설정된 값에 가깝게 유지합니다.
- 콘솔의 라이브 트랜스 코딩 페이지에서 템플릿이 바인딩된 도메인과 API를 통해 수행되는 더 세밀한 바인딩을 볼 수 있습니다. 여기에서 템플릿을 [바인딩 해제](#untie)할 수도 있습니다.
- 하나의 재생 도메인 이름을 **여러 트랜스 코딩 템플릿**과 바인딩하거나, 하나의 트랜스 코딩 템플릿을 **여러 재생 도메인 이름**과 바인딩할 수 있습니다.
- 최대 **50개**의 트랜스 코딩 템플릿을 생성할 수 있습니다.

[](id:create)
## 트랜스 코딩 템플릿 생성
[](id:C_trans)
### 표준 트랜스 코딩 템플릿 생성

1. CSS 콘솔에 로그인하여 **기능 설정** > [**라이브 트랜스 코딩**](https://console.cloud.tencent.com/live/config/transcode)을 선택합니다.
2. **트랜스 코딩 템플릿 생성**을 클릭하고 트랜스 코딩 유형으로 『**표준 트랜스 코딩**』을 선택하고 다음 구성을 완료합니다.
  - 기본 구성: 템플릿 이름, 비디오 비트 레이트, 비디오 해상도 등. 자세한 내용은 [표준 트랜스 코딩 기본 구성](#C_trans_normal)을 참고하십시오.
  - 고급 구성(선택 사항): **고급 구성**을 클릭하여 고급 설정을 표시합니다. 자세한 내용은 [표준 트랜스 코딩 고급 구성](#C_trans_high)을 참고하십시오.
3. 입력 환료 후, **저장**을 클릭합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/d67e6aa3cc7d5bc0ddfe6f47342b6a24.png)

<table id="C_trans_normal">
<tr><th width="20%">표준 트랜스 코딩 기본 구성</th><th>필수 입력 여부</th><th>설명</th></tr>
<tr>
<td>트랜스 코딩 유형</td>
<td>Yes</td>
<td><b>표준 트랜스 코딩</b>, TSC 트랜스 코딩 또는 오디오 전용 트랜스 코딩일 수 있는 트랜스 코딩 유형입니다.</td>
</tr><tr>
<td>템플릿 이름</td>
<td>Yes</td>
<td>라이브 트랜스 코딩 템플릿 이름은 1 - 10자의 문자 또는 숫자와 문자의 조합이어야 합니다.</td>
</tr><tr>
<td>템플릿 설명</td>
<td>No</td>
<td>중국어, 영어, 숫자, 언더바(_) 및 하이픈(-)만 포함할 수 있는 라이브 트랜스 코딩 템플릿 설명.</td>
</tr><tr>
<td>권장 매개변수</td>
<td>No</td>
<td><b>저화질, SD 또는 HD</b>를 선택할 수 있습니다. 화질을 선택하면 시스템이 자동으로 권장 비디오 비트 레이트와 높이를 입력하며 수정할 수 있습니다.</td>
</tr><tr>
<td>비디오 비트 레이트<br>(단위: Kbps)</td>
<td>Yes</td>
<td>평균 출력 비트 레이트, 출력값 범위: 101Kbps - 8000Kbps.<ul style="margin:0">
  <li>1000Kbps 보다 크지 않은 값은 100의 배수여야 합니다.</li>
  <li>1000Kbps 보다 큰 값은 500의 배수여야 합니다.</li></ul>
</td>
</tr><tr>
<td>비디오 해상도</td>
<td>Yes</td>
<td>기본값: <b>높이를 설정</b>합니다. <li>입력된 값은 트랜스 코딩된 비디오의 높이가 됩니다. <b>짧은 변 길이 설정</b>을 선택할 수도 있으며 입력한 값은 트랜스 코딩된 비디오의 짧은 변이 됩니다. <li>값 범위: 0px - 3000px. 값은 2의 배수여야 합니다. 다른 쪽은 자동 크기 조정됩니다.</td>
</tr><tr>
<td>DRM 암호화</td>
<td>No</td>
<td>이 기능을 활성화하려면 DRM 관리로 이동하여 DRM 키를 설정하십시오. HLS 재생 프로토콜에서 Widevine, Fairplay 및 NormalAES의 DRRM 암호화를 지원하며, Fairplay는 Apple에서 받은 인증서를 플레이어에 업로드해야 합니다.</td>
</tr></table>


<table id="C_trans_high">
<tr><th width="20%">표준 트랜스 코딩 고급 구성</th><th>필수 입력 여부</th><th>설명</th></tr>
<tr>
<td>코덱</td>
<td>No</td>
<td>기본적으로 원본 코덱이 사용됩니다. H.264, H.265 및 AV1을 선택할 수도 있습니다.</td>
</tr><tr>
<td>비디오 프레임 레이트(fps)</td>
<td>No</td>
<td>값 범위: 0fps - 60fps. 이 매개변수를 비워두면 기존 프레임 속도를 사용한다는 의미인 0fps가 적용됩니다.</td>
</tr><tr>
<td>GOP <br>(단위: s/초)</td>
<td>No</td>
<td>값 범위: 2초 - 6초. GOP가 클수록 지연 시간이 길어집니다. 이 매개변수를 비워두면 기본값이 사용됩니다.</td>
</tr><tr>
<td>매개변수 제한</td>
<td>No</td>
<td>기본적으로 비활성화되어 있으며 수동으로 활성화할 수 있습니다.<br>제한이 활성화된 후 원래보다 큰 값을 입력하면 입력 스트림의 기존 값이 사용됩니다. 이렇게 하면 높은 비디오 품질 설정을 사용하여 낮은 품질의 비디오를 트랜스 코딩할 때 발생하는 비디오 품질 문제를 피할 수 있습니다.</td>
</tr></table>

[](id:C_topspeed)

### TSC 트랜스 코딩 템플릿 생성
1. CSS 콘솔에 로그인하여 **기능 구성** > [**라이브 트랜스 코딩**](https://console.cloud.tencent.com/live/config/transcode)을 선택합니다.
2. **트랜스 코딩 템플릿 생성**을 클릭하고 트랜스 코딩 유형에 대해 『**TSC 트랜스 코딩**』을 선택하고 다음 구성을 완료합니다.
  - 기본 구성: 템플릿 이름, 비디오 비트 레이트, 비디오 해상도 등. 자세한 내용은 [TSC 트랜스 코딩 기본 구성](#C_topspeed_normal)을 참고하십시오.
  - 고급 구성(선택 사항): **고급 구성**을 클릭하여 고급 설정을 표시합니다. 자세한 내용은 [TSC 트랜스 코딩 고급 구성](#C_topspeed_high)을 참고하십시오.
3. **저장**을 클릭합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/54965fbb96dc3a1ac6c51793b579954a.png)

<table  id="C_topspeed_normal">
<tr><th width="20%">TSC 트랜스 코딩 기본 구성</th><th>필수 입력 여부</th><th>설명</th>
</tr><tr>
<td>트랜스 코딩 유형</td>
<td>Yes</td>
<td>표준 트랜스 코딩, <b>TSC 트랜스 코딩</b>또는 오디오 전용 트랜스 코딩일 수 있는 트랜스 코딩 유형입니다.</td>
</tr><tr>
<td>템플릿 이름</td>
<td>Yes</td>
<td>라이브 트랜스 코딩 템플릿 은 2 - 10자의 문자 또는 숫자와 문자의 조합이어야 합니다.</td>
</tr><tr>
<td>템플릿 설명</td>
<td>No</td>
<td>중국어, 영어, 숫자, 언더바(_) 및 하이픈(-)만 포함할 수 있는 라이브 트랜스 코딩 템플릿 설명.</td>
</tr><tr>
<td>권장 매개변수</td>
<td>No</td>
<td><b>LD, SD 또는 HD</b>를 선택할 수 있습니다. 화질을 선택하면 시스템이 자동으로 수정 가능한 권장 비디오 비트 레이트와 높이를 입력합니다.</td>
</tr><tr>
<td>비디오 비트 레이트<br>(단위: Kbps)</td>
<td>Yes</td>
<td>평균 출력 비트 레이트, 출력값 범위: 101Kbps - 8000Kbps. <li>1000Kbps 이내의 100의 배수여야 합니다. </li><li>1000Kbps 이상의 500의 배수여야 합니다. </li></td>
</tr><tr>
<td>비디오 해상도</td>
<td>Yes</td>
<td>기본값: <b>높이를 설정합니다</b>. <li>입력된 값은 트랜스 코딩된 비디오의 높이가 됩니다. <b>짧은 변 길이 설정</b>을 선택할 수도 있으며 입력한 값은 트랜스 코딩된 비디오의 짧은 변이 됩니다.</li><li>값 범위: 0px - 3000px. 값은 2의 배수여야 합니다. 다른 변은 자동 크기 조정됩니다.</li></td>
</tr>
</table>

<table  id="C_topspeed_high">
<tr><th width="20%">TSC 트랜스 코딩 고급 구성</th><th>필수 입력 여부</th><th>설명</th>
</tr><tr>
<td>코덱</td>
<td>No</td>
<td>기본 설정: 원본 코덱. H.264 또는 H.265를 선택할 수도 있습니다.</td>
</tr><tr>
<td>비디오 프레임 레이트(fps)</td>
<td>No</td>
<td>값 범위: 0fps - 60fps. 이 매개변수를 비워두면 0fps가 사용됩니다.</td>
</tr><tr>
<td>GOP <br>(단위: s/초)</td>
<td>No</td>
<td>값 범위: 2초 - 6초. GOP가 클수록 지연 시간이 길어집니다. 이 매개변수를 비워두면 기본값이 사용됩니다.</td>
</tr><tr>
<td>매개변수 제한</td>
<td>No</td>
<td><li/>기본적으로 비활성화되어 있으며 수동으로 활성화할 수 있습니다.<li/>제한이 활성화된 후 원래보다 큰 값을 입력하면 입력 스트림의 원래 값이 사용됩니다. 이렇게 하면 높은 비디오 품질 설정을 사용하여 낮은 품질의 비디오를 트랜스 코딩할 때 발생하는 비디오 품질 문제를 피할 수 있습니다.</td>
</tr></table>

[](id:C_audio)
### 오디오 전용 트랜스 코딩 템플릿 생성

1. CSS 콘솔에 로그인하고 **기능 설정** > [**라이브 트랜스 코딩**](https://console.cloud.tencent.com/live/config/transcode)을 선택합니다.
2. **트랜스 코딩 템플릿 생성**을 클릭하고 트랜스 코딩 유형으로 『**오디오 전용 트랜스 코딩**』을 선택한 후, [설정](#C_audio_normal)을 완료한 다음 **저장**을 클릭합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/6e51f4ba0d495176203d2a65a4a4dc57.png)

<table id="C_audio_normal">
<tr><th width="20%">오디오 전용 트랜스 코딩 기본 구성</th><th>필수 입력 여부</th><th>설명</th>
</tr><tr>
<td>트랜스 코딩 유형</td>
<td>Yes</td>
<td>표준 트랜스 코딩, TSC 트랜스 코딩, <strong>오디오 전용 트랜스 코딩</strong>일 수 있는 트랜스 코딩 유형입니다.</td>
</tr>
<tr>
<td>템플릿 이름</td>
<td>Yes</td>
<td>라이브 트랜스 코딩 템플릿 이름은 1 - 10자의 문자 또는 숫자와 문자의 조합이어야 합니다.</td>
</tr>
<tr>
<td>템플릿 설명</td>
<td>No</td>
<td>중국어, 영어, 숫자, 언더바(_) 및 하이픈(-)만 포함할 수 있는 라이브 트랜스 코딩 템플릿 설명.</td>
</tr>
<tr>
<td>오디오 비트 레이트(Kbps)</td>
<td>Yes</td>
<td><b>원본 오디오 비트 레이트</b>를 사용하거나 또는 <b>사용자 지정 비트 레이트</b>를 설정할 수 있습니다. 값 범위: 101kbps - 500kbps.</td>
</tr>
</tr><tr><td>DRM 암호화</td><td>No</td><td>이 기능을 활성화하려면 DRM 관리로 이동하여 DRM 키를 설정하십시오. HLS 재생 프로토콜에서 Widevine, Fairplay 및 NormalAES의 DRRM 암호화를 지원하며, Fairplay는 Apple에서 받은 인증서를 플레이어에 업로드해야 합니다.</td>
</tbody></table>

[](id:related)
## 도메인 이름 바인딩
1. CSS 콘솔에 로그인하고 **기능 설정** > [**라이브 트랜스 코딩**](https://console.cloud.tencent.com/live/config/transcode)을 선택합니다.
2. 다음 방법 중 하나로 도메인 이름 바인딩 페이지로 이동합니다.
  - **기존 템플릿에 도메인 바인딩:** 왼쪽 상단에서 **도메인 이름 바인딩**을 클릭합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/6e7b5d21d7211b08993ccd648c08ea39.png)
  - **트랜스 코딩 템플릿 생성 후 도메인 이름 바인딩**: [템플릿 생성](#create) 후 팝업 창에서 **도메인 이름 바인딩**을 클릭합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/e46853c98ef7a78b4758b5d516d2db22.png)
3. 도메인 이름 바인딩 창에서 **트랜스 코딩 템플릿**과 **재생 도메인 이름**을 선택한 후 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/19098af218a1e131310677e3fa4b6cd7.png)
>? **추가**를 클릭하여 여러 재생 도메인 이름을 템플릿에 바인딩할 수 있습니다.

[](id:untie)
## 도메인 이름 바인딩 해제
1. CSS 콘솔에 로그인하고 **기능 설정** > [**라이브 트랜스 코딩**](https://console.cloud.tencent.com/live/config/transcode)을 선택합니다.
2. 템플릿을 선택하고 타깃 도메인 이름을 찾은 다음 **바인딩 해제**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/06d982f8c5ce34375945196485dfee59.png)
3. 팝업 창에서 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/fcb7537e8ab238617920fd54347da6da.png)

[](id:modify)
## 템플릿 수정
1. CSS 콘솔에 로그인하고 **기능 설정** > [**라이브 트랜스 코딩**](https://console.cloud.tencent.com/live/config/transcode)을 선택합니다.
2. 타깃 트랜스 코딩 템플릿을 선택하고 오른쪽의 **편집**을 클릭하여 수정합니다.
3. 수정 후 **저장**을 클릭합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/995e1529ba890505c2db7ecc0788fac4.png)

[](id:delect)
## 템플릿 삭제
>!   템플릿이 도메인 이름으로 바인딩된 경우 템플릿을 삭제하기 전에 [바인딩 해제](#unite)해야 합니다. 

1. CSS 콘솔에 로그인하고 **기능 설정** > [**라이브 트랜스 코딩**](https://console.cloud.tencent.com/live/config/transcode)을 선택합니다.
2. 재생 도메인 이름과 연결되지 않은 템플릿을 선택하고 **삭제**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/201fbd96756e417eb01bc4c4162c3a3e.png)
3. 팝업 창에서 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e9062327d9cae6164254af7454c878de.png)

## 관련 작업
도메인 이름 **바인딩** 및 **바인딩 해제**에 대한 자세한 내용은 [트랜스 코딩 설정](https://intl.cloud.tencent.com/document/product/267/31062)을 참고하십시오.
