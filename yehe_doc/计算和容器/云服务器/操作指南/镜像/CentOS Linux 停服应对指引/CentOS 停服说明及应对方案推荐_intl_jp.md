
##　CentOSサービス終了の背景
CentOSは、CentOS Linuxプロジェクトのメンテナンスを正式に停止する予定があります。CentOS 8とCentOS 7のメンテナンスを次の表に示します。詳細については、[CentOS公式発表](https://blog.centos.org/2020/12/future-is-centos-stream/?spm=a2c4g.11174386.n2.3.348f4c07hk46v4)をご参照ください。

<table>
<thead>
  <tr>
    <th>OSバージョン</th>
    <th>メンテナンス停止時間</th>
    <th>使用者への影響</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>CentOS 8</td>
    <td>2022年01月01日</td>
    <td rowspan='2'>メンテナンスを停止すると、問題の修正や機能の更新を含むソフトウェアのメンテナンスやサポートを受けることができなくなります。</td>
  </tr>
  <tr>
    <td>CentOS 7</td>
    <td>2024年06月30日</td>
    <td></td>
</tbody>
</table>
このような状況で、CVMインスタンスを新たに購入する場合は、無料のコミュニティ安定版OSであるOpenCloudOS、またはTencentから専門的なサポートを受けられるTencentOS Serverイメージを使用することをお勧めします。

##　OpenCloudOSとTencentOS Serverの紹介
- **OpenCloudOS**はTencentとパートナーの共同イニシアチブにより提出され、完全に中立、全面的に開放され、安全で安定した、高性能なOSおよびエコです。
 -　OpenCloudOSの詳細については、次をご参照ください：[OpenCloudOS概要](https://intl.cloud.tencent.com/document/product/213/46209) 。

-　TencentOS ServerはTencentCloudがクラウドのシナリオに合わせて開発したLinuxオペレーティングシステムであり、特定の機能とパフォーマンスの最適化を提供し、CVMインスタンス内のアプリケーションに、より高いパフォーマンスとより安全で信頼性の高い実行環境を提供します。

###　Linuxディストリビューションのエコサプライチェーンの各フェーズは次のように定義されます
-　OpenCloudOS Streamや有名なFedora/DebianなどのL1上流ディストリビューション。
-　一般的にはTencentOS Server（テンセント）、RHEL（Redhat）、Ubuntu（Canonical）などの会社が主導するL2ビジネス版。
-　OpenCloudOSや旧CentOSディストリビューションなど、ビジネスシステムの無料再発行バージョンであるL3コミュニティ安定版。L2企業版との差異はほとんどありません。
-　L3をベースに最適化・改造、特性のカスタマイズを行ったL4コミュニティ派生版。
![](https://qcloudimg.tencent-cloud.cn/raw/2ceea2b0f8b4ed40c55442d31e4ea950.png)

OpenCloudOSはL3コミュニティ安定版、TencentOS ServerはL2ビジネス版です。OpenCloudOSとTencentOS Serverの関係は、CentOSとレッドハットRHELの関係と一致しています。

OpenCloudOSはTencentOS Serverのビジネス安定版の出力に由来しており、ソースコードにほとんど違いはありません。主な違いは、SLA保証つきのテクニカルサポートサービスを商業的に提供することにあります。

|    |   OpenCloudOS |  TencentOS Server   |
|-------------------|----------------------------------|----------------------------------|
| Kernelバージョン        |  Linux 5.4カーネルベース               | Linux 5.4カーネルベース                                                             |
| ユーザーモード            |  CentOS 8（OpenCloudOS 8.X）対応 | CentOS 7（TencentOS Server 2.4） CentOS 8 （TencentOS Server3.1）対応 |
| テクニカルサポート          | OpenCloudOSコミュニティに依存  | TencentOS Serverテクニカルサポートチームに依存 |
| 欠陥/セキュリティ脆弱性の公開 | コミュニティの公開  | TencentOS Serverテクニカルサポートチームの公開 |

OpenCloudOSはコミュニティ化されたOSで、ユーザーが無料で利用できます。コミュニティ開発者がメンテナンスを行います。
オペレーティングシステムの専門チームによるサービスとメンテナンスが必要な場合は、TencentOS Serverのサブスクリプションサービスを購入するオプションがあります。
##　CentOSの移行ガイド
-　CentOS8からOpenCloudOSへ移行しようとする場合、[CentOSからOpenCloudOSへの移行ガイド](https://www.tencentcloud.com/document/product/213/53801)をご参照ください。
-　CentOSからTencentOS Serverに移行しようとる場合、[CentOS からTencentOSへの移行ガイド](https://intl.cloud.tencent.com/document/product/213/46962)をご参照ください。


