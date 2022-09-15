<style>
    .card-container {
        width: 350px;
        display: block;
        float: left;
        padding-left: 15px;
        padding-right: 15px;
        box-sizing: border-box;
    }

    .card {
        border-radius: 10px;
        padding-top: 10px;
        padding-left: 10px;
        padding-right: 10px;
        padding-bottom: 10px;
        margin-top: 30px;
        border: 1px solid #ebeef5;
        background-color: #fff;
        overflow: hidden;
        box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);
        text-align: center;
    }
    
    .markdown-text-box img {
        box-shadow: none;
    }


    .titlename {
                color:#191919;
        position: relative;
        top: -2px;
                font-weight: bolder;
                font-size: larger;
    }
        
        @media (max-width: 768px){
                .card-container,
                .scene-card-container{
                        width: 100%;
                }
                .scene-card > div{
                        width: 100%!important;
                        margin-left: 0!important;
                }
                img {
        box-shadow: none;
    }
        }
</style>

## SDK 다운로드
Play SDK는 Tencent Cloud RT-Cube 제품군의 하위 제품 중 하나로, 라이브 및 VOD 재생을 위한 비디오 재생 기능을 제공합니다.
[기능 설명](https://intl.cloud.tencent.com/document/product/266/42965)에서 SDK가 지원하는 기능 리스트를 확인할 수 있으며, [Demo 체험](https://intl.cloud.tencent.com/document/product/266/42091)에서는 다양한 플랫폼에 대한 Demo를 가져올 수 있습니다. 이 페이지에서 다양한 플랫폼용 SDK를 다운로드하고 Demo 소스 코드를 가져옵니다.

### Web SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
  <div class="card-container">
      <div class="card">
        <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
        <p class="titlename">Web Player SDK</p>
        <p style="color:#586376;">라이브 재생 및 VOD 재생에 사용할 수 있으며 PC 브라우저 및 모바일 브라우저에 적합합니다.</p>
        <a onclick="reportEvent({name: 'download-click-web', ext1: 'zip'})" target="_blank" href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.2/release.zip">ZIP 다운로드</a>
        <a style="margin-left: 10px;" onclick="reportEvent({name: 'download-click-web', ext1: 'github'})" target="_blank" href="https://intl.cloud.tencent.com/document/product/266/38071">통합 가이드</a>
        <a style="margin-left: 10px;" onclick="reportEvent({name: 'download-click-web', ext1: 'doc-sdk'})" target="_blank" href="https://tcplayer.vcube.tencent.com">Demo 예시</a>
      </div>
  </div>
</div>

### iOS & Android SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                            <img src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                                <p class="titlename">iOS Player SDK</p>
                < style="color:#586376;">VOD 재생 및 라이브 재생 기능이 포함되어 있으며 애플리케이션을 신속하게 구축하는 데 도움이 되는 일반 컴포넌트 및 시나리오별 Demo 소스 코드를 제공합니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_iOS_latest.zip">ZIP 다운로드</a>
                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/266/42005">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/Player_iOS">Demo 소스 코드</a>
            </div>
        </div>
			  <div class="card-container">
            <div class="card">
                                <img class="icon" src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                                <p class="titlename">Android Player SDK</p>
                < style="color:#586376;">VOD 및 실시간 재생 기능이 포함되어 있으며 애플리케이션을 빠르게 설정하는 데 도움이 되는 공통 컴포넌트와 시나리오별 Demo 소스 코드를 제공합니다.</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Android_latest.zip">ZIP 다운로드</a>
                 <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/266/41755">통합 가이드</a>
                                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/Player_Android">Demo 소스 코드</a>
            </div>
        </div>
</div>


### 크로스 플랫폼 SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
									<img src="https://qcloudimg.tencent-cloud.cn/raw/3b6929f89ce1113bc2005873f2338de9.png" data-nonescope="true"/>
									<p class="titlename">Flutter PlayerSDK</p>
                <p style="color:#586376;">Flutter 프레임워크를 기반으로 캡슐화된 SDK로, 하나의 코드 세트를 사용하여 다양한 플랫폼용 App을 빠르게 구축할 수 있습니다.</p>
								<a href="https://github.com/LiteAVSDK/Player_Flutter">ZIP 다운로드</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/266/42098">통합 가이드</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/Player_Flutter">GitHub</a>
            </div>
        </div>
</div>



## SDK 기능 리스트
<table selecttype="cells" ><colgroup><col  ><col width="155.63" ><col  ><col  ><col  ><col  ></colgroup>
<tbody>
<tr  ><th style="width:5%">기능 모듈</td>
<th style="width:20%">기능 항목</td>
<th style="width:70%">기능 소개</td>
<th style="width:1%">Web</td>
<th style="width:1%">iOS & Android</td>
<th style="width:1%">Flutter</td>
</tr>
<tr  ><td colspan="1" rowspan="14" >재생 프로토콜/형식</td>
<td>VOD 및 CSS 지원</td>
<td>VOD 및 라이브 재생 기능 동시 지원</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>지원되는 라이브 재생 형식</td>
<td>RTMP, FLV, HLS, DASH 및 WebRTC 등 라이브 비디오 스트리밍 형식 지원</td>
<td>WebRTC, FLV, HLS, DASH</td>
<td>RTMP, FLV, HLS</td>
<td>RTMP, FLV, HLS</td>
</tr>
<tr  ><td>지원되는 VOD 재생 형식</td>
<td>HLS, DASH, MP4 및 MP3 등 VOD 오디오/비디오 형식 지원</td>
<td>HLS, MP4, MP3, FLV, DASH</td>
<td>MP4, MP3, HLS, DASH</td>
<td>MP4, MP3, HLS, DASH</td>
</tr>
<tr  ><td><a href="https://intl.cloud.tencent.com/document/product/267/41225">LEB</a></td>
<td>Tencent Cloud 밀리초급 초저지연 LEB 비디오 재생 지원</td>
<td>&#10003;</td>
<td>×</td>
<td>×</td>
</tr>
<tr  ><td>DASH 프로토콜 지원</td>
<td>표준 DASH 프로토콜을 통해 비디오 재생</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Quic 가속</td>
<td>Quic 전송 프로토콜 지원, 비디오 전송 효율성 향상</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>SDR/HDR 비디오 재생</td>
<td>HDR 10/HLG 표준에서 SDR 비디오 및 HDR 비디오 재생</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>H.264 비디오 재생 및 소프트웨어 및 하드웨어 디코딩</td>
<td>H.264 비디오 소스 재생 및 소프트웨어/하드웨어 디코딩 지원</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>H.265 비디오 하드웨어 디코딩</td>
<td>하드웨어를 기반으로 H.265 비디오 소스 디코딩</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>오디오 재생</td>
<td>MP3 및 기타 오디오 파일 재생</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>듀얼 사운드 채널</td>
<td>듀얼 사운드 채널 재생</td>
<td>×</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Http Header 설정</td>
<td>동영상 데이터를 요청할 때 사용자 정의 HTTP Headers 사용</td>
<td>×</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>HTTPS 지원</td>
<td>HTTPS 비디오 재생</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>HTTP 2.0</td>
<td>HTTP 2.0 프로토콜 지원</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td colspan="1" rowspan="6" >재생 성능</td>
<td>사전 다운로드</td>
<td>동영상 파일의 콘텐츠를 미리 다운로드하고 미리 다운로드할 파일의 크기와 해상도를 구성하면 첫 번째 프레임까지의 소요 시간(TTFF)을 크게 줄일 수 있음. 재생 장치의 에너지 소비 절감에 최적화되었고, 더 높은 성능을 제공함</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>재생 중 버퍼링</td>
<td>동영상을 재생할 때 콘텐츠를 동시에 다운로드하고 버퍼링하여 네트워크 사용량을 줄이고, 캐시 정책을 구성할 수 있음</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>정확한 seek</td>
<td>진행 표시줄의 지정된 시점에서 미디어 파일을 재생하고, 탐색은 모바일 애플리케이션에서는 프레임 레벨까지 정확하고 Web에서는 밀리초 단위로 정확함</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>실시간 네트워크 다운로드 속도</td>
<td>랙 발생 시 C 엔드 사용자에게 실시간 다운로드 속도를 표시함. 어댑티브 비트레이트 스트리밍의 대역폭 예측 모듈을 구현하기 위한 전제 조건임.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>멀티 인스턴스</td>
<td>동시 재생을 위해 동일한 페이지에 여러 플레이어 추가</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>동적 프레임 동기화</td>
<td>랙 발생 시 ‘빨리 감기’와 유사한 방식으로 현재 라이브 스트리밍 진행 상황을 따라잡아 라이브 스트리밍 이미지의 실시간성 보장</td>
<td>&#10003;</td>
<td>×</td>
<td>×</td>
</tr>
<tr  ><td colspan="1" rowspan="25" >재생 제어</td>
<td>URL을 통한 재생</td>
<td>URL에서 온라인 비디오를 재생, URL은 VOD 재생 주소 또는 라이브 스트림의 풀(pull) 주소일 수 있음</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>FileID를 통한 재생</td>
<td>FileID(VOD 파일 ID)로 동영상 재생. FileID 스트림에는 여러 해상도, 썸네일, 타임스탬프 등의 정보가 포함된 동영상이 포함됨</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>로컬 비디오 재생</td>
<td>로컬 비디오 파일 재생</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>기본 제어</td>
<td>시작, 중지, 일시 중지 및 재개와 같은 재생 제어 기능 지원</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Picture-in-picture(PiP) 재생</td>
<td>PiP 모드의 작은 창에서 미디어 재생, SDK를 통합하는 모바일 애플리케이션의 경우 PiP는 애플리케이션 내/외부에서 모두 지원</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>cache 내에서 seek</td>
<td>seek하는 동안 캐시된 콘텐츠를 지우지 않고 빠른 seek을 지원함</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>라이브 스트림 타임 시프트</td>
<td>사용자가 진행률 표시줄을 드래그하고 이전 지점에서 라이브 스트림을 재생할 수 있는 라이브 스트리밍을 위한 타임 시프트 지원</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>×</td>
</tr>
<tr  ><td>진행률 표시줄 표시 및 썸네일 미리보기</td>
<td>진행률 표시줄 표시 및 썸네일 스프라이트 표시</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>썸네일 설정</td>
<td>동영상에 맞춤 썸네일 추가</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>다시보기</td>
<td>동영상 재생이 끝난 후 수동으로 재생 트리거</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>재생 루프</td>
<td>동영상 재생이 끝난 후 자동으로 동영상 재생</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>목록 재생</td>
<td>재생 목록의 동영상을 순서대로 재생하고 재생 목록 반복(마지막 동영상이 끝난 후 재생 목록의 첫 번째 동영상 재생)</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>체크포인트 재시작</td>
<td>마지막 재생 종료 위치부터 재생 시작</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>사용자 지정 재생 시작 시간</td>
<td>비디오 재생 시작 시간 지정</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>배속 재생</td>
<td>오디오 톤에 영향을 주지 않고 0.5~3배 속도로 미디어 재생</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>백그라운드 재생</td>
<td>애플리케이션이 백그라운드로 전환되어도 오디오/비디오 계속 재생</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>재생 콜백</td>
<td>재생 상태, 첫 번째 프레임 렌더링, 재생 종료 및 재생 실패에 대한 콜백</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>재생 실패 시 재시도</td>
<td>재생 실패 시 자동으로 재시도하고 라이브 스트림 연결 실패 시 자동 재접속</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>볼륨 레벨 설정</td>
<td>실시간으로 볼륨 레벨 조정 또는 미디어 파일 음소거</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>해상도 전환</td>
<td>랙 없이 HLS 동영상의 여러 해상도 간에 원활하게 전환</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>해상도 이름 지정</td>
<td>다양한 재생 해상도에 사용자 정의 이름 지정</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>화면 캡처</td>
<td>동영상에서 프레임 추출</td>
<td>-</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>미리보기</td>
<td>동영상 미리보기</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>화면 댓글</td>
<td>재생 중 화면에 댓글 표시</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>자막 가져오기</td>
<td>자막 파일 가져오기</td>
<td>&#10003;</td>
<td>x</td>
<td>x</td>
</tr>
<tr  ><td colspan="1" rowspan="8" ><a href="https://intl.cloud.tencent.com/document/product/266/38131">비디오 암호화 개요</a></td>
<td>블록리스트/얼로우리스트 referer</td>
<td>얼로우리스트/블록리스트 구성 및 재생 요청의 Referer 필드를 사용하여 요청 허용 또는 차단 여부 결정</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Key 링크 도용 방지</td>
<td>재생 요청 URL에 유효 기간, 미리보기 시간 및 최대 IP 수에 대한 매개변수 추가</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>HLS 암호화</td>
<td>동영상 데이터는 키 및 HLS 기반 AES encryption 방식으로 암호화 가능</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>프라이빗 HLS 암호화</td>
<td>클라우드에서 프라이빗 VOD 프로토콜을 통해 동영상 암호화, 암호화된 동영상은 재생용 Player SDK를 통해서만 복호화할 수 있으므로 다양한 브라우저 확장 프로그램 및 해커 툴에 의해 동영상이 복호화되는 것을 효과적으로 방지</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>상업용 DRM</td>
<td>Apple FairPlay 및 Google Widevine과 같은 네이티브 암호화 솔루션 제공</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>보안 다운로드</td>
<td>오프라인으로 암호화된 동영상 다운로드 및 Player SDK를 사용하여 동영상 복호화 및 재생</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>동적 워터마크</td>
<td>불규칙하게 움직이는 텍스트 워터마크를 플레이어에 추가하여 불법 복제 방지</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>디지털 워터마크</td>
<td>동영상에 디지털 워터마크를 적용하여 저렴한 비용으로 해적 식별 및 추적 가능</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td colspan="1" rowspan="8" >디스플레이 효과</td>
<td>사용자 지정 UI</td>
<td>필요에 따라 선택할 수 있도록 UI가 있는 통합 솔루션 및 UI가 있는 공통 재생 컴포넌트 제공</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>화면 채우기</td>
<td>동영상을 화면에 맞추는 방법 지정</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>플레이어 크기 설정</td>
<td>플레이어 너비 및 높이 사용자 지정</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>롤 이미지</td>
<td>재생이 일시 중지되면 광고에 사용할 수 있는 이미지 표시</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>비디오 미러링</td>
<td>비디오를 수평 또는 수직으로 뒤집기</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>동영상 회전</td>
<td>특정 각도로 동영상 회전(동영상 파일의 rotate 매개변수를 지정하여 자동 회전 가능)</td>
<td>x</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>화면 잠금</td>
<td>몰입 모드에서 동영상 재생(방향 잠금 및 시스템 표시줄 숨기기)</td>
<td>-</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>밝기 조정</td>
<td>비디오 밝기 조정</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td colspan="1" rowspan="2" >부가 기능</td>
<td>TSC(Top Speed Codec) 트랜스코딩</td>
<td>Top Speed Codec(TSC) 트랜스코딩을 통해 플레이어는 후처리 과정에서 실시간으로 온라인 동영상에 대한 초고해상도 기술을 구현할 수 있습니다. 높은 이미지 품질을 유지하면서 대역폭 사용량을 줄이는 데 사용하거나 동영상 재생 정의 및 주관적인 동영상 품질을 향상시키는 데 사용할 수 있습니다.</td>
<td>x</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>재생 품질 모니터링</td>
<td>리포트된 재생 데이터를 기반으로 VOD 및 CSS 서비스를 통합하여 전체 연결 재생 데이터 통계 수집, 품질 모니터링 및 시각적 분석 서비스를 제공합니다.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
</tbody>
</table>

>! 표에서 ‘-’는 단말기에 해당 기능이 필요하지 않거나 관련 개념이 없음을 나타냅니다.
