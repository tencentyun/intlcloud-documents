## 問題の説明
ログ収集で例外が発生し、関連付けられているサーバーグループは例外であることがわかりました。

## 考えられる原因
サーバーグループとCLSシステムとの間のハートビートが中断され、ログの収集と報告が失敗します。サーバーグループの例外の考えられる原因は次のとおりです。  
1.IPアドレスが正しくありません。  
2.ネットワークが切断されています。  
3.LogListenerは失敗します。  
4.LogListenerの構成が正しくありません。

## 解決策
上記の原因に従って問題を解決してください。

## 手順
1.サーバーグループに追加されているIPアドレスが正しいか確認してください。  
2.次のコマンドでネットワークが接続されているか確認してください。
```shell
telnet <region>.cls.myqcloud.com 80
```
その中で、`<region>`はCLSが存在する地域の略語です。詳細な地域情報については、[Available Region](https://cloud.tencent.com/document/product/614/18940)ドキュメントを参照してください。
通常の接続では、以下のコードが表示されます。そうでなければ、接続に失敗します。ネットワーク環境をチェックして、正常なネットワーク接続を確認する必要があります。
![](https://main.qcloudimg.com/raw/2660316a4496ac356b6e7ca5cdeb9daa.png)
3.LogListenerプロセスが正常に動作しているかどうかを確認します。インストールディレクトリに入り、次のコマンドを実行します。
```shell
cd loglistener/tools && ./p.sh
```
一般的に、下記の通り3つのプロセスがあります。
```shell
bin/loglistenerm -d                                #デーモン
bin/loglistener --conf=etc/loglistener.conf        #主要プロセス   
bin/loglisteneru -u --conf=etc/loglistener.conf    #アップデートプロセス
```
**失敗したプロセスがある場合**、再起動してインストールディレクトリに入り、次のコマンドを実行する必要があります。
```shell
cd loglistener/tools && ./start.sh
```
4.LogListenerのキーとIP IDの構成情報が間違っていないかを確認してください。構成ファイルのパス：`/loglistener/etc/loglistener.conf`。
![](https://main.qcloudimg.com/raw/cfa012cfb136cbbcf78667d4d1307d26.png)
 - キーは、Tencent Cloudアカウントまたは協力者のAPIキーですが、プロジェクトキーはサポートされていません。
 - 構成ファイルのgroup_ip情報は、コンソールサーバーグループに入力されているIPアドレスと同じである必要があります。LogListenerは自動的にサーバーIPを取得します。サーバーに複数のENIがある場合、それらが一致しているかどうかを確認します。

