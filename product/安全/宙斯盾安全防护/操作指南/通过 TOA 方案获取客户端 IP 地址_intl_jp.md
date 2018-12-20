サービス要求が高保護IPにより4層転送された後、サービスサーバ側がメッセージを受信してから、見られるソースIPアドレスは高保護IPのエクスポートIPアドレスです。サーバー側がクライアントの実際のIPアドレスを取得できるようにするには、次のTOAスキームを使用できます。サービスのLinuxサーバーで、対応するTOAカーネルパッケージをインストールし、サーバーを再起動します。そうすると、サービス側はクライアントの実際のIPアドレスを取得できます。

##TOA原則
高保護転送された後、データパケットは同時にSNATとDNATが行われ、データパケットのソースアドレスと宛先アドレスが変更されます。
TCPプロトコルでは、クライアントIPをサーバに送信するために、転送時にクライアントのIPとportがカスタムtcp optionフィールドに配置されます。
		
    #define TCPOPT_ADDR	200  
    #define TCPOLEN_ADDR 8	/* |opcode|size|ip+port| = 1 + 1 + 6 */

    /*
    *insert client ip in tcp option, now only support IPV4,
    *must be 4 bytes alignment.
    */
    struct ip_vs_tcpo_addr {
    __u8 opcode;
    __u8 opsize;
    __u16 port;
    __u32 addr;
    }; 
Linuxカーネルは、リスニングソケットがスリーウェイハンドシェイクのACKパケットを受信した後、`SYN_REVC`状態から`TCP_ESTABLISHED`状態に入ります。この時点で、カーネルは`tcp_v4_syn_recv_sock`関数を呼び出します。Hook関数`tcp_v4_syn_recv_sock_toa `は、まず、元の`tcp_v4_syn_recv_sock`関数を呼び出し、その後、`get_toa_data`関数を呼び出してTCP OPTIONからTOA OPTIONをを抽出し、`sk_user_data`フィールドに格納します。

そして、`inet_getname_toa hook inet_getname`を用いて、ソースIPアドレスとポートを取得するときは、最初に元の`inet_getname`を呼び出してから、`sk_user_data`が空であるかどうかを判断し、実際のIPとportを抽出するデータがある場合は、`inet_getname`の戻り値を置き換えます。

クライアントプログラムはユーザーモードでgetpeernameを呼び出し、返されたIPとportはクライアントの元のIPです。

##カーネルパッケージのインストール手順
###Centos 6.x/7.x
インストール手順

