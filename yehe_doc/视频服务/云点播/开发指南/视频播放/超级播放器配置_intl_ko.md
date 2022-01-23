Superplayer를 사용하여 비디오를 재생할 때, 비디오 **이미지 콘텐츠**는 [어댑티브 비트레이트 스트리밍](https://intl.cloud.tencent.com/document/product/266/33942) 출력이며, **썸네일** 미리 보기는 [스프라이트 이미지](https://intl.cloud.tencent.com/document/product/266/33940) 출력입니다.
비디오에 여러 개의 어댑티브 비트레이트 스트리밍 및 스프라이트 이미지 출력이 있는 경우 다음을 지정해야 합니다.

* 재생할 어댑티브 비트스트림.
* 썸네일로 사용할 스프라이트 이미지.

어댑티브 비트스트림에는 해상도 전환 시 서로 다른 해상도 이름에 해당하는 여러 서브 스트림이 포함되어 있습니다. 플레이어에 표시되는 각 서브 스트림의 해상도 이름을 지정할 때 서브 스트림 해상도에 대한 이름 생성 규칙을 지정해야 합니다.

## 플레이어 구성 항목

VOD는 **어댑티브 비트레이트 스트리밍 템플릿 ID**와 **스프라이트 이미지 템플릿 ID**를 지정할 수 있는 **Superplayer 구성**을 지원하며, 각 서브 스트림의 **해상도 이름 생성 규칙**(LD, SD, HD 등)을 사용자 정의할 수 있습니다.

| 구성 항목 | 구성 방법 | 기능 |
| -- | -- | -- |
| 재생용 어댑티브 비트스트림 | 어댑티브 비트레이트 스트리밍 템플릿 ID | 플레이어가 재생하는 콘텐츠를 제어합니다. |
| 썸네일 미리보기용 스프라이트 이미지 템플릿 | 스프라이트 이미지 템플릿 ID | 진행률 표시줄에 표시되는 축소판을 제어합니다. |
| 플레이어 표시용 서브스트림 해상도 이름 | 서브스트림 짧은 변 길이 이름 지정 | 해상도 전환을 위한 해상도의 이름을 제어합니다. |

## 사전 설정 구성
VOD는 편의를 위해 다음 두 가지 사전 설정 구성을 제공합니다.

<table class="table auto-table"><tbody><tr ><th rowspan="2">구성 이름</td><th colspan="3">구성 항목</td></th>
<tr><th>재생할 어댑티브 비트스트림(템플릿 ID)</td><th>사용할 스프라이트 이미지(템플릿 ID)</td><th>해상도 이름 생성 규칙(서브스트림 짧은 변 길이 기준)</td></tr>
<tr><td>default</td><td>10</td><td>10</td><td rowspan="2"><ul style="margin:0;"><li >240px: LD</li><li>480px: SD</li><li>720px: HD</li><li>1080px: FHD</li><li>1440px: 2K</li><li>2160px: 4K</li><li>기타:<code>xx</code>p(<code>xx</code>: 비디오의 짧은 변의 길이)</li></td></tr>
<tr><td>basicDrmPreset</td><td>12</td><td>10</td>
</tbody></table>

* 비디오 콘텐츠에 암호화가 필요하지 않은 경우, 어댑티브 비트레이트 스트리밍을 위한 LongVideoPreset 사전 설정 태스크 플로우와 재생용 default 사전 설정 Superplayer 구성을 사용할 수 있습니다. 구체적인 예시는 [통합 가이드](https://intl.cloud.tencent.com/document/product/266/38098)를 참고하십시오.
* 암호화된 콘텐츠를 재생하려면 어댑티브 비트레이트 스트리밍을 위한 SimpleAesEncryptPreset 사전 설정 태스크 플로우와 재생을 위한 basicDrmPreset 사전 설정 Superplayer 구성을 사용할 수 있습니다. 구체적인 예시는 [통합 가이드](https://intl.cloud.tencent.com/document/product/266/38294)를 참고하십시오.

## 사용자 정의
사전 설정된 Superplayer 구성을 사용하는 것 외에도 [콘솔](https://intl.cloud.tencent.com/document/product/266/38261)이나 [API](https://intl.cloud.tencent.com/document/product/266/37567)를 통해 구성을 사용자 정의할 수도 있습니다.
[통합 가이드](https://intl.cloud.tencent.com/document/product/266/38098)에 따라 재생을 위해 사용자 정의 Superplayer 구성을 사용할 수 있습니다.

## 구성 사용
default 사전 설정 구성 이외의 구성을 사용하는 경우 [Superplayer 서명](https://intl.cloud.tencent.com/document/product/266/38099)을 사용하고 `pcfg` 서명 매개변수에 사용할 구성 이름을 지정해야 합니다.
[통합 가이드](https://intl.cloud.tencent.com/document/product/266/38098)에 따라 Superplayer 서명을 사용하여 재생할 수 있습니다.
