カスタム構成は、より豊富なイメージプラットフォーム、およびストレージ、帯域幅、セキュリティグループなどの高度な設定を提供し、必要に応じて適切な構成を選択できます。このドキュメントでは、カスタム構成を例に詳しく説明します。

## 登録と認証

CVMを使用する前に、次の操作を実行する必要があります。
1. Tencent Cloudアカウントを登録し、実名認証を完了する必要があります。実名認証が完了していない場合は、中国本土のCVMインスタンスを購入できません。
新規ユーザーは、Tencent Cloudの公式ウェブサイトに[登録](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F)する必要があります。詳細については、[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)をご参照ください 。
2. [Tencent Cloud CVMの紹介画面](https://intl.cloud.tencent.com/product/cvm)にアクセスし、【今すぐ購入】をクリックします。

<span id="SelectType"></span>
## モデルの選択

1.画面の指示に従って次の情報を設定します
![リージョンとモデルを選択する](https://main.qcloudimg.com/raw/40c2812ff1294f901238cc3e39ba25f9.png)
<table>
<tr><th style="width：20％">カテゴリー</th><th style="width: 12%">選択必須/オプション</th><th>説明</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/213/2180">課金方式</a></td><td>選択必須</td><td><ul><li><b>従量課金</b>：CVMの柔軟な課金方法</li></ul></td></tr>
<tr><td>リージョン</td><td>選択必須</td><td>アクセス遅延を低減し、アクセス速度を向上させるために、お客様のユーザーに最も近いリージョンを選択することをお勧めします。</td></tr>
<tr><td>アベイラビリティーゾーン</td><td>選択必須</td><td>実際のニーズに応じてアベイラビリティーゾーンを選択します。</br>複数のCVMを購入する必要のある場合は、迅速な災害復旧を実現するために異なるアベイラビリティーゾーンを選択することをお勧めします。</td></tr>　
<tr><td>ネットワーク</td><td>選択必須</td><td>Tencent Cloudに構築された、論理的に分離されたネットワークスペースを示します。1つのVirtual Private Cloudは、少なくとも1つのサブネットが含まれます。システムは、各リージョンにデフォルトのVPCとサブネットを提供します。</br>
既存のVPC/サブネットがお客様の要件を満たしていない場合、VPCコンソールでVPCまたはサブネットを作成できます。</br><b>注意</b>：<ul><li>同じVPC内のリソースは、プライベートネットワーク内で共有できます。</li><li>CVMを購入する時、CVMは同じアベイラビリティーゾーン属性を持つサブネットに作成する必要があります。</li></ul></td></tr>
<tr><td>インスタンス</td><td>選択必須</td><td>基盤となるハードウェアの違いによって、現在、Tencent Cloudは、さまざまなインスタンスタイプを提供します。最適なパフォーマンスを実現するために、新世代種類のインスタンスの使用をお勧めします。</br>インスタンスの詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/11518">インスタンス仕様</a>をご参照ください。</td></tr>
<tr><td>イメージ</td><td>選択必須</td><td>Tencent Cloudは、パブリックイメージ、カスタムイメージ、共有イメージを提供します。 <a href="https://intl.cloud.tencent.com/document/product/213/4941">イメージタイプ</a>を参照して選択してください。</br>Tencent Cloudの使用を開始したばかりの場合、パブリックイメージを選択することをお勧めします。パブリックイメージにはWindows OSの正規版を含み、別途料金が発生することはありません（北米地域を除く）。 </td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">システムディスク</a></td><td>選択必須</td><td>OSのインストールに使用されます。 容量はデフォルトで50 GBです。</br>リージョンによって、選択可能なCloud Block Storageの種類が異なります。ページの指示に従って選択してください。</br>CBSの詳細については、<a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS種類</a>をご参照ください。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">データディスク</a></td><td>オプション</td><td>CVMのストレージ容量を拡張し、効率的で信頼性の高いストレージデバイスを提供するために使用されます。CBSデータディスクはデフォルトでは追加されません。</br>CBSの詳細については、<a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS種類</a>をご参照ください。</td></tr>
<tr><td>パブリックネットワーク帯域幅</td><td>選択必須</td><td>Tencent Cloudは、次の2種類のネットワーク課金方式を提供します。実際のニーズに応じて選択してください。<ul><li><b>帯域幅課金</b>：固定帯域幅を指定します。指定した帯域幅を超えるとパケットロスが発生します。ネットワークの変動が小さいシナリオに適しています。</li><li><b>従量課金</b>：実際に使用されるトラフィックに基づいて課金されます。ピーク帯域幅を指定することで、予期しないトラフィック料金の発生を防ぎます。瞬時帯域幅がこの値を超えるとパケットロスが発生します。ネットワークの変動が大きいシナリオに適しています。</li></ul></td></tr>
<tr><td>数 </td><td>選択必須 </td><td>購入が必要なCVMの数を示します。</td></tr>
</table>
2. 【次へ：ホストの設定】をクリックして、ホストの設定ページに入ります。

## ホストの設定
1.画面の指示に従って次の情報を設定します。
![セキュリティグループとホスト](https://main.qcloudimg.com/raw/be9b22616da76afd527f855368707899.png)
<table>
<tr><th style="width：20％">カテゴリー</th><th style="width: 12%">選択必須/オプション</th><th>説明</th></tr>
<tr><td>セキュリティグループ</td><td>選択必須</td><td>は、単一または複数のCVMのネットワークアクセス制御を設定するために使用されます。</br><b>ログインポート3389が開いていることを確認します。</b>詳細情報については、<a href="https://intl.cloud.tencent.com/document/product/213/12452">セキュリティグループ</a>をご参照ください。</td></tr>
<tr><td>所属プロジェクト</td><td>選択必須</td><td>デフォルトのプロジェクトが選択されています。必要に応じて既存のプロジェクトを選択して、さまざまなCVMを管理できます。</td></tr>
<tr><td>タグ</td><td>オプション</td><td>CVMインスタンスを分類および管理するために使用されます。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/19548">タグを使ってインスタンスを管理する</a>ドキュメントをご参照ください。</td></tr>
<tr><td>インスタンス名</td><td>オプション</td><td>作成するCVMの名前を示します。</br>ユーザーによるカスタマイズが可能であり、「CVM-01」が推奨されます。</td></tr>
<tr><td>ログイン方法</td><td>選択必須</td><td>ユーザーがCVMにログインするための方法を設定します。実際のニーズに応じて設定してください。<ul><li><b>パスワードの設定</b>：インスタンスのログインパスワードをカスタマイズできます。</li><li><b>キーを関連付ける：インスタンスのログイン資格情報としてキーペアを設定します。（Linux OSのみサポートします）。</li><li><b>パスワードの自動生成</b>：自動生成されたパスワードは、 <a href="https://console.cloud.tencent.com/message">サイト内メール</a>の形で送信されます。</li></ul></td></tr>
<tr><td>セキュリティーサービス</td><td>オプション</td><td>セキュリティサービスは無料でご利用いただけます。CVMセキュリティシステムを構築してデータ漏洩を防止するのに役立ちます。</td></tr>
<tr><td>クラウド監視</td><td>オプション</td><td>クラウド監視サービスは無料でご利用いただけます。包括的なCVMデータ監視、インテリジェントなデータ分析、リアルタイムの故障アラーム、およびカスタムデータレポートを提供します。これにより、ユーザーはサービスとCVMのヘルス状態を正確に把握できます。</td></tr>
<tr><td>高度な設定</td><td>オプション</td><td>実際のニーズに応じてインスタンスの設定を追加します。<ul><li><b>ホスト名</b>：CVM OSでコンピューターの名前をカスタマイズできます。CVMが作成されたら、CVMにログインしてホスト名を表示できます。</li><li><b>CAMロール</b>：ロールを設定し、それを使用して、Tencent Cloudのサービス、操作およびリソースへのアクセス権をロールエンティティに付与できます。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/38290">インスタンスロールの管理</a> をご参照ください。</li><li><b>Placement Group</b>：必要に応じて、インスタンスをplacement groupに追加し、サービスの可用性を向上させます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/15486">、Placement Group</a> をご参照ください。</li><li><b>カスタムデータ</b>：カスタムデータを指定してインスタンスを設定できます。構成されたスクリプトは、インスタンスの起動時に実行されます。一度に複数のCVMを購入する場合、カスタムデータがすべてのCVMで実行されます。Windows OSは、PowerShell形式をサポートし、最大で16KBの生データをサポートします。詳細については、 <a href="https://intl.cloud.tencent.com/document/product/213/17525">カスタムデータ</a>をご参照ください。</br><b>注</b>：カスタムデータ設定はWindowsパブリックイメージのみサポートします。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/19670">cloudbase-init</a>をご参照ください。</li></ul></td></tr>
</table>
2.【次へ：設定情報の確認】をクリックして、設定情報の確認ページに入ります。

## 設定情報の確認

1.購入したCVM情報を照会し、各設定の費用明細を確認します。
2. 【今すぐ購入】/【アクティブ】をクリックして支払いを完了します。支払いが完了したら、[CVMコンソール](https://console.cloud.tencent.com/cvm)にログインしてCVMを表示できます。
CVMのインスタンス名、パブリックIPアドレス、プライベートIPアドレス、ログイン名、初期ログインパスワードなどの情報は、[サイト内メール](https://console.cloud.tencent.com/message)の形でアカウントに送信されます。これらの情報を使用することで、インスタンスにログインして管理できます。また、CVMのセキュリティを確保するために、できるだけ早くCVMのログインパスワードを変更してください。

## インスタンスへのログインと接続

CVMの操作が完了したら、Tencent Cloudコンソールを介してCVMにログインし、実際のニーズに応じてサイト構築などの操作を実行できます。
必要に応じて、Tencent Cloud コンソールでCVMにログインする方法を選択します。
- [RDPファイルを使用してWindowsインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5435)
- [リモートデスクトップを使用してWindowsインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32498)

## データディスクのフォーマットとパーティション

 [インスタンスタイプの選択](#SelectType)時にデータディスクを追加した場合、インスタンスにログインした後にデータディスクをフォーマットしてパーティション分割する必要があります。**データディスクを追加していない場合は、この手順をスキップしてください。**
ディスク容量とCVM OSの種類に応じて、適切な操作ガイドを選択してください。
-ディスク容量が2TB未満の場合：
[クラウドディスクを初期化する（Windows）](https://intl.cloud.tencent.com/document/product/362/31597)
- ディスク容量が2TB以上の場合：
[クラウドディスクを初期化する（Windows）](https://intl.cloud.tencent.com/document/product/362/31598)

その他の操作については、 [初期化シナリオの紹介](https://intl.cloud.tencent.com/document/product/362/31596)をご参照ください。
