<style>.markdown-text-box table td, .markdown-text-box table th {text-align: center;}</style>

Tencent Cloud 오디오/비디오 SDK 모바일(Android & iOS & Flutter) 10.1 버전이 배포되었으며, 새 버전의 SDK는 ‘Tencent Video’와 동일한 재생 커널을 사용하여 비디오 재생 능력을 전면 최적화 및 업그레이드하였습니다. 자세한 내용은 [업그레이드 특성](#up)을 참고하십시오.

동시에 이번 버전부터는 **비디오 재생** 기능 모듈의 권한 부여 인증 기능이 추가됩니다.

SDK의 새 버전에서 **라이브 방송 또는 VOD 재생 기능을 사용하려면 지정된 License를 무료로 활성화하여 권한을 획득해야 합니다**. 자세한 내용은 [무료 권한 부여 방식](#warrant)을 참고하십시오. 비디오 재생 기능이 필요하지 않거나 SDK 10.1 이상 버전으로 업그레이드하지 않은 경우 이 변경 사항의 영향을 받지 않습니다.

>! **App에 이미 라이브 방송 License 또는 UGSV License가 있는 경우 버전 10.1로 업그레이드한 후에도 정상적으로 계속 사용할 수 있으며** 이 변경 사항의 영향을 받지 않습니다. [CSS 콘솔](https://console.intl.cloud.tencent.com/live)에 로그인하면 현재 라이브 방송 License 정보를 볼 수 있고, [VOD 콘솔](https://console.intl.cloud.tencent.com/vod)에 로그인하면 현재 VOD License 정보를 볼 수 있습니다.

[](id:warrant)

## 무료 권한 부여 방식

10.1 이후 버전에서 **비디오 재생** 기능 모듈을 사용하려면 비디오 재생 License 권한이 필요하며, 이 License 권한은 무료입니다. 자세한 권한 부여 방식은 다음과 같습니다.

1단계, Tencent Cloud 계정에 등록/로그인하고 [TRTC 콘솔](https://console.tencentcloud.com/trtc)로 이동합니다.

2단계, 왼쪽 사이드바에서 ‘**관련 클라우드 서비스**’를 클릭하고 ‘**License 발급**’란에서 **정식 License 생성**을 클릭합니다. 안내에 따라 내용을 입력한 후 ‘**확인**’을 클릭하면 권한 부여가 완료됩니다.


[](id:up)

## 업그레이드 특성

업그레이드된 Tencent Cloud 오디오/비디오 단말 SDK 비디오 재생 커널은 Tencent 내부에서 완전히 자체 개발되었으며, 장기 최적화와 대량 서비스 인증을 거쳐 성능이 시스템 플레이어 대비 30% ~ 50% 향상되었습니다. 동시에 대역폭 비용 제어, 운영 성장 지원, 액세스 진입 장벽 감소 등의 측면에서 엔터프라이즈 사용자를 위한 전문 최적화 업그레이드를 수행하였으며, 단말 TESHD, 저작권 보호, 풀 링크 데이터 통찰력 및 시나리오별 로우 코드 등의 솔루션을 추가하여 엔터프라이즈급 요구를 완전히 충족하는 업계 독점, 업계 선두의 엔터프라이즈급 비디오 재생 솔루션을 구축하였습니다.

<table>
<thead>
<tr>
<th width=16% style="text-align: left;">특성</th>
<th style="text-align: left;">설명</th>
</tr>
</thead>
<tbody><tr>
<td style="text-align: left;">‘Tencent Video’와 동일</td>
<td style="text-align: left;">최초로 ‘Tencent Video’의 재생 기능이 SDK 형태로 개발자들에게 공개되었으며, ‘컬러풀 시청각’, 정밀 Seek, 해상도 전환, 작은 창 재생, 오프라인 캐시 등 ‘Tencent Video’와 동일한 재생 기능을 가지면서 동시에 동일한 수준의 비디오 재생 안정성과 모델 적응성을 갖췄습니다.</td>
</tr><tr>
<td style="text-align: left;">추가된 형식 지원</td>
<td style="text-align: left;">QUIC, AV1, H.266 등 형식에 대한 지원을 추가하여 H.264/H.265에 비해 대역폭을 20%~55% 절약하여 다양한 비즈니스 시나리오를 충족하고 고객 비용을 절감합니다.</td>
</tr><tr>
<td style="text-align: left;">저작권 보호 업그레이드</td>
<td style="text-align: left;">사유 프로토콜 암호화, 로컬 암호화, 링크 도용 방지 등 솔루션을 지원한다는 전제 하에 상업용 DRM 암호화 솔루션에 대한 지원을 추가했으며 전면적으로 비디오 저작권을 보호하는 완전한 비디오 보안 솔루션 매트릭스를 보유하고 있습니다.</td>
</tr><tr>
<td style="text-align: left;">화질 향상 솔루션</td>
<td style="text-align: left;">‘Tencent Video-컬러풀 시청각’ HDR 10 비디오 재생 기능 지원 추가; 단말 TESHD 솔루션을 제공하여 비디오의 주관적 화질을 저하시키지 않으면서 기업의 전송 대역폭 비용을 절약할 수 있습니다.</td>
</tr><tr>
<td style="text-align: left;">시나리오별 로우 코드</td>
<td style="text-align: left;">관련 시나리오 App을 빠르게 구축할 수 있는 Tencent Channels(몰입형 UGSV) 및 Tencent 뉴스(비디오 Feed 스트림)와 유사한 시나리오별 솔루션 제공; 비디오 커버, 동적 워터마크, 목록 루프 등 다양한 기능 컴포넌트를 추가하여 다양한 비즈니스 시나리오에 적합하며 개발 비용을 줄입니다.</td>
</tr>
</tbody></table>
