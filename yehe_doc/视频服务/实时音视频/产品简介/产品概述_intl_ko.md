
Tencent Real-Time Communication(TRTC)은 Tencent가 다년간 네트워크와 멀티미디어 기술 분야에서 이룩한 성과가 적용된 솔루션으로 그룹 멀티미디어 통화와 저지연의 ILVB(Interactive Live Video Broadcasting)에 적합합니다. Tencent Cloud 서비스를 통해 신속성, 저비용, 저지연, 고품질을 특징으로 한 멀티미디어 인터랙션 솔루션을 제공합니다.
- 그룹 멀티미디어 솔루션
 Tencent Cloud의 전용 네트워크가 연결되는 전세계 어디서나 휴대폰, 데스크톱 플랫폼의 클라이언트 SDK, Cloud API로 인터랙티브하게 사용할 수 있습니다. 또한 Web 페이지에서도 간편하게 사용 가능합니다.
- 저지연 ILVB 솔루션
 업계 선두의 네트워크 및 멀티미디어 기술과 Tencent Cloud의 우수한 노드 리소스를 접목해 랙 발생률이 낮고, 딜레이 시간 1초 이내의 TRTC 사용 환경을 제공하며, 라이브 방송의 CDN 2.0시대를 구현합니다.




## 제품 아키텍처
TRTC는 다양한 플랫폼을 대상으로 그룹 멀티미디어 통화 및 저지연의 ILVB를 지원하는 솔루션으로서 미니프로그램, Web, Android, iOS, Electron, Windows, macOS 등 플랫폼에 SDK를 제공합니다. 이로써 신속한 통합이 가능하며, TRTC의 클라우드 서비스 백그라운드와 연결할 수 있습니다. Tencent Cloud의 다양한 제품과 상호 연동이 가능해 TRTC를 IM, CSS, VOD 등 클라우드 서비스와 연계 사용함으로써 보다 다양한 작업이 가능합니다. 제품 구성은 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/be1345a58328913f7dae524a4cc5e153.svg)

## 플랫폼 지원
TRTC는 **업계 모든 플랫폼의 상호 연동을 구현하는 솔루션**입니다. 플랫폼 지원 사항 및 개발 환경에 관한 자세한 사항은 아래 표를 참고하십시오.

<table>
<tr><th>플랫폼</th><th>개발 환경 요건</th></tr>
<tr>
<td>iOS</td>
<td>
  <li>iOS 9.0 이상 버전의 iPhone 또는 iPad 지원</li>
  <li>Xcode 9.0+</li>
  <li>유효한 개발자 서명이 설정되어있는 프로젝트</li>
</td>
</tr><tr>
<td>Android</td>
<td>
  <li>Android Studio 3.5+</li>
  <li>Android 4.1(SDK API Level 16) 이상 시스템 사용 권장</li>
</td>
</tr><tr>
<td>Windows</td>
<td>
  <li>Windows 7 이상 버전 지원</li>
  <li>Visual Studio 2010 이상 버전, Visual Studio 2015 사용 권장</li>
  <li>.Net Framework 4.0 이상 버전</li>
</td>
</tr><tr>
<td>Mac OS</td>
<td>
  <li>Xcode 9.0+</li>
  <li>OS X10.10+의 Mac</li>
  <li>유효한 개발자 서명이 설정되어있는 프로젝트</li>
</td>
</tr><tr>
<td>Web</td>
<td>데스크톱에서는 Chrome 56+ 사용을 권장하며, 자세한 개발 환경 요건 사항은 <a href="https://intl.cloud.tencent.com/document/product/647/35096">빠른 통합(Web)</a>을 참고하십시오.</td>
</tr><tr>
<td>Electron</td>
<td>
  <li>Windows 7 이상 버전, Mac OS 10.10 이상 버전 지원</li>
  <li>Electron 4.0.0 이상 버전 지원, 최신 버전의 Electron SDK 사용 권장</li>
</td>
</tr><tr>
<td>WeChat 미니프로그램</td>
<td>
  <li>WeChat App iOS 최소 버전 요구 사항: 7.0.9</li>
  <li>WeChat App Android 최소 버전 요구 사항: 7.0.8</li>
  <li>미니프로그램 기본 라이브러리 최소 버전 요구 사항: 2.10.0</li>
  <li>미니프로그램 개발자 툴은 네이티브 컴포넌트를 지원하지 않으므로(예: &lt;live-pusher&gt; 및 &lt;live-player&gt; 태그), 실제 시스템에서 경험해야 합니다.</li>
</td>
</tr><tr>
<td>Flutter</td>
<td>iOS:
  <li>iOS 9.0 이상 버전의 iPhone 또는 iPad 지원</li>
  <li>Xcode 9.0+</li>
  <li>유효한 개발자 서명이 설정되어있는 프로젝트</li>Android: <li>Android Studio 3.5+</li>
  <li>Android 4.1(SDK API Level 16) 이상 시스템 사용 권장</li>
</td>
</tr></table>

[](id:safe)
## 컴플라이언스
컴플라이언스는 Tencent Cloud TRTC 개발의 기초입니다. TRTC는 제공되는 서비스의 **안전성, 합법성, 가용성, 보안성 및 프라이버시를 보장**하며, 여러 국가 및 산업의 컴플라이언스 요구 사항을 준수합니다. 또한 TRTC 사용 고객에게 관련 지원을 제공하여 **기업 및 기업 고객의 여러 규정 준수 및 모니터링 요구 사항을 충족하고, 기업 및 기업 고객의 감사 작업에 대한 반복적 비용을 줄여 감사 및 관리 효율성을 향상시킵니다.**

**TRTC는 SOC 감사 보고서(SOC 1, SOC 2, SOC 3 포함), 네트워크 보안 등급 보호 2.0 및 ISO 인증(ISO 9001, ISO 20000 포함)을 취득했습니다.**
![](https://main.qcloudimg.com/raw/3cd618fd25165dde224dd0c3781cf129.png)
