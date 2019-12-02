CDN 콘솔에서 도메인 이름에 액세스하고 Tencent Cloud CDN에서 제공하는 가속 서비스를 이용할 수 있습니다. 구체적인 조작 방법은 다음과 같습니다.

## 도메인 이름 추가

[CDN 콘솔에 로그인] (https://console.cloud.tencent.com/cdn) 왼쪽의 [도메인 이름 관리] 메뉴를 클릭한 다음 [도메인 이름 추가]를 선택하십시오.
![](https://main.qcloudimg.com/raw/3cee079d180314cfaef452b836e0f565.jpg)
도메인 이름 추가 페이지로 이동하여 도메인 이름과 관련된 설정을 완료하십시오. 구성 설명은 아래의 [도메인 이름 구성](# m1) 표를 참고하십시오. 
![](https://main.qcloudimg.com/raw/48e8c71e7b7e84b5fdd13ffc1b30ded2.jpg)

<span ID ="m1"> </a>
## 도메인 구성

<table >
<thead>
	<tr>
		<th scope="col" colspan = "2"  style="width: 18%;">구성 항목</th>
		<th scope="col">설명</th>
	</tr>
</thead>
<tbody>
	<tr>
	<td style="text-align: center;" colspan = "2">도메인 이름</td>
		<td>대량의 도메인 이름 액세스를 지원합니다. [추가] 버튼을 클릭하여 최대 10개의 도메인 이름을 추가할 수 있습니다. 도메인 이름은 다음 조건을 충족해야 합니다. <li> 도메인 이름은 공업정보화부 ICP 비안에 등록되어 있어야 합니다. <li> 도메인 이름에 Tencent Cloud CDN이 액세스된 적이 없었어야 합니다. <br><br> 광범위한 도메인 액세스가 지원되지만 인증이 필요합니다. Tencent Cloud에서 제공한 인증 파일을 웹 사이트의 루트 디렉터리에 업로드합니다. 인증이 완료되면 광범위한 도메인 이름에 액세스할 수 있습니다. 다음 두 가지 사항에 유의하십시오.
<li>* .test.com과 같이 도메인 이름이 이미 Tencent Cloud에 엑세스 되어있는 경우 다른 계정에서 액세스 할 수 없습니다.</li>
<li>만약 ? * .test.com과 같은 광범위 도메인 이름으로 이미 엑세스했다면 해당 계정에서 * . path.test.com 및 기타 일반 도메인에 액세스할 수 없습니다.</li>
</td>
	</tr>
	<tr>
	<td style="text-align: center;" colspan = "2">소속 프로젝트</td>
	<td>도메인 이름에 해당하는 항목을 선택한 후, 도메인 이름의 분할 항목을 관리하십시오. 항목은 Tencent Cloud의 모든 제품에서 공유되며 <a href = "https://console.cloud.tencent.com/project">항목 관리</a>에서 항목을 추가 할 수 있습니다.</td>
	</tr>
	<tr>
	<td style="text-align: center;" colspan="2">원본 서버 유형</td>
		<td>외부 원본 서버 또는 <a href = "https://intl.cloud.tencent.com/product/cos">Tencent Cloud Object Storage(COS)</a> 서버 중에서 선택하십시오.</td>
	</tr>
	<tr>
		<td colspan="1" rowspan="2" style="text-align: center;" >원본 서버 설정</td>
			<td style="text-align: center; ">외부 원본 서버 </td>
			<td > 안정된 비즈니스 서버(예: 원본 서버) 가 이미 있는 경우 본래 갖고 있는 소스를 통해 CDN에 액세스 할 수 있습니다. 원본 서버 자체를 수정할 필요가 없으며 CDN 콘솔 액세스 프로세스 및 DNS 구성을 통해서만 가속 서비스를 사용 할 수 있습니다. 원본 서버 설정에 입력 하는 IP 주소와 원본 서버 도메인 이름은 다음 조건을 충족해야 합니다.<br>
<li>도메인 이름 입력 시, 액세스 도메인 이름(즉, 액세스 한 가속 도메인 이름)과 같아서는 안 됩니다. "도메인 이름: PORT" 형식을 지원하며 포트 번호는 0보다 크고 65535보다 작거나 같습니다.
<li>IP 주소 입력 시, 여러 IP를 입력 할 수 있으며 "IP : PORT" 형식을 지원하고, 포트 번호는 0보다 크고 65535보다 작거나 같습니다. 여러 개의 IP 입력 시, 원본 가져오기 요청은 각 IP에 차례로 액세스합니다.
<li>IP가 여러 개인 경우 가중치를 구성할 수 있습니다. 가중 형식을 IP: PORT : WEIGHT로 설정하십시오(여기서 PORT는 생략 할 수 있습니다). 형식은 IP :: WEIGHT이며 WEIGHT의 범위는 0-1000입니다. (IPv4 주소만 해당)
<li>입력한 IP는 개인 IP일 수 없습니다.</td>
	</tr>
	<tr>
		<td style="text-align: center; ">COS 원본 </td>
		<td> <a href = "https://intl.cloud.tencent.com/product/cos">를 사용하려는 경우 Tencent Cloud Object Storage(COS)</a> 정적 가속 내용을 저장하면, COS 원본 액세스 방법을 사용하여 도메인 이름을 CDN에 직접 연결할 수 있습니다. 액세스 방법은 다음과 같습니다.<br>
<li>원본 서버 유형은 COS입니다. 드롭다운 메뉴를 사용하거나 키워드를 입력하여 Bucket의 도메인 이름을 선택할 수 있습니다.
<li>해당 항목 중 버킷이 없는 경우 <a href ="https://console.cloud.tencent.com/cos5">COS 콘솔</a> 에 로그인하여 버킷 <a href ="https://console.cloud.tencent.com/cos5">을</a> 생성하거나 (자세한 내용 <a href = "https://intl.cloud.tencent.com/document/product/436/13309">은 버킷 생성</a> 참조) 개발자 계정에 연락하여 해당 버킷 사용 권한을 받으십시오.
<li>버킷을 원본 서버로 선택하면 <a href ="https://console.cloud.tencent.com/cos5">COS 콘솔</a> 에서 원본 서버 콘텐츠를 관리할 수 있습니다. 
<blockquote class="d-mod-notice">
							<div class="d-mod-title d-notice-title">
								<i class="d-icon-notice"></i>참고:
							</div>
               <p></p>
<ul>
<li>CDN에서 COS 원본 도메인 이름에 액세스 할 때 COSV5 버전으로 완전히 전환되었으므로 COSV4 버킷을 원본 서버로 추가해야 하는 경우 COSV4 콘솔로 이동하여 해당 버킷에 대한 가속 서비스를 활성화해야 합니다.</li>
<li> COSV5 버킷이 개인용인 경우 CDN 서비스가 해당 COS 버킷에 액세스 할 수 있게 한 다음, 원본 가져오기 액세스를 활성화해야 합니다. 이때, 개인용 버킷의 모든 리소스는 CDN 공용 네트워크를 통해 배포될 수 있으므로 비교적 높은 보안 위험이 존재합니다. 신중하게 조작하시기 바랍니다.</li>
</ul></blockquote>
</td>
	</tr>
</tbody>
</table>



## 가속화 서비스 구성

가속화 서비스 유형 및 기본 구성을 선택하십시오.
![](https://main.qcloudimg.com/raw/2f0b3ff1c1c8fa1313b96d856fb3b1fd.jpg)
1. **서비스 유형** 
   서비스 유형 선택에 따라 도메인 이름 예약을 위한 리소스 플랫폼이 결정됩니다. 플랫폼의 가속 구성에는 다음과 같은 차이점이 있습니다. 서비스와 일치하는 유형을 선택하십시오.
	- 정적 가속: 전자 상거래, 전자 상거래, 웹 사이트 및 게임 이미지 정적 리소스의 가속화 환경
	- 다운로드 가속: 게임 설치 패키지, 오디오 및 비디오 원본 파일 다운로드, 모바일 펌웨어 배포 및 기타 환경
	- 주문형 스트리밍 가속: 주문형 오디오 및 비디오 스트리밍 환경
2. **기본 구성
   CDN은 사용자를 위해 필터링 파라미터 서비스를 제공하며, 비즈니스의 필요에 따라 사용자의 요구에 맞는 제어가 되고 있는지 URL에서 ** "?"** 뒤의 파라미터로 필터링할 수 있습니다. 필터링 파라미터를 사용하여 버전을 제어하거나 토큰으로 리소스를 인증 할 수 있습니다. 자세한 내용은 [필터링 파라미터 구성](https://intl.cloud.tencent.com/doc/product/228/6291)을 참조하십시오.
3. **캐시 만료 설정**
   캐시 만료 설정이란 CDN 캐시 노드가 사용자의 서비스 내에서 캐시될 때 준수해야 하는 만료 규칙입니다. 자세한 내용은 [캐시 만료 설정](https://intl.cloud.tencent.com/doc/product/228/6290)을 참조하십시오.

## 액세스 완료

도메인 이름 추가를 완료하려면 [제출]을 클릭하십시오. 도메인 이름 구성이 전체 네트워크 노드에 전달될 때까지 약 5~10 분이 소요됩니다.
![](https://main.qcloudimg.com/raw/0bf658a80d21a62e6bc30a54cbc21ff8.jpg)

>!액세스가 완료되면 Tencent Cloud CDN에서 해당 CNAME 주소를 할당하므로 CDN 서비스를 적용하려면 CNAME 구성을 완료해야 합니다. 자세한 내용은 [CNAME 구성](https://intl.cloud.tencent.com/document/product/228/3121)을 참고하십시오.
