

CVM 구입 후 구입한 서버에서 자신만의 웹 사이트나 포럼을 구축할 수 있습니다.
<dx-alert infotype="explain" title="">
또한 Lighthouse를 통해 ‘원클릭 구축’이 가능하며, 직접 설정할 필요가 없습니다. 생성 시 필요한 애플리케이션 이미지를 선택하기만 하면 개인 웹 사이트 구축을 완료할 수 있습니다. 자세한 내용은 [Lighthouse 구입 방법](https://intl.cloud.tencent.com/document/product/1103/41404)을 참고하십시오.
</dx-alert>

![](https://main.qcloudimg.com/raw/47d7f76597e7e9318a31ab72590692cb.png)




## 구축 방법
Tencent Cloud는 주요 웹 사이트 시스템을 위한 다양한 유형의 튜토리얼을 제공합니다. 구축 방식은 미러 이미지 배포와 수동 구축의 두 종류이며, 그 특징은 다음과 같습니다.


<table>
<thead>
<tr>
<th style="
    width: 13%;
">비교 항목</th>
<th>미러 이미지 배포</th>
<th>수동 구축</th>
</tr>
</thead>
<tbody><tr>
<td>구축 방식</td>
<td>Tencent 클라우드 마켓</a>의 시스템 이미지 직접 설치 및 배포를 선택합니다.</td>
<td>필요한 소프트웨어를 수동으로 설치합니다. 사용자 정의할 수 있습니다.</td>
</tr>
<tr>
<td>특징</td>
<td>패키지 소프트웨어 버전은 비교적 고정되어 있습니다.</td>
<td>패키지 버전을 유연하게 선택할 수 있습니다.</td>
</tr>
<tr>
<td>소요 시간</td>
<td>비교적 짧음. 원클릭 배포.</td>
<td>비교적 김. 관련 소프트웨어 직접 설치.</td>
</tr>
<tr>
<td>난이도</td>
<td>비교적 쉬움.</td>
<td>소프트웨어 패키지 버전과 설치 방법에 대해 어느 정도 이해하고 있어야 합니다.</td>
</tr>
</tbody></table>

## 웹 사이트 구축

실제 필요에 따라 다양한 시스템의 개인 웹 사이트 구축을 시작할 수 있습니다.

<table>
	<tr>
	<th width="15%">웹 사이트 유형</th>
	<th width="18%">구축 방법</th>
	<th>설명</th>
	</tr>
	<tr>
	<td rowspan=2>WordPress</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/8044">WordPress(Linux) 수동 구축</a></td>
	<td rowspan=2>WordPress 는 PHP 언어를 사용해 개발된 블로그 플랫폼입니다. 사용자는 PHP와 MySQL 데이터베이스를 지원하는 서버에 개인 웹 사이트를 구축할 수 있습니다. WordPress를 콘텐츠 관리 시스템(CMS)으로 사용할 수도 있습니다.</td>
	</tr>
	<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/8044">WordPress(Linux) 수동 구축</a></td>
	</tr>
	<tr>
	<td rowspan=1>Discuz! </td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/8043">Discuz! 수동 구축</a></td>
	<td rowspan=1>Discuz!는 PHP+MySQL 아키텍처로 개발된 범용 커뮤니티 포럼입니다. 사용자는 서버에서 간단한 설치 구성을 통해 완전한 포럼 서비스를 배포할 수 있습니다.</td>
	</tr>
	<tr>
	<td rowspan=3>LNMP 환경</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/32733">LNMP 환경 수동 구축<br>(CentOS 7)</a></td>
	<td rowspan=3>LNMP 환경은 Linux 시스템에서 Nginx + MySQL/MariaDB + PHP로 구성된 웹 사이트 서버 아키텍처를 나타냅니다.</td>
	</tr>
	<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/34818">LNMP 환경 수동 구축<br>(CentOS 6)</a></td>
	</tr>
	<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/2127">LNMP 환경 수동 구축<br>(openSUSE)</a></td>
	</tr>
	<tr>
	<td rowspan=1> LAMP 환경</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/34813">LAMP 수동 구축</a></td>
	<td rowspan=1>LAMP 환경은 Linux 시스템에서 Apache + MySQL/MariaDB + PHP로 구성된 웹 사이트 서버 아키텍처를 나타냅니다.</td>
	</tr>
	<tr>
	<td>WIPM 환경</td>
	<td><a href="https://intl.cloud.tencent.com/zh/document/product/213/34813">WIPM 수동 구축</a></td>
	<td>WIPM 환경은 Windows 시스템에서 IIS + PHP + MySQL 로 구성된 웹 사이트 서버 아키텍처를 나타냅니다.</td>
	</tr>
	<tr>
	<td>Drupal</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/34814">Drupal 수동 구축</a></td>
	<td>Drupal은 PHP 언어로 작성된 오픈 소스 콘텐츠 관리 프레임워크(CMF)로, 콘텐츠 관리 시스템(CMS)과 PHP 개발 프레임워크(Framework)로 공동 구성됩니다. 사용자는 Drupal을 개인 또는 그룹 웹 사이트 개발 플랫폼으로 사용할 수 있습니다.</td>
	</tr>
	<tr>
	<td>Ghost</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/34816">Ghost 수동 구축</a></td>
	<td>Ghost는 Node.js 기반의 오픈 소스 블로그 플랫폼입니다. 신속한 배포 및 간소화된 온라인 출판물 프로세스 등 기능 특징을 통해, 사용자는 Ghost로 개인 블로그를 빠르게 구축할 수 있습니다.</td>
	</tr>
		<tr>
	<td>Microsoft SharePoint 2016</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/36778">Microsoft SharePoint 2016 구축</a></td>
	<td>Microsoft SharePoint는 Microsoft SharePoint Portal Server 의 약칭으로 기업이 지능형 포털 사이트를 개발할 수 있는 포털 사이트입니다. 이 사이트는 사용자가 비즈니스 프로세스에서 관련 정보를 더 잘 이용하고 더 효율적으로 작업할 수 있도록 합니다.</td>
	</tr>
</table>




## 관련 작업
개인 웹 사이트는 도메인 가입, 웹 사이트 ICP 비안, 리졸브 등의 작업을 거친 후에야 외부 액세스가 가능합니다. 개인 웹 사이트를 CVM에 배치 완료했으며, 웹 사이트를 인터넷에 배포할 계획인 경우, 사용 가능한 도메인을 준비합니다.







<style>
	.params{margin-bottom:0px !important;}
</style>
