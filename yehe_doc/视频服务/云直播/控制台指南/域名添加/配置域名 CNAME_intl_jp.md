ドメイン名がCSSへ接続した後、システムは一つのCNAMEドメイン名（`.tlivecdn.com`を拡張子とする）を自動的にアサインし、**[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)**リスト内で表示できます。CNAMEドメイン名は直接アクセスできず、ドメイン名サービスプロバイダでCNAME設定を完了する必要があります。設定が有効になると、CSSを利用できます。


## 注意事項
- プッシュドメイン名と再生ドメイン名はどちらもCNAME解析を完了してください。
- ドメイン名前解決プロバイダにアクセスして、CNAMEレコードを設定してください。具体的な操作については、お客様のドメイン名前解決プロバイダにお問い合わせください。
- CNAME設定が完了してから約15分で有効となります。マルチレベルCNAMEを設定した場合、CSSは名前解決結果を効果的に監視できません。実際のアクセス状況をご参照ください。
- CNAME設定完了後にその旨が長時間表示されない場合、[ドメイン名設定関連](https://intl.cloud.tencent.com/document/product/267/32478)をご参照ください。

## 前提条件
- ドメイン名を準備したこと。
- CSSコンソールの**[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)**で[独自のドメイン名の追加](https://intl.cloud.tencent.com/document/product/267/35970)が完了し、ドメイン名の所有権検証が完了し、ドメイン名CNAMEのアドレスステータスが![](https://main.qcloudimg.com/raw/ed1ac2f8541f629814a3f2420b1eb79c.png)（CNAME未設定）であること。



## 設定手順
このドキュメントでは、Tencent Cloud、Alibaba Cloud、Baidu Cloud、DNSPod、HiChina、XinnetでのCNAMEドメイン名前解決の設定を例とします。操作手順はあくまで参考で、実際の設定と合わない場合は、ご自身のDNSプロバイダの情報を正としてください。ドメイン名CNAMEの設定が完了すると、[CNAMEの有効化状態を確認](#check)に記載された方法でドメイン名がCNAMEを完了しているかどうかを検証できます。

[](id:tencent)
### CNAMEのワンタッチ設定
ドメイン名をTencent Cloud DNSPodにホスティングしている場合は、ワンタッチでCNAMEを設定できます。
1. ライブストリーミングコンソール[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)にログインすると、次の3つの方法でCNAMEプロセスをワンタッチ設定できます。
  - 「ドメイン名管理」ページで、ドメイン名CNAMEのステータスが![](https://main.qcloudimg.com/raw/ed1ac2f8541f629814a3f2420b1eb79c.png)であることを確認します。通知メッセージで**ワンタッチ設定**をクリックすると入ります。
  - 「ドメイン名管理」ページでCNAMEを設定するドメイン名を選択し、ドメイン名のアドレスまたは管理をクリックして、ドメイン名の基本情報ページに移動します。基本情報で**ワンタッチ設定**をクリックして入ります。
  - 「ドメイン名管理」ページでドメイン名を追加し、基本設定を完了したらCANME設定プロセスに進みます。
2. ドメイン名の有効状態が未有効の場合は、ワンタッチで設定できます。設定は約**15分**後に有効になります。

3. ドメイン名前解決レコードの追加に失敗した場合、Tencent Cloudの[DNSPod](https://console.cloud.tencent.com/cns)コンソールで処理することができます。

   

[](id:dnspod)

### DNSPodでの設定方法
DNSプロバイダがDNSPodの場合は、下記の手順でCNAMEレコードを追加できます。
1. [DNSPodドメイン名サービスコンソール](https://console.dnspod.cn/dns/list)にログインします。
2. リストから、CNAMEレコードを追加するドメイン名がある行を見つけて、対応するドメイン名をクリックし、「レコードの追加」インターフェースにジャンプします。
3. 以下の手順でCNAMEレコードを追加します。
    1.ホストレコードにサブドメイン名を記入します。（例えば、`www.123.com`の解決を追加する場合は、ホストレコードに`www`を記入します。`123.com`の解決のみを追加する場合は、ホストレコードを空にします。システムは自動的に「@」を入力ボックスに記入します。@のCNAMEはMXレコードの正常な解決に影響を与えるため、慎重に追加してください。）
  2. ログ種類はCNAMEです。
  3. 回線タイプ：「デフォルト」タイプを選択します。選択しないと、一部のユーザーが名前解決できません。
例えば、聯通ユーザーを2.comに、聯通以外ののユーザーを1.comに指定する必要があります。これを行うには、回線タイプがデフォルトで、レコード値が1.com、そして回線タイプが聯通で、レコード値が2.comの2つのCNAMEレコードを追加します。
  4. レコード値がCNAMEのリンク先であるドメイン名について、ドメイン名のみを入力可能です。レコードが生成されると、ドメイン名の後ろに「.」が自動的に追加されますが問題ありません。
  5. MXの優先度は、記入不要です。
  6. TTLは追加時にシステムによって自動的に生成されるので、記入する必要はありません。デフォルト値は600秒です。（TTLはキャッシュ時間であり、値が小さいほど、レコードの修正が各地で反映されるまでの時間が短くなります。）

[](id:ali)
### Alibaba Cloud設定方法
お客様のDNSプロバイダがAlibaba Cloudであり、ドメイン名のICP登録が完了している場合は、次の手順を参照してCNAMEを設定することができます。

1. Alibaba Cloudコンソールにログインし、**クラウド解決DNS**>[**ドメイン名前解決**](https://dns.console.aliyun.com/#/dns/domainList)に進みます。
2. CNAMEを追加するドメイン名を選択し、**名前解決設定**をクリックします。
3. **レコードの追加**を選択し、レコードの追加ページで次の設定を行います。
  -  レコードタイプ： `CNAME`を選択します。
  -  ホストレコード：サブドメイン名のプレフィックスを入力します。再生ドメイン名が`play.myqcloud.com`の場合は、`play`を追加します。メインドメイン名の`myqloud.com`を直接解決する必要がある場合は、`@`を入力します。ワイルドカードドメイン名を解決する必要がある場合は、`\*` を入力します。
  - 解決ルート：`デフォルト`を選択することをお勧めします。
  -  レコード値：Tencent Cloudコンソールのドメイン名管理ページのドメイン名に対応するCNAME値を、`domain.tlivecdn.com`の形式で入力します。
  -  TTL：`10分間`と入力することをお勧めします。
4. **OK**をクリックすれば完了です。



[](id:baidu)
### Baidu Cloudでの設定方法
ドメイン名サービスプロバイダがBaidu Cloudの場合は、下記の手順でCNAMEレコードを追加できます。
1. Baidu Cloudコンソールにログインし、[**ドメイン名管理**](https://console.bce.baidu.com/bcd/?_=1550137564099#/bcd/manage/list)を選択し、ドメイン名の管理リストページに進みます。
2. CSSで追加したドメイン名を選択し、操作列で**名前解決**をクリックしてDNS名前解決ページに進みます。
3. 解決レコードを追加し、このページで次の設定を行います。
 - ホストレコード：セカンドレベルドメイン名、すなわちドメイン名プレフィックスを入力します。再生ドメイン名が`play.myqcloud.com`の場合は、`play`を追加します。メインドメイン名である`myqloud.com`を直接解決する必要がある場合は、`@`を入力します。ワイルドカードドメイン名を解決する必要がある場合は、`\*`を入力します。
 - レコードタイプ：`CNAMEレコード`を選択します。
 - 解決ルート：`デフォルト`を選択することをお勧めします。
 - レコード値：CSSコンソールのドメイン名管理ページのドメイン名に対応するCNAME値。形式は`domain.tlivecdn.com`です。
 - TTL：`10分間`と入力することをお勧めします。
4. **OK**をクリックしてサブミットすれば完了です。


[](id:wwwnet)
### HiChinaでの設定方法
DNSプロバイダがHiChinaの場合は、下記の手順でCNAMEレコードを追加できます。

1. HiChinaの会員センターにログインします。
2. 会員センターの左側ナビゲーションバーの**製品管理** > **マイクラウド解決**をクリックしてウェブ上のクラウド解決リストページに移動します。
3. 解析するドメイン名をクリックし、解析レコードページに入ります。
4. 解決レコードページに入ってから、**解決の追加**ボタンをクリックし、解決レコードの設定を開始します。
5. CNAME解析ログを設定する場合は、レコード種類をCNAMEに選んでください。ホストログはすなわちドメイン名のプレフィックスで、任意（例えば：`www`）を記入できます。レコード値は現在のドメイン名のリンク先となる別のドメイン名を記入してください。解析回線とTTLは、デフォルト値のままでよいです。

6. 入力後に**保存**をクリックすると、解決の設定が完了します。


[](id:xinnet)
### Xinnetでの設定方法
DNSプロバイダがXinnetの場合は、**エイリアス（CNAMEレコード）を設定する**ことでCNAMEレコードを追加できます。
エイリアスレコードによって、複数の名前を1つのコンピュータにマッピングすることが可能になります。一般的には、WWWとMAILサービスの両方を提供するコンピュータに適用されます。例えば、名前が`host.mydomain.com`（Aレコード）で、WWWとMAILサービスを同時に提供しているコンピュータがあります。ユーザーからのアクセスを便利にするために、下図に示すように、そのコンピュータにWWWとMAILの2つのエイリアス(CNAME)を設定します。

[](id:check)
## CNAMEの有効化状態を確認
DNSプロバイダによって、CNAMEの有効化にかかる時間が異なりますが、一般的には30分以内に完了します。以下の方法でCNAMEの有効化状態を確認できます。
- **方法1：**CSSコンソールの**[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)**に進んで拡張子が`.myqcloud.com`のドメイン名ステータス記号が![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png)に変更されていることを確認できれば、それはCNAMEが完了していることになります。
![](https://main.qcloudimg.com/raw/7930331f6eb7f4271014083cab27fb26.png)
- **方法2：**CSSコンソールの[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)にアクセスしてドメイン名を追加し、基本設定を設定したら、CNAME設定でCNAMEのステータスを確認できます。
- **方法3：**Linux/Macシステムにおいて、digコマンドで確認します。コマンド形式は`dig独自ドメイン名`です。1行目にCSSが提供したターゲットドメイン名の解決内容が表示されれば、それはCNAMEが完了していることになります。 
![](https://main.qcloudimg.com/raw/2cbe7fdc1c9d7dbed7851aa86dd64ff1.png)
- **方法4：**Windowsシステムにおいて、**開始** > **実行** >cmdを入力してエンターキーを押すことで、コマンド行モードで`nslookup独自ドメイン名`を入力できます。CSSが提供したターゲットドメイン名を解決済みであれば、それはCNAMEが完了していることになります。
![](https://main.qcloudimg.com/raw/765ac099e7c79a70496563f00cdab9a7.png)


>!CNAME設定完了後にその旨が長時間表示されない場合、[ドメイン名設定関連](https://intl.cloud.tencent.com/document/product/267/32478)をご参照ください。