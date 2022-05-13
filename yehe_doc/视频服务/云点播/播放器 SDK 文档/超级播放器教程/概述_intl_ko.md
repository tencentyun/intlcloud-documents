Tencent Cloud RT-Cube Player는 Tencent Cloud 서비스에 연결하고 클라우드 기반 통합 기능을 구축하는 데 필요한 중요한 컴포넌트입니다. Web, iOS, Android 및 Flutter에서 지원되는 Superplayer 및 Superplayer Adapter의 두 가지 VOD 재생 시나리오용 Player를 제공합니다. 원활한 시청 경험을 신속하게 제공하고 다양한 기능을 통합하는 고성능 솔루션을 제공합니다.
본 문서에서는 RT-Cube Player에서 제공하는 다양한 플레이어 유형의 차이점과 적절한 플레이어 유형을 선택하는 데 도움이 되는 사용 방법을 설명합니다.



## 기본 컨셉[](id:concept)
### Superplayer
Superplayer는 URL 및 FileID를 통한 재생을 지원합니다.
<table>
   <tr>
      <th width="178px" style="text-align:center">재생 방법</td>
      <th width="0px"  style="text-align:center">설명</td>
   </tr>
   <tr>
      <td style="text-align:center">Superplayer - URL을 통한 재생</td>
      <td>사용자는 URL을 통해 비디오를 재생합니다. 이 재생 방법은 FileID 기반 통계 수집 및 복합 미디어 자산 기능을 지원하지 않으며 일반적으로 <b>숏폼 비디오</b> 및 <b>숏-미디엄폼 비디오</b>와 같이 다른 보조 미디어 자산 정보가 필요하지 않은 시나리오에서 사용됩니다.</td>
   </tr>
   <tr>
      <td>Superplayer - FileID를 통한 재생</td>
      <td>사용자는 VOD에서 생성된 FileID를 통해 동영상을 재생합니다. 이 재생 방법은 VOD 리소스를 플레이어 SDK와 긴밀하게 연결하는 기능을 제공하고 FileID를 기반으로 데이터 리포트, 모니터링 및 복잡한 미디어 자산 바인딩 기능을 구현할 수 있습니다. 일반적으로 <b>롱폼 비디오</b>와 같이 다른 보조 미디어 자산 정보가 필요한 시나리오에서 사용됩니다.</td>
   </tr>
</table>