1. インストールパッケージをダウンロードします
 (1) [Centos 6.xのダウンロード](http://toakernel-1253438722.cossh.myqcloud.com/kernel-2.6.32-220.23.1.el6.toa.x86_64.rpm)
 (2) [Centos 7.xのダウンロード](http://toakernel-1253438722.cossh.myqcloud.com/kernel-3.10.0-693.el7.centos.toa.x86_64.rpm)
2. インストールパッケージファイル
							
			rpm -hiv kernel-2.6.32-220.23.1.el6.toa.x86_64.rpm --force						
3. インストールの完了後にホストを再起動します。

			reboot
4. toaモジュールが正常にロードされたかどうかを確認するようにコマンドを実行します。

			lsmod | grep toa
5. ロードされていない場合は手動で開始させる
    
			modprobe toa
6. toaモジュールの自動ロードを開始させるには、次のコマンドを使用できます。

			echo “modprobe toa” >> /etc/rc.d/rc.local
			
###  Ubuntu 16.04
インストールパッケージをダウンロード：
(1) [カーネルパッケージのダウンロード](http://toakernel-1253438722.cossh.myqcloud.com/linux-image-4.4.87.toa_1.0_amd64.deb )
(2) [カーネルヘッダパッケージのダウンロード](http://toakernel-1253438722.cossh.myqcloud.com/linux-headers-4.4.87.toa_1.0_amd64.deb)
インストール手順：

			dpkg -i linux-image-4.4.87.toa_1.0_amd64.deb
Headersパッケージはインストールする必要はありません。関連する開発を行う必要がある場合は、インストールしてください。
インストールが完了したらホストを再起動し、そして、`lsmod|grep toa`によりtoaモジュールがロードされているかどうかを確認します。ロードされていなければ、`modprobe toa`により開始させます。
Toaモジュールのロードを開始させるには、次のコマンドを使用できます。
		
		echo “modprobe toa” >> /etc/rc.d/rc.local
		 
### Debian 8

(1) [カーネルパッケージのダウンロード](http://toakernel-1253438722.cossh.myqcloud.com/linux-image-3.16.43.toa_1.0_amd64.deb)
(2) [カーネルヘッダパッケージのダウンロード](http://toakernel-1253438722.cossh.myqcloud.com/linux-headers-3.16.43.toa_1.0_amd64.deb)

インストール方法はUbuntuと同じです。


サービスサーバーのLinuxオペレーティングシステムの種類とバージョンに応じて、対応するカーネルパッケージをダウンロードし、以下の手順に従ってください。ユーザーのオペレーティングシステムに適合するカーネルパッケージがない場合、ユーザーは次のTOAソースコードのインストールガイドを参照して操作することもできます。

##TOAソースコードのインストールガイド

###ソースコードのインストール

1. [toaパッチ](http://kb.linuxvirtualserver.org/images/3/34/Linux-2.6.32-220.23.1.el6.x86_64.rs.src.tar.gz)を当てたソースパッケージをダウンロードし、toaパッチをクリックしてインストールパッケージをダウンロードします。
2. 解凍します。
3. .configを編集し、`CONFIG_IPV6=M`を`CONFIG_IPV6=y`に変更してください。
4. カスタム説明を追加する必要がある場合は、Makefileを編集できます。
5. make -jn (nはスレッド数)。
6. `make modules_install`。
7. `make install`。
8. /boot/grub/menu.lstを変更して、defaultを新しくインストールされたカーネルに変更します（title順は0から始まります）。
9. Rebootが再起動した後、toaカーネルとなります。
10. `lsmode | grep toa`はtoaモジュールがロードされているかどうかを確認します。ロードされていない場合、`modprobe toa`が有効になります。

###カーネルパッケージの作成

rpmパッケージは自分で作ることができ、当社から入手することもできます。

1. kernel-2.6.32-220.23.1.el6.src.rpmをインストールします 

			rpm -hiv kernel-2.6.32-220.23.1.el6.src.rpm
2. カーネルソースディレクトリを生成します

			rpmbuild -bp ~/rpmbuild/SPECS/kernel.spec
3. ソースディレクトリをコピーします

			cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/ cp -a linux-2.6.32-220.23.1.el6.x86_64/ linux-2.6.32-220.23.1.el6.x86_64_new   
4. コピーしたソースディレクトリでtoaパッチを当てます

			cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/linux-2.6.32-220.23.1.el6.x86_64_new/ 
			patch -p1 < /usr/local/src/linux-2.6.32-220.23.1.el6.x86_64.rs/toa-2.6.32-220.23.1.el6.patch
5. .configを編集してSOURCEディレクトリにコピーします

			sed -i 's/CONFIG_IPV6=m/CONFIG_IPV6=y/g' .config 
			echo -e '\n# toa\nCONFIG_TOA=m' >> .config
			cp .config ~/rpmbuild/SOURCES/config-x86_64-generic
6. 元のソースコードにおける.configを削除します

			cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/linux-2.6.32-220.23.1.el6.x86_64 
			rm -rf .config
7. 最終的なpatchを生成します
    
			cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/
			diff -uNr linux-2.6.32-220.23.1.el6.x86_64 linux-2.6.32-220.23.1.el6.x86_64_new/ >
			~/rpmbuild/SOURCES/toa.patch
8. kernel.specを編集します

    vim ~/rpmbuild/SPECS/kernel.spec
ApplyOptionPathの下に次の2行を追加します（buildidなどのカスタムカーネルパッケージ名も変更できます） 

			Patch999999: toa.patch
    ApplyOptionalPatch toa.patch
9. rpmパッケージを作成します

			rpmbuild -bb --with baseonly --without kabichk --with firmware --without debuginfo --target=x86_64 ~/rpmbuild/SPECS/kernel.spec
10. カーネルrpmパッケージをインストールします
		 rpm -hiv kernel-xxxx.rpm --force
	 
再起動し、toaモジュールをロードします





