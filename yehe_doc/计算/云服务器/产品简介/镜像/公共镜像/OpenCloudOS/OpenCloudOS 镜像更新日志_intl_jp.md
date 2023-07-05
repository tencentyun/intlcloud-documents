
<dx-alert infotype="explain" title="">
- イメージ更新履歴は発行時間順で表示されます。
- イメージは地域ごとに発行されます。CVMインスタンスの作成時に更新履歴にあるイメージが最新バージョンではない場合、その地域にまだ発行されていない可能性があります。
- イメージ更新履歴内のイメージがコンソールで見つからない場合は、当該イメージが全面的に公開されていません。この場合、 [チケットを送信](https://console.intl.cloud.tencent.com/workorder/category)してイメージに関する詳細情報を取得できます。
</dx-alert>

## イメージ更新履歴

<table>
<thead>
<tr>
<th width="60%"><strong>機能更新</strong></th>
<th><strong>更新日</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>
<ul class="params">
<li> firewalld\sssd\rngd サービスを無効にしました</li>
<li> microcode_ctl/nss-softokn/avahi パッケージをアンインストールしました</li>
<li>keymapを設定しました</li>
<li>timezoneを設定しました</li>
<li>kdumpのブート用のcloudinit.target依存関係を設定しました</li>
<li>Mirrors.tencentyun.com をrepoの最初のURLとして設定しました</li>
<li>/etc/rc.d/rc.local ファイルの権限を755に変更しました</li>
<li> /var/lib/ 内の一部のディレクトリの権限エラーを修正しました</li>
</ul>
</td>
<td>2022-09-16</td>
</tr>
<tr>
<td>
<ul class="params">
<li>カーネルバージョンを5.4.119-19.0010に更新しました</li>
<li>他のユーザーモードソフトウェアを更新しました</li>
<li>イメージのタイムスタンプを更新しました</li>
</ul>
</td>
<td>2022-07-27</td>
</tr>
<tr>
<td>
<ul class="params">
<li>パブリッククラウド向けOpenCloudOS 8.5をリリースしました</li>
</ul>
</td>
<td>2022-03-04</td>
</tr>
</tbody></table>