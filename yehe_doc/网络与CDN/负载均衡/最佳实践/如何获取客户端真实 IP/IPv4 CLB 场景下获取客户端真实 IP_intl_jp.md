## CLBでのクライアントリアルIPの取得に関する説明
CLBのレイヤー4（TCP/UDP/TCP SSL）およびレイヤー7（HTTP/HTTPS）サービスでは、どちらもバックエンドCVM上でクライアントのリアルIPを直接取得することができ、追加設定を行う必要はありません。
- レイヤー4 CLBでは、バックエンドCVM上で取得するソースIPがクライアントIPです。
- レイヤー7 CLBでは、`X-Forwarded-For`または`remote_addr`フィールドによってクライアントIPを直接取得することができます。レイヤー7 CLBのアクセスログについては、[アクセスログのCLSへの保存設定](https://intl.cloud.tencent.com/document/product/214/35063)をご参照ください。 

>?
>- レイヤー4 CLBでは、バックエンドCVM上で追加設定を行うことなくクライアントIPを取得できます。
>- SNATを行ったその他のレイヤー7ロードバランシングサービスでは、バックエンドCVM上での設定を行ってからX-Forwarded-Forメソッドを使用してクライアントのリアルIPを取得する必要があります。
>

次に、一般的なアプリケーションサーバー設定スキームについてご説明します。

## IIS 6設定スキーム
1. [F5XForwardedFor](https://devcentral.f5.com/s/articles/x-forwarded-for-log-filter-for-windows-servers)プラグインモジュールをダウンロードしてインストールし、ご自身のサーバーのOSバージョンに応じて`x86\Release`または`x64\Release`ディレクトリ下の`F5XForwardedFor.dll`をあるディレクトリにコピーします。ここでは仮に`C:\ISAPIFilters`とします。同時にIISプロセスのこのディレクトリに対する読み取り権限を確保します。
2. IISマネージャーを開き、現在開いているウェブサイトを見つけ、このウェブサイト上で右クリックして**プロパティ**を選択し、プロパティページを開きます。
3. プロパティページで**ISAPIフィルター**に切り替え、**追加**をクリックすると、追加ウィンドウがポップアップします。
4. 追加ウィンドウの「フィルター名」に「F5XForwardedFor」、「実行可能ファイル」に`F5XForwardedFor.dll`の完全なパスをそれぞれ入力し、**OK**をクリックします。
5. IISサーバーを再起動し、設定が有効になるのを待ちます。

## IIS 7設定スキーム
1. [F5XForwardedFor](https://devcentral.f5.com/s/articles/x-forwarded-for-log-filter-for-windows-servers)プラグインモジュールをダウンロードしてインストールし、ご自身のサーバーのOSバージョンに応じて`x86\Release`または`x64\Release`ディレクトリ下の`F5XFFHttpModule.dll`と`F5XFFHttpModule.ini`をあるディレクトリにコピーします。ここでは仮に`C:\x_forwarded_for`とし、IISプロセスのこのディレクトリに対する読み取り権限を確保します。
2. **IISサーバー**を選択し、**モジュール**機能をダブルクリックします。
![](https://main.qcloudimg.com/raw/21372379584488e72ae3d22af44a5017.png)
3. **ネイティブモジュールの設定**をクリックします。
![](https://main.qcloudimg.com/raw/280f11e95b7ac8cd4a754d98ad0cd2b7.png)
4. ポップアップボックスで、**登録**をクリックします。
![](https://main.qcloudimg.com/raw/1d6f7bd38077f2c9f089eb84a1995aa1.png)
5. 下図のように、ダウンロードしたDLLファイルを追加します。
![](https://main.qcloudimg.com/raw/354a35a203c24d802d59782c91dfe02a.png)
6. 追加が完了したら、チェックを入れて**OK**をクリックします。
![](https://main.qcloudimg.com/raw/9fffdfa02fba225f13090ef2598e1c0e.png)
7. 「ISAPIおよびCGIの制限」に上記の2つのDLLファイルを追加し、制限を許可に設定します。
![](https://main.qcloudimg.com/raw/8585122da39f14d734eb9d6ded7e486c.png)
8. IISサーバーを再起動し、設定が有効になるのを待ちます。

## Apache設定スキーム
1. Apacheのサードパーティモジュール「mod_rpaf」をインストールします。
```
wget http://stderr.net/apache/rpaf/download/mod_rpaf-0.6.tar.gz
tar zxvf mod_rpaf-0.6.tar.gz
cd mod_rpaf-0.6
/usr/bin/apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c
```
2. Apacheの設定`/etc/httpd/conf/httpd.conf`を変更し、末尾に次を追加します。
```
LoadModule rpaf_module modules/mod_rpaf-2.0.so
RPAFenable On
RPAFsethostname On
RPAFproxy_ips IPアドレス（このIPアドレスは最初はCLBが提供するパブリックIPではありません。具体的なIPについてはApacheログで確認できます。通常は2つあり、どちらも入力が必要です）
RPAFheader X-Forwarded-For
```
3. 追加が完了したら、Apacheを再起動します。
```
/usr/sbin/apachectl restart
```

## Nginx設定スキーム
1. Nginxをサーバーにする場合、クライアントのリアルIPを取得するにはhttp_realip_moduleを使用します。デフォルトでインストールされているNginxにはこのモジュールがインストールされていないため、Nginxを再コンパイルして`--with-http_realip_module`を追加する必要があります。
```
yum -y install gcc pcre pcre-devel zlib zlib-devel openssl openssl-devel
wget http://nginx.org/download/nginx-1.17.0.tar.gz
tar zxvf nginx-1.17.0.tar.gz
cd nginx-1.17.0
./configure --prefix=/path/server/nginx --with-http_stub_status_module --without-http-cache --with-http_ssl_module --with-http_realip_module
make
make install
```
2. nginx.confファイルを変更します。
```
vi /etc/nginx/nginx.conf
```
赤色の部分の設定フィールドと情報を変更します。
>?このうち`xx.xx.xx.xx`は実際のIPアドレスに変更する必要があります。このIPアドレスはCLBが提供するパブリックIPではありません。具体的なIPアドレスはNginxログで確認できます。複数のIPアドレスがある場合は、すべて入力が必要です。
<div class="code">
<p>
</p>
<pre>  
fastcgi connect_timeout 300;
fastcgi send_timeout 300;
fastcgi read_timeout 300;
fastcgi buffer_size 64k;
fastcgi buffers 4 64k;
fastcgi busy_buffers_size 128k;
fastcgi temp_file_write_size 128k;
<font color="#f2777a">
set_real_ip_from xx.xx.xx.xx;
real_ip_header X-Forwarded-For;
 </font>
</pre>
</div>
3. Nginxを再起動します。
```
service nginx restart
```
4. Nginxのアクセスログを確認し、クライアントのリアルIPを取得できます。
```
cat /path/server/nginx/logs/access.log
```
