JDKはJavaソフトウェア開発ツールキットです。ここでは、JDK 1.8バージョンを例として、WindowsとLinuxシステムにおけるJDKのインストールと環境設定の手順についてそれぞれご紹介します。

## Windows

#### 1.JDKのダウンロード

[Oracle公式サイト](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)に進み、適切なJDKのバージョンをダウンロードします。

#### 2. インストール

プロンプトに従って、ステップバイステップでインストールします。インストール中にインストールディレクトリをカスタマイズすることができます（デフォルトではCドライブにインストールします）。例えば、選択するインストールディレクトリは、`D:\Program Files\Java\jdk1.8.0_31`と`D:\Program Files\Java\jre1.8.0_31`です。


#### 3. 設定

インストールが完了したら、**コンピュータ>プロパティ>高度なシステム設定>環境変数>システム変数>新規作成**を右クリックして、ソフトウェアをそれぞれ設定します。
変数名(N)：**JAVA_HOME**   
変数値(V)：`D:\Program Files\Java\jdk1.8.0_31`（実際のインストールパスに従って設定してください）。

変数名(N)：**CLASSPATH**   
変数値(V)：`.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;`（変数の値は`.`から始まりますので、ご注意ください）。

変数名(N)：**Path**
変数値(V)：`%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;`


#### 4. テスト
設定が成功したかどうかをテストするには、**スタート（またはショートカットキー：Win+R）>実行（cmdを入力）>OK（またはEnterキーを押す）**をクリックし、コマンドjavacを入力してEnterキーを押します。下図のような情報が表示されれば、環境変数の設定は成功です。


## Linux
yumまたはapt-getコマンドを使用してopenjdkをインストールすると、クラスライブラリが不完全になり、ユーザーがインストール後に関連ツールを実行する際、エラーが報告される場合がありますので、ここでは手動で解凍してJDKをインストールする方法をお勧めします。具体的な手順は、次のとおりです。

#### 1.JDKのダウンロード
[Oracle公式サイト](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)に進み、適切なJDKのバージョンをダウンロードし、インストールの準備を行います。
>!以下は、例としてjdk-8u151-linux-x64.tar.gzを取り上げています。他のバージョンをダウンロードする場合は、ファイルの拡張子が.tar.gzであることに注意してください。

#### 2. ディレクトリの作成 

以下のコマンドを実行し、/usr/ディレクトリにjavaディレクトリを作成します。
```shell
mkdir /usr/java
cd /usr/java 
```
ダウンロードしたファイルjdk-8u151-linux-x64.tar.gzを/usr/java/ディレクトリにコピーします。 

#### 3.JDKの解凍

次のコマンドを実行して、ファイルを解凍します。
```shell
tar -zxvf jdk-8u151-linux-x64.tar.gz 
```

#### 4. 環境変数の設定

/etc/profileファイルを編集し、profileファイルに次の内容を追加して保存します。
```shell
# set java environment
JAVA_HOME=/usr/java/jdk1.8.0_151        
JRE_HOME=/usr/java/jdk1.8.0_151/jre     
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH 
```
>!ここでJAVA_HOME、JRE_HOMEは、実際のインストールパスとJDKのバージョンに応じて設定してください。

変更を有効にするには、以下を実行します。
```shell
source /etc/profile 
```

#### 5. テスト
次のコマンドを実行して、テストを行います。
```sh
java -version
```

Javaのバージョン情報が表示されれば、JDKのインストールは成功です。
```shell
java version "1.8.0_151"
Java(TM) SE Runtime Environment (build 1.8.0_151-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)
```

