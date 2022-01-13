
Superplayer는 VOD에서 제공하는 플레이어 기능으로, 어댑티브 비트레이트 스트리밍, 스프라이트 이미지를 썸네일로 지정하고 관련 구성 항목을 통해 정의할 수 있습니다. 콘솔에서 미리보기도 지원합니다. 자세한 내용은 [Superplayer 미리보기](https://intl.cloud.tencent.com/document/product/266/33896#.E8.B6.85.E7.BA.A7.E6.92.AD.E6.94.BE.E5.99.A8.E9.A2.84.E8.A7.88 )를 참고하십시오.
>!VOD의 기본 템플릿만 도메인 이름에 대한 Key 링크 도용 방지를 활성화할 필요가 없으며, 보안을 위해 다른 템플릿은 Key 링크 도용 방지가 활성화된 후에만 적용할 수 있습니다. Key 링크 도용 방지를 설정하지 않은 경우 [도메인 관리](https://console.cloud.tencent.com/vod/distribute-play/domain)를 클릭하여 활성화합니다.


## 사전 설정 구성
VOD는 편의를 위해 다음 두 가지 사전 설정 구성을 제공합니다.

<table class="table auto-table"><tbody><tr><th rowspan="2">설정명</td><th colspan="3">설정 항목</td></tr>
<tr><th>재생할 어댑티브 비트레이트 스트리밍(템플릿 ID)</td><th>사용할 스프라이트 이미지(템플릿 ID)</td><th>서브스트림 이름 규칙(서브스트림 짧은 변의 길이 기준)</td></tr>
<tr><td>default</td><td>10</td><td>10</td><td rowspan="2"><ul style="margin:0;"><li >240px: LD</li><li>480px: SD</li><li>720px: HD</li><li>1080px: FHD</li><li>1440px: 2K</li><li>2160px: 4K</li><li>기타:<code>xx</code>p(<code>xx</code>는 영상의 짧은 변의 길이를 나타냄)</li></td></tr>
<tr><td>basicDrmPreset</td><td>12</td><td>10</td>
</tbody></table>


## 사용자 정의 구성

콘솔에 로그인하고 [배포 및 재생 설정]>[[Superplayer 설정]](https://console.cloud.tencent.com/vod/distribute-play/super-player)을 선택하고 [생성]을 클릭합니다.
1. 재생 구성 이름을 입력합니다(**숫자**와 **영어**만 지원됨).
2. 재생 구성 설명을 입력합니다(최대 15자).
3. **재생을 위해 어댑티브 비트레이트 스트리밍 템플릿**에서 사전 설정 또는 이전에 만든 사용자 정의 템플릿을 선택합니다.
>?이 구성 항목은 플레이어에서 재생할 수 있는 비디오 파일이 트랜스코딩되는 어댑티브 비트레이트 스트리밍 템플릿을 지정합니다. 예를 들어 재생 구성에서 어댑티브 비트레이트 스트리밍 템플릿 10이 선택되면 플레이어는 이 템플릿을 통해 트랜스코딩된 비디오만 재생할 수 있습니다.
4. **썸네일 미리보기를 위해 스프라이트 이미지 템플릿**에서 사전 설정 또는 이전에 생성된 사용자 정의 스프라이트 이미지 템플릿을 선택합니다.
>?이 구성 항목은 플레이어의 썸네일 미리보기를 위한 스프라이트 이미지 파일을 지정합니다. 예를 들어 재생 구성에서 SpriteScreenShot10 템플릿을 선택한 경우 SpriteScreenShot10 템플릿을 통해 캡처한 스프라이트 이미지만 플레이어에서 미리 볼 수 있습니다.
5. **플레이어가 서브스트림을 재생하는 데 사용되는 이름**에서 플레이어에 대한 다양한 해상도의 서브스트림 이름을 지정합니다. 이 구성 항목을 비워두면 기본값이 사용됩니다. 비디오의 짧은 변 길이와 해상도를 사용자 정의할 수 있습니다.
6. [확인]을 클릭하고 생성을 완료합니다.

구성이 성공적으로 생성되면 Superplayer 구성 목록에 표시됩니다. [Superplayer 미리보기](https://intl.cloud.tencent.com/document/product/266/33896#.E8.B6.85.E7.BA.A7.E6.92.AD.E6.94.BE.E5.99.A8.E9.A2.84.E8.A7.88 ) 문서를 참고하여 해당 구성을 미리보기할 수 있습니다.


