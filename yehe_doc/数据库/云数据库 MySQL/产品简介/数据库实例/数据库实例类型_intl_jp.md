データベースインスタンスはTencent Cloudで実行される独立したデータベース環境です。データベースインスタンスには、ユーザーが作成した複数のデータベースを含めることができ、スタンドアロンデータベースインスタンスにアクセスする場合と同じクライアントツールやアプリケーションを使用してアクセスできます。

TencentDB for MySQLには次の2種類のデータベースインスタンスがあります。

<table>
<thead><tr>
<th>インスタンスタイプ</th><th width="20%">定義</th><th width="15%">アーキテクチャ</th><th>インスタンスリストに表示</th><th>機能</th></tr></thead>
<tbody><tr>
<td>ソースインスタンス</td><td>読み取り/書き込み可能なインスタンス</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">シングルノード</a> <li><a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">2ノード</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39783" target="_blank">3ノード</a></td>
<td>はい</td><td>ソースインスタンスは、読み取り/書き込み分離のために読み取り専用インスタンスをマウントできます</td></tr>
<tr>
<td>読み取り専用インスタンス</td><td>読み取り機能のみを提供するインスタンス</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">シングルノード</a></td><td>はい</td>
<td>読み取り専用インスタンスは単独で存在することはできません。ある特定のソースインスタンスに関連付けられている必要があります。唯一のデータソースはソースインスタンスからのデータ同期であり、ソースインスタンスと同じリージョンにある必要があります</td>


### 関連情報
- 読み取り専用インスタンスの作成方法と注意事項については、[読み取り専用インスタンスの作成](https://intl.cloud.tencent.com/document/product/236/7270)をご参照ください。
- 読み取り専用インスタンスのROグループの作成と設定については、[読み取り専用インスタンスの管理](https://intl.cloud.tencent.com/document/product/236/11361)をご参照ください。

  
