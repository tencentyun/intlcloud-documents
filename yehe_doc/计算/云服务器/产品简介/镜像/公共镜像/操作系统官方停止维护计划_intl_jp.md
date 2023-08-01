Tencent Cloudが提供するパブリックイメージのメンテナンスサイクルは公式に発表されているメンテナンスサイクルと一致します。このドキュメントでは、各バージョンのイメージに対するOSプラットフォームごとのメンテナンスプランを確認できます。

>!OSのメンテナンスが終了すると、問題の修正や機能の更新を含むソフトウェアのメンテナンスやサポートを受けることができなくなります。最新のバージョンに更新するか、より安定したイメージバージョンを選択することをお勧めします。



## Tencent Cloud独自開発OS

### TencentOS Server
<table>
	<tr>
		<th width="50%">バージョン</th>
		<th>メンテナンス終了日</th>
	</tr>
	<tr>
		<td>TencentOS Server 2</td>
		<td>2027-12-31</td>
	</tr>
	<tr>
		<td>TencentOS Server 3</td>
		<td>2029-12-31</td>
	</tr>
</table>





### OpenCloudOS
<table>
	<tr>
		<th width="50%">バージョン</th>
		<th>メンテナンス終了日</th>
	</tr>
	<tr>
		<td>OpenCloudOS 8</td>
		<td>2029-12</td>
		</tr>
</table>



## サードパーティ製OS

### CentOS
<table>
	<tr>
		<th width="40%">バージョン</th>
		<th width="30%">完全更新終了日</th>
		<th width="30%">メンテナンス更新終了日</th>	
	</tr>
	<tr>
		<td>CentOS Stream 9</td>
		<td>2027-05-31</td>
		<td>2027-05-31</td>
	</tr>
	<tr>
		<td>CentOS Stream 8</td>
		<td>2024-05-31</td>
		<td>2024-05-31</td>
	</tr>
		<tr>
		<td>CentOS 8</td>
		<td>2021-12-31</td>
		<td>2021-12-31</td>
	</tr>
		<tr>
		<td>CentOS 7</td>
		<td>2020-08-06</td>
		<td>2024-06-30</td>
	</tr>
		<tr>
		<td>CentOS 6</td>
		<td>2017-05-10</td>
		<td>2020-11-30</td>
	</tr>
</table>

