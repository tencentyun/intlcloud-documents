Tencent Cloud上のLinuxのバージョンに応じて、対応するTOAパッケージをダウンロードして解凍します。
-   [CentOS 7.2 64](http://toamodule-1253438722.file.myqcloud.com/CentOS%207.2%2064.zip)
-  [CentOS 7.3 64](http://toamodule-1253438722.file.myqcloud.com/CentOS%207.3%2064.zip)
-  [CentOS 7.4 64](http://toamodule-1253438722.file.myqcloud.com/CentOS%207.4%2064.zip)
- 	[Debian 8.2 64](http://toamodule-1253438722.file.myqcloud.com/Debian%208.2%2064.zip)
-  [Debian 9.0 64](http://toamodule-1253438722.file.myqcloud.com/Debian%209.0%2064.zip) 
-   [SUSE Linux Enterprise Server 11 SP3 64](http://toamodule-1253438722.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2011%20SP3%2064.zip)
-  [SUSE Linux Enterprise Server 12 64](http://toamodule-1253438722.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2012%2064.zip)
-  [Ubuntu Server 14.04.1 LTS 64](http://toamodule-1253438722.file.myqcloud.com/Ubuntu%20Server%2014.04.1%20LTS%2064.zip)
-  [Ubuntu Server 16.04.1 LTS 64](http://toamodule-1253438722.file.myqcloud.com/Ubuntu%20Server%2016.04.1%20LTS%2064.zip) 


1. 解凍が完了したら、cdコマンドを実行して新しく解凍されたフォルダに入り、モジュールをロードするコマンドを実行します。
```
insmod toa.ko
``` 
2. 以下のコマンドを実行して、ロードが成功したかどうかを確認します。
```
lsmod | grep toa
```
3. ロード成功後、最後に起動スクリプトでtoa.koファイルをロードして完了です（マシンを再起動すると、koファイルを再ロードする必要があります）。


上記のダウンロードファイルにご使用のオペレーティングシステムのバージョンに対応するインストールパッケージが含まれていない場合は、Linuxのユニバーサルバージョンのソースパッケージをダウンロードして、コンパイルして入手します。このバージョンはCentos6.9およびCentos7、Ubuntu14.04などの大部のLinuxリリースバージョンをサポートしています。

1. ソースパッケージを入手します
```
wget http://toamodule-1253438722.file.myqcloud.com/tencenttoa.zip
```

2. ファイルをコンパイルします
```
yum install gcc
yum install kernel-headers
yum install kernel-devel
```

3. toa.koファイルをロードします
```
tar -zxvf linux_toa.tar.gz
cd toa
make
mv toa.ko /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
insmod /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
```
