## 소개
Tencent는 중국에서 가장 초기이자 가장 큰 인스턴트 메시징 개발업체입니다. 산업 디지털 변혁의 추세에 따라 Tencent는 이제 높은 동시성과 매우 안정적인 인스턴트 메시징 기능을 SDK 및 REST API로 공유하고 Tencent Cloud 제품 Instant Massaging(IM)을 출시합니다. Tencent Cloud에서 제공하는 IM SDK를 간단한 방법으로 애플리케이션에 통합할 수 있습니다. 서버 측에서 REST API를 호출하면 강력한 인스턴트 통신 기능을 쉽게 사용할 수 있습니다. 다음 그림은 IM 서비스와 애플리케이션 간의 상호 작용을 보여줍니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2e57bf9cbb3a1855efe7abdfd7d8beab.png)
개발자의 다양한 단계의 요구 사항 및 시나리오를 위해 Instant Messaging(IM) 팀은 Android, iOS, Windows 및 Web의 SDK 컴포넌트, 서버 통합 [REST API](https://intl.cloud.tencent.com/document/product/1047/34620), [서드 파티 콜백 API](https://intl.cloud.tencent.com/document/product/1047/34354) 등을 비롯한 일련의 솔루션을 제공합니다. 이러한 컴포넌트와 기능을 통해 개발자는 자유롭고 글로벌한 커뮤니케이션을 지원하는 안정적인 IM 제품을 구축할 수 있습니다.

## 아키텍처
IM은 글로벌 액세스, 1:1채팅, 그룹 채팅, 메시지 푸시, 데이터 관계망 호스팅, 계정 인증과 같은 광범위한 솔루션을 제공하고, 완벽한 App 액세스 및 백엔드 관리 인터페이스를 제공합니다.
![](https://main.qcloudimg.com/raw/6537f6e705289419963ee647ae851c94.png)

## 서비스
### 액세스 서비스
IM은 높은 연결성, 높은 신뢰성, 강력한 보안성을 갖춘 글로벌 네트워크 연결 채널을 제공합니다. 다중 최적 주소 지정 알고리즘을 자체 개발하여, 전체 네트워크 스케줄링 기능을 보유하고 있으며, 지능형 호환 기능으로 게이트웨이 정책을 통과하고, 영구 연결 다중화, 전송 계층 프로토콜 최적화 및 채널 암호화 전송 등 기술을 통해 기업은 네트워크 세부 사항에 대한 걱정 없이 비즈니스 백엔드와 간단하고 안정적인 커뮤니케이션을 구축할 수 있습니다. 
단말 로그인 시, IM SDK는 가장 가까운 액세스 노드에 연결합니다. 글로벌 액세스 노드 분포는 다음과 같습니다.

- 중국: 화남, 화북, 화동, 중국홍콩, 중국대만 등
- 기타 국가(또는 지역):
 - 아시아: 싱가포르, 인도네시아, UAE, 태국, 말레이시아, 일본, 베트남, 인도, 한국, 필리핀 등.
 - 유럽: 영국, 네덜란드, 프랑스, 독일, 이탈리아, 노르웨이, 프랑스, 러시아, 스페인 등.
 - 남미: 브라질 등.
 - 북미: 미국, 캐나다, 멕시코 등.
 - 오세아니아: 호주 등.
 - 아프리카: 남아공, 나이지리아 등.

### 데이터 스토리지 센터(IDC)
IM은 중국, 남아시아(인도), 동남아시아(싱가포르), 동북아시아(대한민국 서울), 유럽(독일 프랑크푸르트) 및 북미(미국 실리콘밸리)에 IDC를 제공합니다. 귀하의 비즈니스 데이터는 애플리케이션 생성 시 선택한 IDC에 저장되며 각 IDC는 전역적으로 액세스할 수 있습니다.

### 1:1 채팅
1:1 채팅은 텍스트, 이모티콘, 지리적 위치, 이미지, 음성, 쇼트 비디오 및 사용자 정의 메시지 기능을 제공하여, 홍바오, 챗봇, 메시지 수신 확인, 메시지 회수 등 특수 기능을 실현할 수 있습니다. 또한 오프라인 메시징 및 로밍 메시징과 같은 서비스도 제공합니다. 자세한 내용은 [1:1 채팅 메시지](https://intl.cloud.tencent.com/document/product/1047/33523) 문서를 참고하십시오.

### 그룹 채팅
다중 사용자 채팅 서비스는 그룹 참여 방식과 관리 조직 형태에 따라 다음 5가지 그룹 유형을 제공하여 다양한 그룹 채팅 시나리오의 니즈를 충족합니다.

- **업무 그룹(Work)**: 사용자가 그룹 구성원인 친구의 초대를 받아 그룹에 입장할 수 있도록 합니다. 그룹 입장에는 초대받은 사람의 동의나 그룹 소유자의 승인이 필요 없습니다.
- **공개 그룹(Public)**: 그룹 소유자가 그룹 관리자를 지정할 수 있습니다. 그룹에 입장하기 위해서는 사용자가 그룹 ID를 검색하여 요청을 보내야 하며, 그룹 소유자 또는 관리자의 승인을 받아야 그룹에 입장할 수 있습니다.
- **회의 그룹(Meeting)**: 사용자가 자유롭게 입/퇴장할 수 있으며, 사용자 그룹 참여 전의 메시지 기록 보기를 지원합니다. 회의 그룹은 멀티미디어 회의, 온라인 교육 등 Tencent Real-Time Communication(TRTC) 제품 통합 시나리오에 적합합니다.
- **오디오 비디오 그룹(AVChatRoom)**: 사용자가 자유롭게 입/퇴장할 수 있으며, 구성원 인원 제한 및 메시지 기록 저장 기능이 없습니다. Cloud Streaming Services(CSS)와 통합하여 댓글 자막 채팅 시나리오에 활용할 수 있습니다.
- **커뮤니티(Community)**: 생성 후 자유롭게 출입이 가능하여, 지식 공유, 게임 교류 등 대규모 커뮤니티 그룹 채팅 시나리오에 적합합니다.
>?커뮤니티(Community) 기능은 v5.8.1668 이상의 인핸스드 버전 SDK와 v2.17.0 이상의 Web용 SDK에서 지원됩니다. 플래그십 버전을 구매하고 [**콘솔**](https://console.cloud.tencent.com/im/qun-setting) > **그룹 기능 구성** > **커뮤니티**를 활성화해야 합니다.

사용자 정의 그룹 유형, 사용자 정의 그룹 필드, 사용자 정의 그룹 구성원 필드, 사용자 정의 그룹 ID, 사용자 정의 이벤트 콜백 등 다양한 그룹 사용자 정의 기능을 제공합니다. 필요에 따라 App을 커스터마이징 할 수 있습니다. 자세한 내용은 [그룹 시스템](https://intl.cloud.tencent.com/document/product/1047/33529) 문서를 참고하십시오.
>!오디오 비디오 그룹(AVChatRoom)은 그룹 인원 제한이 없으나, 단기간에 그룹 구성원의 급격한 증가가 예상되는 경우(단일 그룹의 구성원 수가 5만명 이상에 도달하는 대규모 온라인 이벤트와 같은 시나리오에서), 사전에 [Tencent Cloud 고객서비스](https://www.tencentcloud.com/contact-us) 또는 세일즈 담당 직원에게 연락하여 SDKAppID 및 이벤트 예상 시작 시간을 제공하여 서비스 리소스 보고를 수행하십시오.



### 프로필 및 관계망 호스팅
IM은 사용자 정보(예: 닉네임, 프로필 사진 및 사용자 정의 프로필 필드), 친구 목록, 블랙리스트 등 정보를 저장하는 프로필 및 관계망 호스팅 솔루션을 제공합니다. IM의 프로필 및 관계망 호스팅 서비스는 서비스 품질과 재해 복구 성능을 향상시키기 위해, 최대 12개의 사본 백업 및 다중 데이터 센터 원격 배포 서비스를 제공합니다. 자세한 내용은 [프로필 관리](https://intl.cloud.tencent.com/document/product/1047/33520) 및 [관계망 관리](https://intl.cloud.tencent.com/document/product/1047/33521) 문서를 참고하십시오.

### 계정 인증
안전한 비대칭 암호화 ECDSA-SHA256 및 해시 암호화 HMAC-SHA256(HMAC-SHA256 사용 권장)를 제공합니다. 개발자는 App의 자체 계정을 통해 IM 서비스를 신속하게 통합하여 번거로운 계정 매핑 작업에서 벗어날 수 있습니다. 간단한 SDK 연동과 편리한 API 호출로 사용자 계정(UserID)과 비밀번호(UserSig)를 쉽게 인증할 수 있습니다. 자세한 내용은 [로그인 인증](https://intl.cloud.tencent.com/document/product/1047/33517) 문서를 참고하십시오.

## 관리 및 모니터링
기본 인스턴트 메시징 기능 외에도 IM은 편리하고 사용하기 쉬운 콘솔을 제공합니다. 콘솔을 통해 애플리케이션 생성, IM SDK 다운로드, 애플리케이션 구성 쿼리, 애플리케이션 연동 테스트 및 인스턴트 메시징 기능 통합을 진행할 수 있습니다. 또한, IM 콘솔은 백엔드 메시지 전달, 그룹 관리, 통계 및 분석과 같은 다양한 기능도 지원합니다. 자세한 내용은 [콘솔 가이드](https://intl.cloud.tencent.com/document/product/1047/34577)를 참고하십시오.

## 고급 기능
### REST API
REST API는 App 백엔드에 백엔드 관리 엔트리를 제공하는 HTTP 관리 API입니다. 현재 IM에서 지원하는 REST API 목록은 [REST API 소개](https://intl.cloud.tencent.com/document/product/1047/34620) 문서를 참고하십시오.

REST API 외에도 IM 콘솔은 데이터 관리, 1:1/그룹 메시징과 같은 간단한 기능도 제공합니다. 개발자는 IM 콘솔에서 데이터를 관리, 확인 및 테스트할 수 있습니다. REST API는 사용자 친화적이지 않지만 더 강력한 관리 기능을 제공합니다.


### 서드 파티 콜백
IM이 [서드 파티 콜백](https://intl.cloud.tencent.com/document/product/1047/34354)을 시작하면, 이벤트 전후에 App 백엔드에 요청을 보내고, App 백엔드는 그에 따라 데이터를 동기화하거나 이벤트의 후속 처리에 개입합니다.
IM은 다양한 콜백 API를 무상 제공합니다. 자세한 내용은 [콜백 명령어 목록](https://intl.cloud.tencent.com/document/product/1047/34355)을 참고하십시오.

## 프라이빗 배포 지원
기업은 프라이빗 배포를 통해 회사 자체 서버에 시스템을 배포하고, 데이터를 로컬에 저장할 수 있습니다. IM은 기업의 프라이빗 버전의 배포, 구현 및 유지 관리를 지원하는 프라이빗 배포 기능을 제공합니다. 
>?신청 시 Tencent Cloud 루트 계정으로 로그인해야 합니다.

## 컴플라이언스
컴플라이언스는 Tencent Cloud IM 개발의 기초입니다. IM은 제공되는 서비스의 **안전성, 합법성, 가용성, 보안성 및 프라이버시를 보장**하며, 여러 국가 및 산업의 컴플라이언스 요구 사항을 준수합니다. 또한 IM 사용 고객에게 관련 지원을 제공하여 **기업 및 기업 고객의 여러 규정 준수 및 모니터링 요구 사항을 충족하고, 기업 및 기업 고객의 감사 작업에 대한 반복적 비용을 줄여 감사 및 관리 효율성을 향상시킵니다.**

<b>IM은 SOC 감사 리포트(SOC 1, SOC 2, SOC 3 포함), 사이버 보안 수준 보호 2.0(레벨3), ISO 인증(ISO 9001, ISO 20000, ISO27001, ISO27017, ISO27018, ISO27701, ISO29151 포함), CSA STAR, NIST CSF, BS10012 및 KISMS 등의 인증을 통과했습니다.</b>

<style>
    .card-container {
        width: 380px;
				height:
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
        text-align: left;
    			height:260px;
    }
    
    .markdown-text-box img {
        box-shadow: none;
    }


    .titlename {
                color:#191919;f
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

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
    <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/7c288e0b31526692c16a8e4fe641d6db.jpg" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/11543">SOC 1 Type Ⅱ 리포트</a> </p>
																<p style="color:#586376;">AICPA 감사 표준 SSAE No. 18의 AT-C section 320 을 참고하여 Tencent Cloud 클라우드 서비스 시스템의 제어 환경에 대해 제출한 리포트</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/7c288e0b31526692c16a8e4fe641d6db.jpg" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/11543">SOC 2 Type Ⅱ 리포트</a> </p>
                                <p style="color:#586376;">AICPA 감사 표준 SSAE No. 18의 AT-C section 205 및 TSP section 100 2017 버전을 참고하여 클라우드 서비스 시스템의 보안성, 가용성 및 기밀성에 대해 제출한 리포트</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/7c288e0b31526692c16a8e4fe641d6db.jpg" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/11543">SOC 3 Type Ⅱ 리포트 </a></p>
																<p style="color:#586376;">Tencent Cloud 서비스 시스템의 보안성, 가용성 및 기밀성을 설명하는 일반 사용 리포트이며 AICPA SSAE No. 18의 AT-C section 205 및 TSP section 100(2017 버전)에 따라 수행</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/7e62e559319afa51562101026009f0e3.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://www.tencentcloud.com/document/product/363/2487">정보 보안 등급 보호 규정(Multi-Level Protection Scheme, MLPS) 2.0 </a></p>
																<p style="color:#586376;">Tencent의 핀테크 솔루션은 레벨 4 보호에 등록되어 있고, 퍼블릭 클라우드 서비스는 레벨 3 보호에 등록되어 있습니다</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/be5a02d7027805cec66391d24d5382d6.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/2410">ISO 9001 품질 관리 시스템 인증</a>
																<p style="color:#586376;">Tencent Cloud는 클라우드 컴퓨팅 분야에서 최초로 ISO 9001 CNAS 및 ANAB 인증을 획득한 중국 클라우드 컴퓨팅 서비스 제공 업체로서 효과적인 품질 관리 프로세스 딜리버리를 구현하여 고품질 클라우드 서비스를 제공합니다.</p></p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/0f2f62361c7420c58bfeab74c42373da.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/2409">ISO 20000 IT 서비스 관리 시스템 인증</a> </p><p style="color:#586376;">Tencent Cloud는 최초로 ISO 20000-1:2018 표준 인증의 새 버전을 통과한 중국 클라우드 컴퓨팅 서비스 제공 업체이며 표준 IT 서비스 관리 프로세스를 수립하고 엄격하게 구현합니다.</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/b3b88a42e294d602d7af7d42aa343b4d.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/2408">ISO 27001 정보 보안 관리 시스템 인증</a></p><p style="color:#586376;">ISO/IEC 27001:2015는 ISO/IEC 27002:2013를 보완합니다. Tencent Cloud는 ISO 27001 지침 인증서를 통과하였으며, 이는 Tencent Cloud가 클라우드 컴퓨팅 정보 보안 제어의 효과적인 설계 및 구현을 실행했음을 증명합니다.</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/4934c5489f0cb35f8e1e16614fc07593.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/33541">클라우드 서비스의 정보 보안 제어를 위한 ISO 27017 구현 가이드</a> </p><p style="color:#586376;">ISO/IEC 27017:2015는 ISO/IEC 27002:2013을 보완합니다. Tencent Cloud는 ISO 27017 지침 인증서를 통과하였으며, 이는 Tencent Cloud가 클라우드 컴퓨팅 정보 보안 제어의 효과적인 설계 및 구현을 실행했음을 증명합니다.</p>
            </div>
 </div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/c5b246657205e0023ea89b19d95b6753.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/14031">ISO 27018 퍼블릭 클라우드 개인 정보 보호 인증 </a></p><p style="color:#586376;">Tencent Cloud는 각 고객의 개인 정보를 보호하고 완전한 개인 정보 관리 시스템을 구축하며 다양한 기술적 수단을 사용하여 사용자의 개인 정보를 보호하기 위해 최선을 다하고 있습니다.</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/0b37fbf8d1bfa04031db30ed15d76f9b.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/33540">개인 정보 관리 시스템에 대한 ISO 27701 국제 표준 </a> <p style="color:#586376;">Tencent Cloud는 ISO/IEC 27701 인증을 통과한 세계 최초의 클라우드 서비스 제공 업체이며 개인 정보 관리 시스템을 구축 및 구현했으며 지속적으로 개선할 수 있는 능력을 갖추고 있습니다.</p></p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/f652574979d9db78c8a991ca4b8a78fc.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://www.tencentcloud.com/document/product/363/39609">개인 식별 정보 보호를 위한 ISO 29151 가이드</a> </p><p style="color:#586376;">Tencent Cloud는 개인 식별 정보 보호를 위한 적절한 정보 보안 리스크 관리 환경을 제공하는 동시에 업계 베스트 프랙티스를 충족하고 지속적으로 개선할 수 있는 능력을 갖추고 있습니다.</p>
            </div>
        </div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/32d85d30e2129e5f22259918ff1d6619.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/7249">CSA STAR 클라우드 보안 관리 시스템 인증</a> </p><p style="color:#586376;">CSA STAR는 클라우드 보안 특성에 대한 국제 인증입니다. Tencent Cloud는 STAR 인증을 골드 레벨로 통과하여 클라우드 보안 기술 관리 및 제어를 강화했습니다.</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/a18be30e18d5f87d324094f9353083d0.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/45469">NIST 네트워크 보안 프레임워크</a> </p><p style="color:#586376;">NIST CSF는 미국 국립 표준 기술 연구소에서 행정 명령(E0) 13636 ‘핵심 인프라 네트워크 보안 개선’에 따라 개발되었으며, 이 프레임워크는 비즈니스 주도형 네트워크 보안 이벤트 가이드에 중점을 두고 있습니다.</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/23115be55af090caf230525be53b883d.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/34542">KISMS 인증</a> </p><p style="color:#586376;">Tencent Cloud는 중국에서 최초로 KISMS 인증을 통과한 클라우드 컴퓨팅 서비스 제공 업체로서 Tencent Cloud가 구축한 정보 보안 관리 시스템 및 기능이 관련 한국 법률 및 표준의 컴플라이언스 요구 사항을 충족함을 증명합니다.</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"  src="https://qcloudimg.tencent-cloud.cn/raw/eac6c9f40236f5ad1028ddbb34a2c5cb.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://www.tencentcloud.com/document/product/363/45470">BS 10012 </a></p><p style="color:#586376;">British Standards Institute에서 발행한 개인 정보 관리 시스템 표준</p>
            </div>
</div>
</div>



