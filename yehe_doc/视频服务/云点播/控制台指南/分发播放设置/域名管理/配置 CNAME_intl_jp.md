カスタムドメイン名がVODにアクセスすると、システムは自動的にCNAMEドメイン名（拡張子は.cdn.dnsv1.com）を割り当てます。VODコンソールの[ドメイン名管理](https://console.cloud.tencent.com/vod/distribute-play/domain) で確認できます。自動的に割り当てられたCNAMEドメイン名は直接アクセスできないため、ドメイン名サービスプロバイダにてCNAME設定を完了する必要があります。設定が有効になると、正常にアクセスできるようになります。

![](https://qcloudimg.tencent-cloud.cn/raw/9ddc932f9b5072705d5d155f7ed2c8b5.png)


## HiChinaでの設定方法
DNSプロバイダがHiChinaの場合は、下記の手順でCNAMEレコードを追加できます。
1. HiChina会員センターにログインします。
2. 会員センターの左側ナビゲーションバーの【製品管理】> 【マイクラウド解決】をクリックしてウェブ上のクラウド解決リスト画面に移動します。
3. 解決するドメイン名をクリックし、解決レコードページに入ります。
4. 解決レコードページに入ってから、「解決の追加」ボタンをクリックし、解決レコードの設定を開始します。

5. CNAME解決レコードを設定する場合は、レコードタイプをCNAMEに選んでください。ホストレコードはドメイン名のプレフィックスで、任意に入力できます（例えば：`www`）。レコード値は現在のドメイン名のリンク先となる別のドメイン名を入力してください。解決回線とTTLは、デフォルト値のままでかまいません。

6. 入力後に【保存】をクリックすると、解決の設定が完了します。

## Xinnetでの設定方法
DNSプロバイダがXinnetの場合は、下記の手順でCNAMEレコードを追加できます。
**エイリアスの設定（CNAMEレコード）**
エイリアスログのことです。この種類のログによって、複数のネームを一つのコンピューターにマッピングすることが可能になり、一般的には、WWWとMAILサービスの両方提供するコンピューターに適用されます。例えば、ネームが`host.mydomain.com`（Aログ）で、WWWとMAILサービスの両方を提供しているコンピューターがあります。ユーザーからのアクセスを便利にするために、下図に示すように、そのコンピューターにWWWとMAILの二つのエイリアス（CNAME）を設定します。

## CNAMEのアクティブ化状態を確認
DNSプロバイダによって、CNAMEのアクティブ化にかかる時間が異なりますが、一般的には30分以内に完了します。以下の方法でCNAME設定のアクティブ化状態を確認できます。
- 方法1：【開始】→【実行】→cmdを入力してエンターキーを押すことで、PINGコマンドを入力してCNAMEがアクティブかどうかを照会できます。返された解決結果がそのドメイン名のCNAME値と一致していれば、CNAME設定がアクティブになっています。

- 方法2：【開始】→【実行】→cmdを入力してエンターキーを押すことで、nslookupコマンドを入力してCNAMEがアクティブかどうかを照会できます。返された解決結果がそのドメイン名のCNAME値と一致していれば、CNAME設定がアクティブになっています。