公式メンテナンスプランの詳細については、[CentOS公式サイト](https://wiki.centos.org/About/Product)をご参照ください。
>?CentOS は、CentOS Linux のサポートを正式に終了する予定です。 Tencent Cloudは、代替案としてCentOS互換のOpenCloudOSまたはTencentOS Serverを提供しています。



### Ubuntu
<table>
	<tr>
		<th width="40%">バージョン</th>
		<th width="30%">標準サポート終了日</th>
		<th width="30%">拡張更新終了日</th>	
	</tr>
	<tr>
		<td>Ubuntu 22.04 LTS</td>
		<td>2027-04</td>
		<td>2032-04</td>
	</tr>
		<tr>
		<td>Ubuntu 20.04 LTS</td>
		<td>2025-04</td>
		<td>2030-04</td>
	</tr>
		<tr>
		<td>Ubuntu 18.04 LTS</td>
		<td>2023-04</td>
		<td>2028-04</td>
	</tr>
		<tr>
		<td>Ubuntu 16.04 LTS</td>
		<td>2021-04</td>
		<td>2026-04</td>
	</tr>
</table>


公式メンテナンス プランの詳細については、[Ubuntu公式サイト](https://wiki.ubuntu.com/Releases)をご参照ください。



### Debian
<table>
	<tr>
		<th width="20%">バージョン</th>
		<th width="20%">サポート終了日</th>
		<th width="30%">EOL-長期サポート終了日（LTS）</th>
		<th width="30%">EOL-延長・長期サポート終了日（ELTS）</th>
	</tr>
	<tr>
		<td>Debian 11</td>
		<td>2024-07</td>
		<td>2026-06</td>
		<td>なし
	</tr>
	<tr>
		<td>Debian 10</td>
		<td>2022-07</td>
		<td>2024-06</td>
		<td>2029-06-30</td>
	</tr>
	<tr>
		<td>Debian 9</td>
		<td>2020-07-06</td>
		<td>2022-06-30</td>
		<td>2027-06-30</td>
	</tr>
</table>


公式メンテナンス プランの詳細については、[Debian公式サイト](https://wiki.debian.org/DebianReleases)をご参照ください。



### Red Hat Enterprise Linux

<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky">バージョン</th>
    <th class="tg-0pky">フルサポート終了日</th>
    <th class="tg-0pky">メンテナンスサポート 1 の終了日</th>
    <th class="tg-0pky">メンテナンスサポート2の終了日</th>
    <th class="tg-0pky">延長ライフサイクルサポートの終了日</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">Red Hat Enterprise Linux 8</td>
    <td class="tg-0pky">2024-05-31</td>
    <td class="tg-0pky">非該当</td>
    <td class="tg-0pky">2029-05-31</td>
    <td class="tg-0pky">2031-05-31</td>
  </tr>
  <tr>
    <td class="tg-0pky">Red Hat Enterprise Linux 7</td>
    <td class="tg-0pky">2019-08-06</td>
    <td class="tg-0pky">2020-08-06</td>
    <td class="tg-0pky">2024-06-30</td>
    <td class="tg-0pky">2026-06-30</td>
  </tr>
</tbody>
</table>

詳細については、[Red Hat公式サイト](https://access.redhat.com/support/policy/updates/errata)をご参照ください。

<dx-alert infotype="explain" title="">

- Red Hat Enterprise Linux イメージは現在ベータ版テスト版実施中で、ベータ版ユーザになろうとする方は、 [チケットを送信](https://console.tencentcloud.com/workorder/category)してください。
- CVMを購入したときにRed Hat Enterprise Linux認証に合格したインスタンスタイプを選択した場合は、 Red Hat Enterprise Linuxイメージを使用できます。サポートされているイメージタグとインスタンスタイプについては、 [Red Hat Enterprise Linux イメージに関するよくあるご質問](https://www.tencentcloud.com/document/product/213/55135)をご参照ください。
</dx-alert> 

 

### AlmaLinux
<table>
	<tr>
		<th width="50%">バージョン</th>
		<th>メンテナンス終了日</th>
	</tr>
	<tr>
		<td>AlmaLinux 8.5</td>
		<td>2031-11</td>
	</tr>
</table>

公式メンテナンス プランの詳細については、[AlmaLinux公式サイト](https://wiki.almalinux.org/Comparison.html)をご参照ください。


### CoreOS
<table>
	<tr>
		<th width="50%">バージョン</th>
		<th>メンテナンス終了日</th>
	</tr>
	<tr>
		<td>CoreOS Container Linux </td>
		<td>2020-05-26</td>
	</tr>
</table>


### FreeBSD
<table>
	<tr>
		<th width="50%">バージョン</th>
		<th>メンテナンス終了日</th>
	</tr>
	<tr>
		<td> FreeBSD 13.1</td>
		<td>2023-06-30</td>
	</tr>
	<tr>
		<td>FreeBSD 13.0</th>
		<td>2022-08-31</td>
	</tr>
	<tr>
		<td>FreeBSD 12.3</td>
		<td>2023-03-31</td>
	</tr>
	<tr>
		<td>FreeBSD 12.2</td>
		<td>2022-03-31</td>
	</tr>
</table>


公式メンテナンスプランの詳細については、[FreeBSD公式サイト](https://www.freebsd.org/releases/)をご参照ください。



### Rocky Linux
<table>
	<tr>
		<th width="50%">バージョン</th>
		<th>メンテナンス終了日</th>
	</tr>
	<tr>
		<td>Rocky Linux 9.0</td>
		<td>2032-05-31</td>
	</tr>
		<tr>
		<td>Rocky Linux 8.6</td>
		<td>2029-05-31</td>
	</tr>
	<tr>
		<td>Rocky Linux 8.5</td>
		<td>2029-05-31</td>
	</tr>
</table>


公式メンテナンスプランの詳細については、[Rocky Linux公式サイト](https://rockylinux.org/news/rocky-linux-9-0-ga-release/)をご参照ください。



### OpenSUSE

<table>
	<tr>
		<th width="50%">バージョン</th>
		<th>メンテナンス終了日</th>
	</tr>
		<tr>
		<td>OpenSUSE Leap 15.4</td>
		<td>2023-11</td>
	</tr>
	<tr>
		<td>OpenSUSE Leap 15.3</td>
		<td>2022-11</td>
	</tr>
	<tr>
		<td>OpenSUSE Leap 15.2</th>
		<td>2022-01-04</td>
	</tr>
	<tr>
		<td>OpenSUSE Leap 15.1</td>
		<td>2021-02-02</td>
	</tr>
</table>


公式メンテナンスプランの詳細については、[OpenSUSE公式サイト](https://en.opensuse.org/Lifetime)をご参照ください。



### Windows
<table>
	<tr>
		<th width="40%">バージョン</th>
		<th width="30%">メインストリームサポート終了日</th>
		<th width="30%">延長サポート終了日</th>	
	</tr>
	<tr>
		<td>Windows Server 2022 Datacenter</td>
		<td>2026-10-13</td>
		<td>2031-10-14</td>
	</tr>
		<tr>
		<td>Windows Server 2019 Datacenter</td>
		<td>2024-01-09</td>
		<td>2029-01-09</td>
	</tr>
		<tr>
		<td>Windows Server 2016 Datacenter</td>
		<td>2022-01-11</td>
		<td>2027-01-12</td>
	</tr>
		<tr>
		<td>Windows Server 2012 R2 Datacenter</td>
		<td>2018-10-09</td>
		<td>2023-10-10</td>
	</tr>
</table>


公式メンテナンスプランの詳細については、[Microsoft Windows Server公式サイト]をご参照ください。


