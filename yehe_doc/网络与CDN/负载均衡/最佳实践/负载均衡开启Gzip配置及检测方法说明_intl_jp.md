**パブリックネットワークCLB、パブリックネットワーク固定IPタイプのCLB**インスタンスでは、**HTTP/HTTPSプロトコル**はユーザーによるGzip圧縮機能の有効化をデフォルトでサポートしています。Gzip機能を有効化すると、ウェブページを圧縮することでネットワーク伝送のデータ量を有効に縮小し、クライアントブラウザのアクセス速度を向上させることができます。ご使用中は次の事項に注意する必要があります。

### 注意事項
- **バックエンドCVMでもGzipのサポートを同時に有効にしておく必要があります**
一般的なNginxサービスコンテナでは、設定ファイル（デフォルトではnginx.conf）でGzipを有効化し、サービスを再起動する必要があります
```
gzip on;
```
- **現在CLBがサポートするファイルタイプは次のとおりです。Gzip_types設定項目でファイルタイプを指定して圧縮することができます**
```
application/atom+xml application/javascript application/json application/rss+xml application/vnd.ms-fontobject application/x-font-ttf application/x-web-app-manifest+json application/xhtml+xml application/xml font/opentype image/svg+xml image/x-icon text/css text/plain text/x-component;
```
>!CLBのバックエンドCVMの業務ソフトウェアでも、上記のファイルタイプのGzipサポートを同時に有効にしておく必要があります。
>
- **クライアントリクエストには圧縮リクエストであることを示す識別子を付ける必要があります**
圧縮を有効にするには、さらにクライアントリクエストの際に次の識別子を付ける必要があります。
```
Accept-Encoding: gzip,deflate,sdch
```

### バックエンドCVMでのGzip有効化フローの例
サンプルCVMの実行環境：Debian 6
1. vimを使用して、ユーザーパスを基にNginx設定ファイルを開きます。
```
vim /etc/nginx/nginx.conf
```
2. 次のコードを見つけます。
```
gzip on;
gzip_min_length 1k;
gzip_buffers 4 16k;
gzip_http_version 1.1;
gzip_comp_level 2;
gzip_types text/html application/json;
```
上記のコードの構文の説明は次のとおりです。

- Gzip：Gzipモジュールを有効化または無効化します。
構文：`gzip on/off`
スコープ：http、server、location	

- gzip_min_length：圧縮を許可するページの最小バイト数を設定します。ページのバイト数はheaderのContent-Lengthから取得できます。デフォルト値は1kです。
構文：`gzip_min_length length`
スコープ：http、server、location	

- gzip_buffers：システムがGzipの圧縮結果のデータストリームを保存するために何単位のキャッシュを取得するかを設定します。16kは16kを単位とすることを表し、16kを単位としてオリジナルデータサイズの4倍のメモリを申請します。
構文： `gzip_buffers number size`
スコープ：http、server、location	

- gzip_http_version ：Gzipの機能を使用できるHTTPの最も低いバージョンを表します。HTTP/1.0を設定した場合、それがGzipの機能を使用できるHTTPの最も低いバージョンとなるため、GzipはHTTP/1.1への前方互換性を有します。Tencent Cloudは全ネットワークでHTTP/1.1をサポートしているため、変更の必要はありません。
構文: `gzip_http_version 1.0 | 1.1;`
スコープ: http、server、location

- gzip_comp_level：Gzipの圧縮比であり、範囲は1～9です。1は圧縮比が最低で処理速度が最も速く、9は圧縮比が最高で処理が最も遅くなります（伝送速度は速くなりますがcpuを消費します）。
構文: `gzip_comp_level 1..9`
スコープ: http、server、location

- gzip_types：マッチするMIMEタイプの圧縮を行います。デフォルトでは"text/html"タイプの圧縮が行われます。また、NginxのGzipはデフォルトではjavascript、画像などの静的リソースファイルの圧縮を行いません。gzip_typesで圧縮するMIMEタイプを指定することができ、設定した値以外のものは圧縮されません。**例えばjson形式のデータを圧縮したい場合は、このステートメントにapplication/jsonタイプのデータを追加する必要があります**。

サポートするタイプは次のとおりです。
```
text/html text/plain text/css application/x-javascript text/javascript application/xml
```
構文: `gzip_types mime-type [mime-type ...]`
スコープ: http、server、location

3. 設定を変更する場合は、先にファイルを保存して終了し、Nginx binファイルディレクトリに進み、次のコマンドを実行してNginxをリロードします。
```
./nginx -s reload
```
4. curlコマンドを使用してGzipの有効化に成功したかどうかをテストします。
```
curl -I -H "Accept-Encoding: gzip, deflate" "http://cloud.tencent.com/example/"
```
