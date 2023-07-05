

当您云服务器购买完成后，您可以在购买的服务器上搭建一个属于自己的网站或者论坛。
<dx-alert infotype="explain" title="">
您也可通过轻量应用服务器（Lighthouse）“一键建站”，无需自行配置，仅在创建时选择所需应用镜像即可完成个人网站搭建。详情请参见 [轻量应用服务器购买方式](https://intl.cloud.tencent.com/document/product/1103/41404)。
</dx-alert>

![](https://main.qcloudimg.com/raw/47d7f76597e7e9318a31ab72590692cb.png)




## 搭建方式
腾讯云针对主流的网站系统，提供了多种类型的建站教程。搭建方式可分镜像部署及手工搭建两种方式，其特点分别为：


<table>
<thead>
<tr>
<th style="
    width: 13%;
">对比项</th>
<th>镜像部署</th>
<th>手动搭建</th>
</tr>
</thead>
<tbody><tr>
<td>搭建方式</td>
<td>选择由腾讯云市场中的系统镜像直接安装部署。</td>
<td>以手动的方式安装所需软件，可定制化。</td>
</tr>
<tr>
<td>特点</td>
<td>配套的软件版本相对比较固定。</td>
<td>配套版本可以灵活选择。</td>
</tr>
<tr>
<td>所需时间</td>
<td>比较短，一键部署。</td>
<td>比较长，需自行安装相关软件。</td>
</tr>
<tr>
<td>难易程度</td>
<td>相对比较简单。</td>
<td>需要对软件配套版本及安装方法有一定的了解。</td>
</tr>
</tbody></table>

## 搭建网站

您可根据实际需求开始搭建不同系统的个人网站：

<table>
	<tr>
	<th width="15%">网站类型</th>
	<th width="18%">搭建方式</th>
	<th>说明</th>
	</tr>
	<tr>
	<td rowspan=2>WordPress</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/8044">手动搭建 WordPress（Linux）</a></td>
	<td rowspan=2>WordPress 是使用 PHP 语言开发的博客平台，用户可以在支持 PHP 和 MySQL 数据库的服务器上架设属于自己的网站。也可以把 WordPress 当作一个内容管理系统（CMS）来使用。</td>
	</tr>
	<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/8044">手动搭建 WordPress（Linux）</a></td>
	</tr>
	<tr>
	<td rowspan=1>Discuz! </td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/8043">手动搭建 Discuz!</a></td>
	<td rowspan=1>Discuz! 是通用的社区论坛，采用 PHP+MySQL 架构开发。用户可在服务器上通过简单的安装配置，部署完善的论坛服务。</td>
	</tr>
	<tr>
	<td rowspan=3>LNMP 环境</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/32733">手动搭建 LNMP 环境<br>（CentOS 7）</a></td>
	<td rowspan=3>	LNMP 环境代表 Linux 系统下 Nginx + MySQL/MariaDB + PHP 组成的网站服务器架构。</td>
	</tr>
	<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/34818">手动搭建 LNMP 环境<br>（CentOS 6）</a></td>
	</tr>
	<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/2127">手动搭建 LNMP 环境<br>（openSUSE）</a></td>
	</tr>
	<tr>
	<td rowspan=1> LAMP 环境</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/34813">手动搭建 LAMP</a></td>
	<td rowspan=1>	LAMP 环境代表 Linux 系统下 Apache + MySQL/MariaDB + PHP 组成的网站服务器架构。</td>
	</tr>
	<tr>
	<td>WIPM 环境</td>
	<td><a href="https://intl.cloud.tencent.com/zh/document/product/213/34813">手动搭建 WIPM</a></td>
	<td>WIPM 环境代表 Windows 系统下 IIS + PHP + MySQL 组成的网站服务器架构。</td>
	</tr>
	<tr>
	<td>Drupal</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/34814">手动搭建 Drupal</a></td>
	<td>Drupal 是使用 PHP 语言编写的开源内容管理框架（CMF），由内容管理系统（CMS）及 PHP 开发框架（Framework）共同构成。用户可使用 Drupal 作为个人或团体网站开发平台。</td>
	</tr>
	<tr>
	<td>Ghost</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/34816">手动搭建 Ghost</a></td>
	<td>Ghost 是基于 Node.js 开发的开源博客平台。具备可快速部署，在线出版物流程简化等功能特点，用户可使用 Ghost 快速搭建个人博客。</td>
	</tr>
		<tr>
	<td>Microsoft SharePoint 2016</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/213/36778">搭建 Microsoft SharePoint 2016</a></td>
	<td>Microsoft SharePoint 是 Microsoft SharePoint Portal Server 的简称，是一个门户站点，可以让企业开发出智能的门户站点。该站点可以无缝连接到团队和知识，使用户能够更好地利用业务流程中的相关信息，更有效地开展工作。</td>
	</tr>
</table>




## 相关操作
个人网站需进行域名注册、网站备案、解析等操作后，网站才可在互联网中被外部访问。当您已在云服务器上部署好个人网站，并计划将网站发布到互联网时准备可用域名。







<style>
	.params{margin-bottom:0px !important;}
</style>
