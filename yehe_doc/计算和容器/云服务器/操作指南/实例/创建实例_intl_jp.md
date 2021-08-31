## ユースケース

このドキュメントは、カスタマイズ設定を例として、Tencent Cloud CVMのインスタンスを作成する方法について説明します。

## 前提条件

CVMインスタンスを作成する前に、以下のことを実行する必要があります：
- [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)、及び [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完成する必要があります。
- Virtual Private CloudのCVMインスタンスをネットワークとして作成する場合は、ターゲットリージョンに [Virtual Private Cloudを作成](https://cloud.tencent.com/document/product/215/20109）する必要があります。VPC配下のターゲットアベイラビリティゾーンに[サブネットを作成](https://cloud.tencent.com/document/product/215/20110)する必要があります。
-　システムによって自動的に作成されたデフォルトプロジェクトを使用しない場合は、[プロジェクトを作成](https://cloud.tencent.com/document/product/378/10861)する必要があります。
- システムによって自動的に作成されたデフォルトのセキュリティグループを使用しない場合は、ターゲットリージョンに[セキュリティグループを作成](https://intl.cloud.tencent.com/document/product/213/18197) する必要があり、業務ニーズを満たすセキュリティグループルールを追加する必要もあります。
-  Linux インスタンスを作成する時に、 SSH キーペアをバインドする必要がある場合、ターゲットプロジェクトに[SSHキーを作成](https://intl.cloud.tencent.com/document/product/213/16691)する必要があります。
- カスタマイズイメージを使用してCVMインスタンスを作成する必要がある場合は、[カスタマイズイメージを作成](https://intl.cloud.tencent.com/document/product/213/4942) するか、 [イメージをインポート](https://intl.cloud.tencent.com/document/product/213/4945)する必要があります。

## 操作手順

1. [Tencent Cloud公式サイト](https://intl.cloud.tencent.com)にログインし、【製品情報】>【クラウドコンピューティング】>【[Cloud Virtual Machine](https://intl.cloud.tencent.com/product/cvm)】を選択して、【今すぐ購入】をクリックして、CVM購入画面に入ります。
 - **[クイック構成](https://buy.cloud.tencent.com/cvm?tab=lite)：**は一般的なシナリオに適用できるため、ユーザーは一般的な要件を満たすCVMインスタンスをすばやく購入できます。
 - **[カスタマイズ設定](https://buy.cloud.tencent.com/cvm?tab=custom)：**は特定のシナリオに適用できるため、ユーザーは特定要件を満たすCVMインスタンスを購入できます。
2. 画面のプロンプトに従って、以下の情報を設定します：
<table>
<tr><th style="width：20％">カテゴリー</th><th style="width: 12%">選択必須/オプション</th><th>設定の説明</th></tr>
<tr><td>課金モード</td><td>選択必須</td><td>実際のニーズに応じて選択してください：<ul><li><b>従量課金</b>：CVMの柔軟な課金モードは、ECプロモーションなどによりデバイスの需要が瞬時に大きく変動するシナリオに適しています。</li><li><b>スポットインスタンス</b>：新しいインスタンス操作モードであり、ビッグデータコンピューティング、Cloud Load Balancerを利用してオンラインサービスとウェブサイトサービスなどのシナリオに適しています。一般的な価格帯は従量課金インスタンスの10％〜20％です。</li></ul>課金モードの詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/2180">課金モードの説明</a>をご参照ください。</td></tr>
<tr><td>リージョン/アベイラビリティーゾーン</td><td>選択必須</td><td><ul><li><b>リージョン</b>：ユーザーに最も近いリージョンを選択することをお勧めします。アクセスレイテンシーを短縮し、アクセス速度を向上させることができます。</li><li><b>アベイラビリティーゾーン</b>：実際にニーズに応じて選択してください。</br>複数のCVMを購入する必要がある場合は、災害復旧を実現するために、異なるアベイラビリティーゾーンを選択することをお勧めします。</li></ul>リージョンとアベイラビリティーゾーンの詳細については、 <a href="https://cloud.tencent.com/document/product/213/6091">リージョンとアベイラビリティーゾーン</a>をご参照ください。</td></tr>
<tr><td>ネットワーク</td><td>選択必須</td><td>Tencent Cloudに構築された論理的に分離されたネットワークスペースを表します。一つのVirtual Private Cloudは、少なくとも1つのサブネットが含まれます。システムは、各リージョンにデフォルトのVPCとサブネットを提供します。</br>
既存のVPC/サブネットがお客様の要件を満たしていない場合、VPCコンソールでVPCまたはサブネットを作成できます。</br><b>注意</b>：<ul><li>同じVPC内のリソースはデフォルトでプライベートネットワーク相互接続します。</li><li>CVMを購入する時、CVMは同じアベイラビリティーゾーン属性を持つサブネットに作成する必要があります。</li></ul></td></tr>
<tr><td>インスタンス</td><td>選択必須</td><td>基盤となるハードウェアの違いによって、Tencent Cloudは現在さまざまな種類のインスタンスを提供しています。 パフォーマンスを最適化するには、最新世代のインスタンスタイプを利用することをお勧めします。</br>
インスタンスの詳細については 、<a href="https://intl.cloud.tencent.com/document/product/213/11518">インスタンス仕様</a>をご参照ください。</td></tr>
<tr><td>イメージ</td><td>選択必須</td><td>Tencent Cloudはパブリックイメージ、カスタマイズイメージ、共有イメージ、サービスマーケットイメージを提供してます。<a href="https://intl.cloud.tencent.com/document/product/213/4941">イメージ種類</a> を参照して選択してください。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">システムディスク</a></td><td>選択必須</td><td>OSのインストールに使用されます。 容量はデフォルトで50 GBです。</br>リージョンによって、選択可能なCloud Block Storageの種類が異なります。実際ページの指示に従って選択してください。</br>CBSの詳細については、<a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS種類</a>をご参照ください。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">データディスク</a></td><td>オプション</td><td>CVMのストレージ容量を拡張し、効率的で信頼性の高いストレージデバイスを提供するために使用されます。CBSデータディスクはデフォルトでは追加されません。</br>CBSの詳細については、<a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS種類</a>をご参照ください。</td></tr>
<tr><td>パブリックネットワーク帯域幅</td><td>選択必須</td><td>デフォルトでは、独立したパブリックIPアドレスが無料で割り当てられます。</br>Tencent Cloudは以下の2つのネットワーク課金モードを提供しています、実際のニーズに応じて0Mbpsより大きい値を設定してください。<ul><li><b>帯域幅によって課金する</b>：固定帯域幅を選択し、この帯域幅を超えると、パケット損失が発生します。ネットワークの変動が小さいシナリオに適しています。</li><li><b>トラフィックによって課金する</b>：実際に使用したトラフィックによって課金します。ピーク帯域幅を制限して、予期しないネットワークトラフィックによって発生する料金を避けられます。瞬時帯域幅がこの値を超えると、パケット損失が発生します。ネットワークの変動が大きいシナリオに適しています。</li></ul><b>注意</b>：無料の独立したパブリックIPはインスタンスとバインド解除することができません。このIPアドレスをバインド解除したい場合は、このパブリックネットワークIPをがEIPに変換してからバインド解除します。EIPの詳細については、 <a href="https://cloud.tencent.com/document/product/213/5733">EIP</a>をご参照ください。</td></tr>
<tr><td>パブリックゲートウェイ</td><td>オプション</td><td> Linuxイメージにのみ適用されます。</br>パブリックゲートウェイは、Virtual Private Cloudとパブリックネットワーク間のインターフェースであり、Virtual Private Cloud中の各サブネットにあるパブリックIPアドレスを持ってないのCVMリクエストを転送できます。</br>詳細については、 <a href="https://cloud.tencent.com/document/product/215/20078">パブリックゲートウェイ</a>をご参照ください。</td></tr> 
<tr><td>数量</td><td>選択必須</td><td>購入するCVMの数を表します。</td></tr>  
</table>
3. 【Next: Complete Configuration】をクリックして、ホストの設定画面に入ります。
4. 画面のプロンプトに従って、以下の情報を設定します：
<table>
<tr><th style="width：20％">カテゴリー</th><th style="width: 12%">選択必須/オプション</th><th>設定の説明</th></tr>
<tr><td>所属プロジェクト</td><td>選択必須</td><td>デフォルトではデフォルトプロジェクトが選択されています。実際のニーズに応じて、既存のプロジェクトを選択することにより、異なるCVMを管理できます。</td></tr>
<tr><td>セキュリティグループ</td><td>選択必須</td><td><ul><li>利用できるセキュリティグループがない場合は、【 Create a security group】を選択してください。</li><li>利用できるセキュリティグループが既にある場合は、【Existing Security Groups】を選択してください。</li></ul>セキュリティグループの詳細については、<a href="https://cloud.tencent.com/document/product/213/12452">セキュリティグループ</a>をご参照ください。</td></tr>
<tr><td>インスタンス名</td><td>オプション</td><td>作成するCVMの名前をカスタマイズできます。</br><ul><li>インスタンス名を定義しない場合は、作成されたインスタンス名は「未命名」になります。</li><li>インスタンス名を定義した場合は、インスタンス名は60文字以内に制限する必要があります。または <a href="https://cloud.tencent.com/document/product/213/34343">バッチ連続命名或は文字列パターン命名することができます</a>。</li></ul><b>注意</b>：この名前はコンソールに表示される名前のみであり、 CVMのホスト名ではありません。</td></tr>
<tr><td>ログイン方法</td><td>選択必須</td><td>実際のニーズに応じて、CVMにログインする方法を設定します。<ul><li><b>パスワードの設定</b>：インスタンスにログインするためのカスタムパスワードを設定します。</li><li><b>直ちにキーを関連します（ Linux インスタンスのみサポートする）</b>： CVMへの安全なログインを確保するために、インスタンスをSSHキーに関連付けます。</br>キーを持ってない或は既存のキーが不適切な場合は、【今すぐ作成】をクリックして作成します。SSH キーの詳細情報はについて、 <a href="http://cloud.tencent.com/doc/product/213/SSH%E5%AF%86%E9%92%A5">SSH キー</a>をご参照ください。</li><li><b>パスワードの自動生成</b>：自動生成されたパスワードは <a href="https://console.cloud.tencent.com/message">サイト内メール</a> 方法で送信されます。</li></ul></td></tr>
<tr><td>セキュリティーサービス</td><td>オプション</td><td>デフォルトでは、 DDoS 保護とHost Security保護を無料で有効になっています。これにより、ユーザーはCVMセキュリティシステムを構築でき、データ漏洩を防ぎます。</td></tr>
<tr><td>クラウド監視</td><td>オプション</td><td>デフォルトでは無料で有効になっています。コンポーネントをインストールしてホスト監視指標を取得し、アイコン形式で表示します。さらに、カスタムアラームの閾値などの設定をサポートします。または、立体的なCVMデータ監視、インテリジェントなデータ分析、リアルタイムな故障アラーム、カスタムデータレポート構成を提供します。これにより、ユーザーがサービスとCVMのヘルス状態を正確に把握できます。</td></tr>
<tr><td>高度な設定</td><td>オプション</td><td>実際のニーズに応じて、インスタンスにより詳細な構成を行います。<ul><li><b>ホスト名</b>：ユーザーはCVM OS 内のコンピューター名をカスタマイズできます。 CVMが作成されたら、CVMにログインしてホスト名を確認できます。</li><li><b>Placement group</b>：必要に応じてインスタンスをPlacement groupに追加して、サービスの可用性を向上させます。詳細については、 <a href="https://cloud.tencent.com/document/product/213/15486">Placement group</a> を参照して、設定してください。</li><li><b>タグ</b>：タグを設定すると、CVMリソースの分類管理を実現できます。詳細については、 <a href="https://cloud.tencent.com/document/product/213/19548">タグ</a> を参照して、設定してください。</li><li><b>カスタムデータ</b>：カスタムデータを指定してインスタンスを構成します。つまり、このインスタンスを起動する時に構成スクリプトが実行されます。一度に複数のCVMを購入する場合、カスタムデータはすべてのCVMで実行されます。Linux OSは Shell 形式、Windows OSは PowerShell 形式をそれぞれサポートし、最大16KBの生データをサポートします。詳細については、 <a href="https://cloud.tencent.com/document/product/213/17525">カスタムデータ</a>をご参照ください。</br><b>注意</b>：カスタムデータ構成は、 Cloudinit サービスをもつパブリックイメージのみをサポートします。詳細については、 <a href="https://cloud.tencent.com/document/product/213/19670">Cloud-Init</a>をご参照ください。</li></ul></td></tr>
</table>
5. 【Next: Confirm Configuration】をクリックして、構成情報の確認画面に入ります。
6. 購入したCVMの情報と各構成アイテムの費用明細を確認します。
7. 【今すぐ購入】をクリックして、支払いが完了したら、 [CVMコンソール](https://console.cloud.tencent.com/cvm)にログインしてCVMを確認できます。
CVMのインスタンス名、パブリックIPアドレス、プライベートIPアドレス、ログイン名、初期ログインパスワードなどの情報は[サイト内メール](https://console.cloud.tencent.com/message) の形式でアカウントに送信されます。この情報を利用して、インスタンスにログインして、管理できます。 セキュリティを確保するために、CVMログインパスワードをできるだけ早く変更してください。





