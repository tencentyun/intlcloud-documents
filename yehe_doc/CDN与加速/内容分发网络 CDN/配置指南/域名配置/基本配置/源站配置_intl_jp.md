## 設定シーン

ドメイン名のオリジンサーバーの基本情報、Back-to-Originリクエストプロトコル、ホストヘッダーなどの情報を変更する場合、オリジンサーバー設定コンポーネントで関連操作を実施できます。

>! アクセラレーションリージョンと同じリージョンのオリジンサーバーを設定することをお勧めします。例えば、アクセラレーションリージョンが中国本土の場合、中国本土のオリジンサーバーを設定してください。オリジンサーバーが中国香港または中国本土以外にある場合、Back-to-Originが国境を越えてアクセスするため、Back-to-Originの効果を保証できません。
アクセラレーションリージョンがグローバルアクセラレーションの場合、ドメイン名の設定-オリジンサーバーの設定で、エリアにある独立したオリジンサーバーを設定できます。中国本土か中国本土以外によって、異なるオリジンサーバーへのBack-to-Originを実行することで、Back-to-Originの効果を保証します。

## 設定ガイド

### プライマリーオリジンサーバーの設定

[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、メニューバーで【ドメイン管理】を選択し、ドメイン名の右側にある【管理】をクリックすると、ドメイン名設定画面に入ります。一番上の欄の基本情報の下にオリジンサーバー設定コンポーネントがあります。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9IJQ709_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224110508.png)

**オリジンサーバータイプ**

<table>
<thead>
<tr>
<td style="width:150px">外部オリジンサーバー</td>
<td>安定して動作している業務サーバー（すなわち、オリジンサーバー）を持っている場合、業務サーバーのIPアドレスリストまたはドメイン名をオリジンサーバーのアドレスとして入力します。</td></ul>
</tr>
</thead>
<tbody><tr>
<td><a href="https://www.tencentcloud.com/products/cos">COSソース</a></td>
<td>クラウドストレージからオリジンサーバーとして1つのバケットを選択します。プライベートバケットへのアクセスを有効にすることができます。</td>
</tr>
<tr>
<td>サードパーティCOS	
</td>
<td>Tencent Cloud以外のサードパーティCOSについては、AWS S3、Alibaba Cloud OSS、Huawei OBS、QiNiu kodoをサポートします。<br/>
<strong>注：</strong>ECDNでは、サードパーティCOSがサポートされていません。</td>
</tr>
</tbody></table>


**オリジンプルプロトコル**
CDN加速ノードがユーザーオリジンサーバーにback to originしたときに使用するプロトコル（HTTPまたはHTTPS）です。

<table>
<thead>
<tr>
<td style="width:150px">HTTP Back-to-Origin</td>
<td>HTTP/HTTPSアクセスはHTTP Back-to-Originを使用します。</td></ul>
</tr>
</thead>
<tbody><tr>
<td>HTTPS Back-to-Origin</td>
<td>HTTP/HTTPSアクセスはHTTPS Back-to-Originを使用します。これにより、Back-to-Originデータの盗聴や改ざんを防ぐことができます。HTTPS Back-to-Originは、オリジンサーバーのCPUリソースを少し占有します（オリジンサーバーでHTTPSアクセスをサポートする必要がある）。</td>
</tr>
<tr>
<td>プロトコル追従</td>
<td>HTTPアクセスはHTTP Back-to-Originを使用し、HTTPSアクセスはHTTPS Back-to-Originを使用します。一部の重要なセンシティブデータのみをHTTPSプロトコルで転送し、その他の業務ではHTTPプロトコルで転送する場合、「プロトコル追従」を選択することをお勧めします（オリジンサーバーはHTTPSアクセスをサポートする必要があります）
</td>
</tr>
</tbody></table>

> !HTTPS Back-to-Originを使用する場合、オリジンサーバーでHTTPSアクセスをサポートすることを確認してください。サポートしない場合、Back-to-Originに失敗します。



