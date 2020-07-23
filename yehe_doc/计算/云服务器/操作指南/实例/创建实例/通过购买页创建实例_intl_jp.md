## 操作シナリオ

このドキュメントでは、カスタマイズ設定方式を例として、Tencent Cloud Virtual Machine（CVM）インスタンスを作成する方法について説明します。

## 前提条件

CVMインスタンスを作成する前に、以下のことを実行する必要があります：
- [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)、及び [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完成する必要があります。
- ネットワークタイプがVirtual Private Cloud（VPC）であるCVMインスタンスを作成するには、ターゲットリージョンに[VPCを作成](https://intl.cloud.tencent.com/document/product/215/31805)し、かつVPCの下のターゲットアベイラビリティゾーンに[サブネットを作成](https://intl.cloud.tencent.com/document/product/215/31806)する必要があります。　
- システムで自動的に作成されたデフォルトプロジェクトを使用しない場合は、[プロジェクトを作成](https://intl.cloud.tencent.com/document/product/378/34726)する必要があります。
- システムで自動的に作成されたデフォルトのセキュリティグループを使用しない場合は、ターゲットリージョンに[セキュリティグループを作成](https://intl.cloud.tencent.com/document/product/213/34271) し、業務ニーズを満たすセキュリティグループルールを追加する必要もあります。
-  Linux インスタンスを作成する時に、SSH キーペアをバインドする必要がある場合、ターゲットプロジェクトに[SSHキーを作成](https://intl.cloud.tencent.com/document/product/213/16691)する必要があります。
- カスタムイメージを使用してCVMインスタンスを作成する必要がある場合は、[カスタムイメージ](https://intl.cloud.tencent.com/document/product/213/4942)を作成するか、[イメージをインポート](https://intl.cloud.tencent.com/document/product/213/4945)する必要があります。

## 操作手順

1. [Tencent Cloud公式サイト](https://intl.cloud.tencent.com/)にログインし、【製品】>【クラウドコンピューティング】>【[CVM](https://intl.cloud.tencent.com/product/cvm)】を選択して、【今すぐ購入】をクリックして、CVM購入画面に入ります。
 - **[カスタマイズ設定](https://buy.cloud.tencent.com/cvm?tab=custom)：**このモードは、特定のユースケースに適しているため、ユーザーは特定の要件を満たすCVMインスタンスを購入できます。
2. 画面の指示に従って次の情報を設定します。
<table>
<tr><th style = "width：20％">カテゴリ</th><th style = "width：12％">記入必須/オプション</th><th>設定の説明</th></Tr>
<tr><td> 課金モード</td><td>記入必須</td><td>実際のニーズに応じて選択してください：<ul><li><b>従量課金</b>：CVMの柔軟な課金モード</ul>課金モードの詳細については、<a href=″https://intl.cloud.tencent.com/document/product/213/2180″> 課金説明 </a>をご参照ください。</td><tr>
<tr><td>リージョン/アベイラビリティーゾーン</td><td>記入必須</td><td><ul><li><b>リージョン</b>：アクセスのレイテンシーを低減し、アクセス速度を向上させるために、顧客に最も近いリージョンを選択することをお勧めします。</li><li><b>アベイラビリティーゾーン</b>：実際のニーズに応じて選択してください。</br>複数のCVMを購入する必要がある場合は、迅速な災害復旧を実現するために異なるアベイラビリティーゾーンを選択することをお勧めします。</li></ul>選択可能なリージョンとアベイラビリティーゾーンの詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/6091">リージョンとアベイラビリティーゾーン</a>をご参照ください。</td></tr>
<tr><td>ネットワーク </td><td>記入必須</td><td>Tencent Cloudに構築された、論理的に隔離されたネットワークスペースを示します。1つのVPCは、少なくとも1つのサブネットが含まれます。システムは、各リージョンにデフォルトのVPCとサブネットを提供します。</br>
既存のVPC/サブネットが要件を満たしていない場合は、VPCコンソールでVPCまたはサブネットを作成できます。</br><b>注</b>：<ul><li>同じVPC内のリソースはデフォルトでプライベートネットワークで相互接続されます。</li><li>CVMを購入する時に、CVMとCVMが作成されるサブネットに同じアベイラビリティーゾーンにあることを確認してください。</li></ul></td></tr>
<tr><td>インスタンス</td><td>記入必須</td><td>Tencent Cloudは、基盤となるハードウェアに基づいてさまざまなインスタンスタイプをご提供します。最適なパフォーマンスを実現するために、最新世代のインスタンスタイプを使用することをお勧めします。</br>　　　
インスタンスの詳細については 、<a href="https://intl.cloud.tencent.com/document/product/213/11518">インスタンスタイプ</a>をご参照ください。</td></tr>
<tr><td>イメージ</td><td>記入必須</td><td>Tencent Cloudは、パブリックイメージ、カスタムイメージ、共有イメージを提供します。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/4941">イメージ種類</a> を参照して選択してください。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">システムディスク</a></td><td>記入必須</td><td>OSのインストールに使用されます。容量はデフォルトで50GBです。</br>リージョンによって、選択可能なCloud Block Storage(CBS)の種類が異なります。実際の画面の指示に従って選択してください。</br>CBSの詳細については、<a href="https://intl.cloud.tencent.com/document/product/362/31636">CBSタイプ</a>をご参照ください。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">データディスク</a></td><td>オプション</td><td>CVMのストレージ容量を拡張し、効率的で信頼性の高いストレージデバイスを提供するために使用されます。CBSデータディスクはデフォルトでは追加されません。</br>CBSの詳細については、<a href="https://intl.cloud.tencent.com/document/product/362/31636">CBSタイプ</a>をご参照ください。</td></tr>
<tr><td>パブリックネットワーク帯域幅</td><td>記入必須</td><td>デフォルトでは、独立したパブリックIPアドレスが無料で割り当てられます。</br>Tencent Cloudは以下の2つのネットワーク課金方式をご提供します。実際のニーズに応じて0Mbpsより大きい値を設定してください。<ul><li><b>帯域幅課金</b>：固定帯域幅を選択します。帯域幅がこの値を超えると、パケット損失が発生します。ネットワークの変動が小さい場合に適しています。</li><li><b>トラフィック課金</b>：実際に使用されるトラフィックに基づいて課金されます。ピーク帯域幅を設定することで、予期しないトラフィックによって発生する料金を防ぐことができます。瞬間帯域幅がこの値を超えるとパケット損失が発生します。ネットワークの変動が大きい場合に適しています。</li></ul><b>注</b>：無料で割り当てられた独立したパブリックIPはインスタンスからバインド解除できません。このIPアドレスをバインド解除したい場合は、このパブリックIPをElastic IP(EIP)に変換してからバインド解除します。Elastic Public IPの詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a>をご参照ください。</td></tr>
<tr><td>パブリックゲートウェイ</td><td>オプション</td><td> Linuxイメージにのみ適用されます。</br>パブリックゲートウェイは、VPCとパブリックネットワーク間のネットワークインターフェースであり、VPC内にある異なるサブネットでパブリックIPアドレスを持たないCVMのリクエストを転送できます。</br><b>注：</br>Tencent Cloudは2019年12月6日以降は、CVM購入画面でのパブリックゲートウェイの設定確認をサポートしません。必要な場合は、 <a href="https://intl.cloud.tencent.com/document/product/213/34835">パブリックゲートウェイの設定</a>に従ってご自身で設定してください。</td></tr> 
<tr><td>数</td><td>記入必須</td><td>購入するCVMの数。</td></tr>
</table>
3. 【次へ：ホストの設定】をクリックして、CVM設定ページに入ります。
4. 画面の指示に従って次の情報を設定します。
<table>
<tr><th style = "width：20％">カテゴリ</th><th style = "width：12％">記入必須/オプション</th><th>設定の説明</th></Tr>
<tr><td>プロジェクト</td><td>記入必須</td><td>デフォルトのプロジェクトが選択されています。実際のニーズに応じて、既存のプロジェクトを選択することで、異なるCVMを管理できます。</td></tr>
<tr><td>セキュリティグループ</td><td>記入必須</td><td><ul><li>使用できるセキュリティグループがない場合は、【セキュリティグループの作成】を選択します。</li><li>使用できるセキュリティグループがすでにある場合は、【既存のセキュリティグループ】を選択します。</li></ul>セキュリティグループの詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/12452">セキュリティグループ</a>をご参照ください。</td></tr>　　
<tr><td>インスタンス名</td><td>オプション</td><td>作成するCVMの名前をカスタマイズできます。</br><ul><li>インスタンス名をカスタマイズしない場合は、デフォルトで**無名**が使用されます。</li><li>インスタンス名をカスタマイズした場合は、そのインスタンス名は60文字以内に制限する必要があります。または <a href="https://intl.cloud.tencent.com/document/product/213/32020">一括順次命名或は文字列パターン命名することができます</a>。</li></ul><b>注</b>：この名前はコンソールにのみ表示されます。CVMのホスト名ではありません。</td></tr>
<tr><td>ログイン方法</td><td>記入必須</td><td>必要に応じて、CVMにログインする方法を設定します。<ul><li><b>パスワードの設定</b>：インスタンスにログインするためのパスワードをカスタマイズできます。</li><li><b>SSHキーペア（Linuxインスタンスの場合のみ）</b>： SSHキーに関連付けて、より安全にCVMにログインすることができます。</br>キーがない場合、または既存のキーが不適切な場合は、【今すぐ作成】をクリックして作成できます。SSH キーの詳細情報はについては、 <a href="http://cloud.tencent.com/doc/product/213/SSH%E5%AF%86%E9%92%A5">SSH キー</a>をご参照ください。</li><li><b>パスワードの自動生成</b>：自動生成されたパスワードは <a href="https://console.cloud.tencent.com/message">サイト内メール</a> の形で送信されます。</li></ul></td></tr>
<tr><td>セキュリティーサービス</td><td>オプション</td><td>デフォルトでは、 DDoS 保護とホストセキュリティは無料で有効にします。これにより、ユーザーはサーバーセキュリティ保護システムを構築でき、データ漏洩を防止することができます。</td></tr>
<tr><td>クラウドモニタリング</td><td>オプション</td><td>デフォルトでは、クラウドモニタリングを無料で有効にします。コンポーネントをインストールしてCVMモニタリング指標を取得して、監視アイコン形式で表示します。さらに、カスタムアラームのしきい値などの設定をサポートします。また、CVMデータ監視、インテリジェントなデータ分析、リアルタイムな障害アラーム、およびデータレポートのカスタマイズ設定を提供します。これにより、ユーザーは業務とCVMのヘルス状態を正確に把握できます。</td></tr>
<tr><td>高度な設定</td><td>オプション</td><td>必要に応じて、インスタンスの追加設定を構成します。<ul><li><b>ホスト名</b>：ユーザーは、CVM OS内のコンピューターの名前をカスタマイズ設定できます。CVMが作成されたら、CVMにログインしてホスト名を表示できます。</li><li><b>Placement Group</b>：サービスの可用性を向上させるために、必要に応じてインスタンスをplacement groupに追加できます。詳細については、 <a href="https://cloud.tencent.com/document/product/213/15486">Placement Group</a> をご参照ください。</li><li><b>タグ</b>：タグを設定した後、CVMリソースをカテゴリ別に管理できます。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/19548">タグ</a> をご参照ください。</li><li><b>カスタムデータ</b>：カスタムデータを指定してインスタンスを設定できます。インスタンスの起動時に構成済みのスクリプトが実行されます。一度に複数のCVMを購入する場合、カスタムデータがすべてのCVMで実行されます。Linux OSは Shell 形式、Windows OSは PowerShell 形式をそれぞれサポートし、最大16KBの生データをサポートします。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/17525">カスタムデータ</a>をご参照ください。</br><b>注</b>：カスタムデータ設定は、Cloudinitサービスを持つ一部のパブリックイメージのみをサポートします。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/19670">Cloud-Init</a>をご参照ください。</li></ul></td></tr>
</table>
5. 【次へ：設定情報の確認】をクリックして、設定情報の確認画面に入ります。
6. 購入したCVMの情報および各設定の費用明細を確認します。
7. 【今すぐ購入】/【アクティブ】をクリックして支払いを完了します。支払いが完了したら、 [CVMコンソール](https://console.cloud.tencent.com/cvm)ログインしてCVMを表示できます。
CVMのインスタンス名、パブリックIPアドレス、プライベートIPアドレス、ログインユーザー名、初期ログインパスワードなどの情報は[内部メール](https://console.cloud.tencent.com/message) の形でアカウントに送信されます。これらの情報を使用して、インスタンスにログインして管理できます。また、 CVMのセキュリティを確保するために、CVMのログインパスワードをできるだけ早く変更してください。





