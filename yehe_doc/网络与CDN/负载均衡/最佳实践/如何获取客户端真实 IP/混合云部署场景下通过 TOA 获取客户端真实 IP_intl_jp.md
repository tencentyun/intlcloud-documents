ここではハイブリッドクラウドのデプロイシーンおよびNAT64 CLBのシーンでのCLBのレイヤー4（TCPのみ）サービスにおいて、TOAによってクライアントのリアルソースIPを取得する方法についてご説明します。
<dx-steps>
-[TOAモジュールのロード](#load-toa)
-[バックエンドサービスの適用](#adapt-rs)
-[（オプション）TOAモジュールのステータス監視](#monitor-toa)
</dx-steps>

>?TOAによってクライアントのリアルソースIPを取得できるのはレイヤー4のTCPのみです。UDPおよびレイヤー7（HTTP/HTTPS）では取得できません。
>
## ユースケース
### ハイブリッドクラウドのデプロイシーン
[ハイブリッドクラウドのデプロイ](https://intl.cloud.tencent.com/document/product/214/38442)において、IDCのIPとクラウド上のVPCのIPの間でアドレスの重複が起こることがあります。このためSNAT IPを設定し、SNATを行ってソースIPの変換を行う必要があります。サーバーではリアルソースIPを取得できないため、TOAによって取得する必要があります。

### NAT64 CLBのシーン
NAT64 CLBの場合、クライアントのリアルなIPv6ソースIPはIPv4のパブリックIPに変換されるため、リアルサーバーのサービス側からはクライアントのリアルIPv6 IPを取得することができません。
Tencent Cloud NAT64 CLBはクライアントのリアルIPを取得する機能を備えています。クライアントのリアルソースIPをTCPプロトコルのカスタムoptionに含めることで、リアルソースIPが埋め込まれたTCPデータパケットがサーバーに送信された際、サーバーが挿入したTOAカーネルモジュールによってTCPデータパケット内のクライアントリアルソースIPを取得することができます。このとき、クライアントのアプリケーションは、TOAカーネルモジュールが提供するインターフェースを呼び出すだけでクライアントリアルソースIPを取得できます。


## 制限事項
<dx-accordion>
::: リソース上の制限
- TOAカーネルモジュールのコンパイル環境のカーネルバージョンはサービス環境のカーネルバージョンと一致している必要があります。
- コンテナ環境では、TOAカーネルモジュールはホストにロードする必要があります。
- TOAカーネルモジュールをロードする環境にはroot権限が必要です。
:::
::: 互換性の制限
 - UDPリスナーではTOAによるソースIPの取得はサポートされていません。
 - クライアントとリアルサーバーの間にあるデバイスの中に、TOAに関連する操作を行ったことがあるデバイスがある場合は、競合が起きる可能性があるため、サーバーによるリアルIP取得の有効性を保証することはできません。
 -  TOAを挿入後、有効となるのは挿入後に新たに確立した接続のみであり、既存の接続に対しては無効です。
 - TOAモジュールはTCP option内のアドレスからの抽出などの処理を多く行う必要があるため、TOAモジュールによってサーバーの一部のパフォーマンスが低下することがあります。
 - Tencent CloudのTOAモジュールは、ユーザーがカスタマイズした他のカーネルモジュールとの互換性が保証されません。また、他のメーカーまたはオープンソースのTOAモジュールとの互換性も保証されません。
 - Tencentが自社開発したTencentOS埋め込みTOAモジュールはハイブリッドクラウドのデプロイシーンでのリアルソースIP取得をサポートしているため、サーバーのシステムがTencentOSであり、かつハイブリッドクラウドにデプロイされている場合は、`modprobe toa`コマンドを直接実行してロードおよび使用する方法を試すことができます。TencentOSとその他のLinuxディストリビューションシステムのTOAは別のものであり、同時に使用できないことに注意が必要です。
:::
</dx-accordion>



## [TOAモジュールのロード](id:load-toa)
1. Tencent Cloud上のLinuxのバージョンに応じて、対応するTOA パッケージを解凍します。
<dx-accordion>
::: centos
[CentOS 8.0 64](https://clb-toa-1255852779.file.myqcloud.com/CentOS%208.0.1905.zip)
[CentOS 7.6 64](https://clb-toa-1255852779.file.myqcloud.com/CentOS%207.6.1810.zip)
[CentOS 7.2 64](https://clb-toa-1255852779.file.myqcloud.com/CentOS%207.2.1511.zip)

:::
::: debian
[Debian 9.0 64](https://clb-toa-1255852779.file.myqcloud.com/Debian%209.zip)
:::
::: suse linux
[SUSE 12 64](https://clb-toa-1255852779.file.myqcloud.com/SUSE%2012.zip)
[SUSE 11 64](https://clb-toa-1255852779.file.myqcloud.com/SUSE%2011.zip)
:::
::: ubuntu
[Ubuntu 18.04.4 LTS 64](https://clb-toa-1255852779.file.myqcloud.com/Ubuntu%2018.04.4%20LTS.zip)
[Ubuntu 16.04.7 LTS 64](https://clb-toa-1255852779.file.myqcloud.com/Ubuntu%2016.04.7%20LTS.zip)
:::
</dx-accordion>

2. [](id:step2)解凍完了後、cdコマンドを実行して解凍されたフォルダに進み、次のコマンドを実行してモジュールをロードします。
```
insmod toa.ko
```
3. 次のコマンドを実行し、TOAモジュールのロードに成功したかどうかを確認します。「toa load success」と表示されれば、ロードは成功です。
```
dmesg -T | grep TOA
```
4. ロードに成功後、起動スクリプト内に`toa.ko`ファイルをロードします（マシンを再起動した場合はkoファイルの再ロードが必要です）。
5. （オプション）それ以降TOAモジュールを使用する必要がない場合は、次のコマンドを実行してアンインストールします。
```
rmmod toa
```
6. （オプション）次のコマンドを実行し、TOAモジュールのアンインストールに成功したかどうかを確認します。「TOA unloaded」と表示されれば、アンインストールは成功です。
```
dmesg -T
```

上記のダウンロードファイルに、ご自身のOSバージョンに対応するインストールパッケージがない場合は、Linux汎用版のソースコードパッケージをダウンロードし、コンパイル後に対応するkoを取得することができます。このバージョンはCentos8、Centos7、Ubuntu18.04、Ubuntu16.04などの数多くの代表的なLinuxディストリビューションをサポートしています。
>? Linuxのカーネルバージョンは数多くあり、LinuxディストリビューションのOS市場も巨大でバージョンも多岐にわたるため、カーネルモジュールの互換性の問題を考慮し、ご利用のシステム上でTOAソースコードパッケージのコンパイルを行ってから使用することをお勧めします。
>
1. ソースコードパッケージのダウンロード
>!LinuxとTencentのTLinuxのTOAモジュールは併用できません。システムに応じて対応するTOAモジュールソースコードパッケージを選択してください。
>
  - Linux
```
wget "https://clb-toa-1255852779.file.myqcloud.com/tgw_toa_linux_ver.tar.gz"
```
  - Tencent TLinux
```
wget "https://clb-toa-1255852779.file.myqcloud.com/tgw_toa_tlinux_ver.tar.gz"
```
2. TOAカーネルモジュールのLinux環境のコンパイルの前に、GCCコンパイラ、Makeツールおよびカーネルモジュール開発パッケージをインストールする必要があります。
<dx-accordion>
::: CentOS環境下でのインストール操作

```
yum install gcc
yum install make
//カーネルモジュール開発パッケージをインストールします。開発パッケージのヘッダーファイルとライブラリのバージョンがカーネルバージョンと一致している必要があります
yum install kernel-devel-`uname -r`
```
:::
::: Ubuntu、Debian環境下でのインストール操作

```
apt-get install gcc
apt-get install make
//カーネルモジュール開発パッケージをインストールします。開発パッケージのヘッダーファイルとライブラリのバージョンがカーネルバージョンと一致している必要があります
apt-get install linux-headers-`uname -r`
```
:::
::: SUSE環境下でのインストール操作
```
zypper install gcc
zypper install make
//カーネルモジュール開発パッケージをインストールします。開発パッケージのヘッダーファイルとライブラリのバージョンがカーネルバージョンと一致している必要があります
zypper install kernel-default-devel
```
:::
</dx-accordion>

3. ソースコードをコンパイルしてtoa.koファイルを生成します。コンパイル中に`warning`および`error`が表示されなければ、コンパイルは成功です。Linuxシステムに対応するソースコードパッケージの例を挙げます。
```
tar zxvf tgw_toa_linux_ver.tar.gz
cd tgw_toa_linux_ver//解凍後のtgw_toaディレクトリに進みます
make
```
4. toa.koのコンパイルに成功後、上記の[ステップ2](#step2)のTOAモジュールロード操作を実行します。


## [バックエンドサービスの適用](id:adapt-rs)
<dx-accordion>
::: ハイブリッドクラウドのデプロイシーン
ハイブリッドクラウドのデプロイシーンでバックエンドサービスを適用する場合、コードの変更は必要なく、Linuxネットワークプログラミングの標準インターフェースを呼び出すだけでアクセスユーザーのリアルソースIPを取得できます。Cコードの例は次のとおりです。
```
struct sockaddr v4addr;  
len = sizeof(struct sockaddr);  
//get_peer_nameはLinuxネットワークプログラミングの標準インターフェースです。
if (get_peer_name(client_fd, &v4addr, &len) == 0) {  
	inet_ntop(AF_INET, &(((struct sockaddr_in *)&v4addr)->sin_addr), from, sizeof(from));  
	printf("real client v4 [%s]:%d\n", from, ntohs(((struct sockaddr_in *)&v4addr)->sin_port));   
}
```
:::
::: NAT64 CLBのシーン
NAT64 CLBのシーンでは、TOAのソースアドレスパススルー機能を使用し、バックエンドサーバーに`toa.ko`カーネルモジュールを挿入した後、アプリケーションのソースコードを変更してリアルソースIP取得機能を適用させる必要があります。
1.初めに、アドレスの保存に用いるデータ構造を定義します。
```
struct toa_nat64_peer {  
	struct in6_addr saddr;  
	uint16_t sport;  
};  
....  
struct toa_nat64_peer client_addr;  
....  
```
2. 次にメッセージを定義し、関数を呼び出してリアルIPv6ソースアドレスを取得します。
```
enum {  
	TOA_BASE_CTL            = 4096,  
	TOA_SO_SET_MAX          = TOA_BASE_CTL,  
	TOA_SO_GET_LOOKUP       = TOA_BASE_CTL,  
	TOA_SO_GET_MAX          = TOA_SO_GET_LOOKUP,  
};  
getsockopt(client_fd, IPPROTO_IP, TOA_SO_GET_LOOKUP, &client_addr, &len);  
```
3. 最後にアドレスを取得します。
```
real_ipv6_saddr = client_addr.saddr;  
real_ipv6_sport = client_addr.sport;
```

完全な例は以下のとおりです。
```
//リアルIP取得用関数の呼び出しメッセージを定義する必要があります。値は4096とします。
enum {  
	TOA_BASE_CTL            = 4096,  
	TOA_SO_SET_MAX          = TOA_BASE_CTL,  
	TOA_SO_GET_LOOKUP       = TOA_BASE_CTL,  
	TOA_SO_GET_MAX          = TOA_SO_GET_LOOKUP,  
};  
//アドレスの保存に用いるデータ構造を定義する必要があります。
struct toa_nat64_peer {  
	struct in6_addr saddr;  
	uint16_t sport;  
};  
//アドレスの保存に用いる変数を宣言します。カスタムタイプのアドレス保存用のデータ構造です。  
struct toa_nat64_peer client_addr;  
.……  
//クライアントのファイルディスクリプタを取得します。このうちlistenfdはサーバーのリスニングファイルディスクリプタです。  
client_fd = accept(listenfd, (struct sockaddr*)&caddr, &length);  
//関数を呼び出して、対応するNAT64シーンのユーザーのリアルソースIPを取得します。  
char from[40];  
int len = sizeof(struct toa_nat64_peer);  
if (getsockopt(client_fd, IPPROTO_IP, TOA_SO_GET_LOOKUP, &client_addr, &len) == 0) {  
	inet_ntop(AF_INET6, &client_addr.saddr, from, sizeof(from));  
	//ソースIPとソースportの情報を取得します  
	printf("real client [%s]:%d\n", from, ntohs(client_addr.sport));  
}  
```
:::
::: ハイブリッドクラウドのデプロイとNAT64 CLBの併用シーン
ハイブリッドクラウドのデプロイとNAT64 CLBの併用シーンでは、TOAのソースアドレスパススルー機能を使用し、バックエンドサーバーに`toa.ko`カーネルモジュールを挿入した後、アプリケーションのソースコードを変更してリアルソースIP取得機能を適用させる必要があります。

完全な例は以下のとおりです。
```
//リアルIP取得用関数の呼び出しメッセージを定義する必要があります。値は4096とします。  
enum {  
	TOA_BASE_CTL = 4096,  
	TOA_SO_SET_MAX = TOA_BASE_CTL,  
	TOA_SO_GET_LOOKUP = TOA_BASE_CTL,  
	TOA_SO_GET_MAX = TOA_SO_GET_LOOKUP,   
};  

//アドレスの保存に用いるデータ構造を定義する必要があります。    
struct toa_nat64_peer {    
	struct in6_addr saddr;    
	uint16_t sport;    
};    

//アドレスの保存に用いる変数を宣言します。カスタムタイプのアドレス保存用のデータ構造です。    
struct toa_nat64_peer client_addr_nat64;    
.......  
//クライアントのファイルディスクリプタを取得します。このうちlistenfdはサーバーのリスニングファイルディスクリプタです。  
//関数を呼び出して、対応するNAT64シーンのリアルなユーザーソースIPを取得します。   
char from[40];    
int len = sizeof(struct toa_nat64_peer);  
int ret;  
ret = getsockopt(client_fd, IPPROTO_IP, TOA_SO_GET_LOOKUP, &client_addr_nat64, &len);  
if (ret == 0) {  
	inet_ntop(AF_INET6, &(client_addr_nat64.saddr), from, sizeof(from));    
	//ソースIPとソースPortの情報を取得します。   
	printf("real client v6 [%s]:%d\n", from, ntohs(client_addr_nat64.sport));   
} else if (ret != 0) {  
	struct sockaddr v4addr;  
	len = sizeof(struct sockaddr);  
	//ソースIPとソースPortの情報を取得します。この関数が取得するソースアドレスについては以下に注意してください。  
	//ハイブリッドクラウドのデプロイシーンのSNAT IPのリンクを経たものはリアルソースアドレスです。  
	//ハイブリッドクラウドのデプロイシーンのSNAT IPを経ておらず、NAT64のリンクも経ていないものはクライアントアドレスであり、これもリアルソースアドレスです。  
	//このため、この関数のセマンティクスはリアルなクライアントアドレス、ポートを取得するためのものとなります。  
	if (get_peer_name(client_fd, &v4addr, &len) == 0) {  
		inet_ntop(AF_INET, &(((struct sockaddr_in *)&v4addr)->sin_addr), from, sizeof(from));  
		printf("real client v4 [%s]:%d\n", from, ntohs(((struct sockaddr_in *)&v4addr)->sin_port));   
	}  
}  
```
:::
</dx-accordion>


## [（オプション）TOAモジュールのステータス監視](id:monitor-toa)
TOAカーネルモジュールはその実行の安定性を保障するための監視機能も備えています。 toa.koをカーネルモジュールに挿入後、コンテナのあるホスト上で、次の2つの方法によりTOAモジュールの動作状態を監視することができます。
<dx-accordion>
::: 方法1：TOAに保存されている接続のIPv6アドレスを確認する
次のコマンドを実行し、TOAに保存されている接続のIPv6アドレスを確認します。
- このコマンドはパフォーマンスを低下させる可能性があるため、このコマンドを頻繁に呼び出して確認することは避けてください。

```
cat /proc/net/toa_table
```
:::
::: 方法2：TOAに関連するカウントステータスを確認する
次のコマンドを実行し、TOAに関連するカウントステータスを確認します。
```
cat /proc/net/toa_stats
```
![](https://qcloudimg.tencent-cloud.cn/raw/0dcbd6a263316481f50d99c2e4fbab7a.png)
このうちの主な監視指標と、その意味は次のとおりです。
<table>
<thead>
<tr>
<th>指標名</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td>syn_recv_sock_toa</td>
<td>受信したTOA情報を含む接続の数です。</td>
</tr>
<tr>
<td>syn_recv_sock_no_toa</td>
<td>受信したTOA情報を含まない接続の数です。</td>
</tr>
<tr>
<td>getname_toa_ok</td>
<td>getsockoptを呼び出してソースIPの取得に成功するとこのカウントが増加するほか、accept関数を呼び出してクライアントリクエストを受信した場合もカウントが増加します。</td>
</tr>
<tr>
<td>getname_toa_mismatch</td>
<td>getsockoptを呼び出してソースIPを取得した際、タイプがマッチしないとこのカウントが増加します。例えば、あるクライアント接続内に含まれるものがIPv6アドレスではなくIPv4ソースIPであった場合、このカウントが増加します。</td>
</tr>
<tr>
<td>getname_toa_empty</td>
<td>TOAを含まないクライアントファイルディスクリプタがgetsockopt関数を呼び出した場合に、このカウントが増加します。</td>
</tr>
<tr>
<td>ip6_address_alloc</td>
<td>TOAカーネルモジュールがTCPデータパケットに保存されたソースIP、ソースPortを取得した際、情報を保存するためのスペースを申請します。</td>
</tr>
<tr>
<td>ip6_address_free</td>
<td>接続がリリースされた際、TOAカーネルモジュールはそれまでソースIP、ソースPortの保存に使用していたメモリをリリースします。すべての接続が切断された状態で、全CPUのこのカウント数の合計はip6_address_allocのカウントと同じでなければなりません。</td>
</tr>
</tbody>
</table>

:::
</dx-accordion>


## FAQ
<dx-accordion>
::: NAT64 CLBシーンでTOAモジュールの挿入後にサーバープログラムを変更しなければならないのはなぜですか。
これはIPのタイプが変わったことによるものです。ハイブリッドクラウドのデプロイシーンでIPv4のFullnat変換が行われた場合、このシーンではクライアントのリアルソースIPは依然としてIPv4のIPから変換された別のIPv4のIPであるため、IPのタイプに変化はありません。しかし、NAT64 CLBのシーンでは、クライアントのリアルソースIPはIPv6からIPv4に変換されたものであり、IPのタイプが変化しています。このためこれがIPv6のIPであるとサーバーに理解させるためには、IPv6アドレスの意味を理解できるようにサーバープログラムを変更する必要があります。
:::
::: 使用中のシステムがLinuxディストリビューションとTencent TLinuxのカーネルのどちらをベースにしたものかを確認するにはどうすればよいですか。
- 次のコマンドを実行してカーネルバージョンを確認できます。実行結果のバージョンに`tlinux`が含まれればTLinuxシステム、そうでなければLinuxディストリビューションです。
```
uname -a
```
![](https://qcloudimg.tencent-cloud.cn/raw/3f266a4c245030173564cff0d3c77f73.png)

- もしくは次のコマンドを実行し、実行結果に`tlinux`または`tl2`が含まれていれば、TLinuxシステムです。
```
rpm -qa | grep kernel
```
<img src="https://qcloudimg.tencent-cloud.cn/raw/4559818bd61436d7a752bcd9caf1b53d.png" width="70%">
:::
::: ソースアドレスを取得できない場合、最初のトラブルシューティングはどのように行えばよいですか。
1. 次のコマンドを実行し、TOAモジュールがロードされているかどうかを確認します。
```
lsmod | grep toa
```
<img src="https://qcloudimg.tencent-cloud.cn/raw/5b92aa9de0db3e43e91316c4363886f1.png" width="70%">
2. サーバープログラムがインターフェースを正しく呼び出してソースアドレスを取得しているかどうかを確認します。上記の[バックエンドサービスの適用](#adapt-rs)の内容をご参照ください。
3. サーバーでパケットをキャプチャしてトラブルシューティングを行い、リアルソースアドレスを含むTCPパケットが到着しているかどうかを確認します。
 - tcp optionの中に`unknown-200`が表示されている場合は、SNATを経たリアルソースIPがTCP optionに挿入済みであることを意味しています。
 - `unknown-253`が表示されている場合は、NAT64シーンでリアルなIPv6のソースIPが挿入済みであることを意味しています。
![](https://qcloudimg.tencent-cloud.cn/raw/e8fed1ab42370a97889c7dcdce660b72.png)
4. 上記の手順での操作中に、TOAアドレスを含むパケットがサーバーに到達していることが確認できれば、toa.koをDEBUGバージョンにコンパイルし、カーネルログによってさらに特定を進めることができます。ダウンロードしたTOAソースコードディレクトリで、MakefileにDEBUGコンパイルオプションを追加します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/e89cf9fd3d96a760485fb04c966ef6b0.png"width="60%">
5. 次のコマンドを実行して再コンパイルします。
```
make clean
make
```
6. 次のコマンドを実行して既存のkoをアンインストールし、コンパイルした最新のkoを再度挿入します。
```
rmmod toa 
insmod ./toa.ko
```
7. 次のコマンドを実行してカーネルログを観察します。
```
dmesg -Tw
```
次の内容が表示された場合、TOAモジュールは正常に動作しています。サーバープログラムがインターフェースを呼び出してリアルソースIPを取得していないか、あるいは間違ったインターフェースを使用していないかのトラブルシューティングをさらに行ってください。
![](https://qcloudimg.tencent-cloud.cn/raw/9a958fc2b0ae9d185cd228c6668c7162.png)
8. 上記の手順をすべて行っても具体的な原因が判明しない場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してください。
:::
</dx-accordion>
