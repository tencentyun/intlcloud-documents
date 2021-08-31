## 概要
GitLabは、Rubyで書かれているオープンソースのバージョン管理システムであり、Gitをコード管理ツールとしてセルフホスティングのGitプロジェクトリポジトリを実現し、Webインターフェースを介してパブリックおよびプライベートプロジェクトにアクセスすることができます。このドキュメントでは、Tencent Cloud CVMでGitLabをインストールおよび使用する方法について説明します。



## ソフトウェア
このドキュメントに使用するCVMインスタンスは次のように構成する必要があります。
- vCPU：2コア
- メモリ：4GB
- Linux OS ：本節では、CentOS 7.7を例として説明します。

## 前提条件
- GitLabをインストールするにはLinux CVMが必要です。Linux CVMをまだ購入していない場合は、[Linux CVM設定のカスタマイズ](https://intl.cloud.tencent.com/document/product/213/10517)をご参照ください。
- Linuxインスタンスのセキュリティグループルールはすでに設定されています。ポート80を開きます。詳細については、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)をご参照ください。

## 操作手順
### GitLabのインストール
1. [標準方法を使用してLinuxインスタンスにログインします（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。実際の操作方法に応じて、他のログイン方法を選択することもできます。　　
 - [リモートログインソフトウェアを使用してLinuxインスタンスにログインします](https://intl.cloud.tencent.com/document/product/213/32502)
 - [SSHキーを使用してLinuxインスタンスにログインします](https://intl.cloud.tencent.com/document/product/213/32501)
2. 以下のコマンドを実行して、依存関係をインストールします。
```
yum install -y curl policycoreutils-python openssh-server
```
3.次のコマンドを順番に実行して、SSHサービスの自動起動を有効にし、SSHサービスを開始します。
```
systemctl enable sshd
```
```
systemctl start sshd
```
4. 次のコマンドを実行して、Postfixをインストールします。
```
yum install -y postfix
```
5. 次のコマンドを実行して、Postfixサービスの自動起動を設定します。
```
systemctl enable postfix
```
6. 次のコマンドを実行して、Postfixの構成ファイルmain.cfを開きます。
```
vim /etc/postfix/main.cf
```
7. **i**を押して編集モードに入り、`inet_interfaces = all`前の`#`を削除し、`inet_interfaces = localhost`の前に`#`を追加します。変更した後は以下の通りです。 
![](https://main.qcloudimg.com/raw/57fa73bdcd05343b5dcee24e47b5f09a.png)
8. **Esc**キーを押して、**:wq**を入力し、変更を保存してからファイルを終了します。
9. 次のコマンドを実行して、Postfixを起動します。
```
systemctl start postfix
```
10. 次のコマンドを実行して、GitLabのソフトウェアリポジトリをインストールします。
```
 curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
```
11. 次のコマンドを実行して、GitLabをインストールします。
```
sudo EXTERNAL_URL="インスタンスのパブリックIPアドレス" yum install -y gitlab-ce
```
インスタンスのパブリックIPを取得する方法の詳細については、[パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940)をご参照ください。
12.ローカルブラウザで、取得したパブリックIPアドレスにアクセスします。以下のようなページが表示されると、GitLabのインストールに成功したことを意味します。
>このページでGitLabアカウントのパスワードを設定してください。
>
![](https://main.qcloudimg.com/raw/791f5250c2bca059369a141c047f2c21.png)


### プロジェクトの新規作成
1. ローカルブラウザで、CVMのパブリックIPアドレスにアクセスして、GitLabのログイン画面に入ります。`root`アカウントおよび設定したログインパスワードを使用してログインします。以下の通りです。
![](https://main.qcloudimg.com/raw/c0639741b40c1fa33d41434c0222c13b.png)
2. 画面の案内に従ってプライベートプロジェクトを新規作成します。本節では、`test`を例として説明します。以下の通りです。
![](https://main.qcloudimg.com/raw/912805dfffcba06558d3adbe8b33b4bc.png)
3. プロジェクト作成に成功した後、ページの上部にある【Add SSH Key】をクリックします。
4. 「SSH Keys」ページに入り、次の手順でSSH Keyを追加します：
 1. [キーの取得](#getKey)ステップで、PCのキー情報を取得し、「Key」に貼り付けます。
 2. 「Title」でこのキーの名前をカスタマイズします。
 3. 【Add key】をクリックするとキーを追加できます。以下の通りです。
![](https://main.qcloudimg.com/raw/c8d21821f0d6919a650cf36d43666f06.png)
次のように表示されるとキーの追加に成功したことを意味します。
![](https://main.qcloudimg.com/raw/6908a9710bd01d57c01892b31247bc02.png)
5. <span id="Step5"></span>プロジェクトのホームページに戻り、【clone】をクリックするとプロジェクトアドレスを記録します。以下の通りです。
![](https://main.qcloudimg.com/raw/972726ec33e5a92c0a778a700ae9b4b0.png)


### プロジェクトの複製
1. 管理対象のPCで次のコマンドを実行して、Gitリポジトリを使用する担当者の氏名を設定します。
```
git config --global user.name "username" 
```
2. 次のコマンドを実行して、Gitリポジトリを使用する担当者のメールボックスを設定します。
```
git config --global user.email "xxx@example.com" 
```
3. 次のコマンドを実行して、プロジェクトを複製します。ここで、「プロジェクトアドレス」を[ステップ5](#Step5)で取得したプロジェクトアドレスに置き換えてください。
```
git clone 「プロジェクトアドレス」
```
プロジェクトの複製が成功すると、ローカルに同名ディレクトリを生成し、その中にプロジェクトのすべてのファイルが格納されます。

### ファイルのアップロード
1. 次のコマンドを実行して、プロジェクトディレクトリに入ります。
```
cd test/
```
2. 次のコマンドを実行して、GitLabにアップロードするターゲットファイルを作成します。本節では、test.shを例として説明します。
```
echo "test" > test.sh
```
3. 次のコマンドを実行して、test.shファイルをインデックスに追加します。
```
git add test.sh
```
4. 次のコマンドを実行して、test.shをローカルリポジトリに提出します。
```
git commit -m "test.sh"
```
5. 次のコマンドを実行して、test.shをGitLabサーバーに同期します。
```
git push -u origin master
```
testプロジェクト画面に戻ると、ファイルのアップロードに成功したことを確認できます。以下の通りです。
![](https://main.qcloudimg.com/raw/e208c7a0f7399e4a42a1bb3d17a89c1c.png)

## 関連操作
### キーの取得<span id="getKey"></span>
1. プロジェクト管理に組み入れる必要があるPCで、次のコマンドを実行して、Gitをインストールします。
```
yum install -y git
```
2. 次のコマンドを実行して、キーファイル.ssh/id_rsaを生成します。キーファイルの生成プロセス中に、**Enter**キーを押してデフォルト設定を保持します。
```
ssh-keygen
```
3. 次のコマンドを実行して、キー情報を表示および記録します。
```
cat .ssh/id_rsa.pub
```
