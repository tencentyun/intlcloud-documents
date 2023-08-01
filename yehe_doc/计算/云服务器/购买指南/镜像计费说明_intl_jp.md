このドキュメントでは、CVMイメージの料金の詳細について説明します。

## 料金の概要
イメージを使用すると、一定の料金が発生します。各タイプのイメージの料金の詳細は次のとおりです：
<table class="tg">
<thead>
  <tr>
    <th width="10%">イメージタイプ</th>
    <th width="90%">説明</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">パブリックイメージ</td>
    <td class="tg-0pky">オープンソースイメージと商用イメージを含む：<br><li>オープンソースイメージはすべて無料で提供されています。</li><li>商用イメージを使用すると、ライセンス利用料金が発生します。Tencent Cloud は現在、Windows Server イメージと Red Hat Enterprise Linux イメージの 2 つの商用イメージを提供しています。</td></li>
  </tr>
  <tr>
    <td class="tg-0pky">カスタム イメージ</td>
    <td class="tg-0pky">カスタムイメージの費用は次の2 つのコンポーネントで構成：<br><li>スナップショット料金：イメージの基盤となるデータストレージは、CBSスナップショットサービスを使用しているため、カスタムイメージを保持すると、スナップショット料金が発生します。中国本土には 80GBの <a href="https://intl.cloud.tencent.com/document/product/362/32415">無料枠</a>が提供されます。使用量が80GBを超えた分は、従量課金となります。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/362/32415">スナップショットの請求</a>をご参照ください。</li><li>イメージ料金：カスタムイメージのソースが有料イメージである場合、そのカスタムイメージを使用すると料金が発生します。</li></td>
  </tr>
  <tr>
    <td class="tg-0pky">共有イメージ</td>
    <td class="tg-0pky">共有イメージは、作成されたカスタムイメージを他のTencent Cloudアカウントに共有したものです。イメージのソースが有料イメージである場合、その共有イメージを使用すると料金が発生します。</td>
  </tr>
</tbody>
</table>

<span id="redhat"></span>

## Windows Server イメージの請求
#### 課金の例

インスタンス仕様: シンガポール 1、標準 S5.MEDIUM2、従量課金制。
- Windows インスタンスの料金は 0.05 USD/時間です。「イメージ」項目は別途課金されません。つまり、0 USDとして表示されます。下図に示すとおり：
![](https://qcloudimg.tencent-cloud.cn/raw/af8b0002847ce5f1542a90a1990e27ce.png)


## Red Hat Enterprise Linux イメージの請求
Red Hat Enterprise Linuxは商用 Linux ディストリビューションです。イメージ料金にはライセンス料が含まれております。料金は、Tencent Cloud のすべてのリージョンで同じです。
<dx-alert infotype="explain" title="">
- Tencent Cloud での Red Hat Enterprise Linux イメージのライセンスの購入には、割引 (スポット インスタンスの割引を含む) とクーポンは適用されません。
- CVMの購入時にRed Hat Enterprise Linux認証に合格したインスタンスタイプを選択した場合は、 Red Hat Enterprise Linuxイメージを使用できます。サポートされているイメージタグとインスタンスタイプについては、 [Red Hat Enterprise Linux イメージに関するよくあるご質問](https://www.tencentcloud.com/document/product/213/55135)
をご参照ください。
- Red Hat Enterprise Linux イメージは現在ベータ版テスト版実施中で、ベータ版ユーザになろうとする方は、 [チケットを送信](https://console.tencentcloud.com/workorder/category)してください。
</dx-alert>

###  Tencent Cloud によって認可された Red Hat Enterprise Linux イメージの料金は下の表をご覧ください。

| ‍インスタンス仕様 | 時間単位の従量課金（1 時間未満の時間は 1 時間として課金）|
|---------|---------|
| 4 vCPU およびそれ以下 |0.06 USD/時間 |
| 4 vCPU 以上 | 0.13USD/小时 |

<dx-alert infotype="explain" title="">
**スポットインスタンス**の作成時にライセンス付きの Red Hat Enterprise Linux イメージを選択した場合、イメージの料金は従量制で請求され、**スポットインスタンス**の割引が適用されません。
</dx-alert>

### OS再インストール後のイメージの請求
-  Red Hat Enterprise Linux OSと他のOS間の切り替えをサポート（説明：中国本土以外の地域では、Windows と Linux 間の切り替えをサポートしません）し、イメージの料金は新たなイメージに基づいて計算されます。‍
-従量課金制インスタンスの場合、Red Hat Enterprise Linux を使用してインスタンス OS を再インストールすると、イメージに対して従量制で請求されます。Red Hat Enterprise Linux イメージが請求サイクル中に使用される場合は、そのサイクル中に発生したイメージライセンス料金を支払う必要があります。
**例**：
2023 年 1 月 1 日の午前 8 時に CentOS インスタンスを購入した、午前 8 時から 9 時まではイメージのライセンス料は発生しません。午前 9 時 30 分に、Red Hat Enterprise Linux を使用してインスタンス OS を再インストールし、午前 9 時から 10 時までの請求サイクルに対してイメージのライセンス料を支払う必要があります。午前 10 時 30 分に、CentOS を使用してインスタンス OS を再インストールし、午前 10 時から 11 時までの請求サイクルに対してイメージのライセンス料を支払う必要があります。 午前 11 時以降は、イメージのライセンス料を支払う必要はありません。

### RIモードでのイメージの請求
- Linux インスタンスに RI を選択する場合は、Red Hat Enterprise Linux イメージのライセンス料を別途支払う必要があります。
- Tencent Cloudによって認可された Red Hat Enterprise Linux イメージを使用した従量課金制インスタンスは、インスタンス使用の属性が RI の属性に一致すれば、RI の割引料金が自動的に請求書に適用されます。ただし、イメージのライセンス料には割引は適用されず、別途請求されます。


### 構成の変更

Red Hat Enterprise Linux OS を使用するインスタンスの構成と課金モードは変更できません。



