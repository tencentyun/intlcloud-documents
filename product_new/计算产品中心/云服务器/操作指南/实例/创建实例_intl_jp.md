## ユースケース

このドキュメントは、カスタマイズ構成方式を例として、Tencent Cloud CVMのインスタンスを作成する方法を説明します。

## 前提条件

CVMインスタンスを作成する前に、以下のことを実行する必要があります：
- [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)、及び [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完成させます。
- Virtual Private CloudのCVMインスタンスをネットワークとして作成する場合は、ターゲットリージョンで [Virtual Private Cloudを作成](https://cloud.tencent.com/document/product/215/20109）する必要があります。Virtual Private Cloud配下のターゲットアベイラビリティゾーンで[サブネットを作成](https://cloud.tencent.com/document/product/215/20110)する必要があります。
- システムで自動的に作成されたデフォルトプロジェクトを使用しない場合は、[プロジェクトを作成](https://cloud.tencent.com/document/product/378/10861)する必要があります。
- システムで自動的に作成されたデフォルトのセキュリティグループを使用しない場合は、ターゲットリージョンで[セキュリティグループを作成](https://intl.cloud.tencent.com/document/product/213/18197) する必要があり、業務ニーズを満たすセキュリティグループ規則を追加する必要もあります。
-  Linux インスタンスを作成する時に、 SSH キーペアをバインディングする必要がある場合、ターゲットプロジェクトに[SSHキーを作成](https://intl.cloud.tencent.com/document/product/213/16691)する必要があります。
- カスタマイズイメージのCVMインスタンスを作成する必要がある場合は、[カスタマイズイメージを作成](https://intl.cloud.tencent.com/document/product/213/4942) 或は [イメージをインポート](https://intl.cloud.tencent.com/document/product/213/4945)する必要があります。

## 操作手順

1. [Tencent Cloud公式サイト](https://intl.cloud.tencent.com)にログインし、【製品】>【基礎】>【コンピューティング】>【[CVM](https://intl.cloud.tencent.com/product/cvm)】を選択して、【すぐに購入】をクリックして、CVM購入画面に入ります。
 - **[クイック構成](https://buy.cloud.tencent.com/cvm?tab=lite)：**は通常のユースケースに適しているため、ユーザーは通常のニーズを満たすCVMインスタンスを迅速に購入できます。
 - **[カスタマイズ構成](https://buy.cloud.tencent.com/cvm?tab=custom)：**は特定のユースケースに適しているため、ユーザーは特定のニーズを満たすCVMインスタンスを購入できます。
2. 画面のプロンプトに従って、以下の情報を設定します：
<table>
<tr><th style="width: 20%">カテゴリ</th><th style="width: 12%">必須/オプション</th><th>構成説明</th></tr>
<tr><td>課金モード</td><td>必須</td><td>実際のニーズに応じて選択してください：<ul><li><b>従量課金</b>：CVMのElastic課金モードはECプロモーションなどによりデバイスの需要が瞬時に大きく変動するユースケースに適しています。</li><li><b>ビッドインスタンス</b>：新しいインスタンス操作モードであり、ビッグデータ計算、Cloud Load Balancerを利用してオンラインサービスとウェブサイトサービスなどのユースケースに適しています。一般的な価格帯は従量課金の10％〜20％です。</li></ul>課金モードの詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/2180">課金モードの説明</a>をご参照ください。</td></tr>
<tr><td>リージョン/アベイラビリティーゾーン</td><td>必須</td><td><ul><li><b>リージョン</b>：ユーザーに最も近いリージョンを選択することをお勧めします。アクセスレイテンシーを短縮し、アクセス速度を向上させることができます。</li><li><b>アベイラビリティーゾーン</b>：実際にニーズに応じて選択してください。</br>複数のCVMを購入する必要がある場合は、異なるアベイラビリティーゾーンを選択して、災害復帰効果を実現することをお勧めします。</li></ul>リージョンとアベイラビリティーゾーンの詳細については、 <a href="https://cloud.tencent.com/document/product/213/6091">リージョンとアベイラビリティーゾーン</a>をご参照ください。</td></tr>
<tr><td>ネットワーク</td><td>必須</td><td>Tencent Cloudに構築された論理的に隔離されたネットワークキャパシティーを表します。一つのVirtual Private Cloudは、少なくとも1つのサブネットで構成されます。システムは、各リージョンにデフォルトのVirtual Private Cloudとサブネットを提供します。</br>
既存のVirtual Private Cloud/サブネットがお客様の要件を満たしていない場合、Virtual Private Cloudコンソールで作成できます。</br><b>注意</b>：<ul><li>同じVirtual Private Cloud内のリソースはデフォルトでプライベートネットワークによって相互接続されます。</li><li>購入する時、CVMは同じアベイラビリティーゾーン属性を持つサブネットに作成する必要があります。</li></ul></td></tr>
<tr><td>インスタンス</td><td>必須</td><td>基盤となるハードウェアの違いによって、Tencent Cloudは現在さまざまな種類のインスタンスを提供しています。 最高のパフォーマンスを得られるために、最新世代のインスタンスタイプを利用することをお勧めします。</br>
インスタンスの詳細については 、<a href="https://intl.cloud.tencent.com/document/product/213/11518">インスタンス仕様</a>をご参照ください。</td></tr>
<tr><td>イメージ</td><td>必須</td><td>Tencent Cloudはパブリックイメージ、カスタマイズイメージ、共有イメージ、サービスマーケットを提供してます。<a href="https://intl.cloud.tencent.com/document/product/213/4941">イメージ種類</a> を参照して選択してください。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">システムディスク</a></td><td>必須</td><td>OSのインストールに使用されて、デフォルトは50GBです。</br>リージョンによってCBS種類の選択に影響して、実際の画面プロンプトに従って選択してください。</br>CBSの詳細については、 <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS種類</a>をご参照ください。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">データディスク</a></td><td>オプション</td><td>CVMのストレージ容量の拡張に使用されて、効率的で信頼性の高いストレージデバイスを提供します。CBSデータディスクはデフォルトでは追加されません。</br>CBSの詳細については 、<a href="https://intl.cloud.tencent.com/document/product/362/31636">CBSタイプ</a>をご参照ください。</td></tr>
<tr><td>パブリックネットワーク帯域幅</td><td>必須</td><td>デフォルトでは、独立したパブリックネットワークIPが無料でアサインされます。</br>Tencent Cloudは以下の二種類のネットワーク課金方式を提供しています、実際のニーズに応じて0Mbpsより大きい値を設定してください。<ul><li><b>帯域幅によって課金する</b>：固定帯域幅を選択し、この帯域幅を超えるとパケットロスになり、ネットワークの変動が小さいユースケースに適しています。</li><li><b>トラフィックによって課金する</b>：実際に使用したトラフィックによって課金します。ピーク値帯域幅を制限して、意外なトラフィックによるコストを避けられます。瞬時帯域幅がこの値を超えるとパケットロスになります。ネットワークの変動が大きいユースケースに適しています。</li></ul><b>注意</b>：独立したパブリックネットワークIPはインスタンスとバインド解除することができません。このIPアドレスをバインド解除したい場合は、このパブリックネットワークIPをがEIPに変換してからバインド解除します。EIPの詳細については、 <a href="https://cloud.tencent.com/document/product/213/5733">EIP</a>をご参照ください。</td></tr>
<tr><td>パブリックネットワークウェイ</td><td>オプション</td><td> Linux 関連のイメージのみです。</br>パブリックネットワークウェイはVirtual Private Cloudとパブリックネットワーク間のインターフェースであり、Virtual Private Cloud中の各サブネットにあるパブリックIPを持ってないのCVMリクエストを転送できます。</br>詳細については， <a href="https://cloud.tencent.com/document/product/215/20078">パブリックゲートウェイ</a>をご参照ください。</td></tr> 
<tr><td>数量</td><td>必須</td><td>購入したいCVMの数を表します。</td></tr>  
</table>
3. 【次へ：ホストの設定】をクリックして、ホストの設定画面に入ります。
4. 画面のプロンプトに従って、以下の情報を設定します：
<table>
<tr><th style="width: 20%">カテゴリ</th><th style="width: 12%">必須/オプション</th><th>構成説明</th></tr>
<tr><td>所属プロジェクト</td><td>必須</td><td>デフォルトではデフォルトプロジェクトに属します。実際のニーズに応じて、作成されたプロジェクトを選択することにより、異なるCVMを管理します。</td></tr>
<tr><td>セキュリティグループ</td><td>必須</td><td><ul><li>利用できるセキュリティグループがない場合は、【セキュリティグループの新規作成】を選択してください。</li><li>利用できるセキュリティグループが既にある場合は、【既存のセキュリティグループ】を選択してください。</li></ul>セキュリティグループの詳細については、<a href="https://cloud.tencent.com/document/product/213/12452">セキュリティグループ</a>をご参照ください。</td></tr>
<tr><td>インスタンス名</td><td>オプション</td><td>ユーザーがカスタマイズして、作成したいCVMの名前を示します。</br><ul><li>インスタンス名を定義しない場合は、作成されたインスタンス名は「未命名」になります。</li><li>インスタンス名を定義した場合は、インスタンス名は60文字以内に制限する必要があります。または <a href="https://cloud.tencent.com/document/product/213/34343">一括連続命名或は文字列パターン命名することができます</a>。</li></ul><b>注意</b>：この名前はコンソールに表示される名前のみであり、CVMの hostname名ではありません。</td></tr>
<tr><td>ログイン方法</td><td>必須</td><td>ユーザーがCVMにログインする方法を設定する場合、実際のニーズに応じて設定してください。<ul><li><b>パスワードの設定</b>：インスタンスのログインパスワードをカスタマイズします。</li><li><b>直ちにキーを関連します（ Linux インスタンスのみサポートする）</b>： SSH キーを関連し、 SSH キー方法を経由して、より安全にCVMにログインすることができます。</br>キーを持ってない或は既存のキーが不適切な場合は、【今すぐ作成】をクリックして作成します。SSH キーの詳細情報はについて、 <a href="http://cloud.tencent.com/doc/product/213/SSH%E5%AF%86%E9%92%A5">SSH キー</a>をご参照ください。</li><li><b>パスワードの自動生成</b>：自動生成されたパスワードは <a href="https://console.cloud.tencent.com/message">内部メッセージ</a> 方法で送信されます。</li></ul></td></tr>
<tr><td>Security Reinforce</td><td>オプション</td><td>デフォルトでは、 DDoS 保護とHost Securityホスト保護を無料で開通されます。これにより、ユーザーはサーバーセキュリティ保護システムを構築でき、データ漏洩を防ぎます。</td></tr>
<tr><td>クラウド監視</td><td>オプション</td><td>デフォルトでは無料開通します。コンポーネントをインストールしてホスト監視指標を取得したり、監視アイコン形式で表示します。さらに、カスタマイズアラーム閾値などの設定をサポートします。または、立体的なCVMデータ監視、インテリジェントなデータ分析、リアルタイムな故障アラーム、個人化されたデータレポート構成を提供します。これにより、ユーザーがサービスとCVMのヘルス状態を正確に把握できます。</td></tr>
<tr><td>詳細設定</td><td>オプション</td><td>実際のニーズに応じて、インスタンスにより詳細な構成を行います。<ul><li><b>ホスト名</b>：ユーザーはCVM OS 内のコンピューター名をカスタマイズで設定できます。CVMが正常に生成された後、CVMにログインして確認できます。</li><li><b>放置グループ</b>：必要に応じてインスタンスを放置グループに追加して、業務の可用性を向上させます。詳細については、 <a href="https://cloud.tencent.com/document/product/213/15486">放置グループ</a> を参照して、設定してください。</li><li><b>タグ</b>：タグを設定すると、CVMにリソースの分類管理を実現できます。詳細については、 <a href="https://cloud.tencent.com/document/product/213/19548">タグ</a> を参照して、設定してください。</li><li><b>カスタマイズデータ</b>：カスタマイズデータを指定してインスタンスを構成します。つまり、このインスタンスを起動する時に構成したスクリプトが実行されます。一度に複数のCVMを購入する場合、カスタマイズデータはすべてのCVMで実行されます。Linux OSは Shell 形式、Windows OSは PowerShell 形式をそれぞれサポートし、最大で16KBの生データをサポートします。詳細については、 <a href="https://cloud.tencent.com/document/product/213/17525">カスタマイズデータ</a>をご参照ください。</br><b>注意</b>：カスタマイズデータ構成は、 一部Cloudinit サービスをもつパブリックイメージのみをサポートします。詳細については、 <a href="https://cloud.tencent.com/document/product/213/19670">Cloud-Init</a>をご参照ください。</li></ul></td></tr>
</table>
5. 【次へ：構成情報の確認】をクリックして、構成情報の確認画面に入ります。
6. 購入したCVM情報を確認し、各構成の費用明細を確認します。
7. 【すぐ購入】をクリックして、支払いが完了したら、 [CVMコンソール](https://console.cloud.tencent.com/cvm)に入り、CVMを確認します。
CVMのインスタンス名、パブリックIPアドレス、プライベートIPアドレス、ログイン名、初期ログインパスワードなどの情報は[内部メッセージ](https://console.cloud.tencent.com/message) の形式でアカウントに送信されます。この情報を利用してログインとインスタンス管理します。早急にCVMのログインパスワードを変更して、ホストの安全性を確保します。





