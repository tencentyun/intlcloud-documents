CVMでのソフトウェアインストールの効率を向上させると同時に、ソフトウェアのダウンロードとインストールのコストを削減するために、Tencent CloudはApt-getダウンロードソースを提供します。OSはUbuntu12.04のCVMであり、ユーザーがApt-getを利用してソフトウェアを迅速にインストールできます。

apt-getダウンロードソースに対して、ソフトウェアソースを追加する必要はありません、ソフトウェアパッケージを直接インストールできます。ソフトウェアインストールを加速するために、システムは予めプライベートネットワークにUbuntuのmirrorを構成されており、このmirrorは公式のx86_64の完全なイメージであり、公式サイトのソースと一致しています。 

## 1. インストール手順
1) OSがUbuntu12.04のCVMにログインします。

2) 下記のコマンドでソフトウェアをインストールします。

```
sudo apt-get install
```
例は以下の通り：

```
sudo apt-get install nginx php5-cli php5-cgi php5-fpm php5-mcrypt php5-mysql mysql-client-core-5.5 mysql-server-core-5.5
```

結果：

![](http://mccdn.qcloud.com/img56af4dfeb631a.png)

3) 「Y」を入力して確認した後、ソフトウェアインストールを開始し、インストールが完了するまで続きます。

## 2. インストールされたソフトウェアの情報を確認する
ソフトウェアがインストールされた後、下記のコマンドでソフトウェアパッケージのインストールディレクトリ、パッケージ内のすべてのファイルを確認できます。

```
sudo dpkg -L 
```

下記のコマンドでソフトウェアパッケージのバージョン情報を確認できます。

```
sudo dpkg -l 
```

例は以下の通り：

```
sudo dpkg -L nginx 
sudo dpkg -l nginx
```

結果は下記の通り（実際のバージョンはこのバージョンと異なる可能性があり、実際にクエリーしたバージョンを基準にしてください。）
![](http://mccdn.qcloud.com/img56af4f1d9e433.png)
![](http://mccdn.qcloud.com/img56af4f7f57949.png)
