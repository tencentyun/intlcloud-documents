サイトのリソースが違法なサイトによってダウンロードされ、盗用されないよう保護するために、必要に応じてType ABCDの4つの認証方式の1つを選択できます。ここでは、Type Cの各パラメータフィールドと原理について詳しくご説明します。

**アルゴリズムの説明**

-  **アクセスURLの形式**
`http://DomainName/md5hash/timestamp/FileName` 
  >!アクセスURLに中国語を含むことはできません。

-  **認証フィールドの説明**
  <table>
  <thead>
  <tr>
  <th>フィールド</th>
  <th>説明</th>
  </tr>
  </thead>
  <tbody><tr>
  <td>DomainName</td>
  <td>CDNドメイン名。</td>
  </tr>
  <tr>
  <td>Filename</td>
  <td>リソースのアクセスパスは、認証時に Filenameがスラッシュ（ <code>/</code> ）で始まる必要があります。</td>
  </tr>
  <tr>
  <td>timestamp</td>
  <td>サーバーが認証URLを発行する時間は、16進数の整数型の正数のUnixタイムスタンプを使用し、UTC時間1970年01月01日00時00分00秒から現在の総秒数までで、その定義と所在するタイムゾーンは関係ありません。</td>
  </tr>
  <tr>
  <td>md5hash</td>
  <td>MD5アルゴリズムによって計算した固定長は32桁の文字列です。具体的な計算公式は次のとおりです： <br>•  md5hash = md5sum(pkeytimestampuri) パラメータの間にはいかなる符号もありません  <br>•  pkey： カスタムキー：6 ～40桁のアルファベットの大文字、小文字と数字で構成されています。キーを大切に保管してください。クライアントとサーバーのみ知っている必要があります。 <br>•   uri リソースのアクセスパスはスラッシュ（/）で始まる必要があります。 <br>•  timestamp: 値は上記のtimestampです。</td>
  </tr>
  </tbody></table>
-  **認証ロジックの説明**
	CDNサーバーはクライアントからのリクエストを受けると、url内のtimestampパラメータ+認証URLの有効期限を解析して現在の時間と比較します。
	1. timestamp + 認証URLの有効期限が現在の時間より小さい場合、サーバーは期限切れによる失効と判定し、HTTP 403エラーが返されます。
	2. timestamp+認証URLの有効期限が現在の時間より大きい場合、MD5アルゴリズムを使用してmd5hashの値を計算し、さらに計算したmd5hash値とurlで渡したmd5hash値を比較し、一致する場合はそのままにし、一致しない場合はHTTP 403エラーを返します。

## 設定ガイド 

**Type-Cで認証する設定を例として、パラメータおよびコンソールを以下のように設定します。**

- **フィールド設定**
  - 認証キー：dimtm5evg50ijsx2hvuwyfoiu65
  - 認証URLの有効期間：1s   
  - 署名アルゴリズムがサーバー認証URLを発行した時間：2020年02月27日16:10:32（UTC+8）は、10進数の整数値1582791032(timestamp)に変換されます
  - オリジンサーバーアドレスのリクエスト：`http://cloud.tencent.com/test.jpg`
	
- 発行プロセス
  - 認証パラメータの取得
    <table>
    <thead>
    <tr>
    <th>パラメータ</th>
    <th>値</th>
    </tr>
    </thead>
    <tbody><tr>
    <td>uri</td>
    <td>リソースのアクセスパスは /test.jpgです</td>
    </tr>
    <tr>
    <td>timestamp</td>
    <td>1582791032</td>
    </tr>
    <tr>
    <td>pkey</td>
    <td>dimtm5evg50ijsx2hvuwyfoiu65</td>
    </tr>
    </tbody></table>
  - 署名文字列の結合：dimtm5evg50ijsx2hvuwyfoiu651582791032/test.jpg
  - 署名文字列のmd5値の計算：md5hash = md5sum(pkeytimestampuri) =md5sum(dimtm5evg50ijsx2hvuwyfoiu651582791032/test.jpg) = ea68b93ac23ebbc6eebf7f163c6e9c4c

-   **認証URLの発行：**
`http://cloud.tencent.com/ea68b93ac23ebbc6eebf7f163c6e9c4c/1582791032/test.jpg` 
クライアントがURLの暗号化によってアクセスする場合、CDNサーバーが計算したmd5hash値とアクセスリクエスト内にあるmd5hash値が同じであれば、いずれもea68b93ac23ebbc6eebf7f163c6e9c4cとなり、認証に合格し、そうでなければ認証に失敗します。

## 注意事項 

**キャッシュのヒット率** 
TypeC認証方式が有効になっているドメイン名は、URLへのアクセスパスに署名とタイムスタンプが保持されます。CDNノードでリソースをキャッシュする時、認証パスが自動的に無視され、ドメイン名キャッシュのヒット率には影響しません。

**back-to-originのポリシー**
TypeC認証方式が有効になっているドメイン名について、アクセスする際の形式は次のとおりです。
 `http://DomainName/md5hash/timestamp/FileName` 

認証にパスした後、ヒットしたCDNノードがない場合、ノードはback-to-originリクエストを送信します。**back-to-originリクエストは、パス中のmd5hashとtimestampパス**を削除します。オリジンサーバーは特別な処理を行う必要はありません。
