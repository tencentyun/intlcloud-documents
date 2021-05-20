## 1. Linux環境ではrootあるいはuser_00のユーザーがゲームプログラムを起動します
現在GSEでは、Linux環境でデフォルトとしてrootユーザーがゲームプロセスを起動します。ユーザーがrootではないユーザーでゲームプロセスを起動する必要がある場合、以下の設定を実行する必要があります。

1. ゲームアセットのルートディレクトリにgse.yamlファイルを追加すると、ゲームサーバーフリートインスタンス上で解凍され、パスは/local/game/gse.yamlとなります。  
2. gse.yamlファイルの内容に、以下のように、ユーザーグループusers内にユーザーuser_00が新規追加されます（現在他のユーザーおよびユーザーグループの設定はサポートされていません）。
```
User: user_00:users
```
アセット内でgse.yamlファイルが適切に設定されると、GSEはuser_00:usersを使用してゲームプロセスを起動し、/local/gameパスの下にあるすべてのファイルのユーザーおよびユーザーグループをuser_00:usersに設定します。

	例は下図のとおりです：
![](https://main.qcloudimg.com/raw/c39326e6328dac93964f6d3e6da5efad.png)

## 2. Linux環境で、ゲームプロセスの起動前にinstall.shを実行します
ゲームプロセスの起動前、ユーザーはCVMインスタンス上で一連のソフトウェアをインストールまたは一連の環境変数等を設定する必要がある可能性があります。具体的な操作手順は次のとおりです。

1. ユーザーはinstall.shスクリプトを新規作成し、ゲームプロセス起動前の操作をinstall.sh中に記述します。  
2. install.shをゲームアセットのルートディレクトリの下に配置すると、ゲームサーバーフリートインスタンス上で解凍され、パスは/local/game/install.shになります。

## 3. Java言語で開発されたゲームプロセスの起動設定
Linux環境でJavaプログラムを起動するためのコマンドは以下のとおりです。java -jar XXXX.jar。Java言語で開発されたゲームプロセスが適切に起動するためには、以下の設定をする必要があります。

1. install.shスクリプトの記述

		#!/bin/bash

		# JDK 1.8をインストールした環境で、-yはanswer yes for all questionsを意味します。
		yum install java-1.8.0-openjdk.x86_64 -y
		# javaコマンドのシンボリックリンクは/local/gameパスの下になります
		ln -s /usr/bin/java /local/game/java

2. install.shスクリプトをゲームアセットのルートディレクトリの下に配置すると、ゲームサーバーフリートインスタンス上で解凍され、パスは/local/game/install.shになります。
3. ゲームサーバーフリートを作成するときは、起動パスに/local/game/javaと入力し、起動パラメータに-jarユーザー指定のjarパッケージを入力します。
![](https://main.qcloudimg.com/raw/50f224688792b05010a583992013d5b2.png)

4. ゲームプロセスの起動に成功すると、/local/gameパスの内容は以下のようになります。
![](https://main.qcloudimg.com/raw/637aebe468e921d845baeb88fa21688c.png)




