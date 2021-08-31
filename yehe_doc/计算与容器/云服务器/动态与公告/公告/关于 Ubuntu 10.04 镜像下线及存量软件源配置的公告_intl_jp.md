UbuntuはUbuntu 10.04 LTSのメンテナンスを正式に停止したため、そのため、Tencent Cloud もUbuntu10.04 バージョンのパブリックイメージの提供を停止しています。

 Ubuntu10.04 LTSのディレクトリツリーは、最新の公式ソースウェアハウスから削除されました。Tencent Cloud のソフトウェアリポジトリは公式サイトと一致するために、公式ソースディレクトリツリーでUbuntu 10.04 LTS のサポートを提供しなくなりました。ユーザーに上位バージョンのイメージを置き換えることを推奨します。 

既存のユーザーが Ubuntu 10.04 ソフトウェアソースを引き続き使用したい場合、次の2つの方法を提供します：

## 方法一：構成ファイルを手動で更新する
ユーザーエクスペリエンスを向上させるために、Tencent Cloud ソフトウェアリポジトリは Ubuntu 10.04 LTSの公式アーカイブソース`http://old-releases.ubuntu.com/ubuntu/`をユーザーに提供します。ユーザーは構成ファイルを手動で変更することにより、当該のリポジトリを使用できます：

apt のソース構成ファイルを開き` vi /etc/apt/sources.list`、以下のコードを変更します：

```
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-updates main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-security main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-backports main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-updates main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-security main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-backports main restricted universe multiverse
```

## 方法二：自動化スクリプトを実行する
Tencent Cloudが提供するスクリプト [old-archive.run](http://ubuntu10-10016717.cos.myqcloud.com/old-archive.run) を使用して設定するには、当該のファイルを Ubuntu 10.04 Cloud Virtual Machine にダウンロードして、以下のコマンドを実行します：

```
chmod +x old-archive.run
./old-archive.run
```
