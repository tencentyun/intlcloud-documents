## CoreOS
2020년 5월 26일 이후 커뮤니티 공식 홈페이지에서 CoreOS Container Linux의 업데이트를 지원하지 않는다고 CoreO 커뮤니티를 통해 발표했습니다. 이에 관련해 Tencent Cloud에서는 다음과 같이 설명했습니다.
-2020년 10월 30일 이후부터 Tencent Cloud에서 제공하는 CoreOS Container Linux를 통해 CVM을 생성할 수 없습니다.
-2020년 5월 26일 이후부터 Tencent Cloud에서는 CoreOS Container Linux의 기술 지원이 제공되지 않습니다. 하지만, CoreOS Container Linux를 통해 이미 설치한 기존의 CVM 인스턴스는 영향을 받지 않고 계속 사용할 수 있습니다. 또한, 해당 운영 체제의 라이프사이클이 끝났고 운영사에서 더는 안전 업데이트 패치를 제공하지 않으므로 Tencent Cloud에서는 해당 이미지 사용 중단을 권장합니다.
- Fedora CoreOS 커뮤니티에서는 Fedora CoreOS 운영 체제를 CoreOS Container Linux로 교체할 것을 권장하며 Tencent Cloud에서는 2020년 9월에 Fedora CoreOS 공용 이미지를 런칭 예정입니다.




### CentOS

<table>
<tr><th style="width: 14%;">이미지 버전</th><th style="width: 42%;">이미지 정보</th><th style="width: 14%;">업데이트 시간</th><th style="width: 30%;">업데이트 내용</th></tr>
	<tr><td>CentOS 8.0</td><td>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-25szkc8t">img-25szkc8t</a><br>커널 버전: 4.18.0-80.11.2.el8_0.x86_64</td><td>2020-08-01</td><td>신규 이미지 런칭.</td></tr>
	<tr>
	<td>CentOS 7.7</td>
	<td>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-1u6l2i9l">img-1u6l2i9l</a><br>커널 버전: 3.10.0-1062.18.1.el7.x86_64</td>
	<td>2020-04-15</td>
	<td>최신 시스템 패치 업데이트.</td>
	</tr>
	<tr>
	<td rowspan=3>CentOS 7.6</td>
	<td rowspan=3> 이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-9qabwvbn">img-9qabwvbn</a><br>커널 버전: 3.10.0-1062.18.1.el7.x86_64</td>
	<td>2020-06-30</td>
	<td>최신 시스템 패치 업데이트.</td>
	</tr>
	<tr>
	<td>2019-12-16</td>
	<td>최신 시스템 패치 업데이트.</td>
	</tr>
	<tr>
	<td>2019-05-06</td>
	<td><ul  class="params"><li>신규 이미지 런칭. </li><li>베어 메탈 지원.</li><li>IPv6 지원.</li></ul></td>
	</tr>
	<tr>
	<td rowspan=2>CentOS 7.5</td>
	<td rowspan=2>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-oikl1tzv">img-oikl1tzv</a><br>커널 버전: 3.10.0-957.27.2.el7.x86_64</td>
	<td>2020-02-10</td>
	<td>최신 시스템 패치 업데이트.</td>
  </tr>
	</tr>
	<tr><td>2019-05-31</td><td><ul class="params"><li>최신 시스템 패치 업데이트.</li><li>IPv6 지원.</li></ul>
</td>
</tr>
<tr>
	<td rowspan=2>CentOS 7.4</td>
	<td rowspan=2>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-8toqc6s3">img-8toqc6s3</a><br>커널 버전: 3.10.0-693.el7.x86_64</td>
	<td>2020-03-01</td>
	<td>최신 시스템 패치 업데이트.</td>
	</tr>
	<tr><td>2019-03-11</td><td>OpenSSH 버전 업데이트.</td></tr>
	<tr>
	<td rowspan=2>CentOS 7.3</td>
	<td rowspan=2>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-dkwyg6sr">img-dkwyg6sr</a><br>커널 버전: 3.10.0-514.21.1.el7.x86_64</td>
	<td>2020-03-15</td>
	<td>최신 시스템 패치 업데이트.</td>
	</tr>
	<tr><td>2019-03-26</td><td>OpenSSH 버전 업데이트.</td></tr>
 <tr>
	<td rowspan=2>CentOS 7.2</td>
	<td rowspan=2>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-31tjrtph">img-31tjrtph</a><br>커널 버전: 3.10.0-514.26.2.el7.x86_64</td>
	<td>2020-03-15</td>
	<td>최신 시스템 패치 업데이트.</td>
	</tr>
	<tr><td>2019-03-26</td><td>OpenSSH 버전 업데이트.</td></tr>
	<tr>
	<td rowspan=2>CentOS 6.9</td>
	<td rowspan=2>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-i5u2lkoz">img-i5u2lkoz</a><br>커널 버전: 2.6.32-754.30.2.el6.x86_64</td>
	<td>2020-03-04</td>
	<td>최신 시스템 패치 업데이트.</td>
	</tr>
	<tr><td>2019-03-26</td><td>OpenSSH 버전 업데이트.</td></tr>
	<tr><td>CentOS 6.8</td><td>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-6ns5om13">img-6ns5om13</a><br>커널 버전: 2.6.32-642.6.2.el6.x86_64</td><td>2019-03-26</td><td>OpenSSH 버전 업데이트.</td></tr>
	</table>


