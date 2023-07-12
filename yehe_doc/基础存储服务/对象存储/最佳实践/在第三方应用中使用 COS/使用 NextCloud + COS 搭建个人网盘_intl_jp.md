## まえがき

NextCloudはオンラインストレージの作成に用いられるオープンソースクライアントおよびサーバーソフトウェアです。このソフトウェアを利用することで、誰でも個人のオンラインストレージサービスを構築することができます。

NextCloudのサーバーはPHPで作成し、基盤ストレージはデフォルトでサーバーのローカルディスクに保存されます。NextCloudの構成を変更することで、Tencent Cloud Object Storage（COS）を基盤ストレージとして使用することができ、COSのより安価なストレージコスト、より高い信頼性と障害復旧機能、ならびに無限のストレージスペースを利用することが可能になります。

ここではNextCloudのサーバーが依存する環境についてご説明するとともに、ローカルストレージとCOSの違いについて分析比較し、最後に個人オンラインストレージ構築の実践について解説します。

>! 既存のNextCloudサーバーインスタンスをローカルストレージからTencent Cloud COSの使用に切り替えると、既存のファイルが見えなくなる可能性があります。既存のインスタンスのストレージ方式を変更したい場合は、このチュートリアルに従って新しいNextCloudサーバーを構築し、Tencent Cloud COSを使用するよう設定した後、古いインスタンスのデータを新しいインスタンスに移行することをお勧めします。
>

## NextCloudサーバー環境の概要

NextCloudサーバーはPHPで作成し、データベースはSQLite、MySQL、MariaDB、PostgreSQLを使用できます。このうちSQLiteはパフォーマンス上の制限があるため、通常実際のユースケースで使用することはお勧めしません。PHP、MySQLおよび関連のサーバーソフトウェアにはすべてWindows版がありますが、NextCloudコミュニティからのフィードバックによると、WindowsでNextCloudサーバーを実行すると文字コードなどの問題が生じることがあるため、公式はWindowsでのNextCloudサーバーのデプロイをサポートしていないとアナウンスしています。

<span id=1></span>
### サーバーの設定

Tencent Cloud Virtual Machine（CVM）には現在複数のインスタンスファミリーがあり、各インスタンスファミリーはそれぞれ複数のサブタイプに分かれています。インスタンスファミリーごとに特化する点（例えば大容量メモリや高IOなど）が異なります。NextCloudの位置づけは個人、家庭、中小企業ユーザー向けであり、各ハードウェアリソースへの要件はどれも高くないため、各リソースのバランスの取れた標準型を選択することでニーズに対応できます。通常、最新のサブタイプはよりコストパフォーマンスが高いため、一般的には最新のサブタイプを選択するとよいでしょう。

インスタンスファミリーとサブタイプを決定した後、具体的なvCPUとメモリ仕様も選択する必要があります。vCPUとメモリ仕様ごとに、対応するプライベートネットワーク帯域幅とネットワーク送受信パケットが異なります。PHPはOPcacheによってパフォーマンスを向上させることができ、NextCloudサーバーもAPCuメモリキャッシュの使用によるパフォーマンス向上をサポートしています。このため、仕様を選択する際は容量が大きめのメモリを選択することをお勧めします。

CVMは購入後に構成の調整が可能なため、例えばvCPU1コアとメモリ4GBなどの比較的低構成の仕様をまず購入し、構築完了後に実際にオンラインで使用する際に、ユーザー数、ファイル数、CVMの関連モニタリングデータなどに基づいて、パフォーマンス向上のための仕様アップグレードが必要かどうかを判断することができます。例えばご家庭または中小企業などの複数ユーザーによる使用を想定している場合は、複数ユーザーでの使用に足る十分なパフォーマンスを提供するため、2コア8GBから4コア16GBの構成の購入をお勧めします。

### サーバーOS

主要なLinuxディストリビューションであれば、どれもNextCloudサーバーを問題なく実行できます。ソフトウェアパッケージインストールをする際に使用するコマンド（パッケージ管理ツール）がシステムによって異なる点を除き、設定作業に違いはありません。

>? ここではCentOS OS 7.7のCVMを例として説明します。
>

### データベース

