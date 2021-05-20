## 操作シナリオ
現在ネイティブCentOS 8はntpサービスのインストールをサポートしていません。このため時間が不正確になる問題が発生し、chronydを使用してタイムサービスを修正する必要があります。ここではCentOS 8オペレーティングシステムのTencent CVM上にchronydタイムサービスをインストールおよび設定する方法について説明いたします。

## 操作手順
### chronydサービスのインストール設定
1. CVMインスタンスにログインします。詳細については、[標準方式を使用してLinuxインスタンス（推奨）にログイン](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。
2. 以下のコマンドを実行して、chronydサービスをインストールします。
```
yum -y install chrony
```
3. 以下のコマンドを実行して、設定ファイル`chrony.conf`を修正します。
```
vim /etc/chrony.conf
```
4. **i**を押して編集モードに切り替え、`#log measurements statistics tracking`の後に行を追加し、以下の内容を入力します。
```
server time1.tencentyun.com iburst
server time2.tencentyun.com iburst
server time3.tencentyun.com iburst
server time4.tencentyun.com iburst
server time5.tencentyun.com iburst
```
編集が完了すると以下のようになります。
![](https://main.qcloudimg.com/raw/578e072599f8d50ea188d3911a9d76c7.png)
5. **Esc**を押し、**:wq**を入力して保存後、編集モードを終了します。
6. 以下のコマンドを順番に実行して、起動時に自動的に有効化され、サービスを再起動するように、chronydサービスを設定します。
```
systemctl restart chronyd
```
```
systemctl enable chronyd
```

### サービス設定の確認
1. 以下のコマンドを実行して、時間が同期されるかどうか確認します。
```
date
```
2. 以下のコマンドを実行して、時間同期ソースのステータスを表示します。
```
chronyc sourcestats -v
```
以下のような結果が表示される場合は、設定が成功したことを示します。
![](https://main.qcloudimg.com/raw/6a5f584638de922f5e80b5b138541c9e.png)

## 付録
### よく使用するコマンド
<table>
<tr>
<th>コマンド</th><th>説明</th>
</tr>
<tr>
<td>
<code>chronyc sources -v</code>
</td>
<td>時間同期ソースを確認します。</td>
</tr>
<tr>
<td>
<code>chronyc sourcestats -v</code>
</td>
<td>時間同期ソースのステータスを確認します。</td>
</tr>
<tr>
<td>
<code>timedatectl set-local-rtc 1</code>
</td>
<td>ハードウェアの時間を設定します。ハードウェアの時間のデフォルトはUTCです。
</td>
</tr>
<tr>
<td>
<code>timedatectl set-ntp yes</code>
</td>
<td>NTP時間同期を有効化します。</td>
</tr>
<tr>
<td>
<code>chronyc tracking</code>
</td>
<td>タイムサーバーを調整します。</td>
</tr>
<tr>
<td>
<code>chronyc -a makestep</code>
</td>
<td>システムクロックを強制的に同期します。</td>
</tr>
</table>