## Debian
<table>
<tr><th style="width: 16%;">이미지 버전</th><th style="width: 38%;">이미지 정보</th><th style="width: 14%;">업데이트 시간</th><th style="width: 32%;">업데이트 내용</th></tr>
	<tr><td>Debian 10.2</td><td>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-h1yvvfw1">img-h1yvvfw1</a><br>커널 버전: 4.19.0-6-amd64</td><td>2020-06-30</td><td>신규 이미지 런칭.</td></tr>
</table>


## OpenSUSE
<table>
<tr><th style="width: 14%;">이미지 버전</th><th style="width: 42%;">이미지 정보</th><th style="width: 14%;">업데이트 시간</th><th style="width: 30%;">업데이트 내용</th></tr>
  <tr>
	<td>OpenSUSE Leap 15.1 </td>
	<td>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-4orfgj3l">img-4orfgj3l</a><br>커널 버전: 4.12.14-lp151.28.36-default</td>
	<td>2020-07-15 </td>
	<td>신규 이미지 런칭.</td>
	</tr>
	<tr>
	<td rowspan=2>OpenSUSE 42.3</td>
	<td rowspan=2>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-0ytr67o7">img-0ytr67o7</a><br>커널 버전: 4.4.76-1-default</td>
	<td>2020-06-04</td>
	<td>최신 시스템 패치 업데이트.</td>
	</tr>
	<tr>
	<td>2019-03-13</td>
	<td>OpenSSH 버전 업데이트.</td>
	</tr>
</table>

## Ubuntu
<table>
<tr><th style="width: 16%;">이미지 버전</th><th style="width: 38%;">이미지 정보</th><th style="width: 14%;">업데이트 시간</th><th style="width: 32%;">업데이트 내용</th></tr>
	<tr>
	<td rowspan=3>Ubuntu 18.04</td>
	<td rowspan=3>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/4/PUBLIC_IMAGE/img-pi0ii46r">img-pi0ii46r</a><br>커널 버전: 4.15.0-88-generic</td>
	<td>2020-03-25</td>
	<td><ul class="params"><li>최신 시스템 패치 업데이트.</li><li>베어 메탈 지원.</li></ul></td>
	</tr>
	<tr><td>2019-06-20</td><td><ul  class="params"><li>시스템 패치 업데이트.</li><li> CVE-2019-11477 취약점 수정.</li></ul>
</td></tr>
	<tr><td>2019-05-15</td><td><ul  class="params"><li>최신 시스템 패치 업데이트.</li><li>베어 메탈 지원.</li></ul>
</td></tr>
	<tr>
	<td>Ubuntu 16.04</td>
	<td rowspan=3>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/4/PUBLIC_IMAGE/img-pyqx34y1">img-pyqx34y1</a><br>커널 버전: 4.15.0-88-generic</td>
	<td>2020-03-25</td>
	<td>최신 시스템 패치 업데이트.</td>
	</tr>
	</table>


## Windows
<table>
<tr><th style="width: 30%;">이미지 버전</th><th style="width: 26%;">이미지 정보</th><th style="width: 14%;">업데이트 시간</th><th style="width: 30%;">업데이트 내용</th></tr>
 <tr>
 <td>Windows Server 2019 데이터센터 버전의 64비트 중국어 버전</td>
 <td>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/4/PUBLIC_IMAGE/img-mmy6qctz">img-mmy6qctz</a></td>
 <td>2020-03-18</td>
 <td>최신 시스템 패치 업데이트.</td>
 </tr>
 <tr>
 <td rowspan=2>Windows Server 2016 데이터센터 버전의 64비트 중국어 버전</td>
 <td rowspan=2>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/4/PUBLIC_IMAGE/img-9id7emv7">img-9id7emv7</a></td>
 <td>	2020-06-02	</td>
 <td>최신 시스템 패치 업데이트.</td>
 </tr>
 	<tr>
	<td>2019-08-19</td>
	<td>Windows-CVE-2019-1125 취약점 수정 및 8월 패치 업데이트.</td>
	</tr>
		<tr>
		<td rowspan=2>Windows Server 2016 데이터센터 버전의 64비트 영어 버전</td>
		<td rowspan=2>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/4/PUBLIC_IMAGE/img-1eckhm4t">img-1eckhm4t</a></td>
		<td>	2020-06-02	</td>
		<td>최신 시스템 패치 업데이트.</td>
		</tr>
			<tr>
	<td>2019-08-19</td>
	<td>Windows-CVE-2019-1125 취약점 수정 및 8월 패치 업데이트.</td>
	</tr>
		<tr>
		<td rowspan=2>Windows Server 2012 R2 데이터센터 버전의 64비트 중국어 버전</td>
		<td rowspan=2>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-29hl923v">img-29hl923v</a></td>
		<td>2020-01-13</td>
		<td>최신 시스템 패치 업데이트.</td>
		</tr>
		<tr>
	<td>2019-08-19</td>
	<td>Windows-CVE-2019-1125 취약점 수정 및 8월 패치 업데이트.</td>
	</tr>
		<tr>
		<td rowspan=2>Windows Server 2012 R2 데이터센터 버전의 64비트 영어 버전</td>
		<td rowspan=2>이미지 ID: <a href="https://console.cloud.tencent.com/cvm/image/detail/1/PUBLIC_IMAGE/img-2tddq003">img-2tddq003</a></td>
		<td>2020-01-13</td>
		<td>최신 시스템 패치 업데이트.</td>
		</tr>
	<tr>
	<td>2019-08-19</td>
	<td>Windows-CVE-2019-1125 취약점 수정 및 8월 패치 업데이트.</td>
	</tr>
</table>


<style>
	.params{margin-bottom:0px !important;}
</style>