上記で述べたとおり、実際のユースケースでは通常MySQLとPHPをセットで使用します。MariaDBはMySQLの「復刻」版であり、MySQLとの間で高度な互換性を有します。このためMySQL 5.7+またはMariaDB 10.2+はどちらも問題なくNextCloudサーバーと組み合わせて使用することができます。

Tencent CloudがホストするTencentDB for MySQLとTencentDB for MariaDBは、CVM上の自作データベースと異なり、デフォルトで1マスター1スレーブの高可用性モードを採用し、より高い信頼性を有するほか、自動バックアップなどの便利な運用保守操作をご提供します。このため、実際のユースケースではこちらのクラウドデータベースのご使用を強く推奨します。

>? ここではTencentDB for MySQL 5.7を例として説明します。
>

### WebサーバーとPHPランタイム

NextCloudサーバーは`.htaccess`によって一部の設定を指定するため、Apacheサーバーソフトウェアを使用する際、NextCloudサーバー自体の設定項目をそのまま使用することができます。Nginxは近年急成長中のWebサーバーソフトウェアであり、Apacheに比べてインストール設定が簡単、リソース占有が少ない、ロードバランシング機能がより強力であるなどのメリットがあります。NextCloudサーバー内の`.htaccess`設定をNginxの設定として移行しても、NextCloudサーバーの実行は問題なくサポートされます。ここではNginxサーバーソフトウェアを使用するとともに、完全なNginx設定の例を参考までに示します。

PHPランタイムは現在PHP 7にバージョンアップしています。保守されている主なバージョンは7.2、7.3、7.4であり、この3バージョンはすべてNextCloudサーバーをサポートしています。最新の7.4の使用をお勧めします。また、NextCloudはPHPの一部拡張モジュールにも依存しています。続いて拡張モジュール要件の詳細についてご説明します。

### Tencent Cloudネットワーク環境

Tencent Cloudでは現在、基幹ネットワークとVirtual Private Cloud（VPC）環境をご提供しています。基幹ネットワークとはTencent Cloud上のすべてのユーザーのための公共のネットワークリソースプールです。すべてのCVMのプライベートIPアドレスはTencent Cloudが一元的に割り当てており、ネットワークセグメントの区分、IPアドレスのカスタマイズは行えません。VPCとは、ユーザーがTencent Cloud上に構築した、論理的に隔離されているネットワークスペースです。VPC内では、ユーザーはネットワークセグメントの区分、IPアドレスおよびルーティングポリシーを自由に定義できます。現在基幹ネットワークは、リソース不足かつ機能の拡張ができないなどの理由により、新規登録アカウントおよび一部の新規アベイラビリティーゾーンでは今後サポートを行わないことになっています。このため、これ以降の説明はVPCを例として行います。

