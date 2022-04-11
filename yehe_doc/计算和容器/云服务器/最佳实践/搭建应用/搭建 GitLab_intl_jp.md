## 操作シナリオ
GitLabは、Rubyで書かれているオープンソースのバージョン管理システムであり、Gitをコード管理ツールとしてセルフホスティングのGitプロジェクトリポジトリを実現し、Webインターフェースを介してパブリックおよびプライベートプロジェクトにアクセスすることができます。このドキュメントでは、Tencent Cloud CVMでGitLabをインストールおよび使用する方法について説明します。



## ソフトウェア
- GitLab：コミュニティ版 14.6.2 
- ここで使用するCVM設定は次のとおりです。
	- vCPU：2コア
	- メモリ：4GB
	- Linuxオペレーティングシステム：CentOS8.2およびCentOS7.9 を例として取り上げます

##  前提条件
- Linux CVMを購入済みであること。
- Linuxインスタンスのセキュリティグループルールはすでに設定されています。ポート80を開きます。詳細については、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)をご参照ください。

## 操作手順
### GitLabのインストール
1.インスタンスにログインします。詳細については、[標準方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。
2. 実際に使用するオペレーティングシステムに応じて、次のコマンドを実行し、依存パッケージをインストールします。
<dx-tabs>
::: CentOS 8.2
```
yum install -y curl policycoreutils-python-utils openssh-server
```
:::
::: CentOS 7.9
```
yum install -y curl policycoreutils-python openssh-server
```
:::
</dx-tabs>
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
インスタンスのパブリックIPアドレスを取得する方法の詳細については、[パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940)をご参照ください。
12.ローカルブラウザで、取得したパブリックIPアドレスにアクセスします。以下のようなページが表示されると、GitLabのインストールに成功したことを意味します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/abaf3b700a58ed5b4a1e13e9d82eaf7e.png"/>


### 管理者アカウントのパスワードを設定
1. 管理者アカウントのデフォルトのパスワードを取得します。
 インスタンスにログインし、次のコマンドを実行し、管理者`root`アカウントのログインパスワードを取得します。
```
cat /etc/gitlab/initial_root_password
```
下図に示すようにパスワードを取得します。
![](https://qcloudimg.tencent-cloud.cn/raw/01bfa701452cc470fbdbfb82ab294237.png)
2. GitLabにログインします。
ローカルブラウザでCVMのパブリックIPにアクセスし、GitLabログインインターフェースに移動します。`root` アカウントおよび取得済みのログインパスワードを使用してログインを実行します。
3. 管理者アカウントのパスワードを変更します。
デフォルトのパスワードが保存されるファイルは初回設定を実行してから24時間後に自動的に削除されますので、できる限り早急に`root`アカウントのログインパスワードを変更してください。
 1. ページ右上コーナーのユーザープロフィール画像を選択し、ポップアップメニューで**Perferences**を選択します。
 2. 「User Settings」 ページで左側ナビゲーションバーの **Password**を選択します。
 3. 下図に示すように、ページに現在のパスワード、新たなパスワードおよび新たなパスワードの確認を入力した後、**Save Password**をクリックします。
 ![](https://qcloudimg.tencent-cloud.cn/raw/25adb5b68d48873392684d1a1030bbe1.png)

### プロジェクトの新規作成
1. `root`アカウントおよび設定済みのログインパスワードを使用してログインを実行します。
2. 画面の案内に従ってプライベートプロジェクトを新規作成します。本節では、`test`を例として説明します。以下の通りです。
![](https://qcloudimg.tencent-cloud.cn/raw/a6d85a83b86a44c1f39dbd363a3311ce.png)
3. プロジェクトが正常に作成されたら、ページ上方のプロンプトの**Add SSH Key**をクリックします。
4. 「SSH Keys」ページに入り、次の手順でSSH Keyを追加します：
 1. [キーの取得](#getKey)ステップで、PCのキー情報を取得し、「Key」に貼り付けます。
 2. 「Title」でこのキーの名前をカスタマイズします。
 3. 下図に示すように、**Add key**をクリックすれば、キーを追加できます。
![](https://qcloudimg.tencent-cloud.cn/raw/504b7a69215471516f7ace36bb5606af.png)
次のように表示されるとキーの追加に成功したことを意味します。
![](https://qcloudimg.tencent-cloud.cn/raw/2d46dcb48b51243ce4fc91b319b3ede3.png)
5. [](id:Step5)下図に示すように、プロジェクトのトップページに戻り、**clone**をクリックして、プロジェクトアドレスを記録します。
![](https://qcloudimg.tencent-cloud.cn/raw/9edb130321b5df140cfc863c73f6837d.png)


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
git push
```
testプロジェクト画面に戻ると、ファイルのアップロードに成功したことを確認できます。以下の通りです。
![](https://qcloudimg.tencent-cloud.cn/raw/0440c9a53b3a93d056119fd47f39638e.png)

## 関連する操作
### キーの取得[](id:getKey)
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
