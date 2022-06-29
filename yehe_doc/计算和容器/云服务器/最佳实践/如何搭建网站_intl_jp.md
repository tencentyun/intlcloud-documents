

CVMの購入が完了したら、購入したサーバーにご自分のウェブサイトやフォーラムを構築することができます。
<dx-alert infotype="explain" title="">
またLighthouseを使用すれば、「ワンクリックでのサイト構築」もでき、手動での設定が不要になります。作成時に必要なアプリケーションイメージを選択するだけで、個人のウェブサイトを構築することができます。詳細については、[Lighthouseの購入方法](https://intl.cloud.tencent.com/document/product/1103/41404)をご参照ください。
</dx-alert>

![](https://main.qcloudimg.com/raw/47d7f76597e7e9318a31ab72590692cb.png)




## 構築方法
Tencent Cloudは、主流のウェブサイトシステム向けに、さまざまなタイプのウェブサイト構築チュートリアルを提供しています。構築方法にはイメージデプロイと手動構築という2種類があり、それぞれ以下のような特徴を持っています。


<table>
<thead>
<tr>
<th style="
    width: 13%;
">比較項目</th>
<th>イメージのデプロイ</th>
<th>手動構築</th>
</tr>
</thead>
<tbody><tr>
<td>構築方法</td>
<td>Tencentクラウドマーケット</a>のシステムイメージから直接インストールしてデプロイすることを選択します。</td>
<td>必要なソフトウェアを手動でインストールすると、カスタマイズが可能です。</td>
</tr>
<tr>
<td>特徴</td>
<td>付属のソフトウェアのバージョンは比較的固定されています。</td>
<td>付属バージョンもフレキシブルに選択することができます。</td>
</tr>
<tr>
<td>所要時間</td>
<td>比較的短い時間で、ワンクリックでデプロイできます。</td>
<td>比較的時間がかかり、手動で関連ソフトをインストールする必要があります。</td>
</tr>
<tr>
<td>難易度</td>
<td>比較的簡単です。</td>
<td>ソフトウェアパッケージのバージョンとインストール方法について、ある程度理解している必要があります。</td>
</tr>
</tbody></table>

## サイトの構築

実際のニーズに応じて、さまざまなシステムで個人のウェブサイトを構築することができます。

<table>
	<tr>
	<th width="15%">ウェブサイトタイプ</th>
	<th width="18%">構築方法</th>
	<th>説明</th>
	</tr>
	<tr>
	<td rowspan=2>WordPress</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/8044">WordPress(Linux)の手動構築</a></td>
	<td rowspan=2>WordPressは、PHP言語を使用して開発されたブログプラットフォームです。ユーザーは、PHPとMySQLデータベースをサポートするサーバーに、自分のウェブサイトを設置することができます。また、WordPressをコンテンツ管理システム(CMS)として使用することも可能です。</td>
	</tr>
	<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/8044">WordPress(Linux)の手動構築</a></td>
	</tr>
	<tr>
	<td rowspan=1>Discuz! </td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/8043">Discuz!の手動構築</a></td>
	<td rowspan=1>Discuz!は、PHP+MySQLアーキテクチャを使用して開発された汎用型のコミュニティフォーラムです。ユーザーは、サーバーへの簡単なインストールと設定により、パーフェクトなフォーラムサービスをデプロイすることができます。</td>
	</tr>
	<tr>
	<td rowspan=3>LNMP環境</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/32733">LNMP環境の手動構築<br>（CentOS 7）</a></td>
	<td rowspan=3>	LNMP環境は、LinuxシステムでNginx+MySQL/MariaDB+PHPで構成されるウェブサイトサーバーアーキテクチャを表しています。</td>
	</tr>
	<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/34818">LNMP環境の手動構築<br>（CentOS 6）</a></td>
	</tr>
	<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/2127">LNMP環境の手動構築<br>（openSUSE）</a></td>
	</tr>
	<tr>
	<td rowspan=1> LAMP環境</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/34813">LAMPの手動構築</a></td>
	<td rowspan=1>	LAMP環境は、LinuxシステムでApache+MySQL/MariaDB+PHPで構成されるウェブサイトサーバーアーキテクチャを表しています。</td>
	</tr>
	<tr>
	<td>WIPM環境</td>
	<td><a href="https://intl.cloud.tencent.com/zh/document/product/213/34813">WIPMの手動構築</a></td>
	<td>WIPM環境は、Windowsシステム上のIIS+PHP+MySQLで構成されるウェブサイトサーバーアーキテクチャを表しています。</td>
	</tr>
	<tr>
	<td>Drupal</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/34814">Drupalの手動構築</a></td>
	<td>Drupalは、PHP言語で記述されたオープンソースのコンテンツ管理フレームワーク(CMF)であり、コンテンツ管理システム(CMS)とPHP開発フレームワーク(Framework)で構成されています。ユーザーは、個人またはグループでのウェブサイト開発のプラットフォームとしてDrupalを使用することができます。</td>
	</tr>
	<tr>
	<td>Ghost</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/34816">Ghostの手動構築</a></td>
	<td>Ghostは、Node.jsをベースとして開発されたオープンソースのブログプラットフォームです。すばやいデプロイや簡素化されたオンライン公開プロセスといった機能的特徴により、ユーザーはGhostを使用すれば、個人のブログをすばやく作成することができます。</td>
	</tr>
		<tr>
	<td>Microsoft SharePoint 2016</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/36778">Microsoft SharePoint 2016の構築</a></td>
	<td>Microsoft SharePointとは、Microsoft SharePoint Portal Serverの略称で、企業がインテリジェントなポータルサイトを開発できるようにするためのポータルサイトです。このサイトではチームやナレッジとシームレスにつながることができ、ユーザーは関連情報をビジネスプロセスで有効活用し、業務をより効率的に進められるようになります。</td>
	</tr>
</table>




## 関連する操作
個人のウェブサイトは、インターネット上で外部からアクセスできるようになるまでに、ドメイン名の登録、ウェブサイトのICP登録、解決などの作業が必要です。CVMに個人のサイトをデプロイ済みで、インターネットに公開することを予定している場合は、使用可能なドメイン名を準備します。







<style>
	.params{margin-bottom:0px !important;}
</style>