>? VPCに関するより詳しい説明については、[Virtual Private Cloud製品概要](https://intl.cloud.tencent.com/document/product/215/535)をご参照ください。
>

## CBSとCOSの比較

CVMでは、Cloud Block Storage（CBS）をCVM内のローカルディスクの形式でOSにマウントします。NextCloudはデフォルトでファイルシステムを使用してオンラインストレージのデータを保存するため、NextCloudのデータはそのままOS内のCBSに保存することができます。CBSと比較した、COSを使用する上でのメリットについて、次のいくつかの点から解説します。

### ユースケース

#### CBS

CBSはブロックストレージの一種であり、CVMのOSに直接マウントしてハードディスクとして使用することができます。通常はOSによって専有されるため、1台のCVMにしかマウントできませんが、読み取り書き込みパフォーマンスが高いため、高IO、低遅延かつ他のCVMとの共有が必要ないケースに適しています。

#### COS

COSはHTTPプロトコルによって外部に提供される読み取り書き込みインターフェースであり、プログラミング方式でCOSのストレージオブジェクト（ファイル）にアクセスする必要があります。COSはオブジェクトキー（Key、ファイルパスであると理解できます）をインデックスとして使用するもので、ストレージ容量の制限がありません。ネットワーク伝送を使用するため、速度と遅延は比較的大きくなりますが、操作がオブジェクトレベルのため、1つのソフトウェアで1つのオブジェクトの操作を行った後、別のソフトウェアですぐに同じオブジェクトの操作を行えることから、パフォーマンスに対する要件が厳しくなく、低コストで大容量のストレージが必要な場合、または共有アクセスが必要なケースに適しています。オンラインストレージの使用自体はネットワーク伝送を通じて行われるため、遅延に対する要件は厳しくなく、かつオンラインストレージクライアントからオンラインストレージサーバーを経由してCOSに至るリンクにおいて、速度と遅延に影響する要因は主にクライアントのネットワーク環境にあり、COS自体の速度制限ではないことから、COSの方がよりオンラインストレージとの併用に適していると言えます。



### メンテナンス

#### CBS

CBSは容量が固定であり、コンソールまたはTencent Cloud APIによるスケーリングが必要です。スケーリング後はOSでパーティションの拡張も行わなければならず、かつパーティションの拡張時にパーティションエラーが発生するリスクも一定程度あり、ある程度のメンテナンスコストがかかります。

#### COS

COSは必要に応じて使用でき、総容量の制限がなく、オブジェクト数（ファイル数）の制限もありません。完全メンテナンスフリーです。

### データセキュリティ

CBSとCOSはどちらもマルチレプリカなどの手段を使用してデータの信頼性を保証しています。

## NextCloudサーバー実行環境の構築

## NextCloudサーバーが依存するクラウド製品の準備

#### CVM
スタート操作については、[Cloud Virtual Machine（CVM）クイックスタート](https://intl.cloud.tencent.com/document/product/213/8036)をご参照ください。


#### TencentDB for MySQL

スタート操作については、[TencentDB for MySQLクイックスタート](https://intl.cloud.tencent.com/document/product/236/37785)をご参照ください。


#### COS

1. [COSコンソール](https://console.cloud.tencent.com/cos5)を開いてログインし（初回使用前にCOSサービスをアクティブ化する必要があります）、**バケットリスト**に進み、**バケットの作成**をクリックし、下表の説明に従って設定します。
<table>
	<tr><th>設定項目</th><th>値</th></tr>
	<tr><td>名前</td><td>カスタマイズしたバケット名（例：nextcloud）を入力します。この名前は決定すると変更できませんのでご注意ください</td></tr>
	<tr><td>所属リージョン</td><td>購入したCVMの所属リージョンと同じものにします</td></tr>
	<tr><td>その他</td><td>デフォルトを維持します</td></tr>
</table>
2. 上記の設定完了後、**OK**をクリックして作成を完了します。

### WebサーバーおよびPHPランタイムのインストールと設定

#### Nginxのインストール

1. SSHツールを使用して新規購入サーバーにログインします。
2. 次のコマンドを実行してNginxをインストールします。
```bash
yum install nginx
```
 次のメッセージが表示された場合は、`Y`を入力してエンターを押し、インストールを確認します（以下同様）。
```bash
Is this ok [y/d/N]:
```
3. 次のメッセージが表示された場合、インストールは完了しています。
```bash
Complete!
[root@VM-0-10-centos ~]#
```
4. 続いて次のコマンドを実行し、Nginxのバージョンが正常に表示されるかどうかを検証します。
```bash
nginx -v
```
 次のメッセージが表示された場合、インストールの完了が検証されました。
```bash
nginx version: nginx/1.16.1
```

#### PHPのインストール

1. SSHツールを使用して新規購入サーバーにログインします。
2. 次のコマンドを実行し、PHP 7.4のインストールを開始します。
```bash
yum install epel-release yum-utils
```
3. 次のコマンドを順に実行します。
**コマンド1：**
```bash
yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```
>? 上記のコマンドの実行時に、速度が遅すぎる、長時間進捗しないなどの問題があった場合は、`Ctrl-C`でキャンセルし、再度このコマンドを実行することができます（以下同様）。
>
**コマンド2：**
```bash
yum-config-manager --enable remi-php74
```
 **コマンド3：**
```bash
yum install php php-fpm
```
4. インストールの完了後に次のコマンドを実行し、PHPのバージョンが正常に表示されるかどうかを検証します。
```bash
php -v
```
 次のメッセージが表示された場合、インストールの完了が検証されました。
```bash
PHP 7.4.8 (cli) (built: Jul 9 2020 08:57:23) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
```

#### PHPモジュールのインストール

基本のPHP以外に、NextCloudは他のPHPモジュールにも依存して一部の機能を実装しています。NextCloudの依存するモジュールについての詳細情報は、[NextCloud公式ドキュメント](https://docs.nextcloud.com/server/19/admin_manual/installation/source_installation.html#prerequisites-for-manual-installation)をご参照ください。

このチュートリアルではNextCloudに必須のPHPモジュールをインストールします。その後、NextCloudのその他のオプション機能を使用するご予定がある場合は、ご注意の上、依存する他のPHPモジュールをご自身でインストールしてください。

1. SSHツールを使用して新規購入サーバーにログインします。
2. 次のコマンドを実行し、PHPモジュールをインストールします。
```bash
yum install php-xml php-gd php-mbstring php-mysqlnd php-intl php-zip
```
3. インストールの完了後、次のコマンドを実行して、インストール済みのPHPモジュールを表示します。
```bash
php -m
```
4. 他のモジュールもインストールする必要がある場合は、`yum install <php-module-name>`を繰り返し実行します。

#### NextCloudサーバーコードのアップロードと解凍

1. [NextCloud公式サイト](https://nextcloud.com/install/#instructions-server)からNextCloudサーバーの最新版のインストールパッケージをダウンロードし、サーバーの`/var/www/`ディレクトリ下にアップロードします。アップロードは以下の方法で行うことができます。
 1. `wget`コマンドを使用して、インストールパッケージのダウンロードとサーバーへのアップロードを直接行います。例えば`/var/www/`ディレクトリに進んだ後、コマンド`wget https://download.nextcloud.com/server/releases/nextcloud-19.0.1.zip`を実行します。
 2. ローカルコンピュータにダウンロードした後、SFTPまたはSCPなどのソフトウェアによって、インストールパッケージを`/var/www/`ディレクトリにアップロードします。
 3. ローカルコンピュータにダウンロードした後、lrzszを使用してアップロードします。方法は次のとおりです。
    1. SSHツールを使用して新規購入サーバーにログインします。
    2. `yum install lrzsz`を実行してlrzszをインストールします。
    3. `cd /var/www/`を実行して目的のディレクトリに進みます。
    4. `rz -bye`を実行し、続いてSSHツールから、ローカルにダウンロードするNextCloudサーバーインストールパッケージを選択します（この操作はSSHツールによって多少異なります）。
2. SSHツールを使用して新規購入サーバーにログインします。
3. `unzip nextcloud-<version>.zip`を実行してインストールパッケージを解凍します。例えば`unzip nextcloud-19.0.1.zip`などとします。

#### PHPの設定

1. SSHツールを使用して新規購入サーバーにログインします。
2. `vim /etc/php-fpm.d/www.conf`を実行してPHP-FPMの設定ファイルを開き、設定項目を順に変更します（vimの具体的な使用方法については関連資料をご参照ください。この設定ファイルの変更は他の方法でも行うことができます）。
 1. `user = apache`を`user = nginx`に変更します。
 2. `group = apache`を`group = nginx`に変更します。
3. 変更完了後、`:wq`を入力してファイルを保存して終了します（vimの詳細な操作ガイドについては関連ドキュメントをご参照ください）。
4. 次のコマンドを実行してディレクトリ所有者を変更し、PHPをNginxで使用できるようにします。
```bash
chown -R nginx:nginx /var/lib/php
```
5. 次のコマンドを順に実行し、PHP-FPMサービスを起動します。
**コマンド1：**
```bash
systemctl enable php-fpm   # コマンド1
```
 **コマンド2：**
```bash
systemctl start php-fpm   # コマンド2
```

#### Nginxの設定

1. SSHツールを使用して新規購入サーバーにログインします。
2. 次のコマンドを実行し、ウェブサイトのディレクトリ所有者を変更します。
```bash
chown -R nginx:nginx /var/www
```
3. 現在のNginx設定ファイル`/etc/nginx/nginx.conf`をバックアップします。次の方法で行うことができます。
 1. `cp /etc/nginx/nginx.conf ~/nginx.conf.bak`を実行し、現在の設定ファイルをホーム（HOME）ディレクトリにバックアップします。
 2. SFTPまたはSCPなどのソフトウェアを使用して、現在の設定ファイルをローカルコンピュータにダウンロードします。
4. `/etc/nginx/nginx.conf`を変更するか、または次の内容に置き換えます。


```plaintext
# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

# Load dynamic modules. See /usr/share/doc/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        root         /var/www/nextcloud;

        add_header Referrer-Policy "no-referrer" always;
        add_header X-Content-Type-Options "nosniff" always;
        add_header X-Download-Options "noopen" always;
        add_header X-Frame-Options "SAMEORIGIN" always;
        add_header X-Permitted-Cross-Domain-Policies "none" always;
        add_header X-Robots-Tag "none" always;
        add_header X-XSS-Protection "1; mode=block" always;

        client_max_body_size 512M;
        fastcgi_buffers 64 4K;

        gzip on;
        gzip_vary on;
        gzip_comp_level 4;
        gzip_min_length 256;
        gzip_proxied expired no-cache no-store private no_last_modified no_etag auth;
        gzip_types application/atom+xml application/javascript application/json application/ld+json application/manifest+json application/rss+xml application/vnd.geo+json application/vnd.ms-fontobject application/x-font-ttf application/x-web-app-manifest+json application/xhtml+xml application/xml font/opentype image/bmp image/svg+xml image/x-icon text/cache-manifest text/css text/plain text/vcard text/vnd.rim.location.xloc text/vtt text/x-component text/x-cross-domain-policy;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
            try_files $uri $uri/ =404;
            index index.php;
        }

        location ~ ^\/(?:build|tests|config|lib|3rdparty|templates|data)\/ {
            deny all;
        }
        location ~ ^\/(?:\.|autotest|occ|issue|indie|db_|console) {
            deny all;
        }

        location ~ ^\/(?:index|remote|public|cron|core\/ajax\/update|status|ocs\/v[12]|updater\/.+|oc[ms]-provider\/.+)\.php(?:$|\/) {
            fastcgi_split_path_info ^(.+?\.php)(\/.*|)$;
            set $path_info $fastcgi_path_info;
            try_files $fastcgi_script_name =404;
            include        fastcgi_params;
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
            fastcgi_param PATH_INFO $path_info;
            fastcgi_param modHeadersAvailable true;
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_intercept_errors on;
            fastcgi_request_buffering off;
        }

        location ~ ^\/(?:updater|oc[ms]-provider)(?:$|\/) {
            try_files $uri/ =404;
            index index.php;
        }

        location ~ \.(css|js|svg|gif)$ {
            add_header Cache-Control "max-age=15778463";
        }

        location ~ \.woff2?$ {
            add_header Cache-Control "max-age=604800";
        }
    }

# Settings for a TLS enabled server.
#
#    server {
#        listen       443 ssl http2 default_server;
#        listen       [::]:443 ssl http2 default_server;
#        server_name  _;
#        root         /usr/share/nginx/html;
#
#        ssl_certificate "/etc/pki/nginx/server.crt";
#        ssl_certificate_key "/etc/pki/nginx/private/server.key";
#        ssl_session_cache shared:SSL:1m;
#        ssl_session_timeout  10m;
#        ssl_ciphers HIGH:!aNULL:!MD5;
#        ssl_prefer_server_ciphers on;
#
#        # Load configuration files for the default server block.
#        include /etc/nginx/default.d/*.conf;
#
#        location / {
#        }
#
#        error_page 404 /404.html;
#            location = /40x.html {
#        }
#
#        error_page 500 502 503 504 /50x.html;
#            location = /50x.html {
#        }
#    }

}
```


5. 次のコマンドを順に実行し、Nginxサービスを起動します。
**コマンド1：**

```bash
systemctl enable nginx
```

 **コマンド2：**

```bash
systemctl start nginx
```

## NextCloudサーバーでのCOS使用設定

### COS関連情報の取得

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 作成済みのバケットを見つけ、バケット名をクリックします。
![](https://main.qcloudimg.com/raw/13e02915f8c2846d7dfa5f2fec0c355b.png)
3. 左側ナビゲーションバーで**概要**タブを選択し、**基本情報**の**バケット名**と**所属リージョン**の中の英語部分をメモします。
![](https://main.qcloudimg.com/raw/2aef2ba23a6a32305ad39b4ef10a970c.png)

### APIキーの取得

サブアカウントキーを使用し、[最小権限ガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従うことで、使用上のリスクを低減させることをお勧めします。サブアカウントキーの取得については、[サブアカウントのアクセスキー管理](https://intl.cloud.tencent.com/document/product/598/32675)をご参照ください。



### NextCloudサーバー設定ファイルの変更

1. テキスト編集ツールを使用して`config.php`を作成し、次の内容を入力して、メモの内容に基づいて関連の値を変更します。

```php
<?php
$CONFIG = array(
  'objectstore' => array(
    'class' => '\\OC\\Files\\ObjectStore\\S3',
    'arguments' => array(
      'bucket' => 'nextcloud-1250000000', // バケット名（スペース名）
      'autocreate' => false,
      'key'  => 'AKIDxxxxxxxx', // ユーザーのSecretIdに置き換えます
      'secret' => 'xxxxxxxxxxxx', // ユーザーのSecretKeyに置き換えます
      'hostname' => 'cos.<Region>.myqcloud.com', // <Region>を所属リージョンに変更します（ap-shanghaiなど）
      'use_ssl' => true,
    ),
  ),
);
```

 下図に示すように：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/yJvR645_b14a23e2cac3ac988745fcd82fe56e18.png)
2. このファイルを保存し、`/var/www/nextcloud/config/`ディレクトリ下にアップロードします（ファイル名は`config.php`のままにしておきます）。SFTPまたはSCPソフトウェアでファイルをアップロードするか、または`rz -bye`コマンドによってアップロードすることができます。
3. 次のコマンドを実行し、設定ファイルの所有者を変更します。

```bash
chown nginx:nginx /var/www/nextcloud/config/config.php
```

## ドメイン名の設定

ご自身のNextCloudサーバーにアクセスするのに、IPアドレスではなくご自身のドメイン名の使用を予定している場合は、各ドメイン名登録プロバイダの説明ドキュメントをご参照の上、新しいドメイン名を登録してCVMのIPアドレスに解決し、ICP登録を完了してください。

NextCloudサーバーはインストールの過程で、インストール時に使用したドメイン名またはIPアドレスを記録するため、インストールの開始前にドメイン名の登録、解決、ICP登録を完了しておくとともに、ドメイン名を使用してNextCloudサーバーのセキュリティ画面にアクセスすることをお勧めします。

NextCloudサーバーの完成後にドメイン名またはIPアドレスを変更したい場合は、ご自身で`/var/www/nextcloud/config/config.php`設定ファイル内の`trusted_domains`を変更することができます。詳細については、[NextCloud公式ドキュメント](https://docs.nextcloud.com/server/19/admin_manual/installation/installation_wizard.html#trusted-domains)をご参照ください。

## NextCloudサーバーのインストール

1. ブラウザを使用してNextCloudサーバーにアクセスし、管理者ユーザー名とパスワードを作成して忘れないように記憶しておきます。
2. **ストレージとデータベース**を開き、下表の説明に従って設定します。

<table>
	<tr><th>設定項目</th><th>値</th></tr>
	<tr><td>データディレクトリ</td><td>/var/www/nextcloud/data（デフォルトを維持）</td></tr>
	<tr><td>データベース設定</td><td>MySQL/MariaDB</td></tr>
	<tr><td>データベースユーザー</td><td>root</td></tr>
	<tr><td>データベースパスワード</td><td>TencentDB for MySQLを初期化した際に入力したrootパスワード</td></tr>
	<tr><td>データベース名</td><td>nextcloud（またはその他の使用されていないデータベース名）</td></tr>
	<tr><td>データベースホスト（デフォルトではlocalhostと表示）</td><td>TencentDB for MySQLのプライベートネットワークアドレス</td></tr>
</table>
3. **インストール完了**をクリックし、NextCloudサーバーのインストールが完了するまで待ちます。
4. インストール中に504 Gateway Timeoutなどのエラーメッセージが表示された場合は、そのまま更新してリトライします。
5. インストール完了後、管理者アカウントを使用してNextCloudサーバーにログインすると、Web版NextCloudの使用を開始できます。

## NextCloudサーバーのチューニング

### バックエンドタスク

NextCloudサーバーは、ユーザーとのインタラクションが必要ないときに、一部のバックエンドタスク（例えばデータベースのクリーンアップ操作など）を実行しなければならない場合があります。PHPには、PHPベースのプログラムが内部で独立した作業プロセスまたはスレッドを維持できないように制限する実行特性があるため、 バックエンドタスクのようなケースでは、対応するPHPプログラムを外部から能動的に呼び出して実行する必要があります。

NextCloudサーバーは3種類のバックエンドタスクの呼び出しメソッドを提供しています。デフォルトは、ウェブページ側のログインユーザーに、ブラウザからAJAXリクエストを自動送信してサーバーのバックエンドタスクを実行するようリマインドする方法です。このメソッドはユーザーのログイン状態に強く依存し、ユーザーがログインしていないとこれらのバックエンドタスクが実行できないため、信頼性が最も低くなっています。

AJAXをベースにしたバックエンドタスクの低信頼性の問題を回避するためには、Linuxのcronを使用してバックエンドタスクを設定する方法を推奨します。Linuxのcronはタスクがリマインドされる時間を正確に制御でき、例えば5分ごと（分数は5の整数倍）や毎時10分などとすることができます。定義できる時間粒度には分、時間、1か月のうちの特定の日、月、特定の曜日などがあり、一部のOSでは秒と年もサポートされているため、高い柔軟性を有します。cronと関連説明および設定については、関連の資料をご参照ください。

cronを設定してNextCloudサーバーのバックエンドタスクを行えるようにする方法について、以下でご説明します。

1. SSHツールを使用して新規購入サーバーにログインします。
2. 次のコマンドを実行し、PHPモジュールをインストールします。

```bash
yum install php-posix
```
3. 次のコマンドを実行し、Nginxアカウントで使用するcronの設定を開くか、または作成します。
```bash
crontab -u nginx -e
```
4. 続いての編集画面はvi/vimです。`i`キーを押して編集モードに入り、次の内容の1行を挿入します。

```plaintext
*/5 * * * * php -f /var/www/nextcloud/cron.php
```

その後、`ESC`を押して編集モードを終了し、`:wq`を入力して保存し、終了します（vi/vimの詳細な操作ガイドについては関連ドキュメントをご参照ください）。
上記の設定ではNextCloud公式が推奨する5分に1回の実行を使用しています（分数は5の整数倍）。5分後にバックエンドタスクの実行が完了すると、ブラウザを開いてNextCloudサーバーにログインできるようになります。右上隅にあるユーザー名のイニシャルのアイコンをクリックし、**設定**に進み、左側メニューから**基本設定**に進むと、**バックエンドタスク**のところにデフォルトでCronが選択されていることを確認できます。


### メモリキャッシュ

PHPはOPcacheによってパフォーマンスを向上させることができ、NextCloudサーバーもAPCuメモリキャッシュの使用によるパフォーマンス向上をサポートしています。関連の操作フローを以下でご説明します。

1. SSHツールを使用して新規購入サーバーにログインします。
2. 次のコマンドを実行し、PHPモジュールをインストールします。
```bash
yum install php-pecl-apcu
```
3. 次のコマンドを順に実行し、Nginx とPHP-FPMを再起動します。
**コマンド1：**

```bash
systemctl restart nginx
```

 **コマンド2：**
```bash
systemctl restart php-fpm
```
4. `vim /var/www/nextcloud/config/config.php`を実行し、NextCloudサーバーの設定ファイルを開き、`$CONFIG = array (` の中に`'memcache.local' => '\OC\Memcache\APCu',`という1行を追加します。その後ファイルを保存して終了します。
![](https://main.qcloudimg.com/raw/eaa28e013991aad579cf6abc2a34d9bb.png)
5. cronを設定してバックエンドタスクを最適化した場合は、PHPのapc設定も変更する必要があります。`vim /etc/php.d/40-apcu.ini`を実行し、PHP APCuの設定ファイルを開き、`;apc.enable_cli=0`を`apc.enable_cli=1`に変更し（同時に前のセミコロンを削除する必要があることにご注意ください）、保存して終了します。パス`/etc/php.d/40-apcu.ini`が存在しない場合は、apcまたはapcuの文字がある`.ini`設定ファイルをご自身で`/etc/php.d/`ディレクトリから見つけて編集してください。
![](https://main.qcloudimg.com/raw/1c57fe0a2078aa0ca5dd7ba07b23fe86.png)

## クライアントアクセス設定

NextCloud公式はデスクトップ同期クライアントとモバイルクライアントを提供しており、NextCloud公式サイトまたは各大手アプリストアからダウンロードできます。NextCloudを設定する際には、NextCloudのサーバーアドレス（ドメイン名またはIP）を入力し、その後ご自身のユーザー名とパスワードを入力してログインすると、クライアントの使用を開始できます。






