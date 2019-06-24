JDKは、Javaソフトウェア開発ツールキットです。本書は、JDK 1.7と1.8のバージョンを例にし、ぞれぞれWindowsとLinuxシステムのJDKのインストールと環境構成を説明します。

## Windows
### 1.JDKのダウンロード
[Oracle公式サイト](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)に入り、適切なJDKバージョンをダウンロードし、インストールの準備を行います。
### 2. インストール
案内に従ってインストールします。インストール過程においてインストール先ディレクトリ（デフォルトでCドライブにインストールする）をカスタマイズ設定できます。例えば、選択したインストール先ディレクトリ：
`D:\Program Files\Java\jdk1.8.0_31`
`D:\Program Files\Java\jre1.8.0_31`
![ローカル同期ツール1](//mc.qcloudimg.com/static/img/0652f9759c4f7fa7e61aa406ca1ad822/image.png)
### 3. 構成
インストール完了後、【コンピュータ】を右クリックし、【属性】>【システム詳細設定】>【環境変数】>【システム変数】>【新規作成】をクリックし、ソフトウェア構成を行います。
変数名(N)：**JAVA_HOME**   
変数値(V)：`D:\Program Files\Java\jdk1.8.0_31`（実際のインストールパスにより構成を行ってください）。
![ローカル同期ツール2](//mc.qcloudimg.com/static/img/f02f0ec6b87576f32fbade9cd8d55c1e/image.png)
変数名(N)：**CLASSPATH**   
変数値(V)：`.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;`（注意：変数値の先頭に`.`が含まれます）。
![ローカル同期ツール3](//mc.qcloudimg.com/static/img/d2c87f5ce4c2927f5e9ca9d20e4478d6/image.png)
変数名(N)：**Path**
変数値(V)：`%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;`
![ローカル同期ツール4](//mc.qcloudimg.com/static/img/5ee8cc105d52f9052cc49251ce88ed9a/image.png)
### 4. テスト
構成が成功であるかどうかをテストする：【開始】（またはショートカットキー：Win+R）>【実行】（`cmd`を入力する）>【OK】（またはEnterキーを押す）をクリックし、コマンド`javac`を入力してEnterキーを押します。下図の情報が表示されると、正常に環境変数を構成したことを示します。
![ローカル同期ツール5](//mc.qcloudimg.com/static/img/83f8417d6f540c20182267acba29f2ad/image.png)

## Linux
yumまたはapt-getコマンドを用いてopenjdkをインストールするとき、クラスライブラリが不完全になることがあるので、ユーザーがインストール後に関連ツールを実行するときにエラーが発生することがあります。したがって、手動で解凍しJDKをインストールする方法がおすすめします。具体的な手順は以下のとおりです。

### 1.JDKのダウンロード
[Oracle公式サイト](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)に入り、適切なJDKバージョンをダウンロードし、インストールの準備を行います。
>!Linuxバージョンをダウンロードする必要があります。jdk-8u151-linux-x64.tar.gを例と挙げると、ダウンロードしたファイルはこのバージョンでなくても構いません。サフィックス（.tar.gz）が一致するだけでよい。

### 2. ディレクトリ作成
`/usr/`ディレクトリで`java`ディレクトリを作成し、
```shell
mkdir /usr/java
cd /usr/java
```
ダウンロードしたファイルjdk-8u151-linux-x64.tar.gzを/usr/java/ディレクトリにコピーします。

### 3. JDK解凍
```shell
tar -zxvf jdk-8u151-linux-x64.tar.gz
```

### 4. 環境変数の設定
/etc/profileファイルを編集し、profileファイルに下記の内容を追加し保存します。
```shell
set java environment
JAVA_HOME=/usr/java/jdk1.8.0_151        
JRE_HOME=/usr/java/jdk1.8.0_151/jre     
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH
```
>!そのうち、JAVA_HOME、JRE_HOMEは、実際のインストールパスとJDK バージョンに応じて構成してください。

変更を有効にします。
```shell
source /etc/profile
```

### 5. テスト
```sh
java -version
```
javaバージョン情報が表示されると、正常にJDKをインストールしたことを表示します。
```shell
java version "1.8.0_151"
Java(TM) SE Runtime Environment (build 1.8.0_151-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)
```
