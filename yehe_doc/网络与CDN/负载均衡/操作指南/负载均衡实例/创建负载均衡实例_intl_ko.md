Tencent Cloud는 공식 웹 사이트 구매 및 API 구매의 두 가지 CLB(Cloud Load Balancer) 구매 방식을 제공합니다. 이 섹션에서는 두 가지 구매 방식에 대해 자세히 설명합니다.

## [공식 웹사이트에서 구매](id:Official-Purchase)
[Tencent Cloud 공식 웹사이트](https://buy.cloud.tencent.com/lb)에서 CLB 인스턴스를 구매할 수 있습니다. Tencent Cloud 계정에는 IP별 청구 계정과 CVM별 청구 계정의 두 가지 유형이 있습니다. 2020년 6월 17일(베이징 시간) 00:00:00 이후에 생성된 계정은 IP별 청구 유형입니다. 그 이전에 계정을 생성했다면 [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246)의 안내에 따라 콘솔에서 계정 유형을 확인할 수 있습니다.

1. [CLB 구매 페이지](https://buy.cloud.tencent.com/lb)에 로그인합니다.
2. 필요에 따라 다음 CLB 구성 항목을 선택합니다.
<dx-accordion>
::: IP별 청구 계정
<table>
<thead>
<tr>
<th width="18%">매개변수</th>
<th width="82%">설명</th>
</tr>
</thead>
<tbody>
<tr>
<td><span style="font-weight:bold">과금 방식</span></td>
<td>
종량제 과금 방식이 지원됩니다.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">리전</span></td>
<td>
리전을 선택하십시오. CLB에서 지원하는 리전에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/214/33792">Region List</a>를 참고하십시오.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">인스턴스 유형</span></td>
<td>
CLB 인스턴스 유형만 지원됩니다.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">네트워크 유형</span></td>
<td>네트워크 유형에는 공중망과 사설망의 두 가지가 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/214/13629#network-type">Network Types</a>를 참고하십시오.
	<ul>
	<li>공중망: CLB는 공중망의 요청을 분산하는 데 사용됩니다.</li>
	<li>사설망: CLB는 Tencent Cloud 사설망의 요청을 분산하는 데 사용됩니다. 사설망 인스턴스는 <strong>EIP</strong>, <strong>IP 버전</strong>, <strong>ISP 유형</strong>, <strong>인스턴스 사양</strong>, <strong>네트워크 과금 방식</strong> 및 <strong>대역폭 한도</strong>와 같은 구성 항목을 지원하지 않으며 기본적으로 표시하지 않습니다.</li>
	</ul>
	지원되는 네트워크 유형은 과금 방식에 따라 다릅니다.
	<ul>
	<li>종량제 과금 방식에서는 공중망 및 사설망 유형이 모두 지원됩니다.</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">IP 버전</span></td>
<td>
IPv4, IPv6 및 IPv6 NAT64와 같은 CLB IP 버전이 지원됩니다. 종량제 인스턴스만 IPv6 버전을 지원합니다. 기타 제한 사항에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/214/13629#IP-type">IP Versions</a>를 참고하십시오.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">네트워크</span></td>
<td>
CLB는 기본 네트워크와 VPC를 지원합니다.
	<ul>
	<li>기본 네트워크는 모든 Tencent Cloud 사용자를 위한 공중망 리소스 풀입니다. 모든 CVM의 사설망 IP는 Tencent Cloud에서 할당합니다. IP 범위 또는 IP 주소를 사용자 지정할 수 없습니다.</li>
	<li>VPC는 Tencent Cloud에서 논리적으로 격리된 네트워크 공간입니다. VPC에서 IP 범위, IP 주소 및 라우팅 정책을 사용자 지정할 수 있습니다.</li>
	</ul>
	두 옵션 중에서 VPC는 사용자 지정 네트워크 구성이 필요한 시나리오에 더 적합하며 기본 네트워크 제품은 2022년 12월 31일에 공식적으로 중단됩니다. VPC를 선택하는 것이 좋습니다.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">ISP 유형</span></td>
<td>
BGP, China Mobile, China Telecom 및 China Unicom과 같은 ISP 유형이 지원됩니다.
	<ul>
	<li>종량제 과금 방식에서는 상기 네 가지 옵션이 모두 지원됩니다.
현재 고정 단일 회선 IP는 광저우, 상하이, 난징, 지난, 항저우, 푸저우, 베이징, 스자좡, 우한, 창사, 청두, 충칭에서만 지원됩니다. 다른 리전은 콘솔을 참고하십시오. 사용을 원하시면 영업 담당자에게 문의하여 신청하십시오. 승인되면 구매 페이지에서 ISP(China Mobile, China Unicom 또는 China Telecom)를 선택할 수 있습니다.
	</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">기본/보조 가용존</span></td>
<td>기본 가용존(AZ)은 현재 트래픽을 유지하는 AZ입니다. 보조 AZ는 기본적으로 트래픽을 유지하지 않으며 기본 AZ를 사용할 수 없는 경우에만 사용됩니다. 현재 광저우, 상하이, 난징, 베이징, 중국홍콩 및 서울 지역의 IPv4 CLB 인스턴스만 기본/보조 AZ를 지원합니다.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">인스턴스 사양</span></td>
<td>공유 인스턴스가 지원됩니다.
	<ul>
	<li>여러 공유 인스턴스는 리소스를 공유하고 단일 인스턴스는 성능을 보장하지 않습니다. 기본적으로 모든 인스턴스는 공유 인스턴스입니다.</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">네트워크 과금 방식</span></td>
<td>다음 네트워크 과금 방식이 지원됩니다: 대역폭 과금(월간 대역폭), 대역폭 과금(시간당 대역폭), 트래픽별 과금 및 대역폭 패키지.
	<ul>
	<li>종량제 인스턴스는 대역폭(시간당 대역폭) 과금과 트래픽 과금의 두 가지 네트워크 과금 방식를 지원합니다.</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">대역폭 최댓값</span></td>
<td>1-1024Mbps.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">프로젝트</span></td>
<td>프로젝트를 선택합니다.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">태그</span></td>
<td>태그 키와 값을 선택합니다. <a href="https://intl.cloud.tencent.com/document/product/651/41575">Creating Tags and Binding Resources</a>의 지침에 따라 태그를 생성할 수도 있습니다.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">인스턴스 이름</span></td>
<td>이름에는 최대 60자의 영어 알파벳, 숫자, 중국어, 하이픈‘-’, 밑줄‘_’ 및 마침표‘.’를 사용할 수 있습니다. 지정하지 않으면 기본적으로 이름이 자동으로 생성됩니다.
</td>
</tr>
</tbody></table>
:::
::: CVM별 청구 계정

<table>
<thead>
<tr>
<th width="18%">매개변수</th>
<th width="82%">설명</th>
</tr>
</thead>
<tbody>
<tr>
<td><span style="font-weight:bold">과금 방식</span></td>
<td>
종량제 과금 방식만 지원됩니다.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">리전</span></td>
<td>
리전을 선택하십시오. CLB에서 지원하는 리전에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/214/33792">Region List</a>를 참고하십시오.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">인스턴스 유형</span></td>
<td>
CLB 인스턴스 유형만 지원됩니다.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">네트워크 유형</span></td>
<td>네트워크 유형에는 공중망과 사설망의 두 가지가 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/214/13629#network-type">Network Types</a>를 참고하십시오.
	<ul>
	<li>공중망: CLB는 공중망의 요청을 분산하는 데 사용됩니다.</li>
	<li>사설망: CLB는 Tencent Cloud 사설망의 요청을 분산하는 데 사용됩니다. 사설 네트워크 인스턴스는 <strong>IP 버전</strong>, <strong>ISP 유형</strong>, <strong>인스턴스 사양</strong>과 같은 구성 항목을 지원하지 않으며 기본적으로 표시되지 않습니다.</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">IP 버전</span></td>
<td>
IPv4, IPv6 및 IPv6 NAT64와 같은 CLB IP 버전이 지원됩니다. 사용 제한에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/214/13629#IP-type">IP Versions</a>를 참고하십시오.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">네트워크</span></td>
<td>
CLB는 기본 네트워크와 VPC를 지원합니다.
	<ul>
	<li>기본 네트워크는 모든 Tencent Cloud 사용자를 위한 공중망 리소스 풀입니다. 모든 CVM의 사설망 IP는 Tencent Cloud에서 할당합니다. IP 범위 또는 IP 주소를 사용자 지정할 수 없습니다.</li>
	<li>VPC는 Tencent Cloud에서 논리적으로 격리된 네트워크 공간입니다. VPC에서 IP 범위, IP 주소 및 라우팅 정책을 사용자 지정할 수 있습니다.</li>
	</ul>
	두 옵션 중에서 VPC는 사용자 지정 네트워크 구성이 필요한 시나리오에 더 적합하며 기본 네트워크 제품은 2022년 12월 31일에 공식적으로 중단됩니다. VPC를 선택하는 것이 좋습니다.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">ISP 유형</span></td>
<td>
BGP, China Mobile, China Telecom 및 China Unicom과 같은 ISP 유형이 지원됩니다.<br/>
현재 고정 단일 회선 IP는 광저우, 상하이, 난징, 지난, 항저우, 푸저우, 베이징, 스자좡, 우한, 창사, 청두, 충칭에서만 지원됩니다. 다른 리전은 콘솔을 참고하십시오. 사용을 원하시면 영업 담당자에게 문의하여 신청하십시오. 승인되면 구매 페이지에서 ISP(China Mobile, China Unicom 또는 China Telecom)를 선택할 수 있습니다.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">인스턴스 사양</span></td>
<td>공유 인스턴스가 지원됩니다.
	<ul>
	<li>여러 공유 인스턴스는 리소스를 공유하고 단일 인스턴스는 성능을 보장하지 않습니다. 기본적으로 모든 인스턴스는 공유 인스턴스입니다.</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">프로젝트</span></td>
<td>프로젝트를 선택합니다.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">태그</span></td>
<td>태그 키와 값을 선택합니다. <a href="https://intl.cloud.tencent.com/document/product/651/41575">Creating Tags and Binding Resources</a>의 지침에 따라 태그를 생성할 수도 있습니다.
</td>
</tr>
<tr>
<td><span style="font-weight:bold">인스턴스 이름</span></td>
<td>이름에는 최대 60자의 영어 알파벳, 숫자, 중국어, 하이픈‘-’, 밑줄‘_’ 및 마침표‘.’를 사용할 수 있습니다. 지정하지 않으면 기본적으로 이름이 자동으로 생성됩니다.
</td>
</tr>
</tbody></table>
:::
</dx-accordion>

4. 상기 구성을 완료한 후 수량과 요금을 확인하고 **즉시 구매**를 클릭합니다.
 -  종량제 과금 방식: ‘확인’ 팝업 창에서 **확인**을 클릭합니다.
5. 구매에 성공하면 CLB가 활성화되고 CLB 인스턴스를 구성하여 사용할 수 있습니다.

### [공유 인스턴스 구매 방법](id:Shared-CLB-Instance)
1. [CLB 구매 페이지](https://buy.cloud.tencent.com/lb)에 로그인합니다.
2. [공식 웹 사이트에서 구매](#Official-Purchase) 항목을 참고하여 공유 인스턴스 구성 항목을 설정하고 ‘인스턴스 사양’으로 **공유**를 선택합니다.
![]()
3. [공식 웹 사이트에서 구매](#Official-Purchase)의 단계를 참고하여 후속 작업을 완료합니다.

### [LCU 인스턴스 구매 방법](id:LCU-CLB-Instance)
1. [CLB 구매 페이지](https://buy.cloud.tencent.com/lb)에 로그인합니다.
2. [공식 웹사이트에서 구매](#Official-Purchase)의 단계를 참고하여 LCU 지원 인스턴스 구성 항목을 설정하고 ‘인스턴스 사양’으로 **LCU**를 선택합니다.

3. [공식 웹 사이트에서 구매](#Official-Purchase)의 단계를 참고하여 후속 작업을 완료합니다.


## [API를 통한 구매](id:API-Purchase)
API를 통해 CLB 인스턴스를 구매하려면 [CreateLoadBalancer](https://intl.cloud.tencent.com/document/product/214/33841)를 참고하십시오.

## 후속 작업
- CLB 인스턴스에 대한 리스너를 생성하려면 [CLB Listener Overview](https://intl.cloud.tencent.com/document/product/214/6151)를 참고하시기 바랍니다.
- [Real Server Overview](https://intl.cloud.tencent.com/document/product/214/32388)에 설명된 대로 CLB 리스너를 리얼 서버에 바인딩할 수 있습니다.

## 관련 문서
[Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629)