<dx-alert infotype="explain" title="">
Superplayer 기능 목록은 [비디오 재생 개요](https://intl.cloud.tencent.com/document/product/266/38295)를 참고하십시오.
</dx-alert>


### Superplayer Adapter
Superplayer Adapter는 타사 또는 독점 플레이어를 사용하여 Tencent Cloud PAAS 리소스에 연결하려는 고객을 위해 VOD에서 제공하는 플레이어 플러그 인입니다. 일반적으로 **플레이어 기능을 사용자 정의해야 하는** 고객이 사용하며 특정 액세스 임계값이 있으며 기본 기능은 Superplayer와 동일합니다.


### 다양한 플레이어 유형 비교
<table>
    <tr>
        <th width="120px">플레이어</td> 
        <th width="250px">기능</td> 
        <th>장점</td>
        <th>커스터마이징 정도</td> 
   </tr>
   <tr>
        <td rowspan="2">Superplayer</td>    
        <td >URL을 통한 재생 지원</td>
        <td > VOD에서 생성된 URL 및 타사 URL을 통한 재생 지원 </td> 
        <td > 낮음 </td> 
   </tr>
   <tr>
        <td> VOD에서 생성된 FileID를 통한 재생 지원 </td> 
        <td> 통합 VOD 데이터 리포트 및 품질 모니터링 서비스 제공 </td> 
        <td > 낮음 </td> 
   </tr>
     <tr>
        <td >Superplayer Adapter</td> 
        <td> VOD에서 생성된 FileID를 통해서만 재생 지원 </td> 
        <td> 타사 또는 독점 플레이어와 통합 가능 </td> 
        <td> 높음 </td>
   </tr>

</table>



## 핵심 강점[](id:core)
<table>
   <tr>
      <th width="120px" style="text-align:center">개요</td>
      <th width="0px"  style="text-align:center">설명</td>
   </tr>
   <tr>
      <td style="text-align:center">클라우드 통합</td>
      <td>VOD의 PAAS 리소스를 손쉽게 활용하여 클라우드 기반의 통합 기능을 구축할 수 있습니다.</td>
   </tr>
   <tr>
      <td style="text-align:center">비디오 보안</td>
      <td>링크 도용 방지, URL 인증, HLS 암호화, 독점 프로토콜 암호화 및 로컬 암호화와 같은 여러 암호화 체계를 제공하여 미디어 자산의 보안을 전방위적으로 보호하고 다양한 시나리오에서 보안 요구 사항을 충족합니다.</td>
   </tr>
   <tr>
      <td style="text-align:center">비디오 재생</td>
      <td>첫 프레임 바로 재생, 재생 중 버퍼링, 배속 재생, 비디오 타임스탬프, 화면 댓글, 애드온 자막 등 다양한 기능을 제공합니다.</td>
   </tr>
   <tr>
      <td style="text-align:center">비디오 전송 가속화</td>
      <td>Tencent Cloud의 대규모 캐시 노드에 의존하여 밀리초 수준의 완벽한 비디오 가속화 기능을 제공하여 초고속 비디오 재생 경험을 제공합니다.</td>
   </tr>
</table>

## 특수 기능[](id:function)
Tencent Cloud RT-Cube Player를 통합하면 여러 기능을 빠르게 통합할 수 있습니다. 더 많은 기능은 [비디오 재생 개요](https://intl.cloud.tencent.com/document/product/266/38295)를 참고하십시오.
<table>
   <tr>
      <th width="120px" style="text-align:center">기능</td>
      <th width="0px" style="text-align:center">설명</td>
      <th width="120px"  style="text-align:center">비고</td>
   </tr>
   <tr>
      <td style="text-align:center">비디오 암호화</td>
      <td>표준 HLS 암호화 및 Tencent Cloud의 독점 프로토콜을 통한 암호화 지원</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/38131">개요</a></td>
   </tr>
   <tr>
      <td style="text-align:center">비디오 재생</td>
      <td>다양한 시나리오에서 FileID를 통해 VOD 미디어 자산 기능 및 관련 보조 미디어 자산 정보를 기반으로 다양한 비디오 재생 기능 구현 지원</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/38295">개요</a></td>
   </tr>
   <tr>
      <td style="text-align:center">안전한 다운로드</td>
      <td>다운로드한 비디오의 로컬 2차 암호화를 지원하여 지정된 애플리케이션을 통해서만 미디어 자산을 재생할 수 있도록 함</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/38295">개요</a></td>
   </tr>
</table>

## 관련 링크[](id:link)
Tencent Cloud RT-Cube Player는 Web, iOS, Android 및 Flutter(Superplayer 전용)에서 지원됩니다. 자세한 내용은 아래 표에 나열된 문서를 참고하십시오.


<table>
   <tr>
      <th width="120px" style="text-align:center">플랫폼</td>
      <th width="70px" style="text-align:center">플레이어</td>
      <th width="0px"  style="text-align:center">SDK & Demo 다운로드 주소</td>
      <th width="0px" style="text-align:center">Demo</td>
      <th width="0px"  style="text-align:center">사용 설명서</td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='2'>Web</td>
      <td>Superplayer</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/33977#transcoding-service-on-vod-platform">SDK</a></td>
      <td><a href="https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html">Demo</a></td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/33977">Web - Superplayer</a></td>
   </tr>
   <tr>
      <td>Superplayer Adapter</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/42095">SDK</a></td>
      <td>-</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/42095">Web - Superplayer Adapter</a></td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='2'>iOS</td>
      <td>Superplayer</td>
      <td><a href="https://github.com/tencentyun/SuperPlayer_iOS">SDK + Demo</a></td>
      <td><a><button style="width:120px;height: 120px;border:none;background-image:url(https://main.qcloudimg.com/raw/12c7da97cc910eda673cb19b66fc7cb3.png);background-size: cover;">
</button></a></td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/33976">iOS - Superplayer</a></td>
   </tr>
   <tr>
      <td>Superplayer Adapter</td>
      <td><a href="https://mediacloud-76607.gzc.vod.tencent-cloud.com/TXCPlayerAdapter/Release/1.0.0/TXCPlayerAdapterSDK_1.0.0_iOS.zip">SDK</a></td>
      <td>-</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/42096">iOS - Superplayer Adapter</a></td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='2'>Android</td>
      <td>Superplayer</td>
      <td><a href="https://github.com/tencentyun/SuperPlayer_Android">SDK + Demo</a></td>
      <td><a><button style="width:120px;height: 120px;border:none;background-image:url(https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png);background-size: cover;">
</button></a></td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/33975">Android - Superplayer</a></td>
   </tr>
   <tr>
      <td>Superplayer Adapter</td>
      <td><a href="https://mediacloud-76607.gzc.vod.tencent-cloud.com/TXCPlayerAdapter/Release/1.0.0/TXCPlayerAdapterSDK_1.0.0_Android.zip">SDK</a></td>
      <td>-</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/42097">Android- Superplayer Adapter</a></td>
   </tr>
   <tr>
      <td  style="text-align:center">Flutter</td>
      <td>Superplayer</td>
      <td><a href="https://github.com/tencentyun/SuperPlayer/tree/main/Flutter">SDK + Demo</a></td>
	     <td><a href="https://github.com/tencentyun/SuperPlayer/tree/main/Flutter">Demo</a></td>
	     <td><a href="https://intl.cloud.tencent.com/document/product/266/42099">Flutter - Superplayer</a></td>
   </tr>
</table>




## 연결 가이드
Superplayer에 빠르게 연결할 수 있도록 연결 단계를 데모로 설명하는 [Superplayer Guide](https://intl.cloud.tencent.com/document/product/266/38098)를 제공합니다.
- 재생 문제가 발생하면 [Web 재생](https://intl.cloud.tencent.com/document/product/266/1303)을 참고하십시오.
- 기술 용어는 [용어집](https://intl.cloud.tencent.com/document/product/266/11732)을 참고하십시오.
  
