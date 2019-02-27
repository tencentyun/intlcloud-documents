[//]: # (chinagitpath:XXXXX)

## 非Webサイトサービス転送規則の使用
Anti-DDoS Advancedは非Webサイトサービス転送規則を使う時、オリジンサーバーはtoaモジュールを用いてクライアントの実際のIPを取得する必要があります。

### 基本原理
Anti-DDoS Advancedは、パブリックプロキシモードを使用しますので、このデータパケットの送信元アドレスと送信先アドレスが変更されます。オリジンサーバーで表示されるデータパケットの送信元アドレスはAnti-DDoS Advancedインスタンスのプル型IPであり、クライアントの実際のIPではありません。クライアントIPをサーバーに転送するには、転送時、Anti-DDoS Advancedは以下のように、クライアントのIPとPortをカスタマイズしたtcp optionフィールドに記録します。
```
#define TCPOPT_ADDR  200
#define TCPOLEN_ADDR 8      /* |opcode|size|ip+port| = 1 + 1 + 6 */

/*
 * insert client ip in tcp option, now only support IPV4,
 * must be 4 bytes alignment.
 */
struct ip_vs_tcpo_addr {
    __u8 opcode;
    __u8 opsize;
    __u16 port;
    __u32 addr;
};
```

### 対応OS
•	CentOS 6.x
•	CentOS 7.x
>!
- Windowsシステムは、toaモジュールを用いてクライアントの実際のIPを取得することをサポートしません。
- Linuxなどの他のOSについては、[Tencent Cloud技術サポート](https://cloud.tencent.com/about/connect)までお問い合わせください。

### 注意事項
- まずテスト環境でインストールとテストを行い、機能が利用可能で運転が安定であることを確認してから正式な環境に配置することをお勧めします。
- カーネルをアップグレードしたい場合、アップグレード失敗などを防ぐために、アップグレードする前に元のカーネルを保存することをお勧めします。
-  toaはIPv4のみサポートします。環境がデフォルトでIPv6を取得すると、クライアントIPを正しく取得できません。

### クライアントの実際のIPの取得
1. rootユーザーとして次のコマンドを実行し、コンパイル環境をインストールします。
`yum install gcc kernel-headers kernel-devel -y `
2. インストールファイルを[ダウンロード](https://daaa-1254383475.cos.ap-shanghai.myqcloud.com/TOA_CentOS_v1.zip)して、解凍します。
 ```
wget  https://daaa-1254383475.cos.ap-shanghai.myqcloud.com/TOA_CentOS_v1.zip
unzip TOA_CentOS_v1.zip
 ```
 <span id="step3"></span>
3. カーネルのバージョンを表示するには、`uname -r`コマンドを実行します。
 例：
```
[root@VM_0_2_centos toa]# uname -r
3.10.0-514.26.2.el7.x86_64
```
4. [ステップ3](#step3)の照合結果から、Makefile構成ファイルのパスパラメータKERNEL_DIRを変更します。
例：
```
[root@VM_0_2_centos toa]# vim Makefile 
obj-m := toa.o
KERNEL_DIR := /usr/src/kernels/3.10.0-514.26.2.el7.x86_64/
PWD := $(shell pwd)
#EXTRA_CFLAGS+=-D__GENKSYMS__
all:
        make -C $(KERNEL_DIR) M=$(PWD) modules
clean:    
        rm *.o *.ko *.mod.c  Module.symvers modules.order
```
5. コンパイルするには、`make`コマンドを実行します。
6. モジュールを移動し読み込みを実行します。
```
mv toa.ko /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
insmod /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
```
 - 読み込み完了後、実際のクライアントソースIPを取得できます。
 - クライアントソースIPの取得ができない場合、`lsmod | grep toa`コマンドを実行して、toaモジュールの読み込み状況をチェックしてください。

### toaモジュールのアンマウント
rootユーザーとして、次のコマンドを実行し、toaモジュールをアンマウントします。
```
rmmod /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
```

## Webサイトサービス転送規則の使用
Anti-DDoS Advancedは、Webサイトサービス転送規則を使う時、HTTPヘッダーのX-Forwarded-Forフィールドを用いてクライアントの実際のIPを取得できます。
X-Forwarded-For：HTTPヘッダー拡張フィールドです。サーバーはプロキシなどによってリンクされるクライアントの実際のIPを取得することができます。
フォーマット：
`X-Forwarded-For：Client、proxy1、proxy2、proxy3……  `
防御IPは、ユーザーのアクセスリクエストをバックエンドのサーバーに転送する時、リクエストユーザーの実際のIPをX-Forwareded-Forフィールドの先頭に記録します。したがって、オリジンサーバーのアプリケーションはHTTPヘッダーのX-Forwarded-Forフィールドの内容を取得すればよい。
詳細については、[7層転送による実際のアクセス元IPの取得方法](https://cloud.tencent.com/document/product/214/3728)を参照してください。