**オリジンサーバーアドレス**
<table>
<thead>
<tr>
<td style="width:80px">外部オリジンサーバー</td>
<td style="padding-bottom:0px;padding-top:15px"><ul><li>オリジンサーバーとして、複数のIPまたはドメイン名（1行に1個）を入力できます。
  <br><strong>マルチIPポーリングBack-to-Origin：</strong>オリジンサーバーとして、複数のIPまたはドメイン名（1行に1個）を入力できます。Back-to-Origin中にポーリングされます。CDNではデフォルトでオリジンサーバー検出機能が有効になっています。IPのBack-to-Originに失敗し、または1分間で実行したBack-to-Originが5回を超えると、600s以内にこのIPアドレスでのBack-to-Originを実行しなくなります。600s経つと、このIPアドレスでのBack-to-Originを実行できるようになります。<br><strong>ドメイン名Back-to-Origin：</strong>オリジンサーバーとして独立したドメイン名を設定できます。 このドメイン名は、CDNアクセラレーションドメイン名を使用できません。IPv6ドメイン名Back-to-Originがサポートされません。<br><strong>注：</strong>オリジンサーバーアドレスに、CDNアクセラレーションに導入し、オリジンサーバーが現在のアクセラレーションドメイン名を指しているサイトを入力することはできません。そうすると、解析が無限ループになり、Back-to-Originに失敗します。<li>ポート(0～65535)とウェイト(1～100)が設定可能：オリジンサーバー：ポート：ウェイト（ポートを省略した場合、オリジンサーバー：：ウェイト）<br><strong>注：</strong>ウェイトは数字の大きさでソートされます。数字が大きいほど、ウェイトが大きく、Back-to-Originの優先度が高いです。<li>オリジンサーバーアドレスは最大511文字を入力できます。</td></ul>
</tr>
</thead>
<tbody><tr>
<td><a href="https://www.tencentcloud.com/products/cos">COSオリジンサーバー</a></td>
<td><li>Tencent Cloud COSからオリジンサーバーとして1つのバケットを選択します。<li>パケットの設定と実際の運用シーンに合わせて、デフォルトドメイン名、静的サイトまたはグローバルアクセラレーションドメイン名を選択します。例えば、バケットで静的サイトの設定が有効になっている場合、静的サイトを選択してください。<li>ご利用のCOSバケットへの読書き権限にプライベート読取りが設定されている場合、CDNを許可しBack-to-Origin認証を有効にする必要があります。つまり、プライベートバケットへのアクセスを許可してください。</td>
</tr>
<tr>
<td>サードパーティCOS</td>
<td style="padding-bottom:0px;padding-top:15px"><ul><li>リソースがすでにサードパーティCOSに保存されている場合、オリジンサーバーとして有効なバケットアクセスアドレスを入力してください。現在サポートしているサードパーティCOSには、AWS S3、Alibaba Cloud OSS、Huawei OBS、QiNiu kodoがあります。</br><strong>例：<code>my-bucket.s3.ap-east-1.amazonaws.com</code> または <code>my-bucket.oss-cn-beijing.aliyuncs.com</code>。</strong><code>http://</code> または <code>http://</code> プロトコルヘッダーを含むことができません。<li>サードパーティプライベートバケットへBack-to-Originする場合、有効なキーを入力しBack-to-Origin認証を有効にする必要があります。つまり、プライベートバケットへのアクセスを許可してください。</td>
</tr></ul>
</tbody></table>




**Origin domain**
Origin domainとは、back-to-origin中にCDNノードがオリジンサーバーのIPアドレスでアクセスするWebサイトのドメイン名を指します。具体的な設定例の説明については、[Origin domainの設定](#exp)をご参照ください。

> ?オリジンサーバーアドレスとOrigin domainの違いは以下の通りです：
> - オリジンサーバーアドレス：back-to-originリクエストの送信先のIPアドレスを指定します。
> - Origin domain：back-to-originリクエストの送信先のIPアドレスに対応するWebサイトを指定します。

<table>
<thead>
<tr>
<td style="width:80px">外部オリジンサーバー</td>
<td >デフォルトでは、現在のアクセラレーションドメイン名とします。ワイルドカードドメイン名が接続されている場合、ワイルドカードドメイン名になり、実際のOrigin domainはアクセスドメイン名になります。実際の業務状況に応じて変更できます。</td></tr>
</thead>
<tbody><tr>
<td><a href="https://www.tencentcloud.com/products/cos">COSオリジンサーバー</a></td>
<td>デフォルトでは、バケットのアクセスアドレスとし、オリジンサーバーのアドレスと同じで、変更できません。</td>
</tr>
<tr>
<td>サードパーティCOS</td>
<td>デフォルトでは、バケットのアクセスアドレスとし、オリジンサーバーのアドレスと同じで、変更できません。</td>
</tr>
</tbody></table>



### ホットバックアップオリジンサーバーの設定

プライマリオリジンサーバーにホットバックアップオリジンサーバーを追加できます。すべてのBack-to-Originリクエストは、最初にプライマリオリジンサーバーに転送されます。4XXまたは5XXエラーコードが返された場合、または接続タイムアウト、プロトコル非互換などが発生した場合、リクエストがホットバックアップオリジンサーバーに転送され、リソースを取得し、Back-to-Originの高可用性を確保します。

ホットバックアップオリジンサーバーは独自のオリジンサーバーアドレスとOrigin domainを設定できます。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fBH6442_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224110649.png)

