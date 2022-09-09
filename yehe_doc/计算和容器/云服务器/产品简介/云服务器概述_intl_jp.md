## Tencent Cloud Virtual Machineとは

Tencent Cloud Virtual Machine（CVM）はTencent Cloudが提供する拡張可能なコンピューティングサービスです。 CVMを使用することで、従来型サーバーの使用においてリソース量と先行投資を見積もる必要がなくなり、短時間で任意の数のCVMを迅速に起動し、リアルタイムにアプリケーションをデプロイできます。
CPU、メモリ、ディスク、ネットワーク、セキュリティポリシーなど、CVMインスタンスのすべてのリソースをカスタマイズでき、需要に応じてこれらのコンピューティングリソースを簡単に調整することができます。

## CVMインスタンスの使用方法

Tencent Cloudは、以下のCVM構成方法と管理方法を提供します。
- **コンソール**：Tencent Cloudが提供するCVMを構成・管理するためのWebベースのサービスインターフェースです。
- **API**：Tencent Cloudは、CVMを管理するためのインターフェースも提供しています。APIの説明については、[API概要](https://intl.cloud.tencent.com/document/api/213/15689)ドキュメントをご参照ください。
- **SDK**：[SDKプログラミング](https://intl.cloud.tencent.com/document/product/494) または [Tencent Cloud CLI](https://intl.cloud.tencent.com/document/product/1013) ツールを使用してCVM APIを呼び出すことができます。

## 関連概念

CVMを使用する前に、以下の概念を理解していただく必要があります。
<table>
<tr>
<th width="12%">概念</th><th>説明</th>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/4939">インスタンス</a></td>
<td>CPU、メモリ、OS、ネットワーク、ディスクなどの最も基本的なコンピューティングコンポーネントを含むクラウド上の仮想コンピューティングリソース。Tencent Cloudは、CVMインスタンスにさまざまなCPU、メモリ、ストレージ、およびネットワーク構成を提供します。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/11518">インスタンス仕様</a>ドキュメントをご参照ください。</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/4940">イメージ</a></td>
<td>事前に構成されたOSやプリインストールされたソフトウェアなど、CVMが動作するためのテンプレートです。Tencent Cloud CVMはWindowsやLinuxなど、さまざまな構成済みイメージを提供します。</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/4953">Cloud Block Storage</a></td>
<td>Tencent Cloudが提供する分散型の永続的なブロックストレージデバイスであり、インスタンスのシステムディスクまたは拡張可能なデータディスクとして利用できます。</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/215/535">VPC</a></td>
<td>Tencent Cloudが提供する論理的に分離した仮想ネットワーク。</td>
</tr>
<tr>
<td>IPアドレス</td>
<td>Tencent Cloud は、 <a href="https://intl.cloud.tencent.com/doc/product/213/5225"> プライベートIPアドレス</a>と<a href="https://intl.cloud.tencent.com/document/product/213/5224">パブリックIPアドレス</a>を提供します。簡単に説明すると、プライベートIPアドレスはローカルエリアネットワーク（LAN）サービスを提供し、CVM間で相互にアクセスできます。パブリックIPアドレスは、ユーザーがCVMインスタンス上でInternetサービスにアクセスする必要がある場合に使用されます。
</tr>
<tr>
<td>EIP</td>
<td>動的​ネットワーク向けに設計された静的パブリックIPアドレスで、迅速なトラブルシューティングの要件に応えられます。</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/12452">セキュリティグループ</a></td>
<td>セキュリティグループは、状態検出とパケットフィルタリング機能を備えた仮想ファイアウォールとして捉えることができます。1台または複数台のCVMのネットワークアクセス制御に使用されて、ネットワークセキュリティ分離の重要な手段です。</td>
</tr>
</table>

## CVMインスタンスの購入とカスタマイズ

ストレージメディア、容量、ネットワーク帯域幅、セキュリティグループ設定のカスタマイズ構成など、CVM構成に対してより高い構成要件がある場合に、次のドキュメントをご覧ください：
- [ Windows CVMのカスタム設定](https://intl.cloud.tencent.com/document/product/213/10516)
- [ Linux CVMのカスタム設定](https://intl.cloud.tencent.com/document/product/213/10517)

## CVM 料金

CVMは従量課金制をサポートしています。詳細については、[料金の概要](https://intl.cloud.tencent.com/document/product/213/2176)ドキュメントをご参照ください。
CVMインスタンスおよびその他のリソースの料金情報については、[製品価格](https://buy.cloud.tencent.com/price/cvm/overview)ドキュメントをご参照ください。

## その他の関連製品

- Auto Scalingを使用すると、条件に基づいてサーバークラスタの数を自動的に増減できます。詳細については、[Auto Scaling](https://intl.cloud.tencent.com/document/product/377)ドキュメントをご参照ください。
- Cloud Load Balancerを使用すると、クライアントからのトラフィックを複数のCVMインスタンスに自動的に分散できます。詳細については、[Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214)ドキュメントをご参照ください。
- Tencent Kubernetes Engineを使用して、CVM 内のアプリケーションのライフサイクルを管理できます。詳細については、[Tencent Kubernetes Engine](https://intl.cloud.tencent.com/document/product/457)ドキュメントをご参照ください。
- Cloud Monitorサービスを使用すると、CVMインスタンスとそのシステムディスクを監視できます。詳細については、[Cloud Monitor](https://intl.cloud.tencent.com/document/product/248)ドキュメントをご参照ください。
- リレーショナルデータベースをクラウドにデプロイするか、TencentDBを使用できます。詳細については、[TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236)ドキュメントをご参照ください。


