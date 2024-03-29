최근 멀티미디어 기반 기술이 성숙해짐에 따라 라이브 방송 업계는 전세계적으로 폭발적인 성장을 거듭하고 있으며 중국 내 인터넷 플랫폼의 해외 진출도 보편화되고 있습니다. 중국 내 서비스형 제품의 해외 진출 경험은 라이브 방송 업계의 해외 진출 시도에 탄탄한 기반을 마련하게 되었습니다. 이미 중국 내에서 남다른 영향력을 구축한 비디오 라이브 방송 기업들은 경쟁적 우위를 확대하기 위해 제품의 글로벌화 계획을 진행하고 있으며, 일부 소규모 라이브 방송 플랫폼은 중국 내에서 입지를 확보하지 못해 해외 시장으로 눈을 돌려 새로운 돌파구를 찾아가고 있습니다. 동시에 해외 라이브 방송 플랫폼 전쟁도 매우 치열한 상황에서 YouTube, Periscope, Facebook이라는 3대 거대 기업들이 각축전을 벌이고 있지만, 아직 개발되지 않은 블루 오션 시장이 많아 소규모 라이브 방송 플랫폼에게 좋은 기회가 될 수 있습니다. Tencent Cloud는 이를 기반으로 해외 라이브 방송 분야에서 리소스 보유량을 지속적으로 확대해 나가고 있으며 라이브 방송 가속 성능을 끊임없이 최적화하여 라이브 방송 플랫폼이 해외 시장에 나갈 수 있도록 지원하고 있습니다.
![](https://main.qcloudimg.com/raw/220512d9f3ec1cdaa7b2f04c7b1e6150.png) 

완벽한 라이브 방송 서비스는 푸시 스트림과 시청 외에도 인증, 트랜스 코딩, 화면 캡처, 녹화, 콜백, 음란물 감지, DRM 등의 기능이 포함되어야 합니다. 다음 이미지는 Tencent Cloud 해외 라이브 방송 솔루션의 기본 기능 모듈입니다.  

![](https://main.qcloudimg.com/raw/057d12ecc304f5e64918536ff2871035.png)


기본 기능 측면에서 해외 라이브 방송과 중국 내 라이브 방송에 필요한 사항은 동일하지만, 해외 라이브 방송에는 광대한 해외 리전, 해외 국가의 복잡한 내부 네트워크, 일정하지 않은 품질의 해외 국가간 네트워크 등 수많은 도전 과제들이 존재합니다. 딜레이 시간 및 랙을 감소하고 안정적이고 신뢰도 높은 서비스를 제공하기 위해 Tencent Cloud는 해외 라이브 방송 시나리오에 대해 **구성, 네트워크, 보안, 리소스** 등을 맞춤형으로 최적화합니다.

<span id="deploy"></span>
### 멀티 센터 배포
**Tencent Cloud는 중국홍콩, 태국, 싱가포르, 독일, 토론토, 실리콘밸리, 러시아, 남아프리카, 한국 등지에 여러 데이터 센터가 구축되어 있으며 데이터 센터를 확충해 커버할 수 있는 국가의 리전을 확대해 나가고 있습니다.**데이터 센터에는 해외 라이브 방송에 필요한 모든 모듈이 포함되어 있으며 동시에 전세계 사용자들에게 서비스합니다. 일부 데이터 센터에 장애 발생 시 전환을 보장하며 모든 구성을 중앙 집중화합니다. 국가간 네트워크 품질과 라이브 방송 딜레이 시간 및 랙 영향에 대한 안정화를 고려하여 해외에 구축한 센터 노드는 모두 전용선을 통해 연결되며 중국 내 및 해외는 중국홍콩 센터 경유 노드 전용선을 통해 연결됩니다. 대략적인 전체 구성은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/db15dda3beb4c7015c5c9505e0164756.png)
해외 센터 노드의 가속 효과를 직관적으로 나타내기 위해 중국 내 사용자가 미국 호스트의 비디오를 시청하는 경우의 통계를 비교, 분석하였으며 효과는 다음 이미지와 같습니다. 다음 이미지에서 분명히 알 수 있듯이 전용선 가속이 랙 발생률이 낮으며 네트워크도 안정적입니다.
![](https://main.qcloudimg.com/raw/4eedf1119b50fda15f83b0bafcbccf0d.png)

<span id="speed"></span>
### 엣지 지역 가속
센터 노드는 로컬 지역 사용자의 수요를 완벽하게 커버할 수 있습니다. 그러나 수많은 중심 지역이 아닌 국가의 사용자들 수요도 간과할 수 없습니다. 제한된 조건으로 인해 해당 지역 국가에는 센터 노드는 구축하지 못하고 가속 포인트 추가가 필요합니다. 일반적으로 이러한 지역은 국가간 네트워크 품질이 비교적 낮고 리전 간 풀 스트리밍 랙 발생률이 상당히 높은 편으로, 해당 지역을 엣지 지역이라 하며 말레이시아, 인도네시아, 중동, 인도, 아프리카, 남미 등의 국가가 있습니다. Tencent Cloud는 이러한 엣지 지역에 대한 서비스 모듈에 우선순위를 결정하여 먼저 로컬 합법 사용자의 시청을 보장하며 로컬 리전 데이터가 국가를 초월하지 않고 작업이 완료될 수 있도록 보장합니다. 다른 모듈 서비스의 경우 엣지 노드에서 센터 노드로 전달하여 최종적으로 센터 노드에서 완료됩니다. **하기 이미지에서 알 수 있듯이 엣지 지역에서 로컬 지역의 노드 가속을 활성화하면 랙 발생률이 현저히 감소하며, 업계 내 다른 벤더 수준보다 더욱 우수하다는 것을 알 수 있습니다.**
![](https://main.qcloudimg.com/raw/590d25023541030ee6266e862a75cc73.png)

<span id="disaster_tolerance"></span>
### 가장 우수한 액세스와 재해 복구 전환
해외의 수많은 국가는 사실 중국대륙과 유사합니다. 예를 들어 태국의 DTAC, AIS, TURE와 중국대만의 중화전신, 다거다(Taiwan Mobile), so-net, 인도네시아의 Telkomsel, XL, INDOSAT 등과 같이 한 지역에 여러 통신사가 있으며, 해당 여러 통신사 간의 액세스는 대역폭과 리소스의 영향을 받아 일정의 제한이 존재합니다. 이러한 통신사 사용자의 액세스 경험을 향상시키기 위해서는 반드시 스케쥴링 시스템에서 통신사별로 최대한 ISP와 액세스하는 문제를 해결해야 합니다. 이와 동시에 Tencent Cloud가 현지에 구축한 가속 노드도 최대한 BGP로 액세스하고 현지 관련 통신사와 peering link를 합니다.
예를 들어, 태국에서는 3개 통신사(DTAC, AIS, TURE)의 사용자에 대해 센터 스케쥴링 시스템에 엄청난 양의 해외 IP와 통신사가 기록되고 사용자 IP에 따라 자동으로 가장 가까운 CND 노드에 스케쥴링하며 식별 정확도가 **99.5%**에 달합니다. 또한 데이터 센터 장애 발생 시 전환을 지원하여 모니터링 노드에 일정 지역 장애가 감지되는 경우 시스템에서 자동으로 가장 적합한 데이터 센터를 선택하여 전환합니다.
![](https://main.qcloudimg.com/raw/e4725d92c9d6adcd3df0cb9a6fa29793.png)

<span id="net"></span>
### 네트워크 전송 최적화
해외 리전 간 외부 네트워크 전송 시 기존의 TCP 전송은 전송 딜레이 시간을 보장하지 못하며, 해외 전송 거리가 멀고 글로벌 발신 게이트웨이 대역폭이 제한되고 네트워크 품질 파동이 비교적 빈번한 프로토콜 특징으로 인해 업데이트 최적화 주기가 길고 패킷 손실률이 높은 시나리오에서 불량 등의 문제가 발생합니다. Tencent Cloud는 QUIC(UDP를 기반으로 신뢰도 높은 데이터 전송 실현)를 채용하여 해외 네트워크 전송을 최적화합니다. QUIC를 통해 상위 레이어 데이터 프록시 가속을 진행하고, 응용 레이어에서 구현하여 매개변수 또는 정체 알고리즘을 조정해 즉시 적용할 수 있으며, 알고리즘 매개 변수를 조정해 긴 딜레이 시간 및 높은 패킷 손실 시나리오에 효과적으로 대응할 수 있습니다. 또한 HOL 블로킹 문제를 방지하고 RTT 시간 소모를 줄여 줍니다. **실제 데이터로 계산한 결과 기존 TCP 대비 연결 시간이 평균 40% 감소하고 랙 발생률이 평균 20% 감소했습니다.**
![](https://main.qcloudimg.com/raw/95c2367e21cbfea268617aff354d1b9d.png)

다음 이미지는 아랍 에미리트 호스트가 아랍 에미리트 가속 노드로 푸시 스트림하고 전세계 사용자가 시청하는 테스트 시나리오에서의 해당 호스트의 랙 발생률 비교 데이터입니다. 해당 비교 데이터로 QUIC 가속 스트리밍 랙 발생률이 더욱 안정적인 것을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/02fe6d2f5cfe7d1c496446811d64548c.png)

<span id="reserve"></span>
### 대량의 리소스 보유
라이브 방송에서 통합 기술 구성 및 솔루션 이외에 더욱 중요한 것이 바로 리소스 보유입니다. 해외 리소스에 대한 기본적인 지원이 없다면 모든 기술은 무용지물과 다름 없습니다. 본 문서 서두의 Tencent Cloud 글로벌 노드 분포도에서 언급한 것과 같이 **Tencent Cloud는 해외 진출 전략과 장기 해외 투자 전략에 따라 전세계 50여 국가 및 지역에 2000+개 이상의 전송 노드를 구축하였으며, 총 100T 이상의 대역폭을 확보하고 전세계 통신사 50곳과 합작 관계를 체결하였으며 1000+개 이상의 해외 가속 포인트를 보유하고 있습니다.** 또한 동일 지역의 여러 통신사와 합작하여 전송 게이트별로 최소 3개 이상의 재해 복구로 나누어 서비스의 안전성과 높은 신뢰도를 보장합니다.자세한 내용은 [CDN](https://intl.cloud.tencent.com/document/product/228/2941?from_cn_redirect=1#nodes-outside-mainland-china)를 참조 바랍니다.

<span id="open"></span>
### 활성화 방법
해외 라이브 방송 서비스는 [CSS 콘솔](https://console.cloud.tencent.com/live)에서 직접 활성화할 수 있습니다.
- 아직 Tencent Cloud 계정에 가입하지 않은 경우, Tencent Cloud 계정 가입이 필요하며 등록 방법은 [Tencent Cloud 회원가입](https://intl.cloud.tencent.com/document/product/378/17985) 문서를 참조하고, [라이브 방송 서비스 활성화 신청](https://intl.cloud.tencent.com/document/product/267/30410)을 참조하십시오.
- Tencent Cloud 계정에 이미 가입하였고 라이브 방송 서비스 활성화를 이미 신청한 경우 다음 단계로 넘어갑니다.

CSS 콘솔로 이동하여 왼쪽 메뉴에서 [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)를 선택한 후 [도메인 추가]를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e0131c5904b8e2a8c20034b10fb7127b.png)

팝업된 도메인 추가 창에서 [재생 도메인] 유형을 선택하고 해당 [가속 지역]을 선택한 후 가속할 [도메인]을 입력합니다.