>!
>- ホットバックアップオリジンサーバーのオリジンサーバータイプは、COSオリジンサーバーとサードパーティCOSをサポートしません。
>- プライマリオリジンサーバーでIPv6オリジンサーバーが有効になっている場合、ホットバックアップオリジンサーバーの追加がサポートされません。
>- ホットバックアップオリジンサーバーで、ウェイトの設定がサポートされません。

### リージョンの特別な設定

ご利用のアクセラレーションドメイン名のサービス提供リージョンがグローバルの場合、国際トラフィックの発生を防ぐために、ドメイン名のサービス提供リージョンごとにオリジンサーバーを設定したければ、下部にある**リージョンごとの設定**をクリックしてください。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XXa9147_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224112431.png)
異なるBack-to-Originポリシーを設定するリージョンを選択し、対応するオリジンサーバーの情報を入力します。具体的な設定例の説明については、[リージョンの特別な設定](#special)をご参照ください。

>!
>
>- オリジンサーバーのタイプがサードパーティCOSの場合、リージョンの特別な設定がサポートされません。


## 設定例

### Origin domainの設定[](id:exp)

CDNオリジンサーバーの設定が以下の場合、アクセラレーションドメイン名「www.test.com」の設定を以下だとすれば、
![](https://main.qcloudimg.com/raw/ec2e007bb32723f7dd12aac17524c8af.png)
ユーザーアクセスパスは次のとおりです：
ユーザーはリソース`http://www.test.com/test.txt`にアクセスします。この時点では、CDNノードにこのリソースがキャッシングされていない場合、CDNノードのBack-to-Originは`www.abc.com`ドメイン名を解決してオリジンサーバーのアドレスを取得します。オリジンサーバーのアドレスを`1.1.1.1`とすれば、`1.1.1.1`サーバーにアクセスし、その上のWebサイトwww.def.comのパス配下にあるtest.txtファイルを見つけて、ユーザーに返します。


[](id:special)
### リージョンの特別な設定

Tencent Cloud CDNオリジンサーバーの設定が以下の場合、アクセラレーションドメイン名「www.test.com」の設定を以下のとおりであるとすると：
![](https://main.qcloudimg.com/raw/e9104ca2b0e38c62bdffb022a933b2b9.png)
実際のBack-to-Originは次のとおりです：

1. 中国本土のユーザーが`http://www.test.com/test.txt`ファイルにアクセスします。中国本土のノードにこのリソースがキャッシングされていない場合、Back-to-Originリクエストがサーバー`1.1.1.1`に転送されます。Webサイト`1.test.com`にあるtest.txtファイルを見つけて、このリソースがあれば直接ユーザーに返します。このリソースがなければ、ステップ2に進みます。
2. CDN中国本土のノードがプライマリオリジンサーバーへのBack-to-Originに失敗し、リソースが見つからなかった場合、Back-to-Originリクエストはサーバー`2.2.2.2`に転送されます。Webサイト`2.test.com`にあるtest.txtファイルを見つけて、ユーザーに返してキャッシングします。
3. この時点で、中国本土以外のユーザーも`http://www.test.com/test.txt`ファイルにアクセスするとすれば、中国本土以外のノードにこのリソースがキャッシングされていない場合、Back-to-Originリクエストがサーバー`3.3.3.3`に転送されます。Webサイト`3.test.com`にあるtest.txtファイルを見つけて、このリソースがあれば直接ユーザーに返します。このリソースがなければ、ステップ4に進みます。
4. CDN中国本土以外のノードが中国本土以外のプライマリオリジンサーバーへのBack-to-Originに失敗し、リソースが見つからなかった場合、Back-to-Originリクエストがサーバー`4.4.4.4`に転送されます。Webサイト`4.test.com`にあるtest.txtファイルを見つけて、中国本土以外のユーザーに返してキャッシングします。
