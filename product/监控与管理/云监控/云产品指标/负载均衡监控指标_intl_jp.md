Tencent Cloud CMはCLBに以下の監視メトリックを提供します。

## CLB装置のインスタンスの監視メトリック

<table class="t"><tbody><tr>
<th><b>メトリック名（日本語）</b></th>
<th><b>メトリック名（英語）</b></th>
<th><b>単位</b></th>
<th><b>ディメンション</b></th>
<tr>
<td>アクティブな接続数
<td> rrv_connum
<td> 個
<td> RS IP、RSポートとVPC ID
<tr>
<td> 非アクティブな接続数
<td> rrv_inactive_conn
<td> 個
<td> RS IP、RSポートとVPC ID
<tr>
<td> インバウンドパケット量
<td> rrv_inpkg
<td> 個/s
<td> RS IP、RSポートとVPC ID
<tr>
<td> インバウンドトラフィック
<td> rrv_intraffic
<td> bps
<td> RS IP、RSポートとVPC ID
<tr>
<td> 新規接続数
<td> rrv_new_conn
<td> 個
<td> RS IP、RSポートとVPC ID
<tr>
<td> アウトバウンドパケット量
<td> rrv_outpkg
<td> 個/s
<td> RS IP、RSポートとVPC ID
<tr>
<td> アウトバウンドトラフィック
<td> rrv_outtraffic
<td> bps
<td> RS IP、RSポートとVPC ID
</tbody></table>

## RSの監視メトリック

<table><tbody><tr>
<th><b>メトリック名（日本語）</b></th>
<th><b>メトリック名（英語）</b></th>
<th><b>単位</b></th>
<th><b>ディメンション</b></th>
<tr>
<td>アクティブな接続数
<td> rv_connum
<td> 個
<td> RS IPとVPC ID
<tr>
<td> 非アクティブな接続数
<td> rv_inactive_conn
<td> 個
<td> RS IPとVPC ID
<tr>
<td> インバウンドパケット量
<td> rv_inpkg
<td> 個/s
<td> RS IPとVPC ID
<tr>
<td> インバウンドトラフィック
<td> rv_intraffic
<td> bps
<td> RS IPとVPC ID
<tr>
<td> 新規接続数
<td> rv_new_conn
<td> 個
<td> RS IPとVPC ID
<tr>
<td> アウトバウンドパケット量
<td> rv_outpkg
<td> 個/s
<td> RS IPとVPC ID
<tr>
<td> アウトバウンドトラフィック
<td> rv_outtraffic
<td> bps
<td> RS IPとVPC ID
</tbody></table>

## RSポートレベルの監視メトリック

<table class="t"><tbody><tr>
<th><b>メトリック名</b></th>
<th><b>意味</b></th>
<th><b>単位</b></th>
<th><b>ディメンション</b></th>
<tr>
<td> アクティブな接続数（ポートレベル）
<td> rrv_connum
<td> 個
<td> RS IP、RSポートとVPC ID
<tr>
<td> 非アクティブな接続数（ポートレベル）
<td> rrv_inactive_conn
<td> 個
<td> RS IP、RSポートとVPC ID
<tr>
<td> インバウンドパケット量（ポートレベル）
<td> rrv_inpkg
<td> 個/s
<td> RS IP、RSポートとVPC ID
<tr>
<td> インバウンドトラフィック（ポートレベル）
<td> rrv_intraffic
<td> bps
<td> RS IP、RSポートとVPC ID
<tr>
<td> 新規接続数（ポートレベル）
<td> rrv_new_conn
<td> 個
<td> RS IP、RSポートとVPC ID
<tr>
<td> アウトバウンドパケット量（ポートレベル）
<td> rrv_outpkg
<td> 個/s
<td> RS IP、RSポートとVPC ID
<tr>
<td> アウトバウンドトラフィック（ポートレベル）
<td> rrv_outtraffic
<td> bps
<td> RS IP、RSポートとVPC ID
</tbody></table>


CLBの監視メトリックの詳細については、CM APIで[監視データAPIの読み取り](https://cloud.tencent.com/doc/api/405/4667)を確認することができます。


