## 概要

このドキュメントでは、カスタム設定モードを例として、Tencent Cloud Virtual Machine（CVM）インスタンスを作成する方法について説明します。

## 前提条件

CVMインスタンスを作成する前に、次の手順を実行する必要があります。
- [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)、及び [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了する必要があります。実名認証を行っていないユーザーは、中国本土のCVMインスタンスを購入できません。
- ネットワークタイプがVirtual Private Cloud（VPC）であるCVMインスタンスを作成するには、ターゲットリージョンに [VPC](https://intl.cloud.tencent.com/document/product/215/31805)を作成し、かつVPCの下のターゲットアベイラビリティゾーンに[サブネットを作成](https://intl.cloud.tencent.com/document/product/215/31806)する必要があります。　
-　システムによって自動的に作成されたデフォルトプロジェクトを使用しない場合は、[プロジェクトを作成](https://intl.cloud.tencent.com/document/product/378/34726)する必要があります。 
- システムによって自動的に作成されたデフォルトセキュリティグループを使用しない場合は、ターゲットリージョンに[セキュリティグループを作成](https://intl.cloud.tencent.com/document/product/213/34271) し、ビジネス要件を満たすセキュリティグループルールを追加する必要があります。
- Linuxインスタンスの作成時にSSH キーペアをバインドするには、ターゲットプロジェクトに[SSHキーを作成](https://intl.cloud.tencent.com/document/product/213/16691)する必要があります。
- カスタムイメージを使用してCVMインスタンスを作成するには、[カスタムイメージを作成](https://intl.cloud.tencent.com/document/product/213/4942)するか、[イメージをインポート](https://intl.cloud.tencent.com/document/product/213/4945)する必要があります。

## 操作手順

1.[Tencent Cloud公式サイト](https://intl.cloud.tencent.com/)にログインし、【製品】>【コンピューティング】>【 [Cloud Virtual Machine](https://intl.cloud.tencent.com/product/cvm)】を選択して、【今すぐ購入】をクリックして、CVM購入画面に入ります。
 - **[カスタム設定](https://buy.cloud.tencent.com/cvm?tab=custom)：**このモードは、特定のユースケースに適しています。ユーザーはニーズに応じて適切なCVMインスタンスを購入できます。
2. 画面の指示に従って次の情報を設定します。
<table>
<tr><th style="width: 20%">カテゴリー</th><th style="width: 12%">選択必須/オプション</th><th>設定の説明</th></tr>
<tr><td>課金方式</td><td>選択必須</td><td>実際のニーズに応じて選択してください：<ul><li><b>従量課金</b>：CVMのフレキシブルな課金方式</ul>より詳細な説明をご覧になる場合は、<a href="https://intl.cloud.tencent.com/document/product/213/2180">課金説明</a>をご参照ください。
<tr><td>リージョン/アベイラビリティーゾーン</td><td>選択必須</td><td><ul><li><b>リージョン</b>：アクセスのレイテンシーを低減し、アクセス速度を向上させるために、顧客に最も近いリージョンを選択することをお勧めします。</li><li><b>アベイラビリティーゾーン</b>：実際のニーズに応じて選択してください。</br>複数のCVMを購入する必要がある場合は、ディザスタリカバリを実現するために異なるアベイラビリティーゾーンを選択することをお勧めします。</li></ul>リージョンとアベイラビリティーゾーンの詳細については、  <a href="https://intl.cloud.tencent.com/document/product/213/6091">リージョンとアベイラビリティーゾーン</a>をご参照ください。</td></tr>
<tr><td>ネットワーク</td><td>選択必須</td><td>Tencent Cloudに構築された、論理的に隔離された領域にある仮想ネットワークです。1つのVPCは、少なくとも1つのサブネットが含まれます。システムは、各リージョンにデフォルトのVPCとサブネットを提供します。</br>
既存のVPC/サブネットが要件を満たしていない場合は、VPCコンソールでVPCまたはサブネットを作成できます。</br><b>注意</b>：<ul><li>同じVPC内のリソースは、プライベートネットワーク内で共有できます。</li><li>CVMを購入する時に、CVMとCVMが作成されるサブネットに同じアベイラビリティーゾーンにあることを確認してください。</li></ul></td></tr>
<tr><td>インスタンス</td><td>選択必須</td><td>Tencent Cloudは、基盤となるハードウェアに基づいてさまざまなインスタンスタイプをご提供します。最適なパフォーマンスを実現するために、最新世代のインスタンスタイプを使用することをお勧めします。</br>
インスタンスの詳細については 、<a href="https://intl.cloud.tencent.com/document/product/213/11518">インスタンス仕様</a>をご参照ください。</td></tr>
<tr><td>イメージ</td><td>選択必須</td><td>Tencent Cloudは、パブリックイメージ、カスタムイメージ、共有イメージを提供します。<a href="https://intl.cloud.tencent.com/document/product/213/4941">イメージ種類</a> を参照して選択してください。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">システムディスク</a></td><td>選択必須</td><td>OSのインストールに使用されます。 容量はデフォルトで50 GBです。</br>リージョンによって、選択可能なCloud Block Storage(CBS)の種類が異なります。画面の指示に従って選択してください。</br>CBSの詳細については、 <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS種類</a>をご参照ください。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">データディスク</a></td><td>オプション</td><td>CVMのストレージ容量を拡張し、効率的で信頼性の高いストレージデバイスを提供するために使用されます。CBSデータディスクはデフォルトでは追加されません。</br>CBSの詳細については、<a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS種類</a>をご参照ください。</td></tr>
<tr><td>パブリックネットワーク帯域幅</td><td>選択必須</td><td>デフォルトでは、専用のパブリックIPアドレスが無料で割り当てられます。</br>Tencent Cloudは以下の2つのネットワーク課金方式をご提供します。実際のニーズに応じて0Mbpsより大きい値を設定してください。<ul><li><b>帯域幅課金</b>：固定帯域幅を選択します。帯域幅がこの値を超えると、パケット損失が発生することがあります。ネットワーク接続が安定しているシナリオに適しています。</li><li><b>トラフィック課金</b>：実際に使用したトラフィックに基づいて課金されます。ピーク帯域幅を設定することで、予期しないトラフィックによって発生する料金を防ぐことができます。瞬時帯域幅がこの値を超えるとパケット損失が発生します。ネットワーク接続が不安定なシナリオに適しています。</li><li><b>共有帯域幅パッケージ課金</b>：ビジネス中のパブリックネットワークのトラフィックピークが異なる時間帯に分散しているとき、共有帯域幅パッケージによって帯域幅の集約課金が実現できます。これは、大規模なビジネスやパブリックネットワークのさまざまなインスタンスがトラフィックピークシフトを形成できるシナリオに適しています。<br>共有帯域幅パッケージは現在、ベータ版テスト段階にあります。使用する必要がある場合は、 <a href="https://intl.cloud.tencent.com/apply/p/86ulv50u1e8">ベータ版テストを申請</a>してください。</li></ul><b>注意</b>：無料で割り当てられた独立したパブリックIPアドレスは、インスタンスからバインド解除できません。このIPアドレスのバインドを解除する必要がある場合は、このパブリックIPをEIPに変換すると、バインドを解除できるようになります。EIPの詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a>をご参照ください。</li><li>次の2つの状況は、独立したパブリックIPの割り当てをサポートしていません。実際の購入ページをご参照ください：
<ul><li>IPリソースは完売しました</li><li>特定のリージョン</li></ul></li></ul></td></tr>
<tr><td>パブリックゲートウェイ</td><td>オプション</td><td>Linuxイメージにのみ適用されます。</br>パブリックゲートウェイは、VPCとパブリックネットワーク間のインターフェースであり、VPC内にある異なるサブネットでパブリックIPを持たないCVMのリクエストを転送できます。</br><b>注意：</b>2019年12月6日以降、Tencent Cloudは、CVMの購入ページでのパブリックネットワークゲートウェイの選択と設定をサポートしません。必要な場合は、<a href="https://intl.cloud.tencent.com/document/product/213/34835">パブリックネットワークゲートウェイの設定</a>に従って、ご自分で設定してください。</td></tr> 
<tr><td>数量</td><td>選択必須</td><td>購入するCVMの数</td></tr>
</table>
3. 【Next: Complete Configuration】をクリックして、ホストの設定画面に入ります。
4. 画面の指示に従って次の情報を設定します。　
<table>
<tr><th style="width: 20%">カテゴリー</th><th style="width: 12%">選択必須/オプション</th><th>設定の説明</th></tr>
<tr><td>所属プロジェクト</td><td>選択必須</td><td>デフォルトのプロジェクトが選択されています。実際のニーズに応じて、既存のプロジェクトを選択することで、異なるCVMを管理できます。</td></tr>
<tr><td>セキュリティグループ</td><td>選択必須</td><td><ul><li>使用可能なセキュリティグループがない場合は、【セキュリティグループの作成】を選択します。</li><li>使用可能なセキュリティグループがある場合は、【既存のセキュリティグループ】を選択します。</li></ul>セキュリティグループの詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/12452">セキュリティグループ</a>をご参照ください。</td></tr>
<tr><td>インスタンス名</td><td>オプション</td><td>作成するCVMの名前をカスタマイズできます。</br><ul><li>インスタンス名を指定しない場合は、デフォルトで**無名**が使用されます。</li><li>インスタンス名を指定した場合は、そのインスタンス名は60文字以内に制限する必要があります。または  <a href="https://intl.cloud.tencent.com/document/product/213/32020"> 一括連続命名または指定パターン文字列命名することができます</a>。</li></ul><b>注</b>：この名前はコンソールにのみ表示されます。CVMのホスト名ではありません。</td></tr>
<tr><td>ログイン方法</td><td>選択必須</td><td>実際のニーズに応じて、CVMにログインする方法を設定します。<ul><li><b>パスワードの設定</b>：インスタンスにログインするためのパスワードをカスタマイズできます。</li><li><b>キーに関連付ける（Linuxインスタンスのみサポート）</b>：インスタンスをSSHキーに関連付けて、SSHキーを介してCVMにより安全にログインします。</br>キーを持ってない或は既存のキーが不適切な場合は、【今すぐ作成】をクリックしてキーを作成します。SSH キーの詳細情報はについて、 <a href="http://cloud.tencent.com/doc/product/213/SSH%E5%AF%86%E9%92%A5">SSH キー</a>をご参照ください。</li><li><b>パスワードの自動生成</b>：自動生成されたパスワードは <a href="https://console.cloud.tencent.com/message"> サイト内メール</a>  の形で送信されます。</li></ul></td></tr>
<tr><td>セキュリティ強化</td><td>オプション</td><td>デフォルトでは、Anti-DDoSとCloud Workload Protection機能が無料で利用でき、ユーザーがサーバーセキュリティ保護システムを構築してデータ漏洩を防ぐのを支援します。</td></tr>
<tr><td>クラウドモニタリング</td><td>オプション</td><td>デフォルトでは、クラウドモニタリング機能が無料で利用できます。コンポーネントをインストールしてCVMモニタリング指標を取得して、監視アイコン形式で表示します。さらに、カスタムアラームのしきい値などの設定をサポートします。また、CVMデータ監視、インテリジェントなデータ分析、リアルタイムな障害アラーム、およびデータレポートのカスタマイズ設定を提供します。これにより、ユーザーは業務とCVMのヘルス状態を正確に把握できます。</td></tr>
<tr><td>高度な設定</td><td>オプション</td><td>実際のニーズに応じて、インスタンスの追加設定を構成します。<ul><li><b>ホスト名</b>：ユーザーはCVM OS 内のコンピューター名をカスタマイズできます。CVMが作成されたら、CVMにログインしてホスト名を確認できます。</li><li><b>Placement group</b>：必要に応じてインスタンスをPlacement groupに追加して、サービスの可用性を向上させます。詳細については、  <a href="https://intl.cloud.tencent.com/document/product/213/15486">Placement group</a> を参照して、設定してください。</li><li><b>タグ</b>：タグを設定すると、CVMリソースの分類管理を実現できます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/19548">タグ</a> を参照して、設定してください。</li><li><b>カスタムデータ</b>：カスタムデータを指定してインスタンスを構成します。構成されたスクリプトは、インスタンスの起動時に実行されます。一度に複数のCVMを購入する場合、カスタムデータはすべてのCVMで実行されます。Linux OSは Shell 形式、Windows OSは PowerShell 形式をそれぞれサポートし、最大16KBの生データをサポートします。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/17525">カスタムデータ</a>をご参照ください。</br><b>注意</b>：カスタムデータ構成は、 Cloudinit サービスを持つパブリックイメージのみをサポートします。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/19670">Cloud-Init</a>をご参照ください。</li></ul></td></tr>
</table>
5. 【Next: Confirm Configuration】をクリックして、設定情報の確認画面に入ります。
6. 購入したCVMの情報および各設定の費用明細を確認します。
7. 『Tencent Cloud Service Terms』を読んで同意します。
7. 【Enable】をクリックして、支払いを完了します。 次に、 [CVMコンソール](https://console.cloud.tencent.com/cvm) にログインして、CVMを確認できます。
CVMのインスタンス名、パブリックIPアドレス、プライベートIPアドレス、ログイン名、初期ログインパスワードなどの情報は[サイト内メール](https://console.cloud.tencent.com/message)  の形式でアカウントに送信されます。この情報を利用して、インスタンスにログインして管理できます。CVMのセキュリティを確保するために、できるだけ早くCVMログインパスワードを変更してください。 





