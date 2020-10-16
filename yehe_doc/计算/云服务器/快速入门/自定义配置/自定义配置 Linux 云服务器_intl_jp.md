カスタマイズ設定はより豊富なイメージプラットフォーム、およびストレージ、帯域幅、セキュリティグループなどの高度な設定をサポートすることで、ニーズに応じた適切な設定を選択できます。このドキュメントでは、カスタマイズ設定を例に説明します。

## 登録と認証

Cloud Virtual Machine(CVM)を使用する前に、次の準備作業を完了する必要があります。
1. Tencent Cloudアカウントを登録し、実名認証を完了させます。
新規ユーザーは、Tencent Cloudの公式ウェブサイトで[登録](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F)する必要があります。詳細については、[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)をご参照ください。
2. [Tencent CVMの紹介画面](https://intl.cloud.tencent.com/product/cvm)にアクセスし、【今すぐ購入】をクリックします。

<span id="SelectType"></span>
## デバイスモデルの選択

>
1. 画面の指示に従って次の情報を設定します。
![リージョンとモデルを選択する](https://main.qcloudimg.com/raw/07493412dd043911fe8aa3ecb0d0bcd4.png)
<table>
<tr><th style="width: 20%">カテゴリ</th><th style="width: 12%">記入必須/オプション</th><th>設定の説明</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/213/2180">課金モード</a></td><td>記入必須</td><td><ul><li><b>従量課金</b>：CVMの柔軟な課金モード</li><ul></td></tr>
<tr><td>リージョン</td><td>記入必須</td><td>アクセスのレイテンシーを低減し、アクセス速度を向上させるために、お客様のユーザーに最も近いリージョンを選択することをお勧めします。</td></tr>
<tr><td>アベイラビリティーゾーン</td><td>記入必須</td><td>実際のニーズに応じてアベイラビリティーゾーンを選択します。</br>複数のCVMを購入する必要のある場合は、異なるアベイラビリティーゾーンを選択することで災害復帰効果を実現することをお勧めします。</td></tr>
<tr><td>ネットワーク</td><td>記入必須</td><td>Tencent Cloudで構築された、論理的に隔離されているネットワークスペースを示します。1つのVirtual Private Cloud(VPC)には、少なくとも1つのサブネットが含まれます。システムは、各リージョンにデフォルトのVPCとサブネットを提供します。</br>
既存のVPC/サブネットが要件を満たしていない場合は、VPCコンソールでVPCまたはサブネットを作成できます。</br><b>注</b>：<ul><li>同じVPC内のリソースはデフォルトでプライベートネットワークを相互接続します。</li><li>CVMを購入するときは、CVMとCVMが作成されるサブネットに同じアベイラビリティーゾーンにあることを確認してください。</li></ul></td></tr>
<tr><td>インスタンス</td><td>記入必須</td><td>基盤となるハードウェアの違いによって、現在、Tencent Cloudは、さまざまなインスタンスタイプを提供します。最適なパフォーマンスを実現するために、最新世代のインスタンスタイプを使用することをお勧めします。</br>インスタンスの詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/11518">インスタンスタイプをご参照ください</a>。</td>
<tr><td>イメージ</td><td>記入必須</td><td> Tencent Cloudは、パブリックイメージ、カスタムイメージ、共有イメージを提供します。イメージの詳細については、<a href = "https：//intl.cloud.tencent.com/document/product/213/4941">イメージ種類</a>を参照して選択できます。</br> Tencent Cloudを使用し始めたばかりのユーザーは、パブリックイメージを選択することを推奨します。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">システムディスク</a></td><td>記入必須</td><td>OSのインストールに使用されます。容量はデフォルトで50GBです。</br>リージョンによって、選択可能なCloud Block Storage(CBS)の種類が異なります。実際の画面の指示に従って選択してください。</br>CBSの詳細については、<a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS種類</a>をご参照ください。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">データディスク</a></td><td>オプション</td><td>CVMのストレージ容量を拡張し、効率的で信頼性の高いストレージデバイスを提供するために使用されます。 CBSデータディスクはデフォルトでは追加されません。</br>CBSの詳細については、<a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS種類</a>をご参照ください。</td></tr>
<tr><td>パブリックネットワーク帯域幅</td><td>記入必須</td><td> Tencent Cloudは、次の2つのネットワーク課金方式を提供します。実際のニーズに応じて選択してください。<ul><li><b>帯域幅課金</b>：固定帯域幅を指定します。指定した帯域幅を超えるとパケットロスが発生します。ネットワークの変動が小さい場合に適しています。</li><li><b>トラフィック課金</b>：実際に使用されるトラフィックに基づいて課金されます。ピーク帯域幅を制限することで、偶発的なトラフィックによる費用を回避することができます。瞬時帯域幅がこの値を超えるとパケットロスが発生します。ネットワークの変動が大きい場合に適しています。</li></ul></td></tr>
<tr><td>パブリックゲートウェイ</td><td>オプション</td><td>VPCとパブリックネットワーク間のネットワークインターフェースとして、パブリックゲートウェイは、VPCの異なるサブネット内にあり、パブリックIPアドレスを持たないCVMのリクエストを転送できます。</br><b>注：</br>Tencent Cloudは2019年12月6日以降は、CVM購入画面でのパブリックゲートウェイの設定確認をサポートしません。パブリックゲートウェイを設定するには、<a href="https://intl.cloud.tencent.com/document/product/213/34835">パブリックゲートウェイの設定</a>をご参照ください。</td></tr> 
<tr><td>数</td><td>記入必須</td><td>購入するCVMの数を示します。</td></tr>
</table>
2. 【次へ：ホストの設定】をクリックして、ホストの設定ページに入ります。
 
## ホストの設定
1. 画面の指示に従って次の情報を設定します。
![セキュリティグループとホスト](https://main.qcloudimg.com/raw/44493e285aee4d9523e009b7690fc616.png)
<table>
<tr><th style = "width：20％">カテゴリ</th><th style = "width：12％">記入必須/オプション</th><th>設定の説明</th></tr>
<tr><td>所属プロジェクト</td><td>記入必須</td><td>デフォルトのプロジェクトが選択されています。実際のニーズに応じて、作成済みのプロジェクトを選択することで、さまざまなCVMを管理できます。</td></tr>
<tr><td>セキュリティグループ</td><td>記入必須</td><td>1つ以上のCVMのネットワークアクセス制御を設定するために使用されます。</br><b> ログインポート22が有効になっていることを確認してください</b>。詳細情報については、<a href="https://intl.cloud.tencent.com/document/product/213/12452">セキュリティグループをご参照ください</a>。</td></tr>
<tr><td>インスタンス名</td><td>オプション</td><td>作成するCVMの名前を示します。</br>ユーザーによるカスタマイズが可能であり、「CVM-01」が推奨されます。</td></tr>
<tr><td>ログイン方法</td><td>記入必須</td><td>必要に応じて、CVMにログインする方法を設定します。<ul><li><b>カスタムパスワード</b>：インスタンスのログインパスワードをカスタマイズ設定します。</li><li><b>SSHキーペア</b>：インスタンスをSSHキーに関連付けて、SSHキーを介してCVMにより安全にログインします。</br>キーがない場合、または既存のキーが適切でない場合は、【今すぐ作成】をクリックして作成できます。SSHキーの詳細情報については、<a href="http://cloud.tencent.com/doc/product/213/SSH%E5%AF%86%E9%92%A5">SSHキー</a>をご参照ください。</li><li><b>パスワードの自動生成</b>：自動生成されたパスワードは、<a href="https://console.cloud.tencent.com/message">サイト内メール</a>の形で送信されます。</li></ul></td></tr>
<tr><td>セキュリティーサービス</td><td>オプション</td><td>デフォルトでは、セキュリティサービスは無料で有効になっており、CVMセキュリティシステムを構築してデータ漏洩を防止するのに役立ちます。</td></tr>
<tr><td>クラウドモニタリング</td><td>オプション</td><td>デフォルトでは、クラウドモニタリングは無料で有効になっています。包括的なCVMデータ監視、インテリジェントなデータ分析、リアルタイムな故障アラーム、およびデータレポートのカスタマイズ設定を提供します。これにより、ユーザーは業務とCVMのヘルス状態を正確に把握できます。</td></tr>
<tr><td>高度な設定</td><td>オプション</td><td>実際のニーズに応じて、インスタンスの追加設定を構成します。<ul><li><b>ホスト名</b>：ユーザーは、CVM OS内のコンピューターの名前をカスタマイズ設定できます。CVMが作成されたら、CVMにログインしてホスト名を表示できます。</li><li><b>CAMロール</b>：ロールを設定し、それを使用して、Tencent Cloudのサービス、操作およびリソースへのアクセス権をロールエンティティに付与できます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/38290">インスタンスロールの管理</a>をご参照ください。</li><li><b>Placement Group</b>：必要に応じて、インスタンスをplacement groupに追加し、業務の可用性を向上させます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/15486">Placement Group</a>をご参照ください。</li><li><b>タグ</b>：タグを設定した後、CVMリソースをカテゴリ別に管理できます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/19548">タグ</a>をご参照ください。</li><li><b>カスタムデータ</b>：カスタムデータを指定してインスタンスを設定できます。インスタンスの起動時に設定済みのスクリプトが実行されます。一度に複数のCVMを購入する場合、カスタムデータがすべてのCVMで実行されます。Linux OSは、Shell形式をサポートし、最大で16KBの生データをサポートします。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/17525">カスタムデータ</a>をご参照ください。</br><b>注</b>：カスタムデータ設定は、Cloudinitサービスを持つ一部のパブリックイメージのみサポートしています。詳細については、<a href = "https://intl.cloud.tencent.com/document/product/213/ 19670"> Cloud-Init</a> をご参照ください。</li></ul></td></tr> 
</table>
2.【次へ：構成情報の確認】をクリックして、構成情報の確認画面に入ります。


## 構成情報の確認

1. 購入したCVM情報を確認し、各構成の費用明細を確認します。
2. 【今すぐ購入】/【アクティブ】をクリックして支払いを完了します。支払いが完了したら、[CVMコンソール](https://console.cloud.tencent.com/cvm)にログインしてCVMを表示できます。
CVMのインスタンス名、パブリックIPアドレス、プライベートIPアドレス、ログイン名、初期ログインパスワードなどの情報は、[サイト内メール](https://console.cloud.tencent.com/message)の形でアカウントに送信されます。これらの情報を使用することで、インスタンスにログインして管理できます。また、CVMのセキュリティを確保するために、できるだけ早くCVMのログインパスワードを変更してください。

## インスタンスへのログインと接続

CVMの操作が完了したら、Tencent Cloudコンソールを介してCVMにログインし、実際のニーズに応じてサイト構築などの操作を実行できます。
必要に応じて、Tencent Cloud コンソールでCVMにログインする方法を選択します。
- [標準ログイン方法を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)
- [リモートログインソフトウェアを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSHを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32501)

## データディスクのパーティションとフォーマット

[モデルの選択](#SelectType)をする際にデータディスクを追加した場合、インスタンスにログインした後にデータディスクをフォーマットし、パーティションを作成する必要があります。**データディスクを追加していない場合は、この手順をスキップしてください。**
ディスク容量とCVM OSの種類に応じて、適切な操作ガイドを選択してください。
- ディスク容量が2TB未満の場合：
 [CBS（Linux）を初期化する](https://intl.cloud.tencent.com/document/product/362/31597)
- ディスク容量が2TB以上の場合：
 [CBS（Linux）を初期化する](https://intl.cloud.tencent.com/document/product/362/31598)

操作の詳細については、 [初期化シナリオ](https://intl.cloud.tencent.com/document/product/362/31596)をご参照ください。
