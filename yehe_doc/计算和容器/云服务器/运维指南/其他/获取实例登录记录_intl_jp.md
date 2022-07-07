## 操作シナリオ
ここでは、CVMのユーザーログイン記録を取得し、有効な障害特定およびセキュリティ分析に役立てる方法についてご説明します。


## 操作手順

<dx-tabs>
::: Linuxインスタンス
<dx-alert infotype="explain" title="">
ここでは、LinuxインスタンスのOSがTencentOS Server 3.1 (TK4)である場合の例を示します。OSのバージョンが異なると手順も異なる場合がありますので、実際の状況に応じて操作してください。
</dx-alert>

1. [標準ログイン方式を使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5436)します。
2. 次の情報を参照し、必要に応じてユーザーログイン情報を確認します。
<dx-alert infotype="explain" title="">
ユーザーログイン情報は、通常は`/var/run/utmp`、`/var/log/wtmp`、`/var/log/btmp`、`/var/log/lastlog`などのファイルに記録されています。
</dx-alert>
 - `who`コマンドを実行し、`/var/run/utmp`で現在ログインしているユーザーの情報を確認します。下図のような結果が返されます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/2f54911fac9ee5cbeb2ca180a802f8bc.png"/>
 - `w`コマンドを実行し、`/var/run/utmp`で現在ログインしているユーザー名を確認し、そのユーザーが実行中のタスクを表示します。下図のような結果が返されます。
![](https://qcloudimg.tencent-cloud.cn/raw/401681d683aafd6cd6ab0f5ffda15cd8.png)
 - `users`コマンドを実行し、`/var/run/utmp`で現在ログインしているユーザー名を確認します。下図のような結果が返されます。
![](https://qcloudimg.tencent-cloud.cn/raw/94f318f2bfa670fae34a0a0015f7587d.png)
 - `last`コマンドを実行し、`/var/log/wtmp`で、システムに現在ログインしている、および過去にログインしたユーザーの情報を確認します。下図のような結果が返されます。
![](https://qcloudimg.tencent-cloud.cn/raw/1262a858b41be61a01d2d31e09c2cc70.png)
 - `lastb`コマンドを実行し、`/var/log/btmp`で、システムへのログインに失敗したすべてのユーザーの情報を確認します。下図のような結果が返されます。
![](https://qcloudimg.tencent-cloud.cn/raw/2208f07aba6e73fa4de6959844d38ca5.png)
 - `lastlog`コマンドを実行し、`/var/log/lastlog`で、ユーザーが最後にログインした際の情報を確認します。下図のような結果が返されます。
![](https://qcloudimg.tencent-cloud.cn/raw/85e42c825afa0bab0e1b25e18895ac52.png)
 - `cat /var/log/secure`コマンドを実行し、ログイン情報を確認します。下図のような結果が返されます。
![](https://qcloudimg.tencent-cloud.cn/raw/d75c5db721f325d56ed0ba7dd4a20c7b.png)

:::
::: Windowsインスタンス

<dx-alert infotype="explain" title="">
ここでは、WindowsインスタンスのOSがWindows Server 2012 R2中国語版である場合の例を示します。OSのバージョンが異なると手順も異なる場合がありますので、実際の状況に応じて操作してください。
</dx-alert>


1.  [標準方式を使用してWindowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/41018)します。
2.  OSの画面で、<img src="https://main.qcloudimg.com/raw/446c1e8cb7da2ce280d710c6a46b693d.png" style="margin:-6px 0px">をクリックし、サーバーマネージャーを開きます。
3. 「サーバーマネージャー」ウィンドウで、右上の**ツール** > **イベントビューア**を選択します。
4. ポップアップした「イベントビューア」ウィンドウで、左側の**Windowsログ** > **セキュリティ**を選択し、右側の**現在のログをフィルタリング**をクリックします。
5.  ポップアップした「現在のログをフィルタリング」ウィンドウで、「<すべてのイベントID>」に`4648`を入力し、**OK**をクリックします。
6. 「イベントビューア」ウィンドウで、フィルタリング条件に合致するログをダブルクリックします。
7.  ポップアップした「イベントのプロパティ」ウィンドウで、**詳細情報**をクリックすると、クライアント名およびクライアントアドレス、およびイベント記録時間などの情報を確認できます。



:::
</dx-tabs>



